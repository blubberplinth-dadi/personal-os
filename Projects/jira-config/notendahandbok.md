# JIRA Notendahandbók fyrir Bót og Ronju

Þessi handbók er fyrir þróunarteymi TM — Bót og Ronju. Hér er lýst hvernig við notum JIRA í daglegu starfi.

---

## 1. Byrjun

### 1.1 Hvaða borð á að nota?

Við notum tvö borð fyrir hvort teymi, auk eins sameiginlegs Bug borðs:

| Borð | Tilgangur | Hvenær á að nota |
|------|-----------|------------------|
| **Epic borð** (t.d. "Bót - Epic board") | Skipulagning og yfirsýn | Þegar þú ert að skipuleggja vinnu, forgangsraða, eða skoða stöðu Epics (stærri verkefna) |
| **Þróunarborð** (t.d. "Bót - Work board") | Dagleg þróunarvinna | Þegar þú ert að vinna í verkefnum, færa hluti í gegnum þróunarferlið |
| **Bug borð** ("Shared - Bug board") | Villuskráning | Villur sem ekki þarf að laga strax fara hingað í forgangsröðunarferli |

### 1.2 Teymis-reiturinn (Teymi)

**Mikilvægt:** Allir JIRA-miðar ættu að hafa teymi valið!

- Veldu **Bót** eða **Ronja** í "Teymi" reitnum þegar þú býrð til nýjan miða
- Þetta tryggir að miðinn birtist á réttu borði

---

## 2. Miðategundir (Issue Types)

### 2.1 Yfirlit

| Tegund | Notkun | Dæmi |
|--------|--------|------|
| **Epic** | Stærri verkefni sem spanna vikur (1–3 mánuðir) | "Betra klára-kaup ferli Vefsölu TM", "Sýsla með skaðabótaáætlun" |
| **Story** | Virkni sem skilar notendum gildi (1–5 dagar) | "Sjá stöðu á klára-kaup aðgerðum", "Stofna mál með skaðabótaáætlun" |
| **Bug** | Villur sem þarf að laga | "Samtala iðgjalda stemmir ekki við summu iðgjaldalína" |

### 2.2 Hvenær á að nota hverja tegund

- **Epic:** Áætlanir sem krefjast skipulagningar og samhæfingar yfir margar vikur. Búðu til Epic ef þú ert með 3+ tengdar sögur eða vinnu fyrir meira en einn sprett.
- **Story:** Virkni sem skilar notendum gildi — t.d. nýr fítus eða bætt upplifun.
- **Bug:** Villur í virkni sem þegar er komin í notkun.

### 2.3 Hvenær á að búa til Epic

**Búðu til Epic þegar:**
- Þú átt 3+ tengdar sögur/tasks
- Vinnan spannar meira en eina vinnulotu
- Skipulagning eða hönnun þarf að eiga sér stað áður en vinna hefst
- Vinna krefst samhæfingar á milli kerfa eða teyma

**Búðu EKKI til Epic þegar:**
- Um er að ræða einstaka litla villu eða lagfæringu
- Vinnan er eitt afmarkað verk sem klárast á stuttum tíma
- Þetta er viðhaldsvinna eða uppfærsla sem krefst ekki skipulagningar

**Viðmið fyrir stærð:** Epic ætti að klárast á 1–3 mánuðum. Ef lengra, brjóttu í fleiri Epics. Ef styttra, þá er þetta líklega bara Story.

**Forðastu ruslaskúffu-Epics:**
- ❌ "Q1 villuleiðréttingar" (of almennt)
- ❌ "Ýmsar endurbætur" (óskýrt)
- ❌ "Tækniskuld" án afmarkaðs markmiðs

### 2.4 Halda sögum litlum

**Meginregla:** Ef saga lítur út fyrir að þurfa >5 daga í vinnu er hún sennilega of stór.

Þrjár leiðir til að brjóta niður vinnu í sögu:

**1. Sub-tasks** — Henta þegar vinnan þarf að fara í hendur mismunandi forritara samhliða, eða þegar stykki þurfa sitt hvora stöðurakninguna. Sub-tasks birtast ekki á borðinu sem kort — þau sjást í nánar-yfirliti foreldramiðans.

**2. Skipta sögunni** — Ef saga er of stór, splittaðu í 2+ minni sögur og tengdu allar við sama Epic.

```
Dæmi - Of stór saga:
Flytja tjónareikninga inn í Bóthildi

Dæmi - Rétt skipt:
Flytja inn debet tjónareikninga  [Epic: Flytja tjónareikninga inn í Bóthildi]
Flytja inn kredit tjónareikninga [Epic: Flytja tjónareikninga inn í Bóthildi]
Flytja inn CABAS tjónareikninga  [Epic: Flytja tjónareikninga inn í Bóthildi]
```

**3. Lýsingarrakning** — Fyrir innleiðingarskref sem þarfnast ekki sérstakra miða, notaðu bullet-lista í lýsingasvæðinu. Notum strikethrough til að merkja lokið.

```
**Skref:**
- ~~Hanna útlit~~
- ~~Grunnútfærsla~~
- Bæta við drag-and-drop
- Skrifa prófanir
```

**Hvenær á að nota hverja leið:**

| Aðstæður | Leið |
|----------|------|
| Vinna getur farið í hendur mismunandi forritara samhliða | Sub-tasks eða skipta í fleiri sögur |
| Stykki þurfa sitt hvora stöðurakninguna undir sömu sögu | Sub-tasks |
| Vinna spannar marga daga með skýr skil á milli | Skipta í fleiri sögur |
| Einföld innleiðingarskref fyrir einn aðila | Lýsingarrakning |
| Gátlisti eða samþykkisskilyrði | Lýsingarrakning |

---

## 3. Vörur / Kerfi (Components)

Veldu alltaf vöru eða kerfi á miða. Þetta segir til um hvaða kerfi vinnan snýr að.

**Dæmi um val:**

```
Bug: Dagsetningarval virkar ekki rétt
└── Component: Rósin

Story: Opna tjónareikning þó málsnúmer vanti
└── Components: Bóthildur, Rafrænir reikningar

Epic: Taka á móti og vinna úr rafrænum reikningum
└── Components: Rafrænir reikningar, Bóthildur, API, Sjálfvirkni
```

**Regla:** Veldu alltaf component. Ef þú ert í vafa, veldu kerfið sem verður mest fyrir áhrifum.

**Undantekning — Sub-tasks:** Ekki þarf að setja component á Sub-tasks. Þau birtast aldrei sjálfstætt á borðum, aðeins inni í foreldramiðanum. Component á foreldramiðanum nægir.

---

## 4. Epic borð

### 4.1 Tilgangur

Epic borðið er þar sem teymi skipuleggja vinnu sína og halda utan um stærri verkefni.

**Hvað birtist á Epic borði:**
- **Öll Epics** í gegnum allt lífsferli þeirra (To Do → In analysis → Ready for development → In Progress → Done)
- **Sjálfstæðir miðar** (sögur/tasks án Epic tengingar) í To Do og In analysis
- **Sub-tasks á Epics** í To Do og In analysis (uppgötvunar- og greiningarvinna)

**Villur (Bugs) birtast ekki á Epic borði** — þær fara á Bug borðið.

### 4.2 Dálkar og stöður

| Dálkur | Lýsing |
|--------|--------|
| **To Do** | Vinna sem hefur verið skilgreind en ekki enn forgangsraðað |
| **In analysis** | Í greiningu og niðurbroti — sögur búnar til, rannsóknir í gangi |
| **Ready for development** | Greining lokið, tilbúið til þróunar |
| **In Progress** | Þróun hafin (Epic helst á borðinu, sögur fara á þróunarborð) |
| **Done** | Lokið |

### 4.3 Hvernig miðar flæða

```
Epic borð (Skipulagning og rakning)
┌───────────────────────────────────────────────────────────────────┐
│                                                                   │
│  To Do → In analysis → Ready for development → In Progress → Done │
│                                                                   │
│  EPICS flæða í gegnum ALLA dálka (haldast á Epic borði)          │
│  ├─ Stofnuð í "To Do"                                            │
│  ├─ Færð í "In analysis" fyrir greiningu og stofnun sagna        │
│  ├─ Færð í "Ready for development" þegar tilbúin                 │
│  ├─ Færð í "In Progress" þegar þróun hefst                       │
│  └─ Færð í "Done" þegar allri vinnu lokið                        │
│                                                                   │
│  SUB-TASKS Á EPICS birtast í "To Do" og "In analysis"            │
│  ├─ Notað til að rekja uppgötvunarvinnu (FD drög, viðtöl o.fl.)  │
│  └─ Hverfa af borði þegar staða fer út fyrir "In analysis"        │
│                                                                   │
│  SJÁLFSTÆÐIR MIÐAR birtast í "To Do" og "In analysis"            │
│  └─ Hverfa þegar staða → Next In (fara á þróunarborð)            │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
                            │
                            │ Staða breytist í Next In
                            ├─ Sögur (tengdar Epic)
                            └─ Sjálfstæðir miðar
                            │
                            ▼
                  Þróunarborð (Dagleg vinna)
```

---

## 5. Þróunarborð

### 5.1 Tilgangur

Þróunarborðið er þar sem dagleg þróunarvinna fer fram. Hér sjást allar sögur, tasks og villur í vinnslu.

**Hvað birtist á þróunarborði:**
- **Sögur, Tasks og Bugs** í þróunarstöðum — bæði Epic-tengd og sjálfstæð
- **Epic nafn** birtist á hverju korti svo samhengið sé skýrt
- Epics sjálf birtast **ekki** á þróunarborði — þau haldast á Epic borði

### 5.2 Dálkar og stöður

| Dálkur | Lýsing |
|--------|--------|
| **Next In** | Í biðröð eftir að komast í vinnslu |
| **In Progress** | Í virkri þróun |
| **In review** | Í kóðayfirferð |
| **In testing** | Í prófunum |
| **Ready for deployment** | Bíður útgáfu |
| **Done** | Lokið / gefið út |

### 5.3 Dagleg notkun

1. **Opnaðu þróunarborð** → Sjáðu alla miða í vinnslu
2. **Epic nafn á kortum** sýnir hvaða Epic hver miði tilheyrir
3. **Notaðu Quick Filters** til að sía eftir ákveðnu Epic eða sjá aðeins sjálfstæða miða
4. **Smelltu á Epic nafn** á korti til að fara á Epic og sjá heildarmynd
5. **Færðu miða** á milli dálka eftir því sem vinna miðast áfram
6. **Þarft að skipuleggja?** Skiptu yfir á Epic borðið

### 5.4 Sýnidæmi um útlit

```
Þróunarborð — Flat kortayfirlit
┌──────────────────────────────────────────────────────────────────┐
│  Next In           │  In Progress       │  In review     │ ...  │
│                    │                    │                │      │
│  TM-503            │  TM-501            │  TM-502        │      │
│  Bæta við staðfest.│  Ljósmyndaupphleðsl│  Bakendapunktur│      │
│  [Tjónamóttaka]    │  [Tjónamóttaka]    │  [Tjónamóttaka]│      │
│                    │                    │                │      │
│                    │  TM-702            │  TM-701        │      │
│                    │  Uppfæra pakka     │  Laga dagsetn. │      │
│                    │  [ekkert epic]     │  [ekkert epic] │      │
│                    │                    │                │      │
│                    │  TM-601            │                │      │
│                    │  Hanna tilboð      │                │      │
│                    │  [Fjölbílatilboð]  │                │      │
└──────────────────────────────────────────────────────────────────┘

[Epic nafn] = Epic nafn birt á korti til samhengis
[ekkert epic] = Sjálfstæður miði, ekki tengdur Epic
```

---

## 6. Bug borð

### 6.1 Tilgangur

Eitt sameiginlegt Bug borð fyrir bæði teymin. Vörustjórar meta villur hér og ákveða hvað fer í vinnslu.

### 6.2 Dálkar

| Dálkur | Lýsing |
|--------|--------|
| **To Do** | Tilkynnt, bíður mats |
| **Next In** | Metin og sett í vinnslu — birtist líka á þróunarborði |
| **Done / Declined** | Lokið eða hafnað |

### 6.3 Hvernig villur flæða

```
Villa tilkynnt → Bug borð ("To Do")
                   │
                   ├─ Lögum ekki → Staða → "Done / Declined"
                   ├─ Lögum núna → Staða → "Next In" (birtist á þróunarborði)
                   └─ Lögum seinna → Setja forgang, raða með því að draga
                                      │
                                      │ Þegar vörustjóri er tilbúinn:
                                      │ Staða → "Next In"
                                      ▼
                                  Þróunarborð (venjulegt þróunarflæði)
```

### 6.4 Hvar birtast villur?

| Borð | Sýnir villur? |
|------|---------------|
| Epic borð | Nei |
| Bug borð | Já — allar villur, bæði teymi |
| Þróunarborð | Já — villur sem hafa náð "Next In" |

---

## 7. Algeng verkefni

### 7.1 Búa til og skipuleggja nýtt Epic

1. **Búðu til Epic:**
   - Smelltu á "Create" í JIRA
   - Veldu "Epic" sem tegund
   - Fylltu út: Summary, Teymi (Bót eða Ronja), Component (vara / kerfi)
   - Epic byrjar í "To Do" stöðu

2. **Færðu í greiningu:**
   - Á Epic borði, dragðu Epic í "In analysis" dálk
   - Bættu Sub-tasks við Epic til að rekja uppgötvunarvinnu (t.d. "Skrifa FD drög", "Tala við notendur", "Story mapping")
   - Sub-tasks á Epic birtast á Epic borði meðan þær eru í "To Do" eða "In analysis"

3. **Búðu til sögur:**
   - Búðu til miða fyrir hvert afmarkað verk
   - Tengdu við Epic með "Epic Link" reitnum
   - Settu rétta vöru / kerfi á hvern miða

4. **Merktu tilbúið:**
   - Þegar allar sögur eru skilgreindar, færðu Epic í "Ready for development"

5. **Byrjaðu þróun:**
   - Færðu Epic í "In Progress" þegar teymið byrjar
   - Epic helst á Epic borði (birtist ekki á þróunarborði)
   - Færðu sögur í þróunarstöður — þær birtast á þróunarborði með Epic nafni

### 7.2 Vinna með sjálfstæðan miða (ekki í Epic)

1. Búðu til Story, Task eða Bug — **ekki** fylla út "Epic Link"
2. Veldu teymi og vöru / kerfi
3. Miði birtist á Epic borði í "To Do" eða "In analysis"
4. Þegar staða breytist í "Next In" færist hann á þróunarborð

### 7.3 Tilkynna og laga villu

1. Búðu til Bug — hann birtist á Bug borði í "To Do"
2. Veldu teymi og vöru / kerfi
3. Ef villan tengist Epic, notaðu "Epic Link"
4. Vörustjóri metur villuna og ákveður forgangsröðun
5. Þegar villan er sett í "Next In" birtist hún líka á þróunarborði teymisins

---

## 8. Flýtiuppflettingar

### 8.1 Hvenær miði birtist hvar

| Miðategund | Epic borð | Þróunarborð | Bug borð |
|------------|-----------|-------------|----------|
| Epic (allar stöður) | ✅ Já | ❌ Nei | ❌ Nei |
| Sub-task á Epic (To Do / In analysis) | ✅ Já | ❌ Nei | ❌ Nei |
| Sub-task á Epic (aðrar stöður) | ❌ Nei | ❌ Nei | ❌ Nei |
| Story tengd Epic (skipulagsstaða) | ❌ Nei | ❌ Nei | ❌ Nei |
| Story tengd Epic (þróunarstaða) | ❌ Nei | ✅ Já (með Epic nafni) | ❌ Nei |
| Sjálfstætt (skipulagsstaða) | ✅ Já | ❌ Nei | ❌ Nei |
| Sjálfstætt (þróunarstaða) | ❌ Nei | ✅ Já | ❌ Nei |
| Bug (To Do) | ❌ Nei | ❌ Nei | ✅ Já |
| Bug (Next In+) | ❌ Nei | ✅ Já | ✅ Já |

### 8.2 Gátlisti fyrir nýjan miða

- [ ] Tegund valin (Epic / Story / Task / Bug)
- [ ] Teymi valið (Bót eða Ronja)
- [ ] Vara / kerfi valið (Vefsala TM / Bóthildur / Rósin / ...)
- [ ] Epic Link ef við á

---

*Síðast uppfært: Mars 2026*
