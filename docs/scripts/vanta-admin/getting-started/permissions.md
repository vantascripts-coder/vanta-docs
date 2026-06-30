# Permissions (ACE)

Vanta Admin uses FiveM's built-in **ACE permission system**. Permissions are
checked **server-side** for every action — the UI only hides buttons cosmetically.

!!! danger "Without ACE permissions, nobody can open the panel."
    This is by design. You must explicitly grant access.

## Full permission list

| Permission | Allows |
|------------|--------|
| `vanta_admin.access` | Open the panel at all |
| `vanta_admin.kick` | Kick players |
| `vanta_admin.ban` | Ban players |
| `vanta_admin.heal` | Heal / revive |
| `vanta_admin.teleport` | Goto / bring |
| `vanta_admin.freeze` | Freeze players |
| `vanta_admin.announce` | Send announcements |
| `vanta_admin.dbview` | View database tables |
| `vanta_admin.dbedit` | Edit database records |
| `vanta_admin.spectate` | Spectate a player's in-game view (needs OneSync) |
| `vanta_admin.noclip` | Free-camera noclip movement |
| `vanta_admin.livemap` | Live player map in the panel (needs OneSync) |

## Grant full admin

Add to your `server.cfg` (or a dedicated `permissions.cfg`):

```cfg
add_ace group.admin vanta_admin.access   allow
add_ace group.admin vanta_admin.kick     allow
add_ace group.admin vanta_admin.ban      allow
add_ace group.admin vanta_admin.heal     allow
add_ace group.admin vanta_admin.teleport allow
add_ace group.admin vanta_admin.freeze   allow
add_ace group.admin vanta_admin.announce allow
add_ace group.admin vanta_admin.dbview   allow
add_ace group.admin vanta_admin.dbedit   allow
add_ace group.admin vanta_admin.spectate allow
add_ace group.admin vanta_admin.noclip   allow
add_ace group.admin vanta_admin.livemap  allow

# Add yourself to the admin group (use YOUR identifier!)
add_principal identifier.fivem:YOUR_ID  group.admin
# or via license:
# add_principal identifier.license:abc123...  group.admin
```

## Granular roles

Permissions are independent, so you can build limited roles. A moderator who can
only open the panel and kick:

```cfg
add_ace group.mod vanta_admin.access allow
add_ace group.mod vanta_admin.kick   allow
add_principal identifier.fivem:123456 group.mod
```

That mod will not even **see** the ban or database buttons — because the server
tells the client which buttons it's allowed to render.

## Finding your identifier

- Use **txAdmin** (Players → your name → identifiers), or
- run a server console command while connected to print identifiers, or
- check the server console log when you join.

Pick `fivem:`, `license:`, `steam:` or `discord:` — any works with
`add_principal`.
