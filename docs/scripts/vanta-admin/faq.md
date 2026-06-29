# FAQ & Troubleshooting

## The panel won't open

1. **Do you have permission?** You need at least `vanta_admin.access` and to be in
   a group via `add_principal`. See [Permissions](getting-started/permissions.md).
2. **Right identifier?** Double-check the identifier you added matches the one you
   connect with (txAdmin shows them).
3. **Resource started?** Confirm `ensure vanta_admin` is in `server.cfg` and the
   console shows the Vanta banner with no errors.

## Will the database editor crash my server?

**No.** Vanta Admin uses oxmysql via exports (no hard dependency), checks at
runtime whether oxmysql is running, and guards every DB call. If oxmysql is
missing, the DB editor is disabled and bans use `bans.json`. Even a broken SQL
query only logs an error to the console — it never crashes FXServer.

## A table shows `[FAIL]` in the console

The `table` name in `Config.DbTables` doesn't exist in the connected database.
Check for typos, the right database in `mysql_connection_string`, and that the
framework/resource creating that table is installed. The entry is skipped safely.

## Bans aren't persisting

- **With oxmysql:** make sure you imported `sql/install.sql` (creates
  `vanta_admin_bans`) and that oxmysql starts **before** vanta_admin.
- **Without oxmysql:** bans go to `bans.json` inside the resource — confirm the
  resource folder is writable.

## Can I edit QBCore money?

The `money` column is JSON (`{"cash":0,"bank":0}`). You can edit it as text, but
keep it valid JSON. For everyday money changes, the framework's own admin menu is
usually more convenient.

## How do I change the open key?

Set `Config.OpenKey` in `config.lua` (e.g. `'F7'`). Players can also rebind it in
GTA's keybinding settings since it's a registered key mapping.

## How do I add another language?

Copy the `['en']` block in `locales.lua`, rename the key, translate the strings
(keep `%s`/`%d`/`{n}`/`{total}`), then set `Config.Language` to your new code. See
[Localization](localization.md).

## Can I sell this / protect the code?

Yes. Client/NUI files are always extractable from the player cache, so never put
secrets there. To protect your IP when selling, use the **Cfx.re Asset Escrow**
system — the resource ships with an `escrow_ignore` block that keeps `config.lua`
and `locales.lua` open for buyers while encrypting the rest.

## Still stuck?

Open the server console and look for lines starting with `[vanta_admin]` — they
tell you the database state and any skipped tables. If you're distributing the
script, point users to your Discord for support.
