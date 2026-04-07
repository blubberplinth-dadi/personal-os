# TM JIRA Reference Material

This guide contains governance best practices and management board configurations.

**Related guides:**
- [Configuration & Workflow](config-and-workflow.md) - Core setup, planning and execution workflows

---

## 1. Epic Governance & Best Practices

### 1.1 Clear Epic Ownership

**Required Fields on Epics:**
- ✅ Teymi field assigned (Bót or Ronja)
- ✅ Component assigned
- ✅ Epic Lead assigned for accountability (optional but recommended)

**Ownership Rules:**
1. Every Epic must have Teymi field assigned → Forces clear ownership
2. Component indicates which product(s) Epic affects → Clear scope
3. Separate Epic boards → Teams don't see each other's Epics during planning
4. Epic Lead field → Assign specific person as Epic owner (optional)

---

### 1.2 Preventing Team Conflicts

#### Clear Ownership Rules
- Every issue must have Teymi field assigned
- Component indicates which product
- Assignee indicates individual owner

#### Separate Boards = Separate Contexts
- Teams primarily work in their own boards
- No visual clutter from other team's work

#### Notification Schemes
- Configure watchers by component
- Team members auto-watch issues in their components
- Reduce noise from other team's updates

#### Permission Schemes (If Needed)
- Generally, keep open — both teams can see all work
- Only restrict if sensitive business reasons exist

---

## 2. Management Board Configurations

### All Epics Overview Board

**Purpose:** Executive/PM view across both teams

**Filter:**
```
project = Insurances
AND issuetype = Epic
ORDER BY Rank
```

**Configuration:**
- **Columns:** To Do → In analysis → Ready for development → In Progress → Done
- **Swim lanes:** By Teymi field (shows Bót and Ronja swim lanes)
- **Card colors:** By Teymi field (visual differentiation)
- **Quick filters:**
  - "Bót Team" → `Teymi = "Bót"`
  - "Bóthildur" → `Component = "Bóthildur"`
  - "Active" → `status != Done`

---

### Cross-Team Work Board (Optional)

**Purpose:** See all in-progress work across teams

**Filter:**
```
project = Insurances
AND issuetype != Epic
AND status IN ("In Progress", "In review", "In testing")
ORDER BY Rank
```

**Configuration:**
- **Columns:** In Progress → In review → In testing
- **Swim lanes:** By Teymi field
- **Quick filters:**
  - "Bót Team" → `Teymi = "Bót"`
  - "Ronja Team" → `Teymi = "Ronja"`
  - By Component
  - By Epic Link

---

## 3. Naming Conventions

### 3.1 Filters

**Format:** `Team/Scope - Description`

Use `Bót`, `Ronja`, or `Shared` as the prefix, followed by what the filter is used for.

**Examples:**
```
Bót - Epic board
Bót - Work board
Ronja - Epic board
Ronja - Work board
Shared - Bug board
Shared - All Epics overview
```

**Work-in-progress filters:** Prefix with `[WIP]` to keep experimental filters out of the shared list.
```
[WIP] Daði - testing epic filter
```

**Rule:** Every filter that drives a board or dashboard gadget must follow this convention. Personal/exploratory filters should use `[WIP]` until promoted.

---

*End of Standards*
