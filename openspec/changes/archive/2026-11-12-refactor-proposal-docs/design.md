# Design

## Context

原始材料為小組的期中 Proposal（Word、PDF、15 頁簡報，見 `docs/original/`）。重構範圍與動機見 proposal.md。老師提供的參考框架為《期末專題提案作業規範》與《A2Z outline example》。

## Goals / Non-Goals

**Goals:**
- 讓 Abstract、Introduction、Related Work 的結構可以逐項對應到規範與 A2Z SOP。
- 讓每一個事實性陳述都有可查核的出處。
- 產出 5 Cores、3 Trade-offs、10 Details，作為系統規格（`add-hybrid-tpa-agent-core`）的共同語言。

**Non-Goals:**
- 不重寫 Deep Research（Q1–Q3）；原內容品質足夠，僅在核心定義中引用。
- 不修改 Pseudocode、Flowchart、架構圖。
- 不產出新的 Word 檔或簡報；由小組依本次內容自行更新。

## Decisions

### D1. 以 Markdown 作為文件的單一事實來源
- **選擇**：在 `docs/proposal/` 以 Markdown 撰寫，Word 與簡報從此同步。
- **理由**：Markdown 可被 Git 追蹤差異，且能與 OpenSpec 規格互相連結。
- **替代方案**：直接修改 Word 檔。缺點是 Git 無法顯示 Word 的內容差異，多人協作時不易追蹤。

### D2. 先寫 Related Work，再寫 Introduction
- **選擇**：先完成文獻查證與 Related Work，再寫 Introduction。
- **理由**：Introduction 的 In literature 與 Judgement 段落必須引用 Related Work 已查證的文獻，順序相反容易出現無出處的陳述。

### D3. 以「證據強度」選擇文獻
- **選擇**：Domain 證據優先採用期刊論文、專書與引述證交所數據的報導（[1]–[6]）；AI 技術優先採用 2025–2026 年的研究，並特別納入 LLM 回測偏誤研究（[15]–[18]）。
- **理由**：口試最可能被質疑的是「LLM 回測績效是否可信」，提前在 Related Work 回應比事後補救更有說服力。
- **替代方案**：只引用支持本系統的研究。缺點是無法回應審查者對 LLM 交易可信度的質疑。

### D4. 新聞數據的使用方式
- **選擇**：台股當沖統計引用新聞 [1]、[2]，但只採用其中引述證交所的數字；[1] 的「全年虧損 272 億元」為報導自行估算，因此不放入正文。
- **理由**：避免把媒體估算當成官方統計。

## Risks / Trade-offs

- [arXiv 預印本尚未經同儕審查] → 在 references.md 標示 preprint，關鍵論點同時引用期刊論文（[3]、[5]、[7]、[9]）。
- [新聞數據可能被修正] → 正式繳交前可改以證交所年報或統計月報的原始數字取代 [1]、[2]。
- [重構內容與 Word、簡報不同步] → tasks.md 保留同步項目作為後續工作。
