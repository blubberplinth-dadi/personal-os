# Færa tryggingar í Rósina 2.0

**Pillar:** Vörustjórnun í tryggingaþjónustu (Ronja)
**Status:** Proposal phase — needs quantified business case before executive decision
**Started:** 2026-01
**Last updated:** 2026-01

---

## Lýsing

Migrate insurance types still managed in legacy AS/400 (Græna) to Rósin while modernizing the UI framework from Angular 1.8 to React.js.

### Three converging challenges
1. Some insurance types still require Græna — staff must work in both systems (~60+ min/day lost)
2. Only 1-2 developers can maintain Græna and they're nearing retirement
3. Rósin's Angular 1.8 frontend is unsupported since 2022 — security risk

## Key Artifacts

- `tryggingar-i-rosina-2-0-IS.md` — Full proposal in Icelandic
- `exec-agent-review.md` — Executive review feedback (readiness score: 6/10)

## Exec Review Summary

Strong foundation but needs quantification before it can support a decision:
- Missing: cost estimates, specific insurance types, CVE-based security case, success criteria
- Recommendation: phased approach (Phase 0 Discovery → Phase 1 PoC → Incremental)
- Timing is good post-LB acquisition

## Næstu skref

- Quantify business case (survey advisors for time lost)
- List specific insurance types to migrate
- Build security case with CVE references
- Add cost estimates
- Frame decision as phased discovery first

## Lykilaðilar

- Óskar Örn, Óli (decision makers)
- Ronja teymið (execution)

## Tengdir fundir

-

## Ákvarðanir

-

## Tengd skjöl

- [[TM]] — Rósin product description, tech stack
