# Contributing Guide

歡迎來貢獻！本份文件補充 [README.md](README.md) 中沒有的協作細節。如果你是第一次參與，請先讀完 README 的任務一。

> **TL;DR**：分支用 `feature/<scope>-<desc>`、commit 用 Conventional Commits、發 PR 後等 CI 綠燈與學長 review、修完評論再 re-request review。

---

## 1. 分支命名

| 用途 | 格式 | 範例 |
|------|------|------|
| 任務一自我介紹 | `feature/intro-<學號>` | `feature/intro-M11315001` |
| 新功能 / 練習 | `feature/<scope>-<desc>` | `feature/ros-topic-demo` |
| Bug 修正 | `fix/<short-desc>` | `fix/docker-x11-mac` |
| 文件 | `docs/<area>` | `docs/contributing` |
| 雜項 / 設定 | `chore/<desc>` | `chore/update-gitignore` |

- 不允許直接 push 到 `main`。
- 完成合併後 head branch 會被自動刪除，本機可 `git branch -d <branch>` 跟著清掉。

## 2. Commit 訊息（Conventional Commits）

格式：`<type>(<scope>): <subject>`

| Type | 用途 |
|------|------|
| `feat` | 新功能 |
| `fix` | Bug 修正 |
| `docs` | 純文件 |
| `chore` | 不影響行為的雜項（CI、設定、相依） |
| `refactor` | 不改變行為的重構 |
| `test` | 新增/修改測試 |

範例：

```
docs(intro): add self-introduction for M11315001
feat(turtle): add square-pattern turtle controller node
fix(docker): correct DISPLAY env on macOS
```

- subject 用祈使句、< 72 字。
- 必要時用空一行後加 body 詳述「為什麼」這樣改。

## 3. PR 流程

1. **發 PR 前**：本機已 commit、已 push、已 `git pull --rebase origin main` 跟上最新主幹。
2. **發 PR 時**：PR 模板會自動帶入，請逐項勾選；CODEOWNERS（`@chenbenlu`）會被自動指派為 reviewer，**無需手動加**。
3. **CI 必須通過**：`Validate student introduction` 是 main 的 required check，紅燈擋 merge。
4. **回應 review**：學長給意見後在本機修改 → 同分支再 commit / push（GitHub 會自動更新 PR）→ 在評論串回覆 → **重新點 reviewer 旁邊的 🔄 re-request review**。
5. **合併方式**：三種都允許，預設用 **Squash merge** 保持 main 線性歷史。

## 4. Review 守則

### 學長（reviewer）

- 收到 review 請求後 **48 小時內** 給出第一輪回覆（哪怕只是「我下週看」）。
- 對「新生第一次 PR」優先給予正面回饋，再提改進建議。
- 若 PR 沒問題，approve 並留下一句鼓勵；若還要改，使用 `Request changes`。

### 新生（PR 作者）

- 每個 review comment 都要回覆（採納就改 + 留「done」，不採納就解釋）。
- 不要關掉 PR 重開——直接在原分支修。
- CI 紅燈時讀 log、修原因、再 push；不要 force push 蓋掉歷史（PR 期間 force push 會讓 reviewer 看不到你後續的改動）。

## 5. 與 README 的關係

- **README.md**：給「第一次參與」的人看的入門教學（任務一、任務二、X11 設定）。
- **CONTRIBUTING.md**（本文件）：通用協作規格，查得到分支命名、commit 規則、review 流程。

兩份文件若不一致以本文件為準，並請開 PR 同步 README。

---

有任何不清楚的地方，發 issue 或在 LINE `#系統工程實驗室` 提問。
