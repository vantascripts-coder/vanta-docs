# General Configuration

All general settings live at the top of `config.lua`.

```lua
Config.OpenKey     = 'F6'       -- key to open the panel
Config.OpenCommand = 'admin'    -- command to open the panel (/admin)
Config.Language    = 'en'       -- en | de | fr | es | pt-BR
Config.RateLimitMs = 400        -- min ms between two actions per admin (anti-spam)
```

## Open key & command

| Setting | Description |
|---------|-------------|
| `Config.OpenKey` | A FiveM [key name](https://docs.fivem.net/docs/game-references/controls/) (e.g. `F6`, `F7`, `INSERT`). Players can also rebind it in the GTA settings since it's registered as a key mapping. |
| `Config.OpenCommand` | The chat command (without `/`). Default opens with `/admin`. |

!!! note
    Both the key and the command trigger the same access request — the server
    decides whether the panel actually opens based on your ACE permissions.

## Language

```lua
Config.Language = 'en'   -- en | de | fr | es | pt-BR
```

Controls **all player-facing text** (notifications + the whole panel UI). The
translations themselves live in `locales.lua`. See **[Localization](../localization.md)**
to add or edit a language.

## Rate limiting

```lua
Config.RateLimitMs = 400
```

Minimum time in milliseconds between two actions from the same admin. Prevents
button-spam and accidental double-actions. Lower = snappier, higher = stricter.
