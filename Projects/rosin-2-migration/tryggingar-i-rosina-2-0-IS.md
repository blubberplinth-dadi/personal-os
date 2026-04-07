# Færa fleiri tryggingar úr Græna og um leið nútímavæða Rósina

**Dagsetning:** Janúar 2026
**Höfundur:** [Nafn]
**Ábyrgðaraðili:** Óskar Örn Ingvarsson
**Staða:** Tillaga

---

## Samantekt

TM stendur frammi fyrir þremur brýnum áskorunum: (1) nokkrar tryggingategundir (þ.á.m. allar fyrirtækjatryggingar) krefjast enn gamla Græna AS/400 kerfisins, sem neyðir starfsfólk til að vinna mikið í bæði Græna og Rósinni; (2) einungis 1-2 forritarar (sem þar að auki fara á eftirlaun innan fárra ára) hjá TM geta viðhaldið Græna og nánast ómögulegt er að ráða aðra í þeirra stað; og (3) notendaviðmót Rósarinnar er byggt á Angular 1.8 sem ekki er lengur studd tækni og hefur ekki verið uppfært síðan 2022 og skapar ákveðna öryggisáhættu.

Við leggjum til að tekið verði á öllum þessum áskorunum í einu heildarverkefni þar sem flutningur ákveðinna tryggingategunda úr Græna fer fram samhliða endurskrift notendaviðmóts Rósarinnar í nútímalegri og vel studdri tækni.

**Tillagan:** Að Ronju-teymið hefji verkefni við að flytja þessar tryggingar úr Græna og um leið nútímavæðingu viðmóts. Tillagan gengur út frá því að upphafið taki mestan tíma. Því næst sé hægt að taka eina tryggingartegund fyrir í einu eða m.v. bandvídd Ronju teymisins sem stjórnast af forgangi vinnu þess við áherslumarkmið LB/TM og nauðsynlegan rekstur núverandi kerfa.

---

## Strategískt samhengi

### Núverandi staða

**Óhagkvæmni tveggja kerfa:**
- Dýrt og flókið að þurfa að viðhalda tengingum milli tveggja tryggingakerfa
- Ekki hægt að selja tryggingar úr Græna í Vefsölunni
- Tryggingaráðgjafar þurfa að skipta á milli Rósarinnar og Græna fyrir ákveðnar tryggingategundir sem tekur tíma og eykur villuhættu.
- Þjálfunarbyrði tvöfaldast fyrir nýtt starfsfólk

**Áhætta vegna öryggisgalla og legacy tækni:**
- Angular 1.8 hefur ekki verið öryggisuppfært síðan í desember 2021
    - Þekktir veikleikar eru til staðar og ekki hægt að laga þá
    - Þetta stangast á við öryggisstaðla LB og kröfur innri endurskoðunar
- Ekki hægt að fá aðra í stað starfandi AS/400 / RPG sérfræðinga nema með rándýrum verktökum

### Hvers vegna þetta skiptir máli

**Áhrif á rekstur:**
- Skilvirkni ráðgjafa: Áætlað 60 mínútur/dag tapast vegna kerfaskipta?!?
- Nýliðaþjálfun: Nýir ráðgjafar þurfa u.þ.b. fjögurra vikna lengri tíma til að ná fullri framleiðni
- Djúp þekking á Græna tryggingakerfinu er hjá ráðgjöfum sem nálgast eftirlaun
- Upplifun viðskiptavina: Hægari þjónusta þegar ráðgjafar þurfa að fara á milli kerfa

**Áhætta af aðgerðaleysi:**
- Öryggisatvik gæti stefnt gögnum viðskiptavina og orðspori TM / LB í hættu
- Tækniskuld safnast upp eftir því sem lausnir bætast við í úreldri tækni
- AS/400 sérfræðiþekking fer á eftirlaun; viðhald verður erfiðara / dýrara ár frá ári

### Samræmi við stefnu

- **Samþætting við LB:** Færsla virkni í nútímaleg, viðhaldshæf kerfi styður samlegðaráhrif banka og trygginga
- **Stafræn umbreyting:** Samræmist markmiði TM um að leggja niður eldri kerfi
- **Rekstrarhagkvæmni:** Gerir hraðari þróun mögulega þegar flutningi lýkur

### Tengsl við könnun á hugbúnaðarkaupum

Samhliða þessu verkefni er unnið að könnun á mögulegum kaupum á tilbúnum tryggingakerfum. Jafnvel þótt ákvörðun verði tekin um kaup á slíkri lausn, þá er mat okkar að Rósin (og Græna á meðan það er til) verði áfram helsta verkfæri starfsfólks í a.m.k. 5 ár til viðbótar á meðan á mögulegri innleiðingu nýs kerfis stæði.

Þessi nútímavæðing er því nauðsynleg óháð niðurstöðu þessarar könnunar:
- Öryggisáhættu vegna Angular 1.8 verður að taka á núna, ekki eftir 5 ár
- Starfsfólk þarf virkt og öruggt kerfi þangað til ný lausn tekur við
- Fjárfestingin heldur gildi sínu sem brú yfir umbreytingartímabilið
---

## Tækifærið

### Markmið

| Markmið | Árangur lítur svona út | Hvernig mælum við |
|---------|------------------------|-------------------|
| Helstu fyrirtækjatryggingar fluttar | Helstu tryggingategundir fyrirtækja virka í Rósinni | 0 daglegir notendur í Græna sýsla með helstu fyrirtækjatryggingar  |
| Útrýma öryggisáhættu | Viðmót í vel studdri tækni með virkum öryggisuppfærslum | Standast öryggisúttekt; engir þekktir veikleikar |
| Minnka rekstraráhættu tryggingakerfa | Tryggingaumsýsla að mestu kominn úr úreldri tækni  | Fjöldi trygginga í Rós mun hærri vs. Græna |
| Bæta skilvirkni ráðgjafa | Eitt kerfi fyrir megnið af tryggingavinnu | Minni meðaltími við tryggingaumsýslu |

### Umfang

**Innan umfangs:**
- Eftirfarandi tryggingategundir [tilgreina tryggingategundir sem eftir eru] er sýslað með í Rósinni í stað Græna
- Endurskrifun viðmóts úr Angular 1.8 yfir í [React/Angular 17/annað - á eftir að ákveða]
- Viðtökuprófanir
- Þjálfun notenda

**Utan umfangs:**
- Virkni Rósarinnar utan tryggingaumsýslu eins og
    - Yfirlit yfir viðskiptavin og öll hans viðskipti við TM
    - Tjónasaga
    - Umsýsla með greiðslufyrirkomulag, ...

---

## Greining valkosta við flutning trygginga

### Valkostur A: Í röð (Flytja fyrst, síðan nútímavæða viðmót)

**Lýsing:** Ljúka AS/400 flutningi inn í núverandi Angular 1.8 tækni, síðan endurskrifa viðmót á eftir.

| Kostir | Gallar |
|--------|--------|
| Minni flækja í upphafi | Öryggisáhætta varir lengur |
| Skýrir áfangar | Tvær stórar breytingar fyrir notendur |
| Hægt að staðfesta flutning áður en viðmót breytist | Lengri heildartími A+C en bara B |

**Mat á vinnu:** ~6 mánuðir samtals
**Áhættustig:** Miðlungs (öryggisáhætta í fyrsta áfanga)

### Valkostur B: Samhliða (Flytja og nútímavæða saman)

**Lýsing:** Endurskrifa viðmót í nútímalegri tækni samhliða flutningi tryggingategunda. Nýjar tegundir birtast beint í nýju viðmóti.

| Kostir | Gallar |
|--------|--------|
| Tekur á öryggisáhættu fyrr | Meiri flækja í upphafi |
| Fleiri, minni breytingar sem skila virði | Ruglingur um í hvaða kerfi tegund er |
| Styttri heildartími | Flóknari tengsl milli verkþátta |

**Vinnuálag:** ~9 mánuðir
**Áhættustig:** Miðlungs-hátt

### Valkostur C: Aðeins viðmót (Nútímavæða viðmót, fresta flutningi)

**Lýsing:** Endurskrifa viðmót í nútímalegri tækni en halda AS/400 tengingu fyrir tegundir sem eftir eru.

| Kostir | Gallar |
|--------|--------|
| Tekur á öryggisáhættu fljótt | Vandamál tveggja kerfa heldur áfram |
| Minna umfang | Þarf að byggja nýja viðmótstengingu við eldra kerfi |
| | Frestar stefnumarkmiði um niðurlagningu AS/400 |

**Vinnuálag:** ~8 mánuðir
**Áhættustig:** Lágt (en leysir ekki kjarnavandann)

### Valkostur D: Gera ekkert

**Hvað gerist:**
- Öryggisáhætta vex; hugsanlegar athugasemdir úr úttektum eða öryggisatvik
- AS/400 viðhald verður erfiðara þegar sérfræðiþekking fer á eftirlaun
- Óhagkvæmni ráðgjafa heldur áfram
- Tækniskuld safnast áfram upp og gerir framtíðarbreytingar erfiðari

---

## Tillaga

**Tillaga að valkosti:** Valkostur B (Samhliða flutningur og nútímavæðing)

**Rökstuðningur:**
- Tekur á báðum vandamálum í einu
- Lágmarkar áhættu sem fylgir mjög stórum breytingum (e. big bang release) með því að setja hverja nýja tryggingu í loftið um leið og hún er tilbúin
- Styttri heildartími dregur úr langvarandi áhættu
- Fluttar tegundir þróaðar á traustum tæknigrunni frá upphafi
- Samræmist væntingum LB / TM um nútímaleg, örugg kerfi

**Lykilforsenda árangurs:** Sérstakt teymi með skýrt eignarhald, ekki skipt á milli annarra forgangsverkefna.

---

## Áætlun

### Teymi

| Hlutverk | Ráðstöfun | Tímalengd |
|----------|-----------|-----------|
| Tæknistjóri | 100% | 12 mánuðir |
| Framendaforritarar | 2 stöðugildi | 12 mánuðir |
| Bakendaforritarar | 1,5 stöðugildi | 12 mánuðir |
| Hönnuður | 50% | 6 mánuðir (viðmótsmynstur) |
| Prófari | 1 stöðugildi | 12 mánuðir |
| Vöruráðgjafi (Daði/Óskar) | 25% | 12 mánuðir |

### Kostnaðaráætlun

| Liður | Áætlaður kostnaður |
|-------|-------------------|
| Þróunarteymi | [Upphæð - á eftir að meta] |
| Innviðir/verkfæri | [Upphæð] |
| Þjálfun/breytingastjórnun | [Upphæð] |
| Varasjóður (15%) | [Upphæð] |
| **Samtals** | **[Upphæð]** |

### Tímalína

| Áfangi | Markdagsetning |
|--------|----------------|
| Verkefni hefst | [1F 2026] |
| Ákvörðun um viðmótsramma og arkitektúr | [+1 mánuður] |
| Fyrsta tryggingategund flutt í nýtt viðmót | [+4 mánuðir] |
| 50% tegunda flutt | [+8 mánuðir] |
| Flutningi lokið | [+11 mánuðir] |
| Stöðugleiki og niðurlagning AS/400 | [+12 mánuðir] |

---

## Áhættur og mótvægisaðgerðir

| Áhætta | Áhrif | Líkur | Mótvægisaðgerð |
|--------|-------|-------|----------------|
| Flækja samhæfingar seinkar framgangi | Mikil | Miðlungs | Sérstakt teymi; skýrt eignarhald; regluleg samstilling |
| Falin flækja í eldri gögnum/lógík | Mikil | Miðlungs | Könnunaráfangi; fá AS/400 sérfræðinga inn snemma |
| Mótstaða notenda við breytingar | Miðlungs | Lítil | Snemmbær þátttaka; þjálfun; áfangaútgáfa |
| Lykilstarfsfólk ekki tiltækt | Mikil | Lítil | Skjalfesta þekkingu; krossþjálfa teymi |
| Valinn rammi verður úreltur | Miðlungs | Lítil | Velja rótgróinn ramma með sterku samfélagi |

---

## Ákvörðun óskast

Samþykkt að Ronju-teymið fari af stað með valkost B (samhliða flutningur og nútímavæðing) með:
- Sérstakri teymisráðstöfun eins og lýst er
- Samþykki kostnaðaráætlunar að upphæð [upphæð]
- 12 mánaða tímalínu sem hefst [dagsetning]

**Frestur til ákvörðunar:** [Dagsetning] til að hefja könnunaráfanga í [mánuður]

---

## Viðaukar

### A. Tryggingategundir sem eftir eru í AS/400

| Tegund | Flækjustig | Notkun |
|--------|------------|--------|
| [Tegund 1] | Hátt/Miðlungs/Lágt | [X notendur/dag] |
| [Tegund 2] | Hátt/Miðlungs/Lágt | [X notendur/dag] |

### B. Öryggisáhyggjur vegna Angular 1.8

- [Tilgreina CVE eða athugasemdir úr öryggisúttektum ef til staðar]
- [Tengill á öryggisstefnu LB]

### C. Valkostir fyrir viðmótsramma

| Rammi | Kostir | Gallar | Tillaga |
|-------|--------|--------|---------|
| React | Stórt vistkerfi, LB notar | Ólíkt núverandi | Íhuga |
| Angular 17+ | Uppfærsluslóð frá Angular 1 | Enn Angular | Íhuga |
| [Annað] | [Kostir] | [Gallar] | [Staða] |
