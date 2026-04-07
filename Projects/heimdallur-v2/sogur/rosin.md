# rosin - Nútímakerfi í Heimdall

> Epic: Bæta við nýju aðgangsstýringunni í Rósina og fjarlægja gömlu úr kóða Rósarinnar. Dragon-core breytingar eru í sérstöku epic.

---

### Aðgangsstýring þjónustunnar (rosin) í Heimdall

**Hvað þarf að gera og af hverju?**
Í `/server/startService.ts` eru aðgerðirnar TRG.G og TIN.K sendar inn í `user.hasAnyAccess` sem listi til að aðgangsstýra þjónustunni sjálfri. Aðgangsstýringin er sett inn við skilgreiningu þjónustunnar. Þetta þarf að skipta út fyrir aðgangsstýringu í Heimdalli.

**Gátlisti**
- □ Skipta `user.hasAnyAccess` í `/server/startService.ts` út fyrir heimild í Heimdalli
- □ Ákvarða hvort TRG.G og TIN.K eigi að vera ein eða tvær heimildir í Heimdalli
- □ Notendur uppfærðir í Heimdalli — nota gömlu hópana sem viðmið (margir hópar eru með TRG.G; NTIAPI er með TIN.K)
- □ Gömul aðgangsstýring fjarlægð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- Aðgangsstýring þjónustunnar (rosin) notar Heimdall í stað `user.hasAnyAccess(['TRG.G', 'TIN.K'])`
- Notendur sem áttu aðgang áður hafa aðgang í gegnum hlutverk í Heimdalli

### isAuthorized fall í Heimdall

**Hvað þarf að gera og af hverju?**
Í `/app/scripts/authUtils.ts` er `isAuthorized` fall sem inniheldur gömlu aðgangsstýringuna. Fallið athugar `user.starfsmadur`, `tegund`, og hvort `kennitala` sé kennitala notanda eða maka, og kastar villu ef notandi hefur ekki heimild. Þetta fall er notað á nokkrum stöðum í rósinni (m.a. í `restdataservice`) og væri fínt að skipta bara þessu eina falli út fyrir aðgangsstýringu í Heimdalli og halda svo áfram að nota það fall í Rósinni (ef mögulegt).

**Gátlisti**
- □ Greina hvaða athuganir `isAuthorized` gerir (starfsmadur, tegund, kennitala, kennitalaMaka)
- □ Ákvarða hvaða heimildir í Heimdalli taka við af þessum athugunum
- □ Endurskrifa `isAuthorized` svo það noti Heimdall í stað gamalla athugana
- □ Skoða alla staði sem kalla `isAuthorized` og tryggja samhæfni
- □ Gömul rökfræði fjarlægð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- `isAuthorized` fallið í `authUtils.ts` notar heimildir í Heimdalli í stað `user.starfsmadur`, `tegund`, og `kennitala` athugana

### ROS.T heimild í Heimdall

**Hvað þarf að gera og af hverju?**
Í `/server/rest/restdataservice.ts` er verið að athuga ROS.T heimild í get tilboðsheimild/:kt endapunkti til að skila `mafanytttilbod: true` ef viðskiptavinur/notandi hefur ROS.T. Annars eru upplýsingar um það sóttar í gagnagrunninn. Þetta er bara test heimild svo það ætti að vera lítið mál að breyta þessu.

**Gátlisti**
- □ Aðgerð/heimild til í kóða (ROS.T eða sambærileg heimild í Heimdalli)
- □ Hlutverk/heimild/aðgerð til í Heimdalli
- □ Notendur uppfærðir í Heimdalli — nota gömlu hópana sem viðmið (ROSTEST hópur er með ROS.T)
- □ Gömul aðgangsstýring fjarlægð úr `/server/rest/restdataservice.ts`
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- `restdataservice.ts` notar Heimdall til aðgangsstýringar í stað `user.hasAccess('ROS.T')`
- Notendur sem voru í ROSTEST hóp hafa aðgang í gegnum hlutverk í Heimdalli

### ROS.I og starfsmaður í Heimdall

**Hvað þarf að gera og af hverju?**
Í `/app/modules/actionlist/actionlist.ts` er verið að athuga hvort notandi sé með ROS.I og er því skilað sem boolean breytu. `hasInnlognExtraAccess` í `includeOnlyIf` fallinu athugar hvort notandi hafi ROS.I heimild. Einnig er `user.starfsmadur` notað til að ákvarða skilagerð í `isStarfsmadurOrTilbod` fallinu. `allowIn` inniheldur líka fall sem tekur inn scope og skilar boolean breytu hvort notandi hafi heimild. Þetta er flóknara en flest og þarf vandlega skoðun.

**Gátlisti**
- □ Greina `includeOnlyIf`, `allowIn`, og `isStarfsmadurOrTilbod` föll
- □ Skipta `hasInnlognExtraAccess` (ROS.I) út fyrir heimild í Heimdalli
- □ Skipta `user.starfsmadur` athugun í `isStarfsmadurOrTilbod` út fyrir Heimdall
- □ Notendur uppfærðir í Heimdalli — nota gömlu hópana sem viðmið (INNLOGN hópur er með ROS.I)
- □ Gömul aðgangsstýring fjarlægð
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- `actionlist.ts` notar heimildir í Heimdalli í stað `user.hasAccess('ROS.I')` og `user.starfsmadur`
- Notendur sem voru í INNLOGN hóp hafa aðgang í gegnum hlutverk í Heimdalli

### Frontend user.starfsmadur í Heimdall

**Hvað þarf að gera og af hverju?**
Í mörgum frontend modules í rósinni er `user.starfsmadur` notað til að ákvarða hvort notandi sé starfsmaður og birta eða fela virkni eftir því. Þetta er notað í a.m.k. 7 skrám: `/app/modules/tjonasaga/tjonasaga.js` (tjónasaga), `/app/modules/customer/customer.js` (sundurliðun virðiseinkunnar og starfsmanna aðgangur), `/app/modules/masval_tryggingar/mas_pakki.js` (aðgerðir starfsmanns), `/app/modules/masval_tryggingar/mas_skirteini.js` (skírteini/tilboð, nav.allow), `/app/modules/vanskil/vanskil.js` (vanskilabirting), `/app/scripts/services/user.ts` (birta upplýsingar), og `/app/scripts/controllers/mas_val.js` (fullan les aðgang). Í öllum tilfellum ætti Heimdallur að stýra þessu.

**Gátlisti**
- □ Fara yfir hverja skrá og ákvarða hvaða heimild í Heimdalli tekur við
- □ Skipta `user.starfsmadur` út fyrir heimild í Heimdalli í hverri skrá
- □ Skoða hvort `nav.allow` í `mas_skirteini.js` þurfi sérstaka meðhöndlun
- □ Gömul `user.starfsmadur` notkun fjarlægð úr öllum 7 skrám
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- Engin `user.starfsmadur` notkun eftir í frontend modules rósinarinnar
- Heimdallur stýrir hvort notandi sjái viðeigandi virkni

### Frontend aðgerðaheimildir í Heimdall

**Hvað þarf að gera og af hverju?**
Þrjár skrár í rósinni nota `hasAccess` með aðgerðakóðum: `/app/modules/adgerdir/adgerdir.js` (TRG.X — boolean breyta sem verið er að skila), `/app/modules/sambond/Atvinna/atvinna.ts` (TRG.A — athuga hvort eigi að sýna atvinnu flokk), og `/app/modules/vidfong/ahaettuskodun/ahaettuskodun.html` (133.A — heimild athuguð inni í html-inu sjálfu). Allt þetta ætti að vera einfalt að skipta nema 133.A í html sem þarf nánari skoðun.

**Gátlisti**
- □ Aðgerðir/heimildir til í kóða (TRG.X, TRG.A, 133.A eða sambærilegar heimildir í Heimdalli)
- □ Hlutverk/heimild/aðgerð til í Heimdalli
- □ Notendur uppfærðir í Heimdalli — nota gömlu hópana sem viðmið (aur, HENRY, UTGLOK eru með TRG.X; LIFUTG, ÚtgHeim eru með TRG.A; FASANSK, ÚtgHeim eru með 133.A)
- □ Skoða 133.A í html skrá sérstaklega og ákvarða bestu leið
- □ Gömul aðgangsstýring fjarlægð úr öllum þremur skrám
- □ Prófað (kóði + aðgangur)

**Done þýðir**
- `adgerdir.js`, `atvinna.ts` og `ahaettuskodun.html` nota heimildir í Heimdalli í stað gamalla hasAccess athugana
- Notendur sem voru í viðeigandi hópum hafa aðgang í gegnum hlutverk í Heimdalli
