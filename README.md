# clamp-reporter

A scheduled reporter for the Clamp Index on Solana devnet.

Every 15 minutes this workflow runs `reporter.mjs`, which:

1. fetches the public GPU rental prices of Vast.ai, RunPod, Akash and Nosana,
2. uploads each raw API answer to the Clamp archive under its SHA-256 (signed with the reporter key),
3. sends `submit_report` to the Clamp program with the prices, capacities and raw hashes.

The program combines the reports of several reporters (a median per source, then a weighted median across sources) and records the index on-chain. Anyone can download a raw file by its hash, hash it again, recompute the price with the public source rules and compare all three with the chain.

This reporter is run by the Clamp team. It is one of three reporters on separate platforms with separate keys.

- Network: Solana devnet only
- Program: `wXKbfiz8yqTgGksXC5ZpN77CzXgW77ttcqHxnpqMrhC`
- Archive: `https://qsszurelcfrzlswkhnkd.supabase.co/storage/v1/object/public/raw/<sha256>.json`
- `reporter.mjs` is a build artifact of the Clamp reporter code (bundled with esbuild). It needs one secret, `REPORTER_KEYPAIR`, and no other credential.
