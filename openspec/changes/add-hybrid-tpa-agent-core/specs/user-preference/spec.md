# Spec Delta

## Purpose

接收並保存使用者的交易目標與風險承受度，讓下游的資料取得、決策與倉位計算都依使用者設定運作。

## ADDED Requirements

### Requirement: Accept trading target settings
系統 SHALL 接收交易標的代號與時間框架，作為一次分析的輸入。

#### Scenario: Valid target is accepted
- **WHEN** 使用者輸入有效的標的代號與支援的時間框架
- **THEN** 系統保存設定並以此啟動資料取得

#### Scenario: Unsupported timeframe is rejected
- **WHEN** 使用者輸入系統不支援的時間框架
- **THEN** 系統拒絕該設定並列出支援的時間框架

### Requirement: Accept risk tolerance
系統 SHALL 接收單筆交易最大風險（帳戶權益百分比）與帳戶權益，作為倉位計算的依據。

#### Scenario: Risk tolerance is used in sizing
- **WHEN** 使用者設定單筆最大風險為帳戶權益的 1%
- **THEN** 後續倉位計算所使用的可承受虧損金額等於帳戶權益的 1%

#### Scenario: Missing risk setting
- **WHEN** 使用者未設定單筆最大風險
- **THEN** 系統不產出任何 APPROVED 報告，並提示使用者完成風險設定
