# Flaws, leaks, overclaims

**Not an audit.** Independent list from public surfaces, for the KNS team. Severity is for a wallet/integrator, not a CVSS.

## Overclaims

| Claim | Reality |
| --- | --- |
| “Uniqueness enforced by consensus, not by a registrar” (site tagline) | Enforced by **this lineage’s gap UTXOs**. Consensus does not know `.k`. A second deployment with different template constants is a second TLD |
| “unique, trustless, decentralized” (X 1/12) | Unique *inside* `ee2128c0…`. Trust the **template pin** (devfund, fees). Directory is still his host unless you bring a node |
| JSON-LD `sameAs` GitHub | 404 |
| “SDKs … already out” (X 8/12) | True for npm. Source repo the packages name is missing |
| Developer page “What the covenants enforce” | True as an essay. False as crawler HTML |

## Protocol / economic

1. **Evict pays the deposit to the devfund; remainder is bounty.** `t_evict = 3000` DAA (~5 minutes). A PENDING name that fails to activate is a 36 KAS gift + 1 KAS gap accounting. Griefing and MEV on the activate race belong in an audit, not a tweet.
2. **Unsalted key.** Docs: a dictionary word is recognizable; a watcher who recovers a key can race a split under a claim only they can activate. Live deeds are not stealable this way. **Unregistered popular names are.**
3. **Split mass.** Docs: split is the protocol’s tightest transaction against KIP-9 storage mass (two gaps out). `gap_value` is the floor that decides whether registration relays at all. If 10 bps mass policy moves, registrations stall until a new deployment.
4. **Upgrade = new namespace.** Baked constants. No migration path for `kaspa.k` if the template is wrong.
5. **Cards are not proved by the indexer.** OpenAPI: “The indexer proves nothing about a card.” SDK: without a node, `proven` is null and you take the API’s word. A wallet that only calls `/v1/names/{name}` can show a spoofed card.
6. **Covenant-owned names.** SDK `addressFor` returns null when a covenant owns the name (nothing to pay). Easy to mishandle in a send box.
7. **Two-step register.** Commit (split) then reveal (activate). Worse UX than KNS’s single reveal; better privacy of the name until activate. PENDING is a new failure mode KNS does not have.
8. **UTF-8 length, not graphemes.** kns-spec MUST #3. Rainbow flag is 1 grapheme for KNS and many bytes here. Pricing disagreement is a product bug waiting for emoji domains.
9. **ECDSA owners.** DOTK allows them (KCC-2 + local y-parity). KNS MUST NOT ECDSA. Wallets that mix the two will send to the wrong class of address if they assume KNS rules.
10. **Compiler 0.1.0 vs official silverc v1.0.0.** kns-spec compiles `KasName.sil` with Ori’s 9 Sep 2026 v1.0.0. DOTK ABI says 0.1.0. Until source + compiler commit, treat bytecode as opaque.

## Product / ops

11. **No iOS wallet** (X 7/12; also a typo `dock.name` in that tweet).
12. **Default directory is centralized**, even if answers are self-proving in theory.
13. **`api.kaspa.org` UTXO objects omit `covenant_id`.** The “query `utxos_by_addresses`” proof SuperTypo posted ([integrators#prove](https://dotk.name/integrators#prove)) needs a node that returns it. Public REST is not that node.
14. **257 names / 2 pending / 585 history events** on launch day. Squatting is the expected FCFS outcome. No reserved list (KNS had a merkle reserved list at launch).
15. **CSP `wasm-unsafe-eval`.** Expected for WASM. Still a browser attack surface.
16. **`Access-Control-Allow-Origin: *`** on HTML. Directory CORS is a separate question; the SDK is designed to be called from wallets.

## Compared to kns-spec MUST NOT

- DOTK does **not** claim indexer FCFS for `.k`. Good.
- DOTK **does** claim consensus uniqueness in the tagline. Too strong.
- Neither has hierarchical subnames. DOTK `blake3(name)` is flat. `opus.dei.k` would be a different key, not a child of `dei.k`. Same class of trap as KNS multi-dot inscriptions.

## Community / political

17. **KNS minters will likely not appreciate this.** Owner note: people who already minted `.kas` paid fees and expect those names to be the names. Launching `.k` the same day as a “closed shop” critique of KNS is technically fair and socially explosive. This desk understands the uniqueness initiative. **Advice: work with KNS.** Bind, don’t alias. Full note: [RISK.md](RISK.md).
