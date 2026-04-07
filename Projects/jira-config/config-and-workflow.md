# TM JIRA Configuration & Workflow Guide (Custom Team Field Version)

This guide covers the core JIRA configuration and workflows for TM's software development teams.

**Related guides:**
- [Standards](standards.md) - Epic governance, management board configurations, naming conventions

---

## 1. Introduction & Context

This guide describes the complete JIRA configuration for TM's software development teams working on multiple insurance products within a single JIRA project.

---

## 2. Core Configuration Elements

### 2.1 Issue Types & Hierarchy

TM uses the standard JIRA issue type hierarchy:

**Issue Types:**
- **Epic** - Large initiatives spanning multiple sprints (1-3 months)
- **Story** - User-facing functionality (if it looks like >5 days of work, it's probably too big)
- **Task** - Development work not directly user-facing
- **Bug** - Defects and fixes
- **Sub-task** - Breakdown of a Story into smaller pieces (hidden from board cards via sub-filter)

**When to Use Each Type:**
- **Epic:** Strategic initiatives requiring planning and coordination across multiple sprints
- **Story:** Features that deliver value to end users
- **Task:** Technical work like setup, configuration, backend improvements, infrastructure, refactoring
- **Bug:** Issues that need fixing in existing functionality

---

### 2.2 Component Structure

Components indicate which system or product the work affects. Always assign at least one component to every issue.

**Available Components (examples):**

```
├── Vefsala TM (online insurance sales)
├── Bóthildur (claims management)
├── Rósin (policy management)
├── API (insurance and claims APIs)
└── ... (other components as needed)
```

**How to Select Components:**

- **Single system:** Select the relevant component
- **Multiple systems:** Select all components the work affects

**Examples:**

```
Bug: Date picker validation error
└── Component: Rósin

Story: Open claim invoice even when case number is missing
└── Components: Bóthildur, Rafrænir reikningar

Epic: Receive and process electronic invoices to TM
└── Components: Rafrænir reikningar, Bóthildur, API, Sjálfvirkni
```

**Rule:** Always select a component. When in doubt, select the component most affected by the work.

**Exception — Sub-tasks:** Don't bother setting Component on Sub-tasks. They're hidden from boards, only visible inside the parent Story's detail view, and never filtered or reported on independently. The component on the parent Story is sufficient.

---

### 2.3 Team Separation

TM uses a **custom Teymi field** to separate work between teams. This field is required on all work items.

**Teymi Field Configuration:**
- **Field Name:** Teymi
- **Field Type:** Single-select dropdown
- **Values:**
  - Bót
  - Ronja
- **Required:** Yes (on all issue types)

**Why Custom Field Over Labels:**
- Single-select ensures each item has exactly one team
- Better for reporting and dashboards
- Cleaner filters and JQL queries
- Can enforce as required field
- Prevents items from having multiple or missing team assignments

**Data Quality:**
- Monitor for items missing Teymi assignment
- Field validation prevents multiple team assignments

---

### 2.4 Status Workflow

TM uses statuses from LB's corporate set plus two custom planning statuses. Status names and column names are identical everywhere. Board filters control which issues appear on which board.

#### Planning Statuses (Epic Board Only)

These custom statuses appear only on the Epic Board:
- **In analysis** - Being analyzed and broken down into actionable items
- **Ready for development** - Ready to transition to active development

#### Development Statuses (Work Board - Stories/Tasks/Bugs)

These statuses from the LB corporate set are used by Stories, Tasks, and Bugs on the Work Board:
- **Next In** - Queued for active development
- **In Progress** - In active development
- **In review** - In code review
- **In testing** - In QA/quality control
- **Ready for deployment** - Awaiting release/deployment
- **Done** - Done/Released

#### Bug Board Statuses

The Bug Board uses three statuses:
- **To Do** - Reported, awaiting triage
- **Next In** - Triaged and scheduled; bug also appears on the team's Work Board
- **Done / Declined** - Completed or declined bugs (last 14 days shown to prevent clutter)

#### Shared Statuses

Three statuses from the corporate set are used on both the Epic Board and Work Board:
- **To Do** - Epic Board: work identified but not yet prioritized. Work Board: not mapped to a column (items in To Do are not visible on the Work Board).
- **In Progress** - Active development on both boards
- **Done** - Completed on both boards

No issue appears on more than one of the three boards — filters guarantee separation.

#### Unused Corporate Statuses

These statuses exist in the LB corporate set but are not mapped to any board column:
- **Blocked** - Can be combined with JIRA's Flag feature for visibility
- **Ready for testing** - Not used; items go directly from In review to In testing

**How Board Visibility Works:**
- Status name = column name everywhere — no translation layer
- Filters define which issue types appear on each board
- Kanban sub-filters hide items that shouldn't appear as cards (e.g., Sub-tasks)
- No manual board movement needed - status change drives the transition

---

## 3. Work Classification: Epic vs Standalone

Not all work items need to be linked to Epics. TM uses a clear framework for deciding when to create an Epic versus when to use standalone work items.

### 3.1 When to Create Epics (Strategic/Planned Work)

**Epic Creation Threshold:**
- Create Epic when you have 3+ related Stories/Tasks
- Create Epic for work estimated > 1 sprint
- Create Epic for strategic initiatives requiring planning/design
- DON'T create Epic for small isolated work

**Use Epics for:**
- ✅ Part of larger initiative spanning 1-3 months
- ✅ Multiple related stories contributing to cohesive goal
- ✅ User-facing features requiring design and planning
- ✅ Work requiring cross-team or cross-system coordination
- ✅ Strategic roadmap initiatives
- ✅ Major refactoring or architectural changes

**Epic Size Guidelines:**
- Epics should be completable in 1-3 months
- If longer, break into multiple Epics
- If shorter, might just be a Story

**Examples of Good Epic Candidates:**
- ✅ "Performance Optimization - Bóthildur Search" (specific goal)
- ✅ "GDPR Compliance - Customer Data" (cohesive initiative)
- ✅ "Modernize Claims Photo Upload" (clear scope)

---

### 3.2 When to Use Standalone Work (Operational/Tactical)

**Use Standalone Work for:**
- ✅ Small bugs — but note: bugs go to the **Bug Board**, not the Epic Board (see Section 6)
- ✅ Individual tech debt items (unless part of larger tech debt Epic)
- ✅ Minor UI/UX improvements and quick fixes
- ✅ Operational/maintenance tasks
- ✅ Documentation updates
- ✅ Performance optimizations (single component)
- ✅ Dependency updates
- ✅ Small enhancements completable in single sprint

**Epic Linking Discipline:**
- Use "Epic Link" field for all Epic-related work
- Leave "Epic Link" empty for standalone work
- Review standalone work periodically to identify patterns that warrant Epic creation

---

### 3.3 Avoiding "Junk Drawer" Epics

**Anti-Patterns to Avoid:**
- ❌ Don't create: "Q1 Bug Fixes" (catch-all)
- ❌ Don't create: "Miscellaneous Improvements" (vague)
- ❌ Don't create: "Tech Debt" without specific goal

**Backlog Refinement for Standalone Work:**
- Review standalone work quarterly
- Identify patterns that warrant Epic creation
- Group related standalone items into new Epic if trend emerges
- Archive completed standalone work regularly

---

### 3.4 Work Breakdown Approaches

Work breakdown is handled through three complementary approaches: Sub-tasks, keeping Stories small, and description tracking.

#### Approach 1: Sub-tasks (With Sub-filter)

Sub-tasks can be used to break down Stories into smaller pieces of work.

**How Sub-tasks work in TM's configuration:**
- Sub-tasks are part of the board scope (included in filter)
- A **Kanban sub-filter** hides Sub-tasks from appearing as cards on the board
- Sub-tasks are visible in the parent Story's detail view
- This gives the benefit of tracking without board clutter

**When to use Sub-tasks:**
- Breaking a Story into parallel work items for multiple developers
- Tracking distinct pieces that need separate status tracking
- Work that benefits from JIRA's built-in progress tracking

**Example:**
```
TM-500: Add photo upload to claims [Story]
├── TM-500-1: Implement upload UI component [Sub-task]
├── TM-500-2: Add backend API endpoint [Sub-task]
└── TM-500-3: Write integration tests [Sub-task]
```

#### Approach 2: Keep Stories Small

**The principle:** If a Story looks like it needs >5 days of work, it's probably too big.

**Guidelines:**
- If a Story seems too large, split it into multiple smaller Stories
- All related Stories link to the same Epic
- Each Story appears independently on the Work Board

**Example - Splitting a large Story:**

*Before (too large):*
```
TM-500: Add photo upload to claims [Story]
```

*After (properly split):*
```
TM-500: Add photo upload UI component [Story] - Epic: Claims Modernization
TM-501: Implement photo upload backend API [Story] - Epic: Claims Modernization
TM-502: Add photo validation and error handling [Story] - Epic: Claims Modernization
```

#### Approach 3: Description Tracking (Within-Story Steps)

For tracking implementation steps within a single Story, use a bulleted list in the Description field. Mark completed items with strikethrough.

**Format:**
```
**Tasks:**
- ~~Design component layout~~
- ~~Implement basic upload button~~
- Add drag-and-drop support
- Write unit tests
- Update API documentation
```

**When to use:**
- Implementation steps that don't warrant separate Stories
- Acceptance criteria checklist
- QA verification steps
- Personal work tracking within an assigned Story

**Tips:**
- Keep the list short (3-7 items)
- Use strikethrough (`-text-` in JIRA wiki markup) for completed items
- Update as work progresses
- If list grows beyond 7 items, consider splitting the Story

#### Choosing Between Approaches

| Situation | Approach |
|-----------|----------|
| Work can be done by different people in parallel | Sub-tasks or split into separate Stories |
| Pieces need separate status tracking under one Story | Sub-tasks |
| Work spans multiple days with distinct deliverables | Split into separate Stories |
| Work needs independent Epic linking | Split into separate Stories |
| Simple implementation steps for one person | Description tracking |
| QA checklist or acceptance criteria | Description tracking |
| Personal task tracking | Description tracking |

---

## 4. Planning Workflow: Using the Epic Board

### 4.1 Epic Board Purpose & Scope

The Epic Board is where teams plan their strategic work and manage upcoming standalone work items before they enter active development.

**What the Epic Board Shows:**
- **All Epics** throughout their entire lifecycle (To Do → In analysis → Ready for development → In Progress → Done)
- **Standalone work items** (Stories/Tasks not linked to any Epic) in To Do and In analysis
- **Sub-tasks on Epics** in To Do and In analysis (discovery/analysis work)

> **Bugs are excluded from the Epic Board.** Bugs have their own Bug Board — see Section 6.

**What Happens on This Board:**
- Epics appear as cards throughout their lifecycle and never leave
- Standalone items appear as cards only while in To Do or In analysis
- Sub-tasks on Epics appear as cards while in To Do or In analysis
- Teams rank items by dragging cards up/down within columns
- "To Do" column holds identified but not-yet-prioritized work
- Teams move Epics to "In analysis" when ready to analyze and break them down
- Epics in "In analysis" are broken down into Stories; sub-tasks on the Epic track discovery work
- Epics in "Ready for development" are ready for development
- **Epics** move to "In Progress" and stay on Epic Board
- **Standalone work** moves to Work Board when status changes to Next In
- **Stories** (linked to Epics) move to Work Board when status changes to Next In

**Board Type:** Board-only (no backlog feature needed)

---

### 4.2 Epic Board Filter Configuration

#### Bót - Epic board

**Filter:**
```
project = Insurances
AND Teymi = "Bót"
AND issuetype != Bug
AND (issuetype = Epic OR (("Epic Link" is EMPTY OR issuetype = Sub-task) AND status in ("To Do", "In analysis")))
ORDER BY Rank
```

**Kanban Sub-filter:**
```
(fixVersion in unreleasedVersions() OR fixVersion is EMPTY)
```

> **Note:** The filter includes all Epics, standalone work in To Do and In analysis, and sub-tasks on Epics in To Do and In analysis. The sub-filter no longer excludes Sub-tasks since they are intentionally shown as cards for discovery tracking.

**Configuration:**
- **Columns:** To Do → In analysis → Ready for development → In Progress → Done
  - **To Do** = Epics and standalone items not yet prioritized
  - **In analysis** = Being analyzed and broken down
  - **Ready for development** = Analysis complete, ready for development
  - **In Progress** = Epics in active development (Stories appear on Work Board)
  - **Done** = Completed Epics
- **Swim lanes:** None (all items displayed in columns without swim lane separation)
- **Quick filters:**
  - "Epics Only" → `issuetype = Epic`
  - "Bóthildur" → `Component = "Bóthildur"`
  - "Current Quarter" → `created >= startOfQuarter()`

#### Ronja - Epic board

**Filter:**
```
project = Insurances
AND Teymi = "Ronja"
AND issuetype != Bug
AND (issuetype = Epic OR (("Epic Link" is EMPTY OR issuetype = Sub-task) AND status in ("To Do", "In analysis")))
ORDER BY Rank
```

Same sub-filter and configuration as Bót - Epic board.

---

### 4.3 Team Lead Planning Flow

**How Team Leads Use the Epic Board:**

1. **Open Team Epic Board** → Review all Epics and upcoming standalone work
2. **Prioritize items** by dragging within columns to set priority order
3. **Move Epic to "In analysis"** when ready to analyze and break down
4. **For Epics during "In analysis":**
   - Break down Epic into Stories
   - Link Stories to Epic using "Epic Link" field
   - Stories start in "To Do" status
5. **Move Epic to "Ready for development"** when planning is complete
6. **Move Epic to "In Progress"** when development starts
7. **For Stories:** Change Story status to "Next In" → Story appears on Work Board
8. **For Standalone work:** Change status to "Next In" → Item disappears from Epic Board and appears on Work Board

---

### 4.4 Visual Workflow Diagram

**How Items Move Through Epic Board:**

```
Epic Board Columns (Planning & Tracking)
┌──────────────────────────────────────────────────────────────────────────┐
│                                                                          │
│  To Do → In analysis → Ready for development → In Progress → Done        │
│                                                                          │
│  EPICS flow through ALL columns (stay on Epic Board)                    │
│  ├─ Created in "To Do"                                                  │
│  ├─ Move to "In analysis" for analysis and Story creation               │
│  ├─ Move to "Ready for development" when ready                          │
│  ├─ Move to "In Progress" when dev starts                               │
│  └─ Move to "Done" when all work complete                               │
│                                                                          │
│  SUB-TASKS ON EPICS show in "To Do" and "In analysis" only              │
│  ├─ Used to track discovery work (FD drafts, user interviews, etc.)    │
│  └─ Disappear from board when status moves beyond "In analysis"        │
│                                                                          │
│  STANDALONE WORK shows in "To Do" and "In analysis" only               │
│  └─ Disappears when status → Next In (moves to Work Board)             │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
                              │
                              │ Status change to Next In
                              ├─ Stories (linked to Epic)
                              └─ Standalone work
                              │
                              ▼
                    Work Board (Development)
```

---

## 5. Execution Workflow: Using the Work Board

### 5.1 Work Board Purpose & Scope

The Work Board is where teams execute their daily development work, showing all active Stories, Tasks, and Bugs as cards.

**What the Work Board Shows:**
- **Stories/Tasks/Bugs** in development statuses (both Epic-linked and standalone)
- Items appear when their status changes from planning status to development status
- **Epic name displayed on each card** provides context for which Epic the work belongs to

**What Happens on This Board:**
- All work items appear as flat cards (no swim lanes)
- Team members see Epic context via the Epic name field on each card
- Stories move through development workflow (Next In → In Progress → In review → etc.)
- Epics themselves stay on the Epic Board only (not shown on Work Board)
- Use Quick Filters to focus on specific Epics or standalone work

**Board Type:** Kanban or Scrum board (team preference)

---

### 5.2 Work Board Filter Configuration

#### Bót - Work board

**Filter:**
```
project = Insurances
AND Teymi = "Bót"
AND issuetype != Epic
ORDER BY Rank
```

**Kanban Sub-filter:**
```
(fixVersion in unreleasedVersions() OR fixVersion is EMPTY) AND issuetype != Sub-task
```

> **Note:** The filter includes all non-Epic work items. Sub-tasks are part of the board scope but the sub-filter hides them from appearing as cards - they're visible in the parent Story's detail view. Stories/Tasks/Bugs show the Epic name on each card for context.

**Configuration:**
- **Columns:** Next In → In Progress → In review → In testing → Ready for deployment → Done
  - **Next In** = Queued for active development (first column items move into)
  - **In Progress** = In active development
  - **In review** = In code review
  - **In testing** = In QA/quality control
  - **Ready for deployment** = Awaiting release/deployment
  - **Done** = Done/Released
- **Swim lanes:** None (flat card view)
- **Card layout:** Configure to show Epic name field on cards for context
- **Quick filters:**
  - "Epic Work" → `"Epic Link" is not EMPTY`
  - "Standalone" → `"Epic Link" is EMPTY`
  - "My Items" → `assignee = currentUser()`
  - Filter by specific Epic → `"Epic Link" = TM-XXX`

#### Ronja - Work board

Same configuration as Bót - Work board, but filter uses `Teymi = "Ronja"`.

---

### 5.3 Team Member Daily Flow

**How Team Members Use the Work Board:**

1. **Open Team Work Board** → See active development work (Stories/Tasks/Bugs)
2. **Epic name on cards** shows which Epic each item belongs to
3. **Use Quick Filters** to focus on a specific Epic or see only standalone work
4. **Click Epic name** on any card to navigate to Epic details and see overall progress
5. **Move items** through development columns as work progresses
6. **Need to plan upcoming work?** Switch to Team Epic Board

---

### 5.4 Epic Progress Tracking

**How Epic Progress is Tracked:**

- **Epics stay on Epic Board** throughout their lifecycle (planning through completion)
- **Epic Board** shows Epic in "In Progress" column when in active development
- **Work Board** shows Stories/Tasks/Bugs with Epic name on each card
- **Epic progress** calculated from Stories (% complete, Story points, etc.) - visible on Epic detail view
- **Team leads** monitor Epic Board to see overall Epic status across all Epics
- **Team members** see Epic context via Epic name field on Work Board cards
- **Click Epic name** on any card to navigate to Epic and see full progress

**Visual Organization:**
```
Work Board (Execution View) - Flat card layout
┌──────────────────────────────────────────────────────────────────────┐
│  Next In           │  In Progress       │  In review     │  ...     │
│                    │                    │                │          │
│  TM-503            │  TM-501            │  TM-502        │          │
│  Add validation    │  Add photo upload  │  Backend API   │          │
│  [Claims Intake]   │  [Claims Intake]   │  [Claims Intake]          │
│                    │                    │                │          │
│                    │  TM-702            │  TM-701        │          │
│                    │  Update deps       │  Fix date bug  │          │
│                    │  [no epic]         │  [no epic]     │          │
│                    │                    │                │          │
│                    │  TM-601            │                │          │
│                    │  Design quote      │                │          │
│                    │  [Multi-Car Quote] │                │          │
└──────────────────────────────────────────────────────────────────────┘

[Epic Name] = Epic name displayed on card for context
[no epic] = Standalone work (not linked to any Epic)
```

---

## 6. Bug Workflow: Using the Bug Board

See [Bug Management](bug-mgmt.md) for the full bug management process. This section covers how the Bug Board fits into the overall board setup.

### 6.1 Bug Board Purpose & Scope

One shared Bug Board for both teams. Product owners triage bugs here and decide what gets scheduled.

**Bug Board Filter:**
```
project = Insurances
AND issuetype = Bug
ORDER BY priority DESC, created ASC
```

**Columns:** To Do → Next In → Done / Declined

**Quick filters:**
- **"Bót"** → `Teymi = "Bót"`
- **"Ronja"** → `Teymi = "Ronja"`
- **"Untriaged"** → `priority is EMPTY`

### 6.2 How Bugs Flow

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

Once a bug reaches "Next In" it's visible on the team's Work Board and flows through the normal development columns.

### 6.3 Bug Board vs Epic/Work Boards

| Board | Shows bugs? |
|-------|-------------|
| Epic Board | No — excluded via `AND issuetype != Bug` in filter |
| Bug Board | Yes — all bugs, both teams |
| Work Board | Yes — bugs that have reached "Next In" |

---

*End of Configuration & Workflow Guide*
