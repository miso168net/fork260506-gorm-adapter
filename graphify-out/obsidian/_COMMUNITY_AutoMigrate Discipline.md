---
type: community
cohesion: 0.47
members: 6
---

# AutoMigrate Discipline

**Cohesion:** 0.47 - moderately connected
**Members:** 6 nodes

## Members
- [[AC-007 AutoMigrate runs unless TurnOffAutoMigrate called]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Adapter.createTable]] - code - adapter.go
- [[NewAdapterByDBWithCustomTable]] - code - adapter.go
- [[TestAdapterWithCustomTable]] - code - adapter_test.go
- [[TestAdapterWithoutAutoMigrate]] - code - adapter_test.go
- [[TurnOffAutoMigrate]] - code - adapter.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/AutoMigrate_Discipline
SORT file.name ASC
```

## Connections to other communities
- 6 edges to [[_COMMUNITY_Constructor Minimal Surface]]
- 1 edge to [[_COMMUNITY_Driver Switch & Convergence]]
- 1 edge to [[_COMMUNITY_Filter Query Helpers]]
- 1 edge to [[_COMMUNITY_Table-Name Helpers]]

## Top bridge nodes
- [[Adapter.createTable]] - degree 7, connects to 4 communities
- [[NewAdapterByDBWithCustomTable]] - degree 7, connects to 1 community
- [[TurnOffAutoMigrate]] - degree 4, connects to 1 community