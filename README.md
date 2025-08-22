# Ma Che Serata – MVP (Netlify + Supabase)

Questo repository contiene un MVP deployabile su Netlify con backend serverless (Netlify Functions) e database/auth su Supabase. Frontend statico (Vanilla JS, PWA-ready).

## Requisiti
- Netlify account (deploy da repo Git o Netlify CLI)
- Supabase project (URL + anon key)
- Facoltativi: Google Maps, OneSignal, Spotify

## Configurazione variabili d'ambiente (Netlify)
Imposta in Netlify → Site Settings → Environment variables:
- `SUPABASE_URL`
- `SUPABASE_ANON_KEY`
- `SUPABASE_SERVICE_ROLE` (server only, NON esporla lato client)
- `GOOGLE_MAPS_API_KEY` (opzionale)
- `ONESIGNAL_APP_ID` (opzionale)
- `SPOTIFY_CLIENT_ID` (opzionale)

Le funzioni serverless espongono in modo sicuro al client solo le chiavi pubbliche tramite `/api/env`.

## Sviluppo locale
```bash
npm i
npm run dev
```
Apri l'URL mostrato dalla CLI (Netlify Dev) per testare funzioni e frontend insieme.

## Deploy
- Collega il repo a Netlify oppure usa `netlify deploy`.
- Publish directory: `public`
- Functions directory: `netlify/functions`

## Supabase schema
Trovi uno schema iniziale in `supabase/schema.sql`. Applicalo al progetto Supabase (SQL editor) prima dell'uso.

## Struttura
```
public/
  index.html
  manifest.webmanifest
  sw.js
  assets/
    css/styles.css
    js/app.js
    js/router.js
    js/pages/
      home.js
      auth.js
      dashboard.js
netlify/
  functions/
    env.js
    events.js
supabase/
  schema.sql
netlify.toml
package.json
```

## Note
- L'autenticazione utente è gestita con Supabase Auth lato client. Le funzioni usano il token dell'utente per eseguire operazioni con RLS attive.
- Aggiungi le icone PWA in `public/assets/img/` e riferiscile in `manifest.webmanifest`.
