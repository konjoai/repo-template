# Konjo Code Quality Framework
## Three Walls Against AI Slop

**Scope:** All KonjoAI repositories

Wall 1: Pre-Commit Hook — local, blocks the commit
Wall 2: CI Gate — GitHub Actions + KIBAN, blocks the merge
Wall 3: Konjo Review Agent — Claude, blocks the merge (run locally until enabled in CI)

See the KonjoAI internal spec repo for the full specification.
