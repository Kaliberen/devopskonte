## Oppgave 1 - DevOps-prosess for team
### 1. Branch-strategi

Teamet bruker branch-strategi inspirert av Git-flow. 
`main`-branchen representerer produksjonsklar kode og skal alltid være stabil. 
All utvikling skjer i egne `feature-branches` som opprettes fra `main`.

#### Ny branch opprettes for hver oppgave eller feature:

Eksempel:
- `feature/docker-multistage-build`
- `feature/controller-quizService`

Direkte commit til `main` er ikke tillatt.

#### Navngivning av branches:
- `main` - Produksjonsklar kode
- `feature/<beskrivelse>` - Nye funksjoner
- `fix/<beskrivelse>` - Bug fixes
- `hotfix/<beskrivelse>` - Kritiske produksjonsrettelser

Branches merges kun via Pull Request
- - - 
### 2. Pull Request-prosess

#### Pull Request opprettes når en selvstendig oppgave er ferdig utviklet og klar for gjennomgang.

1. Utvikler oppretter en branch fra `main`.
2. Endringer implementeres og commits pushes til GitHub.
3. Pull Request opprettes mot `main`.
4. CI-pipeline kjører automatiske tester, build og sikkerhetsskanning.
5. Koden gjennomgås av minst en annen utvikler.
6. Eventuelle kommentarer eller forbedringer implementeres.
7. Når alle krav er oppfylt, merges PR til `main`.

#### Minst en utvikler må godkjenne Pull Request før merge.
Ved større endringer eller arkitekturvalg skal Tech Lead involveres.
Code review skal fokusere på:
- Lesbarhet og struktur
- Overholdelse av prosjektets standarder.
- Sikkerhet og robusthet
- Potensielle edge cases.

#### Før en Pull Request kan merges må følgende krav være oppfylt:
- Alle automatiske tester må bestå
- Docker build må lykkes
- Trivy må ikke rapportere HIGH eller CRITICAL sårbarheter.
- Minst en godkjenning fra annen teammedlem
- Ingen åpne, kritiske review-kommentarer.

- - -

### Branch Protection
Hvilke regler skal main-branch ha?
`main`-branchen er beskyttet med følgende regler:
- Krev Pull Request før merge
- Krev godkjent code review
- Krev at alle status checks (CI pipeline) består
- Forhindre direkte push

Hvorfor er disse viktige for teamarbeid?
#### Dette sikrer at ingen kan omgå kvalitetssikring, og at produksjonskoden alltid holder høy standard

- - -

### Automatisering

Hvilke automatiske sjekker skal kjøres?

#### På Pull Request kjøres:

- `mvn test`
- `mvn package`
- Docker build
- Trivy filesystem scan
- Trivy container image scan
- Generering og opplasting av SARIF-rapport til GitHub Security.

Pipeline feiler dersom det oppdages HIGH eller CRITCAL sårbarheter.

#### På push til `main` kjøres:

- Tester og build
- Docker image build 
- Push til Docker Hub
- Tagging med commit SHA og `latest`

Denne automatiseringen sikrer kontinuerlig kvalitet, rask tilbakemelding og trygg deply-prosess.

![alt text](bilde.png)
![alt text](bilde-1.png)

- - -
