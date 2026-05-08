---
type: "query"
date: "2026-05-08T00:29:36.714481+00:00"
question: "How many write paths does TestAdapters cover, and which ACs lack direct test verification?"
contributor: "graphify"
source_nodes: ["TestAdapters", "Adapter.SavePolicy", "Adapter.AddPolicies", "Adapter.UpdatePolicy", "AC-011 driver-specific code stays in open.go / open_sqlite3.go"]
---

# Q: How many write paths does TestAdapters cover, and which ACs lack direct test verification?

## Answer

Out of 9 canonical write-path methods that AC-001/003/004 promise (AddPolicy, RemovePolicy, RemoveFilteredPolicy, AddPolicies, RemovePolicies, UpdatePolicy, UpdatePolicies, UpdateFilteredPolicies, SavePolicy), only 3 are reachable from any Test* function within graph depth 2 (AddPolicy/RemovePolicy/RemoveFilteredPolicy via testAutoSave INFERRED edges). The other 6 — including SavePolicy — show no direct test edges. Caveat: graph extraction may underreport because Casbin tests typically invoke methods via enforcer.AddPolicies(...) which lives in casbin/casbin/v2, outside this repo's graph scope. Under loose undirected depth-3 reachability, 10 of 11 ACs are connected to a test (AC-001 through AC-010). AC-011 (driver-specific code stays in open.go/open_sqlite3.go) is the single uncovered AC and cannot be unit-tested — it is a code-organization invariant only enforceable via review or static analysis. Concrete spec follow-ups: add TestSavePolicy_FullCycle, TestBatchAdapter, TestUpdatableAdapter, TestAddLogger to make AC verification observable in the graph; reclassify AC-011 as review-verified rather than test-verified.

## Source Nodes

- TestAdapters
- Adapter.SavePolicy
- Adapter.AddPolicies
- Adapter.UpdatePolicy
- AC-011 driver-specific code stays in open.go / open_sqlite3.go