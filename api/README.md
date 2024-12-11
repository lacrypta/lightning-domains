# Lightning Domains API

This API allows you to interact with `user` data, `wallets`, and `waliases` in the **Lightning Domains** ecosystem.

## Table of Contents

- [Introduction](#introduction)

- [Authentication](#authentication)

- [Error Handling](#error-handling)

- [Endpoints](#endpoints)

---

## Introduction

The Lightning Domains API enables developers to manage users, wallets, and waliases within the Lightning Network. It provides endpoints to fetch and update user data, manage wallets associated with users and waliases, and handle walias registrations and transfers.

---

## Authentication

This API uses Nostr-based authentication as defined in [NIP-98](https://github.com/nostr-protocol/nips/blob/master/98.md) . Authenticated methods require an HTTP `Authorization` header in the following format:

```makefile
Authorization: Nostr <encodedEvent>
```

- **`<encodedEvent>`** : Base64-encoded JSON event.

### Example

```javascript
const body = JSON.stringify({
  name: "name",
  domain: "domain",
  pubkey: "2ad91f1dca2dcd5fc89e7208d1e5059f0bac0870d63fc3bac21c7a9388fa18fd",
});

const event = {
  kind: 27235,
  tags: [
    ["u", "/api/walias"],
    ["method", "POST"],
    ["payload", sha256Hex(body)],
  ],
  content: "",
};

// Sign event

const encodedEvent = btoa(JSON.stringify(event));

const headers = `Authorization: Nostr ${encodedEvent}`;
```

---

## Error Handling

The API uses standard HTTP status codes to indicate the success or failure of an API request. Responses containing errors will include a JSON object with `success: false` and a `reason` for the error.

---

## Endpoints

### User

- [Get User Data](./users/get_user_data.md)

- [Update User Data](./users/update_user_data.md)

### Walias

- [Get Walias Public Data](./waliases/get_walias_public_data.md)

- [Register Walias](./waliases/register_walias.md)

- [Update Walias](./waliases/update_walias.md)

- [Delete Walias](./waliases/delete_walias.md)

- [Verify Walias Payment](./waliases/verify_payment.md)

### Wallet

- [Get User Wallets](./wallets/get_user_wallets.md)

- [Get Walias Wallets](./wallets/get_walias_wallets.md)

- [Create Wallet for Walias](./wallets/create_wallet_for_walias.md)

- [Get Wallet by ID](./wallets/get_wallet_by_id.md)

- [Update Wallet by ID](./wallets/update_wallet_by_id.md)

- [Delete Wallet by ID](./wallets/delete_wallet_by_id.md)

- [Get Wallet LNURLP](./wallets/get_wallet_lnurlp.md)

- [Get Wallet LNURLP Callback](./wallets/get_wallet_lnurlp_callback.md)

---

# How to Use the API

To interact with the API, make HTTP requests to the appropriate endpoints with the required parameters, headers, and request bodies as specified in the documentation.

### Example Request with Authentication

```bash
curl -X GET https://api.walias.io/domain.com/users/{pubkey}/wallets \
  -H "Authorization: Nostr {encodedEvent}"
```

---

# Thank You

Thank you for using the Lightning Domains API. We look forward to seeing what you build!

---

# Note to Developers

Please ensure that you follow the authentication and security guidelines when integrating with the API. Always handle sensitive data securely and responsibly.

---

# Footnotes

- **LNURL** is a set of protocols to improve UX for Lightning Network payments.

- **Walias** is the address resulted by joining `name@domain` in the Lightning Network ecosystem.

- **Nostr** is a protocol for decentralized social networking.

---

# Additional Documentation

For more information on related technologies and protocols, you may refer to the following resources:

- [Bitcoin Lightning Network](https://lightning.network/)

- [LNURL Protocol](https://github.com/lnurl/luds)

- [Nostr Protocol](https://github.com/nostr-protocol)

- [NIP-98 Authentication](https://github.com/nostr-protocol/nips/blob/master/98.md)
