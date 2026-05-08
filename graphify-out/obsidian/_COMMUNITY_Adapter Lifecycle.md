---
type: community
cohesion: 0.40
members: 5
---

# Adapter Lifecycle

**Cohesion:** 0.40 - moderately connected
**Members:** 5 nodes

## Members
- [[AC-009 expose Open, Close, AddLogger lifecycle methods]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Adapter struct]] - code - adapter.go
- [[Adapter.AddLogger]] - code - adapter.go
- [[Adapter.Close]] - code - adapter.go
- [[finalizer]] - code - adapter.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Adapter_Lifecycle
SORT file.name ASC
```

## Connections to other communities
- 2 edges to [[_COMMUNITY_Driver Switch & Convergence]]
- 1 edge to [[_COMMUNITY_Persist & LoadPolicy Path]]
- 1 edge to [[_COMMUNITY_Multi-DB Pool & Baseline]]
- 1 edge to [[_COMMUNITY_Constructor Minimal Surface]]

## Top bridge nodes
- [[Adapter struct]] - degree 4, connects to 3 communities
- [[AC-009 expose Open, Close, AddLogger lifecycle methods]] - degree 3, connects to 1 community
- [[finalizer]] - degree 3, connects to 1 community