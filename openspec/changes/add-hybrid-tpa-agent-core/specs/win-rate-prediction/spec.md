# Spec Delta

## Purpose

將價格與供需區的相對位置及技術指標轉為特徵，以機器學習估計價格在該位置反彈或突破的機率 W，供決策與推理使用。

## ADDED Requirements

### Requirement: Extract spatial and technical features
系統 SHALL 為每個候選訊號萃取特徵，至少包含現價與最近供需區的距離、區域寬度、ATR、成交量 Z-score 與動量指標。

#### Scenario: Feature vector is complete
- **WHEN** 系統為一個位於需求區附近的候選訊號萃取特徵
- **THEN** 特徵中包含上述每一項，且所有數值皆只由決策時間點以前的資料計算

### Requirement: Output win probability
系統 SHALL 為每個候選訊號輸出 0 到 1 之間的勝率 W。

#### Scenario: Probability range
- **WHEN** 模型對一個候選訊號進行預測
- **THEN** 輸出的 W 大於等於 0 且小於等於 1

### Requirement: Define win label by barrier hit order
訓練標籤 SHALL 定義為：在 N 根 K 棒內，價格先觸及停利價位者為勝，先觸及停損價位或時間到期者為負。

#### Scenario: Take-profit hit first
- **WHEN** 某訓練樣本在 N 根 K 棒內先觸及停利價位
- **THEN** 該樣本的標籤為勝

#### Scenario: Neither barrier hit
- **WHEN** 某訓練樣本在 N 根 K 棒內未觸及停利或停損
- **THEN** 該樣本的標籤為負

### Requirement: Time-ordered evaluation
模型的訓練與測試資料 MUST 依時間先後切分，測試資料的時間 SHALL 全部晚於訓練資料。

#### Scenario: No overlap between train and test periods
- **WHEN** 系統建立訓練集與測試集
- **THEN** 測試集中最早的樣本時間晚於訓練集中最晚的樣本時間

### Requirement: Report calibration
模型評估 SHALL 同時報告分類準確率與機率校準指標（如 Brier score），因為決策門檻直接使用 W 的數值。

#### Scenario: Evaluation report includes calibration
- **WHEN** 模型完成一次測試集評估
- **THEN** 評估結果同時包含準確率與至少一項校準指標
