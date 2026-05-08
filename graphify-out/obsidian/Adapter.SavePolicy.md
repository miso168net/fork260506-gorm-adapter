---
source_file: "adapter.go"
type: "code"
community: "Filtered Policy Loading"
location: "adapter.go:519-557"
tags:
  - graphify/code
  - graphify/EXTRACTED
  - community/Filtered_Policy_Loading
---

# Adapter.SavePolicy

## Connections
- [[AC-001 satisfy persist.Adapter interface]] - `references` [EXTRACTED]
- [[Adapter.savePolicyLine]] - `calls` [EXTRACTED]
- [[Adapter.truncateTable]] - `calls` [EXTRACTED]
- [[Filtered SavePolicy must not truncate unrelated rules (data-loss invariant)]] - `rationale_for` [EXTRACTED]
- [[Usage Scenario 1 - Persist Casbin policy to a relational database (P1)]] - `references` [EXTRACTED]
- [[Usage Scenario 3 - Filtered policy loading for large policy sets (P3)]] - `references` [EXTRACTED]
- [[initPolicy test helper]] - `calls` [EXTRACTED]

#graphify/code #graphify/EXTRACTED #community/Filtered_Policy_Loading