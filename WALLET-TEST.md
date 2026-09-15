# Wallet test — groks-wallet on TN10

15 Sep 2026. This process used [groks-wallet](https://github.com/STP-KAS/groks-wallet). The seed is not in this file.

## Address

```
kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx
```

## Native KAS till payment (live)

Ishum invoice `i25561d78cc16`: €2.50 coffee → **82.64762669 KAS**.

| Field | Value |
| --- | --- |
| Txid | `a7a042501c32cfede58d8672b12a86deaaa2f538606d82002d2e286e689028e7` |
| Payload | `i25561d78cc16` (invoice id) |
| Fee | 207200 sompi |
| Mass | 2062 |
| UTXOs spent | 1 |
| Ishum match | `payload` |
| Status | **Settled** (71 confirmations at claim) |
| Explorer | [tn10 tx](https://explorer-tn10.kaspa.org/txs/a7a042501c32cfede58d8672b12a86deaaa2f538606d82002d2e286e689028e7) |

Self-pay to the same groks-wallet address. That is a valid till match: unique quote id in the payload.

## Other rails (demonstration)

| Invoice | Rail | How | Status |
| --- | --- | --- | --- |
| `icb36973804f2` | kUSD | `Mark settled (demo)` | Settled, `demo: true` |
| `i6591d8b30d34` | USDT guest | `Mark settled (demo)` | Settled, `demo: true` |

kUSD demo is honest: BitCoffee’s Asset ID exists on TN10; this till cannot transfer it yet.

## BitCoffee protocol

- Six published lifecycle txs accepted (see README).
- Local `cargo test --locked --all-targets`: 88 passed, 0 failed.
- Python scripts `py_compile` clean. `kaspa==2.0.2rc1` installs.
- Did not re-deploy genesis or open a new Position (needs their builder + live Module outpoint).

## Node

Local TN10 kaspad gRPC `127.0.0.1:16210`, Borsh `17210`. `send-tkas.mjs` submitted via Borsh wrpc.
