---
type: community
cohesion: 0.16
members: 20
---

# CasbinRule Model & Policy CRUD

**Cohesion:** 0.16 - loosely connected
**Members:** 20 nodes

## Members
- [[.TableName()]] - code - adapter.go
- [[.queryString()]] - code - adapter.go
- [[.toStringPolicy()]] - code - adapter.go
- [[Adapter.AddPolicies]] - code - adapter.go
- [[Adapter.AddPolicy]] - code - adapter.go
- [[Adapter.RemoveFilteredPolicy]] - code - adapter.go
- [[Adapter.RemovePolicies]] - code - adapter.go
- [[Adapter.RemovePolicy]] - code - adapter.go
- [[Adapter.UpdateFilteredPolicies]] - code - adapter.go
- [[Adapter.UpdatePolicies]] - code - adapter.go
- [[Adapter.UpdatePolicy]] - code - adapter.go
- [[Adapter.dropTable]] - code - adapter.go
- [[Adapter.getTableInstance]] - code - adapter.go
- [[Adapter.rawDelete]] - code - adapter.go
- [[Adapter.savePolicyLine]] - code - adapter.go
- [[CasbinRule]] - code - adapter.go
- [[README v3.0.3 table rename migration note]] - document - README.md
- [[appendWhere()]] - code - adapter.go
- [[checkQueryField()]] - code - adapter.go
- [[testAutoSave]] - code - adapter_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/CasbinRule_Model_&_Policy_CRUD
SORT file.name ASC
```

## Connections to other communities
- 3 edges to [[_COMMUNITY_Multi-DB Pool & Lifecycle]]
- 3 edges to [[_COMMUNITY_Filtered Policy Loading]]
- 3 edges to [[_COMMUNITY_Adapter Policy Methods]]
- 2 edges to [[_COMMUNITY_Adapter Construction & DB Open]]

## Top bridge nodes
- [[CasbinRule]] - degree 10, connects to 3 communities
- [[checkQueryField()]] - degree 3, connects to 2 communities
- [[Adapter.savePolicyLine]] - degree 10, connects to 1 community
- [[Adapter.getTableInstance]] - degree 6, connects to 1 community
- [[appendWhere()]] - degree 4, connects to 1 community