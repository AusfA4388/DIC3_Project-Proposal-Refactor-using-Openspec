# Spec Delta

## Purpose

依供需區邊界、波動度與使用者風險設定，計算停損、停利、風險報酬比、期望值與倉位，並以門檻決定是否產出交易設定，落實風險優先原則。

## ADDED Requirements

### Requirement: Derive stop-loss from zone boundary
做多訊號的停損價 SHALL 設於需求區下緣之外，並加上以 ATR 倍數計算的緩衝距離；做空訊號依供給區上緣對稱處理。

#### Scenario: Long stop-loss placement
- **WHEN** 系統為位於需求區的做多訊號計算停損
- **THEN** 停損價等於需求區下緣減去 ATR 乘以緩衝倍數

### Requirement: Derive take-profit from next opposing zone
做多訊號的停利價 SHALL 設於進場價上方最近一個供給區的下緣；做空訊號依需求區對稱處理。

#### Scenario: No opposing zone found
- **WHEN** 進場價上方不存在任何供給區
- **THEN** 系統不計算停利價，並將該訊號判定為 WAIT／NO_TRADE，原因註明缺少目標區

### Requirement: Compute risk-reward and expected value
系統 SHALL 計算 RR =（停利價 − 進場價）÷（進場價 − 停損價），以及期望值 E = W × RR − (1 − W)。

#### Scenario: Expected value example
- **WHEN** W 為 0.55 且 RR 為 2.0
- **THEN** 系統計算出 E 為 0.65

### Requirement: Approve only when both thresholds are met
系統 SHALL 僅在 W ≥ 0.55 且 RR ≥ 2.0 時將訊號判定為 APPROVED，否則判定為 WAIT／NO_TRADE 並附上未達標的項目。

#### Scenario: Win rate below threshold
- **WHEN** W 為 0.50 且 RR 為 3.0
- **THEN** 訊號判定為 WAIT／NO_TRADE，原因註明勝率未達門檻

#### Scenario: Both thresholds met
- **WHEN** W 為 0.60 且 RR 為 2.5
- **THEN** 訊號判定為 APPROVED

### Requirement: Size position by risk budget
系統 SHALL 以「可承受虧損金額 ÷ 每單位停損距離」計算倉位數量，並無條件捨去至可交易的最小單位。

#### Scenario: Position size calculation
- **WHEN** 可承受虧損為 1,000 元，進場價 100 元，停損價 98 元
- **THEN** 系統計算出的倉位為 500 單位
