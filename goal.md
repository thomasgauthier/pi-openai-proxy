# Incremental pi dependency upgrade

/goal Outcome: Upgrade `@earendil-works/pi-ai`, `@earendil-works/pi-coding-agent`, and `@earendil-works/pi-tui` from the current locked `0.74.0` line to the latest published stable pi release available at execution time, while preserving pi-openai-proxy behavior and keeping the repository healthy.

Context: The repository currently uses pi `0.74.0`; `/tmp/pi_src` contains substantially newer pi releases and unreleased changes. Treat this as a compatibility migration, not a bulk version bump. Do not depend on `Unreleased` source changes unless explicitly required.

Boundaries: Work in this repository and its dependency lockfile. Enumerate the published pi release sequence from the current version to the target, then process every release in order, including patch releases where applicable. Update the three pi packages together for each release; update only directly related peer/types/tooling dependencies when the release requires it. Fix migration issues in `src/`, `extensions/`, and tests. Preserve the stable HTTP API, auth/header semantics, model-ID behavior, security boundaries, and existing hook/tooling policy. Do not upgrade unrelated dependencies, weaken validation, remove tests, or skip a release because it appears small.

Constraints: Use an incremental TDD loop for every release: establish or confirm the relevant failing/passing test, make the smallest dependency or compatibility change, run the focused test, then run typecheck, lint, and build before advancing. Keep each release change reviewable; do not combine multiple release migrations into one step. Preserve meaningful test coverage. Use Node >=24 for verification; clearly distinguish environment failures from migration regressions.

Verify: First record a baseline with `pnpm run typecheck`, `pnpm run lint`, `pnpm test`, and `pnpm run build`. At every release checkpoint, require the lockfile to resolve the intended pi versions and require focused tests plus typecheck, lint, and build to pass. At the final target, run the full test suite and build, inspect the diff for accidental unrelated changes, and verify the stable endpoints and package entrypoints remain intact. Record each release, failures, fixes, and evidence in this file's checkpoint table or an adjacent migration log.

Iterate/done/stop: After each checkpoint, choose the next release only if the current one is green. If a check fails, isolate whether it is a pi breaking change, proxy bug, dependency/tooling issue, or environment issue; add a regression test before fixing proxy behavior, then rerun the checkpoint. Done only when every published release in sequence has been processed, the final stable target passes all gates, and no known migration work remains. Stop and report the exact release, failure, evidence, and required decision if a release cannot be verified or requires an incompatible API/security change.

## Checkpoint ledger

| Release | Dependency versions | Focused test/result | Typecheck | Lint | Build | Status |
|---|---|---|---|---|---|---|
| Baseline 0.74.0 | 0.74.0 / 0.74.0 / 0.74.0 | 313 pass, 2 upstream calls exceeded Bun's 5s default | pass (Node v24.19.0, after build) | passed after aligning Biome schema to installed CLI | pass (Node v24.19.0) | recorded; resolved before final |

Per-release evidence and final verification: [`PI-MIGRATION-LOG.md`](PI-MIGRATION-LOG.md).
