# Localization

Vanta Admin ships with **5 languages** out of the box. You pick the active one in
`config.lua`; the translations themselves live in a separate `locales.lua`.

## Switch language

```lua
-- config.lua
Config.Language = 'en'   -- en | de | fr | es | pt-BR
```

| Code | Language |
|------|----------|
| `en` | English (default) |
| `de` | German |
| `fr` | French |
| `es` | Spanish |
| `pt-BR` | Portuguese (Brazil) |

This controls **all** player-facing text: notifications **and** the entire panel
UI (tabs, buttons, modal, column headers).

!!! info "Unknown code = safe fallback"
    If `Config.Language` is set to a language that doesn't exist, it falls back to
    English and prints a warning in the console.

## Add a new language

Open `locales.lua`, copy the `['en']` block, rename the key, and translate:

```lua
local Locales = {
    ['en'] = { ... },

    ['it'] = {                 -- (1)!
        no_permission = 'Non hai il permesso per farlo.',
        -- ... translate every key ...
        ui = {
            title = 'Admin & Gestione',
            -- ... translate every ui key ...
        },
    },
}
```

1.  Use any code you like (`it`, `pl`, `nl`, …) — it just has to match what you
    set in `Config.Language`.

!!! warning "Keep the placeholders"
    Strings contain format placeholders:

    - `%s` / `%d` (server messages, e.g. `'%s has been kicked.'`)
    - `{n}` / `{total}` (UI counters, e.g. `'{n} / {total} players'`)

    Keep them intact in your translation, or names/numbers won't render.

## How it works (technical)

`config.lua` loads first and defines `Config.Language`. Then `locales.lua` loads
and resolves:

```lua
Config.Locale = Locales[Config.Language] or Locales['en']
```

Both are `shared_scripts`, so server **and** client get `Config.Locale`. The
client passes the `ui` sub-table to the NUI, which fills every element marked
with `data-i18n`.
