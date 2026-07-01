# Contributing

Thanks for your interest in contributing!

## Getting started

1. Fork and clone the repo.
2. Install the Konjo Quality Framework's pre-commit hook:
   ```bash
   bash .konjo/scripts/install-hooks.sh
   ```
3. <!-- TODO: language-specific setup, e.g. `pip install -e ".[dev]"`, `cargo build`, `npm install` -->

## Running tests

<!-- TODO: e.g. `cargo test`, `pytest`, `npm test` -->

## Linting and formatting

<!-- TODO: e.g. `cargo clippy -- -D warnings`, `ruff check .`, `eslint .` -->

## What makes a good PR

- **Focused** — one logical change per PR.
- **Tests pass** — CI green before requesting review.
- **Wall 1 clean** — the pre-commit hook (`.konjo/hooks/pre-commit`) passes.
- **No secrets or generated artifacts committed.**
- **CHANGELOG updated**, if this repo keeps one.

## Reporting bugs

Use [GitHub Issues](../../issues) with the **Bug report** template.

## License

By contributing you agree that your contributions will be licensed under
this repository's [LICENSE](LICENSE).
