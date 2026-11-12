# Proposal

## Why

非專業短線交易者必須在極短時間內同時完成結構判斷、機率判斷與風險計算，而現有工具只解決其中一部分：技術指標 ML 缺乏結構位置資訊，S/R 演算法無法評估勝率，LLM 代理人則有數值不可靠與回測偏誤的問題（見 `docs/proposal/02-related-work.md`）。本 change 將小組 Proposal 第 4、5 章的系統設計轉為 OpenSpec 規格，作為期末實作的依據。

## What Changes

- 建立 Hybrid TPA-Agent 第一版的八個核心能力規格，對應 Proposal 的四層八模組架構。
- 將 5 Cores 與 10 Details（`docs/proposal/00-core-definition.md`）轉為可測試的 requirement 與 scenario。
- 在 design.md 記錄架構決策、風險，以及原 Proposal 中待小組決議的不一致之處。
- 在 tasks.md 列出實作步驟，每個步驟附驗證方式。

## Capabilities

### New Capabilities
- `user-preference`: 接收與保存交易標的、時間框架與風險承受度等使用者設定（模組 1.1，Detail D1）。
- `market-data-ingestion`: 取得歷史與即時 OHLCV 資料、檢查資料品質，並在資料異常時降級（模組 1.2，Detail D2、D10）。
- `supply-demand-zone-detection`: 以確定性演算法辨識供需區（模組 2.1，Core C1，Detail D3）。
- `win-rate-prediction`: 萃取空間與技術特徵，以機器學習估計突破或反彈勝率（模組 2.2，Core C2，Detail D4、D5）。
- `price-action-knowledge-base`: 提供價格行為與風控規則，作為推理依據（模組 3.1，Detail D6）。
- `planner-reasoning-agent`: 以結構化資料與知識庫規則進行情境推理（模組 3.2，Core C3，Detail D7）。
- `trade-decision-risk`: 計算停損、停利、風報比、期望值與倉位，並依門檻做出決策（模組 4.1，Core C4，Detail D8、D9）。
- `trade-report-output`: 產出含證據鏈的結構化交易報告，並保留人工確認（模組 4.2，Core C5，Detail D10）。

### Modified Capabilities

## Impact

- 新增系統程式碼（尚未實作）：資料接收、供需區演算法、ML 模型、知識庫、LLM 推理、風控與報告輸出。
- 外部相依：行情資料來源（API 或歷史檔案）、LLM API、機器學習套件。
- 系統定位為決策輔助，不包含自動下單；任何下單動作都需由交易者確認。
