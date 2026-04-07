# Multi-Epic Projects in JIRA

How to structure a project that spans multiple Epics with 1-3 month milestones.

## The problem

JIRA does not allow Epics to contain other Epics. Each Epic can only contain Stories, Tasks, and Bugs. So when a project is bigger than a single Epic, we need another way to group related Epics together.

## Two main options

### Option 1: Initiatives (parent level above Epic)

JIRA supports a hierarchy level above Epics, often called Initiatives. If available, this is the cleanest solution — purpose-built for this exact problem.

```
Initiative: "Project X"
  ├── Epic: "Milestone 1 – [description]"
  ├── Epic: "Milestone 2 – [description]"
  └── Epic: "Milestone 3 – [description]"
```

**Requires:** Advanced Roadmaps / JIRA Plans (Premium tier on Cloud, or the Advanced Roadmaps add-on on Data Center). Worth checking whether LB already has the license.

### Option 2: Labels + naming convention

Works with any JIRA tier, no configuration changes needed.

1. Create a **label** for the project (e.g. `heimdallur-notandastjornun`)
2. Apply the label to all Epics belonging to the project
3. **Link the Epics** to each other using issue links ("is related to" or "blocks")
4. Create a **saved JQL filter** to see the full project: `labels = "heimdallur-notandastjornun" ORDER BY rank ASC`
5. Add a **quick filter** on the team's board so they can toggle to see only this project's Epics

## Example: Option 2 applied

**Project:** Heimdallur - einn staður til að stýra notanda
**Label:** `heimdallur-notandastjornun`

| Epic name | Label |
|-----------|-------|
| [Heimdallur] Notandi stofnast sjálfkrafa í legacy kerfum | `heimdallur-notandastjornun` |
| [Heimdallur] Öll aðgangsstýring nútímakerfa í Heimdall | `heimdallur-notandastjornun` |
| [Heimdallur] Öll aðgangsstýring Grænna kerfa í Heimdall | `heimdallur-notandastjornun` |

The `[Heimdallur]` prefix is optional — the label carries the project association. The prefix adds context when Epics appear outside the board (notifications, search results, linked issues). Without the prefix, Epic names are cleaner on the board itself.

## Recommendation

1. Check if Initiatives are available in our JIRA instance. If yes, use Option 1.
2. If not, use Option 2 (labels + naming). It covers 90% of the need with zero configuration.
