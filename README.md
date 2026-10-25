# VAULT whitelist

Edit [policy.json](https://github.com/splithinator-oss/vault-script-licenses/edit/main/policy.json), then click **Commit changes**.

```json
{
  "games": [79925779087470, 97694147197404],
  "groups": [745931373]
}
```

| List | What adding an ID allows |
| --- | --- |
| `games` | That exact Roblox place, using the ID from its game-page link |
| `groups` | Every place owned by that Roblox group |

Use either list or both. A game is allowed if its ID is in `games` **OR** its owning group's ID is in `groups`.
You do not need licence names, universe IDs, creator records, or expiry fields.

## Examples

**Only specific games:** put their place IDs in `games`; leave `groups` as `[]`.

**All games owned by a group:** put the group ID in `groups`. For example, to
allow the testing game's group and the main game's group:

```json
{
  "games": [],
  "groups": [745931373, 990686758]
}
```

**Both:** keep specific IDs in `games` and group IDs in `groups`. A specific
game does not have to belong to one of the listed groups.

To add an ID, append it with a comma. To remove one, delete it and fix the comma.
Empty lists (`[]`) allow nobody. IDs can be numbers or quoted strings.
Keep the two lists present and use valid JSON, without comments or trailing commas.

**Removing a game ID will still allow that game if its group remains listed.**
To revoke it completely, remove every permission that covers it.

The whitelist currently allows your two listed games and every game owned by
group `745931373`, which you asked to add. Group `990686758` is an example above;
it has not been added to the group list.

## What to expect

Servers check at startup and every 60-70 seconds. GitHub caching can delay updates.
A received denial stops access. Temporary network failures have a maximum
five-minute allowance only for previously verified servers. New servers need a
successful check. After a denial, restart the game server once you restore access.

Unlicensed copies kick with `Script stolen / unlicensed experience. Owner @o93.`

Only **testing game script** has the gate installed. Save/publish that updated
Studio place for live servers. The main game's ID is listed, but its scripts
have not been modified. Older published installations need the updated gate to
read this simplified file.

This whitelist authorises games using the script; it does not whitelist ordinary
players or issue payment/redemption keys.

## Keep source private

This repository contains public IDs only. Do not upload your game source, tokens,
cookies, or secret keys. The gate downloads JSON data and never executes remote Lua.

An editable copy's owner can patch out local checks. Obfuscation adds effort but
cannot make code unremovable. Keep valuable functionality on a service you control
if it must stay outside distributed copies.
