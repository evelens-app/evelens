**English** · [Русский](guide-ru.md) · [Deutsch](guide-de.md) · [简体中文](guide-zh-Hans.md)

# EveLens user guide

How to install, set up and use EveLens — a free companion app for EVE Online multiboxers on Windows. Button and menu names below are quoted exactly as they appear in the English EveLens interface.

EveLens never sends input to the game, never reads client memory and never modifies game files. It reads the logs EVE writes to disk and the official ESI API, and shows information on your screen.

## Contents

1. [Requirements](#1-requirements)
2. [Installation step by step](#2-installation-step-by-step)
3. [Privacy and security](#3-privacy-and-security)
4. [Tray icon and settings window](#4-tray-icon-and-settings-window)
5. [Thumbnails](#5-thumbnails)
6. [EVE logs folder and client language](#6-eve-logs-folder-and-client-language)
7. [Alerts](#7-alerts)
8. [Intel](#8-intel)
9. [D-Scan and Local analysis](#9-d-scan-and-local-analysis)
10. [Damage monitor and Mining](#10-damage-monitor-and-mining)
11. [Ping and FPS](#11-ping-and-fps)
12. [EVE login (ESI)](#12-eve-login-esi)
13. [EveLens.Snapshot: dashboard and advisor](#13-evelenssnapshot-dashboard-and-advisor)
14. [Language, updates, autostart](#14-language-updates-autostart)
15. [Troubleshooting (FAQ)](#15-troubleshooting-faq)
16. [Support and feedback](#16-support-and-feedback)

---

## 1. Requirements

- **Windows 10 or 11, 64-bit (x64).** You don't need to install .NET or anything else — EveLens is a single `EveLens.exe` file (about 165 MB, the runtime is packed inside).
- **EVE in "Windowed" or "Fixed Window" mode.** In exclusive **Fullscreen** the game takes over the screen: EveLens windows (thumbnails, damage overlay, ping/FPS overlay) can't be drawn on top of it. Use Windowed or Fixed Window (borderless).
- **Memory:** about 115–150 MB of RAM with five clients running; CPU load is usually well under 1%.
- **Internet** is needed only for optional features: ESI login, Intel map and ship classes (a one-time download of CCP static data, about 95 MB), market prices, zKillboard and update checks. Thumbnails and alerts work offline.

## 2. Installation step by step

> [!WARNING]
> **EveLens is not code-signed yet.**
> A code-signing certificate costs about $200–400 per year, which an independent free project can't afford for now. Because of that, Windows SmartScreen shows a blue window when you first start it:
>
> **"Windows protected your PC"**
>
> To start EveLens, click **More info**, then **Run anyway**.
>
> Only do this for a file you downloaded from the official Releases page (step 1) and checked. If you got `EveLens.exe` from anywhere else — don't run it.

### Step 1. Download and check the file

1. Open the Releases page: **https://github.com/evelens-app/evelens/releases** and download `EveLens.exe` from the latest release. Don't download EveLens from other sites, forums or file shares.
2. Your browser may say the file "isn't commonly downloaded". That's normal for a new program: open the download menu ("…") and choose **Keep**.
3. Each release description has a **VirusTotal** link — open it and check the scan result for the file.
4. Optional: compare the checksum. Open **PowerShell** in the folder with the file and run:
   ```powershell
   Get-FileHash EveLens.exe
   ```
   The `SHA256` value must match the one in the release description exactly. If it doesn't — delete the file and download it again from the Releases page.

### Step 2. Put EveLens.exe in its own folder

EveLens doesn't need installing — it runs from wherever the file is. Choose a permanent place for it, for example:

```
%LOCALAPPDATA%\Programs\EveLens\
```

(paste this into the Explorer address bar, create the `EveLens` folder and move `EveLens.exe` there), or any folder of your own.

- **Don't** leave it in "Downloads" — it's easy to delete by accident there.
- **Don't** put it into the EVE game folder.
- EveLens writes nothing next to the exe. Settings, layout and logs are stored in `%APPDATA%\EveLens\`.
- If you turn on autostart, EveLens remembers the exe path. If you later move the file, turn "Start EveLens with Windows" off and on again.

### Step 3. Remove the "downloaded from the Internet" mark

1. Right-click `EveLens.exe` → **Properties**.
2. On the **General** tab, at the bottom, tick **Unblock** (if there's no such checkbox, the file is already unblocked).
3. Click **OK**.

### Step 4. First start and SmartScreen

Double-click `EveLens.exe`. If the **"Windows protected your PC"** window appears, click **More info** → **Run anyway** (see the warning at the top of this section). Windows usually asks only once per file version.

### Step 5. If your antivirus complains

Unsigned programs from small developers sometimes trigger false alarms ("heuristic", "generic", "ML" detections), especially when the program is new and few people have downloaded it yet. What to do:

- **Do not turn your antivirus off.**
- Check the file on VirusTotal (link in the release description) and make sure the checksum matches (step 1).
- If you're confident it's a false positive, add an exclusion **for this one file only**. In Microsoft Defender: **Windows Security** → **Virus & threat protection** → under "Virus & threat protection settings" click **Manage settings** → **Exclusions** → **Add or remove exclusions** → **Add an exclusion** → **File** → choose `EveLens.exe`.
- If in doubt, don't run it and write to us in [Issues](https://github.com/evelens-app/evelens/issues) — tell us which antivirus and what it reported.

### Step 6. Check your EVE client settings

1. **Window mode:** in the EVE display settings choose **Windowed** or **Fixed Window** (not Fullscreen).
2. **Chat logging:** Local alerts and Intel read chat logs, so EVE must write chat to files. In the EVE settings (Esc menu), find the chat option **"Log Chat to File"** and make sure it's on. Without it, Local and Intel won't work (thumbnails and combat alerts still will).
3. **Game logs (Gamelogs)** — combat, warp scrambling, cargo and mining messages — are written by EVE automatically. Nothing to turn on.
4. **Logs folder:** by default EVE writes logs to `Documents\EVE\logs` (subfolders `Gamelogs` and `Chatlogs`). If your Documents folder is moved to OneDrive, the path looks like `…\OneDrive\Documents\EVE\logs`. EveLens finds it automatically in both cases (see [section 6](#6-eve-logs-folder-and-client-language)).

### Step 7. What you'll see after the start

- The EveLens icon (an orange ring) appears in the system tray, in the bottom-right corner next to the clock. Windows often hides new icons under the **^** arrow. To keep it always visible, drag the icon from the **^** area onto the taskbar, or go to **Settings → Personalization → Taskbar → Other system tray icons** (Windows 11) and switch EveLens on.
- **Double-click** the icon to open settings. **Right-click** it for the menu.
- As soon as EVE clients are running, a thumbnail appears for each of them. While a client is on the character selection screen, its thumbnail says "logging in…".
- If the tray menu shows "⚠ EVE logs folder not found", EVE hasn't been started yet on this PC, or the logs are elsewhere — see [section 6](#6-eve-logs-folder-and-client-language).

### Step 8. What you can turn off if you don't need it

Everything in settings applies and saves instantly — there is no Save button.

| Feature | Default | Where to turn it off |
|---|---|---|
| Ping and FPS | off | Tray: "Ping/FPS: thumbnails", "Ping/FPS: main window"; or Settings → "General" → "Ping & FPS" |
| Damage monitor | off | Tray: "Damage monitor"; Settings → "Damage" |
| Intel | off | Settings → "Alerts" → "Watch intel channels" |
| Single alert types | on | Settings → "Alerts" (for all characters) or "Characters" (for one) |
| All alerts for a while | — | Tray: "Pause alerts" |
| Update check | on | Settings → "General" → "Check for updates (daily, GitHub)" |
| Autostart | off | Settings → "General" → "Start EveLens with Windows" |
| Account timers | on (work only after Snapshot login) | Settings → "General" → "Track account timers" |

### Step 9. Updating

1. Download the new `EveLens.exe` from the Releases page and check it (step 1).
2. Close EveLens: right-click the tray icon → **Exit**.
3. Replace the old `EveLens.exe` with the new one in the same folder; unblock it (step 3).
4. Start it. All settings and thumbnail positions are kept — they live in `%APPDATA%\EveLens\`.

### Step 10. Uninstalling

1. Tray icon → **Exit**.
2. If autostart was on: before exiting, untick "Start EveLens with Windows" — or delete the `EveLens` value under `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run` in the Registry Editor.
3. Delete `EveLens.exe` (and `EveLens.Snapshot.exe`, if you used it).
4. Delete the `%APPDATA%\EveLens` folder (settings, layout, tokens, cache). Snapshot reports are in `%USERPROFILE%\eve-snapshot` — delete it too if you don't need them.
5. If you granted FPS rights (section 11), remove yourself from the group: open **Command Prompt as administrator** and run the command shown in EveLens under the "Grant FPS access (UAC)…" button — it looks like `net localgroup "Performance Log Users" "<Computer>\<User>" /delete`. Then sign out of Windows and back in.
6. If you connected characters via ESI, revoke access on the CCP site: https://community.eveonline.com/support/third-party-applications/

## 3. Privacy and security

**Everything runs on your PC.** EveLens has no servers of its own, no telemetry or analytics and no accounts. Nothing is ever sent to the author. EVE logs are read only on your computer and are never uploaded anywhere.

**Where EveLens connects to, and why** — the complete list from the source code:

| Address | What for | When |
|---|---|---|
| `login.eveonline.com` | Official EVE login (SSO) | Only when you connect a character ("Connect ESI", `EveLens.Snapshot login`) and to refresh its access |
| `esi.evetech.net` | Official EVE API. With your permission — data of your connected characters (location, ship, online status; in Snapshot — the data listed in section 13). Without login — public data: Local names → corporations/alliances, market prices | ESI badge about every 30 s for connected characters; Local analysis; prices in the Mining window; account timers every 10 min; Snapshot |
| `developers.eveonline.com` | CCP static game data (SDE): stargate map, ship classes, ore volumes. About 95 MB once, then checked at most every 7 days | Only when Intel, the D-Scan analysis, the Mining window or Snapshot needs it |
| `market.fuzzwork.co.uk` | Jita price aggregates (a popular public EVE market service) | While the Mining window is open; Snapshot |
| `zkillboard.com` | Pilot kill/loss statistics; abyssal losses for fits | Only on the "Check on zKill" button; Snapshot "Abyssal fits" (`--no-fits` turns it off) |
| `images.evetech.net` | Official EVE images (items, characters) for the HTML report | Snapshot only |
| `api.github.com` | Check whether a new EveLens version exists | Once a day; turn off with "Check for updates (daily, GitHub)" |
| EVE game server, port 26000 | An empty TCP connection to measure ping | Only if "Ping by connecting to the server (every 30 s)" is on (off by default) |
| `localhost:8642` | Local only: receives the login answer from your browser | Only during login |

Links in the "About" window and in the Snapshot report (GitHub, zKillboard, EVE University wiki) open in your browser only when you click them.

**Login tokens** are stored only on this computer, encrypted with Windows DPAPI and bound to your Windows user account — another user or another PC can't decrypt them. EveLens never sees your EVE password: you log in on the official EVE website.

**License and revoking access.** EveLens is a registered third-party application on the EVE developer portal (developers.eveonline.com) and works under the [EVE developer license](https://developers.eveonline.com/license-agreement). EVE Online is developed by Fenris Creations (named CCP Games until May 2026); the license is granted by CCP hf. EveLens is not affiliated with Fenris Creations or CCP. You can revoke EveLens's access at any time on the third-party applications page: https://community.eveonline.com/support/third-party-applications/

## 4. Tray icon and settings window

**Opening settings:** double-click the tray icon, or right-click → "Settings…".

**Tray menu** (right-click), top to bottom:

- "Version X available…" — only when a new version is out; opens the release page.
- "Timers" — account timers (section 13), visible when timers are on.
- "Parse clipboard (D-Scan / Local)" — section 9.
- "Mining" — section 10.
- "Damage monitor" — toggles the damage overlay.
- "Edit mode" — move and resize thumbnails.
- "Settings…"
- "Reconnect ESI…" — appears only if a character's ESI access has expired or was revoked.
- "Ping/FPS: thumbnails", "Ping/FPS: main window" — section 11.
- "Pause alerts" — temporarily stops new alerts.
- "About" — version, links, update check, support.
- "Exit"

**Settings tabs:**

| Tab | What's there |
|---|---|
| "Characters" | Every character EveLens has seen: online status, group, per-character alerts, "Connect ESI" button. |
| "Groups & hotkeys" | Groups of characters and hotkeys to cycle between them. |
| "Alerts" | Which alerts are on, "Test" buttons, Local and Intel settings. |
| "Damage" | Damage monitor. |
| "General" | Language, EVE logs folder, thumbnails, edit mode hotkey, clipboard parser, mining, zKillboard contact, ping & FPS, startup and updates, account timers, ESI Client ID. |

At the bottom of the window — the "About / Support" link.

## 5. Thumbnails

**Layout.** Each character gets its own thumbnail position and size; they are remembered per character, so after restarting a client its thumbnail returns to the same place. A new thumbnail is 320 px wide. Thumbnails keep the client window's proportions (black bars if the shapes differ).

**Edit mode** — default hotkey **`Ctrl+Alt+E`** (or tray → "Edit mode"):

- drag a thumbnail to move it; thumbnails snap to each other;
- drag the bottom-right corner to resize (minimum width 120 px);
- position and size are saved as soon as you release the mouse;
- press `Ctrl+Alt+E` again to leave edit mode.

The edit mode hotkey can be changed in "General" → "Edit mode".

**Switching.** Click a thumbnail to bring that client to the front. A minimized client shows "minimized" and is restored by the click.

**Appearance** ("General" → "Thumbnails"):

- "Opacity" — 30–100%, applies to the whole thumbnail window;
- "Hide the active client's thumbnail" — you already see that client;
- "Hide all thumbnails when EVE isn't in the foreground" — thumbnails disappear while you're in a browser, Discord etc.

**Groups and hotkeys** ("Groups & hotkeys" tab):

1. Click "Add" and give the group a name in "Group name" (e.g. "Fleet").
2. Choose a character in the list at the bottom and click "Add to group". Repeat for every character. You can also choose the group for a character on the "Characters" tab.
3. Set "Next character" and "Previous character": click the field and press a combination, e.g. `Ctrl+Alt+F1`. Without Ctrl/Alt/Shift/Win only F1–F24 work; Shift alone isn't enough; Alt+F4 can't be used. Backspace clears, Esc cancels.
4. "Cycle order" is top to bottom: drag rows or use "Up" / "Down". Characters whose clients aren't running are skipped.

If a combination is already taken by another program or another EveLens hotkey, EveLens shows it in red — choose another one.

## 6. EVE logs folder and client language

**Auto-detection.** EveLens looks for logs in `Documents\EVE\logs`, using the real location of your Documents folder — including when Windows has moved it to OneDrive (`…\OneDrive\Documents\EVE\logs`). If the folder doesn't exist yet (EVE has never been started), EveLens waits and picks it up as soon as it appears.

**Check:** "General" → "EVE logs folder". Under the path:

- "Found: Gamelogs and Chatlogs are readable." — all good;
- "Gamelogs folder not found — alerts won't work. …" — specify the folder manually.

**Setting it manually:** click "Browse…" and choose the `logs` folder inside `EVE` (the one containing `Gamelogs` and `Chatlogs`), or paste the path into the field.

**EVE client language for log parsing.** Alerts, damage, mining and Local are recognized from the text of game log lines, so EveLens needs to know your client language. This is separate from the EveLens interface language. "General" → "Language" → "EVE client language (for log parsing)":

- "Auto (from log lines)" — default, recognizes Russian and English clients by the lines themselves;
- "RU — Russian client" / "EN — English client" — only that language's patterns.

> [!NOTE]
> Alerts, damage monitor and mining are currently tuned and verified on the **Russian** EVE client. **English** client support is in testing — if something doesn't trigger on the English client, please report it in Issues. Other client languages (German, Chinese, etc.) are not parsed yet: thumbnails, switching, D-Scan/Local analysis and ESI work, but log-based alerts don't.

## 7. Alerts

Alerts are shown **only as a colored border on the thumbnail — no sounds**. The border flashes for 5 seconds and then stays lit until you switch to that client. The active client (in the foreground) never gets alerts — you're already looking at it.

| Color | Alert | When |
|---|---|---|
| Orange | "Warp scramble/disruption (you're tackled)" | You're warp scrambled or disrupted |
| Red | "Attack (ship is taking damage)" | Your ship is taking damage |
| Purple | "Intel (system near the character reported in intel)" | See section 8 |
| Yellow | "Ship (cargo hold full)" | Cargo/ore hold is full (also from the mining hold estimate, section 10) |
| Cyan | "Local (messages in system chat)" | A message in Local, a system change, or a message from a watched name |

If several alerts are active, the most important one is shown (order as in the table); the others appear as small colored dots.

**Settings ("Alerts" tab):**

- checkboxes turn an alert type on/off for all characters; per-character switches are on the "Characters" tab;
- **"Test"** next to each type lights up all open thumbnails in that color — a quick way to check what it looks like;
- "When Local triggers": "Any message in Local", "System change", and a list "Always alert on messages from these names (one per line)".

EVE doesn't log who enters Local, so a "neutral entered system" alert is impossible. A character logging in and messages from your own characters don't trigger Local alerts.

**Pause:** tray → "Pause alerts" — new events don't light borders until you untick it.

## 8. Intel

EveLens can read your intel channels and highlight the character who is near a reported system.

1. Make sure chat logging is on in EVE (section 2, step 6).
2. "Alerts" → "Intel" → tick **"Watch intel channels"**.
3. In "Channels" enter the channel names, one per line, exactly as at the start of the chat log file name (files look like `<Channel>_YYYYMMDD_HHMMSS_….txt` in `Chatlogs`). Case doesn't matter.
4. Set "Radius:" — 1 to 15 jumps (default 5).

On first use EveLens downloads the CCP static data (about 95 MB) to build the stargate map; the status is shown under the slider ("Map loaded: … systems with gates.").

**How it works:** if a message in the channel names a system within the radius of a character's current system (counted by gates), that character's thumbnail glows purple and its strip shows `Intel: <system> · <N> j` (the nearest one). The character's system is taken from Local or ESI; until it's known, Intel isn't evaluated for that character.

**Clearing:** a message with **`clr`** or **`clear`** (also the Russian `чисто`) clears the alert for the systems named in the same message, e.g. `Perimeter clr`. Switching to the client clears it too.

Limitations: abbreviations and suffixes ("1DQ", "Urlen-gate") aren't recognized; system names that are ordinary words (`Bar`, `Exit`, `Pain`, `Dead End`…) are only caught when written with a capital letter as in the game. System names must be written in Latin letters. Wormhole systems are ignored.

## 9. D-Scan and Local analysis

EveLens reads text from the clipboard — nothing is sent to the game.

**How to copy in the game:**

- **D-Scan:** in the scanner window click the results list, press `Ctrl+A`, then `Ctrl+C`.
- **Local:** in the chat window select the members (click the first, Shift+click the last, or `Ctrl+A`), then `Ctrl+C`.

**How to open the analysis:** tray → "Parse clipboard (D-Scan / Local)", or your own hotkey: "General" → "Clipboard parser (D-Scan / Local)" → "Open parser window" (not set by default). The window detects the format by itself. After copying something new, click "Paste again" or press the hotkey again.

**D-Scan result:** number of ships and other objects; ships by class and type; an "Attention" block for dangerous ships (interdictors/HICs, mobile bubbles, combat probes, interceptors, recons, bombers, Black Ops, logistics, capitals, supers). "On grid only (≤ 10,000 km)" hides far objects.

**Local result:** pilots grouped by alliance and corporation, biggest first (names are resolved through the public ESI API). Corporations and alliances of your connected characters are marked "own" in green. "Check on zKill" (only on click) looks up kills/losses for up to 20 non-friendly pilots from the largest groups; a pilot's name opens their zKillboard page.

Tip: in "General" → "zKillboard contact" you can enter an optional contact (email, in-game name or Discord) — zKillboard asks that tools identify themselves.

## 10. Damage monitor and Mining

### Damage monitor

"Damage" tab (everything off by default):

- **"⬆ 412 · ⬇ 95 DPS" strip on thumbnails during combat** — outgoing (⬆) and incoming (⬇) DPS;
- **"Always-on-top overlay window"** — a small window with DPS, peak and fight total; also toggled from the tray → "Damage monitor";
- **"DPS window:"** — the sliding window for the calculation, 3–60 s (default 10).

The overlay doesn't take clicks or focus. To move it, turn on edit mode (`Ctrl+Alt+E`) and drag it. It shows the active character if they're in combat, otherwise the last one who fought. A fight ends after 30 s without shots. Repairs, neuts, nos and EWAR don't count as damage. Nothing is saved to disk.

### Mining

Open via tray → "Mining" (or a hotkey: "General" → "Mining" → "Open Mining window", not set by default). The window reads mining lines from the game logs of all characters: ore, ice, moon ore, gas.

- Per character: mined amounts by type (units, m³, ISK), "ISK/h · 10 min", "ISK/h · session", "m³/h · 10 min", "m³/h · session", residue.
- A new session starts after a pause longer than N minutes ("New session after a pause longer than", default 10). If EveLens is started mid-session, it picks up the last 6 hours from the logs.
- ISK is calculated at Jita 4-4 buy orders, before taxes. "Value as compressed" — use compressed ore prices where available.

**Hold:** EVE doesn't write hold capacity to the logs — enter it in the character card ("Hold, m³"). Then you'll see the fill and "full in ≈ mm:ss". After unloading, click **"Unloaded"** — the fill is counted again from this minute. "Highlight thumbnail when hold ≈ 95%" lights the yellow "Ship" alert based on this estimate (once per fill, no sound).

## 11. Ping and FPS

**Where to turn on:** "General" → "Ping & FPS" (off by default), or in the tray:

- "Ping/FPS: thumbnails" / "Show on thumbnails" — `62 fps · 38 ms` on the right of each thumbnail strip (the Intel text has priority while it's lit);
- "Ping/FPS: main window" / "Show over the main window (EVE client in focus)" — a small overlay in a corner of the active EVE window; the corner is set in "Main window corner" (default "Top right"). Not visible in exclusive Fullscreen.

Measurements come from Windows system tracing (ETW, the same way PresentMon works). Nothing is injected into the client and, by default, EveLens doesn't connect to CCP servers.

**FPS rights.** Windows tracing requires either running EveLens as administrator or membership in the **"Performance Log Users"** group. Without it, thumbnails show `FPS: no access`, and the settings show the button **"Grant FPS access (UAC)…"**:

1. Click "Grant FPS access (UAC)…" and confirm the Windows UAC prompt. EveLens runs a single command: `net localgroup "<group>" "<you>" /add`.
2. **Sign out of Windows and sign in again** (or reboot) — the right only takes effect after a new sign-in.
3. Start EveLens and click "Check again" if needed. The status should say "Tracing is running: …".

> [!IMPORTANT]
> This is a right for your **whole Windows user account**, not just for EveLens: any program running as you will be able to trace Windows performance. To revoke it, run as administrator the command shown in the settings, `net localgroup "<group>" "<you>" /delete`, then sign in again.

**Ping:** EveLens passively reads the smoothed round-trip time that Windows itself measures for the client's connection to the EVE server (port 26000). `— ms` means there is no connection (login screen, offline) or the client has been silent for more than 60 s.

**"Ping by connecting to the server (every 30 s)"** — off by default. It's a fallback for when passive measurement isn't available (no tracing rights): EveLens opens an empty TCP connection to the CCP server, times the handshake and closes it. No data is sent, but these are extra connections to CCP's server, so we keep it off unless you need it.

## 12. EVE login (ESI)

**What it gives:**

- in EveLens: a "system · ship" badge on the thumbnail (updated about every 30 s; "offline" when the character has logged off) and the current system for Intel even before a jump;
- in EveLens.Snapshot (section 13): character dashboard, advisor and account timers.

**How to connect a character in EveLens:**

1. "Characters" tab → **"Connect ESI"** next to the character.
2. Your browser opens the official EVE login page (login.eveonline.com). Log in and **choose the same character**, then authorize.
3. The browser returns to EveLens, and the status changes to "ESI connected". If you chose another character in the browser, EveLens connects that one and tells you.

EveLens uses its own built-in ESI application, so the "EVE Developers application Client ID" field in "General" **can be left empty**. Fill it in only if you want to use your own application.

**Permissions requested (EveLens):** only three read-only scopes — current location (`esi-location.read_location.v1`), current ship (`esi-location.read_ship_type.v1`) and online status (`esi-location.read_online.v1`).

**Security:** EveLens never sees your password — login goes through EVE SSO. Tokens are stored encrypted with Windows DPAPI under your Windows account (`%APPDATA%\EveLens\tokens.bin`, for Snapshot — `snapshot-tokens.bin`) and never leave your PC.

**Revoking access:** "Disconnect ESI" next to the character removes the token from your PC. To revoke the authorization itself, use the CCP page: https://community.eveonline.com/support/third-party-applications/. If access stops working, the tray shows "Reconnect ESI…" and the character's button changes to "Log in again".

## 13. EveLens.Snapshot: dashboard and advisor

`EveLens.Snapshot.exe` is a separate console program. It takes a read-only snapshot of your character through ESI and builds a Markdown report and a self-contained HTML dashboard: wallet, skills, assets with ISK estimate, orders, contracts, industry, blueprints, PI, clones, LP/standings, fittings — plus the advisor:

- **Production** — profit from your blueprints at Jita prices;
- **Reprocessing and mining** — sell raw, compress or reprocess;
- **PI → P2** — factory vs selling P1;
- **Trading** — selling assets, a Jita station-trading scanner, watching your orders;
- **Abyssal fits** — popular fits from zKillboard checked against your skills and assets, with a Jita multibuy list;
- **To do** — a summary of advice from all sections.

**Commands** (run in a terminal in the folder with `EveLens.Snapshot.exe`; prefix with `.\` in PowerShell):

| Command | What it does |
|---|---|
| `EveLens.Snapshot login` | EVE login in the browser (read-only scopes); do it once per character |
| `EveLens.Snapshot login --fits-write` | Same, plus permission to write saved fittings (needed only for `--export-fits`) |
| `EveLens.Snapshot` | Snapshot of all connected characters |
| `EveLens.Snapshot -c "<character>"` | Snapshot of one character |
| `EveLens.Snapshot -c "<character>" --export-fits <hull\|all> [--top N]` | Write the top N (1–3) abyssal fits for the hull into the game's saved fittings as `EveLens <Hull> #N` |
| `EveLens.Snapshot --lang en` | Report language: `en`, `ru`, `de`, `zh-Hans` (default — the EveLens interface language, otherwise Windows) |
| `EveLens.Snapshot --help` | Full list of options (`--no-open`, `--no-market`, `--no-fits` and others) |

The Snapshot login asks for read-only scopes: skills and queue, wallet, assets, market orders, contracts, industry jobs and mining, blueprints, planets, clones and implants, LP, standings, fittings, structures, and location. Writing is only possible after `login --fits-write`, and only saved fittings are written.

**Where the HTML is:** `%USERPROFILE%\eve-snapshot\` — `latest-<character>.html` (opens in your browser automatically after each snapshot; `--no-open` to skip) and dated copies `<character>-<date>.html` plus `.md`. The file works offline and can be copied anywhere.

**Account timers in the tray:** after `EveLens.Snapshot login`, EveLens checks every 10 minutes for PI extractors, free industry slots and the skill queue. A dot appears on the tray icon when something needs attention; the list is in tray → "Timers" (clicking an entry opens the latest snapshot). Turned off with "General" → "Track account timers".

## 14. Language, updates, autostart

**Interface language:** "General" → "Language" → "Interface language": "Auto (Windows language)", English, Русский, Deutsch, 简体中文. Applies immediately. It doesn't depend on the EVE client language (section 6). Names of items from CCP data are shown in English in all interfaces except Russian.

**Updates:** "Check for updates (daily, GitHub)" is on by default. Once a day EveLens asks GitHub whether a new version exists. If yes — a tray menu item "Version X available…", one pop-up notification and a line in "About". **EveLens never downloads or installs anything by itself** — update manually (section 2, step 9). "Offer beta versions" — also notify about betas. You can check manually in "About" → "Check for updates".

**Autostart:** "General" → "Startup" → "Start EveLens with Windows". It adds EveLens to your user's startup list (registry `HKCU\…\Run`); unticking removes it.

## 15. Troubleshooting (FAQ)

**No thumbnails.**
- Is EVE running in Windowed or Fixed Window mode (not Fullscreen)?
- Is "Hide all thumbnails when EVE isn't in the foreground" on? Then thumbnails are hidden while another program is active.
- Is "Hide the active client's thumbnail" on? With one client, its thumbnail is hidden while it's active.
- Is EveLens running at all (icon in the tray, maybe under **^**)?

**A thumbnail is in the wrong place / off-screen.** Turn on edit mode (`Ctrl+Alt+E`) and drag it. After unplugging a monitor, thumbnails move to the main screen and return when the monitor is back. A thumbnail is bound to a character: until the character is selected, a new client shows "logging in…".

**FPS shows "FPS: no access" or "— fps".**
- "FPS: no access" — grant rights (section 11), then **sign out of Windows and back in**, then "Check again".
- "No tracing rights even though you're in the group" — click "Check again" or reboot.
- "— fps" — there is no data for this client yet, or tracing failed; check the status under "Ping & FPS" in settings. If it mentions a leftover trace session, follow the instructions there (command `logman stop … -ets` as administrator) or reboot.

**Ping shows "— ms".** The client isn't connected to the server (login screen, character selection, offline) or hasn't sent anything for 60 s. Without tracing rights there's no passive ping — grant rights or enable "Ping by connecting to the server (every 30 s)".

**Alerts don't trigger.**
1. "General" → "EVE logs folder" must say "Found: Gamelogs and Chatlogs are readable.".
2. "EVE client language (for log parsing)" should be "Auto" or your client language. Only Russian and English clients are supported; English is in testing.
3. Alerts are never shown for the active client — test with a client in the background, or press "Test" on the "Alerts" tab.
4. Check that the alert type isn't turned off on "Alerts" or for this character on "Characters", and that "Pause alerts" isn't ticked in the tray.
5. Local and Intel need chat logging in EVE (section 2, step 6).

**"Windows protected your PC".** Expected — EveLens isn't code-signed. Check the file (section 2, step 1), then **More info → Run anyway**.

**EveLens doesn't start / shows an error.** The message says where the log is. If settings got corrupted, EveLens restores them from `settings.json.bak` automatically.

**Where is the EveLens log and what to send in an Issue.** Logs are in `%APPDATA%\EveLens\logs\` (one file per day, `evelens-YYYYMMDD.log`). In an [Issue](https://github.com/evelens-app/evelens/issues) please include:
- EveLens version ("About");
- Windows version, EVE window mode, EVE client language, number of clients and monitors;
- what you did, what you expected, what happened (a screenshot helps);
- the log file for that day. Look through it before sending — it may contain your character names; you can replace them.

## 16. Support and feedback

EveLens is free, and no feature is locked behind a donation. If it makes your fleet life easier, you can say thanks with any amount of ISK to the in-game character **Gridsin** ("About" → "Copy character name").

Ideas, wishes and bug reports: [GitHub Issues](https://github.com/evelens-app/evelens/issues) or EVE Mail to **Gridsin**.

EveLens is an independent project made by a fellow EVE player in spare time. It is provided **"as is"**, without warranty of any kind; use it at your own discretion. EveLens is not affiliated with or endorsed by Fenris Creations or CCP hf.

---

© 2014 CCP hf. All rights reserved. "EVE", "EVE Online", "CCP", and all related logos and images are trademarks or registered trademarks of CCP hf.
