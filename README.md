# Lightning Domains Standard

This depo defines the requirements and guidelines for a Lightning Domain implementation.

## Purpose

The purpose of this standard is to

## Rules

- Implement [NIP-05](https://github.com/nostr-protocol/nips/blob/master/05.md)
- Implement [LUD-16](https://github.com/lnurl/luds/blob/luds/16.md)
- Implement [LUD-21](https://github.com/lnurl/luds/blob/luds/21.md)
- Implement [NIP-57](https://github.com/nostr-protocol/nips/blob/master/57.md)
- [NIP-05](https://github.com/nostr-protocol/nips/blob/master/05.md) and [LUD-16](https://github.com/lnurl/luds/blob/luds/16.md) should be owned by the same user
- .well-known file
- User `_` on [NIP-05](https://github.com/nostr-protocol/nips/blob/master/05.md) must have a valid pubkey (ROOT)
- Admin user must be name `admin`.
- Create a badge definition and badge award per pubkey
- Endpoints use [NIP-98](https://github.com/nostr-protocol/nips/blob/master/98.md)
- [Walias endpoints](./api/REST_ENDPOINTS.md)

## Api Endpoints

- Get `waliases` by `pubkey`
- Check `walias` availability and price
- Register/Buy new `walias`
- Update/Transfer `walias`
- Remove `walias`

## Domain .well-known

A json file should be accesable `$DOMAIN/.well-known/domain.json` with the following structure:

- title: The name of the `domain`
- logo: The url of the logo image
- description (optional): A description of the `domain`
- apiEndpoint (optional): The url of the api endpoint (Lightning Domain API) (Default: https://lightningdomain.io/api)
- adminPubkey (optional): The hex encoded public key of the admin (defaults to root if not present)

```json
{
  "title": "La Crypta",
  "logo": "https://image_url",
  "description": "Biggest Bitcoin community in Argentina",
  "apiEndpoint": "https://lightningdomain.io/domain",
  "rootPubkey": "hex_pubkey",
  "adminPubkey": "hex_pubkey" // Optional
}
```

## Updatable Event

Emitted by the Lightning Domain Admin. Badge as defined in [NIP-58](https://github.com/nostr-protocol/nips/blob/master/58.md). Should be re-build and published whenever `walias` names change.

### Badge Definition

```json
{
  "pubkey": "$DOMAIN_ROOT", // root handle _ of the domain
  "kind": 30009, // Badge definition
  "tags": [
    ["d", "$DOMAIN:$USER_PUBKEY"], // Unique Identifier
    ["name", "$DOMAIN profile"],
    ["description", "User profile badge for $USER_PUBKEY at $DOMAIN"],
    ["image", "https://nostr.academy/awards/bravery.png", "1024x1024"], // Domain Logo
    ["thumb", "https://nostr.academy/awards/bravery_256x256.png", "256x256"]

    ["p", "$USER_PUBKEY"], // User
    ["h", "$DOMAIN"],
    ["i", "walias_name1"], // username (without domain)
    ["i", "walias_name"] // Can have multiple handles assigned
    ["i", "walias_name3"]
  ],
  "content": "" // Can be used for user profile data, stats, roles, activity, etc.
  // ...
}
```

### Badge Award

```json
{
  "pubkey": "$DOMAIN_ROOT", // root handle _ of the domain
  "kind": 8,
  "tags": [
    ["a", "30009:$DOMAIN:$USER_PUBKEY"],
    ["p", "$USER_PUBKEY", "wss://relay"]
  ]
  // ...
}
```
