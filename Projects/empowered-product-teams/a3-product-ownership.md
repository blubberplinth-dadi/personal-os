# A3: Óskýrt eignarhald á stafrænum tryggingavörum fyrir einstaklinga

## Bakgrunnur

LB keypti TM vorið 2025. Stefnan er að gera tryggingar að vöru bankans — viðskiptavinir kaupa tryggingar í gegnum LB-rásir, "vátryggt af TM." Þetta þýðir að stafræn upplifun viðskiptavina (Vefsala, Mínar síður, TM appið) á að vera hluti af stafrænu vistkerfi LB.

Áður var eitt teymi (Ronja) ábyrgt fyrir öllu: viðmóti, viðskiptareglum, vinnuflæði og upplifun viðskiptavina. Eftir sameiningu hefur þessi ábyrgð dreifst á mörg teymi og deildir — án þess að skýrt sé skilgreint hver eigi heildarupplifunina.

Þetta skiptir máli núna vegna þess að:
- Vefsala er í virkri þróun með LB-vörumerki
- Nýjar deildir og ábyrgðarsvið eru að mótast
- Ákvarðanir um hvað á að byggja næst eru teknar ad hoc
- TM-fólk er enn með mestu þekkinguna á vörunni og viðskiptavinum

## Núverandi staða

### Innri verkfæri — skýrt eignarhald

| Vara | Eigandi (PM) | Þróunarteymi | Staða |
|------|-------------|---------------|-------|
| Bóthildur | Daði (TM) | Bót (Tryggingalausnir) | Skýrt |
| Rósin | Óskar Örn (TM) | Ronja (Tryggingalausnir) | Skýrt |
| Heimdallur | Óskar Örn (TM) | Ronja (Tryggingalausnir) | Skýrt |

### Viðskiptavinavörur — óskýrt eignarhald

| Vara | Aðilar sem eiga hagsmuna | Hver ákveður hvað á að byggja? |
|------|--------------------------|-------------------------------|
| Vefsala | Óskar Örn (TM), Snæbjörn/Vefdeild (LB), Þórunn Inga (LB), Óli/Tryggingalausnir (LB) | Óljóst — ad hoc |
| Mínar síður | Sömu aðilar | Óljóst — ad hoc |
| TM appið | [NEED: staðfesta stöðu og eignarhald] | Óljóst |

### Skipurit í dag

```
TM                              LB
┌─────────────────┐             ┌──────────────────────────┐
│ Óskar Örn (CPO) │             │ Vefdeild (Snæbjörn)      │
│ - Vöruskilgrein. │             │ - UI fyrir alla viðsk.    │
│ - Viðsk.reglur  │             │ - Vill eiga Vefsölu      │
│ - Þekking       │             │                          │
└────────┬────────┘             ├──────────────────────────┤
         │                      │ Þórunn Inga              │
         │ ?                    │ - Sala og þjónusta       │
         │                      │   trygginga f. einstakl. │
         │                      │ - [NEED: hefur hún PM?]  │
         │                      ├──────────────────────────┤
         │                      │ Tryggingalausnir (Óli)   │
         │                      │ - Backend, viðsk.reglur  │
         │                      │ - Ronja: djúp vöruþekking│
         │                      │   en engin vöruábyrgð    │
         └──────────────────────┘
```

**Fjórir aðilar. Enginn á heildarupplifunina.**

### Ronja-þekkingarvandinn

Forritarar í Ronju (sem þróuðu Vefsöluna) búa yfir djúpri vöruþekkingu: þarfir viðskiptavina, viðskiptareglur, upplifun. Í nýja skipulaginu er hlutverk þeirra afmarkað við "backend" — vöruinnsæi þeirra nýtist ekki formlega.

## Draumastaða

- **Einn eigandi** (einstaklingur eða teymi) ber ábyrgð á heildarupplifun viðskiptavina sem kaupa og nýta tryggingar stafrænt
- Sá eigandi hefur **vald til að forgangsraða** hvað á að byggja næst — ekki bara ráðgjafaraðild
- **Viðskiptareglur, viðmót og upplifun** eru hönnuð saman, ekki í aðskildum sílóum
- **Vöruþekking** Ronju-forritara nýtist í vöruákvarðanir
- Skýr **samhæfing** milli TM (vöruskilgreining, tryggingaþekking) og LB (stafrænar rásir, tækni)
- [NEED: mælanleg markmið — t.d. tími frá hugmynd að afhendingu, ánægja viðskiptavina, conversion rate]

## Greining stöðunnar

### Rótarorsök: Skipulagsleg skipting án samhæfingar

Sameingin skapaði nauðsynlega skipulagsbreytingu (tryggingar verða hluti af bankanum) en framkvæmdin skipti ábyrgð á upplifun viðskiptavina á marga aðila án þess að skilgreina samhæfingaraðila.

### Afleiddar orsakir

**1. Engin heildarábyrgð á upplifuninni**
Vefdeild á UI. Tryggingalausnir á backend. TM á vöruskilgreiningu. Þórunn Inga á sölu og þjónustu. Enginn á keðjuna frá enda til enda — "kaupa tryggingu → nota tryggingu → fá þjónustu."

**2. Óskýr ákvarðanataka**
Þegar enginn á forgangsröðun verða ákvarðanir um hvað á að þróa háðar því hver talar hæst eða hefur bestu tengingarnar. Þetta hægir á afhendingu og getur leitt til rangrar forgangsröðunar.

**3. Samhæfingaráhætta (e. coherence risk)**
Upplifunin þarf að líta út eins og ein vara. Þegar aðskilin teymi byggja sitt hvort án sameiginlegrar vörusýnar verður niðurstaðan ósamræmd.

**4. Ábyrgðarskortur**
Ef conversion í Vefsölu lækkar eða ánægja viðskiptavina fer niður — hver ber ábyrgð? Allir og enginn.

**5. Vöruþekkingarsíló**
Ronju-forritarar búa yfir mikilvægri þekkingu sem nýtist ekki þar sem vöruákvarðanir eru teknar, þar sem hlutverk þeirra er afmarkað við tæknilega framkvæmd.

## Mögulegar lausnir

[Næsti áfangi — vinna með Óskar Örn og öðrum hagsmunaaðilum]

## Tillaga

Engin tillaga enn. Fyrst þarf að:
- Staðfesta núverandi stöðu með Óskari Erni
- Kanna sýn Þórunnar Ingu og Snæbjarnar
- Skilja hvert LB ætlar sér með þetta skipulag

## Næstu skref

- [ ] Fara yfir þetta skjal með Óskari Erni — staðfesta eða leiðrétta skilning
- [ ] Spyrja Óskar Örn: Hefur Þórunn Inga PM eða vörumanneskju?
- [ ] Spyrja Óskar Örn: Hvert er formlegt scope hans á viðskiptavinavörum?
- [ ] Kanna hvort TM appið er sérstök vara eða hluti af Mínar síður
- [ ] Skilgreina mælanlega draumastöðu (conversion, ánægja, afhendingartími)
- [ ] Vinna lausnatillögur þegar staðan er staðfest
