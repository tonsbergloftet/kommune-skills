---
name: "laast-designmal"
description: "Oppskrift for en låst designmal i nettleseren: godkjent design ligger fast, bestilleren endrer tekst, sender den tilbake og laster ned trykkfiler i flere formater."
---

# Låst designmal

Oppskrift, ikke ferdig kode. Designet lages på nytt hver gang. Det som er likt på tvers, ligger i byggeklossene (se «Byggeklosser»).

## Hva appen gjør

Et ferdig, godkjent design ligger fast: illustrasjoner, farger, former, plassering. Bestilleren klikker på tekstene og endrer dem rett i designet, ser med en gang om teksten får plass, og laster ned ferdige filer (PDF og PNG, i flere størrelser, med eller uten utfallende kant). Teksten kan kopieres samlet og sendes tilbake til designeren som tilbakemelding.

Designeren slipper å gjøre små tekstendringer for hånd. Bestilleren slipper å vente, og kan ikke ødelegge designet.

**Passer når**
- et sett med ett eller noen få designede elementer (metodekort, prosessplakat, brukerreise, aktørkart, diplom) skal brukes av én bestiller eller en liten gruppe
- designet er godkjent, men teksten er ikke ferdig, eller skal endres over tid
- det trengs trykkfiler i flere størrelser

**Passer ikke når**
- mange skal lage nye ting fra maler. Bruk skillen **plakatgenerator**.
- layouten må endres (flere bokser, flytte elementer). Da må designet endres først.
- flere skal skrive samtidig i samme utgave. Denne appen har ingen server, og endringer lagres bare i nettleseren til den som redigerer.

## Forarbeid

1. **Godkjent design først.** Appen lages etter at bestilleren har godkjent utseendet, i full størrelse og med ekte tekst. Ikke bruk appen til å finne designet.
2. **Del designet opp i lag:** bakgrunn eller papirtekstur, hvert grafiske element for seg (som PNG med gjennomsiktighet, eller SVG) og tekst. Tekst skal aldri ligge i grafikken.
3. **Mål opp hvert tekstfelt** i piksler på det godkjente bildet (96 dpi i valgt grunnformat): posisjon, bredde, fast høyde eller ikke, skrift, størrelse, linjeavstand, maks linjer.
4. **Bestem hva som er låst:** som regel alle etiketter og overskrifter som er del av designet («Hvem deltar?»), og all grafikk.
5. **Bestem formatene:** grunnformat og andre størrelser. Formater med samme sideforhold kan skaleres (A6, A5 og A4 har samme forhold). Et format med annet sideforhold trenger eget oppsett.
6. **Bestem hvilke felt som er samme tekst** flere steder (f.eks. fasenavn på både forside og plakat).

## Spørsmål til bestiller

- Hvem skal redigere, og skal noen andre få filene?
- Hvilke størrelser trengs, og skal noe til trykkeri (utfallende kant, skjæremerker) eller skrives ut på kontoret (flere per ark)?
- Hvilke tekster kan endres, og hvilke er låst?
- Hvor lang kan hver tekst være? Si det i linjer, ikke tegn.
- Hvordan vil du sende tilbake tekst eller kommentarer: kopiere tekst, sende fil, eller bare laste ned ferdig?
- Kommer det flere elementer senere (et kort til)? Da må designet ha plass til det, og koden må gjøre det enkelt.
- Skal filene brukes digitalt også (skjerm, presentasjon, nettside)?

## Funksjoner som skal med

- **Alle elementene i settet på én side**, hvert med navn og egen nedlastingsknapp.
- **Skriving rett i designet**, som ren tekst. Innliming blir ren tekst, og Enter er sperret i enlinjefelt.
- **Utgangsteksten ligger i koden** (ett dataobjekt øverst). Brukerens endringer lagres som et lag oppå (`BK.endringslag`). Oppdateres utgangsteksten, får brukeren den nye teksten i felt hen ikke har endret.
- **Tilbakestill**, med to trykk.
- **Koblede felt:** samme tekst vises flere steder og oppdateres overalt.
- **Overflyt:** hvert felt har maks antall linjer. Titler og enlinjefelt krymper ned til 70 %. Felt som er for lange, markeres rødt, og en liste øverst sier hvor («Kort 2: innledning, maks 4 linjer»). Nedlasting er lov, med varsel.
- **Formatvalg**, husket i nettleseren.
- **Nedlasting:**
  - PDF med alle elementene, én side per element
  - PNG per element, og alle som zip
  - 300 dpi, med tak for iPhone
  - valgfri 3 mm utfallende kant
  - utskriftsark med flere per A4 og skjæremerker, for små formater
- **Kopier tekst:** all tekst, ordnet etter element og felt, med endrede felt markert. Dette er tilbakemeldingen til designeren.
- **Utkast som fil** (lagre og åpne), for å flytte arbeidet til en annen maskin eller sende det til designeren.
- **Beskjed i appen** om at endringer bare lagres i denne nettleseren.
- **Utskriftsråd** ved nedlastingen: skriv ut med «faktisk størrelse» / 100 %, ikke «tilpass til side».

## UI-mønstre

- **Verktøylinje øverst** (klebrig): tittel med én linje forklaring, formatvalg, utfallende, hovedknapp «PDF (alle)», så PNG (zip), Kopier tekst, Utkast og Tilbakestill.
- **Varselfelt under verktøylinjen.** Overflyt står til den er rettet. Andre meldinger kan lukkes.
- **Elementene i en kolonne**, hver med navn og egne knapper til høyre. Stående elementer vises litt mindre enn liggende.
- **Hvert element tegnes i full størrelse** med faste koordinater og skaleres bare i visningen (`forhandsvisning.js`).
- **Redigerbare felt** har tynn ramme ved hover og tydelig ramme ved fokus. Låste tekster har ingen hover.
- **Felt som data:** id, navn (slik brukeren forstår det), enlinjet, maks linjer, låst. Overflytsjekk, kopiering og varsler leser alle fra samme liste.
- **Grafikk som PNG med `mix-blend-mode: multiply`** over papirtekstur når designet er tegnet for hånd. Gjør papirfargen hvit i PNG-ene, så de smelter inn.

## Leveranse og lagring

**Fra designer**
- Det godkjente designet som PNG eller PDF i full størrelse, per element. Brukes som fasit.
- Grafikken som egne filer: SVG for flate former, PNG (minst 2× grunnformatet) for tegnet og malt grafikk. Filnavn etter innhold og element (`kort2-illustrasjon.png`, `etikett-bla.png`).
- Papirtekstur som en sømløs flis.
- Fonter som woff2, med lisens.
- Liste over tekstfelt: id, navn, utgangstekst, maks linjer, låst eller ikke.

**I repoet**
```
index.html     appen: utgangstekst, felt, oppsett per elementtype
grafikk/       alle lag (PNG/SVG)
fonter/        woff2 + LISENS
fasit/         det godkjente designet, til sammenligning
lib/  bk/      biblioteker og byggeklosser
README.md      bruk, endre utgangstekst, legge til element, publisere, utskrift
```

**Hos brukeren**
- Endringer i nettleseren (endringslag med nøkkel som inneholder appnavn og versjon). Bytt versjon bare når feltene endres, ellers mister brukeren arbeidet sitt.
- Utkast som JSON-fil når arbeidet skal flyttes eller deles.

## Byggerekkefølge

1. **Ett element, statisk:** grafikklagene på plass, tekst i felt med faste koordinater. Legg fasiten oppå med 50 % gjennomsiktighet, og juster til de sammenfaller.
2. **Redigering og overflyt** for det elementet. Test med lengste og korteste tekst.
3. **Eksport til PDF og PNG** for det elementet. Skriv ut på papir med 100 % størrelse og sammenlign med fasiten.
4. **Resten av elementene.** Lag én funksjon per elementtype, ikke per element.
5. **Formater, utfallende, utskriftsark.**
6. **Kopier tekst, utkast, tilbakestill, varsler.**
7. **Del med bestilleren tidlig**, gjerne som Claude-artefakt for en rask runde, deretter på GitHub Pages.

Test lokalt med `python3 -m http.server`. Test eksporten i Safari på Mac og iPhone, ikke bare i Chrome.

## Kvalitetssjekker

- **Sammenlign med fasiten:** hvert element, side om side eller lagt oppå. Avvik over noen få piksler rettes.
- **Overflyt:** lengste realistiske tekst i hvert felt, og et langt sammensatt ord. Ingenting skal kuttes uten at feltet er rødt.
- **Lange navn:** aktør-, sted- og enhetsnavn med flere ledd i etiketter, piller og bokser. Dette er særlig viktig i aktørkart og brukerreiser.
- **æøå:** i alle fontsnitt som brukes, i filnavn og i kopiert tekst.
- **Kontrast** på tekst mot bakgrunnen den står på. Minst 4,5:1 for brødtekst, 3:1 for store titler. Er designet godkjent med lavere kontrast, si fra til bestilleren.
- **Bildeoppløsning:** grafikken skal være skarp ved 300 dpi i største format. Zoom inn i PDF-en.
- **Utskrift:** hvert format med 100 % størrelse. Mål med linjal. Med utfallende kant: sjekk at kanten har riktig farge.
- **Utskriftsark:** skjæremerkene treffer kortkantene.
- **Nettlesere:** Chrome, Edge og Safari. iPhone: last ned PNG og PDF.
- **Tilgjengelighet i appen:** alle knapper og felt kan nås med tastatur, synlig fokus, felt har navn (`aria-label`). Grensesnittet skal oppfylle WCAG 2.1 AA.
- **Etter oppdatering av utgangsteksten:** endringer brukeren har gjort, står fortsatt.

## Kjente fallgruver fra første versjon

- **Et format med annet sideforhold ble strukket** (12,5 × 7,5 cm fikk et bredere oppsett der elementene ble skjøvet). Gi formatet eget oppsett, eller la være å tilby det.
- **Linjegrensene lå i tre tabeller** etter elementtype. Legg grensen ved hvert felt i feltlisten.
- **Ulike strategier for tekstpassing** i ulike apper, valgt av KI-assistenten. Bruk `tilpass-tekst.js`: linjetelling og krymping av titler, med samme varsel.
- **Skrift måles ulikt** i Safari (særlig på iPhone) og Chrome. Gi slingringsmonn: titler kan krympe til 70 %, og linjetellingen bruker en terskel på 0,6 linjehøyde.
- **Elementer som flyttes etter teksten** (illustrasjonen ble sentrert i plassen under ingressen) gjør designet uforutsigbart og vanskelig å godkjenne. Bruk faste plasseringer så langt det går.
- **Utfallende kant laget ved å forlenge papirteksturen** virker bare når kanten av designet er tekstur. Går en flate eller illustrasjon helt ut i kanten, må designet tegnes med utfall.
- **Store lerret på iPhone** gir tomt bilde uten feilmelding. `pikselforhold` har et tak på 16 MP.
- **«Tilpass til side»** ved utskrift gjør kortene for små. Si det i appen og i README.
- **Varsler som forsvant av seg selv** etter seks sekunder. La varselet om overflyt stå til det er rettet.
- **Kode som ikke gjorde noe** (en bekreftelse som alltid svarte ja). Bestem regelen («last ned med varsel») og skriv den rett.
- **Endringer lagres bare i én nettleser.** Bestilleren kan tro at teksten er delt. Si det i appen, og tilby kopier tekst og utkast som fil.

## Byggeklosser

Fra repoet med byggeklosser ({{REPO_BYGGEKLOSSER}}):
`redigerbart-felt.js`, `tilpass-tekst.js`, `lagring.js` (særlig `endringslag`), `nedlasting.js`, `eksport.js` (`lagPDF`, `lagZip`, `medUtfall`, `lagUtskriftsark`), `forhandsvisning.js`. Se README der for innlasting, CSS og publisering.

Finnes ikke repoet der du er, skriv tilsvarende kode etter beskrivelsen i README og kommentarene øverst i hver fil.

## Eksempelapp

- Metodekort «Fra elevstemme til handling»: {{EKSEMPEL_LAAST_DESIGNMAL_URL}}
- Kildekode: {{EKSEMPEL_LAAST_DESIGNMAL_REPO}}

Eksempelappen er laget før denne oppskriften og følger den ikke på alle punkter (se fallgruvene). Følg oppskriften der de er uenige.

## Status

Skrevet ut fra første versjon. Første test: brukerreise/aktørkart for Familiehuset. Det som manglet da, legges tilbake her.