# 🟠 Budget – mein privates Haushaltsbuch

**Aktuelle Version: 2.1.0** · siehe [Versionsverlauf](#-versionsverlauf)

Web-App fürs iPhone (wie das LadeLog).

**Funktionen (v2)**
- **Monate mit Historie:** Gehalt jeden Monat neu eintragen (schwankt ja), Verlauf der letzten 6 Monate
- **Fixkosten versioniert:** Änderung „gilt ab Monat X“ – frühere Monate bleiben korrekt
- **Sparen zählt als Ausgabe** (Kategorie 🐷), nichts wird doppelt gerechnet
- **Variable Ausgaben** manuell oder per **Screenshot aus der Banking-App** – Texterkennung läuft lokal auf dem iPhone, Kategorien werden vorgeschlagen und die App lernt aus deinen Korrekturen
- **Kredite/Abzahlungen** mit Restschuld, Zins, Restlaufzeit und „schuldenfrei im …“
- **Sparziele** frei definierbar, mit Fortschritt, nötiger Monatsrate und Einzahlungen

## So bleibt alles privat

| Was | Wo | Wer kann es sehen? |
|---|---|---|
| App-Code (diese Dateien) | GitHub Pages | Theoretisch jeder mit Link – enthält aber **keine einzige Zahl** von dir |
| Deine Daten | Im Browser-Speicher des iPhones, **AES-256 verschlüsselt** mit deiner 6-stelligen PIN | Nur du |
| Sync (optional) | Verschlüsselte Datei in einem **zweiten, privaten** Repo | Nur du – und selbst GitHub sieht nur Zeichensalat |

➡️ Lege **niemals** eine Datei mit deinen Zahlen (z. B. `meine-startdaten-NICHT-hochladen.json`) in dieses Repo.

## Einrichten – komplett im Browser, nichts installieren

1. Auf <https://github.com> einloggen → oben rechts **+** → **New repository**
   - Name: `budget` · Sichtbarkeit: **Public** (nötig für kostenloses GitHub Pages – siehe oben, im Code steht nichts Privates)
   - **Create repository**
2. Auf der leeren Repo-Seite: **uploading an existing file** → alle Dateien aus diesem Ordner hineinziehen (inkl. Ordner `icons`) → **Commit changes**
3. **Settings → Pages** → *Source*: **Deploy from a branch** → Branch **main** / **(root)** → **Save**
4. Nach 1–2 Minuten läuft die App unter `https://DEIN-NAME.github.io/budget/`

## Aufs iPhone holen

1. Adresse in **Safari** öffnen
2. Teilen-Symbol → **Zum Home-Bildschirm**
3. App öffnen → 6-stellige PIN festlegen
4. Gehalt und Fixkosten eintragen (orangenes **+**)

## Optional: Sync zwischen iPhone und MacBook

1. Zweites Repo anlegen: Name `budget-daten`, Sichtbarkeit **Private**, Haken bei *Add a README*
2. Token erstellen: Profilbild → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**
   - Repository access: **Only select repositories** → `budget-daten`
   - Permissions → Repository → **Contents: Read and write**
   - Ablaufdatum z. B. 1 Jahr → Token kopieren
3. In der App: **Einstellungen (Regler-Symbol oben) → Sync über GitHub → Einrichten** → Benutzername, `budget-daten`, Token und ein **Sync-Passwort** eintragen
4. Auf dem zweiten Gerät dasselbe eintragen (gleiches Sync-Passwort) – der Stand wird geladen

Danach lädt die App nach jeder Änderung automatisch hoch und holt beim Entsperren den neuesten Stand.

## Updates

Neue Dateien über **Add file → Upload files** hochladen (gleichnamige werden ersetzt). In der App dann einfach **von oben nach unten ziehen** – sie erkennt die neue Version und lädt sie. Die Versionsnummer steht unter *Einstellungen → Version*.

## Wichtig

- **PIN vergessen = Daten weg.** Deshalb ab und zu unter *Einstellungen* ein verschlüsseltes Backup in iCloud Drive speichern (oder Sync nutzen).
- Die App sperrt sich nach 1 Minute im Hintergrund.
- **Screenshot-Import:** Beim ersten Mal lädt die App das Texterkennungs-Programm (Tesseract, ca. 10 MB) von cdn.jsdelivr.net. Dabei wird **nichts** von dir übertragen – die Bilder werden ausschließlich auf dem iPhone ausgewertet. Erkennung immer kurz prüfen, bevor du übernimmst.

## 📜 Versionsverlauf

Schema: **Haupt.Neben.Fehlerbehebung** – z. B. 2.1.0 = neue Funktionen, 2.1.1 = nur Fehler behoben, 3.0.0 = großer Umbau.

### 2.1.0 – 27.11.2026
- 💶 Kassen-Sound („Ka-Ching“) beim Speichern – in den Einstellungen abschaltbar (bei aktivem Stummschalter am iPhone ggf. lautlos)
- 💸 Geldscheine (5 € bis 100 €) fliegen durch die Luft statt Konfetti
- 📱 Sperrbildschirm passt sich der Displayhöhe an – Logo auf dem iPhone-Duo-Außendisplay nicht mehr gestaucht/abgeschnitten
- 🔄 Ziehen zum Aktualisieren: holt den Sync-Stand und erkennt neue App-Versionen
- ☁️ Sync führt Änderungen von PC und iPhone zusammen statt zu überschreiben (je Eintrag gewinnt die neuere Änderung, Gelöschtes bleibt gelöscht); automatischer Abgleich beim Zurückkehren in die App und alle 3 Minuten
- 🏷️ Versionsnummer und „Was ist neu“ in den Einstellungen, Hinweis nach einem Update

### 2.0.0 – 27.11.2026
- 📅 Monate mit Historie – Gehalt jeden Monat neu eintragen, Verlauf über 6 Monate
- 🗂️ Fixkosten versioniert („gilt ab Monat“), Historie bleibt korrekt
- 🐷 Sparen zählt als Ausgabe (keine Doppelbelastung)
- 📷 Variable Ausgaben per Screenshot aus der Banking-App (Texterkennung auf dem Gerät) mit lernenden Kategorien
- 🏦 Kredite & Abzahlungen mit Restschuld, Zins und Enddatum
- 🎯 Frei definierbare Sparziele mit Fortschritt und Einzahlungen
- ➕ Neues Schnellmenü über das orange Plus

### 1.0.0 – 27.11.2026
- 🚀 Erste Version: Gehalt, Fixkosten, Kategorien, Übersicht mit Ring und Balken, Fälligkeiten
- 🔐 6-stellige PIN, AES-256-Verschlüsselung auf dem Gerät, Auto-Sperre
- ☁️ Optionaler verschlüsselter Sync über privates GitHub-Repo, verschlüsseltes Backup
