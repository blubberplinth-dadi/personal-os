# Heimdallur v2

**Pillar:** Vörustjórnun í tryggingaþjónustu (Ronja)
**Status:** Active
**Started:** 2026-01-29
**Team:** STM undirteymi (Daði + hluti af Ronja)

---

## Sýn

Skýrari sýn og skilgreining fyrir aðgangsstýringarkerfi TM — þróa Heimdall í að sjá algjörlega um aðgangs- og heimildastýringu fyrir öll tryggingakerfi TM, án legacy kerfa.

Einn staður fyrir alla umsjón með aðgangi og heimildum. Einfalt fyrir notendaþjónustu, skýrt fyrir yfirmenn, öruggt fyrir endurskoðendur.

### Núverandi staða (v1)
- Gott í að skilgreina hlutverk, notendur, heimildir
- Krefst tæknilegarar færni af notendum til að vinna auðveldlega í kerfinu

### Tæknilegt gap
- Mörg tryggingakerfi nota ekki enn Heimdall fyrir aðgangsstýringu
- Þar til þau gera er Heimdallur ekki eini staðurinn til að stýra aðgangi

### Ný krafa frá endurskoðendum
- Forstöðumenn deilda þurfa að flétta upp starfsmönnum sinna deilda
- Sjá hverjir hafa aðgang og hvaða heimildir í tryggingakerfunum

### Tengd kerfi
Bóthildur, Rósin, Vefsala, Græna, og öll önnur tryggingakerfi TM

## Notendahópar

- **Nonni í notendaþjónustu** — veitir og fjarlægir aðgang, stofnar hlutverk
- **Stefanía stjórnandi** — yfirsýn yfir aðgang starfsfólks, kröfur endurskoðenda
- **Finnur forritari** — tengir kerfi við Heimdall
- **Aðgangsstjóri / heimildaarkitekt** — hannar hlutverkastrúktúr (opin spurning: hver gerir þetta í dag?)

## Viðskiptaleg markmið

### Útkoma 1: Auka % þar sem aðgangsstýring fer fram í Heimdalli
| Áfangi | Lýsing |
|--------|--------|
| a | Sjálfvirk stofnun í legacy kerfum |
| b | **Nútímakerfi í Heimdall** — öll aðgangsstýring monorepo-kerfa komin í Heimdall |
| c | Grænu kerfin í Heimdall |
| d | Fjárhæða-/afsláttaheimildir útgáfukerfa í Heimdall |

### Útkoma 2: Auka % þar sem eftirlit með aðgangi fer fram í Heimdalli
_Áfangar ekki skilgreindir enn._

## Staðan á áfanga b

Fríða kortlagði alla staði í monorepo þar sem gömul aðgangsstýring er notuð. Niðurstaða:
- 60 hópar í gamla kerfinu, 820 notenda-hópa tengsl
- 44 einstakar aðgerðir
- Mest notaðar: TRG.G (22 hópar), TRG.U (16), TRG.F (15)

### Epics í áfanga b (Leið A: eftir þjónustu)
1. **dragon-core** — ~20+ sögur, stærsta verkefnið
2. **policyhub-service** — fylla í eyður + fjarlægja gamla
3. **rosin** — eigin kóði + dragon-core hreinsun (6 sögur skilgreindar)
4. **Smærri þjónustur** — ~9 einfaldar þjónustur (sögur tilbúnar, CSV til Jira-innflutnings)
5. **user-client + user-service** — hreinsun, próf (3 sögur skilgreindar, CSV tilbúið)

### Opin atriði
- Utanaðkomandi notendur í hópum (SPATIL: 15, TOYOTA: 13) — eiga þeir hlutverk í Heimdalli?
- UPPFOR1 (18 aðgerðir) — eitt breitt hlutverk eða sundurliðað?
- Tímasetning yfirfærslu: samhliða keyrsla eða hörð skipting per sögu?
- endurnyjun-service þarf rannsókn

## Rannsóknir

Ítarleg rannsókn á aðgangsstýringarlíkönum (Keycloak, AWS IAM, Casbin, OPA) lokið. Lykilinnsýn:
- Role explosion: ABAC og/eða hlutverkastigveldi er lausnin
- Governance: hybrid model (central team setur reglur, teymi vinna innan þeirra)
- Þarf sérstakan notendahóp til að hanna hlutverkastrúktúrinn (innsýn frá Óla)

Sjá nánar: `06-Resources/Learnings/Heimdallur/`

## Lykilaðilar

- Daði (vörustjóri)
- Fríða (greining á gömlum aðgangsheimildum)
- Óli (innsýn um hlutverkastrúktúr)
- Ronja teymið

## Tengdir fundir

-

## Ákvarðanir

- Leið A valin: skipuleggja epics eftir þjónustu (ekki eftir aðgerðartegund)
- Sögusnið samþykkt: 5 skref (aðgerð í kóða → heimild í Heimdalli → notendur → fjarlægja gamla → prófa)
