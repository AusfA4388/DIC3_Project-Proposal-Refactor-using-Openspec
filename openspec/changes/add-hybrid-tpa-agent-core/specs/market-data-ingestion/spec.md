# Spec Delta

## Purpose

取得目標標的的歷史與即時 OHLCV 資料，檢查資料品質，並在資料延遲或中斷時依分級協議降級，避免系統在不可靠的資料上產生訊號。

## ADDED Requirements

### Requirement: Fetch OHLCV data
系統 SHALL 依使用者設定的標的與時間框架，取得包含開盤、最高、最低、收盤價與成交量的 K 棒資料，並依時間先後排序。

#### Scenario: Data is returned in time order
- **WHEN** 系統為某標的與時間框架取得資料
- **THEN** 回傳的每根 K 棒都包含時間戳與 OHLCV 五個欄位，且時間戳嚴格遞增

### Requirement: Flag data quality issues
系統 SHALL 檢查缺漏 K 棒、重複時間戳與不合理價格（如最高價低於最低價），並為資料加上品質旗標。

#### Scenario: Missing bars are flagged
- **WHEN** 取得的資料中有缺漏的 K 棒
- **THEN** 系統將資料標記為品質異常，並記錄缺漏的時間區間

#### Scenario: Invalid bar is flagged
- **WHEN** 某根 K 棒的最高價低於最低價
- **THEN** 系統將該 K 棒標記為無效，且不將其用於後續計算

### Requirement: Use only information available at decision time
在回測與即時模式中，系統 MUST 只使用決策時間點以前已收盤的 K 棒，不得使用未來資料。

#### Scenario: No look-ahead in backtest
- **WHEN** 系統在回測中於時間 t 產生決策
- **THEN** 決策所使用的所有資料時間戳都早於或等於 t 時已收盤的 K 棒

### Requirement: Freeze new signals on data latency
當即時資料延遲超過 2 秒時，系統 SHALL 停止產生新的交易訊號，直到資料恢復正常。

#### Scenario: Latency above threshold
- **WHEN** 即時資料的延遲超過 2 秒
- **THEN** 系統不產生新的 APPROVED 報告，並在報告中顯示資料延遲狀態

### Requirement: Raise circuit-breaker alert on data outage
當即時資料中斷超過 30 秒時，系統 SHALL 發出熔斷警報，提醒交易者檢查未平倉部位。

#### Scenario: Outage above threshold
- **WHEN** 即時資料中斷超過 30 秒
- **THEN** 系統發出熔斷警報，且在資料恢復前持續停止產生新訊號
