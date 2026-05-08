---
type: community
cohesion: 1.00
members: 2
---

# README/Code Driver Drift

**Cohesion:** 1.00 - tightly connected
**Members:** 2 nodes

## Members
- [[Drift README claims glebarezsqlite, code uses gorm.iodriversqlite]] - rationale - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[open_sqlite3.go uses gorm.iodriversqlite while README cites glebarez (drift)]] - rationale - x_fork.tree-20260506.md

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/README/Code_Driver_Drift
SORT file.name ASC
```
