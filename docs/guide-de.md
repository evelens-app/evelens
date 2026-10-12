[English](guide-en.md) · [Русский](guide-ru.md) · **Deutsch** · [简体中文](guide-zh-Hans.md)

# GridSight – Benutzerhandbuch

So installieren, konfigurieren und nutzen Sie GridSight – ein kostenloses Hilfsprogramm für EVE-Online-Multiboxer unter Windows. Die Namen von Schaltflächen und Menüpunkten sind unten wörtlich so angegeben, wie sie in der deutschen Oberfläche von GridSight erscheinen.

GridSight sendet keine Eingaben an das Spiel, liest keinen Client-Speicher und verändert keine Spieldateien. Es liest nur die Logs, die EVE auf die Festplatte schreibt, und die offizielle ESI-API und zeigt die Informationen auf Ihrem Bildschirm an.

## Inhalt

1. [Voraussetzungen](#1-voraussetzungen)
2. [Installation Schritt für Schritt](#2-installation-schritt-für-schritt)
3. [Datenschutz und Sicherheit](#3-datenschutz-und-sicherheit)
4. [Tray-Symbol und Einstellungsfenster](#4-tray-symbol-und-einstellungsfenster)
5. [Miniaturen](#5-miniaturen)
6. [EVE-Logordner und Client-Sprache](#6-eve-logordner-und-client-sprache)
7. [Alarme](#7-alarme)
8. [Intel](#8-intel)
9. [D-Scan- und Lokal-Analyse](#9-d-scan--und-lokal-analyse)
10. [Schadensmonitor und Bergbau](#10-schadensmonitor-und-bergbau)
11. [Ping und FPS](#11-ping-und-fps)
12. [EVE-Login (ESI)](#12-eve-login-esi)
13. [GridSight.Snapshot: Dashboard und Berater](#13-evelenssnapshot-dashboard-und-berater)
14. [Sprache, Updates, Autostart](#14-sprache-updates-autostart)
15. [Problemlösung (FAQ)](#15-problemlösung-faq)
16. [Unterstützung und Feedback](#16-unterstützung-und-feedback)

---

## 1. Voraussetzungen

- **Windows 10 oder 11, 64 Bit (x64).** .NET oder andere Komponenten müssen nicht installiert werden – GridSight ist eine einzige Datei `GridSight.exe` (ca. 165 MB, die Laufzeitumgebung ist enthalten).
- **EVE im Modus „Fenster“ oder „Randloses Fenster“.** Im exklusiven **Vollbildmodus** übernimmt das Spiel den Bildschirm: GridSight-Fenster (Miniaturen, Schadens-Overlay, Ping/FPS-Overlay) können nicht darüber gezeichnet werden. Verwenden Sie „Fenster“ oder „Randloses Fenster“.
- **Arbeitsspeicher:** ca. 115–150 MB RAM bei fünf laufenden Clients; die CPU-Last liegt in der Regel deutlich unter 1 %.
- **Internet** wird nur für optionale Funktionen benötigt: ESI-Login, Intel-Karte und Schiffsklassen (einmaliger Download der statischen Daten von CCP, ca. 95 MB), Marktpreise, zKillboard und Update-Prüfung. Miniaturen und Alarme funktionieren offline.

## 2. Installation Schritt für Schritt

> [!WARNING]
> **GridSight ist noch nicht mit einem Code-Signing-Zertifikat signiert.**
> Ein solches Zertifikat kostet etwa 200–400 $ pro Jahr – für ein unabhängiges kostenloses Projekt ist das derzeit nicht bezahlbar. Deshalb zeigt Windows SmartScreen beim ersten Start ein blaues Fenster:
>
> **„Der Computer wurde durch Windows geschützt“**
>
> Um GridSight zu starten, klicken Sie auf **Weitere Informationen** und dann auf **Trotzdem ausführen**.
>
> Tun Sie das nur für eine Datei, die Sie von der offiziellen Releases-Seite heruntergeladen (Schritt 1) und geprüft haben. Wenn Sie `GridSight.exe` aus einer anderen Quelle haben – nicht ausführen.

### Schritt 1. Datei herunterladen und prüfen

1. Öffnen Sie die Releases-Seite **https://github.com/evelens-app/evelens/releases** und laden Sie `GridSight.exe` aus dem neuesten Release herunter. Laden Sie GridSight nicht von anderen Websites, Foren oder Filehostern.
2. Der Browser meldet eventuell, dass die Datei „nicht häufig heruntergeladen“ wird. Bei einem neuen Programm ist das normal: Öffnen Sie das Download-Menü („…“) und wählen Sie **Beibehalten**.
3. In jeder Release-Beschreibung gibt es einen **VirusTotal**-Link – öffnen Sie ihn und sehen Sie sich das Prüfergebnis der Datei an.
4. Optional: Prüfsumme vergleichen. Öffnen Sie **PowerShell** im Ordner mit der Datei und führen Sie aus:
   ```powershell
   Get-FileHash GridSight.exe
   ```
   Der Wert `SHA256` muss exakt mit dem in der Release-Beschreibung übereinstimmen. Wenn nicht – Datei löschen und erneut von der Releases-Seite herunterladen.

### Schritt 2. GridSight.exe in einen eigenen Ordner legen

GridSight muss nicht installiert werden – es läuft aus dem Ordner, in dem die Datei liegt. Wählen Sie einen dauerhaften Ort, zum Beispiel:

```
%LOCALAPPDATA%\Programs\GridSight\
```

(in die Adressleiste des Explorers einfügen, den Ordner `GridSight` anlegen und `GridSight.exe` dorthin verschieben) oder einen beliebigen eigenen Ordner.

- **Nicht** im Ordner „Downloads“ lassen – dort wird die Datei leicht versehentlich gelöscht.
- **Nicht** in den Spielordner von EVE legen.
- GridSight schreibt nichts neben die exe. Einstellungen, Anordnung und Logs liegen in `%APPDATA%\GridSight\`.
- Wenn Sie den Autostart einschalten, merkt sich GridSight den Pfad der exe. Verschieben Sie die Datei später, schalten Sie „GridSight mit Windows starten“ aus und wieder ein.

### Schritt 3. Markierung „aus dem Internet heruntergeladen“ entfernen

1. Rechtsklick auf `GridSight.exe` → **Eigenschaften**.
2. Auf der Registerkarte **Allgemein** unten das Kästchen **Zulassen** anhaken (fehlt das Kästchen, ist die Datei bereits freigegeben).
3. **OK** klicken.

### Schritt 4. Erster Start und SmartScreen

Doppelklicken Sie auf `GridSight.exe`. Erscheint das Fenster **„Der Computer wurde durch Windows geschützt“**, klicken Sie auf **Weitere Informationen** → **Trotzdem ausführen** (siehe Warnung am Anfang dieses Abschnitts). Normalerweise fragt Windows nur einmal pro Dateiversion.

### Schritt 5. Wenn der Virenscanner Alarm schlägt

Unsignierte Programme kleiner Entwickler lösen manchmal Fehlalarme aus („heuristisch“, „generic“, „ML“), besonders solange das Programm neu ist und erst wenige es heruntergeladen haben. Was tun:

- **Schalten Sie den Virenschutz nicht aus.**
- Prüfen Sie die Datei auf VirusTotal (Link in der Release-Beschreibung) und vergleichen Sie die Prüfsumme (Schritt 1).
- Sind Sie sicher, dass es ein Fehlalarm ist, fügen Sie eine Ausnahme **nur für diese eine Datei** hinzu. Im Microsoft Defender: **Windows-Sicherheit** → **Viren- & Bedrohungsschutz** → unter „Einstellungen für Viren- & Bedrohungsschutz“ auf **Einstellungen verwalten** → **Ausschlüsse** → **Ausschlüsse hinzufügen oder entfernen** → **Ausschluss hinzufügen** → **Datei** → `GridSight.exe` wählen.
- Im Zweifel nicht starten und uns in den [Issues](https://github.com/evelens-app/evelens/issues) schreiben – welcher Virenscanner und was er gemeldet hat.

### Schritt 6. Einstellungen im EVE-Client prüfen

1. **Fenstermodus:** In den Anzeigeeinstellungen von EVE **„Fenster“** oder **„Randloses Fenster“** wählen (nicht Vollbild).
2. **Chat-Protokollierung:** Lokal-Alarme und Intel lesen die Chat-Logs, daher muss EVE den Chat in Dateien schreiben. Suchen Sie in den EVE-Einstellungen (Esc-Menü) die Chat-Option zum Speichern des Chats in eine Datei (im englischen Client **„Log Chat to File“**) und stellen Sie sicher, dass sie aktiviert ist. Ohne sie funktionieren Lokal und Intel nicht (Miniaturen und Kampfalarme schon).
3. **Spiel-Logs (Gamelogs)** – Kampf, Warpstörung, Frachtraum, Bergbau – schreibt EVE automatisch. Hier muss nichts eingeschaltet werden.
4. **Logordner:** Standardmäßig schreibt EVE die Logs nach `Dokumente\EVE\logs` (Unterordner `Gamelogs` und `Chatlogs`). Ist der Ordner „Dokumente“ nach OneDrive verschoben, sieht der Pfad so aus: `…\OneDrive\Dokumente\EVE\logs`. GridSight findet ihn in beiden Fällen selbst (siehe [Abschnitt 6](#6-eve-logordner-und-client-sprache)).

### Schritt 7. Was Sie nach dem Start sehen

- Das GridSight-Symbol (ein orangefarbener Ring) erscheint im Infobereich der Taskleiste unten rechts neben der Uhr. Windows versteckt neue Symbole oft hinter dem Pfeil **^**. Damit es immer sichtbar ist, ziehen Sie das Symbol aus dem **^**-Bereich auf die Taskleiste oder schalten Sie GridSight unter **Einstellungen → Personalisierung → Taskleiste** im Bereich der weiteren Taskleistensymbole (Windows 11) ein.
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
| Account-Timer | an (wirken erst nach Snapshot-Login) | Einstellungen → „Allgemein“ → „Account-Timer überwachen“ |

### Schritt 9. Aktualisieren

1. Neue `GridSight.exe` von der Releases-Seite herunterladen und prüfen (Schritt 1).
2. GridSight schließen: Rechtsklick auf das Tray-Symbol → **Beenden**.
3. Alte `GridSight.exe` im selben Ordner durch die neue ersetzen; freigeben (Schritt 3).
4. Starten. Alle Einstellungen und Positionen der Miniaturen bleiben erhalten – sie liegen in `%APPDATA%\GridSight\`.

### Schritt 10. Deinstallieren

1. Tray-Symbol → **Beenden**.
2. War der Autostart aktiv: vor dem Beenden „GridSight mit Windows starten“ abwählen – oder im Registrierungs-Editor den Wert `GridSight` unter `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run` löschen.
3. `GridSight.exe` löschen (und `GridSight.Snapshot.exe`, falls verwendet).
4. Ordner `%APPDATA%\GridSight` löschen (Einstellungen, Anordnung, Tokens, Cache). Snapshot-Berichte liegen in `%USERPROFILE%\eve-snapshot` – ebenfalls löschen, wenn nicht mehr benötigt.
5. Haben Sie FPS-Rechte erteilt (Abschnitt 11), entfernen Sie sich wieder aus der Gruppe: **Eingabeaufforderung als Administrator** öffnen und den Befehl ausführen, den GridSight unter der Schaltfläche „FPS-Rechte erteilen (UAC)…“ anzeigt – etwa `net localgroup "Leistungsprotokollbenutzer" "<Computer>\<Benutzer>" /delete`. Danach bei Windows ab- und wieder anmelden.
6. Haben Sie Charaktere per ESI verbunden, widerrufen Sie den Zugriff auf der CCP-Seite: https://community.eveonline.com/support/third-party-applications/

## 3. Datenschutz und Sicherheit

**Alles läuft auf Ihrem PC.** GridSight hat keine eigenen Server, keine Telemetrie oder Analyse und keine Benutzerkonten. Es werden keinerlei Daten an den Autor gesendet. EVE-Logs werden nur auf Ihrem Computer gelesen und nirgendwohin hochgeladen.

**Wohin GridSight Verbindungen aufbaut und wozu** – vollständige Liste laut Quellcode:

| Adresse | Wozu | Wann |
|---|---|---|
| `login.eveonline.com` | Offizieller EVE-Login (SSO) | Nur wenn Sie einen Charakter verbinden („ESI verbinden“, `GridSight.Snapshot login`) und zum Verlängern des Zugriffs |
| `esi.evetech.net` | Offizielle EVE-API. Mit Ihrer Erlaubnis – Daten Ihrer verbundenen Charaktere (Standort, Schiff, Online-Status; im Snapshot – die in Abschnitt 13 genannten Daten). Ohne Login – öffentliche Daten: Namen aus Lokal → Corporations/Allianzen, Marktpreise | ESI-Anzeige etwa alle 30 s für verbundene Charaktere; Lokal-Analyse; Preise im Fenster „Bergbau“; Account-Timer alle 10 Min.; Snapshot |
| `developers.eveonline.com` | Statische Spieldaten von CCP (SDE): Gate-Karte, Schiffsklassen, Erzvolumen. Einmalig ca. 95 MB, danach höchstens alle 7 Tage eine Prüfung | Nur wenn Intel, D-Scan-Analyse, Fenster „Bergbau“ oder Snapshot sie brauchen |
| `market.fuzzwork.co.uk` | Aggregierte Jita-Preise (verbreiteter öffentlicher Marktdienst für EVE) | Solange das Fenster „Bergbau“ offen ist; Snapshot |
| `zkillboard.com` | Kill-/Verlust-Statistik von Piloten; Abyss-Verluste für Fittings | Nur über die Schaltfläche „zKill prüfen“; Snapshot-Abschnitt Abyss-Fittings (`--no-fits` schaltet ihn ab) |
| `images.evetech.net` | Offizielle EVE-Bilder (Gegenstände, Charaktere) für den HTML-Bericht | Nur Snapshot |
| `api.github.com` | Prüfen, ob es eine neue GridSight-Version gibt | Einmal täglich; abschaltbar mit „Nach Updates suchen (täglich, GitHub)“ |
| EVE-Spielserver, Port 26000 | Leere TCP-Verbindung zur Ping-Messung | Nur wenn „Ping per Serververbindung (alle 30 s)“ aktiv ist (standardmäßig aus) |
| `localhost:8642` | Nur lokal: nimmt die Login-Antwort aus Ihrem Browser entgegen | Nur während des Logins |

Links im Fenster „Über“ und im Snapshot-Bericht (GitHub, zKillboard, EVE-University-Wiki) öffnen sich im Browser nur, wenn Sie darauf klicken.

**Login-Tokens** werden nur auf diesem Computer gespeichert, mit Windows DPAPI verschlüsselt und an Ihr Windows-Benutzerkonto gebunden – ein anderer Benutzer oder ein anderer PC kann sie nicht entschlüsseln. Ihr EVE-Passwort sieht GridSight nie: Sie melden sich auf der offiziellen EVE-Website an.

**Lizenz und Widerruf des Zugriffs.** GridSight ist eine registrierte Drittanbieter-Anwendung im EVE-Entwicklerportal (developers.eveonline.com) und arbeitet unter der [EVE-Entwicklerlizenz](https://developers.eveonline.com/license-agreement). EVE Online wird vom Studio Fenris Creations entwickelt (bis Mai 2026 hieß es CCP Games); die Lizenz erteilt CCP hf. GridSight ist nicht mit Fenris Creations / CCP verbunden. Sie können den Zugriff von GridSight jederzeit auf der Seite für Drittanbieter-Anwendungen widerrufen: https://community.eveonline.com/support/third-party-applications/

## 4. Tray-Symbol und Einstellungsfenster

**Einstellungen öffnen:** Doppelklick auf das Tray-Symbol oder Rechtsklick → „Einstellungen…“.

**Tray-Menü** (Rechtsklick), von oben nach unten:

- „Version X verfügbar…“ – nur wenn eine neue Version erschienen ist; öffnet die Release-Seite.
- „Timer“ – Account-Timer (Abschnitt 13), sichtbar, wenn die Timer aktiv sind.
- „Zwischenablage analysieren (D-Scan / Lokal)“ – Abschnitt 9.
- „Bergbau“ – Abschnitt 10.
- „Schadensmonitor“ – schaltet das Schadens-Overlay ein und aus.
- „Bearbeitungsmodus“ – Miniaturen verschieben und in der Größe ändern.
- „Einstellungen…“
- „ESI neu verbinden…“ – erscheint nur, wenn der ESI-Zugriff eines Charakters abgelaufen ist oder widerrufen wurde.
- „Ping/FPS: Miniaturen“, „Ping/FPS: Hauptfenster“ – Abschnitt 11.
- „Alarme pausieren“ – neue Alarme vorübergehend nicht anzeigen.
- „Über GridSight“ – Version, Links, Update-Prüfung, Unterstützung.
- „Beenden“

**Tabs der Einstellungen:**

| Tab | Inhalt |
|---|---|
| „Charaktere“ | Alle Charaktere, die GridSight gesehen hat: im Spiel oder nicht, Gruppe, Alarme pro Charakter, Schaltfläche „ESI verbinden“. |
| „Gruppen & Hotkeys“ | Gruppen von Charakteren und Hotkeys zum Umschalten zwischen ihnen. |
| „Alarme“ | Welche Alarme aktiv sind, Schaltflächen „Testen“, Einstellungen für Lokal und Intel. |
| „Schaden“ | Schadensmonitor. |
| „Allgemein“ | Sprache, EVE-Logordner, Miniaturen, Hotkey für den Bearbeitungsmodus, Zwischenablage-Analyse, Bergbau, Kontakt für zKillboard, Ping und FPS, Start und Updates, Account-Timer, ESI Client ID. |

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

## 9. D-Scan- und Lokal-Analyse

GridSight liest Text aus der Zwischenablage – an das Spiel wird nichts gesendet.

**So kopieren Sie im Spiel:**

- **D-Scan:** Im Scannerfenster in die Ergebnisliste klicken, `Strg+A`, dann `Strg+C`.
- **Lokal:** Im Chatfenster die Teilnehmer markieren (ersten anklicken, Umschalt+Klick auf den letzten oder `Strg+A`), dann `Strg+C`.

**Analyse öffnen:** Tray → „Zwischenablage analysieren (D-Scan / Lokal)“ oder eine eigene Tastenkombination: „Allgemein“ → „Zwischenablage-Analyse (D-Scan / Lokal)“ → „Analyse öffnen“ (standardmäßig nicht belegt). Das Fenster erkennt das Format selbst. Nach neuem Kopieren auf „Neu einfügen“ klicken oder die Kombination erneut drücken.

**D-Scan-Ergebnis:** Anzahl der Schiffe und sonstigen Objekte; Schiffe nach Klassen und Typen; ein Block „Achtung“ mit gefährlichen Schiffen (Interdictors/HICs, mobile Bubbles, Kampfsonden, Interceptors, Recons, Bomber, Black Ops, Logistik, Capitals, Supers). „Nur auf dem Grid (≤ 10.000 km)“ blendet entfernte Objekte aus.

**Lokal-Ergebnis:** Piloten nach Allianzen und Corporations gruppiert, die größten oben (Namen werden über die öffentliche ESI-API aufgelöst). Corporations und Allianzen Ihrer verbundenen Charaktere sind grün als „eigene“ markiert. „zKill prüfen“ (nur per Klick) ruft Kills/Verluste für bis zu 20 fremde Piloten aus den größten Gruppen ab; ein Klick auf den Pilotennamen öffnet seine zKillboard-Seite.

Tipp: Unter „Allgemein“ → „Kontakt für zKillboard“ können Sie optional einen Kontakt angeben (E-Mail, Ingame-Name oder Discord) – zKillboard bittet darum, dass sich Tools zu erkennen geben.

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
> Das ist ein Recht für Ihr **gesamtes Windows-Benutzerkonto**, nicht nur für GridSight: Jedes Programm, das unter Ihrem Konto läuft, kann dann Windows-Leistungstracing durchführen. Zum Widerrufen als Administrator den in den Einstellungen angezeigten Befehl `net localgroup "<Gruppe>" "<Sie>" /delete` ausführen und sich danach neu anmelden.

**Ping:** GridSight liest passiv die geglättete Round-Trip-Zeit, die Windows selbst für die Verbindung des Clients zum EVE-Server (Port 26000) misst. `— ms` bedeutet: keine Verbindung (Login-Bildschirm, offline) oder der Client war länger als 60 s still.

**„Ping per Serververbindung (alle 30 s)“** – standardmäßig aus. Eine Ausweichlösung, wenn keine passive Messung möglich ist (keine Tracing-Rechte): GridSight öffnet eine leere TCP-Verbindung zum CCP-Server, misst den Handshake und schließt sie wieder. Es werden keine Daten übertragen, für den CCP-Server sind das aber zusätzliche Verbindungen – deshalb nur bei Bedarf einschalten.

## 12. EVE-Login (ESI)

**Was es bringt:**

- in GridSight: eine Anzeige „System · Schiff“ auf der Miniatur (etwa alle 30 s aktualisiert; „offline“, wenn der Charakter ausgeloggt ist) und das aktuelle System für Intel schon vor dem ersten Sprung;
- in GridSight.Snapshot (Abschnitt 13): Charakter-Dashboard, Berater und Account-Timer.

**So verbinden Sie einen Charakter in GridSight:**

1. Tab „Charaktere“ → **„ESI verbinden“** neben dem Charakter.
2. Der Browser öffnet die offizielle EVE-Anmeldeseite (login.eveonline.com). Melden Sie sich an, **wählen Sie denselben Charakter** und bestätigen Sie.
3. Der Browser leitet zurück zu GridSight, der Status wechselt zu „ESI verbunden“. Wurde im Browser ein anderer Charakter gewählt, verbindet GridSight diesen und weist darauf hin.

GridSight verwendet seine eigene, integrierte ESI-Anwendung; das Feld „Client ID der EVE-Developers-App“ unter „Allgemein“ **kann leer bleiben**. Füllen Sie es nur aus, wenn Sie eine eigene Anwendung verwenden möchten.

**Angefragte Berechtigungen (GridSight):** nur drei Lese-Scopes – aktueller Standort (`esi-location.read_location.v1`), aktuelles Schiff (`esi-location.read_ship_type.v1`) und Online-Status (`esi-location.read_online.v1`).

**Sicherheit:** GridSight sieht Ihr Passwort nie – die Anmeldung läuft über EVE SSO. Tokens werden mit Windows DPAPI verschlüsselt unter Ihrem Windows-Konto gespeichert (`%APPDATA%\GridSight\tokens.bin`, für Snapshot `snapshot-tokens.bin`) und verlassen Ihren PC nicht.

**Zugriff widerrufen:** „ESI trennen“ neben dem Charakter löscht das Token von Ihrem PC. Um die Berechtigung selbst zu widerrufen, nutzen Sie die CCP-Seite: https://community.eveonline.com/support/third-party-applications/. Funktioniert der Zugriff nicht mehr, erscheint im Tray „ESI neu verbinden…“ und beim Charakter die Schaltfläche „Neu anmelden“.

## 13. GridSight.Snapshot: Dashboard und Berater

`GridSight.Snapshot.exe` ist ein separates Konsolenprogramm. Es erstellt per ESI einen Snapshot Ihres Charakters (nur Lesezugriff) und baut daraus einen Markdown-Bericht und ein eigenständiges HTML-Dashboard: Wallet, Skills, Assets mit ISK-Schätzung, Aufträge, Verträge, Industrie, Blaupausen, PI, Klone, LP/Ansehen, Fittings – plus Berater:

- **Produktion** – Gewinn aus Ihren Blaupausen zu Jita-Preisen;
- **Wiederaufbereitung und Bergbau** – Roherz verkaufen, komprimieren oder wiederaufbereiten;
- **PI → P2** – Fabrik vs. Verkauf von P1;
- **Handel** – Verkauf von Assets, Jita-Stationshandel-Scanner, Überwachung Ihrer Aufträge;
- **Abyss-Fittings** – beliebte Fittings von zKillboard, abgeglichen mit Ihren Skills und Assets, mit Jita-Multibuy-Liste;
- **To-do** – Zusammenfassung der Ratschläge aus allen Abschnitten.

**Befehle** (im Terminal im Ordner mit `GridSight.Snapshot.exe` ausführen; in PowerShell mit vorangestelltem `.\`):

| Befehl | Wirkung |
|---|---|
| `GridSight.Snapshot login` | EVE-Login im Browser (nur Lese-Scopes); einmal pro Charakter |
| `GridSight.Snapshot login --fits-write` | Ebenso, plus Schreibrecht für gespeicherte Fittings (nur für `--export-fits` nötig) |
| `GridSight.Snapshot` | Snapshot aller verbundenen Charaktere |
| `GridSight.Snapshot -c "<Charakter>"` | Snapshot eines Charakters |
| `GridSight.Snapshot -c "<Charakter>" --export-fits <Rumpf\|all> [--top N]` | Top-N (1–3) Abyss-Fittings des Rumpfes als `GridSight <Rumpf> #N` in die gespeicherten Fittings im Spiel schreiben |
| `GridSight.Snapshot --lang de` | Sprache des Berichts: `de`, `en`, `ru`, `zh-Hans` (Standard – Sprache der GridSight-Oberfläche, sonst Windows) |
| `GridSight.Snapshot --help` | Vollständige Liste der Optionen (`--no-open`, `--no-market`, `--no-fits` u. a.) |

Der Snapshot-Login fragt nur Lese-Scopes an: Skills und Warteschlange, Wallet, Assets, Marktaufträge, Verträge, Industrie-Jobs und Bergbau, Blaupausen, Planeten, Klone und Implantate, LP, Ansehen, Fittings, Strukturen und Standort. Schreiben ist nur nach `login --fits-write` möglich, und geschrieben werden ausschließlich gespeicherte Fittings.

**Wo das HTML liegt:** `%USERPROFILE%\eve-snapshot\` – `latest-<Charakter>.html` (öffnet sich nach jedem Snapshot automatisch im Browser; `--no-open` verhindert das) sowie datierte Kopien `<Charakter>-<Datum>.html` und `.md`. Die Datei funktioniert offline und lässt sich beliebig kopieren.

**Account-Timer im Tray:** Nach `GridSight.Snapshot login` prüft GridSight alle 10 Minuten PI-Extraktoren, freie Fertigungsslots und die Skill-Warteschlange. Braucht etwas Aufmerksamkeit, erscheint ein Punkt am Tray-Symbol; die Liste steht unter Tray → „Timer“ (ein Klick auf einen Eintrag öffnet den letzten Snapshot). Abschalten mit „Allgemein“ → „Account-Timer überwachen“.

## 14. Sprache, Updates, Autostart

**Sprache der Oberfläche:** „Allgemein“ → „Sprache“ → „Sprache der Oberfläche“: „Auto (Windows-Sprache)“, English, Русский, Deutsch, 简体中文. Wird sofort übernommen. Sie ist unabhängig von der EVE-Client-Sprache (Abschnitt 6). Namen von Gegenständen aus den CCP-Daten werden in allen Oberflächen außer der russischen auf Englisch angezeigt.

**Updates:** „Nach Updates suchen (täglich, GitHub)“ ist standardmäßig aktiv. Einmal täglich fragt GridSight bei GitHub nach einer neuen Version. Gibt es eine – Menüpunkt „Version X verfügbar…“ im Tray, eine Benachrichtigung und eine Zeile unter „Über“. **GridSight lädt und installiert nie selbst etwas** – aktualisieren Sie manuell (Abschnitt 2, Schritt 9). „Betaversionen anbieten“ – auch über Betas informieren. Manuell prüfen: „Über GridSight“ → „Nach Updates suchen“.

**Autostart:** „Allgemein“ → „Start“ → „GridSight mit Windows starten“. Trägt GridSight in den Autostart Ihres Benutzers ein (Registrierung `HKCU\…\Run`); Abwählen entfernt den Eintrag.

## 15. Problemlösung (FAQ)

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

**„Der Computer wurde durch Windows geschützt“.** Erwartet – GridSight ist nicht signiert. Datei prüfen (Abschnitt 2, Schritt 1), dann **Weitere Informationen → Trotzdem ausführen**.

**GridSight startet nicht / zeigt einen Fehler.** Die Meldung nennt den Ort des Logs. Ist die Einstellungsdatei beschädigt, stellt GridSight die Einstellungen automatisch aus `settings.json.bak` wieder her.

**Wo liegt das GridSight-Log und was gehört in ein Issue.** Die Logs liegen in `%APPDATA%\GridSight\logs\` (eine Datei pro Tag, `evelens-JJJJMMTT.log`). Bitte geben Sie in einem [Issue](https://github.com/evelens-app/evelens/issues) an:
- GridSight-Version („Über GridSight“);
- Windows-Version, Fenstermodus von EVE, Sprache des EVE-Clients, Anzahl der Clients und Monitore;
- was Sie getan haben, was Sie erwartet haben, was passiert ist (ein Screenshot hilft sehr);
- die Logdatei des betreffenden Tages. Sehen Sie sie vor dem Senden durch – sie kann Namen Ihrer Charaktere enthalten; diese können Sie ersetzen.

## 16. Unterstützung und Feedback

GridSight ist kostenlos, und keine Funktion hängt von einer Spende ab. Wenn es Ihnen das Flottenleben erleichtert, können Sie sich mit einem beliebigen ISK-Betrag an den Charakter **Gridsin** im Spiel bedanken („Über GridSight“ → „Charakternamen kopieren“).

Vorschläge, Wünsche und Fehlermeldungen: [GitHub Issues](https://github.com/evelens-app/evelens/issues) oder per EVE-Mail an **Gridsin**.

GridSight ist ein unabhängiges Projekt, das ein EVE-Spieler in seiner Freizeit entwickelt. Es wird **„wie besehen“** ohne jegliche Gewährleistung bereitgestellt; die Nutzung erfolgt nach eigenem Ermessen. GridSight ist nicht mit Fenris Creations / CCP hf. verbunden und wird von ihnen nicht unterstützt.

---

© 2014 CCP hf. All rights reserved. "EVE", "EVE Online", "CCP", and all related logos and images are trademarks or registered trademarks of CCP hf.

---

**Gemacht von Gridsin** · *Möge das Licht des Tors dich leiten, Kapselpilot.*
