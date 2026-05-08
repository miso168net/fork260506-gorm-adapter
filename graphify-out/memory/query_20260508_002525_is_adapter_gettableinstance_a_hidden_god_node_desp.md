---
type: "explain"
date: "2026-05-08T00:25:25.020865+00:00"
question: "Is Adapter.getTableInstance a hidden god node despite its low edge count?"
contributor: "graphify"
source_nodes: ["Adapter.getTableInstance", "Adapter.savePolicyLine", "NewAdapterByDBWithCustomTable", "NewAdapterByDBUseTableName"]
---

# Q: Is Adapter.getTableInstance a hidden god node despite its low edge count?

## Answer

Yes — it is a god node by impact rather than by degree. The function is only 3 lines (adapter.go:334-336) and has 6 edges (rank ~18 by edge count), but every one of those 6 edges is load-bearing and from a distinct concern: write encoding (savePolicyLine), schema lifecycle (createTable, dropTable), filter operations (RemoveFilteredPolicy, UpdateFilteredPolicies), and raw mutation (rawDelete). The function exists because of AC-008 Minimal Surface: two constructors NewAdapterByDBUseTableName and NewAdapterByDBWithCustomTable allow per-instance row structs, so no write path can hard-code &CasbinRule{}; everything must dispatch through getTableInstance. Together with savePolicyLine it forms the encoding triangle (savePolicyLine encodes, getTableInstance dispatches, CasbinRule/custom struct provides schema). The 33 combined lines (savePolicyLine 30 + getTableInstance 3) are the core risk surface for any write-path modification. Removing NewAdapterByDBWithCustomTable would make getTableInstance dead code, which is a useful tell for whether AC-008 is justified by current users.

## Source Nodes

- Adapter.getTableInstance
- Adapter.savePolicyLine
- NewAdapterByDBWithCustomTable
- NewAdapterByDBUseTableName