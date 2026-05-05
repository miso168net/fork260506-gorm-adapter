---
type: community
cohesion: 0.18
members: 16
---

# Multi-DB Pool & Lifecycle

**Cohesion:** 0.18 - loosely connected
**Members:** 16 nodes

## Members
- [[.Close()]] - code - adapter.go
- [[.Resolve()]] - code - adapter.go
- [[.switchDb()]] - code - adapter.go
- [[Adapter.Close]] - code - adapter.go
- [[DbPool]] - code - adapter.go
- [[Fork main branch origin record]] - document - x_fork.branch-origin.md
- [[InitDbResolver()]] - code - adapter.go
- [[NewAdapter()]] - code - adapter.go
- [[NewAdapterByMulDb()]] - code - adapter.go
- [[NewFilteredAdapter()]] - code - adapter.go
- [[README simple example]] - document - README.md
- [[TestAdapterWithMulDb]] - code - adapter_test.go
- [[TestNilField]] - code - adapter_test.go
- [[adapter.go]] - code - adapter.go
- [[finalizer()]] - code - adapter.go
- [[specificPolicy]] - code - adapter.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Multi-DB_Pool_&_Lifecycle
SORT file.name ASC
```

## Connections to other communities
- 9 edges to [[_COMMUNITY_Adapter Construction & DB Open]]
- 3 edges to [[_COMMUNITY_CasbinRule Model & Policy CRUD]]
- 3 edges to [[_COMMUNITY_Filtered Policy Loading]]
- 3 edges to [[_COMMUNITY_Adapter Policy Methods]]
- 3 edges to [[_COMMUNITY_Test Suite & Adapter Init]]

## Top bridge nodes
- [[adapter.go]] - degree 18, connects to 4 communities
- [[NewAdapter()]] - degree 9, connects to 2 communities
- [[InitDbResolver()]] - degree 7, connects to 2 communities
- [[NewAdapterByMulDb()]] - degree 4, connects to 2 communities
- [[finalizer()]] - degree 5, connects to 1 community