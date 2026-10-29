# Strategi 2026–2029 – oppsett i Azure Static Web Apps

Innhold:
- `index.html` – hele nettsiden i én fil (logoer og innhold er bakt inn).
- `staticwebapp.config.json` – krever innlogging med Entra ID og setter sikkerhetsheadere.

## Oppsett

1. Opprett en **Static Web App** i Azure-portalen, plan **Standard**.
   Standard-planen er nødvendig for å begrense innlogging til egen tenant.
   Med Free-planen kan hvilken som helst Microsoft-konto logge inn.
2. Lag en **app-registrering** i Entra ID:
   - Redirect URI (Web): `https://<din-app>.azurestaticapps.net/.auth/login/aad/callback`
   - Opprett en client secret.
3. Bytt ut `<TENANT_ID>` i `staticwebapp.config.json` med tenant-ID-en deres.
4. Legg inn to applikasjonsinnstillinger på Static Web App-ressursen:
   `AZURE_CLIENT_ID` (app-registreringens Application ID) og `AZURE_CLIENT_SECRET`.
5. Last opp de to filene, for eksempel via GitHub/Azure DevOps-pipeline eller
   `swa deploy` fra Static Web Apps CLI.
6. Valgfritt: begrens til bestemte brukere eller grupper under
   «Enterprise applications» → «Properties» → «Assignment required».

## Teams-fane

Legg adressen inn som fanen **Nettsted** i ønsket kanal. Test innloggingen i Teams-klienten
først: Microsoft-innlogging lar seg ikke alltid vise inne i en fane, og da åpnes den i nettleseren.

## Lenker til enkeltsider

Hver side har egen adresse, for eksempel `…/#bookup`, `…/#kompetanse`, `…/#forutsetninger`.

## Oppdateringer

Siden oppdateres ikke automatisk fra Claude. Etter endringer lastes ny `index.html` opp.
