# 🟠 Budget – mein privates Haushaltsbuch

**Aktuelle Version: 3.2.0** · siehe [Versionsverlauf](#-versionsverlauf)

Web-App fürs iPhone (wie das LadeLog).

**Funktionen (v3 – Fixkosten-Analyse)**
- **Übersicht:** Hauptzahl „Frei nach Fixkosten“ (Eingang − Fixkosten − Kredite − Sparen), Geldfluss, Fixquote, Fixkosten nach Kategorie
- **Eingänge:** Gehalt pro Monat (schwankt) plus **Sonstige Eingänge** (eBay-Verkauf, Geschenke …) – getrennt vom Gehalt
- **Jahr:** Gehalt gesamt, Ø, höchster/niedrigster Monat, Diagramm mit Fixkosten, Jahresbilanz, Monatstabelle
- **Monatsrückblick:** öffnet sich beim ersten Start im neuen Monat; später über Übersicht (Vormonat wählen) oder Jahr → Monat erneut abrufbar
- **Fixkosten versioniert** (Startmonat, Ende, „neuer Betrag gilt ab“), **Kredite** (auch mit Start in der Zukunft), **Sparziele**
- **Kontoauszüge (PDF) importieren** – auch ein ganzes Jahr auf einmal, inkl. Zinsen vom Tagesgeld (siehe unten)
- **Alltagsausgaben optional** – manuell oder per Screenshot, mit Prognose, was am Monatsende übrig bleibt
- PIN + Touch ID / Face ID, AES-256, verschlüsselter Sync zwischen Geräten

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
2. Auf der leeren Repo-Seite: **uploading an existing file** → alle Dateien aus diesem Ordner hineinziehen (inkl. Ordner `icons` und `sounds`) → **Commit changes**
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

## Kontoauszüge (PDF) importieren

*Plus-Menü → Kontoauszüge (PDF)*, oder unter *Jahr*, *Eingänge* bzw. *Einstellungen*. Mehrere PDFs auf einmal auswählen (z. B. alle Auszüge eines Jahres aus der Dateien-App).

- Ausgewertet wird **nur auf dem Gerät**. Beim ersten Mal lädt die App den PDF-Leser (pdf.js, ca. 2 MB) von cdn.jsdelivr.net – deine PDFs werden nicht übertragen.
- Passwortgeschützte PDFs: Die App fragt nach dem Passwort.
- Automatische Zuordnung, vor dem Übernehmen prüfbar:
  - **Gehalt** → ersetzt/ergänzt das Gehalt des Monats (schon vorhandene gleiche Beträge werden erkannt)
  - **Zinsen** → pro Monat zu einem Eintrag zusammengefasst (netto, Steuern abgezogen), aus allen Konten/Unterkonten; werden erfasst, aber **nicht als Einnahme** gezählt
  - **Abbuchungen, die zu Fixkosten oder Kreditraten passen** → nur bestätigt, nicht doppelt gezählt
  - **Wiederkehrende Abbuchungen** (≥ 3 Monate) → Vorschlag „als neue Fixkosten anlegen“
  - **Umbuchungen** zu Unterkonten/Tagesgeld, Überweisungen an/von dir selbst und ans Gemeinschaftskonto → ignoriert (umstellbar)
  - **Mehrere Konten im PDF** (z. B. Revolut: Girokonto + „Einzahlung“-Unterkonten) → du wählst, welche berücksichtigt werden (Standard: nur Girokonto)
  - **Auswahl:** alles einzeln an-/abhakbar, „alle an/aus“ je Abschnitt; Alltagsausgaben und unklare Eingänge (PayPal, Erstattungen, Personen) sind standardmäßig nicht angehakt
  - Rest → Alltagsausgaben (optional) oder sonstige Eingänge
- Funktioniert mit Text-PDFs (Vorzeichen, S/H oder Soll-/Haben-Spalten). Eingescannte Auszüge (Bilder) werden nicht erkannt.

## Weitere Personen

Die App kann jeder mit dem Link nutzen – **jede Person hat ihren eigenen, getrennten Tresor** auf ihrem iPhone mit eigener PIN. Niemand sieht die Zahlen der anderen.

1. In der App: *Einstellungen → Für eine andere Person einrichten → Link teilen*
2. Die Person öffnet den Link in **Safari** → Teilen → **Zum Home-Bildschirm**
3. App öffnen, eigene PIN festlegen – fertig

### Partner über dein GitHub (ohne eigenes Konto)

Erstelle für deinen Partner einen **zweiten Token** (gleiches Vorgehen wie bei dir, nur Repo `budget-daten`, *Contents: Read and write*, Name z. B. `Budget-Partner`). So kannst du seinen Zugang jederzeit einzeln widerrufen.

In seiner App unter *Einstellungen → Sync über GitHub*:

| Feld | Gemeinsames Haushaltsbudget | Getrenntes eigenes Budget |
|---|---|---|
| Benutzername | dein GitHub-Name | dein GitHub-Name |
| Repo | `budget-daten` | `budget-daten` |
| Token | sein Token | sein Token |
| Dateiname | `budget.enc.json` (wie bei dir) | eigener, z. B. `budget-partner.enc.json` |
| Sync-Passwort | **dasselbe** wie deins | **eigenes** |

Beim getrennten Budget kann er deine Datei ohne dein Sync-Passwort nicht lesen.

## Updates

Neue Dateien über **Add file → Upload files** hochladen (gleichnamige werden ersetzt). In der App dann einfach **von oben nach unten ziehen** – sie erkennt die neue Version und lädt sie. Die Versionsnummer steht unter *Einstellungen → Version*.

## Wichtig

- **PIN vergessen = Daten weg.** Deshalb ab und zu unter *Einstellungen* ein verschlüsseltes Backup in iCloud Drive speichern (oder Sync nutzen).
- Die App sperrt sich nach 1 Minute im Hintergrund.
- **Screenshot-Import:** Beim ersten Mal lädt die App das Texterkennungs-Programm (Tesseract, ca. 10 MB) von cdn.jsdelivr.net. Dabei wird **nichts** von dir übertragen – die Bilder werden ausschließlich auf dem iPhone ausgewertet. Erkennung immer kurz prüfen, bevor du übernimmst.

## 📜 Versionsverlauf

Schema: **Haupt.Neben.Fehlerbehebung** – z. B. 2.1.0 = neue Funktionen, 2.1.1 = nur Fehler behoben, 3.0.0 = großer Umbau.

### 3.2.0 – 28.11.2026
- 🏦 Import an Revolut-Auszüge angepasst (Spalten Geldausgang/Geldeingang, Abschnitte Girokonto/Einzahlung, Kontoinhaber-Erkennung)
- 🗂️ Kontenauswahl in der Prüfliste – Standard: nur das Girokonto
- 📈 Zinsen je Monat zusammengefasst (aus allen Unterkonten) und **nicht mehr als Einnahme** gezählt – angezeigt als „Zinsen erhalten · nicht eingerechnet“
- 🔁 Umbuchungen zu Unterkonten, Eigenüberweisungen und Gemeinschaftskonto werden erkannt
- ☑️ „alle an/aus“ je Abschnitt; Alltag und unklare Eingänge standardmäßig abgewählt; strengerer Fixkosten-Abgleich (keine Zufallstreffer bei gleichem Betrag); bessere Namen und Kategorien

### 3.1.0 – 28.11.2026
- 📄 Kontoauszüge als PDF einlesen – mehrere auf einmal für ein ganzes Jahr, passwortgeschützte PDFs möglich, Auswertung nur auf dem Gerät
- 🔎 Automatische Zuordnung mit Prüfliste: Gehalt (ersetzt/ergänzt), Zinsen, sonstige Eingänge, Abgleich mit Fixkosten & Kreditraten, wiederkehrende Abbuchungen als neue Fixkosten, Umbuchungen ignorieren, Rest als Alltag; Doppelte werden erkannt
- 📈 Neue Eingangsart **Zinsen** (Tagesgeld, netto nach Kapitalertragsteuer/Soli) in Übersicht, Eingänge, Jahr und Rückblick

### 3.0.0 – 27.11.2026
- 🧭 Neue Ausrichtung als **Fixkosten-Analyse**: Hauptzahl „Frei nach Fixkosten“, Geldfluss-Karte, Fixquote
- 📊 Neuer Tab **Jahr** (ersetzt „Monat“): Gehalt gesamt, Ø, höchster/niedrigster Monat, Diagramm, Jahresbilanz, Monatstabelle
- 📅 **Monatsrückblick** mit Vergleich zum Vormonat, Fixquote, Sparquote, automatischen Erkenntnissen (Gehaltsänderung, neue/geänderte/weggefallene Fixkosten, Kreditstand, Sparziele) und Ausblick
- 🎁 **Sonstige Eingänge** getrennt vom Gehalt; bestehende Einträge werden automatisch zugeordnet (Name mit „Gehalt/Lohn“ = Gehalt)
- 🧾 Alltagsausgaben als optionaler Bereich mit **Prognose Monatsende**; erreichbar über die Übersicht
- ➕ Erfassen-Menü: Gehalt und Fixkosten zuerst, Sonstiges & Alltag darunter

### 2.6.2 – 27.11.2026
- 🐞 Gehalt stapelte sich über die Monate (geschätzter Vormonatswert wurde beim Hinzufügen als echter Eintrag mitkopiert) – behoben; betroffene Monate werden beim ersten Öffnen automatisch bereinigt
- 🐞 Fixkosten: Startmonat wird beim Bearbeiten korrekt angezeigt (nicht mehr der gerade gewählte Monat); neues Feld „Endet nach“; „Neuer Betrag gilt ab“ erscheint nur bei Betragsänderung

### 2.6.1 – 27.11.2026
- 🐞 Kredite mit Start in der Zukunft: Startmonat („Erste Rate im“) wird nicht mehr auf den aktuellen Monat zurückgesetzt; Raten zählen erst ab der ersten Rate; Laufzeit und Enddatum werden ab Start berechnet; Feld heißt dann „Kreditbetrag zum Start“

### 2.6.0 – 27.11.2026
- 🔓 Entsperren mit Touch ID / Face ID über einen Passkey (WebAuthn-PRF): *Einstellungen → Touch ID / Face ID* einschalten. Die PIN wird mit einem Schlüssel verschlüsselt, den nur der Fingerabdruck freigibt; PIN bleibt als Ausweg. Fingerabdruck-Taste unten links im Tastenfeld. Benötigt iOS 18 oder neuer.

### 2.5.0 – 27.11.2026
- 💸 Viel mehr Geld: ca. 45 Scheine – Schwall vom Speichern-Knopf plus Geldregen von oben über den ganzen Bildschirm
- 💶 Realistischere Scheine im Stil der Euro-Serie (5 € bis 200 €): echte Farben, Torbogen-Motiv je Schein, Sternenkranz, Silberstreifen, „EURO ΕΥΡΩ“ – bewusst stilisiert (keine Banknoten-Kopie)
- ➕ Plus-Knopf in der unteren Leiste exakt zentriert, rund und weiß

### 2.4.0 – 27.11.2026
- 💰 Neuer Standard-Sound „Katsching!“ als Datei `sounds/katsching.mp3` (Stille entfernt, auf 1,6 s gekürzt, lauter) – andere Sounds weiter wählbar
- ⚠️ Beim Update den Ordner `sounds` mit hochladen

### 2.3.0 – 27.11.2026
- 🎵 Eigener Sound: kurze Audiodatei (MP3, M4A, WAV) aus der Dateien-App als Speicher-Sound wählen – bleibt nur auf dem Gerät (nicht auf GitHub), Stille am Anfang wird abgeschnitten, max. 4 Sekunden

### 2.2.0 – 27.11.2026
- 🤑 Neuer Standard-Sound „Ka-Sching!“ (Verkaufs-Sound im eBay-Stil, selbst erzeugt) – wählbar: Ka-Sching, Registrierkasse, Münzen oder aus (*Einstellungen → Sound*, antippen zum Anhören)
- 📲 *Für eine andere Person einrichten*: Link teilen + Kurzanleitung in der App
- ☁️ Sync: frei wählbarer Dateiname – getrennte oder gemeinsame Budgets im selben Repo

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
