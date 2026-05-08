---
type: community
cohesion: 0.48
members: 7
---

# Driver Switch & Convergence

**Cohesion:** 0.48 - moderately connected
**Members:** 7 nodes

## Members
- [[AC-005 supported driver names mysqlpostgressqlserversqlite3-buildtag]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Adapter.Open]] - code - adapter.go
- [[Constructor Convergence on Adapter.Open()]] - rationale - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[NewAdapter constructor]] - code - adapter.go
- [[NewFilteredAdapter]] - code - adapter.go
- [[Six constructors converge on (a Adapter).Open()]] - rationale - x_fork.tree-20260506.md
- [[TestNilField]] - code - adapter_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Driver_Switch__Convergence
SORT file.name ASC
```

## Connections to other communities
- 7 edges to [[_COMMUNITY_Constructor Minimal Surface]]
- 2 edges to [[_COMMUNITY_Adapter Lifecycle]]
- 2 edges to [[_COMMUNITY_Filtered Policy Loading]]
- 2 edges to [[_COMMUNITY_DB Open Internals]]
- 1 edge to [[_COMMUNITY_Multi-DB Pool & Baseline]]
- 1 edge to [[_COMMUNITY_Persist & LoadPolicy Path]]
- 1 edge to [[_COMMUNITY_Table-Name Helpers]]
- 1 edge to [[_COMMUNITY_AutoMigrate Discipline]]

## Top bridge nodes
- [[NewAdapter constructor]] - degree 12, connects to 5 communities
- [[Adapter.Open]] - degree 9, connects to 5 communities
- [[NewFilteredAdapter]] - degree 5, connects to 2 communities
- [[Constructor Convergence on Adapter.Open()]] - degree 5, connects to 1 community