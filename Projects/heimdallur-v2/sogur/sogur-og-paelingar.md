# Sögur og pælingar - Áfangi b

> Greining á því hvernig brjóta megi áfanga b niður í epics og sögur, byggð á greiningu Fríðu.

## Yfirlit yfir greiningarefni Fríðu

Fríða kortlagði alla staði í monorepo þar sem gömul aðgangsstýring (`user.adgerdir.includes()`, `user.hasAccess()`, `user.hasAnyAccess()`, `user.starfsmadur`, o.s.frv.) er notuð.

### Þjónustur og umfang

| Þjónusta | Umfang | Mat Fríðu |
|----------|--------|-----------|
| **dragon-core** | ~44 aðgerðarkóðar, margar skrár | Blanda af einföldum skiptum og flókinni rökfræði (moli.ts, persona.ts) |
| **policyhub-service** | Nýja aðgangsstýringin að hluta til komin | Fylla í eyður, fjarlægja gamla |
| **rosin** | Eigin kóði + dragon-core | Bæta við nýju, fjarlægja gamla úr báðum |
| **user-client** | Lítið | createStarfsmadurUser notað í prófum, gæti verið síðast |
| **user-service** | Mest á nýju þegar | Minniháttar hreinsun (STM tegund) |
| **server-events-service** | Nýtt, gamla ekki innleidd | Skipta áður en farið í loftið |
| **umsoknir** | Nýtt, gamla ekki innleidd | Skipta áður en farið í loftið |
| **person-service** | Nýtt | Einfalt, bara Heimdallur heimildir |
| **lib2b-service** | Ein heimild | Einfalt skipti |
| **tjon-service** | Nýtt | Einfalt skipti |
| **common-claims-api** | Nýtt | Einfalt skipti |
| **gdpr-service** | Nýtt | Einfalt skipti |
| **insurance-change-request** | Nýtt | Einfalt skipti |
| **ahaettuskodanir-service** | Nýtt | Einfalt skipti |
| **endurnyjun-service** | Einn staður í lib | Óljóst, þarf rannsókn |

### Lykiltölur úr hópa-/aðgerðagreiningu

- 60 hópar í gamla kerfinu
- 820 notenda-hópa tengsl
- 44 einstakar aðgerðir (unique action codes)
- Mest notaðar aðgerðir: TRG.G (22 hópar), TRG.U (16), TRG.F (15), 011.F (13)
- Stærsti hópurinn: TINDGRU (161 notendur), SÖLGJD1 (86), SVGROS (70)
- UPPFOR1 er stærsti hópurinn miðað við einstaka aðgerðir (18 unique)
- 6 hópar skiluðu engum niðurstöðum (tolumsj, FJMGJD2, FYRGJD2, HENRY, LOKTRG, Radgjv)

---

## Leið A: Eftir þjónustu/verkefni

Eitt epic per þjónustu, endurspeglar skjal Fríðu beint.

- **dragon-core - Nútímakerfi í Heimdall** (~20+ sögur, stærsta verkefnið)
- **policyhub-service - Nútímakerfi í Heimdall** (fylla í eyður + fjarlægja gamla)
- **rosin - Nútímakerfi í Heimdall** (eigin kóði + dragon-core hreinsun)
- **Smærri þjónustur - Nútímakerfi í Heimdall** (hægt að flokka ~8 einfaldar þjónustur í 1-2 epics)
- **user-client + user-service - Nútímakerfi í Heimdall** (hreinsun, próf)

---

## Sögusnið: Skref í hverri sögu

Upprunaleg tillaga frá STM:

1. Búa til aðgerð eða nota núverandi í kóða eftir þörfum
2. Búa til hlutverk/heimild/aðgerð í Heimdalli eftir þörfum
3. Uppfæra viðeigandi notendur í Heimdalli svo þeir hafi áfram þann aðgang sem við færðum úr gamla eftir þörfum
4. Fjarlægja gömlu aðgangsstýringu
5. Prófa vel

### Endurbætur á sniðinu

**Skref 3 — ákveða hverjir fá hlutverkið áður en farið er í framkvæmd.** Gamlir hópar hverfa — Heimdallshlutverk taka við. Gömlu hópana má nota sem viðmið en ekki endilega 1:1. Atriði sem þarf að taka afstöðu til:
- Utanaðkomandi notendur í hópum (SPATIL: 15, TOYOTA: 13) — eiga þeir að fá hlutverk í Heimdalli?
- UPPFOR1 (18 einstaka aðgerðir) — á þetta að verða eitt breitt hlutverk eða sundurliðað í fleiri?
- Tómir hópar (tolumsj, HENRY, LOKTRG, o.fl.) — hverfa, engin aðgerð þarf

**Skref 4 (fjarlægja gamla) — tímasetning skiptir máli.** Á að keyra bæði samhliða í stuttan tíma per sögu og síðan skera yfir? Eða hörð skipting per sögu? Stutt samhliða keyrsla gerir afturköllun auðveldari ef eitthvað gleymist.

**Skref 5 (prófa) — tvö stig.** Bæði "notar kóðinn Heimdall rétt" (forritarapróf) og "hafa réttir notendur enn réttan aðgang" (samþykktarpróf, hugsanlega með Nonna eða tengiliðum á sviðinu).

### Dæmi um sögu

#### lib2b-service - Færa aðgangsstýringu í Heimdall

**Hvað þarf að gera og af hverju?**
Í lib2b-service er gömul aðgangsstýring á einum stað: /src/server/index.ts þar sem user.hasAccess athugar TIN.K heimild til að auðkenna notanda og veita aðgang að allri þjónustunni. Nýja aðgangsstýringin hefur ekki verið innleidd í þessari þjónustu svo þarf að skipta út gömlu þegar búið er að ganga úr skugga um að allir viðeigandi notendur hafi réttar heimildir í Heimdalli.

**Gátlisti**
- □ Aðgerð/heimild til í kóða (TIN.K eða sambærileg heimild í Heimdalli)
- □ Hlutverk/heimild/aðgerð til í Heimdalli
- □ Notendur uppfærðir í Heimdalli — nota gömlu hópana sem viðmið (NTIAPI hópur er með TIN.K aðgerð)
- □ Gömul aðgangsstýring fjarlægð úr /src/server/index.ts
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- lib2b-service notar Heimdall til aðgangsstýringar í stað user.hasAccess('TIN.K')
- Notendur sem voru í NTIAPI hóp hafa aðgang í gegnum hlutverk í Heimdalli
