---
type: community
cohesion: 0.31
members: 9
---

# Batch & Update CRUD

**Cohesion:** 0.31 - loosely connected
**Members:** 9 nodes

## Members
- [[AC-003 satisfy persist.BatchAdapter interface]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[AC-004 satisfy persist.UpdatableAdapter interface]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Adapter.AddPolicies]] - code - adapter.go
- [[Adapter.RemovePolicies]] - code - adapter.go
- [[Adapter.UpdateFilteredPolicies]] - code - adapter.go
- [[Adapter.UpdatePolicies]] - code - adapter.go
- [[Adapter.UpdatePolicy]] - code - adapter.go
- [[Adapter.savePolicyLine]] - code - adapter.go
- [[CasbinRule.toStringPolicy]] - code - adapter.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Batch__Update_CRUD
SORT file.name ASC
```

## Connections to other communities
- 3 edges to [[_COMMUNITY_CasbinRule Schema & Queries]]
- 2 edges to [[_COMMUNITY_Filter Query Helpers]]
- 2 edges to [[_COMMUNITY_Persist & LoadPolicy Path]]
- 1 edge to [[_COMMUNITY_Filtered Policy Loading]]
- 1 edge to [[_COMMUNITY_Constructor Minimal Surface]]

## Top bridge nodes
- [[Adapter.savePolicyLine]] - degree 11, connects to 5 communities
- [[Adapter.UpdateFilteredPolicies]] - degree 5, connects to 2 communities
- [[Adapter.RemovePolicies]] - degree 3, connects to 1 community