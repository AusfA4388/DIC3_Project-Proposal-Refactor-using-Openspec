# Tasks

## 1. 論文原始檔

- [x] 1.1 建立 `paper/main.tex`（IEEEtran conference）；驗證：`latexmk -pdf main.tex` 成功產生 PDF
- [x] 1.2 將 DIC3 的 18 篇已查證文獻轉為 `paper/references.bib`；驗證：bibtex 無警告，所有 `\cite` 皆可解析
- [x] 1.3 撰寫 Abstract、Index Terms、Introduction（A2Z G–L 改寫為英文）；驗證：PDF 中可找到各段且貢獻使用預期語氣
- [x] 1.4 撰寫 Related Work 與 Table I 能力比較表；驗證：每個子節至少一個引用
- [x] 1.5 撰寫 Design Principles（C1–C5、式 (1)、T1–T3）；驗證：式 (1) 在 W=0.55、RR=2.0 時得 E=0.65
- [x] 1.6 以 TikZ 繪製架構圖並撰寫八個模組說明；驗證：圖中八個模組各對應一個 capability
- [x] 1.7 撰寫 Algorithm 1；驗證：停損停利、勝率與 LLM 的責任分工符合 `add-hybrid-tpa-agent-core` specs
- [x] 1.8 撰寫 Experimental Plan（Table II）與 Conclusion；驗證：文中沒有任何實驗結果數值
- [x] 1.9 檢查頁數與排版；驗證：PDF 不超過 6 頁，圖表不重疊

## 2. Overleaf 與 MCP

- [x] 2.1 撰寫 `paper/OVERLEAF_MCP.md`；驗證：文件只含佔位 token，步驟涵蓋安裝、設定與驗證
- [ ] 2.2 作者在 Overleaf 上傳 `paper/` 建立專案；驗證：Overleaf 編譯結果與本地 PDF 一致
- [ ] 2.3 作者在 Claude Desktop 設定 Overleaf MCP；驗證：`status_summary` 與 `get_sections` 回傳 main.tex 的章節列表
- [ ] 2.4 透過 MCP 完成至少一次讀寫（例如以 `write_section` 修改一個段落）；驗證：Overleaf 歷史紀錄出現對應 commit

## Workflow follow-up

- 小組確認 Algorithm 1 與 `add-hybrid-tpa-agent-core/design.md` 待決議事項 Q1–Q4 後，再決定是否 archive 本 change。
- Overleaf 上的後續修改需同步回 GitHub 的 `paper/`。
