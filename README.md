# 🧹 ADHS Planer

**ADHS-freundlicher Aufräum-Planer als PWA — KI schätzt Zeitaufwand pro Aufgabe, lernt aus deinen Realzeiten und wird über Sessions hinweg präziser. Foto-Analyse erkennt Aufgaben direkt aus Bildern. Inkl. KI-Tagesplan, Pomodoro-Timer, Session-Reporting und Offline-Unterstützung. Einzel-HTML-Datei, kein Backend.**

---

## Inhaltsverzeichnis

- [Features](#features)
- [Abhängigkeiten](#abhängigkeiten)
- [Installation & Hosting](#installation--hosting)
- [PWA — App auf dem iPhone installieren](#pwa--app-auf-dem-iphone-installieren)
- [Funktionen im Detail](#funktionen-im-detail)
- [API-Schlüssel](#api-schlüssel)
- [Datenschutz & Datenspeicherung](#datenschutz--datenspeicherung)

---

## Features

| Feature | Beschreibung |
|---|---|
| ✅ Aufgabenverwaltung | Vorgefertigte & eigene Aufgaben nach Raum sortiert |
| 🤖 KI-Zeitschätzung | Claude schätzt Minuten pro Aufgabe, adaptiert über Zeit |
| ⏱ Live-Zeitmessung | Timer läuft während der Aufgabe, Realzeit wird erfasst |
| 📈 Adaptives Lernen | KI lernt aus deinen Realzeiten und wird präziser |
| 📷 Foto-Analyse | Bis zu 10 Bilder hochladen, KI erkennt Aufgaben |
| 🧠 KI-Tagesplan | Personalisierter Plan je nach Zeit & Energie |
| 📊 Session-Reporting | Vollständige Analyse mit Mustern & Effizienz-Tipps |
| 💾 Persistentes Gedächtnis | Sessions werden gespeichert, KI lernt dauerhaft |
| 🎮 Gamification | XP-System, Level, Streak-Zähler |
| ⏰ Pomodoro-Timer | 25-Min-Blöcke mit automatischer Pause-Erinnerung |
| 📱 PWA | Installierbar auf iPhone & Android wie eine native App |
| 🌙 Dark Mode | Automatisch je nach System-Einstellung |
| ✈️ Offline | App funktioniert ohne Internet (KI-Funktionen benötigen Verbindung) |

---

## Abhängigkeiten

### Externe Abhängigkeiten

**Keine.** Die App ist eine vollständige Einzel-HTML-Datei ohne externe Libraries, Frameworks oder Build-Tools.

### Laufzeit-Abhängigkeiten

| Abhängigkeit | Zweck | Erforderlich |
|---|---|---|
| **Anthropic Claude API** | KI-Zeitschätzung, Foto-Analyse, Tagesplan, Reporting | Ja, für alle KI-Funktionen |
| **Moderner Browser** | Chrome 80+, Safari 14+, Firefox 80+, Edge 80+ | Ja |
| **HTTPS-Hosting** | Erforderlich für Service Worker / PWA | Ja, für PWA-Features |
| **Internetverbindung** | Nur für KI-Funktionen | Nein (App läuft offline) |

### Verwendete Browser-APIs

- `localStorage` — persistente Datenspeicherung (Sessions, Lernprofil)
- `Service Worker API` — Offline-Caching, PWA
- `Canvas API` — App-Icon-Generierung
- `FileReader API` — Foto-Upload & Bildverarbeitung
- `Fetch API` — Kommunikation mit der Anthropic API
- `Web App Manifest` — PWA-Installation
- `matchMedia` — Dark Mode Erkennung

---

## Installation & Hosting

### Voraussetzungen

- Eine einzige Datei: `adhs-planer.html`
- HTTPS-fähiges Hosting (für PWA/Service Worker zwingend erforderlich)
- Anthropic API-Zugang (die App nutzt `claude-sonnet-4-20250514`)

---

### Option A — Netlify Drop (empfohlen, 2 Minuten)

Die schnellste Methode ohne Account-Pflicht:

1. Gehe auf [netlify.com/drop](https://netlify.com/drop)
2. Ziehe die Datei `adhs-planer.html` per Drag & Drop auf die Seite
3. Netlify generiert automatisch eine URL (z. B. `https://amazing-name-123.netlify.app`)
4. Fertig — die App ist sofort öffentlich erreichbar

> **Hinweis:** Ohne Netlify-Account ist das Deployment temporär (nach einigen Stunden gelöscht). Mit kostenlosem Account bleibt die URL dauerhaft bestehen.

---

### Option B — GitHub Pages

Für eine dauerhafte, versionierte Lösung:

**1. Repository anlegen**

```bash
# Neues Repository auf github.com erstellen
# Name: adhs-planer
# Sichtbarkeit: Public (für GitHub Pages kostenlos erforderlich)
```

**2. Datei hochladen**

```bash
# Via Browser: "Add file" → "Upload files" → adhs-planer.html hochladen
# Oder via Git:
git init
git add adhs-planer.html README.md
git commit -m "Initial commit: ADHS Planer PWA"
git branch -M main
git remote add origin https://github.com/DEIN-USERNAME/adhs-planer.git
git push -u origin main
```

**3. GitHub Pages aktivieren**

```
Repository → Settings → Pages → Source: Deploy from a branch
Branch: main → / (root) → Save
```

**4. URL**

Nach 1–2 Minuten ist die App erreichbar unter:

```
https://DEIN-USERNAME.github.io/adhs-planer/adhs-planer.html
```

---

### Option C — Lokaler Entwicklungsserver

Zum Testen auf dem eigenen Rechner (HTTPS für PWA wird simuliert):

```bash
# Python 3
python3 -m http.server 8080

# Node.js (npx)
npx serve .

# Dann im Browser öffnen:
# http://localhost:8080/adhs-planer.html
```

> **Hinweis:** `localhost` gilt als sicherer Kontext — Service Worker und PWA-Features funktionieren auch ohne HTTPS lokal.

---

## PWA — App auf dem iPhone installieren

Sobald die App unter einer HTTPS-URL erreichbar ist:

1. URL in **Safari** öffnen (nicht Chrome oder Firefox — nur Safari unterstützt PWA-Installation auf iOS)
2. Unten in der Safari-Leiste das **Teilen-Symbol** (□↑) antippen
3. Im Menü nach unten scrollen → **„Zum Home-Bildschirm hinzufügen"** tippen
4. Name bestätigen → **„Hinzufügen"**

Die App erscheint als Icon auf dem Home-Bildschirm und öffnet sich im Vollbild ohne Browser-Leiste — wie eine native App.

> Der eingebaute Install-Banner in der App zeigt diese Anleitung auch automatisch an, wenn die App zum ersten Mal im Mobile-Browser geöffnet wird.

---

## Funktionen im Detail

### Aufgabenverwaltung

Die App enthält 13 vorgefertigte Aufgaben für die Räume Wohnzimmer, Küche, Schlafzimmer, Bad und Flur. Aufgaben können nach Raum gefiltert werden. Eigene Aufgaben lassen sich jederzeit mit Raumzuordnung hinzufügen. Jede Aufgabe zeigt die KI-Zeitschätzung (blau) und — nach Abschluss — die tatsächlich benötigte Realzeit (grün).

### KI-Zeitschätzung & Adaptives Lernen

Beim Hinzufügen einer neuen Aufgabe schätzt die KI automatisch die benötigte Zeit in Minuten. Über den Button „KI schätzt Zeiten" werden alle noch nicht geschätzten Aufgaben in einem einzigen API-Call bewertet. Die KI berücksichtigt dabei einen ADHS-spezifischen Zeitfaktor (typisch 1,3–1,8× mehr als neurotypische Schätzungen) und lernt aus den bereits erfassten Realzeiten der Person. Je mehr Aufgaben abgeschlossen werden, desto präziser werden die Schätzungen.

### Live-Zeitmessung & Zeiterfassung

Nach dem Antippen von „Starten" läuft ein sichtbarer Timer. Nach Abschluss einer Aufgabe erscheint ein Modal mit Zeitvorschlägen rund um die gemessene Zeit — die tatsächlich benötigte Zeit kann dort bestätigt oder korrigiert werden. Diese Realzeit wird dauerhaft im Lernprofil gespeichert.

### Foto-Analyse

Bis zu 10 Bilder von beliebigen Räumen können hochgeladen oder direkt mit der Kamera aufgenommen werden. Die KI analysiert alle Bilder gemeinsam, erkennt sichtbare Unordnung und leitet daraus konkrete, kleine Aufgaben ab (z. B. „Bücher vom Boden aufheben" statt „Zimmer aufräumen"). Die Zeitschätzungen werden dabei aus dem persönlichen Lernprofil abgeleitet. Erkannte Aufgaben können einzeln oder alle auf einmal in die Aufgabenliste übernommen werden.

### KI-Tagesplan

Basierend auf der verfügbaren Zeit (30 Min bis 3+ Stunden) und der aktuellen Energie (Gut / Mittel / Wenig) erstellt die KI einen realistischen Plan mit 3–4 Aufgaben. Pausen werden nach dem Pomodoro-Prinzip automatisch eingebaut. Bei wenig Energie werden leichtere Aufgaben zuerst priorisiert. Der Plan berücksichtigt die bekannten Realzeiten der Person und kann mit einem Klick in die Aufgabenliste übernommen werden. Ein eingebauter Chat-Coach beantwortet Fragen zur Session.

### Pomodoro-Timer

Der Fokus-Timer läuft für 25 Minuten und zählt abgelaufene Pomodoro-Blöcke. Nach jeweils 4 Blöcken erscheint automatisch ein Pause-Banner. Der Timer ist direkt in den Fokus-Bereich der Aufgabenliste integriert.

### Session-Reporting

Nach einer Session — oder jederzeit auf Knopfdruck — erstellt die KI einen vollständigen Bericht:

- **Metriken:** Abschlussrate, Gesamtzeit, KI-Genauigkeit in Prozent
- **Zeitvergleich:** Balkendiagramm KI-Schätzung vs. Realzeit pro Aufgabe
- **KI-Analyse:** Stärken der Session, erkannte Muster (z. B. ADHS-typisches Zeitverhalten), 3 konkrete Effizienz-Tipps für die nächste Session, Lernerkenntnisse für die KI, motivierende Zusammenfassung
- **Tipps für nächste Session:** 4 sofort umsetzbare, kategorisierte Tipps (Zeit / Fokus / Reihenfolge / Belohnung)

Alle Sessions werden im `localStorage` gespeichert. Bei der nächsten Session kennt die KI die gesamte Vorgeschichte und kann gezieltere Empfehlungen geben. Die Session-History zeigt alle vergangenen Sessions mit Datum, Abschlussrate und Genauigkeits-Tags.

### Gamification

Jede abgeschlossene Aufgabe gibt XP-Punkte (abhängig von der Aufgabenschwere). XP füllen eine Level-Leiste — alle 100 XP steigt das Level. Ein Streak-Zähler zählt ohne Unterbrechung erledigte Aufgaben. Nach jeder erledigten Aufgabe erscheint eine kurze Toast-Nachricht mit XP-Gewinn und Vergleich zur KI-Schätzung.

### Offline & PWA

Der eingebettete Service Worker cached die App beim ersten Laden vollständig. Bei fehlender Internetverbindung erscheint ein Offline-Badge — die App bleibt aber vollständig nutzbar (Aufgaben, Timer, Gamification). Nur die Funktionen, die die Claude API benötigen (KI-Schätzung, Foto-Analyse, Tagesplan, Reporting), erfordern eine aktive Internetverbindung.

---

## API-Schlüssel

Die App kommuniziert direkt vom Browser mit der Anthropic API. Da die Datei öffentlich gehostet wird, sollte **kein API-Schlüssel hartcodiert** werden.

Die App sendet API-Anfragen ohne expliziten Key — der Zugriff wird über das Claude.ai-Interface ermöglicht, wenn die App innerhalb der claude.ai-Umgebung genutzt wird. Für eigenständiges Hosting außerhalb von claude.ai muss der API-Key in der Funktion `callAI()` ergänzt werden:

```javascript
async function callAI(prompt, maxTokens = 600) {
  const r = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': 'sk-ant-DEIN-KEY-HIER',  // ← hier einfügen
      'anthropic-version': '2023-06-01',
      'anthropic-dangerous-direct-browser-access': 'true',
    },
    body: JSON.stringify({ ... })
  });
}
```

> ⚠️ **Sicherheitshinweis:** Einen API-Key niemals in einer öffentlich zugänglichen Datei auf GitHub speichern. Für produktiven Einsatz einen serverseitigen Proxy verwenden.

---

## Datenschutz & Datenspeicherung

Alle Daten werden **ausschließlich lokal** im Browser gespeichert (`localStorage`). Es gibt keinen Server, keine Datenbank und keine externe Datenweitergabe außer den API-Anfragen an Anthropic für die KI-Funktionen. Fotos werden nicht hochgeladen — sie werden als Base64 direkt im API-Request an Claude gesendet und danach verworfen.

Über den Button „Gedächtnis zurücksetzen" im Report-Tab können alle gespeicherten Daten jederzeit vollständig gelöscht werden.

---

## Lizenz

MIT License — frei nutzbar, anpassbar und weitergabe erlaubt.
