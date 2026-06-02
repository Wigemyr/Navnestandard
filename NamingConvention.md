# Spørsmål før ferdigstilling av dokument
- Hvor mange subscriptions tenker man å ha i miljøet? Skal det være en del så bør man ha Management Groups.
- Hvor mange avdelinger skal inn å bruke miljøet?
- Er det behov for lengre/mer omfattende navnestruktur? Krever det bedre muligheter for å skille ressurser fra hverandre?

#  Forslag til navnekonvensjon for Azure/Microsoft 365 miljø
Dette dokumentet beskriver et **forslag** til navnestandarder som skal brukes i Azure og Microsoft 365 (M365) miljøer. Konsistente navnestandarder er avgjørende for enkel administrasjon, feilsøking, sikkerhet, og for å sikre at ressursene er lett gjenkjennelige.

## Generelle retningslinjer
1. **Lesbarhet:** Navn skal være lett lesbare og meningsfulle.
2. **Korthet**: Hold navn så korte som mulig, men lange nok til å være beskrivende.
3. **Konsistens:** Bruk enhetlige konvensjoner for å sikre konsistens på tvers av alle ressurser.
4. **Unikhet:** Navn må være unike for å unngå konflikter.
5. **Unngå Spesialtegn:** Bruk ikke spesialtegn, mellomrom, eller store bokstaver. Bruk bindestrek (-) og understrek (_).
6. **Alfanumerisk:** Når man lager navn på diverse grupper/ressurser og annet i miljøet skal man bruke alfanumeriske tegn (a-z og 0-9). Dette vil si at: Æ -> AE, Ø -> O og Å -> A

## Hvordan opprettholde "Best Practice" for navnestandard
1. **Dokumentasjon:** Dokumenter alle navnestandarder i en sentral guide som er tilgjengelig for alle administratorer.
2. **Automatisering:** Bruk automatiserte verktøy for å håndheve navnekonvensjoner *(eksempel Tagging Policy og andre regler for navn ved opprettelse)*
3. **Revisjon:** Gjennomfør regelmessige revisjoner for å sikre at navnestandarder følges.
4. **Opplæring:** Gi opplæring til alle relevante medarbeidere om viktigheten av og retningslinjene for navnestandarder.

## Navnestandard for Subscriptions
Et Azure Subscription er en konto som gir tilgang til Azure-tjenester og fungerer som en container for ressurser som virtuelle maskiner, databaser, lagringskontoer og mye mer. Hver subscription har en unik ID og kan være assosiert med en spesifikk organisasjon eller avdeling.
  
### Forslag til navnestandard for Subscriptions
Under er et forslag til navnestandard for alle subscriptions som blir opprettet i Azure miljøet. 

Navnestruktur: 
`{miljo}-sub` skrives med små bokstaver.

Tabellen under viser et eksempel på hvordan navnestrukturen for subscriptions kan se ut.
| Miljø | Subscription Navn  |
|-------|--------------------|
| utv   | utv-sub            |
| prod  | prod-sub           |
| utv   | utv-sub            |
| utv   | utv-sub            |

## Navnestandard for Tags
Tags i Azure brukes til å organisere og kategorisere ressurser, noe som gjør administrasjon og rapportering enklere og mer effektivt.

### Noen vanlige brukstilfeller for tagging inkluderer:

- **Fakturering:** Gruppe ressurser og assosiere dem med fakturering eller kostnadskoder.
- **Tjenestekontekstidentifikasjon:** Identifisere grupper av ressurser på tvers av ressursgrupper for felles operasjoner og gruppering.
- **Forvalter eller kontaktperson:** Gjøre det enkelt for personer som ikke har kjennskap til ressursene å finne kontaktpersoner.

For Tags bruker vi **camelCase** som er en skrivemåte der hvert ord i en sammensatt ordsekvens starter med en stor bokstav, unntatt det første ordet, og det er ingen mellomrom eller spesialtegn mellom ordene (f.eks. forvaltesAv eller prosjektNavn).

Tabellen under viser et eksempel på hvordan navnestrukturen for tags kan se ut.  

| Tagg Navn                                 | Nøkkel           | Eksempel                        | Kommentar                                  |
|-------------------------------------------|------------------|---------------------------------|--------------------------------------------|
| Faktureres Til / Intern Kostnads-ID       | fakturaTil       | `TSS` eller `Intern Kostnads-ID`| Avdeling eller Intern Kostnads-ID          |
| Forvalter eller kontaktperson             | forvaltesAv      | `joe@contoso.com`               | Alias eller e-postadresse                  |
| Prosjektnavn (valgfritt)                  | prosjektNavn     | `B024`                          | Navn på prosjektet eller prosjekt ID       |
| Prosjektversjon (valgfritt)               | prosjektVersjon  | `1.0`                           | Versjon av prosjektet                      |
| Miljø                                     | miljo            | `<prod eller utv>`              | Miljøidentifikator (prod eller utv)        |
| Avdeling                                  | avdeling         | `TSS`                           | Navn på avdeling                           |

### Policy for Tags
En tagging policy i Azure er en regel eller et sett med regler som automatisk sørger for at ressurser blir merket med spesifikke tagger når de opprettes eller oppdateres. Disse reglene hjelper med å sikre at alle ressurser følger samme standard for tagging, noe som gjør det lettere å organisere, finne og administrere dem på tvers av organisasjonen. Når en ressurs opprettes i Azure kan man kreve at diverse tagger er lagt på denne ressursen *(eksempel at det må kreve en forvaltesAv- eller miljø-tag)*.

## Forslag til navnestandard for Azure Ressursgrupper

Navnestruktur: 
`{applikasjonsnavn, prosjekt eller funksjon}-{miljø}-rg` skrives med små bokstaver.

Tabellen under viser et eksempel på hvordan navnestrukturen for ressursgrupper kan se ut.  

| Applikasjonsnavn, prosjekt eller funksjon | Miljø | Navn på ressursgruppe                 |
|-------------------------------------------|-------|---------------------------------------|
| hrsystem                                  | prod  | hrsystem-utv-rg                       |
| analyseapplikasjon                        | utv   | analyseapplikasjon-prod-rg            |
| teamsbestilling                           | utv   | teamsbestilling-utv-rg                |
| B024 *(eksempel på prosjekt)*             | utv   | b024-utv-rg                           |

## Forslag til navnestandard for Ressurser i Azure
Hver ressurstype eller tjenestetype i Azure innebærer et sett med navnerestriksjoner og omfang; enhver navnekonvensjon eller mønster må overholde de nødvendige navnerestriksjonene og omfanget. For eksempel, mens navnet på en VM knyttes til et DNS-navn (og derfor må være unikt over hele Azure), er navnet på et VNET (virtuelt nettverk) begrenset til Ressursgruppen det er opprettet i, og kan derfor ha et samme navn i en annen ressursgruppe.

Navnestruktur: 
`<applikasjonnavn eller prosjekt>-<miljø>-{funksjon}-<ressurs-forkortelse>` skrives med små bokstaver.

Når det gjelder <ressurs-forkortelse> tar man utgangspunkt i Microsoft sine anbefalinger. Les mer om disse her: [Abbreviation recommendations for Azure resources - Microsoft](https://learn.microsoft.com/nb-no/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations)

Tabellen under viser et eksempel på hvordan navnestrukturen for ressurser i Azure kan se ut.  

| Azure Ressurs      | Forkortelse   | Miljø         | Applikasjonsnavn eller prosjekt    | Funksjon         | Fullstendig navn for Ressurs                    |
|--------------------|---------------|---------------|-------------------------------------------------------|-------------------------------------------------|
| Virtual Machine    | vm            | utv           | analyseapplikasjon                 | publisernyheter  | analyseapplikasjon-utv-vm01                     |
| Load Balancer      | lb            | prod          | B024 (eksempel på prosjekt)        | balensertrafikk  | b024-prod-lb01                                  |
| Piblic IP Address  | pip           | utv           | analyseapplikasjon                 | analyserer       | analyseapplikasjon-utv-pip01                    |
| Virtul Machine     | vm            | utv           | teamsbestilling                    | teamsbestilling  | teamsbestilling-utv-vm01                        |
| Virtul Machine     | vm            | utv           | analyseapplikasjon                 | analyserer       | analyseapplikasjon-utv-vm02                     |

Generelt bør du unngå å ha spesialtegn (- eller _) som første eller siste tegn i noe navn, da disse vil feile de fleste valideringsregler.

I tabellen under ser man eksempler på noen av de mest vanlige ressurser som kan opprettes i Azure i tillegg til deres restriksjoner for navn:

| Kategori        | Tjeneste eller Enhet     | Omfang           | Lengde på ressursnavn         | Skriftform                                   | Gyldige tegn                                     |
|-----------------|--------------------------|------------------|-------------------------------|----------------------------------------------|--------------------------------------------------|
| Ressursgruppe   | Ressursgruppe            | Global           | 1-64                          | Skiller ikke mellom store og små bokstaver   | Alfanumerisk, understrek og bindestrek           |
| Databehandling  | Virtuell Maskin          | Ressursgruppe    | 1-15 (Windows), 1-64 (Linux)  | Skiller ikke mellom store og små bokstaver   | Alfanumerisk, understrek og bindestrek           |
| Lagring         | Lagringskontonavn        | Global           | 3-24                          | Små bokstaver                                | Alfanumerisk                                     |
| Nettverk        | Virtuelt Nettverk (VNet) | Ressursgruppe    | 2-80                          | Skiller ikke mellom store og små bokstaver   | Alfanumerisk, bindestrek, understrek og punktum  |
| Nettverk        | Subnett                  | Overordnet VNet  | 2-80                          | Skiller ikke mellom store og små bokstaver   | Alfanumerisk, understrek, bindestrek og punktum  |
| Database        | Azure SQL Database       | Server           | 1-128                         | Skiller ikke mellom store og små bokstaver   | Alfanumerisk, understrek og bindestrek           |
| Apptjeneste     | Web App                  | Global           | 1-60                          | Små bokstaver                                | Alfanumerisk, bindestrek                         |
| Generelt        | Tag                      | Tilknyttet Enhet | 512 (navn), 256 (verdi)       | Skiller ikke mellom store og små bokstaver   | Alfanumerisk                                     |

*Skiller ikke mellom store og små bokstaver betyr at systemet ikke gjør forskjell på store og små bokstaver i navnene på ressurser. Dette innebærer at en ressurs med navnet "MinRessurs" behandles som identisk med "minressurs" eller "MINRESSURS".*


For å lese mer om restriksjoner og krav for navn for ressurser, se her: [Naming rules and restrictions for Azure resources - Microsoft](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/resource-name-rules)

## Navnestandard for grupper i Entra ID (tidl. Azure Active Directory (AAD))

Entra ID, tidligere kjent som Azure Active Directory (AAD), er en skybasert identitets- og tilgangsstyringstjeneste som gir en rekke funksjoner for å administrere brukere og grupper i organisasjonen din. Grupper i Entra ID brukes til å administrere tilgang til ressurser ved å samle brukere som trenger lignende rettigheter. Hver gruppe kan ha en unik ID og kan være assosiert med spesifikke avdelinger, prosjekter eller funksjoner innen organisasjonen.

### Viktigheten rundt en konsekvent- og veldefinert navnestandard i Entra ID

En konsekvent og veldefinert navnestandard for grupper i Entra ID (tidligere Azure Active Directory) er avgjørende for flere grunner:

1. **Enklere Administrasjon**:
   - Klare og konsistente gruppenavn gjør det lettere for IT-administratorer å opprette, vedlikeholde og administrere grupper. Dette reduserer tiden og innsatsen som kreves for å håndtere brukertilgang og tillatelser.

2. **Forbedret Sikkerhet**:
   - Ved å bruke standardiserte navn kan du lettere identifisere og administrere sikkerhetsinnstillinger og tilgangskontroller. Dette bidrar til å redusere risikoen for feilkonfigurasjoner som kan føre til sikkerhetsbrudd.

3. **Bedre Oversikt og Organisering**:
   - Standardiserte navn gir en bedre oversikt over hvilke grupper som finnes, og deres tilhørende funksjoner eller avdelinger. Dette er spesielt nyttig i store organisasjoner med mange grupper.

4. **Effektiv Feilsøking**:
   - Når gruppenavnene klart indikerer deres formål og tilhørighet, blir det enklere å feilsøke problemer relatert til tilgang og rettigheter. Dette gjør det også lettere å gjennomføre revisjoner og kontrollere samsvar med retningslinjer.

5. **Skalerbarhet**:
   - En veldefinert navnestandard gjør det lettere å skalere IT-miljøet når organisasjonen vokser. Nye grupper kan enkelt opprettes og integreres i eksisterende systemer uten å skape forvirring eller konflikter.

6. **Redusert Risiko for Feil**:
   - En standardisert tilnærming minimerer risikoen for feil ved opprettelse og administrasjon av grupper. Dette bidrar til å sikre at riktige brukere har tilgang til riktige ressurser.

*Ved å implementere en standardisert navnekonvensjon for grupper i Entra ID, kan organisasjonen oppnå en mer effektiv og sikker administrasjon av brukerrettigheter og tilganger, samtidig som man sikrer samsvar med interne og eksterne retningslinjer og krav.*

## Forslag til navnestandard for grupper i Entra ID (tidl. Azure Active Directory (AAD))

Generell: `{avdeling}-{miljø}-{funksjon}-{rolle/hensikt/område}` skrives med små bokstaver.  
For PIM: `{avdeling}-{miljø}-{funksjon}-{rolle}-{ressursgruppe/subscription eller ressurs)` skrives med små bokstaver.

Tabellen under viser et par eksempel på hvordan navnestrukturen for ressurser i Azure kan se ut.  
!! Trenger innspill rundt navnestruktur for grupper i Entra ID. 

| Kategori                                 | Navnestruktur                                          | Hensikt                                                           | Fullstendig navn på Entra ID gruppe                 |
|------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------|
| Tilgangsgrupper (PIM for rolle)          | `{avdeling}-{miljø}-pim-{rolle/hensikt/område}`        | PIM Gruppe for Security Reader                                    | `tss-prod-pim-securityreader`                       |                  
| Tilgangsgrupper (PIM for ressurstilgang) | `{avdeling}-{miljø}-pim-{rolle/hensikt/område}`        | Contributor tilgang i ressursgruppen "contoso-hrsystem-utv-rg"    | `tma-utv-pim-contributor-contoso-hrsystem-utv-rg`   |
| Sikkerhetsgrupper (security gruppe)      | `{avdeling}-{miljø}-sec-{rolle/hensikt/område}`        | Sikkerhetsgruppe for brukere til VPN-løsning                      | `tma-prod-sec-vpn`                                  |
| Prosjektgrupper                          | `{avdeling}-{miljø}-prosjekt-{rolle/hensikt/område}`   | Prosjektgruppe for B024-prosjektet                                | `tikt-utv-prosjekt-b024`                            |
| SharePoint-grupper                       | `{avdeling}-{miljø}-sp-{rolle/hensikt/område}`         | SharePoint gruppe for Intranet                                    | `tss-prod-sp-intranet`                              | 
| Exchange grupper                         | `{avdeling}-{miljø}-exchange-{rolle/hensikt/område}`   | Exchange gruppe for brukere som behøver videresendelsesregel      | `tma-utv-exchange-videresendelsesregel`             |
| Microsoft 365 grupper                    | `{avdeling}-{miljø}-m365-{rolle/hensikt/område}`       | Microsoft 365 (samarbeidsgruppe) for TSS-avdelingen               | `tikt-prod-m365-tss`                                |

Dokumentet er under oppdatering ...

Trenger innspill og innsikt på hva som gjenstår av navnestandard.

Forslag:
- Conditional Access
- Compliance, Intune og andre admin-portaler når det kommer til konfigurasjons- og policynavn.
