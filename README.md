# repo-template

📃 The starting point for new KonjoAI repos — Konjo Code Quality Framework,
KIBAN CI gates, and the license/legal/community boilerplate every repo needs,
already wired together.

## Using this template

1. Click **Use this template** → **Create a new repository**.
2. Fill in the placeholders (search for `TODO` and `<...>`):
   - `LICENSE` — licensor name, project name, change date, change license.
   - `.konjo/profile.yml` — `repo:`, `stack:`, `packs:` (see below).
   - `SECURITY.md` — supported versions, contact method.
   - `CODE_OF_CONDUCT.md` — contact email.
3. Run `bash .konjo/scripts/install-hooks.sh` to install the Wall 1 pre-commit hook.
4. In the new repo's **Settings → General → Pull Requests**, turn on
   **"Automatically delete head branches."** This is a per-repository GitHub
   setting — it is not carried over by "Use this template" and can't be set
   through a template file, so it has to be flipped by hand in every new repo.
5. Delete this section once you're set up.

## Konjo Quality Framework

Three walls against AI slop — see [`KONJO_QUALITY_FRAMEWORK.md`](KONJO_QUALITY_FRAMEWORK.md).

- **Wall 1 — Pre-commit** (`.konjo/hooks/pre-commit`, installed via
  `.konjo/scripts/install-hooks.sh`): language-aware — it only runs Rust
  checks if it finds a `Cargo.toml`, Python checks if it finds a
  `pyproject.toml`/`requirements.txt`, etc. Blocks the commit.
- **Wall 2 — CI gate** (`.github/workflows/konjo-gates.yml`): installs the
  pinned [KIBAN](#what-is-kiban) distribution and runs `konjo-gates` against
  `.konjo/profile.yml`. Blocks the merge.
- **Wall 3 — Adversarial review** (`.konjo/scripts/konjo_review.py`, local
  only, disabled in CI by default): `git diff HEAD~1 | python3 .konjo/scripts/konjo_review.py`.

### What is KIBAN?

KIBAN is the versioned engine that Wall 2 installs and runs (`pip install
"kiban @ git+https://github.com/konjoai/kiban.git@<ref>"`). It ships the gate
logic and eval cassettes as one pinned package, so CI never depends on local
state — only on `.konjo/kiban.ref` and `.konjo/profile.yml`.

**Do you need to know the language before wiring it up?** Partially:

- Wall 1 (the pre-commit hook) and the DRY/review scripts are already
  cross-language — they detect what's present (`Cargo.toml`, `pyproject.toml`,
  `package.json`, `pixi.toml`, ...) and skip what isn't.
- Wall 2 needs `.konjo/profile.yml` to declare `stack:` and `packs:` (e.g.
  `lang/rust`, `lang/python`, `lang/typescript`, `lang/mojo`, `lang/go`) so
  KIBAN knows which language packs' gates, complexity rules, and specialist
  review lanes to run. That can't be filled in generically — it has to match
  whatever the new repo actually builds.
- The `.github/workflows/konjo-gates.yml` shipped here only unconditionally
  sets up Python (KIBAN itself is a pip package). It conditionally installs a
  Rust toolchain / Node if it detects `Cargo.toml` / `package.json` in the
  repo, so most stacks work without editing the workflow — just fill in
  `profile.yml` and it picks up the rest.

So: you don't need to know the language to *drop the template in*, but you do
need to know it before Wall 2 will actually run meaningful gates — fill in
`profile.yml` once the stack is decided.

## License

[Business Source License 1.1](LICENSE) — converts to the stated Change
License on the Change Date. Fill in the licensor/parameters block before
first release.
