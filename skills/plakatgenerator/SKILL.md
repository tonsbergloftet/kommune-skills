---
name: "plakatgenerator"
description: "Oppskrift for å lage en plakatgenerator i nettleseren som gir profilriktige plakater fra faste maler. Bruk når ansatte selv skal lage plakater etter grafisk profil."
---

# Plakatgenerator

Oppskrift, ikke ferdig kode. Designet lages på nytt for hver virksomhet. Det som er likt på tvers, ligger i byggeklossene (se «Byggeklosser»), og den koden kan gjenbrukes.

## Hva appen gjør

Ansatte velger en mal, skriver tekst rett i plakaten, velger bilde og farge innenfor profilen og laster ned en ferdig fil. De kan ikke gjøre noe som bryter med profilen: logo, ramme og designelementer er låst, og fargene er bare de lovlige.

**Passer når**
- mange ansatte lager plakater, oppslag eller infoskjermbilder, og resultatet varierer i kvalitet
- profilen har tydelige regler (farger, fonter, logo, faste elementer)
- innholdet har kjente typer: budskap, invitasjon, oversikt, veileder, rutine, skilt

**Passer ikke når**
- det trengs fri layout eller mange unike trykksaker. Da er en designer eller Canva/InDesign-maler bedre.
- én person skal justere tekst i ett bestemt, godkjent design. Bruk skillen **låst designmal**.
- innholdet er lange dokumenter. Bruk en dokumentmal.

## Forarbeid

Gjør dette før koden. Det er her de fleste valgene tas.

1. **Samle det som finnes:** 10–20 eksisterende plakater (gode og dårlige), grafisk profil, Word- eller InDesign-maler, logo i vektor, fonter med lisens, faste designelementer (bølger, rammer, mønstre).
2. **Sorter plakatene etter formål**, ikke utseende. Hver gruppe er en kandidat til en mal. Typisk 4–6 maler. Flere enn 8 gjør valget vanskelig.
3. **Bestem formater:** A4 stående er nesten alltid med. Vanlige tillegg: 16:9 for infoskjerm, A3, kvadrat for sosiale medier.
4. **Tegn malene** i et designverktøy, i full størrelse, med ekte eksempeltekst i lang og kort versjon. Godkjenn dem med bestiller før koding.
5. **For hver mal:** skriv ned feltene i rekkefølge, maks lengde (i ord eller linjer), og hvilke felt som kan stå tomme.
6. **Bilder:** finnes det en bildebank med klarert bruksrett? Hvem fyller den, og når utløper rettighetene?

## Spørsmål til bestiller

- Hvem skal bruke generatoren, og på hvilke maskiner (Windows/Edge, Mac, iPad)?
- Hvilke formater, og skal noe til trykkeri (krever utfallende kant) eller bare kontorskriver?
- Hvilke maler, og hvilke felt i hver? Hva er maks lengde på tittel?
- Hvilke fargekombinasjoner er lovlige? Er det regler for tekst på bilde?
- Skal det være bildebank? Hvem eier den, og kan bildene publiseres offentlig?
- Trengs QR-kode? Skal den peke til en fast side eller skrives inn hver gang?
- Skal plakaten kunne ha to sider (forside og bakside)?
- Hvilke språk skal plakatene lages på? Arabisk og andre skrifter som leses fra høyre krever egen tilpasning.
- Skal KI-genererte bilder merkes? Er det lov å bruke dem?
- Hvor skal appen ligge (GitHub-konto eller -organisasjon), og hvem vedlikeholder den etterpå?

## Funksjoner som skal med

- **Maler:** valg av mal med miniatyrer laget med samme kode som plakaten.
- **Format:** veksling mellom formatene. Teksten beholdes når mal eller format byttes.
- **Skriving rett i plakaten:** klikk på en tekst for å endre den. Tomme felt viser grå hjelpetekst og kommer ikke med i den ferdige plakaten.
- **Alle tekstfelt også i sidepanelet**, sammenfoldet. Det er reserven for skjermleser og lange tekster. De to visningene oppdaterer hverandre.
- **Tekstpassing:** teksten krymper for å passe (til 76 % av grunnstørrelsen). Får den fortsatt ikke plass, markeres feltet og panelet varsler med feltnavn. Nedlasting er lov, men varselet står til feilen er rettet.
- **Utheving:** `**ord**` gir uthevet ord i profilfarge i brødtekst.
- **Farger:** bare profilens farger, hver med en lys og en mørk variant som malene bruker.
- **Bilder:** last opp eget bilde, velg fra bildebanken, juster utsnittet (fokuspunkt). Klikk på bildet i plakaten åpner bildevalget.
- **QR-kode** fra nettadressen på plakaten, med valgfri tekst ved siden av.
- **To sider:** en mal kan ha flere sider, hver med egen layout og egne felt. PDF-en får alle sidene. PNG-en får siden som vises.
- **Nedlasting:** PDF for utskrift, PNG i høy oppløsning. Skjermformat i 1920 × 1080.
- **Utkast:** lagres som fil, med bildene, og kan åpnes igjen. Teksten lagres også i nettleseren mens man jobber.
- **Varsel ved nedlasting** hvis plakaten fortsatt har eksempelbilde eller eksempeltekst.
- **KI-merke** på bildet (valgfritt, etter bestillers regler).
- **Kort forklaring** første gang (tre steg: panelet, skriv i plakaten, klikk på bildet). Kan åpnes igjen med «Slik virker det».
- **Zoom:** tilpass, 100 %, 150 %. **Skjul tomme felt** for å se plakaten slik den blir.

## UI-mønstre

- **Oppsett:** sidepanel til venstre (ca. 340 px) med nummererte steg: 1 Mal, 2 Format, 3 Bilde, 4 Farge, 5 QR, 6 Last ned. Utkast og «Alle tekstfelt» nederst.
- **Plakaten tegnes i full størrelse** (A4 = 794 × 1123 px, 16:9 = 1280 × 720 px) og skaleres bare med `transform` i visningen. Eksporten tas fra en uskalert kopi.
- **Malene som funksjoner:** hver mal er en funksjon som tar format og tilstand og returnerer HTML/SVG. Faste posisjoner i piksler for boksene. All typografi inni en boks i `em`, slik at tekstpassingen bare endrer boksens skriftstørrelse.
- **Bakgrunn og bilder i SVG** (ramme, bølge, bildeformer som `clipPath`). Tekst i HTML-bokser oppå.
- **Felt som data:** én liste med felt (id, navn, enlinjet, maks linjer, hjelpetekst, type: tekst, utheving, liste, «Etikett: verdi»). Både plakat, panel og sjekker leser fra den.
- **Mal-definisjon som data:** navn, kort beskrivelse, antall bilder, felt per side.
- **Varsler i panelet**, ikke `alert()`. Bekreftelser som en knapp som endrer tekst («Sikker? Trykk igjen»).
- **Synlig fokus** på alle knapper og felt. Klikkbare deler av plakaten har hover-markering og `title`.
- **Mobil:** appen trenger ikke kunne redigeres på telefon, men skal kunne åpnes og laste ned uten å feile.

## Leveranse og lagring

**Fra bestiller eller designer**
- Logo som SVG (og PNG med høy oppløsning som reserve), i de variantene profilen tillater.
- Fonter som woff2, med lisens. Bare snittene som faktisk brukes.
- Farger som hex, med navn og regler (hvilken tekstfarge på hvilken bakgrunn).
- Faste designelementer som SVG, eller som punktlister/kurver hentet fra maldokumentet.
- Malene som PDF i full størrelse, gjerne også som kilde (InDesign, Figma, Word).
- Eksempeltekst og eksempelbilder som kan publiseres.

**I repoet**
```
index.html            generatoren
profil/farger.md      fargekoder og regler
profil/logo.svg
fonter/               woff2 + LISENS
grafikk/              låste elementer
maler/                godkjente skisser (PDF/PNG) som appen sammenlignes med
lib/  bk/             biblioteker og byggeklosser
bilder/               bildebank (valgfritt) + bildeinfo.csv. Bare bilder rett i mappen blir med.
grafikk/eksempelbilder/  eksempelbilder (ikke i bilder/, da publiseres de ikke)
verktoy/bildebank.py  .github/workflows/publiser.yml
README.md             bruk, oppdatering av bilder, publisering
```
Ikke base64 inne i `index.html`. Da blir fila stor (over 1 MB) og vanskelig å endre for både mennesker og språkmodeller.

**Hos brukeren**
- Tekst og valg autolagres i nettleseren (`lagring.js`, nøkkel med appnavn og versjon).
- Utkast med bilder lagres som JSON-fil. Bilder fra bildebanken lagres som id og hentes på nytt ved åpning. Mangler bildet, brukes en plassholder med beskjed.

### Alternativ: maler fra InDesign (ikke prøvd ennå)

Tanken er at designeren leverer hver mal som PDF + IDML, og at en språkmodell gjenskaper malen presist i HTML. Det krever avtalte regler:
- Tekstrammer har navn som er lik felt-id (`tittel`, `ingress`, `tx1` …). Låste elementer ligger på eget lag.
- Typografi ligger i navngitte avsnittsstiler. Ingen lokal formatering.
- Farger er navngitte fargeprøver med samme navn som i `profil/farger.md`.
- Én side per format, i riktig størrelse.

IDML er en zip med XML: geometrien står i `Spreads/*.xml`, teksten i `Stories/*.xml` og stilene i `Resources/Styles.xml`. PDF-en brukes som fasit for å sammenligne. Første gang dette prøves: les begge, lag malen, legg den oppå PDF-en med 50 % gjennomsiktighet og noter avvik.

## Byggerekkefølge

1. **Én mal, ett format, statisk.** Profilmappe, fonter og logo på plass. Legg den godkjente skissen oppå med 50 % gjennomsiktighet og juster til de sammenfaller.
2. **Felt som data, skriving i plakaten, tekstpassing.** Test med den lengste realistiske teksten og med tomme felt.
3. **Eksport til PNG og PDF.** Skriv ut på papir med 100 % størrelse tidlig. Sjekk mål, skarphet og farger.
4. **Resten av malene**, deretter neste format. Miniatyrene kommer gratis.
5. **Bilder:** opplasting, utsnitt, plassholder. Deretter bildebank og publisering med GitHub Actions.
6. **Utkast, QR, to sider.**
7. **Panelets detaljer:** varsler, forklaring første gang, zoom, «Skjul tomme felt».
8. **Publiser og test hos brukerne.** Se hvordan de faktisk bruker den, og noter hva de lurer på.

Test lokalt med en enkel webserver (`python3 -m http.server`), ikke ved å åpne fila direkte. Bildebanken virker ikke fra `file://`.

## Kvalitetssjekker

- **Kontrast:** all tekst mot bakgrunnen den faktisk står på, også tekst på bilde og på hver slørfarge. Minst 4,5:1 for brødtekst, 3:1 for store titler. Er profilen strengere eller løsere, gjelder profilen, men noter avviket.
- **Overflyt:** lengste realistiske tittel, et langt sammensatt ord («Foreldreveiledningskurs»), en lang nettadresse, alle felt fylt.
- **Lange navn:** person-, sted- og enhetsnavn med bindestrek og flere ledd («Seksjon for oppvekst og kvalifisering – Familiehuset»), i stikktittel, kontaktboks og lenketekst. Ingenting skal kuttes uten at feltet er markert.
- **æøå og andre språk:** i fonten (alle snitt), i filnavn, i QR-kode. Test minst én plakat på et språk som ikke bruker latinsk alfabet, hvis det er aktuelt.
- **Tomme felt:** ingen tomme bokser, streker eller luker i den ferdige plakaten.
- **Bildeoppløsning:** varsle når et bilde gir under 150 dpi på trykk (`BK.effektivDpi`). Test med et lite mobilbilde.
- **Utskrift:** A4 på kontorskriver med 100 % størrelse. Mål logo og marger med linjal.
- **QR:** skann den utskrevne plakaten med både iPhone og Android, på armlengdes avstand.
- **Nettlesere:** Edge og Chrome på Windows, Safari på Mac. iPhone: åpne og last ned.
- **Tilgjengelighet i appen:** alt kan nås med tastatur, synlig fokus, felt har navn (`aria-label`), dialoger kan lukkes med Esc, bevegelse respekterer `prefers-reduced-motion`. Grensesnittet skal oppfylle WCAG 2.1 AA.
- **Eksportfilene:** riktig sidestørrelse i PDF-en, ingen redigeringsmarkeringer eller hjelpetekst i filen.

## Kjente fallgruver fra første versjon

- **Alt som base64 i én fil.** Fonter (ti snitt, fem av dem ubrukt), logo, eksempelbilder og biblioteker ble lagt inn i `index.html`, og README sa «ikke rediger for hånd» uten at det fantes noe byggesteg. Legg filene i mapper.
- **Tegn ikke etter vindusbredden.** Lag plakaten i full størrelse og skaler bare visningen. Ellers blir tekstpassing og eksport forskjellig fra det brukeren ser.
- **Mål tekst først etter at fontene er lastet** (`document.fonts.ready`), og bruk `font-display: block`. Ellers er tekstpassingen feil første gang.
- **Ikke bygg plakaten på nytt mens brukeren skriver.** Da mister feltet fokus. Bygg på nytt når feltet forlates. Nettadressen er unntaket, fordi QR-koden må lages på nytt: bygg da, og sett fokus på feltet brukeren klikket på.
- **Ulike strategier for tekstpassing.** KI-assistenten valgte forskjellige løsninger i ulike apper. Bruk én: `tilpass-tekst.js`.
- **Lange ord og adresser** sprenger bredden. Tillat orddeling i titler bare når ordet ellers ikke får plass, og varsle. Sett inn mulige brudd etter `/` og `.` i nettadresser.
- **Side 2 ble hardkodet** for én mal med egne felt. Bygg flere sider inn i mal-definisjonen fra start.
- **Malnavn etter opphav** («Som ICDP-plakaten», «eksempel 01») sier ikke brukeren noe. Gi malene navn etter bruk.
- **KI-genererte eksempelbilder** kan bli med på ferdige plakater. Bytt dem ut med bilder fra bildebanken når den finnes, og varsle ved nedlasting.
- **Bilder fra andre domener** kommer ikke med i eksporten. Gjør om alle bilder til data-URL (`bildeopplasting.js`, `hentBildebankBilde`).
- **QR-biblioteket koder som latin-1.** æøå går bra, men arabisk og tigrinja blir uleselig. `qr.js` setter UTF-8.
- **Store lerret på iPhone** gir tomt bilde uten feilmelding. `pikselforhold` har et tak.
- **`alert` og `confirm`** stopper siden og fungerer dårlig i innebygde visninger. Vis varsler i panelet.
- **Bildebanken er offentlig** på GitHub Pages. Bare klarerte bilder i `bilder/`.

## Byggeklosser

Fra repoet med byggeklosser ({{REPO_BYGGEKLOSSER}}):
`tilpass-tekst.js`, `redigerbart-felt.js`, `lagring.js`, `nedlasting.js`, `eksport.js`, `qr.js`, `bildeopplasting.js`, `forhandsvisning.js`, `bildebank/`. Se README der for innlasting, CSS og publisering.

Finnes ikke repoet der du er, skriv tilsvarende kode etter beskrivelsen i README og kommentarene øverst i hver fil.

## Eksempelapp

- Plakatgenerator for Tønsberg kommune: {{EKSEMPEL_PLAKATGENERATOR_URL}}
- Kildekode: {{EKSEMPEL_PLAKATGENERATOR_REPO}}

Eksempelappen er laget før denne oppskriften og følger den ikke på alle punkter (se fallgruvene). Følg oppskriften der de er uenige.

## Status

Skrevet ut fra første versjon. Ikke prøvd på en ny app ennå. Når noen har bygget en ny plakatgenerator med den, legg det som manglet tilbake her.