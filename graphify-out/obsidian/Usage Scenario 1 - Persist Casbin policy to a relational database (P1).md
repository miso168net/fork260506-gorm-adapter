---
source_file: "docs/superpowers/specs/2026-05-07-gorm-adapter-baseline-design.md"
type: "document"
community: "Persist & LoadPolicy Path"
location: "lines 22-52"
tags:
  - graphify/document
  - graphify/EXTRACTED
  - community/Persist__LoadPolicy_Path
---

# Usage Scenario 1 - Persist Casbin policy to a relational database (P1)

## Connections
- [[Adapter.AddPolicy]] - `references` [EXTRACTED]
- [[Adapter.LoadPolicy]] - `references` [EXTRACTED]
- [[Adapter.SavePolicy]] - `references` [EXTRACTED]
- [[CasbinRule struct]] - `references` [EXTRACTED]
- [[NewAdapter constructor]] - `references` [EXTRACTED]
- [[gorm-adapter Baseline Reference Spec]] - `references` [EXTRACTED]

#graphify/document #graphify/EXTRACTED #community/Persist__LoadPolicy_Path