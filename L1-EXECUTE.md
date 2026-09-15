# What is needed to execute on L1

BitCoffee’s TN10 demo proves **acceptance**: Kaspa Testnet 10 stored the intended covenant transitions. That is not production safety.

## Must close before any mainnet sentence

1. **Audit.** Independent review of SilverScript/Toccata templates, successor authentication, mint/burn conservation, Auction fail-closed, Savings not minting. Formal verification if the compute budget allows. This desk did not audit bytecode.

2. **Reorg testbed.** A public RPC cannot create a controlled fork. `mint/expire` and `avert/activate` are confirmation races. Need an ephemeral multi-node harness.

3. **Economics.** Every TN10 fixture in `docs/ECONOMICS.md` is deliberately small. 0.035 KUSD/KAS, 100 DAA votes, 20% Savings veto, 1 KUSD proposal fee — convenient, not calibrated. Recalculate against observed DAA rate, KAS volatility, and realistic DEX depth.

4. **Oracle decision, in writing.**
   - Keep oracle-free: competing time-limited Modules + KPS veto + DEX arbitrage. Then say what happens if nobody vetoes a 10× wrong price.
   - Or add a fail-closed oracle later. Then it is no longer the current claim.
   Do not ship “oracle-free” as branding for a constructor constant.

5. **Missing Frankencoin-parity paths, or ADRs that refuse them.**
   - Position adjust / extra mint / collateral change
   - Expired-position purchase
   - Partial challenges (one slice per Position is the author’s recommended first step)
   - Parallel governance proposals

6. **Indexer.** Current indexer starts from a known manifest. Mainnet needs third-party discovery, reorg rollback, and supply/debt that anyone can recompute.

7. **Wallets.** Kasware and Kastle must pay and display the KUSD Asset ID. Ishum can quote kUSD today; it cannot settle it. Until a wallet pays the asset, KUSD is a research protocol.

8. **Market.** Peg discipline without an oracle needs somewhere to buy/sell 1 KUSD vs KAS. No depth → no arbitrage → fixed price is just a number.

9. **Mass and fees.** Demo txs sit at 200k–400k mass. KIP-9 storage mass already kills 1-sompi outputs. Mainnet fee/UX for covenant-heavy N:M txs must be measured, not guessed.

10. **x402 boundary.** [kaspa-x402](https://github.com/elldeeone/kaspa-x402) is native KAS, TN10. Putting KUSD in `asset` is a **new binding**. Do not swap the name in Luke’s envelope.

11. **Law.** A KAS-backed synthetic dollar is not “not a security because UTXO.” Get counsel before mainnet issuance. This desk is not Circle.

12. **Capital.** Users lock KAS. Optional grants pay auditors and a second indexer. DAGKnight / Rust fund wallets are not the reserve.

## Honest “execute” ladder

| Stage | Meaning |
| --- | --- |
| TN10 demo (now) | Published txs accepted. Classroom. |
| Third-party reproduce | Another wallet opens/closes a Position against the live Module. |
| Wallet rail | A shop QR that pays the Asset ID, not a demo button. |
| Audit + reorg harness | Security claim becomes discussable. |
| Calibrated testnet | Parameters that would not immediately brick on mainnet volatility. |
| Mainnet | Only after the above. Still not “the Kaspa dollar.” A protocol among others. |

Toccata is live on Kaspa mainnet. Tooling is early. Consensus activation ≠ this protocol is production-ready.
