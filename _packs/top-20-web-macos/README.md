# Top 20 Skills — Web + macOS

Wybór 20 najbardziej użytecznych skilli z repozytoriów `skilslsls`, `sar-skill` i `.openclaw`,
pod kątem budowania aplikacji webowych i aplikacji na macOS.

Każdy skill to osobne archiwum ZIP. Po rozpakowaniu dostajesz katalog `<nazwa-skilla>/`
z plikiem `SKILL.md` (frontmatter + treść) oraz — tam, gdzie są — katalogami `references/`,
`scripts/`, `data/`.

## Instalacja

```bash
unzip top-20-web-macos-skills.zip -d ./skills-pack
cd skills-pack
for z in *.zip; do unzip -q "$z" -d ~/.claude/skills/; done   # globalnie
# albo do projektu:
for z in *.zip; do unzip -q "$z" -d ./.claude/skills/; done
```

## Zawartość

### Frontend i framework

| Skill | Źródło | Po co |
|---|---|---|
| `react-frontend-development` | skilslsls | React 18+, hooki, Server Components, Suspense, stack 2026, wydajność renderowania |
| `nextjs-framework` | skilslsls | Next.js 15 / App Router, SSR/ISR, routing, data fetching |
| `typescript-development` | skilslsls | Zaawansowane typy, generyki, conditional/mapped types, migracja JS→TS (największy zbiór referencji) |
| `web-design-development` | skilslsls | Fundamenty HTML/CSS, layout, wydajność frontu, dobre praktyki wdrożeniowe |
| `responsive-web-design` | skilslsls | Breakpointy, mobile-first, fluid grids, testowanie responsywności |

### UI / UX / dostępność

| Skill | Źródło | Po co |
|---|---|---|
| `ui-ux-pro-max` | sar-skill | Skrypty (`search.py`, `design_system.py`) + bazy CSV per stack: react, nextjs, svelte, vue, shadcn, tailwind, **swiftui**, flutter. Jeden z dwóch skilli w paczce z wykonywalnym kodem (drugi to `gateway-watchdog`), reszta to proza |
| `web-application-design` | skilslsls | 17 referencji: wzorce aplikacji webowych, tabele danych, formularze, stany, nawigacja, panel admina, onboarding |
| `ui-ux-design-user-experience` | skilslsls | IA, interaction design, design systems, handoff, wzorce mobile i webowe |
| `accessibility-wcag` | skilslsls | WCAG 2.2, ARIA, nawigacja klawiaturą, audyty, zgodność ADA/Section 508 |

### Backend, dane, architektura

| Skill | Źródło | Po co |
|---|---|---|
| `backend-api-development` | skilslsls | REST i GraphQL, kontrakty API, wersjonowanie, obsługa błędów, deployment |
| `database-design-optimization` | skilslsls | Modelowanie schematu, indeksy, optymalizacja zapytań, skalowanie |
| `authentication-authorization` | skilslsls | OAuth 2.0, JWT, RBAC/ABAC, sesje, MFA, SSO |
| `system-architecture-design` | skilslsls | Mikroserwisy, cloud-native, wzorce integracji enterprise |
| `performance-optimization-scaling` | skilslsls | Cache (Redis/Memcached), CDN, load balancing, auto-scaling, monitoring |
| `web-application-security` | skilslsls | OWASP, walidacja wejścia, zarządzanie sekretami, hardening aplikacji |

### Jakość, testy, operacje

| Skill | Źródło | Po co |
|---|---|---|
| `qa-testing-automation` | skilslsls | Playwright, Cypress, Selenium, testy API, architektura testów, integracja z CI |
| `git-version-control` | skilslsls | Strategie branchowania, zaawansowane komendy, recovery, praca zespołowa |
| `docker-containerization` | skilslsls | Obrazy, multi-stage buildy, compose, środowiska dev |

### macOS / natywne

| Skill | Źródło | Po co |
|---|---|---|
| `ios-development-swift-swiftui` | skilslsls | Swift + SwiftUI: deklaratywne UI, MVVM, `@State`/`@Observable`, SwiftData, WidgetKit, HIG. SwiftUI jest wspólne dla iOS i macOS, więc to najbliższy natywnemu Macowi materiał w zbiorze |
| `gateway-watchdog` | .openclaw | Produkcyjny watchdog dla macOS: `launchd`/plist, grace period przy boocie, progresywne retry, wykrywanie stale PID, cooldown restartów. W komplecie znajdują się działające skrypty `scripts/*.sh` — wzorzec do każdego demona na Macu |

## Uwagi

- `gateway-watchdog` jest pisany pod bramkę OpenClaw. Wartość ogólna leży we wzorcu launchd
  (plist + cooldown + boot grace), nie w samym endpointcie — przy adaptacji zmień URL i etykietę joba.
- Skille z `skilslsls` to materiał opisowy z referencjami. Wykonywalny kod wnoszą tylko dwa spoza tego repo:
  `ui-ux-pro-max` (skrypty Pythona + dane CSV) i `gateway-watchdog` (skrypty bash).
- Nie ma tu dedykowanego skilla „macOS AppKit/Catalyst” — w tych repo taki nie istnieje.
  `ios-development-swift-swiftui` + dane `swiftui` z `ui-ux-pro-max` to maksimum pokrycia Maca, jakie dało się zebrać.
