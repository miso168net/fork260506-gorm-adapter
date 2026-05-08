---
source_file: "adapter.go"
type: "code"
community: "Filtered Policy Loading"
location: "adapter.go:427-445"
tags:
  - graphify/code
  - graphify/EXTRACTED
  - community/Filtered_Policy_Loading
---

# Adapter.LoadFilteredPolicy

## Connections
- [[AC-002 satisfy persist.FilteredAdapter interface]] - `references` [EXTRACTED]
- [[Adapter.filterQuery]] - `calls` [EXTRACTED]
- [[Filter struct]] - `references` [EXTRACTED]
- [[Filtered SavePolicy must not truncate unrelated rules (data-loss invariant)]] - `rationale_for` [EXTRACTED]
- [[Usage Scenario 3 - Filtered policy loading for large policy sets (P3)]] - `references` [EXTRACTED]
- [[loadPolicyLine]] - `calls` [EXTRACTED]
- [[testFilteredPolicy]] - `references` [INFERRED]

#graphify/code #graphify/EXTRACTED #community/Filtered_Policy_Loading