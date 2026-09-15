# Sources

Checked 15 Sep 2026. Live JSON snapshots under `live/`.

## DOTK (product)

- https://dotk.name/developers — HTML title + noscript; body is Vue
- https://dotk.name/integrators , `/why`, `/next`, `/names`, `/keyspace` (JS)
- https://dotk.name/sitemap.xml
- https://dotk.name/robots.txt
- App version meta: `a262f2b6f4c7026995508671f6f0e13ed4af166e`
- Assets: `/assets/Developers-CDbB7ZL7.js`, `proofMarks-D563kBIc.js`, `constants-D0F08168.js`, `dotk_wasm-CSPj7aZS.js`
- CSP / JSON-LD from the HTML response headers and head

## Directory

- https://api.dotk.name/v1 — OpenAPI 3.1.0 in-page
- https://api.dotk.name/v1/health
- https://api.dotk.name/v1/health?detail=true
- https://api.dotk.name/v1/genesis
- https://api.dotk.name/v1/keyspace
- https://api.dotk.name/v1/names/supertypo
- https://api.dotk.name/v1/names/kaspa
- https://api.dotk.name/v1/names/kns.k → not_found

## npm (compiled; git missing)

- https://www.npmjs.com/package/@dotk/sdk
- https://www.npmjs.com/package/@dotk/sdk-tx
- https://cdn.jsdelivr.net/npm/@dotk/sdk@1.0.0/README.md
- https://cdn.jsdelivr.net/npm/@dotk/sdk@1.0.0/dist/index.d.ts
- https://cdn.jsdelivr.net/npm/@dotk/sdk@1.0.0/dist/deployments.js
- https://cdn.jsdelivr.net/npm/@dotk/sdk-tx@1.0.0/README.md
- gitHead `5834a71bf7840fb6f820a4e8fe8452806c1d75eb`

## Chain

- https://api.kaspa.org/transactions/e077087a4761098dcb55a953057b4a92aadf0f834c7df85f53c8bae8634d5d10 (authorizing outpoint)
- https://api.kaspa.org/transactions/52f60e696eccc00316aabb32af09ad577310e5fd3246966754dee4fe7b5b3e12 (`supertypo.k` deed)
- https://api.kaspa.org/addresses/kaspa:ppqjpuxrrpgfgtshwfvkc8apwtfp95ugakuhg2yet93g60lzryqp2skze6cpt/utxos
- https://api.kaspa.org/addresses/kaspa:qzaarz9u2qfe6a6tt04j39pej8tk9mhrntjhfaymvwelucq9wclvyneumu0u3/utxos

## SuperTypo

- https://github.com/supertypo
- https://api.github.com/users/supertypo/repos?per_page=100
- https://github.com/supertypo/simply-kaspa-indexer
- https://github.com/supertypo/dotk → 404
- X thread https://x.com/supertypo_kas/status/2099780606674538685 (1/12 … 12/12)
- https://x.com/supertypo_kas/status/2099818408833433663 (prove recipe)
- https://x.com/supertypo_kas/status/2099820396304314631 (KNS closed shop)
- https://x.com/supertypo_kas/status/2099834877432447201 (on-chain names not unique)

## KNS / kns-spec (the other object)

- https://github.com/STP-KAS/kns-spec
- https://stp-kas.github.io/kns-spec/
- https://kns-2.gitbook.io/kns-docs-1/inscriptions/overview
- https://api.knsdomains.org/mainnet/api/v1/kns.kas/owner
- https://api.knsdomains.org/mainnet/api/v1/supertypo.kas/owner
- https://api.knsdomains.org/mainnet/api/v1/kaspa.kas/owner
- https://x.com/knsdomain/status/2091799253119304112 (KNS exploring covenant domains, 24 Aug 2026)

## This desk

- Sister mix: https://github.com/STP-KAS/kns-dotk
- Prior independent-review shape: https://github.com/STP-KAS/kusdt-bitcoffee
