# Monitoring (Spectate, Noclip & Live Map)

Vanta Admin includes tools to keep an eye on your players: spectate their in-game
view, fly around freely with noclip, and see everyone on a live map.

!!! warning "Requires OneSync"
    Spectate and the live map need the server to know every player's position and
    to stream remote entities. This only works with **OneSync enabled**.

    Enable it in `server.cfg`:

    ```cfg
    onesync on
    ```

    …or toggle it in your host panel (e.g. Zap-Hosting → server settings). Without
    OneSync these two features are disabled automatically and the console prints a
    warning on start. Noclip works regardless.

## Spectate

Shows a player's **in-game perspective** — what their character sees in GTA.

- Open the **Players** tab → click **Spectate** on a player.
- You turn invisible and are moved to their location; their view is rendered.
- Press **BACKSPACE** to stop and return to where you were.

!!! info "What 'spectate' is — and isn't"
    Spectate renders the **game world** from the player's position. It does **not**
    capture their real desktop, monitor, or anything outside the game. That would
    be spyware and is neither possible nor included.

Requires `vanta_admin.spectate`. Every spectate is written to the audit log.

## Noclip

A free, invisible camera for **yourself** — great for inspecting an area or
following someone unseen.

| Key | Action |
|-----|--------|
| `W` `A` `S` `D` | Move horizontally |
| `Shift` | Move faster |
| `Ctrl` | Move slower |
| `Space` | Move up |
| `Alt` | Move down |

Click **Noclip** in the Players tab toolbar to toggle it on/off. Requires
`vanta_admin.noclip`.

## Live Map

The **Map** tab shows every connected player as a dot, refreshing automatically.

- Hover a dot to see the player's name and ID.
- Refresh rate is set by `Config.MapRefreshMs` (default 2000 ms).
- Requires `vanta_admin.livemap` **and** OneSync. Without OneSync the tab shows a
  notice instead.

### Adding a real map image (optional)

By default the map is a clean coordinate grid. To overlay an actual GTA map:

1. Put a square GTA map image at `html/map.png`.
2. In `html/style.css`, find `#mapCanvas` and enable the background line:
   ```css
   background-image: url('map.png');
   background-size: cover;
   ```
3. If dots sit slightly off, calibrate `MAP_BOUNDS` in `html/script.js` (the
   in-game world's min/max X and Y that map to the image edges).

## Audit logging

Spectate and noclip actions are recorded in the audit log (console, plus the
`vanta_admin_audit` table if a database is connected) — so there's always a
record of who monitored whom and when.
