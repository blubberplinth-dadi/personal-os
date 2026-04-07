# Sjálfvirk móttaka tjónstilkynninga - skilgreining

# Greining

## Vandinn og tækifærið

Langflestar tjónstilkynningar til TM berast í tölvupósti og þær eru handvirkt unnar af starfsfólki - opnaðar, lesnar og afritaðar handvirkt inn í tjónakerfi. Þetta er mjög tímafrekt og losar starfsfólk ekki til raunverulegrar tjónaþjónustu.

- **Af hverju skiptir þetta máli:** ~15.000 af 20.000 tjónstilkynningum á ári eru handskráðar. Starfsfólk eyðir gífurlegum tíma í að afrita upplýsingar úr PDF-skjölum inn í tjónakerfið - ~500 klst/ár - í stað þess að sinna eiginlegri tjónaafgreiðslu.
- **Núverandi ferli:** Tilkynningar berast sem tölvupóstur, flokkast í möppur í MS Outlook. Starfsmaður opnar póstinn, les tilkynningu (oftast PDF-viðhengi), og afritar textasvæði handvirkt inn á rétta staði í tjónakerfið (Bóthildi eða Græna) þar til nægar upplýsingar eru komnar til að stofna gilt mál.
- **Þrjár aðalleiðir tilkynninga:** Langstærsti hluti tölvupóststilkynninga berst sem PDF-skjöl eftir þremur leiðum:
  1. **Ökutækjatjón frá Lögreglunni** - lögregluskýrslur
  2. **Ökutækjatjón frá arekstur.is** - tilkynningar frá Akstur & Öryggi
  3. **Tilkynningar af tm.is** - úr tjónstilkynningarferli TM sem byggir á Taktikal-eyðublöðum

**Tækifærið:** Sjálfvirkja móttöku þessara þriggja tegunda tilkynninga og búa til tjón í tjónakerfi sjálfkrafa þegar tilkynning hefur allar nauðsynlegar upplýsingar - og ákveða hvað gerist þegar hún hefur það ekki.

**Gögn og vísbendingar:**
  - ~20.000 tjón tilkynnt á ári
  - ~15.000 þeirra berast sem PDF í tölvupósti og eru handskráðar
  - Áætlaður sparnaður: ~500 klst/ár

### Dæmisögur

_TODO_

### Markmið og mælikvarðar

| # | Markmið | Mælikvarði | Núgildi | Markgildi |
|---|---------|------------|---------|-----------|
| 1 | Losa starfsfólk við handvirka skráningu tilkynninga | Klst/ár í handvirka skráningu | ~500 klst | Nálægt núlli |
| 2 | Sjálfvirkja móttöku tilkynninga | Hlutfall tilkynninga sem skráðar sjálfkrafa (af þremur leiðum) | 0% | _TODO_ |
| 3 | Færri villur í skráningu | Villutíðni í skráðum tjónum | _TODO_ | _TODO_ |

### Utan markmiða

1. **Aðrar tjónstilkynningar en þessar þrjár leiðir** - t.d. frjáls texti sendur á tjon@tm.is. Við sjálfvirkjum aðeins móttöku PDF-tilkynninga frá Lögreglunni, arekstur.is og tm.is (Taktikal).
2. **Sjálfsafgreiðsluferli fyrir tjónatilkynningar** - TM vill á lengri tíma gera tilkynningarferlið að sjálfsafgreiðslu, en það er mun stærra verkefni og utan umfangs hér.

## Lausnin

### Möguleg nálgun í grófum dráttum

Nota AI til að lesa PDF-viðhengi úr tölvupósti, draga út nauðsynlegar upplýsingar og stofna tjón sjálfkrafa í Bóthildi. Þrjár leiðir, þrjú mismunandi PDF-snið sem þarf að kunna á. Outlook innhólfið verður áfram staðurinn til að taka á móti tjónstilkynningum nema að í stað þess að fá email með PDF skjali þá kemur email með hlekk inn í Bóthildi (eða annað ef ekki tekst að búa til tjón).

**Leiðir 1 og 2 (Lögreglan og arekstur.is) - einfaldari:**
- Alltaf ökutækjatjón, svo tegund tryggingar er þekkt fyrirfram
- PDF-skjölin innihalda yfirleitt allar nauðsynlegar upplýsingar, þar á meðal kennitölu tilkynnanda
- Kerfið finnur ökutækjatryggingarskírteini hjá tilkynnanda og stofnar tjón út frá því

**Leið 3 (tm.is / Taktikal) - flóknari:**
- Getur verið um alls konar tegundir tjóna að ræða, ekki bara ökutækjatjón
- Getum notað sömu aðferð og í leið 1 og 2 að lesa pdf skjalið, sem inniheldur alltaf kennitölu og tegund tjóns.
- Einnig er hægt að nýta webhooks eins og í rúðutjónum, en þar berast upplýsingar sem json, með auðlesanlegum upplýsingum úr skjalinu.

**Lykilupplýsingar til að stofna tjón:**
1. Kennitala tilkynnanda
2. Við hvers konar tryggingu passar tjónstilkynningin

**Opin spurning:** Hvað gerist þegar tilkynning vantar upplýsingar eða kerfið er ekki nógu öruggt um lestur? Stofna ófullkomið tjón, setja í biðröð fyrir starfsmann, eða hafna?

### Mögulegir kerfishlutar

**Áfangi 1 - Leiðir 1 og 2 (Lögreglan og arekstur.is):**
1. **Tölvupóstlesari** - fylgist með tölvupóstmöppu/möppum og greinir tilkynningar frá Lögreglunni og arekstur.is
2. **PDF-lestur (AI)** - les PDF-viðhengi og dregur út nauðsynlegar upplýsingar (kennitala, ökutækjaupplýsingar, atvik, o.fl.)
3. **Sjálfvirk stofnun tjóns** - finnur ökutækjatryggingarskírteini tilkynnanda og stofnar tjón í Bóthildi
4. **Meðhöndlun óvissutilvika** - _TODO: ákveða hvað gerist þegar upplýsingar vantar eða lestur er óviss_

**Áfangi 2 - Leið 3 (tm.is / Taktikal):**
5. **Stuðningur við Taktikal-eyðublöð** - víkka PDF-lestur til að þekkja fjölbreyttari tjónategundir
6. **Tryggingavörpun** - kortleggja hvernig mismunandi tjónategundir úr Taktikal tengjast réttum tryggingum

### Notandasögur (titlar)

**Sjálfvirk móttaka (leiðir 1 og 2)**
1. Kerfið les PDF-tilkynningu frá Lögreglunni og dregur út lykilupplýsingar
2. Kerfið les PDF-tilkynningu frá arekstur.is og dregur út lykilupplýsingar
3. Kerfið finnur skírteini (ökutækjatrygging) tilkynnanda út frá kennitölu
4. Kerfið stofnar tjón sjálfkrafa þegar allar nauðsynlegar upplýsingar eru til staðar
5. Kerfið sendir tölvupóst á tjónafulltrúa með hlekk á nýstofnað tjón í Bóthildi
6. Kerfið sendir tölvupóst með upphaflegu PDF-tilkynningunni ef ekki tókst að stofna tjón

**Sjálfvirk móttaka (leið 3 - Taktikal)**
7. Kerfið les PDF-tilkynningu af tm.is og greinir tegund tjóns
8. Kerfið varpar tegund tjóns á rétta tryggingu og stofnar tjón


### Framtíðarmöguleikar

1. **Sjálfsafgreiðsluferli** - viðskiptavinir tilkynna tjón beint inn í kerfið án PDF-milliliðs
2. **Fleiri tilkynningaleiðir** - t.d. frjáls texti í tölvupósti, tilkynningar frá öðrum aðilum

## Tæknikröfur

_TODO_

## Tímalína og áfangar

_TODO_

## Áhættur og mótvægisaðgerðir

| Áhætta | Áhrif | Líkur | Mótvægisaðgerð |
|--------|-------|-------|----------------|
| | _TODO_ | | |
