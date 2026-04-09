# LB (Landsbankinn)

## Company Background

**Founded:** 1886
**Headquarters:** Reykjavik, Iceland
**Industry:** Banking and financial services
**Business lines:** Personal banking, corporate banking, insurance (via TM acquisition)
**Employees:** ~850 people

**Mission:** Traustur banki fyrir farsæla framtíð.

## Key People (relevant to Daði's work)

| Person | Role | Notes |
|--------|------|-------|
| Arinbjörn Ólafsson | VP of IT | |
| Óskar Sigurgeirsson (Óskar S) | Head of Software Solutions | Óli's boss |
| Snæbjörn Konráðsson | Head of Web Solutions (Vefdeild) | Owns customer-facing UI for bank customers. Wants broader ownership of Vefsala. |
| Þórunn Inga Ingjaldsdóttir | Head of Insurance Sales & Service (individuals) | Leads a small LB dept focused on sales and service of insurance for individuals. Some TM people moved to this dept. |
| Ólafur Þórðarson (Óli) | Engineering Lead, Tryggingalausnir | Owns the eng team that builds TM's digital products |

## Relevant Teams

**Tryggingalausnir** — Group within LB IT that develops and maintains TM's digital products (Bóthildur, Rósin, Vefsala, Heimdallur, etc.). This is the eng team Daði works with day to day. Two dev teams within Tryggingalausnir:

- **Bót** — Develops TM's digital claims services, most notably Bóthildur
- **Ronja** — Develops TM's digital insurance services, plus some shared services used by both claims and insurance

See [team.md](team.md) for detailed team composition and ways of working.

**Vefdeild** — Web Solutions group within LB IT (led by Snæbjörn). Responsible for customer-facing UI across the bank's digital channels. Adjacent to Tryggingalausnir — Vefdeild handles frontend/UI for bank customers while Tryggingalausnir handles insurance backend. For customer-facing insurance products (Vefsala, Mínar síður), this creates a split where UI and business logic are owned by different groups.

**Þórunn Inga's dept** — Small department within LB focused on insurance sales and service for individual customers. Some TM employees were moved here. Relationship to digital product ownership is still being defined.

## Digital Products & Systems (relevant to TM)

**Banking portal** — LB's web-based banking platform for customers.
**Mobile apps** — iOS and Android banking apps.
**Shared infrastructure** — Infrastructure shared between LB and TM systems.
**Shared services (APIs)** — APIs used across both LB and TM products.

## Relationship with TM

**Acquisition:** LB acquired TM in early spring 2025. TM remains a separate corporation under LB's control — the insurance business operates independently but gets certain services from LB, most notably software development and other IT services.

**Org structure overlap:**
- TM's digital products are built by the Tryggingalausnir group within LB IT (led by Óli), not by TM's own developers
- Product management sits at TM (Óskar Örn as CPO, Daði as PM), engineering sits at LB
- Óskar S (LB) → Óli (LB/Tryggingalausnir) → eng team that builds TM products

**Product ownership:**
- **TM-owned:** Bóthildur, Rósin, Heimdallur, Græna tryggingakerfið, Græna tjónakerfið
- **Transitioning to LB:** Vefsala, Mínar síður — originally developed by TM, now moving to LB ownership. Product ownership is fragmented across Óskar Örn (TM), Vefdeild (LB), Þórunn Inga's dept (LB), and Tryggingalausnir (LB). See `Projects/empowered-product-teams/a3-product-ownership.md` for analysis.
- **LB-owned (shared):** Banking portal, mobile apps, shared infra and APIs
