# DOTK vs kns-spec CONFORMANCE

kns-spec [CONFORMANCE.md](https://github.com/STP-KAS/kns-spec/blob/main/CONFORMANCE.md) is the implementer contract for **KNS `.kas`**. DOTK is not KNS. This table is “if a wallet treated DOTK as KNS, what breaks” plus “which kns-spec lessons DOTK already absorbed.”

## MUST (KNS) — does DOTK match?

| # | KNS MUST | DOTK |
| --- | --- | --- |
| 1 | URL-encode domains in API paths | Names are `[a-z0-9-]{1,32}`. Path `/v1/names/{name}` — encoding still required for safety; charset is tighter than KNS |
| 2 | ENS-normalize (UTS-46) | SDK folds case, trims, strips `.k`. **Not `@adraffy/ens-normalize`.** Homographs are a leftover risk |
| 3 | Price with graphemes | **No.** UTF-8 byte length, five tiers |
| 4 | `POST /domains/check` before create | Different: `available` / `lookup` on the directory or a gap probe. Two-phase commit. Losing split still burns fees |
| 5 | Reveal output 0 pays protocol address | Activate output 1 pays **baked devfund**, floor = tier |
| 6 | Wallet holds domain × 1.05 KAS | Bond 1 + deposit 36 + fee + two gap values. SDK-tx measures mass before sign. **Show the plan.** SuperTypo: always check deducted amount |
| 7 | Resolve warning before send | SDK README is careful (`addressFor` vs `lookup`). The **webapp** must still show the kaspa: address. Not verified here in a browser |
| 8 | Show resolved `kaspa:` | SDK `addressFor`. Covenant-owned → null |
| 9 | No ECDSA addresses | **DOTK allows ECDSA.** Opposite of KNS |
| 10 | Non-supporting wallet warning | KasWare, Kastle, Kaspire (Android). No iOS |
| 11 | Kastle mobile cannot inscribe | Different write path (covenant, not inscription). Kastle ext is listed |

## SHOULD (Web4) — absorbed?

| kns-spec SHOULD | DOTK |
| --- | --- |
| Profile keys `ipfs`, `kas`, … | Cards: ENSIP-5 keys + free text + `primary` boolean. **Better packing** than one inscription per field |
| One-shot resolve | `resolve(name)` → address + records + proven. **This is the API kns-spec asked KNS for** |
| Local resolve via simply-kaspa-indexer | Local resolve via **any node** + bundled manifest. Stronger, if the wallet actually passes `node` |
| Don’t iframe website as the dApp | Not a contenthash system yet |
| Clear profile on transfer | Cards are minted on transfer; old card is sweepable. Need to confirm the webapp offers clear |
| Payee ≠ owner | `primary` record + `addressFor`. Good |

## MUST NOT (kns-spec)

| kns-spec | DOTK |
| --- | --- |
| Claim consensus uniqueness of `.kas` | Claims it for `.k`. **Same overclaim, better mechanism** |
| Treat multi-dot as parent-child | Flat blake3. Same trap, different TLD |
| Ask for a seed | Webapp uses injected wallets. Not re-tested for a fake seed prompt |
| Public peer as privacy | N/A |

## KasName.sil vs DotkDeed

`KasName.sil` (kns-spec, silverc v1.0.0): owner + `sha256("kns/v1/" \|\| label)`. Continuation keeps sompi. **No keyspace covering.** Anyone can genesis another alice.

`DotkDeed.sil` (unpublished, ABI 0.1.0): status, key, ownerType, owner, name. Uniqueness lives in **DotkGap**, not in the deed. That is the design kns-spec said was missing.

Do not “elevate” a KNS inscription by deploying KasName.sil and calling it DOTK. Different TLD, different lineage, different compiler pin.
