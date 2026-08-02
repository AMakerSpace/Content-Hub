# 🎬 Content Hub 1.0

**Dein YouTube-Videoplaner — eine einzige Datei, die auf deinem Rechner läuft.**

Kein Account 🙅, kein Server 🙅, kein Upload 🙅. Du machst einen Doppelklick, und es läuft.
Alles bleibt auf deinem Gerät.

---

## 🚀 In 60 Sekunden loslegen

1. 📂 Öffne den Ordner `Content Hub 1.0`
2. 🖱️ Doppelklick auf **`Content Hub.html`** — die App öffnet sich im Browser
3. 👤 Lege dein Profil an: Name, Channel, optional ein Logo
4. ➕ Klick auf **New video** und tippe deinen Titel
5. 💾 Fertig — gespeichert wird automatisch, während du tippst

> 💡 **Tipp:** Lege dir ein Lesezeichen an oder zieh die Datei ins Dock, dann findest du sie
> immer wieder.

---

## 🧭 Was du wo findest

### 🏠 Startseite

Deine Übersicht. Hier siehst du alle laufenden Projekte als Karten mit Thumbnail und
Status — und einen Kalender mit deinen Deadlines.

Die Restzeit ist farbig, damit du sie auf einen Blick erfassen kannst:

| Farbe | Bedeutung |
| ----- | --------- |
| 🟢 Grün | Noch mehr als 7 Tage Zeit |
| 🟠 Orange | Weniger als 7 Tage — wird eng |
| 🔴 Rot | Deadline ist vorbei |

### 📝 Editor

Klick auf ein Projekt, und du bist drin. Pro Video gibt es:

* 🖼️ **Thumbnail** — reinziehen, einfügen oder anklicken zum Auswählen
* ✏️ **Titel, Status, Zieldatum, Kategorie, Tags**
* 📁 **Ordner & Videolink** — mit *Open*- und *Copy*-Button
* 🎤 **Script** in drei Ansichten: schreiben, lesen und **Teleprompter** (Vollbild mit
  Auto-Scroll — perfekt fürs Aufnehmen)
* 🗒️ **Beschreibung, Notizen und Checkliste** für die Vorbereitung

Der Status führt dich durch die Produktion:

```
💡 Idea → 🗓️ Planning → 🎥 Filming → ✂️ Cutting → ✅ Ready
```

### 👤 Profil

Klick oben auf deinen Namen. Dort pflegst du dein Logo und deine Social-Media-Accounts
(YouTube, Instagram, TikTok, X, Twitch und mehr).

> ⚠️ Die Follower-Zahlen trägst du **selbst** ein. Eine App ohne Server kann diese Zahlen
> nicht automatisch abrufen — dafür bräuchte es API-Schlüssel und einen Anbieter im
> Hintergrund. Genau das wollen wir hier nicht.

---

## 💾 Deine Daten sichern — bitte lesen! ⚠️

Content Hub speichert automatisch **im Speicher deines Browsers**. Das ist bequem, aber
**es ist kein Backup**:

* ❌ Browser-Verlauf oder Cache gelöscht → Daten weg
* ❌ Anderer Browser auf demselben Rechner → sieht deine Daten nicht
* ❌ Anderer Computer → sieht deine Daten nicht

**Die Lösung:** ab und zu auf **Export .txt** klicken (oder <kbd>Cmd</kbd>/<kbd>Ctrl</kbd> +
<kbd>S</kbd>). Diese eine Datei enthält **alles** — auch deine Bilder. Leg sie in deine
Cloud oder auf eine Festplatte. 🗄️

**Umzug auf einen neuen Rechner?** Exportieren → Datei mitnehmen → dort beim Start auf
*Profil importieren* klicken. Fertig. ✨

### 📦 Ein Projekt weitergeben

**Share .zip** (oder <kbd>Alt</kbd> + <kbd>Z</kbd>) packt ein einzelnes Projekt als
normalen Ordner mit echten Dateien:

```
mein-video/
  script.md
  plan.txt
  notes.txt
  thumbnail.jpg
```

Ideal für deinen Cutter oder Thumbnail-Designer — die brauchen kein Content Hub, um das zu
öffnen. 🤝

---

## ⌨️ Tastenkürzel

| Kürzel | Wirkung |
| ------ | ------- |
| <kbd>Cmd</kbd>/<kbd>Ctrl</kbd> + <kbd>S</kbd> | 💾 Alles als `.txt` sichern |
| <kbd>Alt</kbd> + <kbd>Z</kbd> | 📦 Projekt als `.zip` packen |
| <kbd>Alt</kbd> + <kbd>F</kbd> | 📁 Projektordner öffnen |
| <kbd>Alt</kbd> + <kbd>V</kbd> | ▶️ Video öffnen |
| <kbd>Leertaste</kbd> | 🎤 Teleprompter starten / pausieren |
| <kbd>Esc</kbd> | ✖️ Teleprompter schließen |

---

## ❓ Häufige Fragen

<details>
<summary><b>Brauche ich Internet?</b></summary>

Nein. 🔌 Nur die Schriftart wird online geladen — bist du offline, nutzt die App einfach
die Systemschrift und funktioniert ganz normal weiter.
</details>

<details>
<summary><b>Muss ich etwas installieren?</b></summary>

Nein. Es gibt keine Installation, kein Setup, keine Updates. Eine Datei, ein Browser,
fertig. 🎉
</details>

<details>
<summary><b>Sieht irgendjemand meine Daten?</b></summary>

Nein. Nichts verlässt deinen Rechner. Es gibt keinen Server, der sie empfangen könnte. 🔒
</details>

<details>
<summary><b>Kann ich mehrere Kanäle verwalten?</b></summary>

Pro Browser ist ein Profil aktiv. Mit *Switch profile* wechselst du — **exportiere aber
vorher**, denn das gespeicherte Profil wird dabei ersetzt. ⚠️
</details>

<details>
<summary><b>Warum wird nichts mehr gespeichert?</b></summary>

Steht in der Leiste oben *„Not saved — storage full"*, ist der Browserspeicher voll
(meist nach 8–15 Thumbnails). Exportiere deine Daten und lösche alte Projekte. 🧹
</details>

<details>
<summary><b>Wie schreibe ich mein Script?</b></summary>

Ganz normal drauflos — oder mit Markdown für Überschriften (`#`), **fett** (`**Text**`)
und Listen (`-`). Zeilen wie `[COLD OPEN]` oder `SPONSOR:` werden automatisch blau
hervorgehoben, damit du sie im Teleprompter sofort siehst. 🔵
</details>

---

## 🧠 Für Fortgeschrittene

Du willst wissen, wie das intern funktioniert — Speicherformat, ZIP-Aufbau,
Markdown-Syntax im Detail, Sicherheit und Performance?

👉 **[ADVANCED.md](ADVANCED.md)**

---

## 🌐 Getestete Browser

Chrome, Safari und Firefox in aktuellen Versionen auf macOS. ✅

---

© Arthur Pletzer 2026
