# Meteo Calabria — Sync Starter (GitHub + Cloudflare/Netlify)

Questa cartella è pronta da caricare su GitHub.
Contiene:
- `data/` → i 3 file JSON condivisi
- `public/index.html` → la tua pagina con pulsanti **Carica da remoto** e **Sincronizza (invio)**
- `backend-cloudflare/worker.js` → backend minimale (Cloudflare Workers)
- `backend-netlify/` → backend minimale (Netlify Functions)

## Passi rapidi

1. **Crea repo su GitHub** (pubblico). Carica **tutta questa cartella** così com'è.
2. **Prendi la tua readBase** (sostituisci OWNER/REPO/BRANCH):
   `https://raw.githubusercontent.com/OWNER/REPO/BRANCH/data/`
3. **Scegli un backend** per scrivere sui JSON del repo:
   - **Cloudflare Workers**: crea Worker, imposta variabili:
     - Secret `GITHUB_TOKEN` (PAT con Contents: Read/Write sul repo)
     - Vars `REPO="OWNER/REPO"`, `BRANCH="main"`
     - Incolla `backend-cloudflare/worker.js`, Deploy → copia l'URL dell'endpoint
   - **Oppure Netlify**: deploya questo repo; in **Site Settings → Environment variables** aggiungi:
     - `GITHUB_TOKEN`, `REPO="OWNER/REPO"`, `BRANCH="main"`
     - L'endpoint sarà: `https://TUO-SITO.netlify.app/.netlify/functions/sync`
4. **Apri `public/index.html`** e metti i 2 valori:
   ```js
   const SYNC = {
     readBase: "https://raw.githubusercontent.com/OWNER/REPO/BRANCH/data/",
     writeEndpoint: "https://IL-TUO-ENDPOINT"
   };
   ```
5. **Prova**:
   - Apri la pagina (GitHub Pages o Netlify) → fai modifiche → **Sincronizza (invio)**
   - Su un altro dispositivo → **Carica da remoto** → vedi le stesse modifiche

Note:
- Il token NON va mai nell'HTML. Resta nei Secrets del backend.
- I file `data/*.json` sono dinamici: supportano anche **nuovi marker**.
