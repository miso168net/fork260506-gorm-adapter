---
type: community
cohesion: 0.22
members: 27
---

# Test Suite & Adapter Init

**Cohesion:** 0.22 - loosely connected
**Members:** 27 nodes

## Members
- [[.AddPolicies()]] - code - adapter.go
- [[.LoadPolicy()]] - code - adapter.go
- [[TestAdapterWithCustomTable()]] - code - adapter_test.go
- [[TestAdapterWithMulDb()]] - code - adapter_test.go
- [[TestAdapterWithoutAutoMigrate()]] - code - adapter_test.go
- [[TestAdapters()]] - code - adapter_test.go
- [[TestAddPolicies()]] - code - adapter_test.go
- [[TestAddPoliciesFullColumn()]] - code - adapter_test.go
- [[adapter_test.go]] - code - adapter_test.go
- [[arrayEqualsWithoutOrder()]] - code - adapter_test.go
- [[initAdapter()]] - code - adapter_test.go
- [[initAdapterWithGormInstance()]] - code - adapter_test.go
- [[initAdapterWithGormInstanceAndCustomTable()]] - code - adapter_test.go
- [[initAdapterWithGormInstanceByMulDb()]] - code - adapter_test.go
- [[initAdapterWithGormInstanceByName()]] - code - adapter_test.go
- [[initAdapterWithGormInstanceByPrefixAndName()]] - code - adapter_test.go
- [[initPolicy()]] - code - adapter_test.go
- [[testAutoSave()]] - code - adapter_test.go
- [[testBasicFeatures()]] - code - adapter_test.go
- [[testFilteredPolicy()]] - code - adapter_test.go
- [[testGetPolicy()]] - code - adapter_test.go
- [[testGetPolicyWithoutOrder()]] - code - adapter_test.go
- [[testIndependenceBetweenMulDb()]] - code - adapter_test.go
- [[testSaveLoad()]] - code - adapter_test.go
- [[testUpdateFilteredPolicies()]] - code - adapter_test.go
- [[testUpdatePolicies()]] - code - adapter_test.go
- [[testUpdatePolicy()]] - code - adapter_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Test_Suite_&_Adapter_Init
SORT file.name ASC
```

## Connections to other communities
- 17 edges to [[_COMMUNITY_Adapter Policy Methods]]
- 9 edges to [[_COMMUNITY_Adapter Construction & DB Open]]
- 3 edges to [[_COMMUNITY_Multi-DB Pool & Lifecycle]]
- 2 edges to [[_COMMUNITY_Filtered Policy Loading]]

## Top bridge nodes
- [[testIndependenceBetweenMulDb()]] - degree 6, connects to 3 communities
- [[TestAdapters()]] - degree 13, connects to 2 communities
- [[.LoadPolicy()]] - degree 10, connects to 2 communities
- [[testBasicFeatures()]] - degree 8, connects to 2 communities
- [[TestAdapterWithoutAutoMigrate()]] - degree 6, connects to 2 communities