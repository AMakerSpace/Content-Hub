# 🧠 Content Hub 1.0 — Technische Referenz

Für alle, die genauer wissen wollen, was unter der Haube passiert.
Für den Einstieg reicht die [README](README.md). 👈

---

## 📦 Aufbau

| Datei | Zweck |
| ----- | ----- |
| `Content Hub 1.0/Content Hub.html` | Die komplette App — Markup, CSS und Logik in einer Datei |
| `README.md` | Einstieg für Anwender |
| `ADVANCED.md` | Dieses Dokument |

**Keine Abhängigkeiten:** kein Build-Schritt, kein `npm install`, keine externen Skripte.
Einzige Ausnahme ist die Schriftart `Stack Sans Notch` von Google Fonts — ohne
Internetverbindung fällt die App per `font-family`-Kette sauber auf die Systemschrift
zurück. Icons, ZIP-Erzeugung und Markdown-Rendering sind selbst implementiert.

---

## 🎨 Oberfläche im Detail

### 🏠 Startseite

* Begrüßung nach Uhrzeit: **Moin** vor 11 Uhr, **Servus** bis 18 Uhr, sonst **Hallo**.
* **Current projects** — sortiert nach Deadline, Projekte ohne Datum stehen hinten.
  Farbschwelle der Restzeit: grün > 7 Tage, orange ≤ 7 Tage, rot überfällig.
* **Calendar** — Monatsansicht mit Montag-Start. Tage mit Zieldatum sind markiert,
  anklickbar und zeigen beim Hover alle Termine des Tages. Darunter die nächsten sechs
  Fristen.
* Der Schriftzug „Content Hub" steht auf der Startseite mittig; im Editor rutscht er nach
  links, ein **← Home**-Button erscheint. Ein Klick auf den Schriftzug führt ebenfalls
  zurück.

### 📝 Editor

* **Thumbnail** in voller Breite (16:9, nichts wird beschnitten) — per Klick, Drag & Drop
  oder aus der Zwischenablage. Auflösung und Dateigröße werden eingeblendet, **Full size**
  öffnet das Original in einem eigenen Tab.
* **Status:** Idea → Planning → Filming → Cutting → Ready, jeweils mit eigener Farbe, die
  auch Liste und Kalender einfärbt.
* **Project folder / Video** — absolute Pfade oder Links mit *Open* und *Copy*.
* **Script** in drei Ansichten: *Write*, *Read* (gerendertes Markdown) und *Teleprompter*.
  Wortzahl und geschätzte Sprechdauer laufen mit, gerechnet mit **150 Wörtern pro Minute**.

---

## ✍️ Markdown im Script

Unterstützte Syntax:

```
# Überschrift 1        ## Überschrift 2       ### Überschrift 3
**fett**   *kursiv*   `code`
- Aufzählung           1. Nummerierung
> Zitat
---                    (Trennlinie)
```

**Cues** sind eine Besonderheit: Zeilen in eckigen Klammern (`[COLD OPEN]`) oder in
Großbuchstaben mit Doppelpunkt (`SPONSOR:`) werden in der Leseansicht und im Teleprompter
blau hervorgehoben.

* **Open .md** lädt eine Markdown-Datei ins Script. Eine führende `# Überschrift` wandert
  in den Titel, falls dieser noch leer ist.
* **Save .md** speichert das Script als `.md`.

---

## 💾 Speicherformat

### Auf dem Gerät

Automatisch im `localStorage` des Browsers, gebündelt mit allen Bildern. Getippte
Änderungen werden gebündelt nach einer kurzen Pause geschrieben; beim Schließen des Tabs
wird sofort gespeichert (`beforeunload`), damit ein ausstehender Debounce keine Arbeit
verliert.

`localStorage` gehört zu *einem* Browser auf *einem* Gerät und ist **kein Backup**.

### Export `.txt`

Die Exportdatei ist bewusst zweigeteilt:

1. **Oben:** der Plan im Klartext — lesbar in jedem Editor, ausdruckbar, weitergebbar.
2. **Unten**, nach der Markierung `### CONTENT-HUB-DATA`: der exakte Zustand als JSON,
   **inklusive aller Bilder**.

Dadurch ist dieselbe Datei gleichzeitig menschenlesbar und ein vollständiges Backup. Der
Import sucht nach der Markierung und liest nur den JSON-Teil — der Klartext darüber darf
also gefahrlos bearbeitet werden.

### Share `.zip`

Packt das aktuelle Projekt als echtes ZIP-Archiv:

```
mein-video/
  script.md
  plan.txt
  notes.txt
  thumbnail.jpg
  logo.jpg
```

Für den **Gerätewechsel** ist trotzdem die `.txt` die richtige Wahl, weil nur sie den
vollständigen Zustand aller Projekte enthält.

### 🖼️ Wie Bilder gespeichert werden

Als Base64-Data-URLs, also als Text direkt im Profil. Konsequenzen:

* ✅ Bilder reisen im Export mit, nichts hängt an Dateipfaden.
* ⚠️ Base64 ist rund ein Drittel größer als die Rohdatei. Deshalb werden Thumbnails auf
  max. **1920 px** und Logos auf max. **512 px** heruntergerechnet.
* ⚠️ `localStorage` ist je nach Browser bei etwa **5–10 MB** gedeckelt, was ungefähr für
  8–15 Thumbnails reicht. Läuft der Speicher voll, zeigt die Navigationsleiste
  *„Not saved — storage full, export instead"*, statt still zu scheitern.

---

## 🚧 Grenzen — und warum

* **Keine automatischen Social-Media-Statistiken.** Braucht API-Schlüssel und einen
  Server; beides würde die Offline-Eigenschaft aufgeben.
* **Keine Synchronisierung zwischen Geräten.** Der Austausch läuft über die `.txt`.
* **Ordner und Videos öffnen** funktioniert, weil die Seite selbst von der Festplatte läuft
  (`file://` darf auf `file://` verlinken). Blockt ein Browser das Fenster, greift
  automatisch der *Copy*-Button.
* **Ein Profil pro Browser.** *Switch profile* ersetzt das gespeicherte Profil — vorher
  exportieren.

---

## 🔒 Sicherheit

* Kein `innerHTML` mit Nutzerdaten. Alle Inhalte — Script, Titel, Notizen, Handles —
  werden über `textContent` bzw. DOM-Knoten gesetzt, auch der Markdown-Renderer.
  Eingefügter Text kann also kein Markup einschleusen.
* Keine Netzwerkaufrufe außer dem Stylesheet der Schriftart. Es gibt keine Stelle im Code,
  die Nutzerdaten irgendwohin sendet.

---

## ⚡ Performance

* Reines ES5-taugliches JavaScript in einer IIFE, kein Framework, kein Build.
* Das ZIP-Format wird direkt geschrieben (`store`, ohne Kompression, mit korrekter
  CRC32-Prüfsumme). Eine Bibliothek wäre für eine Handvoll kleiner Dateien nur Ballast,
  und JPEGs komprimieren ohnehin nicht weiter.
* Die Videoliste wird punktuell aktualisiert statt neu gebaut: Tippen im Titel patcht drei
  Textknoten, statt die Liste bei jedem Tastendruck zu verwerfen.
* Die Wortzählung ist entkoppelt (Debounce), das Speichern gebündelt.
* Der Teleprompter läuft über `requestAnimationFrame` — gleiches Tempo auf 60- und
  120-Hz-Displays, keine Arbeit im Hintergrund-Tab.
* Kein `background-attachment: fixed` (erzwingt großflächiges Neuzeichnen beim Scrollen).
* **Animationen** bewegen ausschließlich `opacity` und `transform`, laufen also auf dem
  Compositor ohne Layout- oder Repaint-Arbeit pro Frame. Alle Übergänge sind einmalig und
  kurz (0,12–0,26 s), nichts läuft dauerhaft. `prefers-reduced-motion` schaltet alles ab.
* `backdrop-filter` wird an genau **einer** Stelle eingesetzt: der Navigationsleiste. Der
  Effekt kostet dort wenig, weil die Fläche klein und konstant ist — großflächig
  eingesetzt wäre er ein Performance-Problem.

---

## 🧪 Getestete Bereiche

* Export → Import-Roundtrip
* ZIP-Struktur gegen das echte `unzip`: CRC-Prüfung, Umlaute, Binärdaten
* Markdown-Klassifikation
* Kalender-Arithmetik: Montag-Start, Schaltjahr, Monatslängen, Sommerzeit-Wechsel

---

## 🌐 Browser-Anforderungen

Entwickelt gegen aktuelle Chromium-, Safari- und Firefox-Versionen auf macOS. Benötigt
werden `localStorage`, `FileReader`, `canvas.toDataURL`, `Blob`, `TextEncoder` und
`aspect-ratio` in CSS — alles seit 2021 überall vorhanden.

---

© Arthur Pletzer 2026
