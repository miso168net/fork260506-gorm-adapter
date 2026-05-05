# Graph Report - .  (2026-05-06)

## Corpus Check
- Corpus is ~6,044 words - fits in a single context window. You may not need a graph.

## Summary
- 121 nodes · 282 edges · 10 communities detected
- Extraction: 82% EXTRACTED · 18% INFERRED · 0% AMBIGUOUS · INFERRED: 51 edges (avg confidence: 0.8)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Test Suite & Adapter Init|Test Suite & Adapter Init]]
- [[_COMMUNITY_Adapter Policy Methods|Adapter Policy Methods]]
- [[_COMMUNITY_CasbinRule Model & Policy CRUD|CasbinRule Model & Policy CRUD]]
- [[_COMMUNITY_Adapter Construction & DB Open|Adapter Construction & DB Open]]
- [[_COMMUNITY_Multi-DB Pool & Lifecycle|Multi-DB Pool & Lifecycle]]
- [[_COMMUNITY_Filtered Policy Loading|Filtered Policy Loading]]
- [[_COMMUNITY_DB Open Driver Switch|DB Open Driver Switch]]
- [[_COMMUNITY_SQLite3 Open Helper|SQLite3 Open Helper]]
- [[_COMMUNITY_Logger Wiring|Logger Wiring]]
- [[_COMMUNITY_IsFiltered Check|IsFiltered Check]]

## God Nodes (most connected - your core abstractions)
1. `Adapter` - 27 edges
2. `TestAdapters()` - 13 edges
3. `initPolicy()` - 12 edges
4. `CasbinRule` - 10 edges
5. `NewAdapterByDBUseTableName()` - 10 edges
6. `testAutoSave()` - 10 edges
7. `Adapter.savePolicyLine` - 10 edges
8. `NewAdapter()` - 9 edges
9. `NewAdapterByDBWithCustomTable()` - 9 edges
10. `testGetPolicy()` - 9 edges

## Surprising Connections (you probably didn't know these)
- `README Customize table columns example` --references--> `CasbinRule`  [EXTRACTED]
  README.md → adapter.go
- `README v3.0.3 table rename migration note` --rationale_for--> `CasbinRule`  [INFERRED]
  README.md → adapter.go
- `README simple example` --references--> `NewAdapter()`  [EXTRACTED]
  README.md → adapter.go
- `README Turn off AutoMigrate section` --references--> `TurnOffAutoMigrate()`  [EXTRACTED]
  README.md → adapter.go
- `README Turn off AutoMigrate section` --references--> `NewAdapterByDBWithCustomTable()`  [EXTRACTED]
  README.md → adapter.go

## Hyperedges (group relationships)
- **Multi-DB resolver setup flow** — adapter_initdbresolver, adapter_dbpool, adapter_specificpolicy, adapter_dbpool_switchdb, adapter_newadapterbymuldb [EXTRACTED 0.90]
- **Policy save/load round-trip** — adapter_savepolicy, adapter_loadpolicy, adapter_savepolicyline, adapter_loadpolicyline, adapter_casbinrule [EXTRACTED 0.90]
- **Adapter constructor variants** — adapter_newadapter, adapter_newadapterbydb, adapter_newadapterbydbusetablename, adapter_newadapterbydbwithcustomtable, adapter_newfilteredadapter, adapter_newadapterbymuldb [EXTRACTED 0.90]

## Communities

### Community 0 - "Test Suite & Adapter Init"
Cohesion: 0.22
Nodes (24): arrayEqualsWithoutOrder(), initAdapter(), initAdapterWithGormInstance(), initAdapterWithGormInstanceAndCustomTable(), initAdapterWithGormInstanceByMulDb(), initAdapterWithGormInstanceByName(), initAdapterWithGormInstanceByPrefixAndName(), initPolicy() (+16 more)

### Community 1 - "Adapter Policy Methods"
Cohesion: 0.22
Nodes (3): Adapter, initAdapterWithoutAutoMigrate(), TestNilField()

### Community 2 - "CasbinRule Model & Policy CRUD"
Cohesion: 0.16
Nodes (17): Adapter.AddPolicies, Adapter.AddPolicy, appendWhere(), CasbinRule, checkQueryField(), Adapter.dropTable, Adapter.getTableInstance, Adapter.rawDelete (+9 more)

### Community 3 - "Adapter Construction & DB Open"
Cohesion: 0.15
Nodes (17): Adapter.casbinRuleTable scope, Adapter.createDatabase, Adapter.createTable, Adapter.getFullTableName, NewAdapterByDB(), NewAdapterByDBUseTableName(), NewAdapterByDBWithCustomTable(), Adapter.Open (+9 more)

### Community 4 - "Multi-DB Pool & Lifecycle"
Cohesion: 0.18
Nodes (12): Adapter.Close, DbPool, finalizer(), InitDbResolver(), NewAdapter(), NewAdapterByMulDb(), NewFilteredAdapter(), specificPolicy (+4 more)

### Community 5 - "Filtered Policy Loading"
Cohesion: 0.19
Nodes (12): Filter, Adapter.filterQuery, Adapter.LoadFilteredPolicy, Adapter.LoadPolicy, loadPolicyLine(), Adapter.SavePolicy, Adapter.truncateTable, initAdapter test helper (+4 more)

### Community 6 - "DB Open Driver Switch"
Cohesion: 1.0
Nodes (0): 

### Community 7 - "SQLite3 Open Helper"
Cohesion: 1.0
Nodes (0): 

### Community 8 - "Logger Wiring"
Cohesion: 1.0
Nodes (1): Adapter.AddLogger

### Community 9 - "IsFiltered Check"
Cohesion: 1.0
Nodes (1): Adapter.IsFiltered

## Ambiguous Edges - Review These
- `README simple example` → `Fork main branch origin record`  [AMBIGUOUS]
  x_fork.branch-origin.md · relation: references

## Knowledge Gaps
- **12 isolated node(s):** `Adapter.AddLogger`, `Adapter.Close`, `Adapter.dropTable`, `Adapter.IsFiltered`, `Adapter.AddPolicies` (+7 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **Thin community `DB Open Driver Switch`** (1 nodes): `open.go`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `SQLite3 Open Helper`** (1 nodes): `open_sqlite3.go`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Logger Wiring`** (1 nodes): `Adapter.AddLogger`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `IsFiltered Check`** (1 nodes): `Adapter.IsFiltered`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **What is the exact relationship between `README simple example` and `Fork main branch origin record`?**
  _Edge tagged AMBIGUOUS (relation: references) - confidence is low._
- **Why does `Adapter` connect `Adapter Policy Methods` to `Test Suite & Adapter Init`, `Adapter Construction & DB Open`, `Multi-DB Pool & Lifecycle`, `Filtered Policy Loading`?**
  _High betweenness centrality (0.228) - this node is a cross-community bridge._
- **Why does `CasbinRule` connect `CasbinRule Model & Policy CRUD` to `Adapter Construction & DB Open`, `Multi-DB Pool & Lifecycle`, `Filtered Policy Loading`?**
  _High betweenness centrality (0.144) - this node is a cross-community bridge._
- **Why does `NewAdapter()` connect `Multi-DB Pool & Lifecycle` to `Adapter Construction & DB Open`, `Filtered Policy Loading`?**
  _High betweenness centrality (0.101) - this node is a cross-community bridge._
- **Are the 2 inferred relationships involving `TestAdapters()` (e.g. with `.Open()` and `.AddLogger()`) actually correct?**
  _`TestAdapters()` has 2 INFERRED edges - model-reasoned connections that need verification._
- **Are the 2 inferred relationships involving `initPolicy()` (e.g. with `.LoadPolicy()` and `.SavePolicy()`) actually correct?**
  _`initPolicy()` has 2 INFERRED edges - model-reasoned connections that need verification._
- **Are the 2 inferred relationships involving `NewAdapterByDBUseTableName()` (e.g. with `initAdapterWithGormInstanceByName()` and `initAdapterWithGormInstanceByPrefixAndName()`) actually correct?**
  _`NewAdapterByDBUseTableName()` has 2 INFERRED edges - model-reasoned connections that need verification._