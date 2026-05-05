# Graphify session 紀錄 — 2026-05-06

本檔案記錄一次完整的 `/graphify` 知識圖譜建構與探索 session 的過程、發現與決定,用於日後追溯。

## 1. Session 元資料

| 項目 | 內容 |
|---|---|
| 日期 | 2026-05-06 |
| 工具 | Claude Code 內建 `/graphify` skill (graphify Python 套件) |
| 觸發指令 | `/graphify . --obsidian` |
| 工作目錄 | `/mnt/d/AnewSpaces/Local/x_Project/TEST-claude/fork-go-admin/fork260506-gorm-adapter` |
| 起始分支 | `main` (HEAD = `618f1d7`) |
| 產出分支 | `graphify-20260506` (已合併並刪除) |
| 合併 commit | `2e1e86d Merge pull request #1 from miso168net/graphify-20260506` |
| 內容 commit | `398bc54 chore(graphify): add knowledge graph snapshot 2026-05-06` |
| Pull Request | https://github.com/miso168net/fork260506-gorm-adapter/pull/1 (MERGED) |

## 2. 偵測結果

| 類別 | 數量 | 檔案 |
|---|---|---|
| code | 4 | `adapter.go`、`adapter_test.go`、`open.go`、`open_sqlite3.go` |
| document | 2 | `README.md`、`x_fork.branch-origin.md` |
| paper / image / video | 0 | — |
| 合計 | 6 files / ~6,044 words | — |

graphify 主動警告:「Corpus 只有 ~6,044 字,可能不需要圖譜」,但仍依使用者要求繼續執行(目的是體驗完整流程並產生 Obsidian vault)。

## 3. 抽取結果

| 階段 | nodes | edges |
|---|---|---|
| Step 3A AST(deterministic、Go AST parser) | 78 | 237 |
| Step 3B Semantic(1 個 general-purpose subagent,~133 秒) | 64 | 88(含 3 hyperedges) |
| Step 3C 合併 + 去重 | 121 | 325 |
| Step 4 重新 score(去重後) | 121 | 285 |
| **手動修正後最終值** | **121** | **282** |

## 4. Community 命名(10 個)

| ID | 名稱 | nodes | cohesion |
|---|---|---|---|
| 0 | Test Suite & Adapter Init | 27 | 0.22 |
| 1 | Adapter Policy Methods | 20 | 0.22 |
| 2 | CasbinRule Model & Policy CRUD | 20 | 0.16 |
| 3 | Adapter Construction & DB Open | 20 | 0.15 |
| 4 | Multi-DB Pool & Lifecycle | 16 | 0.18 |
| 5 | Filtered Policy Loading | 14 | 0.19 |
| 6 | DB Open Driver Switch | 1 | 1.00 |
| 7 | SQLite3 Open Helper | 1 | 1.00 |
| 8 | Logger Wiring | 1 | 1.00 |
| 9 | IsFiltered Check | 1 | 1.00 |

> Communities 6–9 是單節點、cohesion=1.0 的 thin communities,屬於圖譜結構的雜訊。

## 5. God Nodes(top 10)

1. `Adapter` — 27 edges(全圖最高)
2. `TestAdapters()` — 13 edges
3. `NewAdapter()` — 12 edges
4. `initPolicy()` — 12 edges
5. `CasbinRule` — 10 edges
6. `NewAdapterByDBUseTableName()` — 10 edges
7. `testAutoSave()` — 10 edges
8. `Adapter.savePolicyLine` — 10 edges
9. `NewAdapterByDBWithCustomTable()` — 9 edges
10. `testGetPolicy()` — 9 edges

## 6. Hyperedges(語意群組關係)

- **Multi-DB resolver setup flow** — `InitDbResolver`、`DbPool`、`specificPolicy`、`DbPool.switchDb`、`NewAdapterByMulDb`
- **Policy save/load round-trip** — `Adapter.SavePolicy`、`Adapter.LoadPolicy`、`Adapter.savePolicyLine`、`loadPolicyLine`、`CasbinRule`
- **Adapter constructor variants** — 6 個 `NewAdapter*` 變體 constructor

## 7. 探索對話追蹤(5 個追問)

### Q1. `Adapter` 為何橋接 5 個 community?(betweenness 0.217)

**結論:** 這是 Go 套件的典型 **God Object** 模式 — Casbin 的 `persist.Adapter`、`persist.FilteredAdapter`、`persist.UpdatableAdapter` 三個 interface 強制把 LoadPolicy / SavePolicy / AddPolicy / RemovePolicy / RemoveFilteredPolicy 全部綁在同一個 receiver 上。任何方法都掛在 `*Adapter` receiver,所以每個 community 物理上都「擁有」一個 method on `*Adapter`,造成高 betweenness。**架構上無法降低**,除非用 wrapper struct 拆三層,但會破壞 Casbin interface 契約。

### Q2. `README v3.0.3 table rename migration note` --rationale_for--> `CasbinRule` 是什麼故事?

**Graph 邊:** [INFERRED, conf 0.7]

**README.md:4-8 內文:** v3.0.3 之前 `NewAdapterByDB` 產出 `casbin_rules`(複數),之後固定為 `casbin_rule`(單數),用戶必須手動 migrate。

**程式碼對應:** `adapter.go:39-41` 的 `func (CasbinRule) TableName() string { return "casbin_rule" }` 是個**已凍結的相容性 lock**。任何想「整理掉」這兩行的 PR 都會悄悄破壞所有 v3.0.3+ 用戶的 schema。graphify 把這條 README → struct 的 rationale 邊抓出來,正是為了避免未來有人(或 LLM agent)誤判為冗餘程式碼。

### Q3. `README Customize table columns example` 怎麼示範繞過 `CasbinRule` schema?

**README.md:82-126 範例核心:**
```go
type CasbinRule struct {
    ID    uint   `gorm:"primaryKey;autoIncrement"`
    Ptype string `gorm:"size:512;uniqueIndex:unique_index"`  // 100 → 512
    V0..V5 string `gorm:"size:512;uniqueIndex:unique_index"`
}
a, _ := gormadapter.NewAdapterByDBWithCustomTable(db, &CasbinRule{})
```

**揭露兩件事:**
1. **CasbinRule 的形狀其實是凍結的 schema 契約** — README 說 _"the table structure must stay the same"_,等於告訴用戶能改 size、加 uniqueIndex,但**不能加減欄位、改名、改順序**。所有 query 都假設 `Ptype/V0..V7` 這 9 個欄位存在。
2. **用 `context.WithValue(customTableKey, t)` 傳 struct 是反模式但無解** — 因為 GORM 的 callback hook 會讀 context,adapter 必須在 GORM 內部呼叫鏈中途取出這個 struct,沒有其他注入點。是被 GORM API 形狀逼出來的。

### Q4. `NewAdapter()` 的 3 條 INFERRED 邊驗證

**問題邊:**
- `NewAdapter()` --calls [INFERRED]--> `initAdapter()`
- `NewAdapter()` --calls [INFERRED]--> `TestNilField()`
- `NewAdapter()` --calls [INFERRED]--> `TestAdapterWithMulDb()`

**驗證結論:** **3 條全部方向反了**。實際源碼是 test 函式呼叫 `NewAdapter()`,不是反過來。Go `_test.go` 檔在編譯時根本不在 production binary 裡,production 程式碼**絕對不可能**呼叫 test 函式。LLM subagent 在判斷無向 co-occurrence 時把方向猜反。

### Q5. graphify 工具本身的隱藏 bug

驗證 Q4 後發現,**Step 3A 的 Go AST extractor** 也產生了 3 條同類型 EXTRACTED(conf 1.0)邊:
- `NewAdapter()` --calls [EXTRACTED]--> `initAdapter test helper`
- `NewAdapter()` --calls [EXTRACTED]--> `TestAdapterWithMulDb`
- `NewAdapter()` --calls [EXTRACTED]--> `TestNilField`

這比 INFERRED 更難察覺 — `GRAPH_REPORT.md` 不會主動列為「需驗證」,且 confidence 是滿分 1.0。代表 graphify 的 Go AST extractor 在跨檔案 call 處理上有方向反轉的瑕疵,這是**工具層級的問題,不只是這次跑的雜訊**。

## 8. 手動修正(共 6 條邊)

| 動作 | 邊 | 原因 |
|---|---|---|
| 刪除 ×3 | `NewAdapter() --[INFERRED]--> {initAdapter, TestNilField, TestAdapterWithMulDb}` | LLM 推論方向錯,且違反 Go test 隔離 |
| 翻轉 ×3 | `NewAdapter() --[EXTRACTED]--> {initAdapter test helper, TestAdapterWithMulDb, TestNilField}` | AST extractor bug,改為 caller → callee |

**邊數變化:** 285 → 282

**注意事項:** 此圖建為 `directed: False`(undirected),所以對 networkx 演算法(cluster、betweenness、shortest_path)而言 `A--B` 與 `B--A` 拓撲完全等價,**這次翻轉不影響任何分析數據**。翻轉的價值在於未來任何人直接讀 `graph.json` 或 Cypher 匯出時,邊的方向不會誤導判斷。

**改善建議:** 下次跑 `/graphify . --directed --obsidian` 可建為 `DiGraph` 並一致保留方向。

## 9. 最終產出(`graphify-out/`)

```
GRAPH_REPORT.md    -  121 nodes / 282 edges / 10 communities,稽核報告
graph.json         -  原始圖譜資料(EXTRACTED 230 / INFERRED 51 / AMBIGUOUS 1)
graph.html         -  互動式圖譜,瀏覽器可開
obsidian/          -  131-note Obsidian vault + graph.canvas
cache/             -  semantic 抽取快取(下次 --update 會 hit)
manifest.json      -  下次 --update 用的快照
cost.json          -  累計 token 成本追蹤
```

**Token cost benchmark:** 4.9× reduction(naive corpus 8,058 tokens → avg query cost 1,642 tokens)

## 10. 未提交的環境檔案

- `graphify-out/.graphify_python` — Python 直譯器路徑,環境特定,**未納入 git**(亦非 `.gitignore`,因為下次跑 graphify 會自動重建)

## 11. Git workflow

```
1. git checkout -b graphify-20260506
2. git add graphify-out/{GRAPH_REPORT.md, graph.json, graph.html, cost.json, manifest.json, cache, obsidian}
   (排除 .graphify_python)
3. git commit -m "chore(graphify): add knowledge graph snapshot 2026-05-06"
   → 398bc54, 144 files changed, 10,514 insertions
4. git push -u origin graphify-20260506
5. gh pr create --base main --head graphify-20260506 --title "..."
   → PR #1
6. gh pr merge 1 --merge
   → 2e1e86d
7. git checkout main && git pull origin main
8. git branch -d graphify-20260506
9. git push origin --delete graphify-20260506
```

## 12. 對未來自己的提醒

1. **Go AST extractor 的方向反轉 bug 是 graphify 工具本身的問題**。下次跑時若看到 production code 有邊指向 test 函式,直接視為錯誤方向,不需逐條驗證。

2. **Undirected graph 的 source/target 順序只是顯示順序,不影響演算法**。要真正方向感知就用 `--directed` flag。

3. **小 corpus(< 10K 字)graphify 警告「不需要圖譜」是真的** — 以這次為例,單檔 `adapter.go` 約 4,400 字本來就能一次讀完,圖譜的價值主要在練習工具流程與產生 Obsidian vault 視覺化,而非 token 節省。

4. **`graphify-out/.graphify_python` 是環境特定檔**,移到別台機器或重灌 Python 後會失效。下次直接刪除讓 graphify 自動重建。

5. **回頭追 INFERRED 邊很有價值** — `README v3.0.3 migration` → `CasbinRule` 這條 rationale 邊把 README 的歷史警告與 `TableName()` 兩行程式碼綁在一起,是純讀程式碼絕對發現不了的「為什麼這段不能改」資訊。

## 13. 這次 session 沒做但下次可以試

- `--directed` 建立 DiGraph,真正保留邊方向
- `--graphml` 匯出 Gephi / yEd 可讀格式
- `--neo4j` 匯出 Cypher 並 push 到 Neo4j 做圖查詢
- `--mcp` 啟動 stdio MCP server,讓其他 agent 可即時查詢圖譜
- `--watch` 自動 rebuild on file change(配合長期維護)
- `graphify hook install` 安裝 git post-commit hook,每次 commit 自動更新 AST 部分

## 14. 注意事項

本檔案只記錄一次 graphify session 的過程與發現,不影響任何程式邏輯,可以安全忽略或刪除。
