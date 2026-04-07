# Sjálfvirk enduráætlun tjóna - skilgreining

# Greining

## Vandinn og tækifærið

Starfsmenn tjónaþjónustu þurfa að fara handvirkt yfir áætlanir allra opinna tjóna (~10.000 á hverjum tíma) til að tryggja að tjónaskuld TM sé rétt metin. Þetta er svo tímafrek handavinna (~325 klst í hvert skipti) að það gerist aðeins 4x á ári.

- **Af hverju þetta skiptir máli fyrir TM:** Tjónaskuld er ein mikilvægasta stærð í bókhaldi tryggingafélags. Starfsmenn eyða ~1.300 klst/ári í þessa handavinnu í stað raunverulegrar tjónaþjónustu.
- **Núverandi ferli:** ~4x á ári hittast nokkrir starfsmenn til að fara yfir öll opin tjón og uppfæra áætlanir. Hver athugun tekur ~2 mín (opna tjón, skoða stöðu, meta hvort áætlun standist, breyta ef þarf).
- **Tækifærið:** Sjálfvirkja uppfærslu áætlana til að losa starfsmenn við handavinnu.

**Gögn og vísbendingar:**
  - ~10.000 opin tjón á hverjum tíma
  - ~40.000–80.000 handvirkar athuganir á ári
  - Áætlanir uppfærðar aðeins 4x/ár vegna tímaskorts
  - ~2 mín per athugun

### Dæmisögur

**Algeng athugun:** Sigga tjónafulltrúi opnar tjón 4521001 í ársfjórðungslegri endurskoðun í mars. Tjónið var stofnað í janúar með áætlun upp á 450.000 kr í viðgerð. Síðan þá hefur reikningur komið frá verkstæði upp á 380.000 kr og varahlutareikningur upp á 95.000 kr. Sigga sér að raunkostnaður er þegar kominn yfir áætlun og uppfærir hana. Þetta tók 2 mínútur - margfaldað með þúsundum tjóna.

**Jaðardæmi:** Tjón sem hefur legið án hreyfingar í 8 mánuði - er áætlunin enn raunhæf eða á að lækka hana? Starfsmaður þarf að leggja mat á.

### Markmið og mælikvarðar

| # | Markmið | Mælikvarði | Núgildi | Markgildi |
|---|---------|------------|---------|-----------|
| 1 | Losa starfsmenn við handvirka endurskoðun | Klst/ár í handvirka endurskoðun | ~1.300 klst | ~300 klst (80% sjálfvirkni) |
| 2 | Starfsmenn treysta sjálfvirkninni | Upplifun starfsfólks | — | Treysta að áætlanir séu réttar |

### Utan markmiða

1. **Við ætlum ekki að breyta því hvernig tjónsáætlanir eru gerðar** - við sjálfvirkjum uppfærsluna, ekki skipulag áætlana
2. **Við ætlum ekki að spá fyrir um kostnað nýrra tjóna** - þetta snýst um að uppfæra áætlanir á opnum tjónum, ekki að búa til fyrstu áætlun sjálfkrafa
3. **Við ætlum ekki að byggja AI-líkan í fyrstu útgáfu** - byrjum á forrituðum reiknireglum

## Lausnin

### Möguleg nálgun í grófum dráttum

Forrita þær reiknireglur sem starfsmenn nota í dag til að meta hvort uppfæra þurfi tjónsáætlun, og láta kerfið keyra þær sjálfkrafa á reglulegri tíðni á öllum opnum tjónum. Í fyrstu myndi kerfið uppfæra áætlanir sjálfkrafa sem “gerviáætlanir”. Þannig gætum við svo greint nákvæmni gerviáætlunar vs. raunáætlunar og þegar nákvæmni væri orðin ásættanleg, yrði kerfinu breytt í að uppfæra raunáætlun.

**Líkleg nálgun:** Forritaðar reiknireglur fremur en AI-líkan. Þarf að kortleggja nákvæmlega hvaða reglur starfsmenn nota (t.d. "ef tjón hefur verið opið í X mánuði án hreyfingar, lækka áætlun um Y%", "ef reikningur berst sem er hærri en áætlun, hækka áætlun", o.s.frv.).

**Opin spurning:** Þarf eftirlitsviðmót þar sem starfsmenn geta fylgst með að sjálfvirknin sé að virka rétt? T.d. yfirlit yfir hvaða áætlanir breyttust, hversu mikið, og hvers vegna - svo hægt sé að grípa inn í ef reglurnar skila röngum niðurstöðum.

**Hverju var velt upp:** AI-líkan sem spáir fyrir um kostnað út frá sögulegum gögnum. Talið er líklegra að hægt sé að leysa þetta með reiknireglum, sem er einfaldara og gagnsærra.

### Mögulegir kerfishlutar

1. **Reikniregluvél** - kjarni lausnarinnar sem keyrir reglurnar á öllum opnum tjónum
2. **Regluleg keyrsla enduráætlunar** - stilla hversu oft reglurnar keyra (daglega/vikulega)
3. **Eftirlitsviðmót** - yfirlit fyrir starfsmenn yfir hvaða áætlanir breyttust, hversu mikið og hvers vegna

### Notandasögur (titlar)

**Sjálfvirk enduráætlun**
1. Kerfið keyrir reiknireglur á öllum opnum tjónum á ákveðinni tíðni
2. Kerfið uppfærir tjónsáætlun sjálfkrafa þegar regla segir til um breytingu
3. Kerfið skráir ástæðu breytingar (hvaða regla olli henni)

**Eftirlit og yfirferð**
4. Starfsmaður sér yfirlit yfir allar áætlanir sem þarf handvirka enduráætlun
5. Starfsmaður sér hversu mikið áætlun breyttist og hvaða regla olli breytingunni
6. Starfsmaður getur handvirkt hnekkt sjálfvirkri breytingu á áætlun

**Uppsetning og reglustjórnun**
7. Kerfið styður mismunandi reiknireglur eftir tegund tjóns
8. Stjórnandi getur breytt tíðni keyrslu og þröskuldgildum reglna

### Framtíðarmöguleikar

1. **AI-líkan** - nota söguleg gögn til að spá betur fyrir um kostnað, ef reiknireglur reynast ófullnægjandi
2. **Sjálfvirk fyrsta áætlun** - búa til áætlun sjálfkrafa þegar nýtt tjón er stofnað (utan scope núna, sjá utan markmiða)

## Tæknikröfur

Nota reiknireglur sem starfsmenn tjónaþjónustu eru að taka saman (sjá PDF frá Elínborgu)

## Tímalína og áfangar

_Bíður - vinna með teyminu eftir að hlið 2 greining er kláruð._

## Áhættur og mótvægisaðgerðir

| Áhætta | Áhrif | Líkur | Mótvægisaðgerð |
|--------|-------|-------|----------------|
| Reiknireglur ná ekki að endurspegla mat starfsmanna | Há | Meðal | Kortleggja reglur vandlega með starfsfólki, prófa á sögulegum gögnum |
| Starfsmenn treysta ekki sjálfvirkninni | Meðal | Meðal | Eftirlitsviðmót, smám saman innleiðing |
| Reiknireglur eru of einfaldar fyrir flókin tjón | Meðal | Meðal | Skilgreina hvaða tjónategundir fá sjálfvirka uppfærslu vs. handvirka |
