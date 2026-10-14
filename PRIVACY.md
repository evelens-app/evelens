# Privacy Policy

**Short version:** GridSight runs on your PC. It has no servers, no accounts of its own, no telemetry and no analytics — the
author receives nothing from you. Some features do talk to EVE services and a few public EVE community services; this page
says exactly which, what is sent, what is stored on your PC and how to delete it.

This policy describes GridSight 1.0.0-beta.2. Items marked *(beta.2+)* are not in 1.0.0-beta.1.

## 1. What data GridSight works with

| Data | Where it comes from | Used for |
|---|---|---|
| EVE window titles (character names) | Windows | Thumbnails, layouts, hotkeys |
| EVE game logs (combat, mining) | `Documents\EVE\logs\Gamelogs` | Alerts, damage, mining |
| Local chat and the intel channels **you choose** | `Documents\EVE\logs\Chatlogs` | Local alerts, hostile-near-you alerts |
| Clipboard text | Only when you open the clipboard tool | D-Scan / Local analysis, item appraisal |
| Ping and FPS of EVE clients | Windows performance tracing (only if enabled) | Ping/FPS display |
| Your character's data from ESI | EVE servers, only after you log in | Badge, dashboard, advisor, timers, profit; *(beta.2+)* your open market orders for the orders watch |

GridSight does not read other chats (private conversations, corp or alliance chat) unless you add them as intel channels
yourself. It never reads game memory.

## 2. What is processed only on your PC

Everything above is processed locally. Chat and game logs are never uploaded anywhere. Character names from Local are sent
to EVE servers only when you run Local analysis (see §3).

## 3. Data sent to official EVE services (CCP)

| Service | When | What is sent |
|---|---|---|
| EVE SSO (`login.eveonline.com`) | When you log in, and to refresh access | Login data handled by CCP; GridSight never sees your password |
| ESI (`esi.evetech.net`) with your login | Badge (~every 30 s while on), timers (every 10 min), watching your open market orders *(beta.2+, every 10 min with the timers)*, dashboard snapshots, trade-history sync *(beta.2+, about hourly while "Track account timers" and "Collect trade history (hourly)" are on)* | Your access token and character ID |
| ESI without login | Local/D-Scan analysis, market data, item card *(beta.2+)*; every 10 min with the timers *(beta.2+)*: public market books for your orders (orders watch) and for items with a price alert | Names of pilots you pasted (Local), item IDs, and — in the item card — your current solar system for jump counts; for the market books — region ID and item type IDs, no login |
| Image server (`images.evetech.net`) | Dashboard icons | Item / character / corporation IDs |
| Static data (`developers.eveonline.com`) | At most once a week, for features that need it | Nothing personal |

## 4. Data sent to third-party services

| Service | When | What is sent |
|---|---|---|
| zKillboard (`zkillboard.com`) | "Check on zKill" in Local analysis (button); abyssal fits in the dashboard | Character IDs of pilots you check; ship type IDs; the **zKillboard contact**, only if you entered one in Settings (it is part of the request header — leave it empty if you don't want zKillboard to see it) |
| Fuzzwork (`market.fuzzwork.co.uk`) | Mining window prices; clipboard appraisal *(beta.2+)*; dashboard trade and industry analysis | Trade hub station and a list of item type IDs (from your assets and fits) |
| GitHub (`api.github.com`) | Update check once a day (can be turned off) | Nothing personal |
| Microsoft Edge WebView2 *(beta.2+)* | Dashboard window | GridSight does not send data through it; WebView2 is a Microsoft component with its own behavior |

Like any website, these services see your IP address. Every request carries a User-Agent with the GridSight version and
the project address (`GridSight/<version> (+github.com/evelens-app/evelens)`). It contains no contact of the author or of
you; only requests to zKillboard add your own zKillboard contact, and only if you entered one *(beta.2+)*.

## 5. Automatic network requests

Without any action from you, GridSight may: check GitHub for updates (daily, if enabled); refresh the ESI badge (if
connected); poll account timers every 10 minutes (if "Track account timers" is on and a character is connected to the dashboard)
and, on the same cycle, read your open market orders and the public market books for them, and check your price alerts *(beta.2+)*; sync trade history about once an hour *(beta.2+)* (if, in addition, "Collect trade history (hourly)" is on — a
separate switch under "Account timers", on by default); download EVE static data (at most weekly). Watching your orders is a separate switch too: uncheck "Watch my market orders (outbid, expiring)" under "Account timers" (on by default; GridSight only reads your orders and never changes them). Price alerts are checked only if you have set any (item card in the Dashboard window) and stop when you remove them in the item card or turn off "Track account timers". Everything else
happens only when you use the feature.

## 6. Analytics and telemetry

None. No usage statistics, crash reports, advertising IDs or tracking of any kind. There are no developer servers.

## 7. Data stored on your PC

| Location | Contents | Kept |
|---|---|---|
| `%APPDATA%\GridSight\tokens.bin`, `snapshot-tokens.bin` | EVE login (refresh) tokens, encrypted with Windows DPAPI | Until you disconnect / delete |
| `%APPDATA%\GridSight\history.db` *(beta.2+)* | Your wallet transactions, wallet journal, industry jobs, blueprint ME, manual cost entries. Filled with every dashboard snapshot and, if "Collect trade history (hourly)" is on, by the hourly sync | Indefinitely, grows over time |
| `%APPDATA%\GridSight\price-alerts.json` *(beta.2+)* | Your price alerts: item, hub, side (sell/buy) and the price you set; up to 50 | Until you remove the alerts or delete the file |
| `%APPDATA%\GridSight\networth.json` *(beta.2+)* | Net worth history for the "Net worth" strip: one point per hour per character (total, wallet, assets, sell and buy orders), written with every dashboard snapshot. Local only, **not encrypted** | 400 days; delete the file to clear it |
| `%APPDATA%\GridSight\*.json` | Settings (incl. zKillboard contact), layout, mining stats, timers state | Until deleted |
| `%APPDATA%\GridSight\backup-<date-time>` and `import-pending` *(beta.2+)* | Created by "Move to another PC" → "Import settings…": `import-pending` holds the checked files until the next start; `backup-<date-time>` holds copies of the previous settings, layout, timers, mining and price-alert files that the import replaced | Until you delete them |
| `%APPDATA%\GridSight\sde`, `market`, `img`, `zkill` | Caches of public data | Refreshed automatically; zKillboard cache kept |
| `%APPDATA%\GridSight\webview2` *(beta.2+)* | WebView2 profile (dashboard view settings) | Until deleted |
| `%APPDATA%\GridSight\logs` (and `%TEMP%\GridSight-logs`) | Diagnostic logs with character names, no tokens | 14 days *(beta.2+)*: older `gridsight-*.log` files are deleted when GridSight starts |
| `%USERPROFILE%\eve-snapshot` | Dashboard reports and raw ESI data: wallet, assets, orders, contracts, clones, implants, standings, location, fits — **not encrypted** | *(beta.2+)* The 20 most recent dated snapshots per character (`.md`, `.html`, `raw\*.json`); older ones are deleted after each new snapshot. `latest-<character>.html` is always kept. Change with `GridSight.Snapshot --keep N` (`0` keeps everything). In 1.0.0-beta.1 every snapshot is kept until you delete it |
| Registry `HKCU\…\Run\GridSight` | Autostart path | Only while "Start with Windows" is on |

**Settings export** *(beta.2+)*. "Settings → General → Move to another PC → Export settings…" writes a .zip that you save where you choose. It contains only `settings.json` (including the zKillboard contact, if you entered one), `layout.json`, `timers.json`, `mining.json` and `price-alerts.json`. ESI tokens (`*.bin`), the trade history (`history.db`), the net worth history, logs and caches are never included. Nothing is sent anywhere; treat the archive like any file with your settings and share it with care. "Import settings…" accepts only those file names (each up to 2 MB, each a JSON object).

Do not share the `eve-snapshot` files or screenshots of the dashboard unless you are comfortable showing that information.

## 8. How to delete your data

1. Disconnect your characters: Settings → "Characters" → **Disconnect ESI**, and *(beta.2+)* **Disconnect** in the
   Dashboard window (or `GridSight.Snapshot logout --all`). This deletes the tokens and asks EVE SSO to revoke them.
2. If you enabled autostart, turn off "Start GridSight with Windows" in Settings (or later delete `GridSight` under
   `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`).
3. If you granted FPS access: *(beta.2+)* **Revoke ETW rights (UAC)…** in Settings → "General" → "Ping & FPS", or
   `net localgroup "Performance Log Users" %USERNAME% /delete` in an administrator prompt.
4. Quit GridSight (tray → Exit).
5. Delete `%APPDATA%\GridSight` (this also removes `networth.json`, `backup-*` and `import-pending`) and `%USERPROFILE%\eve-snapshot`. To clear only the net worth history, delete `%APPDATA%\GridSight\networth.json` while GridSight is not running; also delete any settings archive you exported. If you used EveLens before, also delete `%APPDATA%\EveLens`.
6. Optionally delete `%TEMP%\GridSight-logs`.
7. Revoke ESI access on the CCP website (next section).

## 9. Revoking ESI access

In GridSight: **Disconnect ESI** (Settings → "Characters") and *(beta.2+)* **Disconnect** in the Dashboard window delete
the token from your PC and ask EVE SSO to revoke it.

To be sure, also open the [EVE Third-Party Applications page](https://community.eveonline.com/support/third-party-applications/)
and revoke GridSight. This invalidates the tokens on CCP's side, even if copies remain on your disk. Deleting local files
alone does not revoke access.

## 10. Children

GridSight is a tool for EVE Online players and follows the age requirements of EVE Online. It does not knowingly collect
anything from anyone — it has no servers to collect into.

## 11. Changes to this policy

New features may add network requests or local data. Any such change will be listed in the release notes and in this file
before or with the release that introduces it. The date below shows the last update.

*Last updated: 2026-10-14 (draft).*
