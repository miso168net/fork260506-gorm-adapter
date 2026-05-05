---
type: community
cohesion: 0.19
members: 14
---

# Filtered Policy Loading

**Cohesion:** 0.19 - loosely connected
**Members:** 14 nodes

## Members
- [[.LoadFilteredPolicy()]] - code - adapter.go
- [[.filterQuery()]] - code - adapter.go
- [[Adapter.LoadFilteredPolicy]] - code - adapter.go
- [[Adapter.LoadPolicy]] - code - adapter.go
- [[Adapter.SavePolicy]] - code - adapter.go
- [[Adapter.filterQuery]] - code - adapter.go
- [[Adapter.truncateTable]] - code - adapter.go
- [[Filter]] - code - adapter.go
- [[TestAdapters]] - code - adapter_test.go
- [[initAdapter test helper]] - code - adapter_test.go
- [[initPolicy test helper]] - code - adapter_test.go
- [[loadPolicyLine()]] - code - adapter.go
- [[testFilteredPolicy]] - code - adapter_test.go
- [[testSaveLoad]] - code - adapter_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Filtered_Policy_Loading
SORT file.name ASC
```

## Connections to other communities
- 3 edges to [[_COMMUNITY_Multi-DB Pool & Lifecycle]]
- 3 edges to [[_COMMUNITY_CasbinRule Model & Policy CRUD]]
- 2 edges to [[_COMMUNITY_Adapter Policy Methods]]
- 2 edges to [[_COMMUNITY_Test Suite & Adapter Init]]
- 1 edge to [[_COMMUNITY_Adapter Construction & DB Open]]

## Top bridge nodes
- [[loadPolicyLine()]] - degree 6, connects to 3 communities
- [[.LoadFilteredPolicy()]] - degree 4, connects to 2 communities
- [[Filter]] - degree 4, connects to 1 community
- [[TestAdapters]] - degree 4, connects to 1 community
- [[Adapter.SavePolicy]] - degree 3, connects to 1 community