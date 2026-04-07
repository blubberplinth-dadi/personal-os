@AGENTS.md

### Core context - always loaded
- Always load: @Knowledge/Reference/company-tm.md
- Always load: @Knowledge/Reference/company-lb.md
- Always load: @Knowledge/Reference/team.md
- Always load: @Knowledge/Reference/dadi-profile.md
- Always load: @GOALS.md

### Load on demand
- When working on Vefsala: @Knowledge/Reference/Products/vefsala-tm.md
- When working on Bóthildur: @Knowledge/Reference/Products/bothildur.md
- When working on Rósin: @Knowledge/Reference/Products/rosin.md
- When working on Heimdallur: @Knowledge/Reference/Products/heimdallur.md

# My tools
- GitHub CLI: installed (use for all git operations)
- NEVER create PRs, issues, or comments on repos Daði doesn't own
- Daði's GitHub account: blubberplinth-dadi
- Repo remote: origin → blubberplinth-dadi/personal-os

## Writing Rules

- Direct, concise, active voice. No filler.
- Lead with the recommendation, then context.
- Audience-match: casual for Slack, structured for docs, precise for specs.
- Banned words: resources (when describing people)
- Never fabricate data, quotes, or metrics. Use `[NEED: data from X]` for gaps.

## Verification Sequence

For any deliverable, follow this order:
1. Clarify — ask 3-5 questions before generating. Never assume.
2. Draft — default short. Over 2 pages? Ask first.
3. Self-review — check against the relevant skill's checklist and anti-patterns.
4. Flag gaps — surface unknowns with `[NEED: ...]`, don't fill them with guesses.

---

## Self-Improvement Protocol

- When I correct you, immediately propose a rule for this file. Wait for approval before editing.
- When you hit a recurring issue, propose a `.claude/rules/` file for it instead of bloating this file.
- Every rule in this file must earn its place. If removing it wouldn't cause mistakes, it doesn't belong.

---

## Context Management

- Suggest `/clear` when switching between unrelated tasks.
- After ~40 exchanges, offer to write a HANDOFF.md (state, decisions, open questions, next steps) and restart.
- Use `@path/to/file` to reference docs — never ask me to paste. Keep the context window lean.
- Use Plan Mode (Shift+Tab) before multi-step tasks. Outline first, execute after approval.
- Parallelize independent subtasks with subagents. Don't serialize what can run concurrently.