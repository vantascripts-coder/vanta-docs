# Framework Presets

Ready-made `Config.DbTables` entries for the most common frameworks. They live
commented-out in `config.lua` — just remove the `--` for the ones you use, or
copy them here.

=== "ESX (es_extended)"

    ```lua
    { name = 'ESX | Players', table = 'users', primaryKey = 'identifier',
      columns = 'auto', editable = { 'job', 'job_grade', 'group' } },

    { name = 'ESX | Vehicles', table = 'owned_vehicles', primaryKey = 'plate',
      columns = 'auto', editable = { 'owner', 'stored' } },
    ```

=== "QBCore / Qbox"

    ```lua
    { name = 'QB | Players', table = 'players', primaryKey = 'citizenid',
      columns = { 'citizenid', 'name', 'money', 'job', 'gang' }, editable = { 'money' } },

    { name = 'QB | Vehicles', table = 'player_vehicles', primaryKey = 'plate',
      columns = 'auto', editable = { 'citizenid', 'garage', 'state' } },
    ```

=== "vRP"

    ```lua
    { name = 'vRP | User IDs', table = 'vrp_user_ids', primaryKey = 'identifier',
      columns = 'auto', editable = {} },
    ```

=== "Custom / any resource"

    ```lua
    { name = 'My Shop', table = 'my_shop_items', primaryKey = 'id',
      columns = 'auto', editable = {} },
    ```

!!! tip
    Not sure of the exact table/column names? Set `columns = 'auto'` and
    `editable = {}` first to just **view** the table, then add the columns you
    want to edit once you can see them.

!!! note "QBCore money is JSON"
    In QBCore the `money` column is a JSON string (`{"cash":0,"bank":0}`). Editing
    it as raw text works, but be careful to keep valid JSON. For per-account
    editing you'd typically use the framework's own admin tools.
