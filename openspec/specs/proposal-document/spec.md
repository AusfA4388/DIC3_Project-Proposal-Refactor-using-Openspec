# proposal-document Specification

## Purpose
規範 Hybrid TPA-Agent 專題提案文件的結構與品質，確保摘要、緒論與相關研究符合期末專題規範與 A2Z SOP，且所有證據可被查核。

## Requirements

### Requirement: Abstract follows A–F structure
提案摘要 SHALL 依序包含 Attention Getter、But、Cure、Development、Experiments、Findings 六個段落，且每一段落都能在文件中被明確辨識。

#### Scenario: Reviewer checks abstract structure
- **WHEN** 審查者閱讀 `docs/proposal/00-core-definition.md` 的 Part 1
- **THEN** 能找到 A 到 F 六個標示清楚的段落，且順序正確

### Requirement: Attention Getter cites recent evidence
Attention Getter 與 Introduction 的 General 段落 SHALL 至少引用一項 2025–2026 年的統計資料或研究，而不只使用「近年來 AI 快速發展」等泛稱。

#### Scenario: Evidence is dated and cited
- **WHEN** 審查者檢查 A 段與 1.1 段的引用
- **THEN** 至少一個引用編號指向 references.md 中年份為 2025 或 2026 的條目

### Requirement: Findings state expected outcomes only
在實驗完成前，Findings 段落 MUST 只陳述預期成果，不得出現任何虛構的實驗數值。

#### Scenario: No fabricated results
- **WHEN** 審查者檢查 F 段
- **THEN** 段落中沒有以實驗結果語氣呈現的效能數字，並明確標示為 Expected Outcomes

### Requirement: Introduction follows A2Z G–L
Introduction SHALL 依序包含 General、However、In literature、Judgement、Keypoint、List organization 六個小節。

#### Scenario: Reviewer checks introduction structure
- **WHEN** 審查者閱讀 `docs/proposal/01-introduction.md`
- **THEN** 能找到 1.1 至 1.6 六個小節，分別對應 G、H、I、J、K、L

### Requirement: Contributions use prospective wording
Keypoint 小節列出的核心貢獻 MUST 使用預期語氣，不得以「成功」、「已證明」等完成式描述尚未實作的工作，且每項貢獻 SHALL 對應至少一個 Core。

#### Scenario: Contribution wording check
- **WHEN** 審查者檢查 1.5 小節的貢獻列表
- **THEN** 每項貢獻都標示對應的 Core 編號，且不含完成式宣稱

### Requirement: Related work balances AI and domain knowledge
Related Work SHALL 同時涵蓋 AI 技術與領域知識，兩者各至少兩個小節。

#### Scenario: Section balance check
- **WHEN** 審查者計算 `docs/proposal/02-related-work.md` 的小節類型
- **THEN** 標示為 Domain 的小節與標示為 AI 的小節各至少兩個

### Requirement: Article summary table uses required columns
Related Work SHALL 包含一張 Article Summary Table，欄位為 Ref.、Year、Problem、AI Method、Domain Knowledge、Dataset、Findings、Limitation，且至少收錄 8 篇文獻，其中至少 5 篇為 2025–2026 年。

#### Scenario: Table completeness check
- **WHEN** 審查者檢查 2.7 小節的表格
- **THEN** 表格欄位與規範一致，列數至少 8，且至少 5 列的 Year 為 2025 或 2026

### Requirement: Research gap follows four-step synthesis
Related Work SHALL 以 Existing Research、Limitations、Research Gap、Our Project 四個步驟歸納研究缺口，且每個步驟都引用對應文獻或對應 Core。

#### Scenario: Gap synthesis check
- **WHEN** 審查者閱讀 2.8 小節
- **THEN** 四個步驟依序出現，且 Our Project 步驟對應到 C1 至 C5

### Requirement: References are verifiable
每一則參考文獻 SHALL 提供足以查找原文的資訊（作者、標題、年份，以及期刊卷期、DOI、arXiv 編號或網址之一），且預印本 MUST 標示為 preprint。

#### Scenario: Reference lookup
- **WHEN** 審查者隨機抽查 references.md 中的一則條目
- **THEN** 能依條目資訊找到原文，且 arXiv 條目標示為 preprint
