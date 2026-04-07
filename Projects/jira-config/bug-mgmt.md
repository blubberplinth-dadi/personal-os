# Bug Management for TM

**Related guides:**
- [config-and-workflow.md](config-and-workflow.md) - Core configuration and workflow
- [standards.md](standards.md) - Epic governance, management board configurations, naming conventions

---

## Approach

Every bug gets triaged within 2 business days. Non-urgent bugs live on a shared Bug Board until the product owner explicitly moves them to the Work Board. Bugs that sit for 3 months without being scheduled get declined.

---

## How bugs flow

```
Bug reported → Bug Board ("To Do")
                 │
                 ├─ Won't fix → Status → "Done / Declined"
                 ├─ Fix now → Status → "Next In" (appears on Work Board)
                 └─ Fix later → Set priority, rank by dragging
                                  │
                                  │ When product owner is ready:
                                  │ Status → "Next In"
                                  ▼
                              Work Board (normal dev flow)
```

Bugs are filtered OUT of the Epic Board. The Epic Board stays focused on strategic planning.

---

## Bug Board configuration

**One shared board for both teams.**

**Filter:**
```
project = Insurances
AND issuetype = Bug
ORDER BY priority DESC, created ASC
```

**Columns:** To Do → Next In → Done / Declined

Once a bug reaches "Next In" it's visible on the team's Work Board where it flows through the full dev workflow. "Done / Declined" shows recently completed and recently declined bugs in one place. Configure the column to only show bugs from the last 14 days to prevent clutter.

**Quick filters:**
- **"Bót"** → `Teymi = "Bót"`
- **"Ronja"** → `Teymi = "Ronja"`
- **"Untriaged"** → `priority is EMPTY`

---

## Epic Board change

Add this to each team's Epic Board filter to exclude bugs:

```
AND issuetype != Bug
```

---

## Priority meanings

| Priority | Meaning | Scheduling signal |
|----------|---------|-------------------|
| High | Real problem, workaround exists | Within ~4 weeks |
| Medium | Minor annoyance, edge case | Within ~8 weeks |
| Low | Cosmetic, extremely rare | When convenient or decline at expiry |

---

## Bug budget

Each team reserves ~15–20% of capacity for bugs each cycle. The product owner fills this by moving bugs from "To Do" to "Next In" on the Bug Board.

---

## Monthly review (30 min)

Product owner opens the Bug Board with their team's quick filter:
- Bugs older than 3 months → move to "Next In" or "Declined"
- Re-rank remaining bugs
- Done

---

## Automation rules

**Triage reminder** (daily, one rule per team):
- Condition: `issuetype = Bug AND Teymi = "[team]" AND status = "To Do" AND priority is EMPTY AND created <= -2d`
- Action: Notify product owner

**Expiry warning** (weekly Monday, one rule per team):
- Condition: `issuetype = Bug AND Teymi = "[team]" AND status = "To Do" AND created <= -11w`
- Action: Comment on issue + notify product owner

---

## Setup summary

| Change | Effort |
|--------|--------|
| Create shared Bug Board with filter and quick filters | 15 min |
| Add `AND issuetype != Bug` to both Epic Board filters | 2 min |
| Set up 4 automation rules (2 per team) | 20 min |
| Agree on priority meanings and bug budget % | One conversation |
