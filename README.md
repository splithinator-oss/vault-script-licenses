# VAULT script licences

Owner: @o93. Edit **policy.json** to manage who may run the licensed game code.
This repository contains public permission records only. Never upload game scripts,
Roblox cookies, GitHub tokens, Discord tokens, or secret licence keys here.

## Allow or revoke an experience

1. Open `policy.json`, click the pencil, and edit the existing `o93-owner` licence.
2. Each object in `experiences` must contain the exact **placeId**, **universeId**,
   **creatorType** (`User` or `Group`), and **creatorId** of the licensed game.
   Keep IDs inside quotation marks. A place ID and a universe ID are different.
3. Add an experience object to allow a place. Remove its object to revoke that place.
4. Set a licence's `enabled` to `false` to revoke every place on that licence.
   The root `enabled` switch disables every licence.
5. Click **Commit changes**. Keep valid JSON: commas between objects, no trailing commas.

The owner licence currently permits only:

| Game | Place ID | Universe ID | Owning group |
| --- | --- | --- | --- |
| Testing game script | 79925779087470 | 10766735380 | 745931373 |
| 3unny's Closet | 97694147197404 | 9320774242 | 990686758 |

## Add a customer

Add another named record under `licenses`, for example:

```json
"customer-name": {
  "enabled": true,
  "expiresAt": 0,
  "experiences": [
    {
      "label": "Customer game",
      "placeId": "123",
      "universeId": "456",
      "creatorType": "User",
      "creatorId": "789"
    }
  ]
}
```

Replace every example ID with verified real IDs. In that customer's server-only
`VaultLicense.Settings`, set `LicenseId` to `customer-name`. This name identifies a
licence; it is public metadata, **not a password or redeemable player key**.
Licences authorise developers' experiences. They do not restrict ordinary players
who join an authorised game. Roblox usernames and Discord IDs are not creator IDs.

`expiresAt` is a Unix timestamp in seconds, UTC. `0` means no expiry. At the
exact expiry second the licence is invalid. No Studio bypass is enabled.

## Timing and failures

Each running server checks on startup and every 60-70 seconds. GitHub/CDN caching
can delay edits; changes are not guaranteed to be instantaneous. A valid denial
revokes access as soon as it is received. A previously verified server can survive
a temporary network outage for at most 300 seconds from its last verification.
New servers never start without a successful check. Malformed policies deny access.
Denied servers require a restart after fixing or restoring their licence.

Unlicensed copies kick with `Script stolen / unlicensed experience. Owner @o93.`
Network/policy errors use a temporary-unavailability message instead.

## Protection limits

The gate runs on the server and the protected entry scripts require it before
starting. Removing only the gate stops those entry scripts. No remote Lua is
downloaded or executed. No game objects, player data, or saved progress are deleted.

Someone who owns an editable copy can change or remove all local checks. Obfuscation
only increases the effort; it is not unbreakable DRM. Stronger protection requires
keeping valuable functionality behind an authenticated service you control.
Do not place GitHub credentials in Roblox source to read a private repository.

Only the **testing game script** Studio place was instrumented during setup.
The main game's ID is permitted by policy, but it needs its own installation to
enforce these checks.
