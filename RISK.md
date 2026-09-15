# Community risk

**Not an audit.** Owner note, 15 Sep 2026.

## Risk

Kaspa community who have minted KNS domains will likely not appreciate the effort.

DOTK launched a live `.k` registry the same day SuperTypo called knsdomains a closed shop. People already paid KNS fees, hold `.kas` inscriptions, and type those names in wallets. A competing TLD will read as a raid on that installed base, even when the uniqueness engineering is real.

## Initiative

This desk understands the initiative. SuperTypo is right that KNS uniqueness is an indexer rule, not a node rule. Gap covering of `blake3(name)` is the uniqueness KNS never had.

That does not make a second TLD welcome to the people who already minted.

## Advice: work with KNS

Do not ship a silent second namespace as the default. Bind, don’t alias. If uniqueness v2 happens, it should be **with** the installed `.kas` base, not against it.

- Keep `.kas` as the human string.
- Offer a bind (owner of `alice.kas` may mint a v2 deed). Never auto-map `.kas` → `.k` (`supertypo.kas` ≠ `supertypo.k` on 15 Sep 2026).
- Publish `github.com/supertypo/dotk` and the `.sil` sources.
- Do not take fees on a competing TLD and call that “fixing KNS.”

Sister mix: [STP-KAS/kns-dotk](https://github.com/STP-KAS/kns-dotk).
