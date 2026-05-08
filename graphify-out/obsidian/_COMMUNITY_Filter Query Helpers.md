---
type: community
cohesion: 0.50
members: 4
---

# Filter Query Helpers

**Cohesion:** 0.50 - moderately connected
**Members:** 4 nodes

## Members
- [[Adapter.RemoveFilteredPolicy]] - code - adapter.go
- [[Adapter.dropTable]] - code - adapter.go
- [[Adapter.getTableInstance]] - code - adapter.go
- [[checkQueryField]] - code - adapter.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Filter_Query_Helpers
SORT file.name ASC
```

## Connections to other communities
- 2 edges to [[_COMMUNITY_Batch & Update CRUD]]
- 2 edges to [[_COMMUNITY_CasbinRule Schema & Queries]]
- 2 edges to [[_COMMUNITY_Persist & LoadPolicy Path]]
- 1 edge to [[_COMMUNITY_AutoMigrate Discipline]]

## Top bridge nodes
- [[Adapter.getTableInstance]] - degree 6, connects to 3 communities
- [[Adapter.RemoveFilteredPolicy]] - degree 5, connects to 2 communities