# Spec Delta

## Purpose

以可檢索、可引用的形式提供價格行為學與風控規則，讓 LLM 推理有明確的領域依據，而不依賴模型自身記憶。

## ADDED Requirements

### Requirement: Provide price action rules
知識庫 SHALL 至少包含 S/R Flip、假突破、Pinbar／Hammer 回測確認、風險優先原則與風險報酬比公式等規則，且每條規則有唯一識別碼。

#### Scenario: Rule lookup by identifier
- **WHEN** 推理代理人以規則識別碼查詢
- **THEN** 知識庫回傳該規則的名稱、適用條件與說明

### Requirement: Retrieve rules relevant to context
知識庫 SHALL 依目前的市場情境（如價格位於需求區、剛跌破區域）回傳相關規則。

#### Scenario: Context-based retrieval
- **WHEN** 輸入情境為價格回測需求區
- **THEN** 回傳的規則包含回測確認與停損位置相關規則

### Requirement: Rules are traceable in reports
每一則被推理引用的規則 SHALL 能在最終報告中以識別碼追溯。

#### Scenario: Cited rule appears in report
- **WHEN** 推理過程引用某條規則
- **THEN** 最終報告的推理依據中列出該規則的識別碼與名稱
