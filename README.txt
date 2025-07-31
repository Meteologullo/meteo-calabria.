# Meteo Calabria — Cloudflare Ready

Questa cartella è pronta da caricare su GitHub nel repo **Meteologullo/meteo-calabria**.

## Cosa contiene
- `index.html` (già configurato con `readBase` corretto)
- `data/` con i 3 file JSON vuoti
- `cloudflare-worker/worker.js` (codice da incollare su Cloudflare Worker; NON serve nel repo)

## Cosa fare (3 passi)
1) **Carica questa cartella nel repo** (puoi trascinare i file su GitHub):
   - `index.html` deve stare in **root** del repo
   - la cartella `data/` in **root** del repo
   - la cartella `cloudflare-worker/` è solo di riferimento (puoi non caricarla)

2) **Crea un Cloudflare Worker** e inserisci:
   - Secret `GITHUB_TOKEN` = il tuo token GitHub (contenuti: read+write sul repo)
   - Var `REPO` = `Meteologullo/meteo-calabria`
   - Var `BRANCH` = `main`
   - Incolla `cloudflare-worker/worker.js` nel Worker → Deploy
   - Copia l'URL del Worker (es. `https://calabriamap-sync.tuonome.workers.dev`)

3) **Apri `index.html` su GitHub** e sostituisci:
   ```js
   writeEndpoint: "https://INSERISCI-QUI-URL-WORKER"
   ```
   con l'URL del Worker. Salva.

Finito. Apri la pagina (GitHub Pages) e usa i pulsanti:
- **Sincronizza (invio)** → invia al Worker e committa su GitHub
- **Carica da remoto** → legge i JSON da `data/` su GitHub
