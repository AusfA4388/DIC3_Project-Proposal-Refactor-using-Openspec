# Spec Delta

## Purpose

以確定性演算法辨識 K 線上的供給區與需求區，提供可重現的空間結構資訊，作為勝率預測、LLM 推理與停損停利計算的共同基礎。

## ADDED Requirements

### Requirement: Detect swing points
系統 SHALL 依可設定的回看長度，從 K 棒資料中辨識波段高點（Swing High）與波段低點（Swing Low）。

#### Scenario: Swing high is detected
- **WHEN** 某根 K 棒的最高價高於其前後回看長度內所有 K 棒的最高價
- **THEN** 系統將該 K 棒標記為 Swing High

### Requirement: Output zones with boundaries
系統 SHALL 將供需區輸出為具有上緣、下緣、類型（Supply 或 Demand）、形成時間與被測試次數的區域，而非單一價格水平線。

#### Scenario: Zone record is complete
- **WHEN** 系統辨識出一個需求區
- **THEN** 該區域記錄包含上緣價格、下緣價格、類型為 Demand、形成時間與被測試次數，且上緣高於下緣

### Requirement: Confirm zones with volume
系統 SHALL 以成交量作為供需區的確認條件，只輸出形成時成交量達到設定門檻的區域。

#### Scenario: Low-volume zone is excluded
- **WHEN** 某個候選區域形成時的成交量低於設定門檻
- **THEN** 系統不將該候選區域輸出為供需區

### Requirement: Deterministic and reproducible output
相同的輸入資料與參數 MUST 產生完全相同的供需區結果。

#### Scenario: Re-run produces identical zones
- **WHEN** 以相同資料與參數重複執行供需區辨識兩次
- **THEN** 兩次輸出的區域數量、邊界與類型完全相同

### Requirement: Track zone role flip
當價格以收盤價有效跌破需求區時，系統 SHALL 將該區域標記為已轉換為壓力（S/R Flip）；有效突破供給區時亦同。

#### Scenario: Demand zone flips to resistance
- **WHEN** 某根 K 棒的收盤價低於需求區下緣
- **THEN** 系統將該區域標記為已失效的需求區並轉為壓力區，後續分析依新角色使用
