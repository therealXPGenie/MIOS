# MIOS — Acoustic Internet Browser

MIOS is an experimental browser/networking system that uses **sound as the
link between a Remote and an Internet-connected Router**.

```text
                 Internet
                    │
                    ▼
             ┌─────────────┐
             │    Router   │
             │  web gateway│
             └──────┬──────┘
                    │
                 🔊 acoustic
                    │
                    ▼
             ┌─────────────┐
             │    Remote   │
             │  no network  │
             └─────────────┘
```

The Remote does not use a normal network transport for browsing. It requests
content over the acoustic link; the Router retrieves the content and sends the
result back as MIOS packets.

## Features

- Single-file browser application: `MIOS.html`
- Embedded ggwave acoustic modem; no separate modem download is required
- Router / Remote roles
- Acoustic request, acknowledgement, data and end-of-transfer packets
- Request IDs for Remote isolation
- Ordered multi-packet page reconstruction
- Router-side web retrieval
- Remote-side network isolation guard
- Built-in dual-peer protocol self-test
- Works as a static HTML application when served from HTTPS or localhost

## Running

Open `MIOS.html` from a suitable HTTPS or localhost origin and allow microphone
access when prompted.

Use one browser/device as **Router** and another as **Remote**. The Router is
the Internet-connected side. The Remote is intended to remain offline and use
the acoustic link for content delivery.

## Protocol

The current protocol uses frames of the general form:

`mios|PKT|KIND|...`

Current protocol kinds include `REQ`, `COR`, `DATA`, `END`, `CHAT`, and `HELLO`.

The Remote uses a request ID (`rid`) to associate returned packets with the
request that initiated them. Page data is transferred as ordered `DATA`
packets and rendered after the expected transfer has completed.

## Acoustic transport

MIOS embeds **ggwave**, an open-source data-over-sound library. ggwave is
licensed under the MIT License by Georgi Gerganov. See
`THIRD_PARTY_NOTICES.md` for the applicable notice and license text.

Upstream project: https://github.com/ggerganov/ggwave

## License

The original MIOS project code is licensed under the **MIT License**. See
`LICENSE`.

Third-party components retain their respective copyrights and license terms;
see `THIRD_PARTY_NOTICES.md`.

## Repository contents

- `MIOS.html` — complete standalone MIOS application
- `LICENSE` — MIT license for MIOS project code
- `THIRD_PARTY_NOTICES.md` — third-party attribution and ggwave license
- `README.md` — project documentation
- `SHA256SUMS.txt` — release checksums
