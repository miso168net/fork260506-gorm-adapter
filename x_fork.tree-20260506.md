# 專案檔案結構與用途註解(2026-05-06 snapshot)

本檔案對應 `tree` 命令在 `fork260506-gorm-adapter/` 根目錄的輸出,
為每個檔案/目錄補上一行用途註解,作為閱讀程式碼前的索引。

- 命名沿用 `x_fork.graphify-20260506.md` 的「snapshot 日期」慣例。
- `graphify-out/` 為 graphify 工具自動生成的知識圖譜目錄,僅以一行
  帶過其作用,不展開內容。
- 其餘 Go 原始碼、設定、文件每一檔都附註解。

```
.
├── CLAUDE.md                             # 給 Claude Code 看的專案指令(graphify 規則 + 圖譜優先導覽)
├── LICENSE                               # Apache 2.0 授權書(沿用 upstream casbin/gorm-adapter)
├── README.md                             # 函式庫使用說明(driver 列表、constructor 範例、自訂表名 / AutoMigrate 開關)
├── adapter.go                            # 主程式:Adapter / CasbinRule / Filter / DbPool + 6 個 constructor + persist 介面實作
├── adapter_test.go                       # 完整測試套件(TestAdapters 為總入口,涵蓋各 driver / 特性子測試)
│
├── examples/                             # Casbin RBAC 範例(README 與測試共用的 model + policy)
│   ├── rbac_model.conf                   # 基本 RBAC 模型定義(角色 / 權限 / 動作)
│   ├── rbac_policy.csv                   # 基本 RBAC policy 種子資料
│   ├── rbac_with_domains_model.conf      # 多租戶 RBAC(含 domain)模型
│   └── rbac_with_domains_policy.csv      # 多租戶 RBAC policy 種子資料
│
├── go.mod                                # Go module 宣告(github.com/go-admin-team/gorm-adapter/v3, go 1.14)
├── go.sum                                # 依賴版本鎖定檔
│
├── graphify-out/                         # graphify 知識圖譜輸出(整個目錄由工具生成:GRAPH_REPORT/graph.html/graph.json/cache/obsidian/...;勿手改)
│
├── open.go                               # Driver 開啟邏輯(MySQL / PostgreSQL / SQL Server)— build tag `!sqlite3`
├── open_sqlite3.go                       # Driver 開啟邏輯(含 SQLite3)— build tag `sqlite3`,實際 import `gorm.io/driver/sqlite`(⚠ README 段落寫 glebarez,實 code 與其不符)
│
├── x_fork.branch-origin.md               # fork 由來說明(本 main 自 master@bc66b93 拉出,master 已停滯)
└── x_fork.graphify-20260506.md           # graphify session 紀錄(本次 fork 生圖譜過程)
```

---

## 補充說明

**幾個重要慣例**:

- `*_test.go` 一律是 Go 標準測試檔(本專案僅 `adapter_test.go` 一個,
  以 `TestAdapters` 為對外總入口,內部呼叫一系列小寫 `test*` helper)。
- `open.go` 與 `open_sqlite3.go` 透過 Go build tag 互斥編譯。預設
  (不下 `-tags`)用 `open.go`,**不含 SQLite**;下 `-tags sqlite3` 才換成
  `open_sqlite3.go`。憲章 Principle II「Cross-Database Parity」需配合
  此 build tag 前提理解。
- 6 個 public constructor(`NewAdapter` / `NewAdapterByDB` /
  `NewAdapterByDBUseTableName` / `NewAdapterByDBWithCustomTable` /
  `NewFilteredAdapter` / `NewAdapterByMulDb`)共用 `(a *Adapter).Open()`
  作為收斂點;新增 constructor 受憲章 Principle V「Minimal Surface」約束。
- `x_fork.*` 開頭的檔案都是這份 fork 的 meta 紀錄,不影響任何程式邏輯,
  可安全忽略或刪除(可參考 `x_fork.branch-origin.md` 的尾註)。憲章
  Principle IV「Fork Hygiene & Upstream Traceability」要求所有 fork 差異
  以此格式留痕。

**最常被引用的 god nodes**(來自 graphify GRAPH_REPORT):

| 節點 | 所在檔案 | 邊數 |
|---|---|---|
| `Adapter` | `adapter.go` | 27 |
| `TestAdapters()` | `adapter_test.go` | 13 |
| `initPolicy()` | `adapter_test.go` | 12 |
| `CasbinRule` | `adapter.go` | 10 |
| `NewAdapterByDBUseTableName()` | `adapter.go` | 10 |
| `testAutoSave()` | `adapter_test.go` | 10 |
| `Adapter.savePolicyLine` | `adapter.go` | 10 |
| `NewAdapter()` | `adapter.go` | 9 |
| `NewAdapterByDBWithCustomTable()` | `adapter.go` | 9 |
| `testGetPolicy()` | `adapter_test.go` | 9 |

讀程式碼建議從 `Adapter`(主結構)出發,沿著 6 個 constructor 看初始化路徑,
再讀 `LoadPolicy` / `SavePolicy` 的 round-trip 即可掌握全貌。`adapter_test.go`
的 `TestAdapters` 是行為合約的事實清單。

---

*本檔案於 2026-05-08 由 Claude Code 依 `tree` 輸出生成,日期 `20260506`
沿用 fork 的 snapshot 命名慣例(對齊 `x_fork.graphify-20260506.md`)。*
