# Content Hub 1.0

Ein Planungs-Tool für YouTube-Videos, das **komplett auf dem eigenen Gerät läuft**.
Kein Server, kein Account, kein Upload. Eine einzige HTML-Datei, die man per Doppelklick
im Browser öffnet.

---

## Inhalt des Ordners

| Datei             | Zweck                                                        |
| ----------------- | ------------------------------------------------------------ |
| `Content Hub.html` | Die komplette App. Mehr wird nicht gebraucht.                |
| `README.md`        | Diese Datei.                                                 |

Die App hat **keine** Abhängigkeiten: kein Build-Schritt, kein `npm install`, keine
externen Skripte. Nur die Schriftart `Stack Sans Notch` wird von Google Fonts geladen —
ist keine Internetverbindung da, fällt die App sauber auf die Systemschrift zurück.
Alles andere (Icons, ZIP-Erzeugung, Markdown-Darstellung) ist in der Datei selbst
implementiert.

---

## Starten

Doppelklick auf `Content Hub.html`. Beim ersten Start erscheint ein Overlay:

* **Profil anlegen** — Logo (optional), Name, Channel.
* **Profil importieren** — eine `.txt`, die früher exportiert wurde.

Danach landet man auf der **Startseite**, nicht direkt in einem Video.

---

## Aufbau

### Startseite

* Begrüßung mit Vornamen — **Moin** vor 11 Uhr, **Servus** bis 18 Uhr, sonst **Hallo**.
* Darunter eine Zeile mit laufenden Projekten und der nächsten Frist.
* **Current projects** — Karten mit Thumbnail, Status und Restzeit. Die Sortierung
  richtet sich nach der Deadline, Projekte ohne Datum stehen hinten. Die Restzeit ist
  farbig: grün (> 7 Tage), orange (≤ 7 Tage), rot (überfällig).
* **Calendar** — Monatsansicht, Montag zuerst. Tage mit Zieldatum sind markiert und
  anklickbar. Darunter die nächsten sechs Fristen als Liste.
* Der Schriftzug „Content Hub" steht auf der Startseite mittig; im Editor rutscht er
  nach links und ein **← Home**-Button erscheint. Ein Klick auf den Schriftzug führt
  ebenfalls zurück.

### Editor

Pro Video:

* **Thumbnail** in voller Größe (16:9, nichts wird beschnitten), per Klick, Drag & Drop
  oder Einfügen aus der Zwischenablage. Auflösung und Dateigröße werden eingeblendet,
  **Full size** öffnet das Original in einem eigenen Tab.
* **Titel, Status, Zieldatum, Kategorie, Tags.**
  Status: Idea → Planning → Filming → Cutting → Ready, jeweils mit eigener Farbe.
* **Project folder** und **Video** — absolute Pfade oder Links, mit *Open*- und
  *Copy*-Button.
* **Script** mit drei Ansichten: *Write*, *Read* (gerendertes Markdown) und
  **Teleprompter** (Vollbild, dunkel, Auto-Scroll). Wortzahl und geschätzte Sprechdauer
  laufen mit, gerechnet mit 150 Wörtern pro Minute.
* **Working description**, **Planning notes**, **Pre-production checklist**.

### Profil

Klick auf den Namen in der Navigationsleiste öffnet das Profil: Logo, Name, Channel und
die verbundenen Accounts — YouTube, Instagram, TikTok, X, Twitch, Facebook, LinkedIn,
Threads, Pinterest, Website. Jeder Eintrag hat Handle, Follower-Zahl und einen
*Open*-Button zum echten Profil. In der Seitenleiste zeigt **Reach** eine Kurzfassung.

> **Wichtig:** Die Follower-Zahlen werden von Hand eingetragen. Eine Seite, die lokal von
> der Festplatte läuft, kann diese Zahlen nicht automatisch abrufen — dafür bräuchte es
> API-Schlüssel und einen Server. Das Datum unter „checked" aktualisiert sich beim
> Eintippen von selbst.

---

## Markdown im Script

Unterstützt werden:

```
# Überschrift 1        ## Überschrift 2       ### Überschrift 3
**fett**   *kursiv*   `code`
- Aufzählung           1. Nummerierung
> Zitat
---                    (Trennlinie)
```

Zusätzlich gibt es **Cues**: Zeilen in eckigen Klammern (`[COLD OPEN]`) oder in
Großbuchstaben mit Doppelpunkt (`SPONSOR:`) werden in der Leseansicht und im
Teleprompter blau hervorgehoben.

* **Open .md** lädt eine Markdown-Datei ins Script. Eine führende `# Überschrift` wandert
  in den Titel, falls dieser noch leer ist.
* **Save .md** speichert das Script als `.md`.

---

## Speichern, Teilen, Gerätewechsel

### Auf dem Gerät

Automatisch im `localStorage` des Browsers, gebündelt mit allen Bildern. Getippte
Änderungen werden nach einer kurzen Pause geschrieben; beim Schließen des Tabs wird
sofort gespeichert.

**Wichtig:** `localStorage` gehört zu *einem* Browser auf *einem* Gerät. Ein anderer
Browser auf demselben Rechner sieht die Daten nicht. Es ist kein Backup — wer den
Browser-Cache leert, verliert die Daten. Regelmäßig exportieren.

### Export `.txt` — das Backup und der Umzug

Button **Export .txt** oder <kbd>Cmd</kbd>/<kbd>Ctrl</kbd>+<kbd>S</kbd>.

Die Datei ist zweigeteilt:

1. **Oben:** der Plan im Klartext — lesbar in jedem Editor, ausdruckbar, weitergebbar.
2. **Unten**, nach der Markierung `### CONTENT-HUB-DATA`: der exakte Zustand als JSON,
   **inklusive aller Bilder**.

Damit ist die `.txt` vollständig. Gerätewechsel heißt: exportieren, Datei kopieren,
drüben auf dem Startbildschirm importieren — Thumbnails und Logo sind mit dabei.

### Share `.zip` — zum Weitergeben

Button **Share .zip** oder <kbd>Alt</kbd>+<kbd>Z</kbd> packt das aktuelle Projekt in ein
ZIP-Archiv mit echten Dateien:

```
mein-video/
  script.md
  plan.txt
  notes.txt
  thumbnail.jpg
  logo.jpg
```

Gedacht für Cutter, Thumbnail-Designer oder das Archiv — Empfänger brauchen kein Content
Hub. Für den Umzug auf ein anderes Gerät ist die `.txt` die richtige Wahl, weil nur sie
den vollständigen Zustand enthält.

### Wie Bilder gespeichert werden

Als Base64-Data-URLs, also als Text direkt im Profil. Konsequenzen:

* Bilder reisen im Export mit, nichts hängt an Dateipfaden.
* Base64 ist rund ein Drittel größer als die Rohdatei. Deshalb werden Thumbnails auf
  max. 1920 px und Logos auf max. 512 px heruntergerechnet.
* `localStorage` ist je nach Browser bei etwa 5–10 MB gedeckelt, was ungefähr für 8–15
  Thumbnails reicht. Läuft der Speicher voll, zeigt die Navigationsleiste
  „Not saved — storage full, export instead", statt still zu scheitern. Dann exportieren
  und in Erwägung ziehen, alte Projekte zu löschen.

---

## Tastenkürzel

| Kürzel                                   | Wirkung                                  |
| ---------------------------------------- | ---------------------------------------- |
| <kbd>Cmd</kbd>/<kbd>Ctrl</kbd>+<kbd>S</kbd> | Profil als `.txt` exportieren         |
| <kbd>Alt</kbd>+<kbd>F</kbd>              | Projektordner öffnen                     |
| <kbd>Alt</kbd>+<kbd>V</kbd>              | Video öffnen                             |
| <kbd>Alt</kbd>+<kbd>Z</kbd>              | Projekt als `.zip` packen                |
| <kbd>Leertaste</kbd>                     | Teleprompter starten / pausieren          |
| <kbd>Esc</kbd>                           | Teleprompter schließen                    |

---

## Grenzen

Was diese Version bewusst **nicht** kann, und warum:

* **Keine automatischen Social-Media-Statistiken.** Braucht API-Schlüssel und einen
  Server; beides würde die Offline-Eigenschaft aufgeben.
* **Keine Synchronisierung zwischen Geräten.** Der Austausch läuft über die `.txt`.
* **Ordner und Videos öffnen** funktioniert, weil die Seite selbst von der Festplatte
  läuft (`file://` darf auf `file://` verlinken). Blockt ein Browser das Fenster, greift
  automatisch der *Copy*-Button.
* **Ein Profil pro Browser.** „Switch profile" ersetzt das gespeicherte Profil — vorher
  exportieren.

---

## Technische Notizen

* Reines ES5-taugliches JavaScript in einer IIFE, kein Framework, kein Build.
* Kein `innerHTML` mit Nutzerdaten. Alle Inhalte — Script, Titel, Notizen, Handles —
  werden über `textContent` bzw. DOM-Knoten gesetzt, auch der Markdown-Renderer.
  Eingefügter Text kann also kein Markup einschleusen.
* Das ZIP-Format wird direkt geschrieben (`store`, ohne Kompression, mit korrekter
  CRC32-Prüfsumme). Eine Bibliothek wäre für eine Handvoll kleiner Dateien nur Ballast,
  und JPEGs komprimieren ohnehin nicht weiter.
* Auf Ressourcenverbrauch geachtet: kein `backdrop-filter` und kein
  `background-attachment: fixed` (beide erzwingen großflächiges Neuzeichnen beim
  Scrollen), die Videoliste wird punktuell aktualisiert statt neu gebaut, die Wortzählung
  ist entkoppelt, das Speichern gebündelt, und der Teleprompter läuft über
  `requestAnimationFrame` — dadurch gleiches Tempo auf 60- und 120-Hz-Displays und keine
  Arbeit im Hintergrund-Tab.
* Getestete Bereiche: Export→Import-Roundtrip, ZIP-Struktur gegen das echte `unzip`
  (CRC-Prüfung, Umlaute, Binärdaten), Markdown-Klassifikation, Kalender-Arithmetik
  (Montag-Start, Schaltjahr, Monatslängen, Sommerzeit-Wechsel).

---

## Getestete Browser

Entwickelt gegen aktuelle Chromium-, Safari- und Firefox-Versionen auf macOS. Benötigt
werden `localStorage`, `FileReader`, `canvas.toDataURL`, `Blob`, `TextEncoder` und
`aspect-ratio` in CSS — alles seit 2021 überall vorhanden.
