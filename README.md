> **Experimental only. Not a product.**
>
> Do not use wallet integrations on this GitHub. STP remains a clown. [DISCLAIMER.md](DISCLAIMER.md)

# Independent review — SuperTypo DOTK

**Not an audit. Not a security review. Not a certification. Not Kaspa core.**

This is an independent Grok pass of public pages, APIs, npm packages, and chain JSON on **15 Sep 2026**, written for the KNS team. It does **not** replace a covenant audit. It does **not** say the Silverscript is safe. It does **not** say you should lock large KAS.

What KNS should learn from it is on [STP-KAS/kns-dotk](https://github.com/STP-KAS/kns-dotk) and in [FOR-KNS.md](https://github.com/STP-KAS/kns-tn10-testing/blob/main/FOR-KNS.md).

---

**A covenant name registry on Kaspa L1 (`.k`, not `.kas`).**

Pass of [dotk.name](https://dotk.name/developers) against [STP-KAS/kns-spec](https://github.com/STP-KAS/kns-spec). It is not SuperTypo’s code. It is not official KNS.

> Mainnet money is real. The Silverscript is **not published**. Do not treat this as a green light to lock large KAS. **Not an audit.**

## Verdict

DOTK shipped a **live mainnet registry** whose uniqueness is a **gap covering of `blake3(name)`**, spent as a double-spend, inside **one covenant lineage**. That is a different object from KNS inscriptions. SuperTypo is right that KNS uniqueness is an indexer rule. He is not right that “consensus unique” means Kaspa nodes know `.k` as a TLD.

The GitHub the site and npm point at — [`github.com/supertypo/dotk`](https://github.com/supertypo/dotk) — **404s**. npm `@dotk/sdk` / `@dotk/sdk-tx` **1.0.0** exist. The covenant sources `sil/DotkGap.sil` and `sil/DotkDeed.sil` do not.

| Claim | Holds? |
| --- | --- |
| Live on Kaspa mainnet | **Yes.** Health, genesis, names, deed UTXO below |
| Uniqueness is FCFS indexer (like KNS) | **No.** Duplicate register = split the same gap UTXO = double-spend |
| Nodes reject a second `alice.k` as a name opcode | **No.** Nodes reject a second spend of that gap. A second *registry* is another lineage |
| Trustless resolve without their host | **Mostly.** Deed address is derivable; `api.kaspa.org` UTXO JSON **omits `covenant_id`**. Need wRPC/WASM node or SuperTypo’s indexer |
| Open source (tweet 9/12, JSON-LD, npm `repository`) | **Not yet.** Repo 404. **Ask for the code.** |
| Cheap | **Relative.** 5+ chars = 38 KAS fee + 1 KAS bond. 1-char = 3998 KAS. Devfund is baked |
| Cards / records | **Yes, with a caveat.** Indexer “proves nothing about a card” unless the client has a node |
| Drop-in replacement for `.kas` | **No.** Different TLD, different owners, different object |

## Why this is not KNS

[kns-spec](https://github.com/STP-KAS/kns-spec) already split two objects. Do not mix them.

| Layer | KNS today | DOTK today |
| --- | --- | --- |
| TLD | `.kas` | `.k` |
| On chain | `kns` commit-reveal envelope | `DotkGap` + `DotkDeed` P2SH, one `covenant_id` |
| Uniqueness | Official indexer, first valid reveal | Gap covering of `blake3(name)` inside this lineage |
| Resolve | `api.knsdomains.org` | `api.dotk.name` + optional node prove |
| Records | One text inscription per field | One **card** output on transfer |
| Compiler claimed | silverc **v1.0.0** (`3ed9733`) in kns-spec | ABI `compiler_version` **0.1.0** |
| Source | Protocol public; indexer closed | SDK on npm; **covenant + directory GitHub missing** |

`supertypo.kas` (KNS) and `supertypo.k` (DOTK) are **different keys**. Same for `kaspa.kas` / `kaspa.k`. Two namespaces, two owners.

## Community risk (owner)

Kaspa community who have minted KNS domains will likely not appreciate the effort. This desk understands the initiative. **Advice: work with KNS.**

Full note: [RISK.md](RISK.md). A live `.k` registrar next to paid `.kas` inscriptions is a social problem, not only a protocol one.

## What Grok did

1. Fetched [dotk.name/developers](https://dotk.name/developers). Without JS the page is a title. With JS it is a full protocol essay. Crawler leak: **the developer docs are not in HTML.**
2. Pulled OpenAPI from [api.dotk.name/v1](https://api.dotk.name/v1) (contact `supertypo` / `suprtypo@pm.me`, ISC, v0.1.0).
3. Hit live `/v1/health`, `/v1/genesis`, `/v1/keyspace`, `/v1/names/supertypo`, `/v1/names/kaspa`.
4. Checked genesis authorizing tx and the `supertypo.k` deed UTXO on `api.kaspa.org`.
5. Read `@dotk/sdk@1.0.0` and `@dotk/sdk-tx@1.0.0` from npm/jsDelivr (compiled JS + `.d.ts` + README). `repository` = `github.com/supertypo/dotk`. GitHub: **404**.
6. Listed all **48** public [supertypo](https://github.com/supertypo) repos. No `dotk`. Independent SuperTypo note: [SUPERTYPO.md](SUPERTYPO.md).
7. Compared against kns-spec `PROTOCOL.md`, `REAL.md`, `CONFORMANCE.md`, `INDEXER.md`, `KasName.sil`.
8. Read SuperTypo’s 15 Sep 2026 12-post launch thread and the later replies about KNS.

**Did not** recompile `DotkGap.sil` / `DotkDeed.sil` — they are not published. **Did not** sign a register. **Did not** run a local rusty-kaspa wRPC prove of `covenant_id` on the deed UTXO.

## Live evidence (15 Sep 2026, ~14:10 UTC)

### Directory

```
GET https://api.dotk.name/v1/health
```

| Field | Value |
| --- | --- |
| `healthy` / `caughtUp` / `selfTest.proven` | true / true / true |
| `network` | mainnet |
| `active` / `pending` / `ownerUnknown` / `gaps` | 257 / 2 / 0 / 260 |
| `historySeq` | 585 |
| `tipDistance` | 2 |
| `netBps` | 10 |
| `registryCovenantId` | `ee2128c03dfac7f6d74734bb3c879bd999434c47a55945b8a6daae2a1e4a21de` |

`gaps ≈ active + pending + 1` matches the docs: gap bounds are deed keys, gaps number deeds + 1.

### Genesis (manifest, not the first name)

| | |
| --- | --- |
| version | 4 |
| gap template | `ba1e7b8e2dfda606a902c89437625b1c31f82668cd8cfdc7cf365a8ad77c5a3d` (`sil/DotkGap.sil`) |
| deed template | `238a8d0a5af1ea136d50dd49973487929b8e713a84f1bd1650e97776b9a3f5a0` (`sil/DotkDeed.sil`) |
| entries (gap) | `split` `2e5318ff`, `merge` `63d25bc2`, `absorbed` `dab76355` |
| entries (deed) | `activate`, `evict`, `release`, `transfer` |
| authorizing outpoint | `e077087a4761098dcb55a953057b4a92aadf0f834c7df85f53c8bae8634d5d10:0` |
| that tx on `api.kaspa.org` | **accepted**, version 0, **P2PK outputs, `covenant_id: null`**. Binding input, not the registry UTXO itself |

### Fees (baked in the template; sompi → KAS)

| | DOTK | KNS (kns-spec) |
| --- | ---: | ---: |
| 1 char | 3998 | 4200 (1–2 graphemes) |
| 2 | 1998 | 4200 |
| 3 | 998 | 2100 |
| 4 | 248 | 525 |
| 5+ | 38 | 35 |
| bond (locked on ACTIVE) | 1 | — |
| deposit (PENDING; returned on activate; **devfund on evict**) | 36 | — |
| gap value | 1 | — |
| `t_evict` | 3000 DAA (~5 min at 10 bps) | — |
| payee | baked `devfund_spk` | protocol address `kaspa:qyp4nvaq…qfcmynn` |

DOTK length is **UTF-8 bytes 1–32, no edge hyphens**, not graphemes. Emoji pricing will disagree with KNS.

### Names

```
GET https://api.dotk.name/v1/names/supertypo
```

| | DOTK `supertypo.k` | KNS `supertypo.kas` |
| --- | --- | --- |
| owner address | `kaspa:qzaarz9u2qfe6a6tt04j39pej8tk9mhrntjhfaymvwelucq9wclvyneumu0u3` | `kaspa:qpg39v5ajkpjzh0fqx65fm2ez0m8fswj3440a0h98s9kddx4tvw6x9gcl79xj` |
| deed / inscription | P2SH `kaspa:ppqjpuxr…p2skze6cpt` | `e8912492…f359fd11i0` |

Deed UTXO on `api.kaspa.org`: **1 KAS** (the bond), outpoint `52f60e696eccc00316aabb32af09ad577310e5fd3246966754dee4fe7b5b3e12:0`, accepted. Activate witness starts `09 73757065727479706f` = push `"supertypo"`. The name is in the redeem script, as the developer page says.

`kns.k` and `dotk.k`: **not registered** (`{"code":"not_found"}`).

## How uniqueness actually works

From the developers JS (not the HTML) and SuperTypo’s own thread:

1. `key = blake3(name)` — unsalted. A dictionary word is recognizable from its key.
2. The registry covers the 256-bit keyspace with **gap UTXOs** `(lo, hi)`.
3. Register = `split` the one gap that contains `key` → two gaps + a **PENDING** deed (hash-blind claim `blake3(name ‖ ownerType ‖ owner)`).
4. A second register of the same name must spend the same gap. Consensus: one wins.
5. `activate` reveals the name, pays the fee to the **devfund**, returns the deposit, stamps ACTIVE.
6. `transfer` spends only the owner’s deed. `release` / `evict` merge the two flanking gaps.

This is the thing `KasName.sil` does **not** do. kns-spec is explicit: `covenant_id` is hashed from an **outpoint**; anyone can genesis another UTXO that writes `alice` in state. DOTK’s answer is: **don’t put uniqueness in the deed; put it in the covering of the keyspace.** Within lineage `ee2128c0…`, that holds.

Outside that lineage it does not. Template constants (devfund, fees, bond, deed template hash) are compile-time. A different set is a different namespace. That is honest engineering. Marketing “consensus-unique `.k` names” still oversells it as a Kaspa TLD.

## Leaks

| Leak | Where | Why it matters |
| --- | --- | --- |
| Lookup log | `https://api.dotk.name` is the default directory (`@dotk/sdk` `DIRECTORIES.mainnet`) | Same class as Infura / `api.knsdomains.org`. kns-spec REAL.md item 5 |
| WalletConnect | CSP `connect-src` includes `wss://relay.walletconnect.org` | Third-party relay sees session metadata |
| SuperTypo infra | CSP allows `*.kaspa.blue/green/red/stream` | The same operator as the registry |
| Unsalted `blake3(name)` | developer docs | Watcher who sees a key can race a split under their own claim (docs admit this; live deeds are not reachable this way) |
| Activate args in mempool | developer docs | Name is public before confirm; copied verbatim funds the victim; swapped owner is an unsatisfiable claim |
| Profile / cards | card output is chain-visible | Do not put email on a card. kns-spec already said this |
| Developer HTML | `/developers` is empty without JS | Integrators and auditors who curl get nothing |
| npm → missing git | `repository.url` = `github.com/supertypo/dotk` | Supply-chain: you can install binaries, you cannot read the Silverscript they encode |

## Code asked for (not found)

See [ASK-FOR-CODE.md](ASK-FOR-CODE.md). Short list:

- `github.com/supertypo/dotk` (tweet 9/12: directory, CLI, covenant)
- `sil/DotkGap.sil`, `sil/DotkDeed.sil` matching the published template hashes
- silverc commit that produced `compiler_version: 0.1.0`
- Indexer/directory source that serves `/v1`

Until those exist, uniqueness is **reproducible in principle** (SDK + a node) and **not reviewable as source**.

## Improvement (DOTK, not the mix)

1. **Publish the repo** the npm field already names. Pin template hashes to source + silverc commit.
2. Put `/developers` in HTML or `llms.txt`. The protocol is good; hiding it in a Vue chunk is a self-own.
3. Document the honest sentence: *unique inside lineage `ee2128c0…`, not a consensus TLD.*
4. Expose `covenant_id` on a public UTXO probe, or tell wallets they **must** use wRPC. `api.kaspa.org` is not enough.
5. Grapheme pricing, or say you price UTF-8 bytes and emoji will surprise people.
6. Separate the public directory from kaspa.stream / WalletConnect defaults. kns-spec: don’t log lookups.
7. Evict → devfund is an incentive. Write the griefing math (36 KAS deposit, 5 min, who runs the bot).
8. iOS: the launch thread already admits there is no wallet. Don’t call the webapp universal.
9. **Work with KNS.** KNS minters will likely not appreciate a competing TLD. Bind, don’t alias. [RISK.md](RISK.md).

The mix with KNS is a different GitHub: [STP-KAS/kns-dotk](https://github.com/STP-KAS/kns-dotk).

## Sources

[SOURCES.md](SOURCES.md). SuperTypo: [SUPERTYPO.md](SUPERTYPO.md). Flaws list: [FLAWS.md](FLAWS.md). Community: [RISK.md](RISK.md). kns-spec checklist: [CONFORMANCE.md](CONFORMANCE.md).

## For the KNS team

Read this pass for the mechanism. The lesson — what to take from DOTK, from covenants, and from the inscription lab — is [FOR-KNS.md](https://github.com/STP-KAS/kns-tn10-testing/blob/main/FOR-KNS.md).

**This is not an audit.** A real audit needs the `.sil` sources, the silverc commit, reorg tests, and someone who is paid to break `split` / `evict` / mass. We did not do that.

## License

MIT. No warranty. **Not an audit.** Not financial advice. Not Kaspa core. Not official KNS. Not SuperTypo.

---

> **Standard disclaimer.** This GitHub, not the topic above.
>
> Intentions are good; thought process is questionable. STP remains delusional. Si vis pacem, para bellum.
>
> Intern at https://sixpack.wtf/  
> X: https://x.com/StppStp · GitHub: https://github.com/STP-KAS
