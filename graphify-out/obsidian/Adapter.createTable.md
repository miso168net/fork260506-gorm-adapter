---
source_file: "adapter.go"
type: "code"
community: "AutoMigrate Discipline"
location: "adapter.go:352-378"
tags:
  - graphify/code
  - graphify/EXTRACTED
  - community/AutoMigrate_Discipline
---

# Adapter.createTable

## Connections
- [[AC-007 AutoMigrate runs unless TurnOffAutoMigrate called]] - `references` [INFERRED]
- [[Adapter.Open]] - `calls` [EXTRACTED]
- [[Adapter.getFullTableName]] - `calls` [EXTRACTED]
- [[Adapter.getTableInstance]] - `calls` [EXTRACTED]
- [[NewAdapterByDBUseTableName]] - `calls` [EXTRACTED]
- [[NewAdapterByDBWithCustomTable]] - `shares_data_with` [INFERRED]
- [[TurnOffAutoMigrate]] - `shares_data_with` [INFERRED]

#graphify/code #graphify/EXTRACTED #community/AutoMigrate_Discipline