# Status Separation Proposal

## Problem

People are confused about which board issues land on when changing statuses. The current status names don't signal which board they belong to.

**Concrete example:** Someone added "To Do" to the Work Board's first column, so new issues now land on the Work Board instead of the Epic Board (planning). This breaks the intended workflow separation.

## Proposal A: Prefix-Based Separation

Create two completely separate status sets with explicit prefixes that signal which board the status belongs to.

### Proposed Status Structure

#### Epic Board Statuses

| Status | Column | Purpose |
|--------|--------|---------|
| `Epic: Næst` | Næst inn | Work identified but not yet prioritized |
| `Epic: Í greiningu` | Í greiningu | Being analyzed and broken down |
| `Epic: Tilbúið` | Tilbúið í þróun | Ready to transition to development |
| `Epic: Í þróun` | Í þróun | Epic in active development |
| `Epic: Lokið` | Lokið | Completed |

#### Work Board Statuses

| Status | Column | Purpose |
|--------|--------|---------|
| `Dev: Næst` | Næst inn | Queued for active development |
| `Dev: Í þróun` | Í þróun | In active development |
| `Dev: Kóðarýni` | Í kóðarýni | In code review |
| `Dev: Gæðaeftirlit` | Í gæðaeftirliti | In QA/quality control |
| `Dev: Bíður útgáfu` | Bíður útgáfu | Awaiting release/deployment |
| `Dev: Lokið` | Tilbúið | Done/Released |

### Benefits

- **Self-documenting:** Status name tells you exactly which board it belongs to
- **Prevents accidental misconfiguration:** Adding `Epic: Næst` to a Work Board column would look obviously wrong
- **Clearer for users:** When changing status, the prefix guides the choice
- **Cleaner JQL:** Can filter by prefix pattern if needed

### Open Question

Should "Lokið/Done" be shared or separate?

**Current proposal:** Separate (`Epic: Lokið` and `Dev: Lokið`)

- Pro: Conceptually cleaner, complete separation
- Con: Two "done" statuses appear in reports

### Migration Steps

1. Create new statuses in JIRA
2. Update workflow to include new statuses and transitions
3. Bulk-update existing issues from old statuses to new ones
4. Update board column mappings
5. Remove old statuses from workflow
6. Delete old statuses

## Next Steps

- [ ] Decide on shared vs separate "Lokið" status
- [ ] Review with Óli and Óskar
- [ ] Plan migration timing

---

## Proposal B: LB Corporate Status Set

### Context

LB mandates a corporate status set across all JIRA projects:
`To Do` · `Next In` · `In Progress` · `Blocked` · `In review` · `Ready for testing` · `In testing` · `Ready for deployment` · `Done`

This proposal maps those statuses to TM's two-board system.

### Mapping Strategy

Board filters separate issues between boards. Status names and column names are identical everywhere — no translation layer needed. Two new custom statuses ("In analysis", "Ready for development") are created for the Epic Board's planning columns. All other statuses come from the corporate set.

**Statuses not mapped to any column:** `Ready for testing` and `Blocked` are available in the corporate set but not used in board columns. `Blocked` can be combined with JIRA's Flag feature for visibility. Add columns later if needed.

### Epic Board

Keeps the current 5-column structure.

**Filter (Bót):**
```jql
project = Insurances AND Teymi = "Bót"
AND (issuetype = Epic OR ("Epic Link" is EMPTY AND status = "To Do"))
```

**Columns:**

| Column | Status | What's here |
|--------|--------|-------------|
| To Do | To Do | Epics + standalone items not yet prioritized |
| In analysis | In analysis | Epics being analyzed and broken down |
| Ready for development | Ready for development | Analysis complete, ready for development |
| In Progress | In Progress | Epics in active development |
| Done | Done | Completed |

- Same 5 columns as current setup
- Standalone items only sit in To Do — status change to Next In moves them to Work Board

### Work Board

**Filter (Bót):**
```jql
project = Insurances AND Teymi = "Bót" AND issuetype != Epic
```

**Columns:**

| Column | Status | What's here |
|--------|--------|-------------|
| Next In | Next In | Queued for development |
| In Progress | In Progress | In active development |
| In review | In review | In code review |
| In testing | In testing | In QA |
| Ready for deployment | Ready for deployment | Awaiting release |
| Done | Done | Released |

- Same 6 columns as current setup
- "Ready for testing" not used — items go directly from code review to testing

### Shared Statuses Across Boards

Two statuses are used on both boards. They mean the same thing on each board, so there's no ambiguity:

| Status | Epic Board | Work Board |
|--------|-----------|------------|
| In Progress | Active development | Active development |
| Done | Completed | Released |

No issue ever appears on both boards — filters guarantee separation.

### How Items Move Between Boards

```
Epic Board                           Work Board
┌──────────────────────────┐        ┌────────────────────────────┐
│                          │        │                            │
│  Epics:                  │        │  Stories/Tasks/Bugs:       │
│  To Do → In analysis →   │        │  Next In → In Progress →   │
│  Ready for development   │        │  In review → In testing →  │
│  → In Progress           │        │                            │
│  → Done                  │        │  Ready for deployment →    │
│                          │        │  Done                      │
│  Standalone:             │  ──→   │                            │
│  To Do (only)            │        │                            │
│     ↓ status → Next In   │        │                            │
│  (moves to Work Board)   │        │                            │
└──────────────────────────┘        └────────────────────────────┘
```

**Epics:** To Do → In analysis → Ready for development → In Progress → Done (stay on Epic Board only)

**Standalone items:**
1. Created in To Do → appears on Epic Board
2. Status changed to Next In → disappears from Epic Board, appears on Work Board

**Epic-linked Stories:**
1. Created in To Do (visible in Epic detail view, not on any board)
2. Changed to Next In → appears on Work Board with Epic name on card

### Trade-offs

**What's lost vs current setup:**
- Standalone items get only one planning column on Epic Board (To Do)
- Two custom statuses needed beyond the corporate set (In analysis, Ready for development)

**What's gained:**
- LB compliance (corporate set used for all development statuses)
- Keeps current column count on both boards (5 Epic, 6 Work)
- No dual-meaning statuses — every status means the same thing wherever it appears
- Status = column name everywhere — no translation layer to learn
- Explicit Blocked status available when needed

### Comparison: Proposal A vs B

| | Proposal A (Prefixes) | Proposal B (Corporate) |
|---|---|---|
| Status naming | Self-documenting (Epic: / Dev:) | Corporate standard names |
| Board confusion risk | Very low (prefix tells you) | Low (filters separate boards, no dual meanings) |
| Epic Board columns | 5 | 5 |
| Work Board columns | 6 | 6 |
| LB compliance | No | Yes |
| Migration | Create all new statuses | Use corporate set + 2 new statuses |

### Open Questions

- Is the corporate set strictly fixed, or can unused statuses (Ready for testing) be hidden from the status dropdown?
- Is Blocked mandatory to use or just available?
- Will LB approve the two custom statuses (In analysis, Ready for development)?
