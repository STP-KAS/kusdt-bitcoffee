# Independent review — BitCoffee0 KUSD

**A UTXO-native, oracle-free, KAS-backed stablecoin candidate on Kaspa L1.**

This repository is an independent Grok pass of BitCoffee0’s KUSD, tested against **groks-wallet** on **Kaspa Testnet 10**. It is not BitCoffee’s code. It is not an audit. It is not mainnet money.

Showcase: [https://sixpack.wtf/kusd.html](https://sixpack.wtf/kusd.html)

Sister: [STP-KAS/poc-revisited](https://github.com/STP-KAS/poc-revisited) — desk PoC (Ishum kUSD chair) revisited against this protocol.

> Experimental and unaudited. Testnet KAS has no value. Do not use this to secure assets of real value.

## Verdict

BitCoffee shipped a **real covenant protocol** on TN10. Six published lifecycle transactions are accepted on the live DAG and carry the published KUSD Asset ID. That is a different object from this desk’s reserved kUSD *chair* in [Ishum](https://github.com/STP-KAS/ishum).

It is **not** ready to execute as a mainnet dollar.

| Claim | Holds? |
| --- | --- |
| Deployed on Kaspa Testnet 10 | Yes. Txids below, `is_accepted: true` |
| Overcollateralized with native KAS | Yes, in the design and in the 1,000 KAS demo position |
| No centralized price oracle | Yes: Module liquidation price is a constructor constant (0.035 KUSD/KAS in the fixture) |
| No issuer freeze key | Yes, in the design. A covenant is not Tether `addBlackList` |
| Peg will hold without a DEX | **Unproven.** Oracle-free is a bet on veto + arbitrage |
| Ready for shops / dapp unit | **No.** No wallet pay path for the Asset ID. Unaudited. Toy parameters |

## What Grok did

1. Read [Kas-Smiths #143](https://kas-smiths.org/t/kusd-a-decentralized-oracle-free-kas-backed-stablecoin-on-l1/143) (BitCoffee0, 13 Sep 2026).
2. Cloned [`bitcoffee0/kusd`](https://github.com/bitcoffee0/kusd) branch `tn10`. Read ARCHITECTURE, ECONOMICS, SECURITY, FRANKENCOIN, TESTNET, GOVERNANCE, DEPLOYMENT, TESTING.
3. Pinned SilverScript `3ed973335b59269293564805cc2c58a14595ec03` as the repo instructs.
4. Probed groks-wallet on live TN10 (`api-tn10.kaspa.org` + local kaspad `:16210`).
5. Verified all six published validation transactions (accepted; Asset ID present in each blob).
6. Restored the original Ishum POS on [sixpack.wtf](https://sixpack.wtf/till.html) so KAS / kUSD / USDT can be chosen as a PoC. Receive address = groks-wallet (`kaspatest:qzffl5…v0ldx`).
7. Mapped every STP-KAS repo against this protocol ([poc-revisited](https://github.com/STP-KAS/poc-revisited)).

Did **not** open a new BitCoffee Position from this wallet in this pass. That needs their Python builder, the live Module outpoint, and a TN10 key in `.env`. The published multi-wallet auction already used distinct owner / challenger / bidder keys on-chain.

## Why Grok named kUSD first

Two weeks earlier the desk asked Grok to think about a Kaspa-native dollar so dapps sequenced on L1 would not have to wait for Tether.

What existed: Parker (1 locked sompi), PegLab (WILL DEPEG), Ishum (EUR keypad), Gramlane (grams), sixpack.wtf (x402 = native KAS), Kasplex USDT/USDC on L2.

What was missing: one working lesson that puts a freeze-capable dollar next to a PoW rail. Grok reserved the name **kUSD** as a till seat: “if someone posts reserves/collateral.” No asset. No covenant. Master file: dollars 0–0.

BitCoffee filled a nearby name with a protocol. Same problem. Different object. Do not weld them.

## TN10 evidence (15 Sep 2026)

Wallet: [`kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx`](https://tn10.kaspa.stream/addresses/kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx)

At probe: **1,033,127.88 tKAS**, 329,884 UTXOs, TN10 DAA **570938367**. Worthless coins.

KUSD Asset ID: `a2d81080bd74ab419f0bfea73b20c5154100520be15d68a190a5d1adf52f32b5`

| Path | Txid | Accepted | Mass |
| --- | --- | --- | ---: |
| Governed Module | `2d571d6b9b12d7f24e745cbb72ea4a825cd04566760773b77ac350624a324453` | yes | 397932 |
| Savings activation | `472af9468824ae3a2a3cda0f82d28bc7633d5bd872111f21c8d4342e0b331a92` | yes | 304692 |
| Repay and close | `680c64086774ae30d027dd745ad9d75d6496cb3d2ac270efefec1a652157c327` | yes | 371824 |
| Savings withdraw | `d34343598556d997cd190012f637b76e7c413180ea9ab4293145010ace1120c5` | yes | 244064 |
| Auction backstop | `67179c8b50079d4454027c5b4a8acc536faad2a224c3b4b018eff11fb441c678` | yes | 266346 |
| Multi-wallet auction | `b4d7e2e4efdf24efe1bfe2200f96245a516b503baa397579726966bf555738e5` | yes | 326525 |

Published indexed snapshot after those paths: 15 KUSD supply, 15 KUSD position debt, 10 KPS, 1,000 KAS in the Reserve. That is BitCoffee’s record, cross-checked by tx acceptance, not re-indexed from scratch here.

## What is needed to execute on L1

See [L1-EXECUTE.md](L1-EXECUTE.md). Short list:

1. Independent covenant + replay + reorg audit (public RPC cannot fake forks).
2. Recalibrate every number in BitCoffee `docs/ECONOMICS.md`. 0.035 is a fixture.
3. Write down the oracle decision: competitive Modules, or a fail-closed oracle later.
4. Partial challenges **or** an ADR that they will not exist.
5. Third-party indexer that survives reorgs.
6. Wallet pay/sign for the KCC Asset ID (Kasware/Kastle). Until then it is not a till rail.
7. A DEX/RFQ so 1 KUSD has an arbitrage loop against KAS.
8. kaspa-x402 stays native KAS. KUSD as `asset` is a new binding.
9. Counsel before mainnet issuance.

## Capital and keys

Asked on [X, 15 Sep 2026](https://x.com/StppStp/status/2099737095065538930):

| Question | Recommendation |
| --- | --- |
| Fund from Discord / DAGKnight / Rust wallets? | **Users lock their own KAS.** Treasuries may grant *audits and indexers*, not back the peg. Do not mix core-fund jobs with a dollar reserve. |
| Who holds the keys — core multisig, covenants, mix? | **Covenants hold the spending rules.** A core freeze multisig recreates Tether. Bootstrap: KPS holders *veto* bad Modules, then fade. Never a blacklist. |

## Sources

- [Kas-Smiths post](https://kas-smiths.org/t/kusd-a-decentralized-oracle-free-kas-backed-stablecoin-on-l1/143)
- [bitcoffee0/kusd](https://github.com/bitcoffee0/kusd) `tn10`
- [Frankencoin 7409532](https://github.com/Frankencoin-ZCHF/Frankencoin/tree/7409532eac3ac77e8f7d4f2887bb538c0ee0c72d)
- [STP-KAS/ishum](https://github.com/STP-KAS/ishum), [grok-heavy-showcase](https://github.com/STP-KAS/grok-heavy-showcase), [groks-wallet](https://github.com/STP-KAS/groks-wallet)
- [sixpack.wtf](https://sixpack.wtf/kusd.html)
- Live REST: `https://api-tn10.kaspa.org`

## License

MIT. No warranty. Not financial advice. Not Kaspa core.
