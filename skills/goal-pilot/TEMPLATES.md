# Reusable Templates / 可复用模板

These templates are used by Claude to structure responses consistently.

---

## Goal Framework Template

```markdown
# [Goal Name] - SOP Framework

## 1. Goal Statement
**What**: [Clear description]
**Why**: [Motivation]
**When**: [Target date]
**Measure**: [Key metric]

## 2. Success Metrics
| Metric | Baseline | Mid-Point | Target | Deadline |
|--------|----------|-----------|--------|----------|
| [primary] | [X] | [Y] | [Z] | [date] |
| [secondary] | [X] | [Y] | [Z] | [date] |

## 3. Quarterly Milestones
| Quarter | Phase | Milestone | Success Criteria |
|---------|-------|-----------|------------------|
| Q1 | Validate | [milestone] | [criteria] |
| Q2 | Scale | [milestone] | [criteria] |
| Q3 | Systematize | [milestone] | [criteria] |
| Q4 | Achieve | [milestone] | [criteria] |

## 4. Strategic Priorities
| Priority | Focus Area | Time % | Why |
|----------|------------|--------|-----|
| P0 | [main] | [X]% | [reason] |
| P1 | [secondary] | [X]% | [reason] |
| P2 | [support] | [X]% | [reason] |

## 5. Risks & Mitigation
| Risk | Likelihood | Impact | Warning Sign | Response |
|------|------------|--------|--------------|----------|
| [risk] | H/M/L | H/M/L | [signal] | [action] |

## 6. Resources
| Resource | Available | Allocated |
|----------|-----------|-----------|
| Time/week | [X] hours | [breakdown] |
| Budget | [X] | [breakdown] |
| Support | [people] | [roles] |
```

---

## Weekly Plan Template

```markdown
# Week [X]: [Date Range]

## Weekly Focus
[One sentence priority]

## Goals
| Goal | Success Metric | Priority |
|------|----------------|----------|
| [goal] | [metric] | P0 |
| [goal] | [metric] | P1 |

## Daily Breakdown

### Monday
| Task | Priority | Est. | Status |
|------|----------|------|--------|
| [task] | P0 | [time] | ⬜ |

### Tuesday
[Same structure]

### Wednesday
[Same structure]

### Thursday
[Same structure]

### Friday
[Same structure]

## Blockers to Address
| Blocker | Resolution | Owner |
|---------|------------|-------|
| [blocker] | [solution] | [who] |
```

---

## Daily Task List Template

```markdown
## 📅 [Day, Date]

### 🎯 Today's Focus
[One sentence - the priority]

### ✅ Tasks

#### 🔴 P0 - Must Complete
| # | Task | Est. | Status |
|---|------|------|--------|
| 1 | [task] | [time] | ⬜ |

#### 🟡 P1 - Should Complete
| # | Task | Est. | Status |
|---|------|------|--------|
| 2 | [task] | [time] | ⬜ |

#### 🟢 P2 - If Time Permits
| # | Task | Est. | Status |
|---|------|------|--------|
| 3 | [task] | [time] | ⬜ |

#### ⏸️ Carried Forward
| # | Task | From |
|---|------|------|
| 4 | [task] | [date] |

---
**Total estimated time**: [X] hours
```

---

## Task Breakdown Template

```markdown
## 🔨 Task: [Name]

### Overview
| Field | Value |
|-------|-------|
| Priority | P0/P1/P2 |
| Est. Time | [X min/hours] |
| Due | [date/time] |

### Objective
[What completing this achieves]

### Steps

**Step 1: [Name]** (~X min)
- [Detail]
- [Detail]
- ✓ Checkpoint: [verification]

**Step 2: [Name]** (~X min)
- [Detail]
- [Detail]
- ✓ Checkpoint: [verification]

### Resources
| Resource | Source |
|----------|--------|
| [resource] | [where to find] |

### Blockers & Solutions
| Blocker | Solution |
|---------|----------|
| [blocker] | [how to handle] |

### Definition of Done
- [ ] [criterion 1]
- [ ] [criterion 2]
```

---

## Progress Update Template

```markdown
## ✅ Progress Updated

| Task | Previous | New |
|------|----------|-----|
| [task] | ⬜ | ✅ |

### Session Progress
- Completed: X/Y tasks
- P0: X/Y | P1: X/Y
- Time: ~X hours

### Key Notes
- [insight or observation]

### Next Action
[What to do next]
```

---

## Session Summary Template

```markdown
## 📊 Session Summary - [Date]

### ✅ Completed
| Task | Priority | Notes |
|------|----------|-------|
| [task] | P0 | [notes] |

### ⬜ Carried Forward
| Task | Reason | Tomorrow Priority |
|------|--------|-------------------|
| [task] | [reason] | P0/P1 |

### 📈 Progress
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Overall | [X]% | [Y]% | +[Z]% |
| Week tasks | X/Y | X/Y | +N |

### 💡 Key Insight
[One main learning or observation]

### 🔮 Next Session Preview
- [Top priority for next time]

---
✅ Memory updated
```

---

## Course Correction Template

```markdown
## ⚠️ Progress Check

### Status
| Metric | Expected | Actual | Gap |
|--------|----------|--------|-----|
| Progress | [X]% | [Y]% | [Z]% |
| [key metric] | [X] | [Y] | [gap] |

### Analysis
[Why the gap exists - 2-3 sentences]

### Options
| # | Option | Pros | Cons |
|---|--------|------|------|
| A | [option] | [pros] | [cons] |
| B | [option] | [pros] | [cons] |
| C | [option] | [pros] | [cons] |

### Recommendation
[Suggested action with reasoning]

---
Which resonates with you?
```

---

## Memory Data Template

This is the format Claude uses to store data in memory:

```
GTD Goal: [One-line goal - max 100 chars]
GTD Target Date: [YYYY-MM-DD]
GTD Current Phase: [Q1-Validate/Q2-Scale/Q3-Systematize/Q4-Achieve]
GTD Progress: [0-100]%
GTD Last Session: [YYYY-MM-DD]
GTD Language: [English/中文/日本語]
GTD Weekly Status: Week [X] - [Y]/[Z] tasks
GTD Key Metrics: [metric1:value, metric2:value]
GTD Active Tasks: [task1|status, task2|status]
GTD Blockers: [blocker1, blocker2] or "none"
```

### Memory Update Rules

**On Goal Setup:**
- Add all GTD entries
- Set Progress to 0%
- Set Phase to Q1-Validate

**On Session End:**
- Replace GTD Progress with new value
- Replace GTD Last Session with today
- Replace GTD Weekly Status
- Replace GTD Active Tasks with current state

**On Phase Change:**
- Replace GTD Current Phase
- Update milestones in conversation

**On Goal Reset:**
- Remove all GTD entries

---

## Status Icons Reference

| Icon | Meaning (EN) | 中文 | Use When |
|------|--------------|------|----------|
| ⬜ | Todo | 待办 | Not started |
| 🔄 | In Progress | 进行中 | Currently working |
| ✅ | Completed | 已完成 | Done |
| ❌ | Cancelled | 已取消 | Won't do |
| ⏸️ | Paused | 暂停 | Temporarily stopped |
| ⚠️ | At Risk | 有风险 | May not complete on time |
| 🎯 | Focus | 焦点 | Priority item |
| 🔴 | P0 | 最高优先 | Must do |
| 🟡 | P1 | 中优先 | Should do |
| 🟢 | P2 | 低优先 | Nice to have |
| 🏆 | Win | 胜利 | Achievement |
| 💡 | Insight | 洞察 | Learning |
| 📊 | Data | 数据 | Metrics |
| 📅 | Date | 日期 | Time reference |
| 📈 | Growth | 增长 | Positive trend |
| 📉 | Decline | 下降 | Negative trend |

---

## Quick Command Reference

| User Says | Claude Action |
|-----------|---------------|
| "今天做什么" / "what's today's task" | Generate daily tasks |
| "开始任务X" / "start task X" | Break down task X |
| "完成了" / "done" | Update progress |
| "结束" / "end session" | Session summary + save |
| "做复盘" / "do review" | Trigger appropriate review |
| "查看进度" / "show progress" | Display goal overview |
| "调整计划" / "adjust plan" | Course correction flow |
| "重置" / "reset" | Clear memory, start fresh |
