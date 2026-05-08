---
type: community
cohesion: 1.00
members: 2
---

# SQLite Build-Tag Drift

**Cohesion:** 1.00 - tightly connected
**Members:** 2 nodes

## Members
- [[Build-tag mutex between open.go and open_sqlite3.go]] - rationale - x_fork.tree-20260506.md
- [[Drift SQLite3 support is build-tag-conditional not unconditional]] - rationale - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/SQLite_Build-Tag_Drift
SORT file.name ASC
```
