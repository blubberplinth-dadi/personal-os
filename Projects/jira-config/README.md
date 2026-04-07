# JIRA Configuration for TM

**Pillar:** Vistkerfið
**Status:** Active — Documentation and configuration
**Started:** 2026-01
**Last updated:** 2026-01

---

## Lýsing

Design and document JIRA configuration and workflows for TM's software development teams. Covers issue types, workflows, components, boards, and navigation across multiple products (Vefsala, Bóthildur, Rósin) and teams (Bót, Ronja).

## Key Artifacts

- `config-and-workflow.md` — **Authoritative** JIRA configuration and workflow guide (single source of truth)
- `standards.md` — Epic governance, management board configurations, naming conventions
- `notendahandbok.md` — User handbook in Icelandic (task-oriented quick reference)
- `bug-mgmt.md` — Bug management process (triage, priorities, bug budget)
- `presentations/jira-kynning.md` — Slide drafts for JIRA intro to Bót and Ronja
- `presentations/jira-kynning.pptx` — The presentation itself

## Research

Explorations and proposals in `research/`:
- `status-separation-proposal.md` — Proposals for separating statuses between boards (Proposal B chosen: LB corporate set)
- `jira-in-app-updates-ideas.md` — How to replicate Asana Inbox-like updates in JIRA
- `multi-epics-as-project-ideas.md` — Structuring multi-Epic projects
- `query-tests-to-show-sub-tasks.md` — JQL experiments

## Documentation Principles

- `config-and-workflow.md` is the single authoritative source for rules and workflow — update it there, nowhere else
- `notendahandbok.md` is task-oriented only — links to config for rules, never restates them
- New content goes into an appropriate existing file; don't create new files without good reason

## Lykilaðilar

- Daði (configuration design)
- Óli (approval, team management)
- Bót og Ronja teymi (users)

## Tengdir fundir

-

## Ákvarðanir

- Proposal B chosen for status separation (LB corporate status set)
- Custom "Teymi" field (Bót/Ronja single-select dropdown, required on all issues)

## Tengd skjöl

- [[TM]] — Team structure and products
