---
type: community
cohesion: 0.36
members: 8
---

# Multi-DB Pool & Baseline

**Cohesion:** 0.36 - loosely connected
**Members:** 8 nodes

## Members
- [[AC-010 InitDbResolver returns DbPool with switchDb (multi-DB)]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Baseline target master @ bc66b93 (2022-11-27)]] - rationale - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[DbPool struct]] - code - adapter.go
- [[DbPool.switchDb]] - code - adapter.go
- [[InitDbResolver]] - code - adapter.go
- [[TestAdapterWithMulDb]] - code - adapter_test.go
- [[gorm-adapter Baseline Reference Spec]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[specificPolicy type]] - code - adapter.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Multi-DB_Pool__Baseline
SORT file.name ASC
```

## Connections to other communities
- 4 edges to [[_COMMUNITY_Constructor Minimal Surface]]
- 2 edges to [[_COMMUNITY_Filtered Policy Loading]]
- 1 edge to [[_COMMUNITY_CasbinRule Schema & Queries]]
- 1 edge to [[_COMMUNITY_Adapter Lifecycle]]
- 1 edge to [[_COMMUNITY_Driver Switch & Convergence]]
- 1 edge to [[_COMMUNITY_Persist & LoadPolicy Path]]

## Top bridge nodes
- [[gorm-adapter Baseline Reference Spec]] - degree 9, connects to 5 communities
- [[DbPool struct]] - degree 6, connects to 1 community
- [[AC-010 InitDbResolver returns DbPool with switchDb (multi-DB)]] - degree 3, connects to 1 community
- [[DbPool.switchDb]] - degree 2, connects to 1 community
- [[TestAdapterWithMulDb]] - degree 2, connects to 1 community