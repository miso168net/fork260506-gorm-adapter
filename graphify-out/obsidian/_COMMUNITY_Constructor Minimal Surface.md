---
type: community
cohesion: 0.52
members: 7
---

# Constructor Minimal Surface

**Cohesion:** 0.52 - moderately connected
**Members:** 7 nodes

## Members
- [[AC-008 expose six top-level constructors (Minimal Surface)]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Constitution Principle V - Minimal Surface (constructor count cap)]] - rationale - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[NewAdapterByDB]] - code - adapter.go
- [[NewAdapterByDBUseTableName]] - code - adapter.go
- [[NewAdapterByMulDb]] - code - adapter.go
- [[Project file tree index 2026-05-06 snapshot]] - document - x_fork.tree-20260506.md
- [[Usage Scenario 2 - Attach Casbin to an existing gorm.DB (P2)]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Constructor_Minimal_Surface
SORT file.name ASC
```

## Connections to other communities
- 7 edges to [[_COMMUNITY_Driver Switch & Convergence]]
- 6 edges to [[_COMMUNITY_AutoMigrate Discipline]]
- 4 edges to [[_COMMUNITY_Multi-DB Pool & Baseline]]
- 1 edge to [[_COMMUNITY_CasbinRule Schema & Queries]]
- 1 edge to [[_COMMUNITY_Filtered Policy Loading]]
- 1 edge to [[_COMMUNITY_Adapter Lifecycle]]
- 1 edge to [[_COMMUNITY_Table-Name Helpers]]
- 1 edge to [[_COMMUNITY_Batch & Update CRUD]]

## Top bridge nodes
- [[Project file tree index 2026-05-06 snapshot]] - degree 12, connects to 7 communities
- [[NewAdapterByDBUseTableName]] - degree 9, connects to 3 communities
- [[AC-008 expose six top-level constructors (Minimal Surface)]] - degree 7, connects to 2 communities
- [[Usage Scenario 2 - Attach Casbin to an existing gorm.DB (P2)]] - degree 5, connects to 2 communities
- [[NewAdapterByDB]] - degree 5, connects to 1 community