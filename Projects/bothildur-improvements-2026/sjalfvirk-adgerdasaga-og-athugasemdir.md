# Sjálfvirk aðgerðasaga og athugasemdir - skilgreining

# Greining

## Vandinn og tækifærið

Tjónafulltrúar skrá athugasemdir um vinnslu tjónamáls og um ákveðnar aðgerðir sem búið er að framkvæma í Memo-kerfið - gamalt sjálfstætt Windows-kerfi. Bóthildur er þegar að logga það sjálfkrafa þegar þessar aðgerðir eru framkvæmdar. Þetta er því tvöföld vinna sem eyðir tíma.

- **Af hverju þetta skiptir máli:** ~10.000 óþarfa handvirkar skráningar á ári. Starfsfólk eyðir ~300 klst/ári í að skrá upplýsingar sem kerfið á þegar.
- **Núverandi ferli:** Þegar tjónafulltrúi opnar tjón í Bóthildi eða Græna opnast Memo-kerfið sjálfkrafa (með hjálp Snara) og sýnir athugasemdir viðkomandi tjóns. Memo er miðstöð fyrir allt activity á tjóni og öllum málum tjónþolanna. Tjónafulltrúar skrifa þar handvirkt niður hvað þeir gerðu (t.d. "greiddi reikning", "sendi bréf á heilsugæslu"), jafnvel þótt Bóthildur loggi sömu aðgerð sjálfkrafa í aðgerðasögu.
- **Tækifærið:** Færa athugasemdavirkni inn í Bóthildi og sameina hana aðgerðasögu kerfisins, svo starfsfólk hafi einn stað fyrir allt activity á tjóni - bæði sjálfvirkar aðgerðir og handvirkar athugasemdir.

**Gögn og vísbendingar:**
  - ~10.000 handvirkar skráningar á ári um aðgerðir sem þegar er verið að logga sjálfkrafa
  - Áætlaður vinnusparnaður: ~300 klst/ár
  - Memo-kerfið er gamalt native Windows forrit

### Dæmisögur

**Algeng tvöföld skráning:** Jón tjónafulltrúi greiðir reikning frá verkstæði í Bóthildi. Bóthildur skráir greiðsluna sjálfkrafa í aðgerðasögu tjónsins. Jón hoppar svo yfir í Memo-kerfið og skrifar "Greiddur reikningur frá Bílverkstæði Suðurnesja, 380.000 kr." Sömu upplýsingar eru nú á tveimur stöðum.

**Athugasemd sem bætir við:** Sigga tjónafulltrúi hringir í tjónþola til að fá frekari upplýsingar um atvikið. Hún skrifar í Memo: "Talaði við Gunnar, hann segir að ökumaður hins bílsins hafi verið á rangri akrein. Bíður eftir lögregluskýrslu." Þetta eru nýjar upplýsingar sem Bóthildur getur ekki loggað sjálfkrafa - hér bætir Memo raunverulegu gildi við.

**Memo ræsist ekki:** Anna tjónafulltrúi opnar tjón í Bóthildi en Memo-kerfið ræsist ekki (Snari ekki virkur). Hún þarf að ræsa það handvirkt, finna rétt tjón, og vonast til að samstarfsmaður sem var síðast með tjónið hafi skráð stöðuna. Þetta er tímasóun og skapar óvissu.

### Markmið og mælikvarðar

| # | Markmið | Mælikvarði | Núgildi | Markgildi |
|---|---------|------------|---------|-----------|
| 1 | Fjarlægja tvöfalda skráningu | Klst/ár í handvirkar skráningar sem kerfið loggaði þegar | ~300 klst | Nálægt núlli |
| 2 | Einn staður fyrir allt activity á tjóni | Fjöldi kerfa sem starfsmaður þarf að skoða til að sjá activity | 2 (Bóthildur + Memo) | 1 (Bóthildur) |
| 3 | Starfsfólk missi ekki af virkni | Allar athugasemdir aðgengilegar í Bóthildi | — | Söguleg og ný Memo-gögn sýnileg |

### Utan markmiða

1. **Breyta því hvernig aðgerðasaga virkar í Bóthildi** - aðgerðasagan heldur áfram að logga sjálfkrafa eins og áður, við bætum athugasemdavirkni við hana.
2. **Flytja gögn úr Memo í gagnagrunn Bóthildar** - í fyrstu útgáfu sækjum við Memo-gögn í gegnum API Memo-kerfisins. Gagnaflutningur kemur til greina seinna þegar Memo-kerfið verður lagt niður.
3. **Leggja niður Memo-kerfið** - önnur svið TM nota Memo í öðrum tilgangi. Hér er einungis verið að útleiða notkun þess hjá tjónaþjónustu.

## Lausnin

### Möguleg nálgun í grófum dráttum

Byggja athugasemdavirkni inn í Bóthildi sem sameinast aðgerðasögu kerfisins. Starfsmaður sér eina tímalínu á tjóni þar sem sjálfvirkar aðgerðir (greiðslur, stöðubreytingar, o.fl.) og handvirkar athugasemdir birtast saman í tímaröð.

Í fyrstu útgáfu tengist Bóthildur Memo-kerfinu í gegnum API - sækir söguleg gögn og skrifar nýjar athugasemdir. Þannig þarf ekkert að flytja gögn og Memo-kerfið heldur áfram að virka fyrir önnur svið TM. Tjónaþjónusta hættir smám saman að nota Memo-gluggann beint og notar Bóthildi í staðinn.

**Lykilhugmynd:** Sameinuð tímalína - ekki tveir aðskildir listar (aðgerðir vs. athugasemdir) heldur einn straumur þar sem allt activity birtist saman.

### Mögulegir kerfishlutar

1. **Athugasemdavirkni í Bóthildi** - starfsfólk getur skrifað frjálsar athugasemdir á tjón og mál, beint í Bóthildi. Nýjar athugasemdir eru skrifaðar í Memo í gegnum API svo gögnin séu áfram í Memo-kerfinu.
2. **Sameinuð tímalína** - sjálfvirkar aðgerðir úr Bóthildi og athugasemdir úr Memo (sóttar í gegnum API) birtast saman í tímaröð á tjóni
3. **Memo API-tenging** - samþætting við Memo-kerfið til að lesa söguleg gögn og skrifa nýjar athugasemdir

### Notandasögur (titlar)

**Athugasemdir**
1. Starfsmaður skrifar athugasemd á tjón beint í Bóthildi
2. Starfsmaður skrifar athugasemd á mál beint í Bóthildi
3. Athugasemd er sjálfkrafa vistuð í Memo í gegnum API

**Sameinuð tímalína**
4. Starfsmaður sér allt activity á tjóni á einni tímalínu (sjálfvirkar aðgerðir + athugasemdir)
5. Söguleg Memo-gögn birtast á tímalínunni
6. Starfsmaður getur síað tímalínu eftir tegund (aðgerðir, athugasemdir, eða allt)


### Framtíðarmöguleikar

1. **Gagnaflutningur úr Memo** - þegar Memo-kerfið verður lagt niður þarf að flytja gögn yfir í gagnagrunn Bóthildar
2. **Sjálfvirkar athugasemdir frá AI** - t.d. samantekt á stöðu tjóns eftir ákveðinn tíma, eða sjálfvirk greining á mikilvægum atburðum
3. **Tenging við tölvupóst** - sjálfkrafa bæta innkomnum og útkomnum tölvupóstum sem tengist tjóni á tímalínuna

## Hönnunarhugmyndir

**Saga máls**


## Tæknikröfur

_TODO_

## Tímalína og áfangar

_Bíður - vinna með teyminu eftir að hlið 2 greining er kláruð._

## Áhættur og mótvægisaðgerðir

| Áhætta | Áhrif | Líkur | Mótvægisaðgerð |
|--------|-------|-------|----------------|
| Starfsfólk vantar virkni úr Memo sem Bóthildur býður ekki upp á | Meðal | Meðal | Kortleggja alla notkun á Memo áður en virkni er hönnuð, prófa með notendum |
| Afköst - hægt að sækja Memo-gögn í gegnum API | Meðal | Meðal | Prófa svartíma snemma, meta hvort þurfi caching |

## Epic og sögur

### Epic: Sýsla með athugasemdir tjóns / máls

Tjónafulltrúi vill geta sýslað með athugasemdir tjóns / máls til að skilja og segja frá því sem gerst hefur í tjóninu / málinu.

### Sögur

| # | Saga | Lýsing |
|---|------|--------|
| 1 | Skoða athugasemdir tjóns / máls | Tjónafulltrúi sér lista yfir allar athugasemdir á tjóni eða máli í tímaröð |
| 2 | Bæta við athugasemd á tjón / mál | Tjónafulltrúi skrifar nýja athugasemd á tjón eða mál |
| 3 | Breyta athugasemd | Tjónafulltrúi lagar eða uppfærir athugasemd sem hann hefur skrifað |
| 4 | Eyða athugasemd | Tjónafulltrúi eyðir athugasemd sem hann hefur skrifað |
| 5 | Leita í athugasemdum | Tjónafulltrúi leitar í athugasemdum tjóns eða máls til að finna tilteknar upplýsingar |
