---
type: community
cohesion: 0.23
members: 14
---

# Filtered Policy Loading

**Cohesion:** 0.23 - loosely connected
**Members:** 14 nodes

## Members
- [[AC-002 satisfy persist.FilteredAdapter interface]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Adapter.IsFiltered]] - code - adapter.go
- [[Adapter.LoadFilteredPolicy]] - code - adapter.go
- [[Adapter.SavePolicy]] - code - adapter.go
- [[Adapter.filterQuery]] - code - adapter.go
- [[Filter V0-V6 vs CasbinRule V0-V7 asymmetry (V7 storable not filterable)]] - rationale - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Filter struct]] - code - adapter.go
- [[Filtered SavePolicy must not truncate unrelated rules (data-loss invariant)]] - rationale - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[TestAdapters]] - code - adapter_test.go
- [[Usage Scenario 3 - Filtered policy loading for large policy sets (P3)]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[initAdapter test helper]] - code - adapter_test.go
- [[initPolicy test helper]] - code - adapter_test.go
- [[testFilteredPolicy]] - code - adapter_test.go
- [[testSaveLoad]] - code - adapter_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Filtered_Policy_Loading
SORT file.name ASC
```

## Connections to other communities
- 5 edges to [[_COMMUNITY_Persist & LoadPolicy Path]]
- 2 edges to [[_COMMUNITY_Multi-DB Pool & Baseline]]
- 2 edges to [[_COMMUNITY_Driver Switch & Convergence]]
- 1 edge to [[_COMMUNITY_CasbinRule Schema & Queries]]
- 1 edge to [[_COMMUNITY_Constructor Minimal Surface]]
- 1 edge to [[_COMMUNITY_Table-Name Helpers]]
- 1 edge to [[_COMMUNITY_Batch & Update CRUD]]

## Top bridge nodes
- [[Adapter.SavePolicy]] - degree 7, connects to 3 communities
- [[Filter struct]] - degree 7, connects to 2 communities
- [[Usage Scenario 3 - Filtered policy loading for large policy sets (P3)]] - degree 6, connects to 2 communities
- [[Adapter.LoadFilteredPolicy]] - degree 7, connects to 1 community
- [[initPolicy test helper]] - degree 4, connects to 1 community