---
type: community
cohesion: 0.67
members: 4
---

# DB Open Internals

**Cohesion:** 0.67 - moderately connected
**Members:** 4 nodes

## Members
- [[Adapter.createDatabase]] - code - adapter.go
- [[openDBConnection]] - code - adapter.go
- [[opens dialect map (no sqlite)]] - code - open.go
- [[opens dialect map (with sqlite)]] - code - open_sqlite3.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/DB_Open_Internals
SORT file.name ASC
```

## Connections to other communities
- 2 edges to [[_COMMUNITY_Driver Switch & Convergence]]

## Top bridge nodes
- [[openDBConnection]] - degree 4, connects to 1 community
- [[Adapter.createDatabase]] - degree 2, connects to 1 community