---
type: community
cohesion: 1.00
members: 2
---

# Cross-DB Parity Principle

**Cohesion:** 1.00 - tightly connected
**Members:** 2 nodes

## Members
- [[AC-011 driver-specific code stays in open.go  open_sqlite3.go]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Constitution Principle II - Cross-Database Parity]] - rationale - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Cross-DB_Parity_Principle
SORT file.name ASC
```
