# ESI Permissions

GridSight never needs your EVE login for its core features (thumbnails, alerts, D-Scan/Local analysis, damage, mining,
ping/FPS). ESI login is optional and only unlocks character-based features. There are two separate logins; you can use
either, both or none. You can revoke access at any time on the
[EVE Third-Party Applications page](https://community.eveonline.com/support/third-party-applications/).

## Why GridSight requests these permissions

- Each permission below is used by a specific feature in the code; none is requested "just in case".
- All permissions are **read-only**, except `esi-fittings.write_fittings.v1`, which is requested only if you explicitly
  ask for it and can only **create** saved fittings.
- EVE SSO asks for all scopes of a login at once. If you don't want the dashboard's broad read access, simply don't use the
  dashboard login — the rest of GridSight keeps working.

## Login 1 — Connect ESI (Settings)

Used for the system · ship badge on thumbnails.

| Scope | Feature | Data it gives | Changes game data |
|---|---|---|---|
| `esi-location.read_location.v1` | Badge: current system / station | Solar system, docked station or structure | No |
| `esi-location.read_ship_type.v1` | Badge: current ship | Ship type and name | No |
| `esi-location.read_online.v1` | Badge: online / offline | Online status, last login | No |

Without this login: no badge; everything else works.

## Login 2 — Dashboard → Connect character *(beta.2+)* / `GridSight.Snapshot login`

Used for the dashboard, advisor, account timers and profit tracking.

| Scope | Feature | Data it gives | Without it |
|---|---|---|---|
| `esi-location.read_location.v1` | Header, jump counts in the item card | Current location | No location info |
| `esi-location.read_ship_type.v1` | Header | Current ship | — |
| `esi-location.read_online.v1` | Header | Online status | — |
| `esi-skills.read_skills.v1` | Skills, advisor (taxes, industry, fits you can fly) | Trained skills and SP | Advisor can't use your skills |
| `esi-skills.read_skillqueue.v1` | Skill queue, timer "queue ends" | Skill queue | No queue timer |
| `esi-wallet.read_character_wallet.v1` | Wallet, 30-day cash flow, profit tracking | Balance, journal, transactions | No wallet / profit |
| `esi-assets.read_assets.v1` | Assets, "sell or list" advice, appraisal of holdings | Items and locations | No asset-based advice |
| `esi-markets.read_character_orders.v1` | Order watch, "your orders" in the item card | Your market orders | No order info |
| `esi-contracts.read_character_contracts.v1` | Contracts list | Your contracts | No contracts |
| `esi-industry.read_character_jobs.v1` | Industry jobs, timers, profit of built items | Industry jobs | No jobs / timers |
| `esi-industry.read_character_mining.v1` | Mining ledger | Mined ore | No mining ledger |
| `esi-characters.read_blueprints.v1` | Production advisor, ME of jobs | Blueprints (ME/TE/runs) | No production advice |
| `esi-planets.manage_planets.v1` | PI colonies, extractor timers | Planetary colonies | No PI info |
| `esi-clones.read_clones.v1` | Clones | Jump clones, home station | — |
| `esi-clones.read_implants.v1` | Implants | Active implants | — |
| `esi-characters.read_loyalty.v1` | LP | Loyalty points | — |
| `esi-characters.read_standings.v1` | Standings, broker fee per trade hub | Standings | Broker fee estimated without standings |
| `esi-fittings.read_fittings.v1` | Saved fits: "can I fly / what to buy" | Saved fittings | — |
| `esi-universe.read_structures.v1` | Names of player structures in assets/orders | Structure names you have access to | Structures shown by ID |

None of these change anything in the game. About `esi-planets.manage_planets.v1`: despite its name, it is the only scope
ESI offers to **read** planetary colonies; GridSight only reads.

ESI does not let you pick individual scopes during login: you approve this whole set or cancel.

## Optional write permission (command line only)

| Scope | Feature | Changes game data |
|---|---|---|
| `esi-fittings.write_fittings.v1` | `GridSight.Snapshot login --fits-write`, then `--export-fits` saves recommended abyssal fits to your in-game fittings | **Yes — creates saved fittings** named `GridSight …`. Never edits or deletes existing fittings. |

Requested only when you add `--fits-write`. Without it, export is unavailable and nothing else changes.

## Not requested

GridSight does not request mail, contacts, calendar, corporation roles/wallets, fleet, UI control (`esi-ui.*`), market
order placement or any other write scopes.
