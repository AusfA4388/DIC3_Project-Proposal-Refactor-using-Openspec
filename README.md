# Hybrid TPA-Agent

**Hybrid Technical & Price Action Agent**：結合確定性供需區演算法、機器學習勝率預測與 LLM 推理之短線交易智慧代理人系統

> 國立中興大學 物聯網數據分析與應用 · 期末專題
> DIC3：Project Proposal Refactor using OpenSpec
> 作者：侯佳旻（7114056115）｜小組成員：陳柏安、陳威碩、陳沐德、古富綿
> 狀態：Proposal 階段（尚未實作）
> AI 使用聲明：本次重構使用 Claude（Anthropic）協助文獻搜尋、文件撰寫與 OpenSpec 規格轉換；所有文獻已逐一查核出處，內容經本人檢視。

---

## DIC3 作業對照

| # | 作業要求 | 完成內容 | 位置 |
|---|---|---|---|
| 1 | 安裝 OpenSpec，熟悉 spec-driven development | 以 OpenSpec v2.0.0 初始化；完整走過 propose → apply → archive 一次 | [`openspec/`](openspec/) |
| 2 | 釐清專題 A–F、5 Cores、3 Trade-offs、10 Details | 摘要 A–F（含 300 字版本）、五個核心能力、三個設計取捨、十個設計細節 | [`docs/proposal/00-core-definition.md`](docs/proposal/00-core-definition.md) |
| 3 | 將 design.md 轉為 OpenSpec workflow | 四層八模組轉為 8 個 capability 規格（含 scenario）、design.md、27 項實作任務 | [`openspec/changes/add-hybrid-tpa-agent-core/`](openspec/changes/add-hybrid-tpa-agent-core/) |
| 4 | Introduction 重構 | 依 A2Z G–L 重寫，補上數據與引用 | [`docs/proposal/01-introduction.md`](docs/proposal/01-introduction.md) |
| 5 | Related Work 重構 | Domain 3 節 + AI 3 節、Article Summary Table（10 篇）、研究缺口四段式歸納 | [`docs/proposal/02-related-work.md`](docs/proposal/02-related-work.md) |
| — | 參考文獻 | 18 篇，已逐一查核 | [`docs/proposal/references.md`](docs/proposal/references.md) |

## 核心概念

> 演算法負責精確，機器學習負責機率，LLM 負責情境，風控負責說不，人負責按下確認。

| Core | 說明 |
|---|---|
| C1 確定性空間結構 | 以可重現的演算法標出供需區 |
| C2 機器學習機率估計 | XGBoost 預測反彈或突破勝率 W |
| C3 LLM 情境推理（與數值解耦） | LLM 只吃結構化 JSON，不產生價格與機率 |
| C4 風險優先決策 | W ≥ 0.55 且 RR ≥ 2.0 才出手 |
| C5 人在迴路與安全降級 | 只出建議報告，不自動下單 |

## Repo 結構

```text
.
├── README.md                      ← 本檔
├── DESIGN.md                      ← 系統設計入口（指向 openspec/）
├── docs/
│   ├── proposal/                  ← DIC3 重構後的提案內容
│   │   ├── 00-core-definition.md  ← A–F、5 Cores、3 Trade-offs、10 Details
│   │   ├── 01-introduction.md     ← Introduction（A2Z G–L）
│   │   ├── 02-related-work.md     ← Related Work（A2Z M、O）
│   │   └── references.md          ← 參考文獻（IEEE）
│   └── original/                  ← 原始期中 Proposal（Word、PDF、簡報、圖）
├── openspec/
│   ├── config.yaml                ← 專案脈絡與規則
│   ├── specs/
│   │   └── proposal-document/     ← 已歸檔的提案文件規格
│   └── changes/
│       ├── add-hybrid-tpa-agent-core/   ← 進行中：系統規格（8 capabilities）
│       └── archive/
│           └── 2026-11-12-refactor-proposal-docs/  ← 已完成：本次文件重構
└── .agents/skills/                ← OpenSpec 產生的 AI 助手指令
```

## OpenSpec 工作流程

本專題的每一項變更都依以下流程進行：

```text
propose（寫 proposal / specs / design / tasks）
   → validate（openspec validate --strict）
   → apply（依 tasks.md 實作並勾選）
   → archive（規格合併到 openspec/specs/，變更移到 archive/）
```

| Change | 狀態 | 說明 |
|---|---|---|
| `refactor-proposal-docs` | ✅ 已歸檔 | DIC3 文件重構；產生 `proposal-document` 規格 |
| `add-hybrid-tpa-agent-core` | 🔄 進行中（0/27） | 系統八模組規格，期末實作依此進行 |

常用指令：

```bash
npm install -g @fission-ai/openspec     # 安裝
openspec list                           # 列出進行中的變更
openspec list --specs                   # 列出正式規格
openspec show add-hybrid-tpa-agent-core # 查看變更內容
openspec validate --all --strict        # 驗證所有規格
openspec view                           # 互動式儀表板
```

## 下一步

1. 小組討論 `design.md` 中「待小組決議事項」Q1–Q7（原 Pseudocode 與架構的不一致）。
2. 決定市場、標的、時間框架與回測期間。
3. 依 `tasks.md` 開始實作。
