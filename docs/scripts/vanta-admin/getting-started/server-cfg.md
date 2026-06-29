# server.cfg Setup

A complete, copy-paste example bringing everything together.

```cfg
# ---- Database (optional, for DB editor + persistent bans) ----
set mysql_connection_string "mysql://user:password@localhost/YOUR_DB?charset=utf8mb4"
ensure oxmysql

# ---- Vanta Admin ----
ensure vanta_admin

# ---- Permissions ----
add_ace group.admin vanta_admin.access   allow
add_ace group.admin vanta_admin.kick     allow
add_ace group.admin vanta_admin.ban      allow
add_ace group.admin vanta_admin.heal     allow
add_ace group.admin vanta_admin.teleport allow
add_ace group.admin vanta_admin.freeze   allow
add_ace group.admin vanta_admin.announce allow
add_ace group.admin vanta_admin.dbview   allow
add_ace group.admin vanta_admin.dbedit   allow

add_principal identifier.fivem:YOUR_ID group.admin
```

!!! warning "Start order matters"
    `oxmysql` must be started **before** `vanta_admin`, otherwise the DB editor
    falls back to disabled on boot. Keep the `ensure oxmysql` line above
    `ensure vanta_admin`.

!!! tip "No database"
    Just omit the `mysql_connection_string` and `ensure oxmysql` lines. Vanta
    Admin runs fine; bans are written to `bans.json` inside the resource.

## Where to put the permission lines

You can keep them directly in `server.cfg`, or move them to a separate
`permissions.cfg` and load it with:

```cfg
exec permissions.cfg
```

This keeps your ACL tidy and easy to back up.
