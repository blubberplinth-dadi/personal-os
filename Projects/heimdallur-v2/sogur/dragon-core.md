# dragon-core - Nútímakerfi í Heimdall

> Epic: Skipta gömlu aðgangsstýringunni út í dragon-core fyrir heimildir í Heimdalli. Hér er mikið af einföldum hasAccess tékkum sem ætti ekki að vera mikið mál, en inn á milli leynast flóknari aðgerðir. Gæti verið sniðugt að styðjast við svipað fall og isAuthorized í policyhub-service. Passa þarf að laga öll próf sem styðjast við gömlu aðgangsstýringuna og bæta við prófum fyrir nýju.

---

### Einföld validator tékk í Heimdall

**Hvað þarf að gera og af hverju?**
Sex skrár í dragon-core nota einföld `user.hasAccess` tékk til að ákvarða hvort skilað sé warn eða error í validation föllum. Þetta eru öll einföld tékk sem ætti að vera auðvelt að skipta út.

Skrárnar eru:
- `/src/shared/model/period_validators.ts` — TRG.L í `maxMonthsInPeriod`: warn eða error eftir heimild. Og TRG.Q + SLS.A í `endBeforeHamarkTil`: warning eða error eftir heimild.
- `/src/shared/model/edit/molar/upphaed_range.ts` — TRG.M: error eða warn í skilaboðum
- `/src/shared/model/edit/vidfong/hestur.ts` — TRG.M: hasAccess í if setningu
- `/src/shared/model/edit/soluvara/validateSlysOgSjuk.ts` — TRG.M: hasAccess í else if skilyrðum
- `/src/shared/model/edit/soluvara/validateGaeludyr.ts` — TRG.M: warn eða error
- `/src/shared/model/vidfong/ahaettuskodun.ts` — 133.A: warn eða error

**Gátlisti**
- □ Heimildir í Heimdalli sem samsvara TRG.L, TRG.M, TRG.Q, SLS.A og 133.A
- □ Hlutverk/heimild/aðgerð til í Heimdalli
- □ Notendur uppfærðir í Heimdalli — nota gömlu hópana sem viðmið
- □ Skipta `user.hasAccess` út í öllum sex skrám
- □ Gömul aðgangsstýring fjarlægð
- □ Próf uppfærð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- Allar sex skrár nota heimildir í Heimdalli í stað gamalla hasAccess tékka
- Validator hegðun (warn vs error) óbreytt — bara uppspretta heimildarinnar breytist

### Einföld hasAccess tékk í Heimdall

**Hvað þarf að gera og af hverju?**
Sjö skrár í dragon-core nota einföld `user.hasAccess` tékk til að stýra aðgangi eða sýnileika. Þetta eru öll einföld tékk — boolean breytur, canToggle, einfalt aðgangsmat.

Skrárnar eru:
- `/src/shared/model/sundurlidun.ts` — TRG.V: einfalt hasAccess tékk, auðvelt að nota frekar nýju aðgangsstýringuna
- `/src/shared/model/molar/soluleidMoli.ts` — ROS.S: einfalt hasAccess tékk
- `/src/shared/model/vernd.ts` — TRG.K: einfalt hasAccess í canToggle falli á vernd objectinu
- `/src/shared/model/edit/mixinEdit.ts` — TRG.X: einfalt hasAccess
- `/src/shared/radgjof/box/born.ts` — 360.A: einfalt boolean — disable-a box ef ekki heimild
- `/src/server/dataaccess/dbdataclient.ts` — TRG.X: einfalt hasAccess í `findMolarByKennitalaAndNafReiLidAndVaraId`
- `/src/shared/model/edit/molar/entered_fjarhaed_moli.ts` — SLS.A: einfalt true/false tékk á dánarbætur ≤ 2.000.000 kr

**Gátlisti**
- □ Heimildir í Heimdalli sem samsvara TRG.V, ROS.S, TRG.K, TRG.X, 360.A og SLS.A
- □ Hlutverk/heimild/aðgerð til í Heimdalli
- □ Notendur uppfærðir í Heimdalli — nota gömlu hópana sem viðmið
- □ Skipta `user.hasAccess` út í öllum sjö skrám
- □ Gömul aðgangsstýring fjarlægð
- □ Próf uppfærð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- Allar sjö skrár nota heimildir í Heimdalli í stað gamalla hasAccess tékka

### createtrygging heimildir í Heimdall

**Hvað þarf að gera og af hverju?**
Í `/src/shared/dataaccess/createtrygging.ts` nota EditAction föll gömlu aðgangsstýringuna. LIF.U er notað til að athuga hvort notandi hafi réttindi til líftryggingaráðgjafa og TBA.U er notað til að athuga hvort notandi eigi rétt á að búa til barnatryggingu. Ætti að vera auðvelt að skipta þessu út.

**Gátlisti**
- □ Heimildir í Heimdalli sem samsvara LIF.U og TBA.U
- □ Hlutverk/heimild/aðgerð til í Heimdalli
- □ Notendur uppfærðir í Heimdalli — nota gömlu hópana sem viðmið (LIFRAD hópur er með LIF.U)
- □ Gömul aðgangsstýring fjarlægð úr `createtrygging.ts`
- □ Próf uppfærð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- `createtrygging.ts` notar heimildir í Heimdalli í stað gamalla EditAction athugana

### fellanidur heimildir í Heimdall

**Hvað þarf að gera og af hverju?**
Þrjár skrár í fellanidur-möppunni nota gömlu aðgangsstýringuna:

- `/src/shared/dataaccess/fellanidur/handlers.ts` — `special90Permission` (F90.A) og `specialTerminateBecauseOfVanskilPermission` (011.F). Þessi föll eru skilgreind ofarlega í skjalinu og eru svo notuð á nokkrum stöðum. `special90Permission` er skilgreint á tveimur mismunandi stöðum — hér væri mögulega hægt að nýta isAuthorized fall en það er samt líka verið að skila upplýsingum um hvort notandinn hafi heimild í niðurstöðunum. Skoða betur.
- `/src/shared/dataaccess/fellanidur/fellanidur.ts` — LIF.N assert tékk: athuga hvort notandi hafi LIF.N heimild í assert falli. Skoða hvort þetta sé stórt mál en ætti ekki að vera flókið.
- `/src/shared/dataaccess/fellanidur/innlogn_numera.ts` — ROS.I assert tékk: basic assert tékk hvort notandi hafi ROS.I heimild. Ekki mikið mál.

**Gátlisti**
- □ Greina `special90Permission` og `specialTerminateBecauseOfVanskilPermission` — hvar eru þau notuð?
- □ Heimildir í Heimdalli sem samsvara F90.A, 011.F, LIF.N, ROS.I
- □ Hlutverk/heimild/aðgerð til í Heimdalli
- □ Notendur uppfærðir í Heimdalli — nota gömlu hópana sem viðmið
- □ Ákvarða hvort isAuthorized fall nýtist fyrir handlers.ts
- □ Gömul aðgangsstýring fjarlægð úr öllum þremur skrám
- □ Skoða assert tékkin í fellanidur.ts og innlogn_numera.ts betur
- □ Próf uppfærð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- Allar þrjár fellanidur skrár nota heimildir í Heimdalli
- `special90Permission` og `specialTerminateBecauseOfVanskilPermission` annaðhvort endurskrifuð eða fjarlægð

### moli.ts aðgangsstýring í Heimdall

**Hvað þarf að gera og af hverju?**
Í `/src/shared/model/moli.ts` er verið að nota breyturnar `synAdgangur`, `issuedVisibility` og `editAdgangur` til að senda inn hvaða aðgerð notandi þarf að hafa heimild fyrir. Þetta gæti orðið flókið í útfærslu þar sem það er ekki einhver ákveðin aðgerð sem þarf heldur er farið eftir sölumolanum. Þurfum við þá að breyta einhverju við gögnunum sem er verið að geyma í gagnagrunninum? Þarf að bæta einhverju við eða mappa einhvernvegin saman aðgerðirnar við heimildir í Heimdalli?

Einnig er `user.starfsmadur === 'J'` tékk á sama stað til að athuga hvort notandi sé starfsmaður.

Hægt er að skoða sölumolana með: `select * from vgsolmol` og `select DISTINCT param from vgsolmol where param like '%Adgangur%' and vkodi = '1'`.

Torfi stakk upp á að vera mögulegameð context á editPolicy heimildinni þannig að þetta væri algerlega "agnostic" í kóðanum og sérútfærslur alfarið í heimildakerfinu.

**Gátlisti**
- □ Kortleggja hvaða mola þetta eru sem eru með svona sérstakar aðgangsstýringar
- □ Útbúa einhverjar heimildir til að ná utan um það í nýja kerfinu
- □ Skoða sölumolana í gagnagrunni: hvað eru mismunandi hlutir?
- □ Ákvarða hvernig `synAdgangur`, `issuedVisibility` og `editAdgangur` mappast á heimildir í Heimdalli
- □ Leysa `user.starfsmadur === 'J'` tékk — fjarlægja og nota Heimdall
- □ Gömul aðgangsstýring fjarlægð
- □ Próf uppfærð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- `moli.ts` notar eingöngu heimildir í Heimdalli til að stýra aðgangi að mólum
- Engin `user.starfsmadur` notkun eftir
- Sölumola aðgangsstýring virkar eins og áður frá sjónarhóli notenda

### default_moli editPermission í Heimdall

**Hvað þarf að gera og af hverju?**
Í `/src/shared/model/edit/molar/default_moli.ts` er verið að nota breytuna `editPermission` til að ákvarða hvaða aðgerð notandi þarf að hafa heimild fyrir. Þetta er flókið þar sem verið er að skoða aðgerð út frá molanum sem verið er að vinna með og gæti því orðið flókið í útfærslu. Skoða betur.

Hér er aftur verið að nota aðgerð út frá molanum sem verið er að breyta. Það væri gott að kortleggja sérstaklega þá mola sem eru með svona sérstakar aðgangsstýringar.

Torfi stakk upp á: editPolicy context á heimildinni í Heimdalli — þannig að kóðinn þyrfti líklega bara að tékka á hvort notandinn hafi editPolicy aðgang með vörunúmerið í contexti. Svo þarf að stilla heimildir Heimdalls megin þannig að þær endurspegli þá aðgangsstýringu sem er barna. T.d. þeir sem eiga að vera með TRG.Q séu þá með editPolicy á VARAID='220' etc.

**Gátlisti**
- □ Greina `editPermission` og hvernig það tengist molum
- □ Kortleggja sérstaklega mola sem eru með sérstakar aðgangsstýringar
- □ Skoða hvort editPolicy context nálgunin (Torfi) henti
- □ Ef já: útfæra editPolicy heimild í Heimdalli með vörunúmer sem context
- □ Stilla heimildir í Heimdalli þannig að þær endurspegli gömlu aðgangsstýringuna
- □ Gömul aðgangsstýring fjarlægð
- □ Próf uppfærð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- `default_moli.ts` notar heimildir í Heimdalli til að ákvarða editPermission
- Kóði er "agnostic" gagnvart sérútfærslum — Heimdallur sér um hvaða notandi má breyta hvaða vöru

### persona.ts aðgerðir í Heimdall

**Hvað þarf að gera og af hverju?**
Í `/src/shared/model/edit/vidfong/persona.ts` er verið að tengja saman vöru týpu við aðgerðir (TRG.Q, SLS.A, 360.A) og athuga hvort notandinn hefur heimild fyrir þeirri týpu sem er að koma inn. Gæti verið ágætt að athuga hvort það sé eitthvað hægt að einfalda þetta með nýju aðgangsstýringunni — þetta er allavegana aðeins meira mál en að bara skipta yfir í nýja.

Neðar í skjalinu er `mixinUnisex` fall þar sem verið er að athuga heimild á einfaldan hátt — ætti að vera auðvelt að skipta því út, bara boolean breytu hvort það sé leyfilegt.

Hér þurfum við líklega bara að tékka á hvort notandinn hafi editPolicy aðgang með vörunúmerið í contexti — sama nálgun og í default_moli (Torfi). Svo þarf að stilla heimildir Heimdalls megin þannig að þær endurspegli þá aðgangsstýringu sem er barna, t.d. TRG.Q séu þá með editPolicy á VARAID='220' o.s.frv.

**Gátlisti**
- □ Greina hvernig vöru týpa er tengd við aðgerðir (TRG.Q, SLS.A, 360.A)
- □ Skoða hvort editPolicy context nálgunin (sama og default_moli) eigi við hér líka
- □ Skipta `mixinUnisex` heimild út — einfalt boolean
- □ Heimildir í Heimdalli sem samsvara TRG.Q, SLS.A, 360.A
- □ Gömul aðgangsstýring fjarlægð
- □ Próf uppfærð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- `persona.ts` notar heimildir í Heimdalli í stað gamalla aðgerðakóða
- `mixinUnisex` notar Heimdall
- Vöru-context heimildir virka rétt í Heimdalli
