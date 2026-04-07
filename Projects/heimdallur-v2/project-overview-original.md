# Project Heimdallur v2

## Goal
Skýrari sýn og skilgreining fyrir aðgangsstýringarkerfi TM (Heimdallur) og vel skilgreint verkefni um að þróa Heimdall í að sjá algjörlega um aðgangs- og heimildastýringu fyrir öll tryggingakerfi TM, án legacy kerfa.

## Context
**Núverandi staða Heimdallar (v1):**
- Gott í að skilgreina hlutverk, notendur, heimildir o.s.frv.
- Krefst tæknilegarar færni af notendum til að vinna auðveldlega í kerfinu

**Ný krafa frá endurskoðendum:**
- Forstöðumenn deilda þurfa að geta flett upp starfsmönnum sinna deilda
- Sjá hverjir hafa aðgang og hvaða heimildir í tryggingakerfunum
- Þetta er krafa á yfirmenn frá endurskoðendum TM

**Tæknilegt gap:**
- Mörg tryggingakerfi nota ekki enn Heimdall fyrir aðgangsstýringu
- Þarf að uppfæra þessi kerfi yfir í að nota Heimdall
- Þar til það gerist er Heimdallur ekki eini staðurinn til að stýra aðgangi

**Role explosion vandamálið:**
- Hvert frávik í aðgangsréttindum krefst nýs hlutverks
- Dæmi: `tjonaFulltrui` (skoða) → `tjonaFulltruiEdit` (skoða + breyta) → `tjonaFulltruiHighApproval` (skoða + breyta + samþykkja ≥10M)
- Helst ætti starfsmaður að hafa eitt hlutverk, en núverandi kerfi leyfir ekki það

## Möguleg vandamálalausn

Rannsókn á öðrum aðgangsstýringarkerfum (Keycloak, AWS IAM, Casbin, OPA) sýndi tvær leiðir:

| Lausn | Lýsing |
|-------|--------|
| **Hlutverkastigveldi** | Hlutverk erfa frá öðrum hlutverkum. Eitt hlutverk á starfsmann. |
| **ABAC (eigindamiðað)** | Heimildir hafa skilyrði byggð á eigindum notanda (t.d. `approvalLimit = 10M`) |

**Sjá nánar:** `research/role-explosion-problem.md`

## User personas

### Nonni í notendaþjónustu
Aðal notendaaðgerðir:
1. Veita nýjum starfsmanni réttan aðgang og heimildir í tryggingakerfum TM
2. Fjarlægja aðgang og heimildir þegar starfsmaður hættir
3. Uppfæra aðgang og heimildir núverandi starfsmanns
4. Stofna og uppfæra Hlutverk (samanstanda af einni eða fleiri Heimildum)
5. Stofna og uppfæra Heimild (samanstendur af einni eða fleiri Aðgerð)

### Stefanía stjórnandi
Aðal notendaaðgerðir:
1. Skoða aðgang starfsfólks sinnar deildar
2. Skoða heimildir ákveðins starfsmanns
3. _(meira kemur seinna)_

### Finnur forritari
Aðal notendaaðgerðir:
1. Tengja kerfi við Heimdall (API, kóði)
2. Skilgreina / uppfæra heimildir kerfis
3. _(meira kemur seinna)_

## Status
- **Current phase**: Research / problem definition
- **Last updated**: 2026-01-30

## Key decisions
_Engar ákvarðanir enn teknar_

## Research
- `research/access-control-models.md` - Rannsókn á Keycloak, AWS IAM, Casbin, OPA
- `research/role-explosion-problem.md` - Greining á role explosion og mögulegum lausnum
- `story-map.yaml` - Uppbygging Heimdallur v1 (úr Miro)
- `elevator-pitch-v1.md` - Elevator pitch fyrir v1

## Related
- Tengist öllum tryggingakerfum TM (Bóthildur, Rósin, Vefsala, Græna...)
- Sjá einnig: `company-context/products/heimdallur.md`
