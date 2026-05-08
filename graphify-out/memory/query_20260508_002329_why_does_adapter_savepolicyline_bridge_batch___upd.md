---
type: "query"
date: "2026-05-08T00:23:29.769802+00:00"
question: "Why does Adapter.savePolicyLine bridge Batch & Update CRUD with Filtered Policy Loading, Constructor Minimal Surface, Persist & LoadPolicy Path, CasbinRule Schema & Queries, and Filter Query Helpers?"
contributor: "graphify"
source_nodes: ["Adapter.savePolicyLine", "CasbinRule struct", "Adapter.getTableInstance", "Adapter.SavePolicy", "Adapter.UpdateFilteredPolicies", "TestAdapters"]
---

# Q: Why does Adapter.savePolicyLine bridge Batch & Update CRUD with Filtered Policy Loading, Constructor Minimal Surface, Persist & LoadPolicy Path, CasbinRule Schema & Queries, and Filter Query Helpers?

## Answer

Adapter.savePolicyLine (adapter.go:486-516) is the shared encoder that converts a Casbin policy slice (Ptype, V0..V5/6/7) into a CasbinRule row. Every write-side method calls it: AddPolicy, RemovePolicy, AddPolicies, RemovePolicies, UpdatePolicy, UpdatePolicies, and SavePolicy. It also references CasbinRule struct (adapter.go:26-37) directly and calls Adapter.getTableInstance (adapter.go:334-336) to support custom-table row models. This puts it at the intersection of three Casbin interfaces (persist.Adapter via AC-001, persist.BatchAdapter via AC-003, persist.UpdatableAdapter via AC-004) and three structural communities: it is in C1 (Batch & Update CRUD) but its callers span C5 (Persist & LoadPolicy Path) and its references span C7 (CasbinRule Schema & Queries) and C9/C3 (via getTableInstance shared with NewAdapterByDBWithCustomTable). The Filtered Policy Loading bridge is indirect: Adapter.UpdateFilteredPolicies uses the same getTableInstance + CasbinRule.queryString/toStringPolicy helper triangle. Practical implication: any change to savePolicyLine affects three Casbin interface contracts simultaneously, so TestAdapters (adapter_test.go:496-607) is the load-bearing safety net, and getTableInstance schema alignment is the runtime invariant to preserve. This is also Constitution Principle V (Minimal Surface) made concrete: six constructors look divergent, but for the write path they all converge to this 30-line function plus getTableInstance.

## Source Nodes

- Adapter.savePolicyLine
- CasbinRule struct
- Adapter.getTableInstance
- Adapter.SavePolicy
- Adapter.UpdateFilteredPolicies
- TestAdapters