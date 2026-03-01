# GRAVURALARM Tankstelle – Komplette Einrichtungsanleitung

## Übersicht

```
Kunde öffnet tankstelle.gravuralarm.de (Vercel)
        ↓
Foto wird gesendet an ngrok Pro Tunnel
        ↓
Node.js Server auf dem PC in der Tankstelle
        ↓
Foto landet im Sawgrass Quick Print Ordner → Drucker
```

---

## SCHRITT 1 – ngrok Pro einrichten (~10 Min)

1. Gehe zu https://ngrok.com/pricing → **Personal Plan** (~10€/Monat)
2. Account anlegen / einloggen
3. Im ngrok Dashboard → **Cloud Edge** → **Domains** → **New Domain**
4. Domain wählen, z.B. `gravuralarm.ngrok.app`
5. Authtoken kopieren: Dashboard → **Your Authtoken**

Auf dem PC der Tankstelle:
```
ngrok config add-authtoken DEIN_AUTHTOKEN
```

ngrok starten (jeden Tag beim PC-Start):
```
ngrok http --domain=gravuralarm.ngrok.app 3000
```

---

## SCHRITT 2 – server.js konfigurieren

In `server\server.js` diese Zeile anpassen:
```
const NGROK_DOMAIN = 'gravuralarm.ngrok.app';
```

---

## SCHRITT 3 – Vercel Deployment

1. GitHub Repository `gravuralarm-tankstelle` erstellen
2. Den Inhalt des Ordners `gravuralarm-tankstelle` pushen
3. Auf https://vercel.com → **New Project** → Repo auswählen → **Deploy**
4. In `index.html` anpassen:
   ```
   const PRINTER_URL = 'https://gravuralarm.ngrok.app';
   ```
5. Commit + Push → Vercel deployed automatisch

---

## SCHRITT 4 – Custom Domain in Vercel

1. Vercel → Projekt → **Settings** → **Domains**
2. `tankstelle.gravuralarm.de` eintragen
3. Vercel zeigt an: `CNAME → cname.vercel-dns.com`

---

## SCHRITT 5 – IONOS DNS einstellen

1. Einloggen auf ionos.de → Domains → gravuralarm.de → DNS
2. Neuen Eintrag hinzufügen:
   - **Typ:** CNAME
   - **Hostname:** tankstelle
   - **Ziel:** cname.vercel-dns.com
3. Speichern – dauert 5-30 Minuten bis aktiv

---

## SCHRITT 6 – Testen

1. https://tankstelle.gravuralarm.de öffnen
2. Foto hochladen
3. Prüfen ob Foto im Sawgrass Ordner landet:
   `C:\Users\User1\Desktop\Sawgrass Quick Print\`

---

## Täglicher Betrieb (Azubi)

Morgens PC starten, dann zwei CMD-Fenster:

**Fenster 1:**
```
cd /d C:\Users\User1\Downloads\tassendruck-system neu\tassendruck
node server\server.js
```

**Fenster 2:**
```
ngrok http --domain=gravuralarm.ngrok.app 3000
```

Azubi-Display öffnen:
```
http://localhost:3000/azubi.html
```

QR-Code für Kunden liegt auf dem Azubi-Display.

---

## Mehrere Tankstellen

Für jede neue Tankstelle:
- Eigene ngrok Domain (z.B. `tankstelle2.ngrok.app`)
- Eigener PC mit eigenem ngrok Authtoken
- Auf tankstelle.gravuralarm.de kann man später zwischen Standorten unterscheiden
