---
source_file: "adapter.go"
type: "code"
community: "Adapter Construction & DB Open"
location: "adapter.go:352-378"
tags:
  - graphify/code
  - graphify/EXTRACTED
  - community/Adapter_Construction_&_DB_Open
---

# Adapter.createTable

## Connections
- [[Adapter.Open]] - `calls` [EXTRACTED]
- [[Adapter.getFullTableName]] - `calls` [EXTRACTED]
- [[Adapter.getTableInstance]] - `calls` [EXTRACTED]
- [[NewAdapterByDBUseTableName()]] - `calls` [EXTRACTED]
- [[NewAdapterByDBWithCustomTable()]] - `shares_data_with` [INFERRED]
- [[TurnOffAutoMigrate()]] - `shares_data_with` [INFERRED]

#graphify/code #graphify/EXTRACTED #community/Adapter_Construction_&_DB_Open