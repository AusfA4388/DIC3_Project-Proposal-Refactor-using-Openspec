# Proposal

## Why

DIC4 要求把期末專題寫成 IEEE 會議論文初稿，在 Overleaf 上撰寫，並以 MCP 與 OpenSpec 管理寫作流程。DIC3 已完成 Abstract（A–F）、Introduction、Related Work 與 18 篇查證過的參考文獻，但仍是中文 Markdown，且缺少論文需要的方法章節、演算法與實驗計畫。本 change 把這些內容整合成一份可編譯、可在 Overleaf 繼續協作的英文 LaTeX 初稿。

## What Changes

- 新增 `paper/`：IEEE 會議格式（IEEEtran, conference）LaTeX 原始檔、BibTeX 參考文獻與以 TikZ 繪製的架構圖。
- 論文章節：Abstract、Index Terms、Introduction、Related Work、Design Principles、Proposed System、Experimental Plan、Conclusion、References。
- 論文中的 Algorithm 1 依 `add-hybrid-tpa-agent-core` 的 specs 撰寫（停損停利由風控引擎計算、LLM 不產生數值），與原期中 Pseudocode 不同之處列於 design.md。
- 新增 `paper/OVERLEAF_MCP.md`：以 Overleaf MCP 將 Claude Desktop 連接到 Overleaf 專案的設定與操作步驟。
- 影響的 Cores：論文呈現 C1–C5，不改變系統規格。

不在範圍內：實驗結果（尚未實作）、投稿特定會議的格式細節（頁數上限、匿名審查）。

## Capabilities

### New Capabilities
- `conference-paper`: 專題會議論文的格式、章節完整性、引用可追溯性、與系統規格的一致性，以及 Overleaf 同步流程的規範。

### Modified Capabilities

## Impact

- 新增 `paper/` 資料夾與 `paper/OVERLEAF_MCP.md`。
- 外部相依：Overleaf 專案、Overleaf Git integration token、Claude Desktop 與 Node.js 18 以上（MCP 伺服器 `@mjyoo2/overleaf-mcp`）。
- 不影響 `openspec/specs/` 中的既有規格與 `add-hybrid-tpa-agent-core` 的系統規格。
