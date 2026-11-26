# Skills for KI-assistenter

Oppskrifter («skills») som lærer KI-assistenter å lage ting slik vi gjør det i kommunen. Hver skill er en mappe med en `SKILL.md` og eventuelle hjelpefiler. Formatet er den åpne Agent Skills-standarden, så de samme filene kan brukes i Claude og i GitHub Copilot.

## Skills

| Skill | Hva den gjør | Status |
|---|---|---|
| [`tonsberg-prototype`](skills/tonsberg-prototype/) | Klikkbare prototypenettsider i stilen til tonsberg.kommune.no, til brukertesting. Bare komponenter som finnes i Acos. | I bruk |
| [`plakatgenerator`](skills/plakatgenerator/) | Oppskrift på en plakatgenerator i nettleseren som gir profilriktige plakater fra faste maler. | Ikke prøvd på ny app |
| [`laast-designmal`](skills/laast-designmal/) | Oppskrift på en låst designmal: designet ligger fast, bestilleren endrer tekst og laster ned trykkfiler. | Første test gjort |
| [`lag-app-skill`](skills/lag-app-skill/) | Metode for å gjøre en app som virker om til en gjenbrukbar skill («vi deler oppskriften, ikke appen»). | Ikke prøvd på ny app |

## Bruke en skill

**Claude (claude.ai):** Pakk skill-mappen (for eksempel `tonsberg-prototype/` med alle filene) som ZIP og last den opp under Skills i innstillingene.

**GitHub Copilot (VS Code agent mode, Copilot CLI, coding agent):** Kopier skill-mappen til
- `.github/skills/` i repoet du jobber i, eller
- `~/.copilot/skills/` hvis du vil ha den i alle prosjekter.

Copilot velger skillen selv når den passer, eller du kan be om den med `/navn`, for eksempel `/tonsberg-prototype`.

Ta alltid med hele mappen. `tonsberg-prototype` virker ikke uten `mal.html`.

## Endre en skill

1. Prøv skillen på en ekte oppgave før du endrer den.
2. Lag en gren og endre `SKILL.md` (eller `mal.html`). Skriv i commit-meldingen *hvorfor*, for eksempel «portalsirkler stemte ikke med Innovasjon-siden».
3. Lag en pull request. Noen andre ser over før den flettes inn.
4. Oppdater status-tabellen over hvis skillen er prøvd på nytt.

Prinsipper:
- Én skill gjør én ting. Skriv i `description` når den skal brukes, og når den ikke skal brukes.
- Regler som kan sjekkes (lukket komponentliste, sjekkliste) virker bedre enn råd.
- Ingen personopplysninger, saksinformasjon eller interne navn i skillene.

## Må fylles inn

Noen skills har plassholdere i `{{KLAMMER}}` for lenker som ikke finnes her ennå:

- `{{REPO_BYGGEKLOSSER}}`: repoet med felles byggeklosser (`plakatgenerator`, `laast-designmal`)
- `{{EKSEMPEL_PLAKATGENERATOR_URL}}`, `{{EKSEMPEL_PLAKATGENERATOR_REPO}}`
- `{{EKSEMPEL_LAAST_DESIGNMAL_URL}}`, `{{EKSEMPEL_LAAST_DESIGNMAL_REPO}}`
