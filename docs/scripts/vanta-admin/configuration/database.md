# Database Editor

The DB editor lets you view and edit database tables **live, in-game** — safely.

## Step 1 — Connection

The connection (host, user, password, database name) is **not** set in
`config.lua`. It's configured for oxmysql in your `server.cfg`:

```cfg
set mysql_connection_string "mysql://user:password@localhost/YOUR_DB?charset=utf8mb4"
```

Vanta Admin automatically uses exactly the database oxmysql is connected to.

## Step 2 — Choose which tables are editable

Each entry in `Config.DbTables` is one table shown in the panel. At minimum you
only need **3 fields** — columns and data types are detected automatically.

```lua
Config.DbTables = {
    {
        name       = 'Players',          -- display name in the panel
        table      = 'users',            -- real table name
        primaryKey = 'identifier',       -- unique column
        columns    = 'auto',             -- 'auto' = all columns, or { 'name','money' }
        editable   = { 'money', 'job' }, -- {} = view only, 'all' = everything, list = only these
    },
}
```

### Fields

| Field | Required | Description |
|-------|:--------:|-------------|
| `name` | ✅ | Display name in the panel (free to choose) |
| `table` | ✅ | Real table name in your database |
| `primaryKey` | ✅ | Column that uniquely identifies a row (`identifier`, `id`, `plate`, `citizenid`, …) |
| `columns` | ➖ | `'auto'` (all columns) or a list `{ 'a', 'b' }`. Defaults to `'auto'`. |
| `editable` | ➖ | Which columns may be changed (see below). Defaults to none. |
| `limit` | ➖ | Rows per page (default 25, max 100) |
| `label` | ➖ | Optional longer title |

### `editable` options

=== "View only"

    ```lua
    editable = {}
    ```
    Nothing can be changed — safest, read-only.

=== "Specific columns"

    ```lua
    editable = { 'money', 'job' }
    ```
    Only these columns are editable. Types are detected automatically
    (number vs. text) and validated server-side.

=== "Everything"

    ```lua
    editable = 'all'
    ```
    All columns except the `primaryKey`.

    !!! warning
        Powerful — anyone with `dbedit` can change every field. Use only for
        trusted high-rank admins.

=== "Fine-grained"

    ```lua
    editable = {
        money = { type = 'number', min = 0, max = 9999999 },
        job   = { type = 'string', maxLen = 50 },
    }
    ```
    Per-column rules with clamping/length limits.

## Automatic schema detection

On start, Vanta Admin reads each table's real schema from `information_schema`:

- **`columns = 'auto'`** → shows every real column.
- **Type detection** → `INT`/`DECIMAL`/… become *number* fields, everything else
  *text* — with matching validation.
- **`maxLen`** is taken from the real column length.

You don't have to declare column types by hand.

## Console feedback

On boot the banner reports each table:

```text
  [ i  ] Whitelist tables (DB editor):
         [ OK ] Players          -> users
         [FAIL] QB Vehicles      -> player_vehicles  (table not found!)
```

A `[FAIL]` means the `table` name doesn't exist (typo, wrong DB, or the resource
isn't installed). The entry is simply skipped — the server never crashes.

## Security

There is **no free-form SQL** from the UI. Table names, column names and order
come exclusively from your config and the detected schema; all values are passed
as **parameters**. This makes SQL injection impossible. See
**[Security Model](../security.md)**.
