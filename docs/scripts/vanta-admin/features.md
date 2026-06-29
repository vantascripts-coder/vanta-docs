# Features

The panel has three tabs. Buttons appear only if your
**[ACE permissions](getting-started/permissions.md)** allow them.

## Players

A live list of connected players with ID, name, ping and license. Per-player
actions:

| Action | Permission | What it does |
|--------|------------|--------------|
| **Heal** | `heal` | Restore health + armor, clear blood damage |
| **Revive** | `heal` | Resurrect if dead, then full heal |
| **Goto** | `teleport` | Teleport yourself to the player |
| **Bring** | `teleport` | Teleport the player to you |
| **Freeze** | `freeze` | Toggle freezing the player in place |
| **Kick** | `kick` | Disconnect with a reason |
| **Ban** | `ban` | Ban with a reason and optional duration (0 = permanent) |

!!! info "Teleport uses synced server coords"
    Goto/Bring read the target's server-synced position — no client trust needed.

## Server

| Feature | Permission | What it does |
|---------|------------|--------------|
| **Announcement** | `announce` | Sends a notification to every connected player |

## Database

Pick a whitelisted table, **Load**, then click a value to edit it inline. Supports
pagination and search by primary key. See **[Database Editor](configuration/database.md)**
for setup.

| Capability | Permission |
|------------|------------|
| View tables & rows | `dbview` |
| Edit values | `dbedit` |

## Bans

- **With oxmysql:** stored in the `vanta_admin_bans` table, checked on connect.
- **Without oxmysql:** stored in `bans.json` inside the resource, checked on connect.

Banned players see the reason and remaining time on the connection screen.

## Audit log

Every admin action (kick, ban, heal, teleport, freeze, announce, DB update) is
logged:

- Always to the **server console** (`[vanta_admin AUDIT]`).
- Additionally to the **`vanta_admin_audit`** table when a database is connected.

This gives you a full who-did-what-and-when trail.
