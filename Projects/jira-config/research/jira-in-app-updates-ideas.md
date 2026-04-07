# JIRA In-App Updates (Asana Inbox equivalent)

How to get automatic, relevant updates about work in JIRA — in one place, without email.

## The problem

Asana's Inbox centralizes all relevant notifications in-app: mentions, assignments, status changes, comments on followed tasks. JIRA's default is email notifications, which is noisy and scattered. How do we get closer to Asana's Inbox experience within JIRA?

## Important constraint: JIRA Data Center

TM runs JIRA Data Center (v10.3.15), not JIRA Cloud. Data Center does **not** have the bell icon / Notification Center that Cloud has. The main in-app awareness tool on Data Center is the **Dashboard with gadgets**.

## Recommended approach

**The Dashboard is the primary tool.** Each person sets their JIRA home page to a well-configured dashboard. This becomes their daily starting point — the closest thing to Asana's Inbox available on Data Center.

### Layer 1: Personal dashboard — start here

Each person creates (or is given) a personal dashboard with these gadgets:

| Gadget | What it shows |
|--------|---------------|
| **Activity Stream** | Recent changes on projects/issues you care about — comments, status changes, new issues |
| **Assigned to Me** | Your current assignments across all projects |
| **Watched Issues** | Issues you're watching but not assigned to |
| **Filter Results: In Progress** | Custom filter showing work in progress on your team |

**Setup:**
1. Go to **Dashboard** (from the "My JIRA Home" menu)
2. The System Dashboard is a shared default that can't be edited — click **Copy Dashboard** to create your own
3. Name it something like "Mitt dashboard" or your name
4. Add/remove gadgets to fit your role
5. Configure the Activity Stream to filter by relevant projects (Bót's project, Ronja's project, or both)
6. Set it as your home via **Profile → My JIRA Home → My Dashboard**

**Alternative — admin creates a template:**
An admin (Óli or another) could create a shared dashboard with good defaults and set it as the starting point for everyone. Then individuals copy *that* instead of the bare System Dashboard. This saves each person from configuring from scratch.

**Watching strategy (still relevant):**
- Watch the Epics for your project → activity on child stories appears in your Activity Stream
- Watch issues you're a stakeholder on but not assigned to
- Óskar and Óli would watch all Epics across both teams

### Layer 2: Shared team dashboards — for team-level awareness

Create a shared dashboard per team (one for Bót, one for Ronja):
- **Activity Stream** — filtered to the team's project(s)
- **Filter Results: In Progress** — what's actively being worked on
- **Filter Results: Recently Resolved** — what just got done

Optionally, a shared STM dashboard for cross-team visibility.

**When to add this:** When Óskar, Óli, or other stakeholders want a team-level view without configuring their own dashboard.

### Team agreements needed

- Use @mentions in comments when you want someone's attention
- Update issue status and leave comments in JIRA (not only in email/phone) so the Activity Stream captures the activity
- Check your dashboard at the start of the day

## Limitations vs Asana Inbox

- Activity Stream is read-only — can't act on items directly from it
- No "unread" state or "mark as done" on individual updates
- Watching is manual — people need to remember to watch relevant issues
- Dashboard must be actively visited — there are no push notifications in-app on Data Center
- Less personal than Asana's Inbox: Activity Stream shows all activity on watched projects, not just things directed at you

## Verification

- After setup, have one person make a change to a watched issue and confirm it appears in others' Activity Stream
- Check that the Activity Stream filter is scoped correctly (not too noisy, not too narrow)
- Review after a sprint: is the dashboard useful as a daily starting point?
