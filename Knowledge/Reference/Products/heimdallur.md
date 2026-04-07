# Heimdallur

## Framtíðarsýn vöru (e. product vision)

**Skilgreining vandamálsins sem varan á að leysa:** Starfsfólk þjónustuvers og deildarstjórar þurfa að nota mörg ótengd kerfi og töflureikna til að sýsla með aðgangsheimildir starfsfólks. Þetta gerir umsýsluna flókna og ógagnsæja. Endurskoðendur krefjast þess að deildarstjórar geti séð hvaða aðgang starfsfólk þeirra hefur — í dag er það ekki hægt á einum stað.

**Tilgangur:** Einn staður til að sýsla með aðgangsheimildir starfsfólks í öllum tryggingakerfum TM.

**Lykilnotendur:** Starfsfólk þjónustuvers (Nonni), deildarstjórar (Stefanía), hugbúnaðarfólk (Finnur)
**Aðrir notendur:** Allir starfsmenn TM sem þurfa aðgang að tryggingakerfum

**Staða vöruþróunar:** Í stöðugri þróun. V1 í notkun — virkar vel til að skilgreina hlutverk og heimildir en krefst tækniþekkingar. V2 í undirbúningi.

### Umfang og notkun
- Stýrir aðgangsheimildum fyrir Bóthildi, Rósina, Vefsöluna og önnur TM kerfi
- ~120 starfsmenn TM + ytri aðilar (SPATIL, TOYOTA)
- 60 hópar, 820 tengingar notanda-hóps, 44 einstök heimildaauðkenni (í gömlu kerfi)

### Tengd kerfi
- **Bóthildur** — tjónakerfi, þegar tengt við Heimdall
- **Rósin** — tryggingarkerfi, að hluta tengt
- **Vefsalan** — sjálfsafgreiðsla viðskiptavina, að hluta tengt
- **Græna** — eldra AS/400 kerfi, ekki enn tengt
- **Dragon-core** — stærsta þjónustan, 44 heimildaauðkenni, ekki enn tengt

### Þarfir notenda
- Auðvelt að bæta við og fjarlægja aðgang þegar starfsfólk byrjar, hættir eða skiptir um deild
- Skýrar upplýsingar um hvaða aðgang starfsmaður hefur og hvers vegna
- Deildarstjórar geta séð aðgang starfsfólks síns án tæknilegrar aðstoðar
- Hugbúnaðarfólk getur tengt kerfi við Heimdall án mikillar fyrirhafnar
- Forðast „hlutverkasprengjuna" — of mörg hlutverk þegar fínkorna þarf heimildir

### Lykilvirkni
- Leit að starfsfólki og einingum
- Yfirsýn yfir hlutverk, heimildir og tengingar notenda
- Búa til, breyta og eyða hlutverkum og heimildum
- Skoða og sýsla með aðgangsheimildir starfsmanns
- Framselja aðgangsumsýslu til deildarstjóra
- Tenging nýrra kerfa við Heimdall (API)

### Grunnreglur upplifunarinnar (e. experience principles)

- Gagnsæi — hver sem er á að sjá hvaða aðgang hann hefur og hvers vegna
- Einfaldleiki — deildarstjóri á að geta sinnt umsýslu án tækniþekkingar
- Sveigjanleiki — styðja mismunandi gerðir aðgangs án þess að fjöldi hlutverka fari úr böndunum
