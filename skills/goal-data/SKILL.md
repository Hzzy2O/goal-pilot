---
name: goal-data
description: Data I/O and summary maintenance skill for Goal Pilot. Handles CSV read/write, state.json management, layered summary generation, decay weight calculation, and pins management. Use this skill for all data persistence operations.
---

# Goal Data - Data Layer Skill

## Overview

This skill provides data layer operations for Goal Pilot. It handles:
- CSV file read/write for reviews and summaries
- state.json CRUD operations
- Layered summary generation (daily → weekly → monthly)
- Decay weight calculation for context retrieval
- Pins management for long-term knowledge

## File Locations

All data files are stored in the plugin's `data/` directory:

```
data/
├── state.json              # Configuration and current plan state
├── reviews_daily.csv       # Daily review records
├── reviews_weekly.csv      # Weekly review records
├── reviews_monthly.csv     # Monthly review records
├── summaries_weekly.csv    # Weekly summary layer (L1)
├── summaries_monthly.csv   # Monthly summary layer (L2)
└── pins.csv                # Long-term non-decaying knowledge
```

## CSV Operations

### Reading CSV Files

When reading CSV data:

1. **Check file existence** - If file doesn't exist, return empty dataset
2. **Parse UTF-8 content** - Handle multi-byte characters correctly
3. **Skip header row** - First row is always column headers
4. **Support date filtering** - Accept `start_date` and `end_date` parameters

**Date Range Query Pattern:**
```
To read daily reviews from last 7 days:
1. Calculate date range: [today - 7 days, today]
2. Filter records where date column is within range
3. Return matching records as structured data
```

### Appending CSV Records

When writing new records:

1. **Validate required fields** - Check all mandatory columns have values
2. **Check for duplicates** - For daily reviews, check if date already exists
3. **Update if exists** - For daily reviews, replace existing record for same date
4. **Preserve file integrity** - Write to temp file first, then rename

**Field Validation Rules:**

| File | Required Fields | Validation |
|------|-----------------|------------|
| reviews_daily.csv | date, energy_1_5, mood_1_5 | energy/mood must be 1-5 |
| reviews_weekly.csv | week_start, week_end | dates must be valid |
| reviews_monthly.csv | month | format YYYY-MM |
| pins.csv | type, content | type must be valid enum |

### CSV Schemas

**reviews_daily.csv:**
```
date,done_top3,blocked,plan_deviation_reason,effort_minutes,energy_1_5,mood_1_5,progress_signal,next_day_focus,pins_to_add,notes
```

**plan_deviation_reason values:**
- `scope_too_big`
- `unclear_next_action`
- `low_energy`
- `external_interrupt`
- `procrastination`
- `other`
- `none`

**reviews_weekly.csv:**
```
week_start,week_end,win,loss,main_blocker,metric_delta,plan_adjustment_suggested,notes
```

**reviews_monthly.csv:**
```
month,major_outcome,trend,root_causes,plan_adjustment_suggested,next_month_strategy,notes
```

**trend values:** `improving`, `stable`, `declining`

**summaries_weekly.csv:**
```
week_start,week_end,total_effort_minutes,avg_energy,avg_mood,deviation_reasons_count,blocked_items,summary_text
```

**summaries_monthly.csv:**
```
month,total_effort_minutes,avg_energy,avg_mood,trend_indicators,key_blockers,summary_text
```

**pins.csv:**
```
created_at,type,content,source,active
```

**type values:**
- `constraint` - Physical/time/resource limitations
- `preference` - User work style preferences
- `non_negotiable` - Absolute requirements
- `recurring_pattern` - Observed behavior patterns
- `lesson` - Learned insights

## state.json Operations

### Reading State

```
1. Read data/state.json
2. Validate schema_version
3. Return parsed JSON object
```

### Updating State

When applying updates (patches):

```
1. Read current state
2. Validate patch structure
3. Deep merge patch into state
4. Update last_run.last_calibration timestamp
5. Write atomically (temp file → rename)
```

**Protected Fields (never overwrite without explicit intent):**
- `schema_version`
- `goal.statement` (only during setup)
- `goal.target_date` (only during setup)

### State Schema Reference

```json
{
  "schema_version": "2.1",
  "user": {
    "language": "zh|en|ja",
    "timezone": "Asia/Shanghai"
  },
  "goal": {
    "statement": "string",
    "target_date": "YYYY-MM-DD",
    "north_star_metric": "string"
  },
  "plan": {
    "current_phase": "Q1-Validate|Q2-Scale|Q3-Systematize|Q4-Achieve",
    "milestones": [
      {
        "id": "M1",
        "due": "YYYY-MM-DD",
        "definition_of_done": "string",
        "weight": 0.0-1.0,
        "completed_weight": 0.0-1.0
      }
    ]
  },
  "domains": ["string"],
  "calibration": {
    "decay": {
      "daily_half_life_days": 30,
      "weekly_half_life_days": 120
    },
    "thresholds": {
      "behind_ratio_yellow": 0.15,
      "behind_ratio_red": 0.30
    },
    "task_adjustment": {
      "force_small_steps": false,
      "force_split_outcomes": false,
      "low_friction_mode": false
    },
    "deviation_counters": {
      "unclear_next_action": 0,
      "scope_too_big": 0,
      "low_energy": 0,
      "last_reset_date": "YYYY-MM-DD"
    }
  },
  "last_run": {
    "today": "YYYY-MM-DD",
    "last_review": "YYYY-MM-DD",
    "last_calibration": "YYYY-MM-DD"
  }
}
```

## Summary Generation

### Weekly Summary Generation

**Trigger:** After weekly review is completed

**Process:**
1. Read all daily reviews for the target week (week_start to week_end)
2. Calculate aggregates:
   - `total_effort_minutes` = sum of effort_minutes
   - `avg_energy` = mean of energy_1_5
   - `avg_mood` = mean of mood_1_5
   - `deviation_reasons_count` = JSON object counting each reason type
   - `blocked_items` = pipe-separated list of unique blockers
3. Generate `summary_text` (1-2 sentences describing the week)
4. Append to summaries_weekly.csv

**Summary Text Pattern:**
```
"本周投入{total_effort}分钟，平均精力{avg_energy}/5，完成了{top_accomplishment}。主要阻塞：{main_blocker}。"
```

### Monthly Summary Generation

**Trigger:** After monthly review is completed

**Process:**
1. Read all weekly summaries for the target month
2. Calculate aggregates:
   - `total_effort_minutes` = sum across weeks
   - `avg_energy` = weighted average
   - `avg_mood` = weighted average
   - `trend_indicators` = JSON object with trend analysis
   - `key_blockers` = most frequent blockers
3. Generate `summary_text` (2-3 sentences)
4. Append to summaries_monthly.csv

## Decay Weight Calculation

### Formula

```
weight = exp(-ln(2) * age_days / half_life_days)
```

Where:
- `age_days` = today - record_date
- `half_life_days` = from state.json.calibration.decay

### Default Half-Life Values

| Data Type | Half-Life | Meaning |
|-----------|-----------|---------|
| Daily review | 30 days | Record from 30 days ago has 50% weight |
| Weekly summary | 120 days | 4-month half-life |
| Monthly summary | 365 days | 1-year half-life |
| Pins | ∞ | Never decay, always weight = 1.0 |

### Context Layer Thresholds

| Age | Layer | Content |
|-----|-------|---------|
| 0-7 days | L0 | Full daily review content |
| 8-30 days | L0 partial | Key fields only (blocked, deviation, energy, mood) |
| 31-90 days | L1 | Weekly summaries |
| 91-180 days | L2 | Monthly summaries + pins |
| 181-365 days | L2 low | Monthly summaries (lower weight) + pins |
| >365 days | Archive | Trend indicators + pins only |

## Pins Management

### Adding Pins

```
1. Validate type is one of: constraint, preference, non_negotiable, recurring_pattern, lesson
2. Set created_at to today
3. Set source to originating review reference (e.g., "daily_review_2026-01-17")
4. Set active to true
5. Append to pins.csv
```

### Querying Active Pins

```
1. Read pins.csv
2. Filter where active = true
3. Return all matching pins (no decay applied)
```

### Deactivating Pins

```
1. Find pin by content or created_at
2. Update active field to false
3. Preserve record for history
```

## Error Handling

### File Not Found
- For read operations: return empty dataset, not error
- For write operations: create file with headers first

### Corrupted CSV
- Attempt to parse what's readable
- Log corrupted lines
- Continue with valid data

## Usage Examples

### Example: Read Last 7 Days Reviews

```
1. Call goal-data skill with operation="read_daily_reviews"
2. Set date_range="last_7_days"
3. Returns array of review objects with decay weights
```

### Example: Append Daily Review

```
1. Call goal-data skill with operation="append_daily_review"
2. Provide structured fields:
   - date: "2026-01-19"
   - done_top3: "完成API集成|修复了3个bug"
   - energy_1_5: 4
   - mood_1_5: 4
   - plan_deviation_reason: "none"
3. Skill validates and appends to CSV
```

### Example: Generate Weekly Summary

```
1. Call goal-data skill with operation="generate_weekly_summary"
2. Set week_start="2026-01-13", week_end="2026-01-19"
3. Skill aggregates daily reviews
4. Skill generates and appends summary
5. Returns generated summary object
```

### Example: Update State with Calibration Patch

```
1. Call goal-data skill with operation="apply_state_patch"
2. Provide patch:
   {
     "calibration.task_adjustment.force_small_steps": true,
     "calibration.deviation_counters.unclear_next_action": 3
   }
3. Skill merges patch atomically
4. Returns updated state
```
