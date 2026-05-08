---
type: community
cohesion: 0.50
members: 5
---

# CasbinRule Schema & Queries

**Cohesion:** 0.50 - moderately connected
**Members:** 5 nodes

## Members
- [[AC-006 default table casbin_rule (singular, post-v3.0.4)]] - document - docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- [[Adapter.rawDelete]] - code - adapter.go
- [[CasbinRule struct]] - code - adapter.go
- [[CasbinRule.queryString]] - code - adapter.go
- [[appendWhere]] - code - adapter.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/CasbinRule_Schema__Queries
SORT file.name ASC
```

## Connections to other communities
- 3 edges to [[_COMMUNITY_Batch & Update CRUD]]
- 3 edges to [[_COMMUNITY_Persist & LoadPolicy Path]]
- 2 edges to [[_COMMUNITY_Filter Query Helpers]]
- 1 edge to [[_COMMUNITY_Multi-DB Pool & Baseline]]
- 1 edge to [[_COMMUNITY_Filtered Policy Loading]]
- 1 edge to [[_COMMUNITY_Constructor Minimal Surface]]

## Top bridge nodes
- [[CasbinRule struct]] - degree 9, connects to 5 communities
- [[Adapter.rawDelete]] - degree 6, connects to 3 communities
- [[CasbinRule.queryString]] - degree 2, connects to 1 community