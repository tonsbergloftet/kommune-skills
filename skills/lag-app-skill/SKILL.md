---
name: "lag-app-skill"
description: "Metode for å gjøre en app som fungerer om til en gjenbrukbar app-skill (oppskrift) og felles byggeklosser. Bruk når noen vil dele «oppskriften, ikke appen»."
---

# Fra app til app-skill

Prinsipp: **vi deler oppskriften, ikke appen.** Designet lages og hardkodes på nytt hver gang, men etter en skill som sier hva appen skal kunne, hvordan den bygges og hva som må leveres. Kode som ikke avhenger av design, deles som byggeklosser.

Dette er LLP («Lære Lage Prøve») på metanivå: appen er laget, oppskriften skrives ned, og oppskriften prøves ved å bygge en ny app.

## Når

- En app fungerer og er brukt (eller testet) av ekte brukere.
- Det er sannsynlig at noen andre trenger samme *type* app med annet design eller innhold.
- Ikke for engangsapper, og ikke før appen har vært i bruk. En oppskrift fra en app ingen har brukt, inneholder bare antakelser.

## 1. Les og spør

Les all koden, også README, byggeskript og publisering. Les den faktiske koden, ikke beskrivelser av den. Noter alt som tyder på omarbeiding: kommentarer om nettlesere, toleranser, spesialtilfeller, kode som ikke gjør noe, ulike løsninger på samme problem.

Still spørsmål før du skriver noe. Spør særlig:
- Hva var vanskelig, og hva måtte gjøres om?
- Hva har brukerne reagert på, og hva lurer de på?
- Hvilke valg var bevisste, og hvilke ble bare sånn (for eksempel fordi KI-assistenten valgte det)?
- Hvem bestilte, hvem bruker, og hvor havner filene?
- Er dette engangsløsninger, eller noe den neste appen også trenger?
- Hvem skal bruke skillen, og med hvilket verktøy?

Godta «vet ikke». Skriv da det koden viser, og merk det som ikke bekreftet.

## 2. Sorter i tre bunker

Gå gjennom alt appen har: funksjoner, UI-mønstre, datastruktur, filstruktur, sjekker, tekster og publisering.

- **Fast:** skal være med hver gang.
- **Tilpasses:** bestemmes for hver ny sammenheng (design, felt, profil, formater, språk).
- **Tilfeldig:** ble bare sånn, og skal ikke videreføres. **Skriv for hvert punkt hva som skal gjøres i stedet.** Et tilfeldig punkt uten erstatning blir gjentatt.

Vis sorteringen før du går videre, og spør om noe skal flyttes. Sjekk at ingenting er glemt. Det som ikke ble sortert, havner tilfeldig i neste app.

## 3. Skriv app-skillen

Én skill per app-type. Ikke press ulike apper inn i samme skill. Navngi skillen etter hva appen *er* («låst designmal»), ikke etter oppdraget den kom fra («metodekort»). Navnet og beskrivelsen avgjør når skillen blir valgt.

Fast struktur (se malen nederst):
1. Hva appen gjør, og når den passer og ikke passer (nevn andre skills som passer bedre)
2. Forarbeid: hva som må samles inn og bestemmes før man bygger
3. Spørsmål til bestiller
4. Funksjoner som skal med
5. UI-mønstre
6. Leveranse og lagring: hvordan design, logo, fonter, farger og andre elementer leveres og lagres, med mappestruktur
7. Byggerekkefølge: hva lages først, og hvor testes det
8. Kvalitetssjekker
9. Kjente fallgruver fra de første versjonene
10. Byggeklosser som brukes
11. Eksempelapp
12. Status

Regler for teksten:
- Oppskrift og instrukser, ikke ferdig kode. Kodebiter bare der de er kortere enn å forklare.
- Konkrete tall der appen har dem (794 × 1123 px, 76 %, 300 dpi, 16 MP), slik at neste person slipper å finne dem på nytt.
- **Fallgruver skal ha årsak og løsning**, ikke bare navn. Test påstander før de skrives inn. Det som ikke er testet, merkes som antakelse.
- Bruk plassholdere (`{{EKSEMPEL_URL}}`) for lenker som ikke finnes ennå.
- Si at eksempelappen ble laget før oppskriften, og at oppskriften gjelder der de er uenige.

## 4. Skill ut byggeklossene

En byggekloss er kode som **ikke avhenger av design** og som minst to app-typer trenger, eller med stor sannsynlighet vil trenge. Eksempler: eksport, tekstpassing, lagring, nedlasting, QR, bildeopplasting, publisering.

- Liten og avgrenset: én fil, ett ansvar, få avhengigheter.
- Vanlig skript som legger funksjoner på et felles navnerom (`window.BK`), så det virker uten byggesteg og fra disk.
- Kommentar øverst: hva klossen gjør, prinsippet, avhengigheter og kjente svakheter.
- Har to apper løst samme problem på ulike måter, velg én løsning og skriv den som kloss.
- En testside som bruker alle klossene og kan kjøres automatisk. Kjør den hver gang en kloss endres.
- Oppdater README for klossene: oversikt, innlasting, CSS klossene forventer, publisering.

Lag ikke klosser for ting bare én app bruker. Det kan komme senere.

## 5. Harmoniser der det hjelper neste skill

App-skillene kan skille seg fra hverandre. Men der de løser samme ting, bør de løse det likt, så klossene og neste skill passer inn. Gjeldende felles valg:

- **Filstruktur:** `index.html`, `profil/`, `fonter/`, `grafikk/`, `lib/`, `bk/`, eventuelt `bilder/` og `verktoy/`. Biblioteker og fonter som egne filer, ikke base64.
- **Felt som data:** id, navn, enlinjet, maks linjer, type og hjelpetekst, samlet ett sted. Plakat, panel, sjekker og kopiering leser fra samme liste.
- **Design i full størrelse**, skalert bare i visningen. Eksport fra uskalert kopi.
- **Tekstpassing:** krymp til et gulv, så marker og varsle med feltnavn. Nedlasting er lov med varsel.
- **Lagring:** autolagring i nettleseren for tekst og valg, utkast som fil for bilder og deling.
- **Eksport:** fast dpi, tak på pikselstørrelse, valgfri utfallende kant, filnavn med æøå omskrevet.
- **Sider:** et dokument har én eller flere sider. Det dekker bakside, kortsett og flersidige maler.
- **Varsler** i appen, ikke `alert()`.
- **Teknisk standard:** én HTML-side uten backend eller database, GitHub Pages, lagring i nettleseren.
- **Tilgjengelighet:** grensesnittet skal oppfylle WCAG 2.1 AA. Kontrasten i designet sjekkes, men profilen avgjør.

Når en ny skill trenger et nytt felles valg, legg det til her.

## 6. Ferdig først når den er prøvd

En app-skill er **ikke ferdig** når den er skrevet. Den er ferdig når noen har bygget en ny app med den, i en ny sammenheng.

Ved første bruk:
1. Bygg den nye appen bare med skillen og klossene. Ikke se i den gamle koden med mindre skillen viser dit.
2. Noter underveis: hva manglet, hva var feil, hva måtte du spørre om, hva var overflødig.
3. Legg det tilbake i skillen: nye spørsmål, fallgruver og sjekker. Fjern det som ikke trengtes.
4. Kode som ble skrevet på nytt og ikke avhenger av design, blir ny eller endret byggekloss.
5. Oppdater **Status** med hvilke apper skillen er prøvd på.

Hver ny app gjør oppskriften bedre. Skill nummer tre, fire og fem skal gå raskere enn de to første.

## Format og verktøy

- Skriv skillen som `SKILL.md` med frontmatter (`name`, `description`) og vanlig markdown. Det fungerer som skill i Claude, og kan limes inn som instruksjon i ChatGPT og Copilot.
- Copilot tåler mindre tekst og følger lange instrukser dårligere. Gi den én del om gangen (forarbeid, så én mal, så eksport), og lim inn byggeklossene som filer.
- Skriv på bokmål, konsist, uten salgsspråk.

## Mal for en app-skill

```markdown
---
name: <app-type>
description: Oppskrift for å lage <hva> i nettleseren som <gjør hva for hvem>. Bruk når <situasjon>.
---

# <App-type>

Oppskrift, ikke ferdig kode. …

## Hva appen gjør
**Passer når** …
**Passer ikke når** … (bruk heller skillen …)

## Forarbeid
1. …

## Spørsmål til bestiller
- …

## Funksjoner som skal med
- …

## UI-mønstre
- …

## Leveranse og lagring
**Fra bestiller eller designer** …
**I repoet** (mappestruktur) …
**Hos brukeren** …

## Byggerekkefølge
1. …
Hvor det testes: …

## Kvalitetssjekker
- Kontrast, overflyt, æøå, lange navn, bildeoppløsning, utskrift, nettlesere, mobil, tilgjengelighet …

## Kjente fallgruver fra første versjon
- **<Hva skjedde>.** <Hvorfor>. <Gjør dette i stedet>.

## Byggeklosser
…

## Eksempelapp
- {{EKSEMPEL_URL}}

## Status
Skrevet ut fra første versjon. Ikke prøvd på en ny app ennå.
```