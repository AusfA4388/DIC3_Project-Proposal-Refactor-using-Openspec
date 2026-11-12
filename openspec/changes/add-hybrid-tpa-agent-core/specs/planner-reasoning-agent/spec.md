# Spec Delta

## Purpose

以 LLM 結合供需區結構、勝率與知識庫規則，對目前市場情境進行可解釋的語意推理，並產出交易計畫的情境判斷與理由。

## ADDED Requirements

### Requirement: Reason over structured input
推理代理人 SHALL 以結構化資料作為輸入，至少包含現價、供需區邊界與類型、勝率 W，以及知識庫回傳的相關規則。

#### Scenario: Structured context is assembled
- **WHEN** 系統呼叫推理代理人
- **THEN** 輸入內容為結構化格式，且包含上述所有欄位

### Requirement: Produce explainable reasoning
推理代理人 SHALL 輸出情境判斷（如回測確認、疑似假突破、結構不明）與逐步推理理由，並列出所引用的知識庫規則識別碼。

#### Scenario: Reasoning output is complete
- **WHEN** 推理代理人完成一次推理
- **THEN** 輸出包含情境判斷、推理理由與至少一個規則識別碼

### Requirement: Stay consistent with input values
推理代理人的輸出中引用的價格、區域邊界與勝率 MUST 與輸入的結構化資料一致。

#### Scenario: Inconsistent value is rejected
- **WHEN** 推理輸出中引用的區域邊界或勝率與輸入值不一致
- **THEN** 系統將該次推理標記為無效，且不據以產生 APPROVED 報告

### Requirement: Handle reasoning failure safely
當 LLM 呼叫失敗、逾時或輸出無法解析時，系統 SHALL 回報 WAIT／NO_TRADE 並說明原因，不得以預設值產生交易設定。

#### Scenario: LLM timeout
- **WHEN** 推理代理人逾時未回應
- **THEN** 系統產出狀態為 WAIT／NO_TRADE 的報告，原因註明推理失敗
