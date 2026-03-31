# Heimdallur

## Framtíðarsýn vöru (e. product vision)

**Skilgreining vandamálsins sem varan á að leysa:** Aðgangsstýring að tryggingakerfum TM er dreifð á mörg kerfi og erfitt að hafa yfirsýn yfir hverjir hafa aðgang að hverju. Notendaþjónusta þarf að vinna í mörgum kerfum til að veita og afturkalla aðgang. Forstöðumenn deilda geta ekki auðveldlega séð hvaða aðgang starfsfólk þeirra hefur - sem er krafa frá endurskoðendum.

**Tilgangur:** Miðlægt kerfi til að stýra aðgangi og heimildum starfsfólks í öllum tryggingakerfum TM.

**Lykilnotendur:** Notendaþjónusta, forstöðumenn deilda
**Aðrir notendur:** Allir sem þurfa að skoða aðgangsupplýsingar

**Staða vöruþróunar:** Í stöðugri þróun

### Þarfir notenda

**Notendaþjónusta (Nonni):**
- Veita nýjum starfsmanni réttan aðgang og heimildir í tryggingakerfum
- Fjarlægja aðgang og heimildir þegar starfsmaður hættir
- Uppfæra aðgang og heimildir núverandi starfsmanns
- Stofna og uppfæra Hlutverk (safn af Heimildum)
- Stofna og uppfæra Heimild (safn af Aðgerðum)

**Forstöðumenn (Stefanía):**
- Skoða aðgang starfsfólks sinnar deildar
- Skoða heimildir ákveðins starfsmanns
- Skoða starfsfólk með ákveðinn aðgang eða heimildir
- Fá yfirlit til að uppfylla kröfur endurskoðenda

### Lykilvirkni

- Notendaumsýsla (stofna, uppfæra, afvirkja)
- Hlutverkaumsýsla (stofna, uppfæra, úthluta)
- Heimildaumsýsla (stofna, uppfæra, tengja við hlutverk)
- Umboðaumsýsla (aðili veitir öðrum aðgang að sínum gögnum)
- Leit að notendum, hlutverkum og heimildum
- Yfirsýn yfir aðgang starfsfólks (fyrir forstöðumenn)

### Grunnreglur upplifunarinnar (e. experience principles)

- Skýrt og einfalt fyrir daglega notkun
- Góð yfirsýn fyrir stjórnendur og endurskoðendur
- Öruggt - breytingar skráðar og rekjanlegar

### Hugtakamódel

```
Notandi → Hlutverk → Heimild → Aðgerð
```

| Hugtak | Lýsing |
|--------|--------|
| **Notandi** | Starfsmaður eða kerfisnotandi sem þarf aðgang |
| **Hlutverk** | Safn af heimildum sem tilheyra ákveðnu starfi (t.d. "Tjónafulltrúi") |
| **Heimild** | Leyfi til að framkvæma ákveðnar aðgerðir (t.d. "Skoða tjón") |
| **Aðgerð** | Tæknileg aðgerð í kerfi (t.d. read:claims, write:payment) |
| **Umboð** | Þegar aðili veitir öðrum aðgang að sínum gögnum |

### Tengsl við önnur kerfi

Heimdallur á að sjá um aðgangsstýringu fyrir:
- Bóthildur (tjónakerfi)
- Rósin (tryggingaumsýsla)
- Vefsala TM (netverslun)
- Önnur innri kerfi TM

**Núverandi staða:** Ekki öll kerfi hafa verið uppfærð til að nota Heimdall - sum nota enn eigin aðgangsstýringu.
