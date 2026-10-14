# Network Connections

All network connections GridSight makes, taken from the source code. GridSight has no servers of its own and sends no
telemetry. You can verify this list with any network monitor (for example Windows Resource Monitor → Network, GlassWire or
Wireshark). Items marked *(beta.2+)* are not in 1.0.0-beta.1.

Every request uses HTTPS (except the local login callback) and carries a User-Agent
`GridSight/<version> (+github.com/evelens-app/evelens)` — the app version and the project address, no contact of the
author or of you. *(beta.2+)* Only requests to zKillboard add `; contact: …` with the **zKillboard contact** you entered
in Settings; if the field is empty, no contact is sent. (In 1.0.0-beta.1 every request carried a contact: yours, or the
author's in-game name if the field was empty.)

| Service | Purpose | When | Data sent | Required | Can be turned off |
|---|---|---|---|---|---|
| **EVE SSO** — `login.eveonline.com` | Log in, refresh access | When you log in; when access expires | OAuth login data (handled by CCP); refresh token | Only for ESI features | Don't log in |
| **Local login callback** — `http://localhost:8642` | Receives the login result from your browser | Only while logging in (≤ 5 min) | Nothing leaves your PC | Only for login | — |
| **ESI (authorized)** — `esi.evetech.net` | Badge, dashboard snapshot, account timers, trade-history sync *(beta.2+)*, watching your market orders: `GET /characters/{id}/orders` *(beta.2+)* | Badge ~every 30 s while connected; timers every 10 min; orders watch every 10 min (same cycle as timers); history ~hourly; snapshots when you refresh | Access token, character ID | Only for ESI features | Disconnect ESI / Disconnect *(beta.2+)*; turn off "Track account timers" or only "Collect trade history (hourly)" *(beta.2+)*; turn off only the orders watch with "Watch my market orders (outbid, expiring)" *(beta.2+)*; don't use the dashboard |
| **ESI (public)** — `esi.evetech.net` | Local analysis (pilot names → corp/alliance), market data, routes, item card *(beta.2+)* | When you analyze Local, open the dashboard or click an item | Pilot names you pasted; item IDs; in the item card — your current system (for jump counts) | No | Don't use these features |
| **ESI (public), periodic market requests** — `esi.evetech.net` *(beta.2+)* | Orders watch: `GET /markets/{region_id}/orders?order_type=buy\|sell&type_id=…` for the types of your open orders. Price alerts: `GET /markets/{region_id}/orders?order_type=all&type_id=…` and `POST /universe/names` for item names | Every 10 min on the account-timers cycle (needs "Track account timers" and a character connected in the dashboard). At most 40 market books per character per cycle for the orders watch (the rest of the orders are checked by expiry only); at most 30 market books per cycle for price alerts (only if you have set alerts) | Region ID and item type IDs (and item IDs for names); no login data | No | Uncheck "Watch my market orders (outbid, expiring)"; remove your price alerts in the item card; turn off "Track account timers" |
| **EVE image server** — `images.evetech.net` | Icons and portraits in the dashboard | Dashboard snapshot; item card *(beta.2+)* | Item / character / corporation IDs | No | — |
| **EVE static data** — `developers.eveonline.com` | Item, ship and map data | At most once every 7 days, for intel, mining, appraisal and the dashboard | Nothing personal | For those features | Don't use them |
| **zKillboard** — `zkillboard.com` | Pilot danger stats; abyssal fit statistics | "Check on zKill" button (≤ 20 pilots, 1 request/s); dashboard fits (cached 24 h) | Character IDs you check; ship type IDs; your zKillboard contact, only if you entered one | No | Don't press the button; `--no-fits` for the CLI |
| **Fuzzwork** — `market.fuzzwork.co.uk` | Bulk market prices | Mining window; clipboard appraisal *(beta.2+)*; dashboard trade/industry analysis (cached 1 h; falls back to public ESI if Fuzzwork is down) | Trade hub station; list of item type IDs (from your assets and fits) | No | Close the mining window; `--no-market` for the CLI |
| **GitHub API** — `api.github.com` | Check for a new release | Once a day | Nothing personal | No | Settings → "Check for updates" |
| **EVE game server** — the server your client is connected to, port 26000 | Ping measurement | Only if "Ping by connecting to the server" is on and no passive measurement is available; every 30 s | An empty TCP connection, closed immediately | No | Off by default; *(beta.2+)* asks for confirmation when turned on |
| **Microsoft Edge WebView2** *(beta.2+)* | Renders the dashboard window | When the dashboard is open | GridSight sends nothing through it; the Microsoft component may have its own network behavior | For the dashboard window | Don't open the dashboard |

GridSight also opens pages in your default browser when you click a link (GitHub release page, zKillboard pilot page, EVE
login). Those are normal browser visits.

## What is never sent

Your EVE password, your chat logs, your game logs, your clipboard text (except pilot names you explicitly analyze), your
files, or any data to the author.
