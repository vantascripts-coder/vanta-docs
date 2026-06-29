# Installation

## 1. Add the resource

Copy the `vanta_admin` folder into your server's resources, e.g.
`resources/[local]/vanta_admin`, and add it to your `server.cfg`:

```cfg
ensure vanta_admin
```

## 2. (Optional) Enable the database

For the **DB editor** and **persistent bans**, install
[oxmysql](https://github.com/overextended/oxmysql) and start it **before**
`vanta_admin`:

```cfg
ensure oxmysql
ensure vanta_admin
```

Then import the schema into your database:

```bash
# sql/install.sql  -> import via HeidiSQL / phpMyAdmin / DBeaver
```

!!! info "No database? No problem."
    Without oxmysql, the DB editor is disabled automatically and bans are stored
    in `bans.json`. Every other feature keeps working.

## 3. Grant yourself permission

Nothing opens until you have ACE permissions. See
**[Permissions (ACE)](permissions.md)** for the full block — at minimum:

```cfg
add_ace group.admin vanta_admin.access allow
add_principal identifier.fivem:YOUR_ID group.admin
```

## 4. Open the panel

In-game press **`F6`** or type **`/admin`**.

## Verify it loaded

On server start the console prints a status banner. A healthy start looks like:

```text
=================================================================
  VANTA ADMIN   v1.0.0   -   Admin & Management Tool (Standalone)
=================================================================
  [ OK ] Connected to       : your_database
  [ i  ] MySQL version       : 8.0.36
  [ i  ] Ban storage         : database (vanta_admin_bans)
  [ i  ] Whitelist tables (DB editor):
         [ OK ] Players          -> users
  [ OK ] ACE permissions    : 9 defined (vanta_admin.*)
  [ OK ] Open panel with    : /admin  or key F6
  [ OK ] In-game language   : en
=================================================================
```

If you see `[FAIL]` next to a table, check the spelling in
[`Config.DbTables`](../configuration/database.md).
