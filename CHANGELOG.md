# Changelog

User-facing changes in each GridSight release. Downloads and SHA-256 hashes: [GitHub Releases](https://github.com/evelens-app/evelens/releases).

## 1.0.0-beta.2 (unreleased)

### New
- **Dashboard built in.** The character dashboard now opens in a GridSight window (tray → "Dashboard"); the separate `GridSight.Snapshot.exe` is no longer needed for it. Connect a character with **Connect character** and take a snapshot. Requires Microsoft Edge WebView2 Runtime (included in Windows 11).
- **Market now:** the first Dashboard section (also tray → "Market now") sums up what to sell to buy orders right now, what to list as a sell order, the best station-trading rows to buy and resell, which of your orders are outbid or expiring, and which stacks sell for noticeably more at another hub — per hub, with totals, the age of the prices and a button that copies the item name for the in-game market search. Cards also have a "price X" button that copies a price for the in-game order field (the suggested list price, the buy-order price, or the price that beats the best competitor).
- **Watch my market orders:** every 10 minutes (with account timers) GridSight checks your open orders; outbid orders, orders expiring within 24 hours and expired orders appear in tray → "Timers" with a dot on the tray icon, and a new outbid order shows one notification. Clicking an outbid line copies the price that beats the best one by one EVE price step. Read-only: GridSight never changes your orders. Turn off with "Watch my market orders (outbid, expiring)" in Settings → "General" → "Account timers".
- **Price alerts:** in the item card (Dashboard window) set "sell drops to ≤" or "buy rises to ≥" for an item at a hub; when it triggers, tray → "Timers" shows it in the group "Price alerts" with a dot and one notification, and clicking copies the current price. Up to 50 alerts, stored locally in `price-alerts.json`, checked every 10 minutes together with account timers.
- **Trading at five hubs:** Jita, Amarr, Dodixie, Rens and Hek, with a hub selector and broker fees based on your standings.
- **Item card:** click any item for live prices at five hubs, margin after taxes, daily volume, jumps from your location, 90-day price history, a margin calculator and short signals ("Good time to buy", "Hub arbitrage", "Where to sell").
- **Market movers:** rising, falling and spiking items for each hub.
- **Real profit:** FIFO profit from your trades across all connected characters, with taxes, broker fees and production cost. Trade history is kept in a local database (`history.db`) because ESI only keeps about 30 days.
- **Price list:** set your own cost for items without a purchase history, or mark items as "Personal use".
- **Appraisal:** copy items from an inventory window and get buy/sell totals and volume at the selected hub (in the clipboard parser).
- **Filters and search** in Dashboard tables, plus a search across the whole snapshot (`Ctrl+K` or `/`).
- **Welcome window** on the first start: where the tray icon is, what to do next, and whether EVE clients and the game log folder were found.
- **Help & feedback** in the tray menu: "User guide", "Report a bug", "Suggest a feature", "Security & privacy", "Check for updates". **About** gets a "Suggest a feature" button. These only open GitHub in your browser; nothing is sent automatically.
- **Net worth:** a strip under the key figures on the Dashboard — wallet + assets (market estimate) + sell orders + buy orders, with the change over 7 and 30 days and a small chart. One point per hour per character is saved locally to `networth.json` (kept 400 days).
- **Quiet hours:** Settings → "General" → "Notifications" → "Quiet hours" turns off pop-up notifications about prices, orders and a finished snapshot for the hours you choose (also across midnight); the tray dot and the lines in "Timers" stay. "Test notification" shows a sample even during quiet hours. Off by default.
- **Move to another PC:** Settings → "General" → "Move to another PC" — "Export settings…" saves settings, thumbnail layout, timers, mining and price alerts to a .zip (never ESI tokens or trade history); "Import settings…" applies it on the next start and keeps the previous files in a `backup-<date-time>` folder.

### Privacy and security
- **Disconnect** button in the Dashboard: deletes the character's token from your PC and revokes it at EVE SSO. Command line: `GridSight.Snapshot logout -c "<character>"` or `logout --all`. **Disconnect ESI** in Settings now revokes the badge token at EVE SSO too.
- Separate switch for the hourly background trade-history sync: **Collect trade history (hourly)** under "Account timers".
- Dashboard reports are rotated: the 20 most recent dated snapshots per character are kept (`--keep N` in the command line; `0` keeps everything). Report files now carry a warning not to share them.
- **Revoke ETW rights (UAC)…** button removes the Windows tracing right that ping/FPS uses.
- "Ping by connecting to the server" now asks for confirmation before it is turned on.
- The User-Agent of network requests no longer contains the author's contact. zKillboard sees a contact only if you enter your own in "zKillboard contact".
- GridSight log files older than 14 days are deleted automatically.
- After moving data from EveLens, old token copies in `%APPDATA%\EveLens` are deleted.
- Stricter EVE SSO login checks, a content security policy in the Dashboard page, size limits for downloaded static data, and gentler zKillboard request pacing with retries.

### Documentation
- New [SECURITY.md](SECURITY.md), [PRIVACY.md](PRIVACY.md), [ESI_PERMISSIONS.md](ESI_PERMISSIONS.md), [NETWORK_CONNECTIONS.md](NETWORK_CONNECTIONS.md), [DOWNLOAD_VERIFICATION.md](DOWNLOAD_VERIFICATION.md) and [FAQ.md](FAQ.md).
- Bug report and feature request forms in GitHub Issues.

## 1.0.0-beta.1

First public beta.

- Live thumbnails of every EVE client with per-character layout, group hotkeys and click to switch.
- Visual alerts on thumbnails from game logs: under attack, warp scrambled, cargo full, Local.
- Intel from chat channels, D-Scan and Local analysis.
- Damage monitor, mining panel, ping/FPS overlay.
- EVE SSO (ESI) login for character features; tokens stored encrypted on your PC.
- Interface in English, Russian, German and Chinese.
- Update check once a day — GridSight never updates itself.
- Settings and data are moved automatically from EveLens, the app's former name.

Log-based alerts are tuned for the Russian client; English client support is in testing.
