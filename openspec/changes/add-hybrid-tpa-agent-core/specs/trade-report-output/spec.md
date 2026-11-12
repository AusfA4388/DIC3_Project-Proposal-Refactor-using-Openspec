# Spec Delta

## Purpose

將決策結果整理成含數學依據與價格行為依據的結構化報告，交由交易者確認後才執行，確保系統是決策輔助而非自動下單。

## ADDED Requirements

### Requirement: Structured report fields
每份報告 SHALL 包含狀態（APPROVED 或 WAIT／NO_TRADE）、標的、時間框架、產生時間、W、RR、E，以及推理依據；狀態為 APPROVED 時另包含進場價、停損價、停利價與倉位。

#### Scenario: Approved report is complete
- **WHEN** 系統產出一份 APPROVED 報告
- **THEN** 報告包含上述所有欄位，且沒有任何欄位為空

#### Scenario: Rejected report explains why
- **WHEN** 系統產出一份 WAIT／NO_TRADE 報告
- **THEN** 報告列出未達標的項目或失敗原因

### Requirement: Evidence chain in report
報告 SHALL 列出決策所依據的供需區、勝率來源、引用的知識庫規則識別碼與資料品質狀態，讓交易者能追溯每一個數字的來源。

#### Scenario: Evidence is traceable
- **WHEN** 交易者檢視一份 APPROVED 報告
- **THEN** 報告中的停損與停利價格都能對應到列出的供需區邊界

### Requirement: Human confirmation before execution
系統 MUST NOT 自動送出任何委託；APPROVED 報告只作為建議，須由交易者確認後才執行。

#### Scenario: No automatic order
- **WHEN** 系統產出 APPROVED 報告
- **THEN** 系統不送出任何委託，並等待交易者確認

### Requirement: Display degraded state
當資料品質異常或系統處於降級狀態時，報告 SHALL 明顯標示該狀態。

#### Scenario: Degraded data warning
- **WHEN** 產生報告時資料品質旗標為異常
- **THEN** 報告最上方顯示資料異常警告
