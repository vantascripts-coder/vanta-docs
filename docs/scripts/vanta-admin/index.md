# Vanta Admin

An in-game **admin & management tool** for FiveM: player management, server
announcements and a **secure database editor** — all through a clean NUI
interface, with **no framework dependency** (works standalone, ESX, QBCore, …).

!!! warning "Not released yet"
    Vanta Admin is **launching soon**. The docs below are a preview so you can see
    exactly what to expect — the script isn't downloadable yet. Join the
    [Discord](https://discord.gg/your-invite) for the release announcement.

<div class="grid cards" markdown>

- :material-rocket-launch: **[Get started](getting-started/installation.md)**
  Install in minutes — copy, `ensure`, set permissions.

- :material-shield-lock: **[Secure by design](security.md)**
  The client is never trusted. ACE permissions, server-side validation, audit log.

- :material-database-edit: **[In-game DB editor](configuration/database.md)**
  Edit your database tables live — whitelisted, injection-safe, auto schema detection.

- :material-translate: **[Multi-language](localization.md)**
  English, German, French, Spanish, Portuguese (BR) — switch with one config line.

</div>

## What it can do

| Area | Actions |
|------|---------|
| **Players** | Live list, Kick, Ban (timed), Heal, Revive, Goto, Bring, Freeze |
| **Server** | Announcements to everyone |
| **Database** | View & edit whitelisted tables/columns, paginated, searchable |

## Highlights

!!! success "Standalone"
    No ESX/QBCore required. oxmysql is **optional** — without it everything works
    except the DB editor, and bans are stored in a JSON file.

!!! tip "Built for safety"
    Every action is checked server-side via **ACE permissions**. The UI only hides
    buttons cosmetically — even a tampered client cannot bypass a permission.

!!! note "Fully configurable"
    `config.lua` and `locales.lua` are open and documented — set the open key,
    language, permissions and which database tables are editable, all without
    touching the core code.

---

New here? Head to **[Installation](getting-started/installation.md)**.
