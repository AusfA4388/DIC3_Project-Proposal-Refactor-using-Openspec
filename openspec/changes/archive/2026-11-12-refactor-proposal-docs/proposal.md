# Proposal

## Why

期中 Proposal 的 Introduction 沒有任何數據與引用，Related Work 只有一篇有出處的文獻且缺少規範要求的 Article Summary Table，Abstract 也沒有依 A–F 分段。這些項目合計占 Proposal 評分的 40%（Introduction 20%、Related Work 20%），且期末口試會針對證據來源提問，因此需要在進入實作前先完成文件重構。

## What Changes

- 新增專題核心定義：Abstract A–F、5 Cores、3 Trade-offs、10 Details（`docs/proposal/00-core-definition.md`）。
- 依 A2Z SOP G–L 重寫 Introduction（`docs/proposal/01-introduction.md`）。
- 依 A2Z SOP M、O 重寫 Related Work，新增 Article Summary Table 與四段式研究缺口歸納（`docs/proposal/02-related-work.md`）。
- 新增經查核的參考文獻清單（`docs/proposal/references.md`）。
- 不修改原 Proposal 的 Pseudocode、Flowchart 與架構圖；發現的不一致記錄於 `add-hybrid-tpa-agent-core` 的 design.md。

## Capabilities

### New Capabilities
- `proposal-document`: 專題提案文件的內容與品質規範，包括摘要結構、緒論結構、相關研究的文獻比較，以及引用與預期成果的誠實揭露。

### Modified Capabilities

## Impact

- 影響文件：`docs/proposal/` 下四份 Markdown 文件。
- 不影響任何程式碼或系統行為規格。
- 後續 Proposal Word 檔與簡報應以本次重構內容為準更新。
