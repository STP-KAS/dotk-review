# Independent review — SuperTypo

**Not an audit.** [@supertypo](https://github.com/supertypo) is invited on this repo as collaborator to check and correct.

Person: GitHub [supertypo](https://github.com/supertypo) (user id 6649964, created 2014-02-11). X [@supertypo_kas](https://x.com/supertypo_kas). OpenAPI contact name `supertypo`, email `suprtypo@pm.me`. Bio on X: Kaspa API / infra, maintainer, maker of kaspa.stream.

This is **not** a character study and **not** a security audit. It is what the public repos and the DOTK launch imply for a name system.

## What he actually runs

Public GitHub (48 repos, 15 Sep 2026). The ones that matter:

| Repo | What it is | Weight |
| --- | --- | --- |
| [simply-kaspa-indexer](https://github.com/supertypo/simply-kaspa-indexer) | Rust PostgreSQL L1 indexer. **31★ / 23 forks.** KNS GitBook: the KNS resolver uses this class of indexer | Highest. This is real public-goods infra |
| kaspa-rest-server (fork), kaspa-rest-proxy | REST in front of kaspad | The public `api.kaspa.org` generation |
| docker-rusty-kaspa, docker-kaspad, dnsseeder | Node / seeder ops | How people run the network |
| simply-kaspa-utxo-exporter | Rich list / distribution from kaspad datadir | Reads UTXO set |
| simply-kaspa-cli-wallet, simply-kaspa-dnsseeder | Own tools | Small |
| silverscript (**fork**, updated 1 Sep 2026) | Compiler he used for DOTK ABI 0.1.0? | Relevant; not the official tagged v1.0.0 pin in kns-spec |
| kccs (fork of kaspanet/kccs) | Covenant conventions | He is reading KCC-1 / KCC-2 |
| **dotk** | Named everywhere | **Does not exist as a public repo** |

There is no public `dotk` among the 48. npm still points at it.

## What he is good at

- Shipping infra that other products sit on. kns-spec `INDEXER.md` is explicit: simply-kaspa-indexer is the L1 feed, **not** the KNS name API. He is the L1 man. KNS is the name shop on top of his blocks/txs.
- Toccata-aware indexer fields: `tx_in_covenant_id`, `tx_out_covenant_id`. DOTK’s “single lineage, easy to spot” only works because those fields exist.
- kaspa.stream already decodes DOTK txs (launch tweet 10/12). Vertical integration: explorer + registry + API.
- The DOTK *design* (gap covering, hash-blind split, self-proving deed address, SDK that **bundles the manifest** so the indexer cannot mark its own homework) is the strongest name-system engineering on Kaspa this desk has seen. Stronger than `KasName.sil`, which is a lock, not a registrar.

## Conflicts (state them, don’t moralize)

1. **He is the L1 indexer KNS depends on, and he launched a competing TLD.** His 15 Sep replies call knsdomains “a centralized closed (source) shop, with their indexer/api as the sole arbiter of names.” That critique of KNS is **true** (kns-spec REAL.md already said uniqueness is “trust knsdomains.org”). It is also **self-serving** the same day he ships `.k`.
2. **His own registry source is closed the day of launch**, while npm and schema.org claim a GitHub. Closed-source critique of KNS + unpublished `.sil` is the same shape he attacks.
3. **Default prove path still hits his directory** (`https://api.dotk.name`) and his node brands (`kaspa.stream`, `kaspa.blue/green/red`). The SDK *can* take a node. The webapp CSP *does* pin his hosts.
4. **Devfund is a template constant.** Registration fees and evicted deposits go to a baked scriptPublicKey, not a burn, not a DAO. That is allowed. It is not “no registrar.” The registrar is a covenant; the **cash register** is still his.
5. **Fee table is his parameter set.** Changing it is a new namespace. Users who buy `kaspa.k` for 998 KAS are buying *this* deployment.

None of that makes the gap covering fake. It makes “trustless, decentralized, no registrar” a marketing sentence that needs the lineage id next to it.

## Advice (owner)

Work with KNS. People who minted `.kas` will likely not appreciate a competing TLD. The uniqueness critique is understood. Bind, don’t alias. See [RISK.md](RISK.md).

## What he is not

- Not Kaspa core.
- Not the official KNS team ([@knsdomain](https://x.com/knsdomain), app.knsdomains.org).
- Not a substitute for a covenant audit. 257 names in hours is a launch, not a battle-test of evict/merge races, reorgs, or KIP-9 mass at the split (the docs themselves call split the tightest mass tx).

## Kron

SuperTypo’s reply also names “Kron's implementation” as another distinct-lineage, no unique-enforcement design. This review did not re-test Kron. `@kronsdk/kaspa-names` exists on npm. Different object again. Do not weld Kron, KNS, and DOTK.

## Ask

Publish `github.com/supertypo/dotk`. Until then this desk treats SuperTypo as: **excellent L1 infra, unpublished name-system source, operator of the default directory and the explorer that decodes it.** Work with KNS if the goal is uniqueness for names people already own.
