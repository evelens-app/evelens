**English** · [Русский](guide-ru.md) · [Deutsch](guide-de.md) · [简体中文](guide-zh-Hans.md)

# GridSight user guide

> This guide describes **GridSight 1.0.0-beta.2**. Features marked *(beta.2+)* are not in 1.0.0-beta.1.

How to install, set up and use GridSight — a free companion app for EVE Online multiboxers on Windows. Button and menu names below are quoted exactly as they appear in the English GridSight interface.

GridSight never sends input to the game, never reads client memory and never modifies game files. It reads the logs EVE writes to disk, uses the official ESI API and a few public EVE community services, and shows information on your screen. The only thing it can change in your EVE account is saved fittings — and only when you explicitly run the command-line export (section 14).

## Contents

1. [Requirements](#1-requirements)
2. [Installation step by step](#2-installation-step-by-step)
3. [Privacy and security](#3-privacy-and-security)
4. [Tray icon and settings window](#4-tray-icon-and-settings-window)
5. [Thumbnails](#5-thumbnails)
6. [EVE logs folder and client language](#6-eve-logs-folder-and-client-language)
7. [Alerts](#7-alerts)
8. [Intel](#8-intel)
9. [D-Scan, Local and appraisal](#9-d-scan-local-and-appraisal)
10. [Damage monitor and Mining](#10-damage-monitor-and-mining)
11. [Ping and FPS](#11-ping-and-fps)
12. [EVE login (ESI)](#12-eve-login-esi)
13. [Dashboard](#13-dashboard)
14. [GridSight.Snapshot for advanced users (command line)](#14-gridsightsnapshot-for-advanced-users-command-line)
15. [Language, updates, autostart](#15-language-updates-autostart)
16. [Troubleshooting (FAQ)](#16-troubleshooting-faq)
17. [Support and feedback](#17-support-and-feedback)

---

## 1. Requirements

- **Windows 10 or 11, 64-bit (x64).** You don't need to install .NET or anything else — GridSight is a single `GridSight.exe` file with the runtime packed inside.
- **EVE in "Windowed" or "Fixed Window" mode.** In exclusive **Fullscreen** the game takes over the screen: GridSight windows (thumbnails, damage overlay, ping/FPS overlay) can't be drawn on top of it. Use Windowed or Fixed Window (borderless).
- **Memory:** about 115–150 MB of RAM with five clients running (Dashboard window closed); CPU load is usually well under 1%.
- **Dashboard window** *(beta.2+)* uses the Microsoft Edge **WebView2 Runtime**. Windows 11 has it; on Windows 10 it sometimes has to be installed — the Dashboard window then shows "Download WebView2 Runtime", and meanwhile you can use "Open in browser".
- **Internet** is needed only for optional features: ESI login and the Dashboard, Intel map and ship classes (a one-time download of CCP static data, about 95 MB), market prices and appraisal, zKillboard and update checks. Thumbnails and alerts work offline.

## 2. Installation step by step

> [!WARNING]
> **GridSight is not code-signed.**
> A code-signing certificate costs about $200–400 per year, which an independent free project can't afford for now. Because of that, Windows cannot tell you who made the file, and SmartScreen shows a blue window when you first start it:
>
> **"Windows protected your PC"**
>
> Windows shows this for new files without a digital signature or download history. It does not mean malware was found. If you downloaded the file from the official Releases page and the SHA-256 matched (step 1), click **More info**, then **Run anyway**.
>
> If you got `GridSight.exe` from anywhere else — don't run it. If your PC is managed by an organization, or Windows or your antivirus blocks the file with no "Run anyway" option, don't try to bypass it.

### Step 1. Download and verify the file

1. Open the Releases page: **https://github.com/evelens-app/evelens/releases** and download `GridSight.exe` from the latest release. Don't download GridSight from other sites, forums, Discord or file shares — even if the name is the same.
2. Your browser may say the file "isn't commonly downloaded". That's normal for a new program: open the download menu ("…") and choose **Keep**.
3. **Check the SHA-256 before the first run.** Open **PowerShell** in the folder with the file and run:
   ```powershell
   Get-FileHash .\GridSight.exe -Algorithm SHA256
   ```
   The `Hash` value must match the SHA-256 in the release notes of the version you downloaded exactly (upper/lower case doesn't matter). If it doesn't — delete the file and download it again from the Releases page. If it still doesn't match, don't run it and report it privately (see [SECURITY.md](../SECURITY.md)).
4. A matching hash proves the file is byte-for-byte the one the author published. It does not by itself prove the file is safe — what GridSight does and its limits are described in [SECURITY.md](../SECURITY.md). Step-by-step guide with extra checks: [DOWNLOAD_VERIFICATION.md](../DOWNLOAD_VERIFICATION.md).

### Step 2. Put GridSight.exe in its own folder

GridSight doesn't need installing — it runs from wherever the file is. Choose a permanent place for it, for example:

```
%LOCALAPPDATA%\Programs\GridSight\
```

(paste this into the Explorer address bar, create the `GridSight` folder and move `GridSight.exe` there), or any folder of your own.

- **Don't** leave it in "Downloads" — it's easy to delete by accident there.
- **Don't** put it into the EVE game folder.
- GridSight writes nothing next to the exe. Settings, layout, logs and other data are stored in `%APPDATA%\GridSight\`; Dashboard reports in `%USERPROFILE%\eve-snapshot\` (full list: [PRIVACY.md](../PRIVACY.md)).
- If you turn on autostart, GridSight remembers the exe path. If you later move the file, turn "Start GridSight with Windows" off and on again.

### Step 3. Remove the "downloaded from the Internet" mark

1. Right-click `GridSight.exe` → **Properties**.
2. On the **General** tab, at the bottom, tick **Unblock** (if there's no such checkbox, the file is already unblocked).
3. Click **OK**.

### Step 4. First start and SmartScreen

Double-click `GridSight.exe`. If the **"Windows protected your PC"** window appears and the hash matched, click **More info** → **Run anyway** (see the warning at the top of this section). Windows usually asks only once per file version.

*(beta.2+)* On the very first start GridSight shows a short welcome window. After you close it, GridSight keeps running in the tray.

### Step 5. If your antivirus complains

Some antivirus programs are suspicious of new unsigned files and of features GridSight really uses (a single-file EXE that unpacks its runtime to `%TEMP%`, optional autostart, Windows performance tracing for FPS, global hotkeys). What to do:

- **Do not turn your antivirus off.**
- Check the SHA-256 first (step 1). A file with a different hash is a real problem — delete it.
- With a matching hash, you can submit the file to your antivirus vendor as a possible false positive using the vendor's official form, and let us know in [Issues](https://github.com/evelens-app/evelens/issues) — which antivirus and what it reported.
- If you're confident it's a false positive, you can add an exclusion **for this one file only**. In Microsoft Defender: **Windows Security** → **Virus & threat protection** → under "Virus & threat protection settings" click **Manage settings** → **Exclusions** → **Add or remove exclusions** → **Add an exclusion** → **File** → choose `GridSight.exe`.
- If in doubt, don't run it.

### Step 6. Check your EVE client settings

1. **Window mode:** in the EVE display settings choose **Windowed** or **Fixed Window** (not Fullscreen).
2. **Chat logging:** Local alerts and Intel read chat logs, so EVE must write chat to files. In the EVE settings (Esc menu), find the chat option **"Log Chat to File"** and make sure it's on. Without it, Local and Intel won't work (thumbnails and combat alerts still will).
3. **Game logs (Gamelogs)** — combat, warp scrambling, cargo and mining messages — are written by EVE automatically. Nothing to turn on.
4. **Logs folder:** by default EVE writes logs to `Documents\EVE\logs` (subfolders `Gamelogs` and `Chatlogs`). If your Documents folder is moved to OneDrive, the path looks like `…\OneDrive\Documents\EVE\logs`. GridSight finds it automatically in both cases (see [section 6](#6-eve-logs-folder-and-client-language)).

### Step 7. What you'll see after the start

- The GridSight icon appears in the system tray, in the bottom-right corner next to the clock. Windows often hides new icons under the **^** arrow. To keep it always visible, drag the icon from the **^** area onto the taskbar, or go to **Settings → Personalization → Taskbar → Other system tray icons** (Windows 11) and switch GridSight on.
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
| Autostart | off | Settings → "General" → "Start GridSight with Windows" |
| Account timers | on (work only after a character is connected in the Dashboard) | Settings → "General" → "Track account timers" |
| Background trade-history sync *(beta.2+)* | on (together with account timers) | Settings → "General" → "Account timers" — a separate switch (section 13) |

### Step 9. Updating

1. Download the new `GridSight.exe` from the Releases page and check its SHA-256 (step 1).
2. Close GridSight: right-click the tray icon → **Exit**.
3. Replace the old `GridSight.exe` with the new one in the same folder; unblock it (step 3).
4. Start it. Settings, thumbnail positions, connected characters and trade history are kept — they live in `%APPDATA%\GridSight\`.

### Step 10. Uninstalling

1. If autostart is on, untick "Start GridSight with Windows" first — or later delete the `GridSight` value under `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run` in the Registry Editor.
2. Optional: disconnect your characters — "Disconnect ESI" on the "Characters" tab and the disconnect button in the Dashboard window *(beta.2+)* (sections 12–13).
3. Tray icon → **Exit**.
4. Delete `GridSight.exe` (and `GridSight.Snapshot.exe`, if you used it).
5. Delete the `%APPDATA%\GridSight` folder: settings, layout, login tokens (`tokens.bin`, `snapshot-tokens.bin`), trade history (`history.db`), the Dashboard's WebView2 profile (`webview2\`), logs and caches.
6. Delete `%USERPROFILE%\eve-snapshot` — Dashboard reports and raw ESI data (wallet, assets, location and more, **not encrypted**).
7. If you used EveLens (the old name) before, also delete `%APPDATA%\EveLens` — it may still contain old copies of the login tokens.
8. Optional: delete `%TEMP%\GridSight-logs` (a fallback log folder).
9. If you granted FPS rights (section 11), remove yourself from the group: open **Command Prompt as administrator** and run `net localgroup "Performance Log Users" %USERNAME% /delete` (on a non-English Windows the group name is translated — GridSight shows the exact command under the "Grant FPS access (UAC)…" button). Then sign out of Windows and back in.
10. If you connected characters via ESI, revoke access on the CCP site: https://community.eveonline.com/support/third-party-applications/. Deleting local files alone does not revoke access.

The same list with explanations is in [PRIVACY.md](../PRIVACY.md), section 8.

## 3. Privacy and security

**No GridSight servers, no telemetry, no analytics.** GridSight has no servers or accounts of its own and nothing is ever sent to the author. EVE game and chat logs are read only on your computer and are never uploaded anywhere.

**What GridSight reads on your PC:** the log files EVE writes to disk (read-only; only game logs, Local and the intel channels you choose yourself), your clipboard only when you open the clipboard tool, and Windows performance data (ETW) for ping/FPS only if you enable it. It never reads game memory and never sends input to the game.

**Network.** GridSight connects to official EVE services (SSO login, ESI API, image server, static data), zKillboard, Fuzzwork market prices and the GitHub API for the update check. Without any action from you it may: check GitHub for updates once a day (if enabled), refresh the ESI badge about every 30 s for connected characters, check account timers every 10 minutes and sync your trade history about once an hour *(beta.2+)*, and download EVE static data at most once a week. Everything else happens only when you use the feature. The full list — what is sent where, when, and how to turn it off — is in [NETWORK_CONNECTIONS.md](../NETWORK_CONNECTIONS.md).

**What is stored on your PC:** settings, encrypted login tokens, your trade history *(beta.2+)*, caches of public data, logs, and Dashboard reports in `%USERPROFILE%\eve-snapshot`. The reports and the trade history are **not encrypted** — don't share these files or screenshots of the Dashboard unless you're comfortable showing that information. Details and how to delete everything: [PRIVACY.md](../PRIVACY.md).

**Login tokens** are stored only on this PC, encrypted with Windows DPAPI for your Windows account — another Windows user can't decrypt them (programs running under your own account can). They are sent only to CCP's own servers: to `login.eveonline.com` to refresh access and to `esi.evetech.net` with each authorized request — never to the author or any third party. GridSight never sees your EVE password: you log in on the official EVE website. Which permissions are requested and why: [ESI_PERMISSIONS.md](../ESI_PERMISSIONS.md).

**CCP's rules.** GridSight uses its own application registration on the EVE developer portal and is designed to follow our reading of the [CCP developer license](https://developers.eveonline.com/license-agreement) and the EULA. It has **not** been reviewed or approved by CCP or Fenris Creations; a registration on the developer portal is not an endorsement. EVE Online is developed by Fenris Creations (named CCP Games until May 2026); the license is granted by CCP hf. GridSight is not affiliated with Fenris Creations or CCP.

**Limits.** The EXE is not code-signed, the source code is closed, and there has been no independent audit yet. What GridSight does with EVE and Windows, its limitations and how to report a security problem privately: [SECURITY.md](../SECURITY.md).

**Revoking access:** at any time on the third-party applications page: https://community.eveonline.com/support/third-party-applications/

## 4. Tray icon and settings window

**Opening settings:** double-click the tray icon, or right-click → "Settings…".

**Tray menu** (right-click), top to bottom:

- "Version X available…" — only when a new version is out; opens the release page.
- "Timers" — account timers (section 13), visible when timers are on.
- "Dashboard" *(beta.2+)* — the Dashboard window (section 13).
- "Parse clipboard (D-Scan / Local / appraisal)" — section 9.
- "Mining" — section 10.
- "Damage monitor" — toggles the damage overlay.
- "Edit mode" — move and resize thumbnails.
- "Settings…"
- "Reconnect ESI…" — appears only if a character's ESI access has expired or was revoked.
- "Ping/FPS: thumbnails", "Ping/FPS: main window" — section 11.
- "Pause alerts" — temporarily stops new alerts.
- "Язык / Language" — interface language.
- "User guide" — opens this guide.
- "About" — version, links, update check, support.
- "Exit"

**Settings tabs:**

| Tab | What's there |
|---|---|
| "Characters" | Every character GridSight has seen: online status, group, per-character alerts, "Connect ESI" button. |
| "Groups & hotkeys" | Groups of characters and hotkeys to cycle between them. |
| "Alerts" | Which alerts are on, "Test" buttons, Local and Intel settings. |
| "Damage" | Damage monitor. |
| "General" | Language, EVE logs folder, thumbnails, edit mode hotkey, clipboard parser, mining, Dashboard hotkey, zKillboard contact, ping & FPS, startup and updates, account timers, ESI Client ID. |

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

If a combination is already taken by another program or another GridSight hotkey, GridSight shows it in red — choose another one.

## 6. EVE logs folder and client language

**Auto-detection.** GridSight looks for logs in `Documents\EVE\logs`, using the real location of your Documents folder — including when Windows has moved it to OneDrive (`…\OneDrive\Documents\EVE\logs`). If the folder doesn't exist yet (EVE has never been started), GridSight waits and picks it up as soon as it appears.

**Check:** "General" → "EVE logs folder". Under the path:

- "Found: Gamelogs and Chatlogs are readable." — all good;
- "Gamelogs folder not found — alerts won't work. …" — specify the folder manually.

**Setting it manually:** click "Browse…" and choose the `logs` folder inside `EVE` (the one containing `Gamelogs` and `Chatlogs`), or paste the path into the field.

**EVE client language for log parsing.** Alerts, damage, mining and Local are recognized from the text of game log lines, so GridSight needs to know your client language. This is separate from the GridSight interface language. "General" → "Language" → "EVE client language (for log parsing)":

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

GridSight can read your intel channels and highlight the character who is near a reported system.

1. Make sure chat logging is on in EVE (section 2, step 6).
2. "Alerts" → "Intel" → tick **"Watch intel channels"**.
3. In "Channels" enter the channel names, one per line, exactly as at the start of the chat log file name (files look like `<Channel>_YYYYMMDD_HHMMSS_….txt` in `Chatlogs`). Case doesn't matter.
4. Set "Radius:" — 1 to 15 jumps (default 5).

On first use GridSight downloads the CCP static data (about 95 MB) to build the stargate map; the status is shown under the slider ("Map loaded: … systems with gates.").

**How it works:** if a message in the channel names a system within the radius of a character's current system (counted by gates), that character's thumbnail glows purple and its strip shows `Intel: <system> · <N> j` (the nearest one). The character's system is taken from Local or ESI; until it's known, Intel isn't evaluated for that character.

**Clearing:** a message with **`clr`** or **`clear`** (also the Russian `чисто`) clears the alert for the systems named in the same message, e.g. `Perimeter clr`. Switching to the client clears it too.

Limitations: abbreviations and suffixes ("1DQ", "Urlen-gate") aren't recognized; system names that are ordinary words (`Bar`, `Exit`, `Pain`, `Dead End`…) are only caught when written with a capital letter as in the game. System names must be written in Latin letters. Wormhole systems are ignored.

## 9. D-Scan, Local and appraisal

GridSight reads text from the clipboard only when you open this window — nothing is sent to the game.

**How to copy in the game:**

- **D-Scan:** in the scanner window click the results list, press `Ctrl+A`, then `Ctrl+C`.
- **Local:** in the chat window select the members (click the first, Shift+click the last, or `Ctrl+A`), then `Ctrl+C`.
- **Items for appraisal** *(beta.2+)*: select items in an inventory window (cargo, hangar, container), press `Ctrl+A` if needed, then `Ctrl+C`.

**How to open the analysis:** tray → "Parse clipboard (D-Scan / Local / appraisal)", or your own hotkey: "General" → "Clipboard parser (D-Scan / Local / appraisal)" → "Open parser window" (not set by default). The window detects the format by itself; the "D-Scan" / "Local" / "Appraisal" buttons force a mode for the current text. After copying something new, click "Paste again" or press the hotkey again.

**D-Scan result:** number of ships and other objects; ships by class and type; an "Attention" block for dangerous ships (interdictors/HICs, mobile bubbles, combat probes, interceptors, recons, bombers, Black Ops, logistics, capitals, supers). "On grid only (≤ 10,000 km)" hides far objects.

**Local result:** pilots grouped by alliance and corporation, biggest first (names are resolved through the public ESI API — the pasted names are sent to ESI). Corporations and alliances of your connected characters are marked "own" in green. "Check on zKill" (only on click) looks up kills/losses for up to 20 non-friendly pilots from the largest groups; a pilot's name opens their zKillboard page.

**Appraisal result** *(beta.2+)*: "Buy total", "Sell total", "Volume (packaged)" and the number of items, then a table per item with buy and sell prices and a hint — "sell to buy orders" or "place a sell order". Choose the trade hub in "Hub" (Jita, Amarr, Dodixie, Rens, Hek). Prices are Fuzzwork aggregates for the hub station (5% of the order book from the best side), refreshed hourly; to get them, GridSight sends Fuzzwork the hub and the list of item type IDs. Lines that couldn't be matched to an item are listed under "Not recognized". "Copy summary" puts a short summary (hub, totals, volume, items) into the clipboard. The first appraisal loads CCP static data (SDE) and can take a couple of minutes.

Tip: in "General" → "zKillboard contact" you can enter an optional contact (email, in-game name or Discord) — zKillboard asks that tools identify themselves. The contact is sent to zKillboard in the request header; leave the field empty if you don't want zKillboard to see it.

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
- A new session starts after a pause longer than N minutes ("New session after a pause longer than", default 10). If GridSight is started mid-session, it picks up the last 6 hours from the logs.
- ISK is calculated at Jita 4-4 buy orders, before taxes. "Value as compressed" — use compressed ore prices where available.

**Hold:** EVE doesn't write hold capacity to the logs — enter it in the character card ("Hold, m³"). Then you'll see the fill and "full in ≈ mm:ss". After unloading, click **"Unloaded"** — the fill is counted again from this minute. "Highlight thumbnail when hold ≈ 95%" lights the yellow "Ship" alert based on this estimate (once per fill, no sound).

## 11. Ping and FPS

**Where to turn on:** "General" → "Ping & FPS" (off by default), or in the tray:

- "Ping/FPS: thumbnails" / "Show on thumbnails" — `62 fps · 38 ms` on the right of each thumbnail strip (the Intel text has priority while it's lit);
- "Ping/FPS: main window" / "Show over the main window (EVE client in focus)" — a small overlay in a corner of the active EVE window; the corner is set in "Main window corner" (default "Top right"). Not visible in exclusive Fullscreen.

Measurements come from Windows system tracing (ETW, the same way PresentMon works). Nothing is injected into the client and, by default, GridSight doesn't connect to CCP servers.

**FPS rights.** Windows tracing requires either running GridSight as administrator or membership in the **"Performance Log Users"** group. Without it, thumbnails show `FPS: no access`, and the settings show the button **"Grant FPS access (UAC)…"**:

1. Click "Grant FPS access (UAC)…" and confirm the Windows UAC prompt. GridSight runs a single command: `net localgroup "<group>" "<you>" /add`.
2. **Sign out of Windows and sign in again** (or reboot) — the right only takes effect after a new sign-in.
3. Start GridSight and click "Check again" if needed. The status should say "Tracing is running: …".

> [!IMPORTANT]
> This is a right for your **whole Windows user account**, not just for GridSight: any program running as you will be able to trace Windows performance. It stays until you remove it — turning off Ping & FPS or uninstalling GridSight does not remove it. To revoke it: *(beta.2+)* use the button for revoking FPS access in "General" → "Ping & FPS" (it asks for UAC again), or run as administrator the command shown in the settings, `net localgroup "<group>" "<you>" /delete`. Then sign in again.

**Ping:** GridSight passively reads the smoothed round-trip time that Windows itself measures for the client's connection to the EVE server (port 26000). `— ms` means there is no connection (login screen, offline) or the client has been silent for more than 60 s.

**"Ping by connecting to the server (every 30 s)"** — off by default. It's a fallback for when passive measurement isn't available (no tracing rights): GridSight opens an empty TCP connection to the CCP server, times the handshake and closes it. No data is sent, but these are extra connections to CCP's server, so we keep it off unless you need it.

## 12. EVE login (ESI)

ESI login is optional: thumbnails, alerts, D-Scan/Local analysis, damage, mining and ping/FPS never need it. There are **two separate logins** with different permissions; you can use either, both or none.

| Login | Where | Permissions | What it gives |
|---|---|---|---|
| **Connect ESI** | Settings → "Characters" | 3 read-only scopes: current location, ship and online status | "system · ship" badge on the thumbnail; current system for Intel |
| **Connect character** *(beta.2+)* | Dashboard window (section 13), or `GridSight.Snapshot login` (section 14) | read access to your character data: wallet, assets, skills, industry, market orders, contracts, planets, clones, standings, fittings and more | Dashboard, advisor, account timers, profit |

The full list of permissions, what each is used for and what happens without it: [ESI_PERMISSIONS.md](../ESI_PERMISSIONS.md). EVE SSO asks you to approve all permissions of a login at once — you can't pick individual ones. If you don't want the Dashboard's broad read access, simply don't use that login; the rest of GridSight keeps working. All permissions are read-only, except an optional one to create saved fittings, which is only requested from the command line (`login --fits-write`, section 14).

**How to connect a character for the badge:**

1. "Characters" tab → **"Connect ESI"** next to the character.
2. Your browser opens the official EVE login page (login.eveonline.com). Log in and **choose the same character**, then authorize.
3. The browser returns to GridSight, and the status changes to "ESI connected". If you chose another character in the browser, GridSight connects that one and tells you.

The badge updates about every 30 s; "offline" when the character has logged off.

GridSight uses its own built-in ESI application, so the "EVE Developers application Client ID" field in "General" **can be left empty**. Fill it in only if you want to use your own application.

**Security:** GridSight never sees your password — login goes through EVE SSO; the login page returns to `http://localhost:8642/callback` on your own PC, and GridSight listens there only while you are logging in. Tokens are stored only on this PC, encrypted with Windows DPAPI under your Windows account (`%APPDATA%\GridSight\tokens.bin` for the badge, `snapshot-tokens.bin` for the Dashboard), and are sent only to CCP's servers (see section 3).

**Disconnecting and revoking access:**

- "Disconnect ESI" next to the character removes the badge token from your PC.
- *(beta.2+)* The Dashboard window has a button to disconnect the selected character: it deletes the character's token from your PC and revokes it at CCP. From the command line: `GridSight.Snapshot logout -c "<character>"`.
- To be sure access is revoked, use the CCP page: https://community.eveonline.com/support/third-party-applications/ — this invalidates the tokens on CCP's side even if copies remain on your disk.

If access stops working, the tray shows "Reconnect ESI…" and the character's button changes to "Log in again".

## 13. Dashboard

*(beta.2+)* The **Dashboard** is a window inside GridSight with your character's data from ESI and the advisor. In 1.0.0-beta.1 this needed the separate `GridSight.Snapshot.exe`; now it's built in.

**Opening:** tray → "Dashboard", or your own hotkey: "General" → "Dashboard" → "Open the Dashboard" (not set by default). Clicking an entry in tray → "Timers" also opens the Dashboard.

**First start:**

1. Click **"Connect character"**. Your browser opens the official EVE login page — log in, choose the character and authorize (permissions: section 12).
2. Click **"Take first snapshot"**. The first snapshot takes a couple of minutes: game static data and market prices are downloaded.
3. Connect more characters the same way and switch between them in the list at the top of the window.

**Buttons at the top:** "Refresh" — take a new snapshot of the selected character; "Connect character"; "Open in browser" — open the same report in your default browser; a button to disconnect the selected character (section 12). The time of the snapshot is shown next to them.

**What's inside:** key figures, "To do" (a summary of advice from all sections), "Wallet", "Assets" with ISK estimate, "Skills", "Market" (orders and contracts), "Trade", "Industry", "Production", "PI", "PI → P2", "Mining", "Reprocessing", "Clones", "LP & standings", "Abyssal fits", "Fits" and "Profit". The advisor:

- **Production** — profit from your blueprints at Jita prices;
- **Reprocessing and mining** — sell raw, compress or reprocess;
- **PI → P2** — factory vs selling P1;
- **Trade** — selling assets, a station-trading scanner and watching your orders, for 5 trade hubs;
- **Abyssal fits** — popular fits from zKillboard checked against your skills and assets, with a Jita multibuy list;
- **To do** — a summary of advice from all sections.

**Filters and search.** Tables with a search field also have drop-down filters by column, "Ranges" with from–to values (you can type amounts like `300k` or `1.5m`), a "N of M" counter and "Reset filters". Filters, sorting and the chosen hub are remembered. **`Ctrl+K`** or **`/`** (or the "Search" button) opens a search across the whole snapshot — items, skills, locations: type at least 2 letters, pick with ↑↓, Enter jumps to the row, Esc closes.

**Trade hubs.** The "Trade" section is calculated for Jita, Amarr, Dodixie, Rens and Hek; switch the hub with the "Hub" selector. Broker fees take your standings into account. "To do" and the other sections use Jita.

**Market movers.** Each hub in "Trade" has a "Market movers" card with three lists: "Rising" and "Falling" (7-day average vs 30-day average) and "Price spikes" (last day vs the monthly median). It's not the whole market — only items the snapshot already knows (scanner candidates and your stacks for sale).

**Item card.** Click an item name anywhere in the Dashboard. The card loads live ESI data for 5 hubs: best sell and buy, margin after tax and broker fee, daily volume, number of orders and jumps from your current location. Click a hub for the 90-day price history, the "Margin calculator" and the station order books with "Your order" marked. The card also shows signals from the price history (rising, falling, spike, historically cheap or expensive, low supply…) and a short verdict, e.g. "Good time to buy", "Hub arbitrage" or "Where to sell" for items you have. These are hints from ESI history and orders, not a guarantee — check the order book before trading.

**Profit.** The "Profit" section calculates real profit from your trades: FIFO across all your connected characters, sales tax from the wallet journal, broker fees for the period, production cost from blueprint materials; periods, a daily chart and the top items. "No cost basis" lists sales without a purchase in history (loot, mining, LP, contracts or purchases before the history began) — they're not counted in profit. "Bought, not sold yet" is what's left in the FIFO queue. ESI keeps transactions for only about 30 days, so GridSight accumulates them in a local database, `%APPDATA%\GridSight\history.db`, with every snapshot and in the background (see below).

**Price list.** In the Dashboard window you can correct the profit calculation: "Set cost" for items under "No cost basis" (for one batch or "for all future sales"), and "Personal use" for items you bought for yourself — they leave the FIFO queue and aren't counted as sales. Entries can be edited or deleted; GridSight saves them to `history.db` and refreshes the snapshot. These buttons only work inside the Dashboard window, not in a browser.

**Account timers in the tray.** Once a character is connected in the Dashboard, GridSight checks every 10 minutes for PI extractors, free industry slots and the skill queue. A dot appears on the tray icon when something needs attention; the list is in tray → "Timers". On the same cycle, about once an hour per character, GridSight also syncs your wallet transactions, wallet journal and industry jobs into `history.db` for the "Profit" section. "General" → "Track account timers" turns timers off; *(beta.2+)* a separate switch in the same block turns off the background trade-history sync.

**Network and files.** The Dashboard page opens without network by itself. When you open an item card, the page requests live market data from the public ESI and icons from `images.evetech.net`; no login data is sent, but the jump-count lookup tells CCP your current solar system. Reports are saved to `%USERPROFILE%\eve-snapshot\`: `latest-<character>.html`, dated copies `<character>-<date>.html` and `.md`, and raw ESI responses in `raw\`. They contain your wallet, assets, orders, location and more and are **not encrypted** — don't share them. Details: [PRIVACY.md](../PRIVACY.md), [NETWORK_CONNECTIONS.md](../NETWORK_CONNECTIONS.md).

## 14. GridSight.Snapshot for advanced users (command line)

`GridSight.Snapshot.exe` is a separate console program that takes the same snapshot as the Dashboard and writes the same reports. You don't need it for the Dashboard; it's for scripts, a different report language, the abyssal-fit export and fine-tuning the advisor. It uses the same tokens (`snapshot-tokens.bin`) as the Dashboard.

**Commands** (run in a terminal in the folder with `GridSight.Snapshot.exe`; prefix with `.\` in PowerShell):

| Command | What it does |
|---|---|
| `GridSight.Snapshot login` | EVE login in the browser (read-only permissions, same as "Connect character"); once per character |
| `GridSight.Snapshot login --fits-write` | Same, plus permission to create saved fittings (needed only for `--export-fits`) |
| `GridSight.Snapshot logout -c "<character>"` | *(beta.2+)* Delete the character's token from your PC and revoke it at CCP |
| `GridSight.Snapshot` | Snapshot of all connected characters |
| `GridSight.Snapshot -c "<character>"` | Snapshot of one character |
| `GridSight.Snapshot -c "<character>" --export-fits <hull\|all> [--top N]` | Write the top N (1–3) abyssal fits for the hull into the game's saved fittings as `GridSight <Hull> #N` |
| `GridSight.Snapshot --keep N` | *(beta.2+)* Keep only the N most recent dated copies of the reports |
| `GridSight.Snapshot --lang en` | Report language: `en`, `ru`, `de`, `zh-Hans` (default — the GridSight interface language, otherwise Windows) |
| `GridSight.Snapshot --help` | Full list of options (`--no-open`, `--no-market`, `--no-fits`, `--hubs` and others) |

**Writing to your account.** `--export-fits` is the only thing in GridSight that changes your EVE account: it **creates** saved fittings named `GridSight …` and never edits or deletes existing ones. It works only after `login --fits-write`.

**Where the files are:** `%USERPROFILE%\eve-snapshot\` — `latest-<character>.html` (opens in your browser after each snapshot; `--no-open` to skip), dated copies `<character>-<date>.html` plus `.md`, and `raw\`. The HTML file opens offline; the item card loads live data from the public ESI when you click an item (section 13).

## 15. Language, updates, autostart

**Interface language:** "General" → "Language" → "Interface language": "Auto (Windows language)", English, Русский, Deutsch, 简体中文 (also tray → "Язык / Language"). Applies immediately. It doesn't depend on the EVE client language (section 6). Names of items from CCP data are shown in English in all interfaces except Russian.

**Updates:** "Check for updates (daily, GitHub)" is on by default. Once a day GridSight asks GitHub whether a new version exists. If yes — a tray menu item "Version X available…", one pop-up notification and a line in "About". **GridSight never downloads or installs anything by itself** — update manually (section 2, step 9). "Offer beta versions" — also notify about betas. You can check manually in "About" → "Check for updates".

**Autostart:** "General" → "Startup" → "Start GridSight with Windows". It adds GridSight to your user's startup list (registry `HKCU\…\Run`); unticking removes it.

## 16. Troubleshooting (FAQ)

**No thumbnails.**
- Is EVE running in Windowed or Fixed Window mode (not Fullscreen)?
- Is "Hide all thumbnails when EVE isn't in the foreground" on? Then thumbnails are hidden while another program is active.
- Is "Hide the active client's thumbnail" on? With one client, its thumbnail is hidden while it's active.
- Is GridSight running at all (icon in the tray, maybe under **^**)?

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

**The Dashboard window is empty or says "WebView2 Runtime required".** Install the runtime with "Download WebView2 Runtime", or use "Open in browser" meanwhile.

**"Windows protected your PC".** Expected — GridSight isn't code-signed. Check the SHA-256 (section 2, step 1), then **More info → Run anyway**.

**GridSight doesn't start / shows an error.** The message says where the log is. If settings got corrupted, GridSight restores them from `settings.json.bak` automatically.

**Where is the GridSight log and what to send in an Issue.** Logs are in `%APPDATA%\GridSight\logs\` (one file per day, `gridsight-YYYYMMDD.log`; fallback folder — `%TEMP%\GridSight-logs`). Logs contain character names, but no tokens. In an [Issue](https://github.com/evelens-app/evelens/issues) please include:
- GridSight version ("About");
- Windows version, EVE window mode, EVE client language, number of clients and monitors;
- what you did, what you expected, what happened (a screenshot helps — but don't post Dashboard screenshots with your wallet or assets);
- the log file for that day. Look through it before sending — it may contain your character names; you can replace them.

Security problems — please report privately, not in Issues: [SECURITY.md](../SECURITY.md).

## 17. Support and feedback

GridSight is free, and no feature is locked behind a donation. If it makes your fleet life easier, you can say thanks with any amount of ISK to the in-game character **Gridsin** ("About" → "Copy character name").

Ideas, wishes and bug reports: [GitHub Issues](https://github.com/evelens-app/evelens/issues) or EVE Mail to **Gridsin**.

GridSight is an independent project made by a fellow EVE player in spare time. It is provided **"as is"**, without warranty of any kind; use it at your own discretion. GridSight is not affiliated with or endorsed by Fenris Creations or CCP hf.

---

© 2014 CCP hf. All rights reserved. "EVE", "EVE Online", "CCP", and all related logos and images are trademarks or registered trademarks of CCP hf.

---

**Made by Gridsin** · *May the light of the Gate guide you, capsuleer.*
