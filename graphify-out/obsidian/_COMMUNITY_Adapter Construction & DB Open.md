---
type: community
cohesion: 0.15
members: 20
---

# Adapter Construction & DB Open

**Cohesion:** 0.15 - loosely connected
**Members:** 20 nodes

## Members
- [[.Open()]] - code - adapter.go
- [[.casbinRuleTable()]] - code - adapter.go
- [[.createDatabase()]] - code - adapter.go
- [[Adapter.Open]] - code - adapter.go
- [[Adapter.casbinRuleTable scope]] - code - adapter.go
- [[Adapter.createDatabase]] - code - adapter.go
- [[Adapter.createTable]] - code - adapter.go
- [[Adapter.getFullTableName]] - code - adapter.go
- [[NewAdapterByDB()]] - code - adapter.go
- [[NewAdapterByDBUseTableName()]] - code - adapter.go
- [[NewAdapterByDBWithCustomTable()]] - code - adapter.go
- [[README Customize table columns example]] - document - README.md
- [[README Turn off AutoMigrate section]] - document - README.md
- [[README sqlite driver choice rationale]] - document - README.md
- [[TestAdapterWithCustomTable]] - code - adapter_test.go
- [[TestAdapterWithoutAutoMigrate]] - code - adapter_test.go
- [[TurnOffAutoMigrate()]] - code - adapter.go
- [[openDBConnection()]] - code - adapter.go
- [[opens dialect map (no sqlite)]] - code - open.go
- [[opens dialect map (with sqlite)]] - code - open_sqlite3.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Adapter_Construction_&_DB_Open
SORT file.name ASC
```

## Connections to other communities
- 9 edges to [[_COMMUNITY_Multi-DB Pool & Lifecycle]]
- 9 edges to [[_COMMUNITY_Test Suite & Adapter Init]]
- 8 edges to [[_COMMUNITY_Adapter Policy Methods]]
- 2 edges to [[_COMMUNITY_CasbinRule Model & Policy CRUD]]
- 1 edge to [[_COMMUNITY_Filtered Policy Loading]]

## Top bridge nodes
- [[.Open()]] - degree 12, connects to 3 communities
- [[NewAdapterByDBUseTableName()]] - degree 10, connects to 3 communities
- [[NewAdapterByDBWithCustomTable()]] - degree 9, connects to 3 communities
- [[TurnOffAutoMigrate()]] - degree 5, connects to 2 communities
- [[NewAdapterByDB()]] - degree 3, connects to 2 communities