# Claude Code Subagent 團隊定義

一套「主 agent 派工、subagent 執行、PM 決策」的開發團隊定義，供 Claude Code 全域使用（跨專案共用）。

## 安裝

```bash
git clone https://github.com/timwei0801/AI_Agent_For_Full_Stack_Engineer.git ~/.claude/agents
```

已安裝過的機器更新：

```bash
cd ~/.claude/agents && git pull
```

## 結構

```
~/.claude/agents/
├── _PROTOCOL.md          ★ 派工協定：所有 agent 共同遵守（任務書格式、統一回報格式、
│                           DoD、阻塞協定、scope 鎖、一次性回覆、產出路徑、git 規範）
├── product-manager.md    PRD
├── tech-lead.md          架構／技術選型／schema／任務拆解／ADR
├── research-analyst.md   技術、資料源、市場、競品調研
├── backend-engineer.md   所有非 UI 程式碼（服務端、資料管線、腳本、ML）
├── frontend-engineer.md  UI 層（web、儀表板、TUI、通知模板）
├── qa-code-reviewer.md   實跑測試＋逐檔審查，只審不修，APPROVE／REQUEST_CHANGES
├── devops-engineer.md    容器化、CI、部署、排程、密鑰、備份、監控、runbook
└── risk-manager.md       專案健康度與風險（讀 PROJECT_STATE、issues、commit；不訪談人）
```

設計原則：

- **角色檔只寫該角色與眾不同的部分**；共同規則在 `_PROTOCOL.md`，每個角色檔第一句是「先讀協定」。
- **不預設專案類型與技術棧**（web／資料管線／ML／CLI 皆可用）；專案特有規範由各專案根目錄的 `CLAUDE.md` 帶入，且**專案 CLAUDE.md 優先於協定**。
- `model: inherit`：模型由主 agent 派工時決定（Agent tool 的 `model` 參數可逐次覆寫）。
- 文件角色（PM／RA／RM）有 `tools` 白名單，不寫程式；工程角色用完整工具。

## 搭配的專案側設定

每個專案根目錄需要一份 `CLAUDE.md`（專案憲法）與 `docs/PROJECT_STATE.md`（交接文件），內容包含：角色分工（PM＝使用者、主 agent＝主導人）、工作原則、開發流程、GitHub Issues 規範、文件地圖、換 session 交接 SOP。範例見 AI_invest 專案。

## 版本

- v2（2026-08）：整體重構——新增 `_PROTOCOL.md`，8 個角色檔由 12.8K 行精簡至約 1.2K 行，去 web／電商／K8s 化，修正一次性 subagent 不適用的中途對話模板、雙 frontmatter、舊工具名、預填假數字。
- v1（2025-11）：初版（web 全端導向）。
