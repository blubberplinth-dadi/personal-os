# user-client + user-service - Nútímakerfi í Heimdall

> Epic: Hreinsun á gömlum aðgangsstýringarleifum í user-service og user-client.

---

### STM tegund í user-service í Heimdall

**Hvað þarf að gera og af hverju?**
Í user-service er `tegund === 'STM'` notað til að flokka notendur sem starfsmenn þegar þeir eru sóttir og búnir til. Þetta er í `/src/driven/stores/user/index.ts` þar sem 'STM' týpan (ásamt 'STU' og 'UMB') er notuð í SQL query til að sækja starfsmenn. Þessu þarf að hætta þar sem Heimdallur tekur við af tegundaflokkun notenda. Þarf að skoða hvort aðrar tegundir ('STU', 'UMB') hafi áhrif á breytinguna.

**Gátlisti**
- □ Skoða hvernig `tegund === 'STM'` er notað í `/src/driven/stores/user/index.ts`
- □ Ákvarða hvort 'STU' og 'UMB' tegundir þurfi einnig meðhöndlun
- □ Skipta út tegundaathugun fyrir heimild eða hlutverk í Heimdalli
- □ Gömul tegundaathugun fjarlægð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- user-service notar Heimdall til að flokka notendur í stað `tegund === 'STM'`

### Unit test STM tegund í Heimdall

**Hvað þarf að gera og af hverju?**
Í `/src/domain/authentication/login-rs.unit.test.ts` er `tegund === 'STM'` notað til að sækja notandann og athuga tegundina. Þetta er unit test skrá og þarf að uppfæra prófin svo þau endurspegli nýju aðgangsstýringuna eftir að framangreind breyting á user-service hefur verið gerð.

**Gátlisti**
- □ Uppfæra próf í `/src/domain/authentication/login-rs.unit.test.ts` svo þau noti Heimdall í stað STM tegundar
- □ Skoða hvort önnur test skjöl vísa í STM tegund
- □ Öll próf standast

**Done þýðir**
- Unit próf í user-service nota aðgangsstýringu í Heimdalli í stað STM tegundar

### createStarfsmadurUser í Heimdall

**Hvað þarf að gera og af hverju?**
Í user-client er `createStarfsmadurUser` fall í `/src/model/user.ts` sem notar `userJson.starfsmadur`. Þetta fall er mikið notað í prófum um allan kóðabasann. Samkvæmt greiningu Fríðu er þetta eitthvað sem við þurfum að skoða vel þegar við förum að útfæra og jafnvel breyta testum — það er möguleiki að þetta verði bara úrelt hægt og rólega og ef það gerist þá þarf að muna eftir því að fjarlægja þetta fall. Gæti verið eitt af síðustu verkefnunum.

**Gátlisti**
- □ Kortleggja hvar `createStarfsmadurUser` er notað í prófum
- □ Ákvarða hvort hægt sé að fjarlægja fallið eða hvort það þurfi að endurskrifa
- □ Uppfæra eða fjarlægja öll próf sem nota `createStarfsmadurUser`
- □ Fjarlægja `userJson.starfsmadur` úr user-client ef ekkert notar það lengur
- □ Prófað (öll tengd próf standast)

**Done þýðir**
- user-client inniheldur ekki `createStarfsmadurUser` eða `userJson.starfsmadur` leifar af gömlu aðgangsstýringarmynstri
