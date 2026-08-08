# Pi package migration log

Target: published stable `0.84.1`, excluding `/tmp/pi_src` `Unreleased` changes. The npm version listing contained no published `0.80.0` or `0.80.4`, so those source tags were not release checkpoints. All checkpoints used Node `v24.19.0`, the three direct pi packages were advanced together, and the focused gate was `bun test test/unit/` followed by build, typecheck, Biome, and Oxlint. The package manager overrides kept pi's related transitive `pi-agent-core` and `pi-tui` releases aligned while testing historical checkpoints; the final direct TypeBox dependency is also aligned to pi 0.84's `1.3.7` requirement.

| Release | Result | Notes |
|---|---|---|
| 0.74.1 | green | 275 unit tests; build/typecheck/lint green |
| 0.74.2 | green | 275 unit tests; build/typecheck/lint green |
| 0.75.0 | green | 275 unit tests; build/typecheck/lint green |
| 0.75.1 | green | 275 unit tests; build/typecheck/lint green |
| 0.75.2 | green | 275 unit tests; build/typecheck/lint green |
| 0.75.3 | green | 275 unit tests; build/typecheck/lint green |
| 0.75.4 | green | 275 unit tests; build/typecheck/lint green |
| 0.75.5 | green | 275 unit tests; build/typecheck/lint green |
| 0.76.0 | green | 275 unit tests; build/typecheck/lint green |
| 0.77.0 | green | 275 unit tests; build/typecheck/lint green |
| 0.78.0 | green | 275 unit tests; build/typecheck/lint green |
| 0.78.1 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.0 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.1 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.2 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.3 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.4 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.5 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.6 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.7 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.8 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.9 | green | 275 unit tests; build/typecheck/lint green |
| 0.79.10 | green | 275 unit tests; build/typecheck/lint green |
| 0.80.1 | green | Migrated `pi-ai` global helpers to `/compat`; 275 unit tests; gates green |
| 0.80.2 | green | Aligned transitive `pi-agent-core`/`pi-ai`; 275 unit tests; gates green |
| 0.80.3 | green | 275 unit tests; build/typecheck/lint green |
| 0.80.5 | green | 275 unit tests; build/typecheck/lint green |
| 0.80.6 | green | 275 unit tests; build/typecheck/lint green |
| 0.80.7 | green | 275 unit tests; build/typecheck/lint green |
| 0.80.8 | green | Migrated `AuthStorage` setup to async `ModelRuntime`; unit, integration, and SDK conformance gates green |
| 0.80.9 | green | 275 unit tests; build/typecheck/lint green |
| 0.80.10 | green | 275 unit tests; build/typecheck/lint green |
| 0.81.0 | green | 275 unit tests; build/typecheck/lint green |
| 0.81.1 | green | 275 unit tests; build/typecheck/lint green |
| 0.82.0 | green | 275 unit tests; build/typecheck/lint green |
| 0.82.1 | green | 275 unit tests; build/typecheck/lint green |
| 0.83.0 | green | Added `pending` stop-reason mapping; 276 unit tests; final gates green |
| 0.84.0 | green | Added `deferred` stop-reason mapping, forwarded auth-resolved base URLs, and refreshed extension model catalogs; 310 CI tests; build/typecheck green |
| 0.84.1 | green | Published patch checkpoint; 310 CI tests; build/typecheck green |

## Final evidence

- `pnpm test` (30s per-test timeout for real-provider conformance): **317 passed, 0 failed**, 1,270 assertions across 22 files.
- `pnpm run test:ci`: **310 passed, 0 failed**, 1,217 assertions across 18 files.
- `pnpm run typecheck`: passed.
- `pnpm run lint:biome` and `pnpm run lint:oxlint`: passed.
- `pnpm run build`: passed; all package entrypoints generated, and `bun dist/index.mjs --help` passed.
- `pnpm install --frozen-lockfile`: passed with direct pi packages at `0.84.1`.
- `GET /v1/models`, encoded model lookup, chat validation, streaming, tools, auth, and security conformance passed at 0.84.1.

The configured aggregate lint command was also run through pnpm's CLI entrypoint and passed.
