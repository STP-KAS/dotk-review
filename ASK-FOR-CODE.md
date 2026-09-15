# Ask for the code

**Not an audit.** [@supertypo](https://github.com/supertypo) — collaborator invite is on this repo. This pass could not find the source the product claims. A second pass against `.sil` is still not an audit.

## What is advertised

| Claim | Where | What we got |
| --- | --- | --- |
| `https://github.com/supertypo/dotk` | JSON-LD on [dotk.name/developers](https://dotk.name/developers) (`sameAs`) | **404** (GitHub HTML and `api.github.com/repos/supertypo/dotk`) |
| “dotk will be open source — directory (indexer/api), cli tools and the covenant itself” | SuperTypo [9/12](https://x.com/supertypo_kas/status/2099780625074938022) 15 Sep 2026 08:41 UTC | Promise. Repo still missing the same day |
| npm `repository.url` = `git+https://github.com/supertypo/dotk.git` | `@dotk/sdk@1.0.0`, `@dotk/sdk-tx@1.0.0` | Packages install. Git does not |
| `sil/DotkGap.sil`, `sil/DotkDeed.sil` | `/v1/genesis` ABI `source_path` | Paths only. No files |
| `docs/CARDS.md` | OpenAPI `CardOut` description | Not published |

npm `gitHead` on both packages: `5834a71bf7840fb6f820a4e8fe8452806c1d75eb`. That commit is not on a public GitHub.

## What to send

If you are SuperTypo, or anyone with the tree: publish or mail the following. This desk will re-run the review against source.

1. **Git repo** at `github.com/supertypo/dotk` (or a public mirror). Tag the npm 1.0.0 tree.
2. **Covenant source** `sil/DotkGap.sil` + `sil/DotkDeed.sil` that compile to:
   - gap template `ba1e7b8e2dfda606a902c89437625b1c31f82668cd8cfdc7cf365a8ad77c5a3d`
   - deed template `238a8d0a5af1ea136d50dd49973487929b8e713a84f1bd1650e97776b9a3f5a0`
3. **Compiler**: silverc commit for ABI `compiler_version: "0.1.0"`. kns-spec pins official **v1.0.0** `3ed9733`. These may not be the same binary.
4. **Directory/indexer** that serves `https://api.dotk.name/v1` (the self-test, snapshot, journal).
5. **Build recipe**: how `generated/mainnet/genesis.js` in `@dotk/sdk` is produced from the manifest.

Until then: the **SDK is inspectable** (compiled JS on npm). The **Silverscript is not**. A template hash without source is a pin, not a review.

## What we already have (not a substitute)

- Live OpenAPI + genesis bytecode arrays (ABI, not `.sil`)
- `@dotk/sdk` / `@dotk/sdk-tx` dist + README + `.d.ts`
- Minified Vue app + WASM glue at `dotk.name/assets/*`
- SuperTypo’s other public repos (indexer, docker, forks) — [SUPERTYPO.md](SUPERTYPO.md)

Contact on the OpenAPI: `suprtypo@pm.me` (spelling as published).
