[English](guide-en.md) · [Русский](guide-ru.md) · **Deutsch** · [简体中文](guide-zh-Hans.md)

# GridSight – Benutzerhandbuch

> Dieses Handbuch beschreibt **GridSight 1.0.0-beta.2**. Mit *(beta.2+)* markierte Funktionen gibt es in 1.0.0-beta.1 nicht.

So installieren, konfigurieren und nutzen Sie GridSight – ein kostenloses Hilfsprogramm für EVE-Online-Multiboxer unter Windows. Die Namen von Schaltflächen und Menüpunkten sind unten wörtlich so angegeben, wie sie in der deutschen Oberfläche von GridSight erscheinen.

GridSight sendet keine Eingaben an das Spiel, liest keinen Client-Speicher und verändert keine Spieldateien. Es liest die Logs, die EVE auf die Festplatte schreibt, nutzt die offizielle ESI-API und einige öffentliche Dienste der EVE-Community und zeigt die Informationen auf Ihrem Bildschirm an. Das Einzige, was es in Ihrem EVE-Account ändern kann, sind gespeicherte Fittings – und nur, wenn Sie den Export über die Kommandozeile ausdrücklich ausführen (Abschnitt 14).

## Inhalt

1. [Voraussetzungen](#1-voraussetzungen)
2. [Installation Schritt für Schritt](#2-installation-schritt-für-schritt)
3. [Datenschutz und Sicherheit](#3-datenschutz-und-sicherheit)
4. [Tray-Symbol und Einstellungsfenster](#4-tray-symbol-und-einstellungsfenster)
5. [Miniaturen](#5-miniaturen)
6. [EVE-Logordner und Client-Sprache](#6-eve-logordner-und-client-sprache)
7. [Alarme](#7-alarme)
8. [Intel](#8-intel)
9. [D-Scan, Lokal und Schätzung](#9-d-scan-lokal-und-schätzung)
10. [Schadensmonitor und Bergbau](#10-schadensmonitor-und-bergbau)
11. [Ping und FPS](#11-ping-und-fps)
12. [EVE-Login (ESI)](#12-eve-login-esi)
13. [Übersicht (Dashboard)](#13-übersicht-dashboard)
14. [GridSight.Snapshot für Fortgeschrittene (Kommandozeile)](#14-gridsightsnapshot-für-fortgeschrittene-kommandozeile)
15. [Sprache, Updates, Autostart](#15-sprache-updates-autostart)
16. [Problemlösung (FAQ)](#16-problemlösung-faq)
17. [Unterstützung und Feedback](#17-unterstützung-und-feedback)

---

## 1. Voraussetzungen

- **Windows 10 oder 11, 64 Bit (x64).** .NET oder andere Komponenten müssen nicht installiert werden – GridSight ist eine einzige Datei `GridSight.exe`, die Laufzeitumgebung ist enthalten.
- **EVE im Modus „Fenster“ oder „Randloses Fenster“.** Im exklusiven **Vollbildmodus** übernimmt das Spiel den Bildschirm: GridSight-Fenster (Miniaturen, Schadens-Overlay, Ping/FPS-Overlay) können nicht darüber gezeichnet werden. Verwenden Sie „Fenster“ oder „Randloses Fenster“.
- **Arbeitsspeicher:** ca. 115–150 MB RAM bei fünf laufenden Clients (Fenster „Übersicht“ geschlossen); die CPU-Last liegt in der Regel deutlich unter 1 %.
- **Das Fenster „Übersicht“** *(beta.2+)* verwendet die Microsoft-Edge-Komponente **WebView2 Runtime**. Windows 11 bringt sie mit; unter Windows 10 muss sie manchmal nachinstalliert werden – die „Übersicht“ zeigt dann „WebView2 Runtime herunterladen“, und solange können Sie „Im Browser öffnen“ nutzen.
- **Internet** wird nur für optionale Funktionen benötigt: ESI-Login und „Übersicht“, Intel-Karte und Schiffsklassen (einmaliger Download der statischen Daten von CCP, ca. 95 MB), Marktpreise und Schätzung, zKillboard und Update-Prüfung. Miniaturen und Alarme funktionieren offline.

## 2. Installation Schritt für Schritt

> [!WARNING]
> **GridSight ist nicht mit einem Code-Signing-Zertifikat signiert.**
> Ein solches Zertifikat kostet etwa 200–400 $ pro Jahr – für ein unabhängiges kostenloses Projekt ist das derzeit nicht bezahlbar. Deshalb kann Windows nicht bestätigen, wer die Datei erstellt hat, und SmartScreen zeigt beim ersten Start ein blaues Fenster:
>
> **„Der Computer wurde durch Windows geschützt“**
>
> Windows zeigt es bei neuen Dateien ohne digitale Signatur und ohne Download-Verlauf. Es bedeutet nicht, dass Schadsoftware gefunden wurde. Wenn Sie die Datei von der offiziellen Releases-Seite haben und der SHA-256 übereinstimmt (Schritt 1), klicken Sie auf **Weitere Informationen** und dann auf **Trotzdem ausführen**.
>
> Wenn Sie `GridSight.exe` aus einer anderen Quelle haben – nicht ausführen. Wird Ihr PC von einer Organisation verwaltet oder blockieren Windows oder Ihr Virenscanner die Datei ohne die Option „Trotzdem ausführen“, versuchen Sie nicht, das zu umgehen.

### Schritt 1. Datei herunterladen und prüfen

1. Öffnen Sie die Releases-Seite **https://github.com/evelens-app/evelens/releases** und laden Sie `GridSight.exe` aus dem neuesten Release herunter. Laden Sie GridSight nicht von anderen Websites, Foren, Discord oder Filehostern – auch nicht, wenn der Name gleich ist.
2. Der Browser meldet eventuell, dass die Datei „nicht häufig heruntergeladen“ wird. Bei einem neuen Programm ist das normal: Öffnen Sie das Download-Menü („…“) und wählen Sie **Beibehalten**.
3. **SHA-256 vor dem ersten Start prüfen.** Öffnen Sie **PowerShell** im Ordner mit der Datei und führen Sie aus:
   ```powershell
   Get-FileHash .\GridSight.exe -Algorithm SHA256
   ```
   Der Wert `Hash` muss exakt mit dem SHA-256 in der Release-Beschreibung der heruntergeladenen Version übereinstimmen (Groß-/Kleinschreibung egal). Wenn nicht – Datei löschen und erneut von der Releases-Seite herunterladen. Stimmt er immer noch nicht, nicht ausführen und vertraulich melden (siehe [SECURITY.md](../SECURITY.md)).
4. Ein übereinstimmender Hash beweist, dass die Datei Byte für Byte die vom Autor veröffentlichte ist. Er beweist für sich allein nicht, dass die Datei sicher ist – was GridSight tut und wo seine Grenzen liegen, steht in [SECURITY.md](../SECURITY.md). Schritt-für-Schritt-Anleitung mit weiteren Prüfungen: [DOWNLOAD_VERIFICATION.md](../DOWNLOAD_VERIFICATION.md) (auf Englisch).

### Schritt 2. GridSight.exe in einen eigenen Ordner legen

GridSight muss nicht installiert werden – es läuft aus dem Ordner, in dem die Datei liegt. Wählen Sie einen dauerhaften Ort, zum Beispiel:

```
%LOCALAPPDATA%\Programs\GridSight\
```

(in die Adressleiste des Explorers einfügen, den Ordner `GridSight` anlegen und `GridSight.exe` dorthin verschieben) oder einen beliebigen eigenen Ordner.

- **Nicht** im Ordner „Downloads“ lassen – dort wird die Datei leicht versehentlich gelöscht.
- **Nicht** in den Spielordner von EVE legen.
- GridSight schreibt nichts neben die exe. Einstellungen, Anordnung, Logs und weitere Daten liegen in `%APPDATA%\GridSight\`, Berichte der „Übersicht“ in `%USERPROFILE%\eve-snapshot\` (vollständige Liste: [PRIVACY.md](../PRIVACY.md)).
- Wenn Sie den Autostart einschalten, merkt sich GridSight den Pfad der exe. Verschieben Sie die Datei später, schalten Sie „GridSight mit Windows starten“ aus und wieder ein.

### Schritt 3. Markierung „aus dem Internet heruntergeladen“ entfernen

1. Rechtsklick auf `GridSight.exe` → **Eigenschaften**.
2. Auf der Registerkarte **Allgemein** unten das Kästchen **Zulassen** anhaken (fehlt das Kästchen, ist die Datei bereits freigegeben).
3. **OK** klicken.

### Schritt 4. Erster Start und SmartScreen

Doppelklicken Sie auf `GridSight.exe`. Erscheint das Fenster **„Der Computer wurde durch Windows geschützt“** und der Hash stimmt, klicken Sie auf **Weitere Informationen** → **Trotzdem ausführen** (siehe Warnung am Anfang dieses Abschnitts). Normalerweise fragt Windows nur einmal pro Dateiversion.

*(beta.2+)* Beim allerersten Start zeigt GridSight ein kurzes Begrüßungsfenster. Nachdem Sie es geschlossen haben, läuft GridSight im Tray weiter.

### Schritt 5. Wenn der Virenscanner Alarm schlägt

Manche Virenscanner sind misstrauisch gegenüber neuen unsignierten Dateien und gegenüber Funktionen, die GridSight tatsächlich nutzt (eine Single-File-exe, die ihre Laufzeitumgebung nach `%TEMP%` entpackt, optionaler Autostart, Windows-Leistungstracing für FPS, globale Hotkeys). Was tun:

- **Schalten Sie den Virenschutz nicht aus.**
- Prüfen Sie zuerst den SHA-256 (Schritt 1). Eine Datei mit anderem Hash ist ein echtes Problem – löschen Sie sie.
- Stimmt der Hash, können Sie die Datei über das offizielle Formular des Herstellers als möglichen Fehlalarm einreichen und uns in den [Issues](https://github.com/evelens-app/evelens/issues) Bescheid geben – welcher Virenscanner und was er gemeldet hat.
- Sind Sie sicher, dass es ein Fehlalarm ist, können Sie eine Ausnahme **nur für diese eine Datei** hinzufügen. Im Microsoft Defender: **Windows-Sicherheit** → **Viren- & Bedrohungsschutz** → unter „Einstellungen für Viren- & Bedrohungsschutz“ auf **Einstellungen verwalten** → **Ausschlüsse** → **Ausschlüsse hinzufügen oder entfernen** → **Ausschluss hinzufügen** → **Datei** → `GridSight.exe` wählen.
- Im Zweifel nicht starten.

### Schritt 6. Einstellungen im EVE-Client prüfen

1. **Fenstermodus:** In den Anzeigeeinstellungen von EVE **„Fenster“** oder **„Randloses Fenster“** wählen (nicht Vollbild).
2. **Chat-Protokollierung:** Lokal-Alarme und Intel lesen die Chat-Logs, daher muss EVE den Chat in Dateien schreiben. Suchen Sie in den EVE-Einstellungen (Esc-Menü) die Chat-Option zum Speichern des Chats in eine Datei (im englischen Client **„Log Chat to File“**) und stellen Sie sicher, dass sie aktiviert ist. Ohne sie funktionieren Lokal und Intel nicht (Miniaturen und Kampfalarme schon).
3. **Spiel-Logs (Gamelogs)** – Kampf, Warpstörung, Frachtraum, Bergbau – schreibt EVE automatisch. Hier muss nichts eingeschaltet werden.
4. **Logordner:** Standardmäßig schreibt EVE die Logs nach `Dokumente\EVE\logs` (Unterordner `Gamelogs` und `Chatlogs`). Ist der Ordner „Dokumente“ nach OneDrive verschoben, sieht der Pfad so aus: `…\OneDrive\Dokumente\EVE\logs`. GridSight findet ihn in beiden Fällen selbst (siehe [Abschnitt 6](#6-eve-logordner-und-client-sprache)).

### Schritt 7. Was Sie nach dem Start sehen

- Das GridSight-Symbol erscheint im Infobereich der Taskleiste unten rechts neben der Uhr. Windows versteckt neue Symbole oft hinter dem Pfeil **^**. Damit es immer sichtbar ist, ziehen Sie das Symbol aus dem **^**-Bereich auf die Taskleiste oder schalten Sie GridSight unter **Einstellungen → Personalisierung → Taskleiste** im Bereich der weiteren Taskleistensymbole (Windows 11) ein.
- **Doppelklick** auf das Symbol öffnet die Einstellungen. **Rechtsklick** öffnet das Menü.
- Sobald EVE-Clients laufen, erscheint für jeden eine Miniatur. Solange ein Client in der Charakterauswahl ist, steht auf der Miniatur „Login…“.
- Zeigt das Tray-Menü „⚠ EVE-Logordner nicht gefunden“, wurde EVE auf diesem PC noch nicht gestartet oder die Logs liegen woanders – siehe [Abschnitt 6](#6-eve-logordner-und-client-sprache).

### Schritt 8. Was Sie abschalten können, wenn Sie es nicht brauchen

Alle Einstellungen werden sofort übernommen und gespeichert – eine Schaltfläche „Speichern“ gibt es nicht.

| Funktion | Standard | Wo abschalten |
|---|---|---|
| Ping und FPS | aus | Tray: „Ping/FPS: Miniaturen“, „Ping/FPS: Hauptfenster“; oder Einstellungen → „Allgemein“ → „Ping und FPS“ |
| Schadensmonitor | aus | Tray: „Schadensmonitor“; Einstellungen → „Schaden“ |
| Intel | aus | Einstellungen → „Alarme“ → „Intel-Kanäle überwachen“ |
| Einzelne Alarmarten | an | Einstellungen → „Alarme“ (für alle) oder „Charaktere“ (für einen) |
| Alle Alarme vorübergehend | – | Tray: „Alarme pausieren“ |
| Update-Prüfung | an | Einstellungen → „Allgemein“ → „Nach Updates suchen (täglich, GitHub)“ |
| Autostart | aus | Einstellungen → „Allgemein“ → „GridSight mit Windows starten“ |
| Account-Timer | an (wirken erst, wenn ein Charakter in der „Übersicht“ verbunden ist) | Einstellungen → „Allgemein“ → „Account-Timer überwachen“ |
| Hintergrund-Sync der Handelshistorie *(beta.2+)* | an (zusammen mit den Account-Timern) | Einstellungen → „Allgemein“ → „Account-Timer“ – eigener Schalter (Abschnitt 13) |

### Schritt 9. Aktualisieren

1. Neue `GridSight.exe` von der Releases-Seite herunterladen und den SHA-256 prüfen (Schritt 1).
2. GridSight schließen: Rechtsklick auf das Tray-Symbol → **Beenden**.
3. Alte `GridSight.exe` im selben Ordner durch die neue ersetzen; freigeben (Schritt 3).
4. Starten. Einstellungen, Positionen der Miniaturen, verbundene Charaktere und die Handelshistorie bleiben erhalten – sie liegen in `%APPDATA%\GridSight\`.

### Schritt 10. Deinstallieren

1. Ist der Autostart aktiv, zuerst „GridSight mit Windows starten“ abwählen – oder später im Registrierungs-Editor den Wert `GridSight` unter `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run` löschen.
2. Optional: Charaktere trennen – „ESI trennen“ im Tab „Charaktere“ und die Schaltfläche zum Trennen im Fenster „Übersicht“ *(beta.2+)* (Abschnitte 12–13).
3. Tray-Symbol → **Beenden**.
4. `GridSight.exe` löschen (und `GridSight.Snapshot.exe`, falls verwendet).
5. Ordner `%APPDATA%\GridSight` löschen: Einstellungen, Anordnung, Login-Tokens (`tokens.bin`, `snapshot-tokens.bin`), Handelshistorie (`history.db`), WebView2-Profil der „Übersicht“ (`webview2\`), Logs und Caches.
6. `%USERPROFILE%\eve-snapshot` löschen – Berichte der „Übersicht“ und ESI-Rohdaten (Wallet, Assets, Standort u. a., **unverschlüsselt**).
7. Haben Sie früher EveLens (den alten Namen) verwendet, auch `%APPDATA%\EveLens` löschen – dort können noch alte Kopien der Login-Tokens liegen.
8. Optional: `%TEMP%\GridSight-logs` löschen (Ausweich-Logordner).
9. Haben Sie FPS-Rechte erteilt (Abschnitt 11), entfernen Sie sich wieder aus der Gruppe: **Eingabeaufforderung als Administrator** öffnen und `net localgroup "Leistungsprotokollbenutzer" %USERNAME% /delete` ausführen (in einem englischen Windows heißt die Gruppe `"Performance Log Users"`; den genauen Befehl zeigt GridSight unter der Schaltfläche „FPS-Rechte erteilen (UAC)…“). Danach bei Windows ab- und wieder anmelden.
10. Haben Sie Charaktere per ESI verbunden, widerrufen Sie den Zugriff auf der CCP-Seite: https://community.eveonline.com/support/third-party-applications/. Das Löschen lokaler Dateien allein widerruft den Zugriff nicht.

Dieselbe Liste mit Erläuterungen steht in [PRIVACY.md](../PRIVACY.md), Abschnitt 8.

## 3. Datenschutz und Sicherheit

**Keine GridSight-Server, keine Telemetrie, keine Analyse.** GridSight hat keine eigenen Server und Benutzerkonten, und es werden keinerlei Daten an den Autor gesendet. Spiel- und Chat-Logs von EVE werden nur auf Ihrem Computer gelesen und nirgendwohin hochgeladen.

**Was GridSight auf Ihrem PC liest:** die Logdateien, die EVE schreibt (nur lesend; nur Spiel-Logs, Lokal und die Intel-Kanäle, die Sie selbst wählen), die Zwischenablage nur, wenn Sie das Analysefenster öffnen, und Windows-Leistungsdaten (ETW) für Ping/FPS nur, wenn Sie das einschalten. Es liest nie den Spielspeicher und sendet nie Eingaben an das Spiel.

**Netzwerk.** GridSight verbindet sich mit offiziellen EVE-Diensten (SSO-Login, ESI-API, Bildserver, statische Daten), mit zKillboard, mit den Marktpreisen von Fuzzwork und mit der GitHub-API für die Update-Prüfung. Ohne Ihr Zutun kann es: einmal täglich bei GitHub nach Updates fragen (wenn aktiviert), die ESI-Anzeige verbundener Charaktere etwa alle 30 s aktualisieren, alle 10 Minuten die Account-Timer prüfen und etwa stündlich die Handelshistorie synchronisieren *(beta.2+)*, höchstens einmal pro Woche statische EVE-Daten herunterladen. Alles andere geschieht nur, wenn Sie die Funktion nutzen. Die vollständige Liste – was wohin, wann gesendet wird und wie man es abschaltet – steht in [NETWORK_CONNECTIONS.md](../NETWORK_CONNECTIONS.md) (auf Englisch).

**Was auf Ihrem PC gespeichert wird:** Einstellungen, verschlüsselte Login-Tokens, Ihre Handelshistorie *(beta.2+)*, Caches öffentlicher Daten, Logs und Berichte der „Übersicht“ in `%USERPROFILE%\eve-snapshot`. Die Berichte und die Handelshistorie sind **nicht verschlüsselt** – geben Sie diese Dateien und Screenshots der „Übersicht“ nur weiter, wenn Sie diese Informationen zeigen möchten. Details und wie Sie alles löschen: [PRIVACY.md](../PRIVACY.md).

**Login-Tokens** werden nur auf diesem PC gespeichert, mit Windows DPAPI für Ihr Windows-Konto verschlüsselt – ein anderer Windows-Benutzer kann sie nicht entschlüsseln (Programme unter Ihrem eigenen Konto schon). Sie werden nur an die Server von CCP gesendet: an `login.eveonline.com`, um den Zugriff zu verlängern, und an `esi.evetech.net` mit jeder autorisierten Anfrage – nie an den Autor oder Dritte. Ihr EVE-Passwort sieht GridSight nie: Sie melden sich auf der offiziellen EVE-Website an. Welche Berechtigungen angefragt werden und warum: [ESI_PERMISSIONS.md](../ESI_PERMISSIONS.md).

**Regeln von CCP.** GridSight nutzt eine eigene Anwendungsregistrierung im EVE-Entwicklerportal und ist so gestaltet, dass es unserer Auslegung der [CCP-Entwicklerlizenz](https://developers.eveonline.com/license-agreement) und der EULA entspricht. Es wurde von CCP oder Fenris Creations **weder geprüft noch genehmigt**; eine Registrierung im Entwicklerportal ist keine Billigung. EVE Online wird vom Studio Fenris Creations entwickelt (bis Mai 2026 hieß es CCP Games); die Lizenz erteilt CCP hf. GridSight ist nicht mit Fenris Creations / CCP verbunden.

**Grenzen.** Die exe ist nicht signiert, der Quellcode ist geschlossen, und ein unabhängiges Audit gab es noch nicht. Was GridSight mit EVE und Windows tut, seine Grenzen und wie Sie ein Sicherheitsproblem vertraulich melden: [SECURITY.md](../SECURITY.md).

**Zugriff widerrufen:** jederzeit auf der Seite für Drittanbieter-Anwendungen: https://community.eveonline.com/support/third-party-applications/

## 4. Tray-Symbol und Einstellungsfenster

**Einstellungen öffnen:** Doppelklick auf das Tray-Symbol oder Rechtsklick → „Einstellungen…“.

**Tray-Menü** (Rechtsklick), von oben nach unten:

- „Version X verfügbar…“ – nur wenn eine neue Version erschienen ist; öffnet die Release-Seite.
- „Timer“ – Account-Timer (Abschnitt 13), sichtbar, wenn die Timer aktiv sind.
- „Übersicht“ *(beta.2+)* – das Fenster „Übersicht“ (Abschnitt 13).
- „Zwischenablage analysieren (D-Scan / Lokal / Schätzung)“ – Abschnitt 9.
- „Bergbau“ – Abschnitt 10.
- „Schadensmonitor“ – schaltet das Schadens-Overlay ein und aus.
- „Bearbeitungsmodus“ – Miniaturen verschieben und in der Größe ändern.
- „Einstellungen…“
- „ESI neu verbinden…“ – erscheint nur, wenn der ESI-Zugriff eines Charakters abgelaufen ist oder widerrufen wurde.
- „Ping/FPS: Miniaturen“, „Ping/FPS: Hauptfenster“ – Abschnitt 11.
- „Alarme pausieren“ – neue Alarme vorübergehend nicht anzeigen.
- „Язык / Language“ – Sprache der Oberfläche.
- „Anleitung“ – öffnet dieses Handbuch.
- „Über GridSight“ – Version, Links, Update-Prüfung, Unterstützung.
- „Beenden“

**Tabs der Einstellungen:**

| Tab | Inhalt |
|---|---|
| „Charaktere“ | Alle Charaktere, die GridSight gesehen hat: im Spiel oder nicht, Gruppe, Alarme pro Charakter, Schaltfläche „ESI verbinden“. |
| „Gruppen & Hotkeys“ | Gruppen von Charakteren und Hotkeys zum Umschalten zwischen ihnen. |
| „Alarme“ | Welche Alarme aktiv sind, Schaltflächen „Testen“, Einstellungen für Lokal und Intel. |
| „Schaden“ | Schadensmonitor. |
| „Allgemein“ | Sprache, EVE-Logordner, Miniaturen, Hotkey für den Bearbeitungsmodus, Zwischenablage-Analyse, Bergbau, Hotkey der „Übersicht“, Kontakt für zKillboard, Ping und FPS, Start und Updates, Account-Timer, ESI Client ID. |

Unten im Fenster – der Link „Über / Unterstützen“.

## 5. Miniaturen

**Anordnung.** Jeder Charakter hat eine eigene Position und Größe der Miniatur; sie werden pro Charakter gespeichert, sodass die Miniatur nach einem Client-Neustart an ihren Platz zurückkehrt. Eine neue Miniatur ist 320 px breit. Miniaturen behalten das Seitenverhältnis des Client-Fensters (schwarze Ränder, wenn die Form abweicht).

**Bearbeitungsmodus** – Standard-Hotkey **`Strg+Alt+E`** (oder Tray → „Bearbeitungsmodus“):

- Miniatur ziehen, um sie zu verschieben; Miniaturen rasten aneinander ein;
- an der rechten unteren Ecke ziehen, um die Größe zu ändern (Mindestbreite 120 px);
- Position und Größe werden gespeichert, sobald Sie die Maus loslassen;
- erneutes `Strg+Alt+E` beendet den Modus.

Der Hotkey lässt sich unter „Allgemein“ → „Bearbeitungsmodus“ ändern.

**Umschalten.** Ein Klick auf eine Miniatur holt diesen Client in den Vordergrund. Ein minimierter Client zeigt „minimiert“ und wird per Klick wiederhergestellt.

**Darstellung** („Allgemein“ → „Miniaturen“):

- „Deckkraft“ – 30–100 %, gilt für das gesamte Miniaturfenster;
- „Miniatur des aktiven Clients ausblenden“ – diesen Client sehen Sie ohnehin;
- „Alle Miniaturen ausblenden, wenn EVE nicht im Vordergrund ist“ – Miniaturen verschwinden, solange Sie im Browser, in Discord usw. sind.

**Gruppen und Hotkeys** (Tab „Gruppen & Hotkeys“):

1. Auf „Hinzufügen“ klicken und im Feld „Gruppenname“ einen Namen vergeben (z. B. „Flotte“).
2. Unten einen Charakter wählen und auf „Zur Gruppe hinzufügen“ klicken. Für alle Charaktere wiederholen. Die Gruppe lässt sich auch im Tab „Charaktere“ wählen.
3. „Nächster Charakter“ und „Vorheriger Charakter“ festlegen: ins Feld klicken und eine Kombination drücken, z. B. `Strg+Alt+F1`. Ohne Strg/Alt/Umschalt/Win nur F1–F24; Umschalt allein reicht nicht; Alt+F4 ist nicht möglich. Rücktaste – löschen, Esc – abbrechen.
4. „Reihenfolge“ – von oben nach unten: Zeilen ziehen oder „Hoch“ / „Runter“ verwenden. Charaktere, deren Clients nicht laufen, werden übersprungen.

Ist eine Kombination bereits von einem anderen Programm oder einem anderen GridSight-Hotkey belegt, zeigt GridSight das rot an – wählen Sie eine andere.

## 6. EVE-Logordner und Client-Sprache

**Automatische Erkennung.** GridSight sucht die Logs in `Dokumente\EVE\logs` und berücksichtigt dabei den tatsächlichen Ort des Ordners „Dokumente“ – auch wenn Windows ihn nach OneDrive verschoben hat (`…\OneDrive\Dokumente\EVE\logs`). Existiert der Ordner noch nicht (EVE wurde noch nie gestartet), wartet GridSight und übernimmt ihn, sobald er erscheint.

**Prüfen:** „Allgemein“ → „EVE-Logordner“. Unter dem Pfad steht:

- „Gefunden: Gamelogs und Chatlogs werden gelesen.“ – alles in Ordnung;
- „Ordner Gamelogs nicht gefunden – Alarme funktionieren nicht. …“ – Ordner manuell angeben.

**Manuell angeben:** auf „Durchsuchen…“ klicken und den Ordner `logs` innerhalb von `EVE` wählen (den mit `Gamelogs` und `Chatlogs`) oder den Pfad ins Feld einfügen.

**EVE-Client-Sprache für die Log-Auswertung.** Alarme, Schaden, Bergbau und Lokal werden am Text der Spiel-Logzeilen erkannt, deshalb muss GridSight die Sprache des Clients kennen. Sie ist unabhängig von der Sprache der GridSight-Oberfläche. „Allgemein“ → „Sprache“ → „EVE-Client-Sprache (Logs)“:

- „Auto (aus Logzeilen)“ – Standard, erkennt russische und englische Clients an den Zeilen selbst;
- „RU — russischer Client“ / „EN — englischer Client“ – nur die Muster dieser Sprache.

> [!NOTE]
> Alarme, Schadensmonitor und Bergbau sind derzeit auf den **russischen** EVE-Client abgestimmt und daran geprüft. Die Unterstützung des **englischen** Clients ist im Test – wenn auf dem englischen Client etwas nicht auslöst, melden Sie es bitte in den Issues. Andere Client-Sprachen (Deutsch, Chinesisch usw.) werden noch nicht ausgewertet: Miniaturen, Umschalten, D-Scan-/Lokal-Analyse und ESI funktionieren, Alarme aus den Logs jedoch nicht.

## 7. Alarme

Alarme sind **nur ein farbiger Rahmen um die Miniatur – ohne Ton**. Der Rahmen blinkt 5 Sekunden und leuchtet dann, bis Sie zu diesem Client wechseln. Der aktive Client (im Vordergrund) bekommt nie Alarme – Sie sehen ihn ja schon.

| Farbe | Alarm | Wann |
|---|---|---|
| Orange | „Warpstörer/-unterbrecher (Sie werden festgehalten)“ | Sie werden per Warpstörer oder Warpunterbrecher festgehalten |
| Rot | „Angriff (Ihr Schiff nimmt Schaden)“ | Ihr Schiff nimmt Schaden |
| Violett | „Intel (System in der Nähe im Intel-Kanal)“ | Siehe Abschnitt 8 |
| Gelb | „Schiff (Frachtraum voll)“ | Frachtraum voll (auch anhand der Füllstandsschätzung beim Bergbau, Abschnitt 10) |
| Hellblau | „Lokal (Nachrichten im Systemchat)“ | Nachricht in Lokal, Systemwechsel oder Nachricht eines beobachteten Namens |

Leuchten mehrere Alarme, wird der wichtigste angezeigt (Reihenfolge wie in der Tabelle), die übrigen als kleine farbige Punkte.

**Einstellungen (Tab „Alarme“):**

- Häkchen schalten eine Alarmart für alle Charaktere ein oder aus; für einzelne Charaktere – im Tab „Charaktere“;
- **„Testen“** neben jeder Art lässt alle offenen Miniaturen in dieser Farbe aufleuchten – so sehen Sie schnell, wie es aussieht;
- „Wann Lokal auslöst“: „Jede Nachricht in Lokal“, „Systemwechsel“ und die Liste „Namen, bei deren Nachrichten immer alarmiert wird (einer pro Zeile)“.

EVE protokolliert nicht, wer Lokal betritt – ein Alarm „Neutraler im System“ ist daher nicht möglich. Das Einloggen eines Charakters und Nachrichten Ihrer eigenen Charaktere lösen keinen Lokal-Alarm aus.

**Pause:** Tray → „Alarme pausieren“ – neue Ereignisse lassen keine Rahmen aufleuchten, bis Sie das Häkchen entfernen.

## 8. Intel

GridSight kann Ihre Intel-Kanäle lesen und den Charakter hervorheben, in dessen Nähe ein System genannt wurde.

1. Stellen Sie sicher, dass die Chat-Protokollierung in EVE aktiv ist (Abschnitt 2, Schritt 6).
2. „Alarme“ → „Intel“ → **„Intel-Kanäle überwachen“** anhaken.
3. Im Feld „Kanäle“ die Kanalnamen eintragen, einen pro Zeile, so wie sie am Anfang des Chatlog-Dateinamens stehen (Dateien der Form `<Kanal>_JJJJMMTT_HHMMSS_….txt` im Ordner `Chatlogs`). Groß-/Kleinschreibung egal.
4. „Radius:“ festlegen – 1 bis 15 Sprünge (Standard 5).

Beim ersten Einschalten lädt GridSight die statischen Daten von CCP herunter (ca. 95 MB), um die Gate-Karte aufzubauen; der Status steht unter dem Schieberegler („Karte geladen: … Systeme mit Gates.“).

**So funktioniert es:** Nennt jemand im Kanal ein System, das nicht weiter als der Radius vom aktuellen System eines Charakters entfernt ist (über Gates gezählt), leuchtet dessen Miniatur violett, und im Balken steht `Intel: <System> · <N> Spr.` (das nächstgelegene). Das System des Charakters stammt aus Lokal oder ESI; solange es unbekannt ist, wird Intel für ihn nicht ausgewertet.

**Aufheben:** Eine Nachricht mit **`clr`** oder **`clear`** (auch das russische `чисто`) hebt den Alarm für die in derselben Nachricht genannten Systeme auf, z. B. `Perimeter clr`. Auch der Wechsel zum Client hebt ihn auf.

Einschränkungen: Abkürzungen und Zusätze („1DQ“, „Urlen-Gate“) werden nicht erkannt; Systeme, deren Namen gewöhnliche Wörter sind (`Bar`, `Exit`, `Pain`, `Dead End` …), werden nur in der Schreibweise mit Großbuchstaben wie im Spiel erkannt. Systemnamen müssen in lateinischen Buchstaben geschrieben sein. Wurmlochsysteme werden ignoriert.

## 9. D-Scan, Lokal und Schätzung

GridSight liest Text aus der Zwischenablage nur, wenn Sie dieses Fenster öffnen – an das Spiel wird nichts gesendet.

**So kopieren Sie im Spiel:**

- **D-Scan:** Im Scannerfenster in die Ergebnisliste klicken, `Strg+A`, dann `Strg+C`.
- **Lokal:** Im Chatfenster die Teilnehmer markieren (ersten anklicken, Umschalt+Klick auf den letzten oder `Strg+A`), dann `Strg+C`.
- **Gegenstände zur Schätzung** *(beta.2+)*: Gegenstände in einem Inventarfenster markieren (Frachtraum, Hangar, Container), bei Bedarf `Strg+A`, dann `Strg+C`.

**Analyse öffnen:** Tray → „Zwischenablage analysieren (D-Scan / Lokal / Schätzung)“ oder eine eigene Tastenkombination: „Allgemein“ → „Zwischenablage-Analyse (D-Scan / Lokal / Schätzung)“ → „Analyse öffnen“ (standardmäßig nicht belegt). Das Fenster erkennt das Format selbst; die Schaltflächen „D-Scan“ / „Lokal“ / „Schätzung“ erzwingen einen Modus für den aktuellen Text. Nach neuem Kopieren auf „Neu einfügen“ klicken oder die Kombination erneut drücken.

**D-Scan-Ergebnis:** Anzahl der Schiffe und sonstigen Objekte; Schiffe nach Klassen und Typen; ein Block „Achtung“ mit gefährlichen Schiffen (Interdictors/HICs, mobile Bubbles, Kampfsonden, Interceptors, Recons, Bomber, Black Ops, Logistik, Capitals, Supers). „Nur auf dem Grid (≤ 10.000 km)“ blendet entfernte Objekte aus.

**Lokal-Ergebnis:** Piloten nach Allianzen und Corporations gruppiert, die größten oben (Namen werden über die öffentliche ESI-API aufgelöst – die eingefügten Namen werden an ESI gesendet). Corporations und Allianzen Ihrer verbundenen Charaktere sind grün als „eigene“ markiert. „zKill prüfen“ (nur per Klick) ruft Kills/Verluste für bis zu 20 fremde Piloten aus den größten Gruppen ab; ein Klick auf den Pilotennamen öffnet seine zKillboard-Seite.

**Schätzungsergebnis** *(beta.2+)*: „Summe Buy“, „Summe Sell“, „Volumen (verpackt)“ und die Zahl der Positionen, darunter eine Tabelle pro Gegenstand mit Buy- und Sell-Preis und einem Hinweis – „an Kaufaufträge verkaufen“ oder „Verkaufsauftrag einstellen“. Das Handelszentrum wählen Sie im Feld „Handelszentrum“ (Jita, Amarr, Dodixie, Rens, Hek). Die Preise sind Fuzzwork-Aggregate für die Station des Handelszentrums (5 % des Orderbuchs von der besten Seite), stündlich aktualisiert; um sie abzurufen, sendet GridSight das Handelszentrum und die Liste der Typ-IDs an Fuzzwork. Zeilen, die keinem Gegenstand zugeordnet werden konnten, stehen unter „Nicht erkannt“. „Zusammenfassung kopieren“ legt eine kurze Zusammenfassung (Handelszentrum, Summen, Volumen, Positionen) in die Zwischenablage. Die erste Schätzung lädt die statischen Daten von CCP (SDE) und kann einige Minuten dauern.

Tipp: Unter „Allgemein“ → „Kontakt für zKillboard“ können Sie optional einen Kontakt angeben (E-Mail, Ingame-Name oder Discord) – zKillboard bittet darum, dass sich Tools zu erkennen geben. Der Kontakt wird im Header der Anfrage an zKillboard gesendet; lassen Sie das Feld leer, wenn zKillboard ihn nicht sehen soll.

## 10. Schadensmonitor und Bergbau

### Schadensmonitor

Tab „Schaden“ (standardmäßig alles aus):

- **„Balken „⬆ 412 · ⬇ 95 DPS“ auf Miniaturen im Kampf“** – ausgehender (⬆) und eingehender (⬇) Schaden pro Sekunde;
- **„Overlay-Fenster über allem“** – ein kleines Fenster mit DPS, Spitze und Summe pro Kampf; auch über Tray → „Schadensmonitor“ schaltbar;
- **„DPS-Fenster:“** – gleitendes Berechnungsfenster, 3–60 s (Standard 10).

Das Overlay fängt weder Klicks noch Fokus ab. Zum Verschieben den Bearbeitungsmodus (`Strg+Alt+E`) einschalten und es ziehen. Angezeigt wird der aktive Charakter, wenn er im Kampf ist, sonst der zuletzt kämpfende. Ein Kampf endet nach 30 s ohne Schüsse. Reparatur, Neutralisierung, Nosferatu und EW zählen nicht als Schaden. Auf der Festplatte wird nichts gespeichert.

### Bergbau

Öffnen über Tray → „Bergbau“ (oder per Tastenkombination: „Allgemein“ → „Bergbau“ → „Fenster „Bergbau“ öffnen“, standardmäßig nicht belegt). Das Fenster liest die Abbauzeilen aus den Spiellogs aller Charaktere: Erz, Eis, Mondgestein, Gas.

- Pro Charakter: abgebaut nach Typen (Einheiten, m³, ISK), „ISK/Std. · 10 Min.“, „ISK/Std. · Sitzung“, „m³/Std. · 10 Min.“, „m³/Std. · Sitzung“, Verlust.
- Eine neue Sitzung beginnt nach einer Pause von mehr als N Minuten („Neue Sitzung nach Pause länger als“, Standard 10). Wird GridSight mitten im Abbau gestartet, übernimmt es die letzten 6 Stunden aus den Logs.
- ISK wird nach Kaufaufträgen in Jita 4-4 berechnet, ohne Steuern. „Komprimiert rechnen“ – Preise von komprimiertem Erz, wo vorhanden.

**Frachtraum:** EVE schreibt das Frachtraumvolumen nicht in die Logs – tragen Sie es in der Charakterkarte ein („Frachtraum, m³“). Dann sehen Sie den Füllstand und „voll in ≈ mm:ss“. Nach dem Entladen auf **„Entladen“** klicken – der Füllstand wird ab dieser Minute neu berechnet. „Miniatur hervorheben bei Frachtraum ≈ 95 %“ lässt anhand dieser Schätzung den gelben Alarm „Schiff“ aufleuchten (einmal pro Füllung, ohne Ton).

## 11. Ping und FPS

**Wo einschalten:** „Allgemein“ → „Ping und FPS“ (standardmäßig aus) oder im Tray:

- „Ping/FPS: Miniaturen“ / „Auf Miniaturen anzeigen“ – `62 fps · 38 ms` rechts im Balken jeder Miniatur (der Intel-Text hat Vorrang, solange er leuchtet);
- „Ping/FPS: Hauptfenster“ / „Über dem Hauptfenster anzeigen (EVE-Client im Fokus)“ – ein kleines Overlay in einer Ecke des aktiven EVE-Fensters; die Ecke unter „Ecke im Hauptfenster“ (Standard „Oben rechts“). Im exklusiven Vollbild nicht sichtbar.

Die Messwerte stammen aus dem Windows-Systemtracing (ETW – so arbeitet auch PresentMon). In den Client wird nichts eingeschleust, und standardmäßig verbindet sich GridSight nicht mit CCP-Servern.

**FPS-Rechte.** Für das Windows-Tracing muss GridSight entweder als Administrator laufen, oder Sie müssen Mitglied der Gruppe **„Leistungsprotokollbenutzer“** sein. Sonst zeigen die Miniaturen `FPS: keine Rechte`, und in den Einstellungen erscheint die Schaltfläche **„FPS-Rechte erteilen (UAC)…“**:

1. Auf „FPS-Rechte erteilen (UAC)…“ klicken und die UAC-Abfrage bestätigen. GridSight führt einen einzigen Befehl aus: `net localgroup "<Gruppe>" "<Sie>" /add`.
2. **Bei Windows ab- und wieder anmelden** (oder neu starten) – das Recht wirkt erst nach einer neuen Anmeldung.
3. GridSight starten und bei Bedarf „Erneut prüfen“ klicken. Der Status sollte „Tracing läuft: …“ lauten.

> [!IMPORTANT]
> Das ist ein Recht für Ihr **gesamtes Windows-Benutzerkonto**, nicht nur für GridSight: Jedes Programm, das unter Ihrem Konto läuft, kann dann Windows-Leistungstracing durchführen. Es bleibt bestehen, bis Sie es entfernen – Abschalten von „Ping und FPS“ oder Deinstallieren von GridSight entfernt es nicht. Zum Widerrufen: *(beta.2+)* die Schaltfläche zum Widerrufen der FPS-Rechte unter „Allgemein“ → „Ping und FPS“ verwenden (fragt erneut nach UAC) oder als Administrator den in den Einstellungen angezeigten Befehl `net localgroup "<Gruppe>" "<Sie>" /delete` ausführen. Danach neu anmelden.

**Ping:** GridSight liest passiv die geglättete Round-Trip-Zeit, die Windows selbst für die Verbindung des Clients zum EVE-Server (Port 26000) misst. `— ms` bedeutet: keine Verbindung (Login-Bildschirm, offline) oder der Client war länger als 60 s still.

**„Ping per Serververbindung (alle 30 s)“** – standardmäßig aus. Eine Ausweichlösung, wenn keine passive Messung möglich ist (keine Tracing-Rechte): GridSight öffnet eine leere TCP-Verbindung zum CCP-Server, misst den Handshake und schließt sie wieder. Es werden keine Daten übertragen, für den CCP-Server sind das aber zusätzliche Verbindungen – deshalb nur bei Bedarf einschalten.

## 12. EVE-Login (ESI)

Der ESI-Login ist optional: Miniaturen, Alarme, D-Scan-/Lokal-Analyse, Schaden, Bergbau und Ping/FPS brauchen ihn nie. Es gibt **zwei getrennte Logins** mit unterschiedlichen Berechtigungen; Sie können einen, beide oder keinen nutzen.

| Login | Wo | Berechtigungen | Wofür |
|---|---|---|---|
| **„ESI verbinden“** | Einstellungen → „Charaktere“ | 3 Lese-Scopes: aktueller Standort, Schiff und Online-Status | Anzeige „System · Schiff“ auf der Miniatur; aktuelles System für Intel |
| **„Charakter verbinden“** *(beta.2+)* | Fenster „Übersicht“ (Abschnitt 13) oder `GridSight.Snapshot login` (Abschnitt 14) | Lesezugriff auf Ihre Charakterdaten: Wallet, Assets, Skills, Industrie, Marktaufträge, Verträge, Planeten, Klone, Ansehen, Fittings u. a. | „Übersicht“, Berater, Account-Timer, Gewinn |

Die vollständige Liste der Berechtigungen, wofür jede genutzt wird und was ohne sie passiert: [ESI_PERMISSIONS.md](../ESI_PERMISSIONS.md) (auf Englisch). EVE SSO fragt alle Berechtigungen eines Logins auf einmal ab – einzelne lassen sich nicht auswählen. Wenn Sie der „Übersicht“ keinen breiten Lesezugriff geben möchten, nutzen Sie diesen Login einfach nicht; der Rest von GridSight funktioniert weiter. Alle Berechtigungen sind nur lesend, außer einer optionalen zum Anlegen gespeicherter Fittings, die nur über die Kommandozeile angefragt wird (`login --fits-write`, Abschnitt 14).

**So verbinden Sie einen Charakter für die Anzeige:**

1. Tab „Charaktere“ → **„ESI verbinden“** neben dem Charakter.
2. Der Browser öffnet die offizielle EVE-Anmeldeseite (login.eveonline.com). Melden Sie sich an, **wählen Sie denselben Charakter** und bestätigen Sie.
3. Der Browser leitet zurück zu GridSight, der Status wechselt zu „ESI verbunden“. Wurde im Browser ein anderer Charakter gewählt, verbindet GridSight diesen und weist darauf hin.

Die Anzeige wird etwa alle 30 s aktualisiert; „offline“, wenn der Charakter ausgeloggt ist.

GridSight verwendet seine eigene, integrierte ESI-Anwendung; das Feld „Client ID der EVE-Developers-App“ unter „Allgemein“ **kann leer bleiben**. Füllen Sie es nur aus, wenn Sie eine eigene Anwendung verwenden möchten.

**Sicherheit:** GridSight sieht Ihr Passwort nie – die Anmeldung läuft über EVE SSO; die Anmeldeseite leitet auf `http://localhost:8642/callback` auf Ihrem eigenen PC zurück, und GridSight lauscht dort nur während der Anmeldung. Tokens werden nur auf diesem PC gespeichert, mit Windows DPAPI unter Ihrem Windows-Konto verschlüsselt (`%APPDATA%\GridSight\tokens.bin` für die Anzeige, `snapshot-tokens.bin` für die „Übersicht“) und nur an die Server von CCP gesendet (siehe Abschnitt 3).

**Trennen und Zugriff widerrufen:**

- „ESI trennen“ neben dem Charakter löscht das Token der Anzeige von Ihrem PC.
- *(beta.2+)* Im Fenster „Übersicht“ gibt es eine Schaltfläche zum Trennen des gewählten Charakters: Sie löscht sein Token von Ihrem PC und widerruft es bei CCP. Über die Kommandozeile: `GridSight.Snapshot logout -c "<Charakter>"`.
- Um den Zugriff sicher zu widerrufen, nutzen Sie die CCP-Seite: https://community.eveonline.com/support/third-party-applications/ – damit werden die Tokens bei CCP ungültig, auch wenn Kopien auf Ihrer Festplatte bleiben.

Funktioniert der Zugriff nicht mehr, erscheint im Tray „ESI neu verbinden…“ und beim Charakter die Schaltfläche „Neu anmelden“.

## 13. Übersicht (Dashboard)

*(beta.2+)* Die **„Übersicht“** ist ein Fenster in GridSight mit den ESI-Daten Ihres Charakters und dem Berater. In 1.0.0-beta.1 brauchte man dafür das separate `GridSight.Snapshot.exe`; jetzt ist alles eingebaut.

**Öffnen:** Tray → „Übersicht“ oder eine eigene Tastenkombination: „Allgemein“ → „Übersicht“ → „Übersicht öffnen“ (standardmäßig nicht belegt). Ein Klick auf einen Eintrag unter Tray → „Timer“ öffnet ebenfalls die „Übersicht“.

**Erster Start:**

1. Klicken Sie auf **„Charakter verbinden“**. Der Browser öffnet die offizielle EVE-Anmeldeseite – anmelden, Charakter wählen und bestätigen (Berechtigungen: Abschnitt 12).
2. Klicken Sie auf **„Ersten Snapshot erstellen“**. Der erste Snapshot dauert einige Minuten: Statische Spieldaten und Marktpreise werden heruntergeladen.
3. Weitere Charaktere verbinden Sie genauso und wechseln zwischen ihnen in der Liste oben im Fenster.

**Schaltflächen oben:** „Aktualisieren“ – neuen Snapshot des gewählten Charakters erstellen; „Charakter verbinden“; „Im Browser öffnen“ – denselben Bericht im Standardbrowser öffnen; eine Schaltfläche zum Trennen des gewählten Charakters (Abschnitt 12). Daneben steht die Zeit des Snapshots.

**Inhalt:** Kennzahlen, „To-do“ (Zusammenfassung der Ratschläge aus allen Abschnitten), „Wallet“, „Assets“ mit ISK-Schätzung, „Skills“, „Markt“ (Aufträge und Verträge), „Handel“, „Industrie“, „Fertigung“, „PI“, „PI → P2“, „Bergbau“, „Wiederaufbereitung“, „Klone“, „LP & Ansehen“, „Abyssal-Fittings“, „Fittings“ und „Gewinn“. Der Berater:

- **Produktion** – Gewinn aus Ihren Blaupausen zu Jita-Preisen;
- **Wiederaufbereitung und Bergbau** – Roherz verkaufen, komprimieren oder wiederaufbereiten;
- **PI → P2** – Fabrik vs. Verkauf von P1;
- **Handel** – Verkauf von Assets, Stationshandel-Scanner und Überwachung Ihrer Aufträge für 5 Handelszentren;
- **Abyss-Fittings** – beliebte Fittings von zKillboard, abgeglichen mit Ihren Skills und Assets, mit Jita-Multibuy-Liste;
- **To-do** – Zusammenfassung der Ratschläge aus allen Abschnitten.

**Filter und Suche.** Tabellen mit Suchfeld haben zusätzlich Auswahlfilter pro Spalte, „Bereiche“ mit Von–bis-Werten (Beträge wie `300k` oder `1.5m` sind möglich), einen Zähler „N von M“ und „Filter zurücksetzen“. Filter, Sortierung und das gewählte Handelszentrum werden gespeichert. **`Strg+K`** oder **`/`** (oder die Schaltfläche „Suche“) öffnet eine Suche im gesamten Snapshot – Gegenstände, Skills, Orte: mindestens 2 Buchstaben eingeben, mit ↑↓ wählen, Enter springt zur Zeile, Esc schließt.

**Handelszentren.** Der Abschnitt „Handel“ wird für Jita, Amarr, Dodixie, Rens und Hek berechnet; das Handelszentrum wechseln Sie im Feld „Handelszentrum“. Die Maklergebühr berücksichtigt Ihr Ansehen. „To-do“ und die übrigen Abschnitte rechnen mit Jita.

**Marktbewegungen.** Jedes Handelszentrum hat unter „Handel“ eine Karte „Marktbewegungen“ mit drei Listen: „Im Aufwind“ und „Fallend“ (7-Tage-Mittel gegen 30-Tage-Mittel) und „Preissprünge“ (letzter Tag gegen den Monatsmedian). Das ist nicht der ganze Markt – nur Gegenstände, die der Snapshot bereits kennt (Scanner-Kandidaten und Ihre Stapel zum Verkauf).

**Gegenstandskarte.** Klicken Sie irgendwo in der „Übersicht“ auf einen Gegenstandsnamen. Die Karte lädt Live-Daten von ESI für 5 Handelszentren: bester Sell und Buy, Marge nach Steuer und Maklergebühr, Tagesvolumen, Anzahl der Aufträge und Sprünge von Ihrem aktuellen Standort. Ein Klick auf ein Handelszentrum zeigt den 90-Tage-Preisverlauf, den „Margenrechner“ und die Orderbücher der Station mit Markierung „Ihre Order“. Außerdem zeigt die Karte Signale aus dem Preisverlauf (steigend, fallend, Sprung, historisch günstig oder teuer, knappes Angebot …) und ein kurzes Fazit, z. B. „Kaufgelegenheit“, „Hub-Arbitrage“ oder „Wo verkaufen“ für Gegenstände, die Sie besitzen. Das sind Hinweise aus ESI-Verlauf und Aufträgen, keine Garantie – prüfen Sie das Orderbuch vor dem Handel.

**Gewinn.** Der Abschnitt „Gewinn“ berechnet den tatsächlichen Gewinn aus Ihren Geschäften: FIFO über alle verbundenen Charaktere, Verkaufssteuer aus dem Wallet-Journal, Maklergebühren im Zeitraum, Fertigungskosten aus den Materialien der Blaupausen; Zeiträume, ein Tagesdiagramm und die wichtigsten Gegenstände. „Ohne Einstand“ listet Verkäufe ohne Kauf in der Historie (Loot, Bergbau, LP, Verträge oder Käufe vor Beginn der Historie) – sie zählen nicht zum Gewinn. „Gekauft, noch nicht verkauft“ ist der Rest der FIFO-Warteschlange. ESI hält Transaktionen nur etwa 30 Tage vor, daher sammelt GridSight sie in einer lokalen Datenbank, `%APPDATA%\GridSight\history.db` – bei jedem Snapshot und im Hintergrund (siehe unten).

**Preisliste.** Im Fenster „Übersicht“ können Sie die Gewinnberechnung korrigieren: „Kosten festlegen“ für Gegenstände unter „Ohne Einstand“ (für eine Charge oder „für alle künftigen Verkäufe“) und „Eigenbedarf“ für Gegenstände, die Sie für sich gekauft haben – sie verlassen die FIFO-Warteschlange und zählen nicht als Verkauf. Einträge lassen sich ändern oder löschen; GridSight speichert sie in `history.db` und aktualisiert den Snapshot. Diese Schaltflächen funktionieren nur im Fenster „Übersicht“, nicht im Browser.

**Account-Timer im Tray.** Sobald ein Charakter in der „Übersicht“ verbunden ist, prüft GridSight alle 10 Minuten PI-Extraktoren, freie Fertigungsslots und die Skill-Warteschlange. Braucht etwas Aufmerksamkeit, erscheint ein Punkt am Tray-Symbol; die Liste steht unter Tray → „Timer“. Im selben Zyklus, etwa einmal pro Stunde und Charakter, synchronisiert GridSight außerdem Wallet-Transaktionen, Wallet-Journal und Industrie-Jobs in `history.db` für den Abschnitt „Gewinn“. „Allgemein“ → „Account-Timer überwachen“ schaltet die Timer ab; *(beta.2+)* ein eigener Schalter im selben Block schaltet den Hintergrund-Sync der Handelshistorie ab.

**Netzwerk und Dateien.** Die Seite der „Übersicht“ öffnet sich für sich genommen ohne Netzwerk. Wenn Sie eine Gegenstandskarte öffnen, fragt die Seite Live-Marktdaten bei der öffentlichen ESI und Symbole bei `images.evetech.net` ab; Login-Daten werden nicht gesendet, aber die Abfrage der Sprungzahl teilt CCP Ihr aktuelles Sonnensystem mit. Berichte werden in `%USERPROFILE%\eve-snapshot\` gespeichert: `latest-<Charakter>.html`, datierte Kopien `<Charakter>-<Datum>.html` und `.md` sowie rohe ESI-Antworten in `raw\`. Sie enthalten Wallet, Assets, Aufträge, Standort u. a. und sind **nicht verschlüsselt** – geben Sie sie nicht weiter. Details: [PRIVACY.md](../PRIVACY.md), [NETWORK_CONNECTIONS.md](../NETWORK_CONNECTIONS.md).

## 14. GridSight.Snapshot für Fortgeschrittene (Kommandozeile)

`GridSight.Snapshot.exe` ist ein separates Konsolenprogramm, das denselben Snapshot wie die „Übersicht“ erstellt und dieselben Berichte schreibt. Für die „Übersicht“ brauchen Sie es nicht; es ist für Skripte, eine andere Berichtssprache, den Export von Abyss-Fittings und die Feinabstimmung des Beraters. Es verwendet dieselben Tokens (`snapshot-tokens.bin`) wie die „Übersicht“.

**Befehle** (im Terminal im Ordner mit `GridSight.Snapshot.exe` ausführen; in PowerShell mit vorangestelltem `.\`):

| Befehl | Wirkung |
|---|---|
| `GridSight.Snapshot login` | EVE-Login im Browser (nur Lesezugriff, wie „Charakter verbinden“); einmal pro Charakter |
| `GridSight.Snapshot login --fits-write` | Ebenso, plus Recht zum Anlegen gespeicherter Fittings (nur für `--export-fits` nötig) |
| `GridSight.Snapshot logout -c "<Charakter>"` | *(beta.2+)* Token des Charakters von Ihrem PC löschen und bei CCP widerrufen |
| `GridSight.Snapshot` | Snapshot aller verbundenen Charaktere |
| `GridSight.Snapshot -c "<Charakter>"` | Snapshot eines Charakters |
| `GridSight.Snapshot -c "<Charakter>" --export-fits <Rumpf\|all> [--top N]` | Top-N (1–3) Abyss-Fittings des Rumpfes als `GridSight <Rumpf> #N` in die gespeicherten Fittings im Spiel schreiben |
| `GridSight.Snapshot --keep N` | *(beta.2+)* Nur die N neuesten datierten Kopien der Berichte behalten |
| `GridSight.Snapshot --lang de` | Sprache des Berichts: `de`, `en`, `ru`, `zh-Hans` (Standard – Sprache der GridSight-Oberfläche, sonst Windows) |
| `GridSight.Snapshot --help` | Vollständige Liste der Optionen (`--no-open`, `--no-market`, `--no-fits`, `--hubs` u. a.) |

**Schreiben in den Account.** `--export-fits` ist das Einzige in GridSight, das Ihren EVE-Account verändert: Es **legt** gespeicherte Fittings mit dem Namen `GridSight …` **an** und ändert oder löscht nie vorhandene. Es funktioniert nur nach `login --fits-write`.

**Wo die Dateien liegen:** `%USERPROFILE%\eve-snapshot\` – `latest-<Charakter>.html` (öffnet sich nach jedem Snapshot im Browser; `--no-open` verhindert das), datierte Kopien `<Charakter>-<Datum>.html` und `.md` sowie `raw\`. Die HTML-Datei öffnet sich ohne Netzwerk; die Gegenstandskarte lädt bei einem Klick Live-Daten von der öffentlichen ESI (Abschnitt 13).

## 15. Sprache, Updates, Autostart

**Sprache der Oberfläche:** „Allgemein“ → „Sprache“ → „Sprache der Oberfläche“: „Auto (Windows-Sprache)“, English, Русский, Deutsch, 简体中文 (auch Tray → „Язык / Language“). Wird sofort übernommen. Sie ist unabhängig von der EVE-Client-Sprache (Abschnitt 6). Namen von Gegenständen aus den CCP-Daten werden in allen Oberflächen außer der russischen auf Englisch angezeigt.

**Updates:** „Nach Updates suchen (täglich, GitHub)“ ist standardmäßig aktiv. Einmal täglich fragt GridSight bei GitHub nach einer neuen Version. Gibt es eine – Menüpunkt „Version X verfügbar…“ im Tray, eine Benachrichtigung und eine Zeile unter „Über“. **GridSight lädt und installiert nie selbst etwas** – aktualisieren Sie manuell (Abschnitt 2, Schritt 9). „Betaversionen anbieten“ – auch über Betas informieren. Manuell prüfen: „Über GridSight“ → „Nach Updates suchen“.

**Autostart:** „Allgemein“ → „Start“ → „GridSight mit Windows starten“. Trägt GridSight in den Autostart Ihres Benutzers ein (Registrierung `HKCU\…\Run`); Abwählen entfernt den Eintrag.

## 16. Problemlösung (FAQ)

**Keine Miniaturen.**
- Läuft EVE im Modus „Fenster“ oder „Randloses Fenster“ (nicht Vollbild)?
- Ist „Alle Miniaturen ausblenden, wenn EVE nicht im Vordergrund ist“ aktiv? Dann sind die Miniaturen verborgen, solange ein anderes Programm aktiv ist.
- Ist „Miniatur des aktiven Clients ausblenden“ aktiv? Bei nur einem Client ist seine Miniatur verborgen, solange er aktiv ist.
- Läuft GridSight überhaupt (Symbol im Tray, evtl. hinter **^**)?

**Miniatur am falschen Platz / außerhalb des Bildschirms.** Bearbeitungsmodus einschalten (`Strg+Alt+E`) und sie verschieben. Nach dem Abziehen eines Monitors wandern Miniaturen auf den Hauptbildschirm und kehren zurück, wenn der Monitor wieder angeschlossen ist. Eine Miniatur gehört zu einem Charakter: Solange er nicht gewählt ist, zeigt ein neuer Client „Login…“.

**FPS zeigt „FPS: keine Rechte“ oder „— fps“.**
- „FPS: keine Rechte“ – Rechte erteilen (Abschnitt 11), dann **bei Windows ab- und wieder anmelden**, dann „Erneut prüfen“.
- „Keine Tracing-Rechte, obwohl Sie in der Gruppe sind“ – „Erneut prüfen“ klicken oder neu starten.
- „— fps“ – für diesen Client gibt es noch keine Daten oder das Tracing ist fehlgeschlagen; prüfen Sie den Status unter „Ping und FPS“ in den Einstellungen. Ist dort von einer übrig gebliebenen Tracing-Sitzung die Rede, folgen Sie dem Hinweis (Befehl `logman stop … -ets` als Administrator) oder starten Sie neu.

**Ping zeigt „— ms“.** Der Client ist nicht mit dem Server verbunden (Login-Bildschirm, Charakterauswahl, offline) oder hat 60 s lang nichts gesendet. Ohne Tracing-Rechte gibt es keinen passiven Ping – Rechte erteilen oder „Ping per Serververbindung (alle 30 s)“ einschalten.

**Alarme lösen nicht aus.**
1. Unter „Allgemein“ → „EVE-Logordner“ muss „Gefunden: Gamelogs und Chatlogs werden gelesen.“ stehen.
2. „EVE-Client-Sprache (Logs)“ sollte „Auto“ oder Ihre Client-Sprache sein. Unterstützt werden nur russische und englische Clients; Englisch ist im Test. Ein deutscher Client wird noch nicht ausgewertet.
3. Der aktive Client bekommt nie Alarme – testen Sie mit einem Client im Hintergrund oder mit „Testen“ im Tab „Alarme“.
4. Prüfen Sie, dass die Alarmart unter „Alarme“ bzw. für diesen Charakter unter „Charaktere“ nicht abgeschaltet ist und im Tray nicht „Alarme pausieren“ angehakt ist.
5. Lokal und Intel brauchen die Chat-Protokollierung in EVE (Abschnitt 2, Schritt 6).

**Das Fenster „Übersicht“ ist leer oder meldet „WebView2 Runtime erforderlich“.** Installieren Sie die Komponente über „WebView2 Runtime herunterladen“ und nutzen Sie solange „Im Browser öffnen“.

**„Der Computer wurde durch Windows geschützt“.** Erwartet – GridSight ist nicht signiert. SHA-256 prüfen (Abschnitt 2, Schritt 1), dann **Weitere Informationen → Trotzdem ausführen**.

**GridSight startet nicht / zeigt einen Fehler.** Die Meldung nennt den Ort des Logs. Ist die Einstellungsdatei beschädigt, stellt GridSight die Einstellungen automatisch aus `settings.json.bak` wieder her.

**Wo liegt das GridSight-Log und was gehört in ein Issue.** Die Logs liegen in `%APPDATA%\GridSight\logs\` (eine Datei pro Tag, `gridsight-JJJJMMTT.log`; Ausweichordner – `%TEMP%\GridSight-logs`). Die Logs enthalten Charakternamen, aber keine Tokens. Bitte geben Sie in einem [Issue](https://github.com/evelens-app/evelens/issues) an:
- GridSight-Version („Über GridSight“);
- Windows-Version, Fenstermodus von EVE, Sprache des EVE-Clients, Anzahl der Clients und Monitore;
- was Sie getan haben, was Sie erwartet haben, was passiert ist (ein Screenshot hilft sehr – aber keine Screenshots der „Übersicht“ mit Wallet oder Assets veröffentlichen);
- die Logdatei des betreffenden Tages. Sehen Sie sie vor dem Senden durch – sie kann Namen Ihrer Charaktere enthalten; diese können Sie ersetzen.

Sicherheitsprobleme bitte vertraulich melden, nicht in den Issues: [SECURITY.md](../SECURITY.md).

## 17. Unterstützung und Feedback

GridSight ist kostenlos, und keine Funktion hängt von einer Spende ab. Wenn es Ihnen das Flottenleben erleichtert, können Sie sich mit einem beliebigen ISK-Betrag an den Charakter **Gridsin** im Spiel bedanken („Über GridSight“ → „Charakternamen kopieren“).

Vorschläge, Wünsche und Fehlermeldungen: [GitHub Issues](https://github.com/evelens-app/evelens/issues) oder per EVE-Mail an **Gridsin**.

GridSight ist ein unabhängiges Projekt, das ein EVE-Spieler in seiner Freizeit entwickelt. Es wird **„wie besehen“** ohne jegliche Gewährleistung bereitgestellt; die Nutzung erfolgt nach eigenem Ermessen. GridSight ist nicht mit Fenris Creations / CCP hf. verbunden und wird von ihnen nicht unterstützt.

---

© 2014 CCP hf. All rights reserved. "EVE", "EVE Online", "CCP", and all related logos and images are trademarks or registered trademarks of CCP hf.

---

**Gemacht von Gridsin** · *Möge das Licht des Tors dich leiten, Kapselpilot.*
