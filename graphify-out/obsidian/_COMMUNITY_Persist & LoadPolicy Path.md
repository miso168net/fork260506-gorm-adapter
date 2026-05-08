---
type: community
cohesion: 0.38
members: 7
---

# Persist & LoadPolicy Path

**Cohesion:** 0.38 - loosely connected
**Members:** 7 nodes

## Members
- [[AC-001 satisfy persist.Adapter interface]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Adapter.AddPolicy]] - code - adapter.go
- [[Adapter.LoadPolicy]] - code - adapter.go
- [[Adapter.RemovePolicy]] - code - adapter.go
- [[Usage Scenario 1 - Persist Casbin policy to a relational database (P1)]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[loadPolicyLine]] - code - adapter.go
- [[testAutoSave]] - code - adapter_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Persist__LoadPolicy_Path
SORT file.name ASC
```

## Connections to other communities
- 5 edges to [[_COMMUNITY_Filtered Policy Loading]]
- 3 edges to [[_COMMUNITY_CasbinRule Schema & Queries]]
- 2 edges to [[_COMMUNITY_Batch & Update CRUD]]
- 2 edges to [[_COMMUNITY_Filter Query Helpers]]
- 1 edge to [[_COMMUNITY_Adapter Lifecycle]]
- 1 edge to [[_COMMUNITY_Driver Switch & Convergence]]
- 1 edge to [[_COMMUNITY_Multi-DB Pool & Baseline]]

## Top bridge nodes
- [[Usage Scenario 1 - Persist Casbin policy to a relational database (P1)]] - degree 6, connects to 4 communities
- [[AC-001 satisfy persist.Adapter interface]] - degree 6, connects to 3 communities
- [[Adapter.RemovePolicy]] - degree 4, connects to 2 communities
- [[testAutoSave]] - degree 4, connects to 2 communities
- [[loadPolicyLine]] - degree 3, connects to 2 communities