---
name: "tonsberg-prototype"
description: "Lag klikkbare prototypenettsider i Tønsberg kommunes nettsidestil (tonsberg.kommune.no) som én HTML-fil, til brukertesting lokalt eller på GitHub Pages."
---

# Prototypenettside i Tønsberg kommune-stil

Bruk denne når noen vil teste en ny nettside, portal eller temaside for Tønsberg kommune på brukere **før** den bygges i Acos. Resultatet er én selvstendig HTML-fil som ser ut som tonsberg.kommune.no.

Målet er å teste **innhold, struktur og språk**, ikke ny funksjonalitet. Prototypen skal bare inneholde det redaktører faktisk kan lage i Acos på kommunens nettside i dag.

Komponentlisten under er kontrollert mot tonsberg.kommune.no (portalsiden «Alt i meg», artikkelen «Den voksnes rolle», kategorisiden «Barn, ungdom og familie», tjenestesiden «Helsestasjon for barn 0–5 år», «Vakttelefoner» og forsiden) i november 2026. Portalsidens sirkler, tittel og lenkefliser er i tillegg justert etter portalsiden «Innovasjon – å jobbe på nye måter» (26.11.2026).

## Ufravikelige regler

1. **Bruk bare komponentene i katalogen under.** Ikke finn på nye elementer (chatbot, filterpaneler, faner, karuseller, kart, quiz, kort med tall, fargede varselbokser, knapper, animasjoner, dashbord) med mindre brukeren eksplisitt ber om det. Passer ikke innholdet i katalogen, spør brukeren i stedet for å improvisere. Hvis brukeren likevel vil ha et nytt element, merk det i koden med `<!-- FINNES IKKE I ACOS -->` og nevn det når du leverer.
2. **Bruk komponentene slik kommunen bruker dem** (se «Brukes til» i katalogen). For eksempel er den grønne rammeboksen bare for ingressen på artikler, ikke en fri boks.
3. **Start alltid fra startmalen `mal.html` i samme mappe som denne filen.** Behold CSS-en, logoen, toppen, bølgen og bunnen uendret. Endre bare innholdet i `<main>`, `TOPICS`, `CRUMBS` og `PORTAL`.
4. **Kommunens topp og bunn er pynt.** Min side, Kart, Kontakt oss, Søk, Meny og alt i bunnen kan ikke klikkes. Søk virker ikke.
5. **Testerne skal holde seg inne i prototypen.** Alle lenker ut av prototypen skrives som `<span class="fake">…</span>`. Eksterne nettsider får i tillegg klassen `ext` (pil-ikon, som på kommunens sider): `<span class="fake ext">Helsenorge</span>`. Telefonnumre og e-post: `<span class="fake">`. Bare interne lenker (`href="#id"`) er klikkbare.
6. **Én fil, ingen byggesteg, ingen database.** Ingen rammeverk og ingen eksterne skript. Eneste eksterne ressurs er Inter fra Google Fonts. Tilbakemeldinger lagres ikke.
7. **Ingen personopplysninger.** Bruk fiktive eller generiske eksempler. Ekte navn på kontaktpersoner bare hvis brukeren gir dem.
8. **Norsk bokmål og klarspråk.** Korte setninger, «du» til leseren, aktive verb, fagord forklart første gang.

## Sidetyper på kommunens nettside

| Sidetype | Eksempel | Innhold, i rekkefølge |
|---|---|---|
| Kategoriside | Barn, ungdom og familie | Brødsmuler, `h1`, lenkefliser. Ingenting annet. |
| Portalside | Alt i meg, Helsestasjon, Innovasjon | Dekorsirkler i bakgrunnen (ligger i malen), brødsmuler, `h1` i merkefarge (`section.page.page-portal`), ingress i full bredde (avsnitt, eventuelt en kort punktliste), lenkefliser, eventuelt nyhetsliste. |
| Artikkel/tjenesteside | Den voksnes rolle, Helsestasjon for barn 0–5 år | Brødsmuler, `h1` (svart), ingress (grønn ramme, eller en kort punktliste), eventuelt bilde, eventuelt «Innhold på denne siden», brødtekst med `h2`/`h3`, nedtrekk, bokser, tabell, «Sist endret». |

Alle sider avsluttes med «Fant du det du lette etter?», bølgen og bunnen. Det ligger i malen.

## Komponentkatalog (lukket liste)

| Komponent | Markup | Brukes til |
|---|---|---|
| Brødsmuler | `#crumbs`, styres av `CRUMBS`/`PORTAL` | Alltid. Viser hvor siden ville ligget på nettsiden. Bare portalnavnet er klikkbart. |
| Tittel | `<h1>` | Én per side. Merkefarge på portalsider, svart på artikler. |
| Ingress, portal | `<p class="ingress">` | Portalsider: 1–3 setninger. |
| Ingress, artikkel | `<div class="ingress-box"><p>…</p></div>` | Artikler: grønn ramme, kursiv. Tjenestesider kan i stedet ha en kort punktliste i vanlig `<ul>` rett under `h1`. |
| Dekorsirkler | `<div class="portal-bg" aria-hidden="true">` med `.c1`–`.c3` (ligger i malen) | Bare portalsider. Sirklene ligger i bakgrunnen bak brødsmuler og tittel, og blir beskåret av toppen. Ikke flytt dem inn i en egen kolonne, og ikke legg ikoner eller tekst i dem. Vil brukeren ha en egen illustrasjon i en sirkel (som «Alt i meg»), spør først og sjekk mot den ekte siden. |
| Lenkefliser | `<ul class="tiles">` (fylles fra `TOPICS`) | Lenker til undersider fra portal- og kategorisider. Bare titler, ingen beskrivelser. |
| Innhold på denne siden | `<div class="toc"><h2>Innhold på denne siden</h2><ul class="toc-list">…</ul></div>` | Lange tjenestesider. Vertikal liste med lenker til `h2`-er eller nedtrekk på samme side. |
| Nedtrekk | `<details class="acc" id="…"><summary>…</summary><div class="acc-body">…</div></details>` | Seksjoner og spørsmål som ikke alle trenger. Grå, pil, grønn ramme når åpen. Innholdet står uten boks. Kan ha lister, lenker og tabeller inni. Ikke nummerer dem og ikke legg nedtrekk i nedtrekk. |
| Blå boks | `<div class="box box-blue">` | Fremhevet innhold eller lenkeliste, gjerne uten overskrift. |
| Gul boks | `<div class="box box-yellow"><h2>…</h2><ul>…</ul></div>` | Lenkeliste med overskrift, for eksempel «Sider om …», «Nyttige lenker». |
| Bilde til høyre | `<figure class="right"><img alt="…"><figcaption>Foto: …</figcaption></figure>` + `<div class="clear"></div>` etter teksten | Bilde ved siden av et avsnitt. Bildetekst er valgfri. |
| Bilde i full bredde | `<figure><img alt="…"><figcaption>…</figcaption></figure>` | Rett under ingressen i artikler. |
| Tabell | `<div class="tablewrap"><table><caption>…</caption>…</table></div>` | Oversikter, for eksempel tidspunkter og typer konsultasjoner. |
| Nyhetsliste | `<ul class="news"><li><img alt=""><time>dd.mm.åååå</time><h3><a href="#…">…</a></h3><p>…</p></li></ul>` + `<span class="fake">Se alle saker</span>` | Bare portalsider med egne nyheter. Bilde og ingress er valgfritt per sak. |
| Sist endret | `<p class="updated">Sist endret dd.mm.åååå</p>` | Nederst i artikler. |
| Tilbakemelding | Ligger i malen | «Fant du det du lette etter?» JA/NEI. NEI åpner tekstfelt. Lagres ikke. |

Vanlig tekst (`<p>`, `<ul>`, `<ol>`, `<h2>`, `<h3>`, `<strong>`) trenger ingen klasse. Kontaktinformasjon skrives som `h3` + avsnitt (for eksempel «Åpningstid:», «Telefon: …»), ofte inni et nedtrekk. Nødnumre og vakttelefoner skrives som tekst i nedtrekk, slik «Vakttelefoner» gjør, ikke som egne kort.

## Finnes ikke på nettsiden – ikke bruk

Fargede varsel- eller tipsbokser (rød, grønn), store CTA-kort, lenker som «chips»/piller, ja/nei-kolonner, kort med etiketter og definisjonslister, store talltavler, nummererte nedtrekk, faner, karuseller, «Andre temaer»-blokker, egne knapper i innholdet.

## Farger og typografi (fra malen, ikke endre)

Verdiene er avlest fra skjermbilder av nettsiden og er nære, men ikke nødvendigvis identiske med kommunens stilark.

- Merkefarge (portal-`h1`, knapperammer): `#0e3b4e`. Lenker: `#0e4f69`. Bunn: `#003a52`.
- Portalsirkler: fersken `#f0a68c`, salvie `#dfe7d6`, himmelblå `#8fc7df`, merkefarge. Oransje pil i fliser: `#e0805f`.
- Nedtrekk `#e8e8e6`, grønn ramme `#2b8763`. Blå boks `#dfeef8`. Gul boks `#fbeccb`.
- Logoblå: `#2384c6`. Logoteksten bruker `currentColor`.
- Font: Inter 400/500/600/700. Brødtekst 17 px, linjehøyde 1,6. Innholdskolonne maks 700 px (`.wrap.narrow`) på artikler. Sidebredde ca. 972 px.
- `h1`: halvfet (600), maks 32 px. Ingress på portalsider: samme størrelse som brødteksten (17 px).
- Lenkefliser: tekst i merkefarge, halvfet (600), 15 px, med god avstand mellom pil og tekst.

## Arbeidsflyt

1. **Samle innhold først.** Les vedlagte dokumenter, skjermbilder og nettadresser. Finn ut hvem siden er for, hvilke undersider den har, og hvor den ville ligget på tonsberg.kommune.no.
2. **Velg sidetype for hver side** (tabellen over), og bygg informasjonsarkitekturen: en portalside med lenkefliser til artikler/tjenestesider. Lenk mellom sidene der det er naturlig med `<a href="#side-id">` eller `#anker-id` på en annen side. Routeren åpner riktig side og eventuelt nedtrekk.
3. **Bygg fra startmalen.** Kopier `mal.html`, bytt plassholderne i `[klammer]`, legg til én `<section class="page">` per underside og én rad per underside i `TOPICS`.
4. **Test.** Åpne filen i en nettleser (gjerne med Playwright hvis tilgjengelig): fliser, «Innhold på denne siden» og andre interne lenker virker, brødsmulene stemmer, nedtrekk åpner, ingen JavaScript-feil, og ingen horisontal scrolling ved 390 px bredde.
5. **Lever filen** og si i én linje hva som er pynt/ikke klikkbart, og om noe er merket `FINNES IKKE I ACOS`.

## Sjekkliste før levering

- [ ] Hver side følger én sidetype. Ingen elementer utenfor katalogen (eller de er merket `FINNES IKKE I ACOS`).
- [ ] Grønn rammeboks bare som artikkelingress. Gul boks har overskrift og lenkeliste.
- [ ] Portalsiden har dekorsirklene i bakgrunnen (`.portal-bg`), ingen egen bildekolonne og ingen ikon-sirkel.
- [ ] Ingen klikkbare lenker ut av prototypen. Eksterne lenker har `fake ext`.
- [ ] Hver `<section class="page">` har unik `id` og `data-title` og står i `TOPICS` (unntatt `forside`). Portalsiden har `page-portal`.
- [ ] Interne lenker peker på id-er som finnes.
- [ ] Ingen personopplysninger eller ekte saksinformasjon.
- [ ] Ingen JS-feil, ingen horisontal scrolling på mobil (390 px).
- [ ] Klarspråk: korte setninger, du-form, fagord forklart.

## Startmal

Startmalen ligger i `mal.html` i samme mappe. Les hele filen og kopier den. Plassholdere står i `[klammer]`. Logoen er Tønsberg kommunes offisielle logo, vektorisert.

Finner du ikke `mal.html` (for eksempel fordi bare denne filen er lastet opp), si fra til brukeren og ikke lag en egen mal.
