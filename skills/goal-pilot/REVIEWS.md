# Review Templates / 复盘模板

## Review Schedule Logic

Claude automatically triggers reviews based on:

| Review Type | Trigger Condition |
|-------------|-------------------|
| Daily | End of each session |
| Weekly | 7+ days since last session, or Sunday, or user request |
| Monthly | First session of new month |
| Quarterly | First session of new quarter |

---

## Daily Review / 每日复盘

### Template (Auto-fill from session data)

```markdown
## 📊 Daily Review - [Date]

### ✅ Completed
| Task | Priority | Time | Notes |
|------|----------|------|-------|
| [task] | P0/P1/P2 | [actual] | [notes] |

### ⬜ Incomplete → Tomorrow
| Task | Reason | Priority Tomorrow |
|------|--------|-------------------|
| [task] | [why] | [P0/P1/P2] |

### 💡 Learnings
1. What worked: [insight]
2. What didn't: [insight]
3. Tomorrow's adjustment: [action]

### 🎯 Tomorrow's Top Priority
[One sentence - the #1 thing]

### Energy Level (1-5): [X]

---
**Memory Updated**: Progress [X]% → [Y]%
```

---

## Weekly Review / 每周复盘

### Template

```markdown
## 📈 Weekly Review - Week [X]

### Week Overview
| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Tasks planned | [X] | [Y] | ✅/⚠️/❌ |
| Tasks completed | [X] | [Y] | [Y/X]% |
| P0 completion | 100% | [X]% | ✅/⚠️/❌ |

### 🏆 Wins This Week
1. [Win + impact]
2. [Win + impact]
3. [Win + impact]

### 🚧 Challenges
| Challenge | Root Cause | Learning |
|-----------|------------|----------|
| [challenge] | [cause] | [lesson] |

### 🔄 Process Check
| Question | Answer |
|----------|--------|
| What should I START doing? | [action] |
| What should I STOP doing? | [action] |
| What should I CONTINUE? | [action] |

### 📅 Next Week Focus
| Priority | Goal | Key Tasks |
|----------|------|-----------|
| P0 | [goal] | [tasks] |
| P1 | [goal] | [tasks] |

### 🎯 Progress Toward Goal
- Overall: [X]% → [Y]% (+[Z]%)
- On track for quarterly milestone? [Yes/No/At Risk]

---
**Memory Updated**: Weekly status saved
```

---

## Monthly Review / 月度复盘

### Template

```markdown
## 📅 Monthly Review - [Month Year]

### Monthly Goals Assessment
| Goal | Target | Actual | Score | Analysis |
|------|--------|--------|-------|----------|
| [goal] | [target] | [actual] | [X]% | [why] |

### 📊 Key Metrics
| Metric | Month Start | Month End | Change |
|--------|-------------|-----------|--------|
| [metric] | [X] | [Y] | [+/-Z%] |

### 🏆 Major Accomplishments
1. **[Title]**: [Description and impact]
2. **[Title]**: [Description and impact]

### 😰 Biggest Challenge
- What: [description]
- Root cause: [analysis]
- How handled: [response]
- Lesson: [learning]

### 📈 Goal Progress
| Timeframe | Expected | Actual | Gap |
|-----------|----------|--------|-----|
| By end of month | [X]% | [Y]% | [Z]% |
| By end of quarter | [X]% | Projected [Y]% | |

### 💰 Resources Used
| Resource | Budgeted | Used | Remaining |
|----------|----------|------|-----------|
| Time (hrs) | [X] | [Y] | [Z] |
| Money | [X] | [Y] | [Z] |

### 🔮 Next Month
#### Focus Areas
1. [Focus 1]
2. [Focus 2]

#### Key Objectives
| Objective | Success Metric |
|-----------|----------------|
| [objective] | [metric] |

### 💭 Reflection
1. Most proud of this month?
2. What would I do differently?
3. One habit to build next month?

---
**Memory Updated**: Monthly progress saved
```

---

## Quarterly Review / 季度复盘

### Template

```markdown
## 📊 Quarterly Review - [Quarter Year]

### Quarterly Milestone Assessment
| Milestone | Target | Actual | Status |
|-----------|--------|--------|--------|
| [milestone] | [target] | [actual] | ✅/⚠️/❌ |

### Key Results Scorecard
| Key Result | Target | Actual | Score (0-1.0) |
|------------|--------|--------|---------------|
| [KR1] | [target] | [actual] | [0.X] |
| [KR2] | [target] | [actual] | [0.X] |
| [KR3] | [target] | [actual] | [0.X] |
| **Average** | | | **[0.X]** |

### 🏆 Quarter Highlights
1. [Highlight with measurable impact]
2. [Highlight with measurable impact]
3. [Highlight with measurable impact]

### 📉 What Didn't Work
| Area | Issue | Root Cause | Learning |
|------|-------|------------|----------|
| [area] | [issue] | [cause] | [lesson] |

### 🔄 Strategic Assessment

#### Direction Evaluation
| Direction | Time Spent | ROI | Decision |
|-----------|------------|-----|----------|
| [P0] | [X]% | [result] | Continue/Adjust/Stop |
| [P1] | [X]% | [result] | Continue/Adjust/Stop |
| [P2] | [X]% | [result] | Continue/Adjust/Stop |

#### Start / Stop / Continue
| Action | Items |
|--------|-------|
| **Start** | [new initiatives] |
| **Stop** | [ineffective activities] |
| **Continue** | [working well] |
| **Amplify** | [do more of] |

### 📈 Annual Goal Progress
| Metric | Start of Year | Now | Year-End Target | Projected |
|--------|---------------|-----|-----------------|-----------|
| [primary] | [baseline] | [current] | [target] | [projected] |

### Confidence Assessment
- On track to achieve annual goal? [Yes/No/At Risk]
- Confidence level: [High/Medium/Low]
- Key risks: [risks]

### 📅 Next Quarter Planning

#### Quarterly Milestone
[Clear, measurable milestone]

#### Key Objectives
| # | Objective | Key Results |
|---|-----------|-------------|
| 1 | [objective] | [KRs] |
| 2 | [objective] | [KRs] |

#### Resource Allocation
| Resource | This Quarter | Next Quarter |
|----------|--------------|--------------|
| Time split | [breakdown] | [new breakdown] |
| Budget | [X] | [Y] |

### 💭 Deep Reflection
1. Biggest learning this quarter?
2. What surprised me?
3. What am I avoiding?
4. Am I still pursuing the right goal?
5. What would I tell myself 3 months ago?

---
**Memory Updated**: Quarterly progress and new phase saved
```

---

## Review Trigger Phrases

Claude should trigger reviews when user says:

| Phrase | Review Type |
|--------|-------------|
| "做复盘" / "do a review" | Ask which type |
| "日复盘" / "daily review" | Daily |
| "周复盘" / "weekly review" | Weekly |
| "月复盘" / "monthly review" | Monthly |
| "季度复盘" / "quarterly review" | Quarterly |
| "总结一下" / "summarize" | Based on timeframe |

---

## Auto-Review Logic

```
On session start:
  - If new month → Prompt monthly review first
  - If new quarter → Prompt quarterly review first
  - If 7+ days since last session → Prompt weekly review first
  
On session end:
  - Always do brief daily summary
  - Update memory with progress
```
