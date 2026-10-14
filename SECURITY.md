# Security Policy

GridSight is a free, closed-source Windows companion app for EVE Online. This page explains how it interacts with EVE
and Windows, how your EVE login is protected, and how to report a security problem. It describes **GridSight
1.0.0-beta.2**; items marked *(beta.2+)* are not in 1.0.0-beta.1.

No software is perfectly secure. This page lists what GridSight does and does not do, and where its limits are, so you
can decide for yourself. What data GridSight stores and sends, and how to delete it, is in [PRIVACY.md](PRIVACY.md).
Common questions: [FAQ.md](FAQ.md).

## 1. Supported Versions

| Version | Security fixes |
|---|---|
| Latest release (currently 1.0.0-beta.x) | Yes |
| Older releases | No — please update |

Security fixes ship as a new release on [GitHub Releases](https://github.com/evelens-app/evelens/releases). GridSight
never updates itself; it only tells you a new version exists.

## 2. Security Overview

**What GridSight does with EVE**
- Shows live previews of your EVE windows using the Windows Desktop Window Manager (DWM thumbnails). The image is drawn by
  Windows; GridSight does not read the game's pixels or memory.
- Switches to an EVE window when you press one of your hotkeys or click a preview — one action, one window brought to the
  front. Alerts never switch windows on their own.
- Reads the log files EVE writes to `Documents\EVE\logs` (read-only): combat and mining game logs, Local chat and the intel
  channels you choose yourself.
- Uses the official EVE SSO login and the ESI API for features that need your character's data.

**What GridSight does not do**
- It does not read or write EVE client memory, inject code or DLLs, or modify game files.
- It does not send keystrokes or mouse clicks to the game and does not broadcast input between clients.
- It does not automate gameplay.
- It does not download or install updates by itself and does not load plugins or scripts.

**What GridSight does with Windows**
- Runs as a normal user; it does not require administrator rights.
- Uses global hotkeys you configure (`RegisterHotKey`) and watches which window is in front (`SetWinEventHook`).
- Reads the clipboard **only** when you open the clipboard tool (hotkey, tray menu or "Paste" button).
- Optional, off by default:
  - **Start with Windows** — one value `GridSight` under `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`.
  - **Ping and FPS** — Windows performance tracing (ETW). To work without administrator rights it can add your account to
    the built-in Windows group *Performance Log Users*. This happens only when you press **Grant FPS access (UAC)…** and
    confirm the Windows prompt. This right applies to your whole Windows account and stays until you remove it:
    **Revoke ETW rights (UAC)…** in Settings → "General" → "Ping & FPS" *(beta.2+)*, or
    `net localgroup "Performance Log Users" %USERNAME% /delete` in an administrator prompt.
  - **Ping by connecting to the server** — opens an empty TCP connection to the EVE server every 30 s when no passive
    measurement is available. *(beta.2+)* GridSight asks for confirmation before turning it on.
- The Dashboard window *(beta.2+)* uses Microsoft Edge WebView2 to show the dashboard page.

Whether third-party tools are allowed is decided by CCP / Fenris Creations. GridSight follows our reading of the
[CCP Developer License](https://developers.eveonline.com/license-agreement) and the EULA. **It has not been reviewed or
approved by CCP or Fenris Creations.** Having an application registered on the EVE developer portal is not an endorsement.

## 3. EVE Account Security

- Login uses **EVE SSO** in your browser (OAuth 2.0 authorization code with PKCE). GridSight never sees your password.
- The login page returns to `http://localhost:8642/callback` on your own PC; GridSight listens there only while you are
  logging in (up to 5 minutes).
- There are two logins with different permissions — see [ESI_PERMISSIONS.md](ESI_PERMISSIONS.md):
  - **Connect ESI** (Settings): 3 read-only location scopes for the system/ship badge.
  - **Dashboard → Connect character** *(beta.2+)* or `GridSight.Snapshot login`: read access to your character data
    (wallet, assets, skills, industry and more).
- GridSight can change something in your account in exactly one case: creating saved fittings, only if you logged in with
  `GridSight.Snapshot login --fits-write` and then run `--export-fits`. It never deletes fittings.
- You can revoke GridSight's access at any time on the
  [EVE Third-Party Applications page](https://community.eveonline.com/support/third-party-applications/).

## 4. Token Storage

- Only **refresh tokens** are saved, in `%APPDATA%\GridSight\tokens.bin` (Connect ESI) and
  `%APPDATA%\GridSight\snapshot-tokens.bin` (Dashboard / Snapshot). Access tokens are kept in memory only.
- Both files are encrypted with **Windows DPAPI** for your Windows user account. Other Windows users on the PC cannot
  decrypt them; programs running under your own account can.
- Tokens are sent only to CCP: to `login.eveonline.com` to refresh access and to `esi.evetech.net` with each authorized
  request. They are never sent to the author or any third party, and are not written to logs or reports.
- **Disconnect ESI** in Settings → "Characters" deletes the badge token from your PC and *(beta.2+)* asks EVE SSO to
  revoke it.
- *(beta.2+)* **Disconnect** in the Dashboard window deletes the selected character's Dashboard / Snapshot token from your
  PC and revokes it at EVE SSO (after a confirmation). From the command line: `GridSight.Snapshot logout -c "<character>"`
  or `GridSight.Snapshot logout --all`. If EVE SSO can't be reached, the token is still deleted locally and GridSight
  tells you to revoke access on the CCP website.
- To be sure access is revoked on CCP's side, also revoke GridSight on the
  [EVE Third-Party Applications page](https://community.eveonline.com/support/third-party-applications/).
- If you upgraded from EveLens, old copies of the token files in `%APPDATA%\EveLens` are deleted after the move
  *(beta.2+)*; in 1.0.0-beta.1 they may remain — delete that folder.

## 5. Local Data Access

GridSight **reads**: EVE log files (`Documents\EVE\logs`, read-only), your clipboard when you ask it to, the Windows list of
TCP connections and ETW performance events (only if Ping/FPS is enabled), and its own files.

GridSight **writes** only to `%APPDATA%\GridSight`, `%USERPROFILE%\eve-snapshot` (dashboard reports), `%TEMP%` (runtime
files of the single-file EXE; a fallback log folder) and, if enabled, the autostart registry value above.
Details and how to delete everything: [PRIVACY.md](PRIVACY.md).

## 6. Network Connections

GridSight has no servers of its own and sends no telemetry or analytics. It connects to EVE services (SSO, ESI, image
server, static data), zKillboard, Fuzzwork market prices and the GitHub API (update check). The full list, with what is
sent and when: [NETWORK_CONNECTIONS.md](NETWORK_CONNECTIONS.md).

## 7. Reporting Vulnerabilities

Please **do not** post details of a security problem in public Issues.

- Preferred: **GitHub Private Vulnerability Reporting** — "Report a vulnerability" on the
  [Security tab](https://github.com/evelens-app/evelens/security) of this repository.
- Alternative: in-game mail to **Gridsin** asking for a private channel (no technical details in the mail).

Please include the GridSight version, what you found and how to reproduce it. You can expect a reply within about a week.
Fixes for serious issues ship in the next release, and we will credit you in the release notes if you wish.

## 8. Release Verification

Download GridSight **only** from [GitHub Releases](https://github.com/evelens-app/evelens/releases). Each release lists
the SHA-256 of `GridSight.exe`. Check it before the first run:

```powershell
Get-FileHash .\GridSight.exe -Algorithm SHA256
```

The hash must match the one in the release notes exactly. A matching hash proves the file is the one the author published —
it does not by itself prove the file is safe. Step-by-step guide: [DOWNLOAD_VERIFICATION.md](DOWNLOAD_VERIFICATION.md).

## 9. Security Limitations

- **The EXE is not code-signed.** Windows SmartScreen may show "Windows protected your PC", and some antivirus programs may
  flag a new unsigned file. This is expected for unsigned software and does not mean malware was found — but it also means
  Windows cannot confirm who made the file. Verify the SHA-256.
- **The source code is closed.** Nobody outside the project can rebuild the EXE and compare it. This page describes the
  behavior of the code, not a third-party guarantee.
- **No independent audit yet.** The project has had an internal review only.
- **Same-account access.** DPAPI protects tokens from other Windows users, not from malware already running under your
  account.
- **Plain-text reports.** Dashboard reports in `%USERPROFILE%\eve-snapshot` (wallet, assets, location) and the local trade
  history are not encrypted. Do not share these files.
- **Distribution channel.** Release files and their hashes are published in the same place (GitHub). If the publishing
  account were compromised, both could be replaced.
- **Antivirus heuristics.** Some legitimate features (single-file unpacking, autostart, performance tracing, global hotkeys)
  resemble patterns that antivirus programs watch for. GridSight does not try to hide these behaviors.
