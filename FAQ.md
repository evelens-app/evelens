# GridSight FAQ

Short answers to common questions. Details are in the [user guide](docs/guide-en.md) ([Русский](docs/guide-ru.md) · [Deutsch](docs/guide-de.md) · [中文](docs/guide-zh-Hans.md)).

- [Is it safe?](#is-it-safe)
- [Why is it closed-source?](#why-is-it-closed-source)
- [Why is it unsigned, and why does SmartScreen warn me?](#why-is-it-unsigned-and-why-does-smartscreen-warn-me)
- [Does it need ESI?](#does-it-need-esi)
- [Is it allowed by CCP?](#is-it-allowed-by-ccp)
- [Where is my data stored?](#where-is-my-data-stored)
- [How do I uninstall it and remove all data?](#how-do-i-uninstall-it-and-remove-all-data)
- [How do I disconnect ESI?](#how-do-i-disconnect-esi)
- [My antivirus flags GridSight](#my-antivirus-flags-gridsight)
- [Multiple clients and window modes](#multiple-clients-and-window-modes)

## Is it safe?

We can't give you a guarantee, and no one else has checked GridSight independently yet. What we can do is tell you exactly what it does so you can decide:

- It does not read or write game memory, inject anything into the client, modify game files or send keystrokes or clicks to the game.
- It runs as a normal user and does not need administrator rights. The only UAC prompts are the optional buttons for ping/FPS rights, and only when you press them.
- It has no servers and no telemetry. Every network connection is listed in [NETWORK_CONNECTIONS.md](NETWORK_CONNECTIONS.md); you can check them with any network monitor.
- Download it only from [GitHub Releases](https://github.com/evelens-app/evelens/releases) and check the SHA-256 ([DOWNLOAD_VERIFICATION.md](DOWNLOAD_VERIFICATION.md)).

Limitations (unsigned EXE, closed source, internal review only) are listed openly in [SECURITY.md](SECURITY.md#9-security-limitations).

## Why is it closed-source?

It's the author's choice for this project. The source code is not published, so nobody outside the project can rebuild the EXE and compare it. To make up for that, the behavior is documented in detail — [SECURITY.md](SECURITY.md), [PRIVACY.md](PRIVACY.md), [ESI_PERMISSIONS.md](ESI_PERMISSIONS.md), [NETWORK_CONNECTIONS.md](NETWORK_CONNECTIONS.md) — and much of it (network traffic, files, registry, ESI permissions) can be checked from the outside.

## Why is it unsigned, and why does SmartScreen warn me?

A code-signing certificate is a paid yearly subscription, and this free project doesn't have one. Windows SmartScreen shows **"Windows protected your PC"** for new files without a signature or download history. It does not mean malware was found — it means Windows doesn't know who made the file. Check the SHA-256 first; if it matches, click **More info → Run anyway**. If your organization's policy blocks the file, don't bypass it.

## Does it need ESI?

No. Thumbnails, switching, alerts from game logs, Intel, D-Scan/Local analysis, appraisal, the damage monitor, mining and ping/FPS work without any EVE login. ESI is only needed for the "system · ship" badge, the Dashboard and advisor, account timers and the trade-history sync. See the table in the [README](README.md#why-you-can-use-it-without-esi) and [ESI_PERMISSIONS.md](ESI_PERMISSIONS.md).

## Is it allowed by CCP?

CCP does not certify or approve third-party tools, and GridSight has not been reviewed or approved by CCP or Fenris Creations. GridSight is designed to follow CCP's rules for third-party tools as the developer understands them, including the [CCP developer license](https://developers.eveonline.com/license-agreement): no input broadcasting, no automation, no client modification, no memory reading. One hotkey or click brings one window to the front; everything else is information shown on your screen. Whether a tool is allowed is ultimately CCP's decision — if in doubt, ask CCP support.

## Where is my data stored?

On your PC only:

- `%APPDATA%\GridSight\` — settings, layout, encrypted login tokens, trade history (`history.db`), net worth history (`networth.json`), caches, logs (`logs\`, kept 14 days).
- `%USERPROFILE%\eve-snapshot\` — Dashboard reports and raw ESI data (wallet, assets, location…), **not encrypted**. The 20 most recent dated snapshots per character are kept.

Full list: [PRIVACY.md](PRIVACY.md#7-data-stored-on-your-pc).

## How do I uninstall it and remove all data?

1. Turn off "Start GridSight with Windows" in Settings if you enabled it.
2. Disconnect your characters (next question), then tray → **Exit**.
3. Delete `GridSight.exe`, `%APPDATA%\GridSight` and `%USERPROFILE%\eve-snapshot` (and `%APPDATA%\EveLens` if you used the old name).
4. If you granted ping/FPS rights, remove them (**Revoke ETW rights (UAC)…** in Settings *(beta.2+)*, before deleting the app).

Step-by-step list: [guide, step 10](docs/guide-en.md#step-10-uninstalling) and [PRIVACY.md](PRIVACY.md#8-how-to-delete-your-data).

## How do I disconnect ESI?

- **Badge login:** Settings → "Characters" → **Disconnect ESI**.
- **Dashboard login** *(beta.2+)*: Dashboard window → **Disconnect**. From the command line: `GridSight.Snapshot logout -c "<character>"` or `GridSight.Snapshot logout --all`.

Both delete the token from your PC and ask CCP to revoke it. To be sure, also revoke GridSight on the [EVE Third-Party Applications page](https://community.eveonline.com/support/third-party-applications/).

## My antivirus flags GridSight

New unsigned files are often treated with suspicion, and some things GridSight really does (a single-file EXE that unpacks to `%TEMP%`, optional autostart, Windows performance tracing for FPS, global hotkeys) look like patterns antivirus programs watch for.

1. Check the SHA-256. A mismatch is a real problem — delete the file.
2. With a matching hash, you can report a false positive to your antivirus vendor through its official form, and tell us in [Issues](https://github.com/evelens-app/evelens/issues/new?template=bug_report.yml) which antivirus and what it said.
3. Never turn your antivirus off to run GridSight. If in doubt, don't run it.

More: [DOWNLOAD_VERIFICATION.md](DOWNLOAD_VERIFICATION.md#4-antivirus-warnings).

## Multiple clients and window modes

- Every running EVE client gets its own thumbnail. With five clients GridSight uses about 115–150 MB of RAM.
- Use **Windowed** or **Fixed Window** mode. In exclusive **Fullscreen** GridSight's thumbnails and overlays can't be drawn over the game.
- Thumbnail positions are remembered per character, on any monitor. If a monitor is unplugged, its thumbnails move to the main screen and come back when it's reconnected.
- Hotkeys switch one window per press; GridSight never sends input to clients.
