# gravuralarm-tankstelle

Statische Webseite für tankstelle.gravuralarm.de
Kunden können hier ein Foto hochladen, das direkt an den Drucker in der Tankstelle gesendet wird.

## Deployment auf Vercel

1. Dieses Repository auf GitHub pushen
2. Auf vercel.com → "New Project" → GitHub Repo auswählen
3. Framework: **Other** (keine Änderung nötig)
4. Deploy klicken

## Nach dem Deployment

In `index.html` die Zeile:
```
const PRINTER_URL = 'NGROK_URL_HIER_EINTRAGEN';
```
ersetzen durch deine ngrok Pro Domain:
```
const PRINTER_URL = 'https://gravuralarm.ngrok.app';
```

Dann neu deployen (Git push reicht).

## Custom Domain in Vercel

1. Vercel → Projekt → Settings → Domains
2. `tankstelle.gravuralarm.de` eintragen
3. Vercel zeigt einen CNAME-Eintrag an → in IONOS eintragen
