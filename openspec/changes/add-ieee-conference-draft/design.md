# Design

## Context

論文內容來源：DIC3 的 `docs/proposal/`（A–F、Introduction、Related Work、18 篇已查證文獻）與 `add-hybrid-tpa-agent-core` 的八個系統規格。動機見 proposal.md，格式與內容規範見 `specs/conference-paper/spec.md`。

限制：
- 作者的 Overleaf 帳號可產生 Git integration token，但 Claude 的雲端工作環境無法連到 Overleaf 的 Git 伺服器（網路代理阻擋 `git.overleaf.com`）。
- 尚未實作，沒有任何實驗結果。

## Goals / Non-Goals

**Goals:**
- 產出一份可編譯、4–6 頁、符合 IEEE 會議格式的英文初稿。
- 論文與 OpenSpec 規格互相可追溯：每個模組對應一個 capability，演算法遵守規格中的數值責任分工。
- 提供在 Overleaf 上以 MCP 讓 AI 助手讀寫論文的工作流程。

**Non-Goals:**
- 不針對特定會議的投稿規則（匿名、版權聲明、頁數上限）調整。
- 不報告實驗結果。

## Decisions

### D1. GitHub 為原始檔的單一事實來源，Overleaf 為寫作與排版介面
- **選擇**：`paper/` 存放在 GitHub repo，由 OpenSpec 追蹤；Overleaf 專案以上傳方式建立，之後的修改透過 Overleaf MCP（`@mjyoo2/overleaf-mcp`）讀寫，再定期將 Overleaf 的版本同步回 GitHub。
- **理由**：GitHub Sync 是 Overleaf 付費功能；Git integration token 可用，但只能從作者自己的電腦連線。把 MCP 放在作者電腦的 Claude Desktop 上，可同時滿足「Overleaf」與「MCP」兩項要求。
- **替代方案**：
  - Overleaf GitHub Sync：付費功能，帳號顯示需升級。
  - 由雲端環境直接 `git push` 到 Overleaf：網路代理阻擋，且需要把 token 貼進對話。

### D2. Algorithm 1 依系統規格撰寫，而非照抄期中 Pseudocode
- **選擇**：停損停利由風控步驟計算；勝率直接取自 XGBoost；在呼叫 LLM 前先檢查資料品質與風險設定；倉位以風險預算計算。
- **理由**：論文中的演算法必須與架構圖、模組描述與 C3 原則一致；期中 Pseudocode 的不一致會在審查時被直接指出。
- **與期中 Pseudocode 的差異**（對應 `add-hybrid-tpa-agent-core/design.md` 待決議事項）：

| 待決議 | 期中 Pseudocode | 論文 Algorithm 1 |
|---|---|---|
| Q1 停損停利來源 | `PlannerAgent.reason()` 輸出 | 第 13 行由風控步驟計算 |
| Q2 勝率來源 | `evaluated_plan.win_probability` | 第 7 行 XGBoost 輸出 W |
| Q3 門檻判斷順序 | LLM 之後 | 仍在 LLM 之後（第 15 行），與 Pseudocode 相同 |
| Q4 倉位計算 | 無 | 第 16 行 |

- **後續**：若小組決議不同，需同時修改 `add-hybrid-tpa-agent-core` 的 spec 與論文。

### D3. 架構圖以 TikZ 重繪
- **選擇**：在 LaTeX 中以 TikZ 繪製英文架構圖。
- **理由**：原架構圖為中文標籤的點陣圖，不適合英文論文；TikZ 為向量圖，可在 Overleaf 直接修改文字。

### D4. 新聞引用的處理
- **選擇**：中文新聞以英文意譯標題並註明 "(in Chinese)"；不在正文使用報導自行估算的虧損金額。
- **理由**：pdflatex 無法直接排版中文，且只引用證交所統計數字可降低可信度疑慮。

## Risks / Trade-offs

- [Overleaf 與 GitHub 兩邊版本分歧] → 在 Overleaf 修改後，以 MCP `read_file` 取得最新內容並提交回 GitHub；tasks.md 列為固定步驟。
- [Git token 外洩] → token 只存在作者電腦的設定檔或 `OVERLEAF_GIT_TOKEN_FILE`，不寫入 repo，不貼進對話。
- [Algorithm 1 與小組最終決議不同] → D2 已列出差異；小組決議後同步修改。
- [第三方 MCP 伺服器的可靠性] → 以 `status_summary` 與 `list_files` 驗證連線；失敗時退回 Overleaf 網頁直接編輯。
