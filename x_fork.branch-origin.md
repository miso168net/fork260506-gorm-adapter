# main 分支來源紀錄

本 `main` 分支建立於 **2026-05-06**,來自這個 repo 內既有的分支。

| 項目 | 內容 |
|---|---|
| 此 repo | `miso168net/fork260506-gorm-adapter` |
| 原始專案(推測) | `casbin/gorm-adapter`(可能透過 `go-admin-team/gorm-adapter` 中轉) |
| Fork 用途 | 個人學習與實驗用 fork |
| Fork 建立日 | 2026-05-06 |
| `main` 來源分支 | `master` |
| 建立時的來源 HEAD | `bc66b93` — Update go.mod(2022-11-27) |
| 原本的 default branch | `master` |
| 改用 main 的原因 | 統一所有個人 fork 的預設分支命名為 `main`。此 repo 在這份 fork 中已停滯。 |

## 歷史說明

- 原本的 default branch `master` 完整保留,沒有刪除或修改。
- `main` 是新建的分支,從 `master` 拉出,目的是對齊本專案實際的開發主線。
- 過程中沒有 squash、rebase 或改寫任何 commit 歷史。

## 如何比對 main 與 master 的差異

```bash
git log master..main --oneline      # 只在 main、不在 master 的 commit
git log main..master --oneline      # 只在 master、不在 main 的 commit
git diff master main -- .           # 兩條分支的內容差異
```

## 注意事項

本檔案只記錄 fork 的元資訊,不影響任何程式邏輯,可以安全忽略或刪除。
