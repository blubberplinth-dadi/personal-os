# Sjálfvirkar bréfasendingar og ítrekanir - skilgreining

# Greining

## Vandinn og tækifærið

Tjónafulltrúar senda mikinn fjölda bréfa og gagnabeiðna á ytri aðila (heilsugæslur, verkstæði, verktaka, o.fl.) sem hluta af tjónaafgreiðslu. Öll þessi samskipti eru handvirk - starfsfólk skrifar bréf, sendir í tölvupósti, og þarf sjálft að muna eftir að ítreka þegar svar berst ekki. Þetta er tímafrekt, leiðir oft til mistaka og ítrekanir gleymast reglulega.

- **Af hverju skiptir þetta máli:** ~600 klst/ár fara í handvirkar bréfasendingar og ítrekanir. Starfsfólk notar Outlook áminningar og eigin kerfi til að halda utan um hvað bíður svars, sem þýðir að þetta gleymist og ytri aðilar fá ekki ítrekanir á réttum tíma. Þetta hægir á tjónaafgreiðslu og getur tafið bótagreiðslur til tjónþola.
- **Núverandi ferli:** Tjónafulltrúi skrifar bréf (oft út frá sniðmáti í Word eða Outlook) og sendir á ytri aðila í tölvupósti. Hann setur sér áminningu í Outlook til að ítreka ef svar berst ekki. Þegar áminning kemur upp þarf hann að fara yfir stöðuna, skrifa ítrekunarbréf og senda aftur. Engin yfirsýn er til yfir hvaða bréf bíða svars á hverju sviði.
- **Tækifærið:** Sjálfvirkja sendingu algengustu bréfategunda beint úr Bóthildi og láta kerfið sjálfkrafa ítreka þegar svar berst ekki innan ákveðins tíma.

**Gögn og vísbendingar:**
  - Áætlaður sparnaður: ~600 klst/ár
  - _TODO: Fá tölur um fjölda bréfa á ári, sundurliðað eftir tegund_
  - _TODO: Fá lista yfir 5 algengustu bréfategundir og viðtakendur_
  - _TODO: Hversu oft gleymist ítrekun? Hver er meðalbiðtími eftir svari?_

### Dæmisögur

**Gagnabeiðni á heilsugæslu - allt gengur vel:** Sigga tjónafulltrúi í persónutjónum er að vinna að afgreiðslu slysatjóns. Hún þarf læknisvottorð frá heilsugæslustöðinni. Í dag skrifar hún bréf í Word, afritar inn upplýsingar um tjónþola og tjón, sendir bréfið í tölvupósti og setur sér reminder eftir 2 vikur. Ef heilsugæslan svarar er allt gott. Ef ekki þarf hún að senda ítrekunarbréf.

**Ítrekun gleymist:** Jón tjónafulltrúi sendi gagnabeiðni á verkstæði fyrir 3 vikum og setti sér Outlook-reminder. Hann var í fríi þegar áminningin kom upp og enginn tók við. Nú eru 5 vikur liðnar og tjónþolinn hringir og spyr af hverju ekkert hafi heyrst. Jón þarf að byrja upp á nýtt.

**Engin yfirsýn:** Björk forstöðumaður vill vita hversu mörg mál á eignatjónasviði bíða svars frá ytri aðilum. Enginn staður er til þar sem hægt sé að sjá þetta - hver tjónafulltrúi hefur sinn eigin hátt á slíkri eftirfylgni.

### Markmið og mælikvarðar

| # | Markmið | Mælikvarði | Núgildi | Markgildi |
|---|---------|------------|---------|-----------|
| 1 | Draga úr tíma í bréfaskrif og sendingar | Klst/ár í handvirkar bréfasendingar | ~600 klst | _TODO_ |
| 2 | Tryggja að ítrekanir gleymist ekki | Hlutfall gagnabeiðna sem fá ítrekun á réttum tíma | Óþekkt (ekkert mælt) | _TODO_ |
| 3 | Yfirsýn yfir bréf sem bíða svars | Hægt að sjá stöðu bréfa á sviði/teymi | Engin yfirsýn | Yfirsýn í Bóthildi |

### Utan markmiða

1. **Öll bréf og samskipti** - við sjálfvirkjum aðeins algengustu bréfategundir (líklega 5), ekki öll samskipti við ytri aðila.
2. **Sjálfvirkur lestur á svörum** - kerfið sjálfvirkir sendingu og ítrekanir, en les ekki sjálfkrafa svör sem berast. Starfsmaður skráir handvirkt að svar hafi borist.
3. **Breyting á samskiptaferli við ytri aðila** - við gerum ráð fyrir að samskiptin séu áfram í tölvupósti, ekki ný vefgátt eða annað viðmót.

## Lausnin

### Möguleg nálgun í grófum dráttum

Byggja bréfasendingavirkni inn í Bóthildi þar sem tjónafulltrúi velur bréfategund, kerfið fyllir sjálfkrafa inn upplýsingar úr tjóninu (nöfn, kennitölur, dagsetningar, o.fl.), og sendir bréfið á viðtakanda í tölvupósti. Kerfið heldur utan um hvaða bréf bíða svars og sendir sjálfkrafa ítrekunarbréf ef svar berst ekki innan ákveðins tíma.

**Aðrar leiðir sem skoðaðar:**
- _TODO: Var skoðað að nota tilbúinn hugbúnað (t.d. workflow-kerfi) frekar en að byggja inn í Bóthildi?_

### Mögulegir kerfishlutar

1. **Bréfasniðmát í Bóthildi** - sniðmát fyrir algengustu bréfategundir með breytum (e. placeholders) sem fyllast sjálfkrafa úr tjónagögnum (nafn tjónþola, kennitala, tjónsnúmer, dagsetningar, o.fl.)
2. **Sendingarvirkni** - starfsmaður velur sniðmát, forskoðar bréf, og sendir beint úr Bóthildi. Bréfið fer á tölvupóst viðtakanda.
3. **Ítrekunarkerfi** - kerfið fylgist með hvaða bréf bíða svars. Ef svar berst ekki innan ákveðins frests (stillanlegs eftir bréfategund) sendir kerfið sjálfkrafa ítrekunarbréf. Starfsmaður fær tilkynningu.
4. **Yfirsýn** - listi yfir öll bréf sem bíða svars, á tjóni, sviði, eða yfir allt.
5. **Skráning svars** - starfsmaður skráir að svar hafi borist, sem stöðvar ítrekunarferlið.

### Notandasögur (titlar)

**Bréfasending**
1. Starfsmaður velur bréfategund og viðtakanda á tjóni
2. Kerfið fyllir sjálfkrafa inn upplýsingar úr tjónagögnum í sniðmát
3. Starfsmaður forskoðar og breytir bréfi áður en sent er
4. Starfsmaður sendir bréf beint úr Bóthildi á tölvupóst viðtakanda
5. Bréfasending skráist sjálfkrafa á tímalínu tjóns

**Ítrekanir**
6. Kerfið sendir sjálfkrafa ítrekunarbréf þegar svar berst ekki innan ákveðins frests
7. Starfsmaður fær tilkynningu þegar ítrekun er send
8. Starfsmaður getur slökkt á sjálfvirkri ítrekun á tilteknu bréfi
9. Starfsmaður skráir að svar hafi borist og stöðvar ítrekunarferlið

**Yfirsýn**
10. Starfsmaður sér öll bréf sem bíða svars á sínu tjóni
11. Forstöðumaður sér öll bréf sem bíða svars á sviði eða yfir allt

### Framtíðarmöguleikar

1. **Sjálfvirkur lestur svara** - AI les innkominn tölvupóst og tengir svör sjálfkrafa við rétt tjón/bréf
2. **Fleiri bréfategundir** - bæta við sniðmátum eftir þörfum
3. **Stafræn samskiptagátt** - bjóða ytri aðilum upp á að svara í gegnum vefviðmót frekar en tölvupóst

## Hönnunarhugmyndir

_Engar enn._

## Tæknikröfur

_TODO_

## Tímalína og áfangar

_Bíður - vinna með teyminu eftir að hlið 2 greining er kláruð._

## Áhættur og mótvægisaðgerðir

| Áhætta | Áhrif | Líkur | Mótvægisaðgerð |
|--------|-------|-------|----------------|
| Sniðmát passa ekki við raunverulega þörf starfsfólks | Meðal | Meðal | Kortleggja algengustu bréfategundir með starfsfólki áður en sniðmát eru hönnuð |
| Ytri aðilar þekkja ekki sjálfvirk bréf sem lögmæt | Lág | Lág | Tryggja að bréf líti út eins og venjuleg TM-bréf, koma frá réttu netfangi |
| Ítrekanir verða of tíðar eða of ágengar | Meðal | Meðal | Stillanlegar ítrekunarreglur eftir tegund, starfsmaður getur slökkt á ítrekun |
| Tölvupóstsendingarkerfi - afkastageta og áreiðanleiki | Meðal | Lág | Skoða innviði snemma, tryggja að sendingar berist rétt og rekjanlega |
