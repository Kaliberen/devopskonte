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

`main`-branchen er beskyttet med følgende regler:
- Krev Pull Request før merge
- Krev godkjent code review
- Krev at alle status checks (CI pipeline) består
- Forhindre direkte push

#### Branch protection regler for `main` er konfigurert med:

- Required Pull Request before merge
- Required status checks
- Required conversation resolution
- No direct push allowed
- Administrators cannot bypass rules


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

![alt text](screenshots/bilde.png)
![alt text](screenshots/bilde-1.png)


- - -

## Oppgave 2

![alt text](screenshots/bilde-3.png)
![alt text](screenshots/bildedock1.png)

#### Før

- quiz-app-old
- 608MB

![alt text](screenshots/bildeFør.png)

#### Etter

- quiz-app-new
- 318MB

![alt text](screenshots/imageEtter.png)

- - -

## Oppgave 3.

Mislykket workflow på main (med docker push) 

![alt text](screenshots/alertVul.png)

![alt text](trivyTable.png)

github action runs
![alt text](bilde.png)

alle sjekkpunkter

![alt text](bilde-1.png)

code scanning
![alt text](bilde-2.png)

Oppgave 4 
Som student innen IT og programmering har jeg opplevd hvor raskt utviklingstempoet kan øke med moderne verktøy og teknologi. Det er i dag mulig å produsere funksjonalitet langt raskere enn tidligere, men denne økte hastigheten gjør også at behovet for struktur og kvalitetssikring blir større. Gjennom dette prosjektet har jeg forstått hvorfor DevOps blir enda viktigere når utviklingshastigheten øker.

I arbeidet med CI/CD-pipeline, Docker og sikkerhetsskanning opplevde jeg at det ikke er nok at applikasjonen “fungerer”. Selv om koden kjørte lokalt, oppdaget Trivy flere HIGH og CRITICAL sårbarheter i dependencies som Spring Boot og Tomcat. Dette viste meg at kvalitet ikke bare handler om funksjonalitet, men også om sikkerhet og vedlikeholdbarhet. DevOps-praksiser som automatiserte tester, container-build og sikkerhetsskanning fungerer som en kontrollmekanisme som sikrer at koden holder produksjonsstandard.

Gjennom branch-strategi, Pull Requests og branch protection-regler erfarte jeg hvor viktig struktur er i teamarbeid. Ingen kode kunne merges til main uten at tester, build og sikkerhetsskanning var vellykket. Dette skapte en trygg og profesjonell arbeidsflyt som reduserer risikoen for feil i produksjon. Når utviklingstempoet øker, blir slike mekanismer avgjørende for å opprettholde stabilitet.

En annen viktig lærdom var hvordan sikkerhet må være en integrert del av utviklingsprosessen. I stedet for å bli håndtert til slutt, ble sikkerhet kontrollert automatisk i pipeline. Når workflowen feilet på grunn av sårbarheter, måtte jeg oppgradere dependencies og forbedre Docker-imaget. Dette gjorde meg mer bevisst på ansvar som utvikler og betydningen av kontinuerlig forbedring.

Økt produktivitet gir flere commits, flere Pull Requests og raskere iterasjon. Uten DevOps kan dette føre til ustabile deploys og teknisk gjeld. Med DevOps på plass blir den økte produktiviteten en styrke i stedet for en risiko. Automatisering sikrer konsistens, testing sikrer kvalitet, og sikkerhetsskanning sikrer robusthet.

For meg har dette prosjektet vist at DevOps ikke bare handler om verktøy, men om en måte å jobbe på. Når utvikling går raskere, må kontroll, kvalitet og sikkerhet være innebygd i prosessen. Som fremtidig IT-programmerer ser jeg tydelig at kombinasjonen av effektiv utvikling og solide DevOps-prinsipper er avgjørende for å levere stabile og sikre løsninger i arbeidslivet.