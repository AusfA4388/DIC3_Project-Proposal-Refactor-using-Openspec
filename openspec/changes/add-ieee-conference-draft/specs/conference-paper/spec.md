# Spec Delta

## Purpose

規範 Hybrid TPA-Agent 會議論文初稿的格式、內容完整性與誠實揭露，並確保論文內容與 OpenSpec 系統規格一致、可在 Overleaf 上持續協作。

## ADDED Requirements

### Requirement: IEEE conference format
論文 SHALL 使用 IEEEtran 文件類別的 conference 選項，以雙欄格式排版，並能在不經手動修改的情況下編譯成 PDF。

#### Scenario: Clean compile
- **WHEN** 以 pdflatex 與 bibtex 編譯 `paper/main.tex`
- **THEN** 產生 PDF，且沒有未定義的引用或參照警告

### Requirement: Page budget
論文初稿含參考文獻 SHALL 不超過 6 頁。

#### Scenario: Page count check
- **WHEN** 檢查編譯後 PDF 的頁數
- **THEN** 頁數小於等於 6

### Requirement: Required sections
論文 SHALL 包含 Abstract、Index Terms、Introduction、Related Work、Design Principles、Proposed System、Experimental Plan、Conclusion 與 References。

#### Scenario: Section completeness
- **WHEN** 審查者瀏覽 PDF 的章節標題
- **THEN** 上述每一個章節都存在且順序合理

### Requirement: Technical representations
Proposed System 章節 SHALL 包含一張系統架構圖與一個附行號的演算法，且圖與演算法中的每個模組都能對應到 `add-hybrid-tpa-agent-core` 的一個 capability。

#### Scenario: Module traceability
- **WHEN** 審查者比對架構圖中的模組與 OpenSpec capability 清單
- **THEN** 八個模組各自對應到一個 capability

### Requirement: Consistency with system specs
論文對數值責任的描述 MUST 與系統規格一致：供需區由確定性演算法產生、勝率由 ML 模型產生、停損停利與倉位由風控引擎計算，LLM 不產生任何價格或機率。

#### Scenario: Algorithm matches specs
- **WHEN** 審查者檢查 Algorithm 1 中停損、停利與勝率的來源
- **THEN** 停損與停利由風控步驟計算，勝率由 ML 步驟產生，LLM 步驟只輸出情境判斷與理由

### Requirement: No fabricated results
在實驗完成前，論文 MUST NOT 呈現任何實驗結果數值；評估章節 SHALL 只描述資料、基準、指標與實驗流程，並明確標示為計畫。

#### Scenario: Experimental section is a plan
- **WHEN** 審查者檢查 Experimental Plan 與 Conclusion
- **THEN** 沒有以結果語氣呈現的效能數字，且文中明確說明結果待實作後報告

### Requirement: Traceable citations
論文中的每一個引用 SHALL 對應到 `paper/references.bib` 中的一筆條目，且條目資訊與 `docs/proposal/references.md` 已查證的文獻一致。

#### Scenario: Citation resolution
- **WHEN** 編譯論文
- **THEN** 所有 `\cite` 皆可解析，參考文獻列表中沒有未被引用的條目

### Requirement: Overleaf synchronization via MCP
專案 SHALL 提供將論文同步到 Overleaf，並透過 MCP 讓 AI 助手讀寫 Overleaf 專案的操作說明，且說明中 MUST NOT 包含任何真實的存取權杖。

#### Scenario: Setup guide without secrets
- **WHEN** 審查者閱讀 `paper/OVERLEAF_MCP.md`
- **THEN** 文件說明安裝、設定與驗證步驟，且權杖欄位只使用佔位字串
