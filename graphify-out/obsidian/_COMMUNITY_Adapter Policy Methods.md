---
type: community
cohesion: 0.22
members: 20
---

# Adapter Policy Methods

**Cohesion:** 0.22 - loosely connected
**Members:** 20 nodes

## Members
- [[.AddLogger()]] - code - adapter.go
- [[.AddPolicy()]] - code - adapter.go
- [[.IsFiltered()]] - code - adapter.go
- [[.RemoveFilteredPolicy()]] - code - adapter.go
- [[.RemovePolicies()]] - code - adapter.go
- [[.RemovePolicy()]] - code - adapter.go
- [[.SavePolicy()]] - code - adapter.go
- [[.UpdateFilteredPolicies()]] - code - adapter.go
- [[.UpdatePolicies()]] - code - adapter.go
- [[.UpdatePolicy()]] - code - adapter.go
- [[.createTable()]] - code - adapter.go
- [[.dropTable()]] - code - adapter.go
- [[.getFullTableName()]] - code - adapter.go
- [[.getTableInstance()]] - code - adapter.go
- [[.rawDelete()]] - code - adapter.go
- [[.savePolicyLine()]] - code - adapter.go
- [[.truncateTable()]] - code - adapter.go
- [[Adapter]] - code - adapter.go
- [[TestNilField()]] - code - adapter_test.go
- [[initAdapterWithoutAutoMigrate()]] - code - adapter_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Adapter_Policy_Methods
SORT file.name ASC
```

## Connections to other communities
- 17 edges to [[_COMMUNITY_Test Suite & Adapter Init]]
- 8 edges to [[_COMMUNITY_Adapter Construction & DB Open]]
- 3 edges to [[_COMMUNITY_Multi-DB Pool & Lifecycle]]
- 3 edges to [[_COMMUNITY_CasbinRule Model & Policy CRUD]]
- 2 edges to [[_COMMUNITY_Filtered Policy Loading]]

## Top bridge nodes
- [[Adapter]] - degree 27, connects to 4 communities
- [[initAdapterWithoutAutoMigrate()]] - degree 8, connects to 2 communities
- [[.UpdateFilteredPolicies()]] - degree 6, connects to 2 communities
- [[.RemoveFilteredPolicy()]] - degree 5, connects to 2 communities
- [[.savePolicyLine()]] - degree 10, connects to 1 community