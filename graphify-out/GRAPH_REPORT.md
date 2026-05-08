# Graph Report - .  (2026-05-08)

## Corpus Check
- 10 files · ~9,705 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 85 nodes · 161 edges · 15 communities (12 shown, 3 thin omitted)
- Extraction: 91% EXTRACTED · 9% INFERRED · 0% AMBIGUOUS · INFERRED: 15 edges (avg confidence: 0.85)
- Token cost: 67,889 input · 16,972 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Filtered Policy Loading|Filtered Policy Loading]]
- [[_COMMUNITY_Batch & Update CRUD|Batch & Update CRUD]]
- [[_COMMUNITY_Multi-DB Pool & Baseline|Multi-DB Pool & Baseline]]
- [[_COMMUNITY_Constructor Minimal Surface|Constructor Minimal Surface]]
- [[_COMMUNITY_Driver Switch & Convergence|Driver Switch & Convergence]]
- [[_COMMUNITY_Persist & LoadPolicy Path|Persist & LoadPolicy Path]]
- [[_COMMUNITY_AutoMigrate Discipline|AutoMigrate Discipline]]
- [[_COMMUNITY_CasbinRule Schema & Queries|CasbinRule Schema & Queries]]
- [[_COMMUNITY_Adapter Lifecycle|Adapter Lifecycle]]
- [[_COMMUNITY_Filter Query Helpers|Filter Query Helpers]]
- [[_COMMUNITY_DB Open Internals|DB Open Internals]]
- [[_COMMUNITY_Table-Name Helpers|Table-Name Helpers]]
- [[_COMMUNITY_Cross-DB Parity Principle|Cross-DB Parity Principle]]
- [[_COMMUNITY_READMECode Driver Drift|README/Code Driver Drift]]
- [[_COMMUNITY_SQLite Build-Tag Drift|SQLite Build-Tag Drift]]

## God Nodes (most connected - your core abstractions)
1. `NewAdapter constructor` - 12 edges
2. `Project file tree index 2026-05-06 snapshot` - 12 edges
3. `Adapter.savePolicyLine` - 11 edges
4. `CasbinRule struct` - 9 edges
5. `NewAdapterByDBUseTableName` - 9 edges
6. `Adapter.Open` - 9 edges
7. `gorm-adapter Baseline Reference Spec` - 9 edges
8. `Filter struct` - 7 edges
9. `NewAdapterByDBWithCustomTable` - 7 edges
10. `Adapter.createTable` - 7 edges

## Surprising Connections (you probably didn't know these)
- `Adapter.createTable` --references--> `AC-007 AutoMigrate runs unless TurnOffAutoMigrate called`  [INFERRED]
  adapter.go → docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- `CasbinRule struct` --references--> `Usage Scenario 1 - Persist Casbin policy to a relational database (P1)`  [EXTRACTED]
  adapter.go → docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- `CasbinRule struct` --references--> `AC-006 default table casbin_rule (singular, post-v3.0.4)`  [EXTRACTED]
  adapter.go → docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- `CasbinRule struct` --references--> `gorm-adapter Baseline Reference Spec`  [EXTRACTED]
  adapter.go → docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md
- `CasbinRule struct` --rationale_for--> `Filter V0-V6 vs CasbinRule V0-V7 asymmetry (V7 storable not filterable)`  [EXTRACTED]
  adapter.go → docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md

## Hyperedges (group relationships)
- **Casbin persist interface contracts the Adapter implements** — 2026_05_07_gorm_adapter_baseline_design_ac_001_persist_adapter, 2026_05_07_gorm_adapter_baseline_design_ac_002_persist_filteredadapter, 2026_05_07_gorm_adapter_baseline_design_ac_003_persist_batchadapter, 2026_05_07_gorm_adapter_baseline_design_ac_004_persist_updatableadapter, adapter_adapter [EXTRACTED 1.00]
- **Six top-level constructors governed by Minimal Surface principle** — adapter_newadapter, adapter_newadapterbydb, adapter_newadapterbydbusetablename, adapter_newadapterbydbwithcustomtable, adapter_newfilteredadapter, adapter_newadapterbymuldb, 2026_05_07_gorm_adapter_baseline_design_ac_008_six_constructors [EXTRACTED 1.00]
- **Three Usage Scenarios (P1/P2/P3) framing baseline behaviour** — 2026_05_07_gorm_adapter_baseline_design_usage_scenario_1_persist_policy, 2026_05_07_gorm_adapter_baseline_design_usage_scenario_2_existing_gorm_db, 2026_05_07_gorm_adapter_baseline_design_usage_scenario_3_filtered_policy_loading, 2026_05_07_gorm_adapter_baseline_design_baseline_spec [EXTRACTED 1.00]

## Communities (15 total, 3 thin omitted)

### Community 0 - "Filtered Policy Loading"
Cohesion: 0.23
Nodes (14): AC-002 satisfy persist.FilteredAdapter interface, Filter V0-V6 vs CasbinRule V0-V7 asymmetry (V7 storable not filterable), Filtered SavePolicy must not truncate unrelated rules (data-loss invariant), Usage Scenario 3 - Filtered policy loading for large policy sets (P3), Filter struct, Adapter.filterQuery, Adapter.IsFiltered, Adapter.LoadFilteredPolicy (+6 more)

### Community 1 - "Batch & Update CRUD"
Cohesion: 0.31
Nodes (9): AC-003 satisfy persist.BatchAdapter interface, AC-004 satisfy persist.UpdatableAdapter interface, Adapter.AddPolicies, CasbinRule.toStringPolicy, Adapter.RemovePolicies, Adapter.savePolicyLine, Adapter.UpdateFilteredPolicies, Adapter.UpdatePolicies (+1 more)

### Community 2 - "Multi-DB Pool & Baseline"
Cohesion: 0.36
Nodes (8): AC-010 InitDbResolver returns DbPool with switchDb (multi-DB), gorm-adapter Baseline Reference Spec, Baseline target master @ bc66b93 (2022-11-27), DbPool struct, DbPool.switchDb, InitDbResolver, specificPolicy type, TestAdapterWithMulDb

### Community 3 - "Constructor Minimal Surface"
Cohesion: 0.52
Nodes (7): AC-008 expose six top-level constructors (Minimal Surface), Constitution Principle V - Minimal Surface (constructor count cap), Usage Scenario 2 - Attach Casbin to an existing *gorm.DB (P2), NewAdapterByDB, NewAdapterByDBUseTableName, NewAdapterByMulDb, Project file tree index 2026-05-06 snapshot

### Community 4 - "Driver Switch & Convergence"
Cohesion: 0.48
Nodes (7): AC-005 supported driver names mysql/postgres/sqlserver/sqlite3-buildtag, Constructor Convergence on Adapter.Open(), NewAdapter constructor, NewFilteredAdapter, Adapter.Open, TestNilField, Six constructors converge on (a *Adapter).Open()

### Community 5 - "Persist & LoadPolicy Path"
Cohesion: 0.38
Nodes (7): AC-001 satisfy persist.Adapter interface, Usage Scenario 1 - Persist Casbin policy to a relational database (P1), Adapter.AddPolicy, Adapter.LoadPolicy, loadPolicyLine, Adapter.RemovePolicy, testAutoSave

### Community 6 - "AutoMigrate Discipline"
Cohesion: 0.47
Nodes (6): AC-007 AutoMigrate runs unless TurnOffAutoMigrate called, Adapter.createTable, NewAdapterByDBWithCustomTable, TurnOffAutoMigrate, TestAdapterWithCustomTable, TestAdapterWithoutAutoMigrate

### Community 7 - "CasbinRule Schema & Queries"
Cohesion: 0.5
Nodes (5): AC-006 default table casbin_rule (singular, post-v3.0.4), appendWhere, CasbinRule struct, CasbinRule.queryString, Adapter.rawDelete

### Community 8 - "Adapter Lifecycle"
Cohesion: 0.4
Nodes (5): AC-009 expose Open, Close, AddLogger lifecycle methods, Adapter struct, Adapter.AddLogger, Adapter.Close, finalizer

### Community 9 - "Filter Query Helpers"
Cohesion: 0.5
Nodes (4): checkQueryField, Adapter.dropTable, Adapter.getTableInstance, Adapter.RemoveFilteredPolicy

### Community 10 - "DB Open Internals"
Cohesion: 0.67
Nodes (4): Adapter.createDatabase, openDBConnection, opens dialect map (no sqlite), opens dialect map (with sqlite)

### Community 11 - "Table-Name Helpers"
Cohesion: 0.67
Nodes (3): Adapter.casbinRuleTable scope, Adapter.getFullTableName, Adapter.truncateTable

## Knowledge Gaps
- **15 isolated node(s):** `Adapter.AddLogger`, `Adapter.dropTable`, `checkQueryField`, `CasbinRule.toStringPolicy`, `TestAdapterWithCustomTable` (+10 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **3 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Project file tree index 2026-05-06 snapshot` connect `Constructor Minimal Surface` to `Filtered Policy Loading`, `Batch & Update CRUD`, `Multi-DB Pool & Baseline`, `Driver Switch & Convergence`, `AutoMigrate Discipline`, `CasbinRule Schema & Queries`, `Adapter Lifecycle`?**
  _High betweenness centrality (0.267) - this node is a cross-community bridge._
- **Why does `Adapter.savePolicyLine` connect `Batch & Update CRUD` to `Filtered Policy Loading`, `Constructor Minimal Surface`, `Persist & LoadPolicy Path`, `CasbinRule Schema & Queries`, `Filter Query Helpers`?**
  _High betweenness centrality (0.199) - this node is a cross-community bridge._
- **Why does `Adapter.Open` connect `Driver Switch & Convergence` to `Constructor Minimal Surface`, `AutoMigrate Discipline`, `Adapter Lifecycle`, `DB Open Internals`, `Table-Name Helpers`?**
  _High betweenness centrality (0.161) - this node is a cross-community bridge._
- **What connects `Adapter.AddLogger`, `Adapter.dropTable`, `checkQueryField` to the rest of the system?**
  _15 weakly-connected nodes found - possible documentation gaps or missing edges._