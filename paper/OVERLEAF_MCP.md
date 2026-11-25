# Overleaf + MCP 設定說明

本專題的論文原始檔放在 GitHub（`paper/`），在 Overleaf 上撰寫與排版，並透過 **Overleaf MCP** 讓 Claude Desktop 直接讀寫 Overleaf 專案。

```text
GitHub repo (paper/)  ──上傳──▶  Overleaf 專案  ◀──MCP (Git integration)──  Claude Desktop
        ▲                                                                       │
        └────────────────────── 定期同步回 GitHub ◀──────────────────────────────┘
```

> ⚠️ Git token 等於 Overleaf 專案的寫入密碼。**不要**把 token 提交到 GitHub，也不要貼到任何聊天對話中。

---

## 1. 在 Overleaf 建立專案

1. 下載本 repo 的 `paper/` 資料夾，壓縮成 zip（需包含 `main.tex` 與 `references.bib`）
2. Overleaf → **New Project → Upload Project**，選擇該 zip
3. 按 **Recompile**，確認 PDF 與 repo 中的 `paper/main.pdf` 一致
4. 從網址記下 **Project ID**：`https://www.overleaf.com/project/<PROJECT_ID>`

## 2. 產生 Git token

Overleaf → **Account Settings → Git integration → Generate token**，複製後存放在安全位置（只會顯示一次）。

## 3. 在 Claude Desktop 設定 Overleaf MCP

前置需求：Claude Desktop、Node.js 18 以上（`node -v` 確認）。

使用的 MCP 伺服器：[`@mjyoo2/overleaf-mcp`](https://github.com/mjyoo2/OverleafMCP)

設定檔位置：
- Windows：`%APPDATA%\Claude\claude_desktop_config.json`
- macOS：`~/Library/Application Support/Claude/claude_desktop_config.json`

**Windows**（需要 `cmd /c` 才能找到 `npx`）：

```json
{
  "mcpServers": {
    "overleaf": {
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@mjyoo2/overleaf-mcp"],
      "env": {
        "OVERLEAF_PROJECT_ID": "<YOUR_OVERLEAF_PROJECT_ID>",
        "OVERLEAF_GIT_TOKEN_FILE": "C:\\Users\\<you>\\overleaf-token.txt"
      }
    }
  }
}
```

**macOS**：

```json
{
  "mcpServers": {
    "overleaf": {
      "command": "npx",
      "args": ["-y", "@mjyoo2/overleaf-mcp"],
      "env": {
        "OVERLEAF_PROJECT_ID": "<YOUR_OVERLEAF_PROJECT_ID>",
        "OVERLEAF_GIT_TOKEN_FILE": "/Users/<you>/overleaf-token.txt"
      }
    }
  }
}
```

建議使用 `OVERLEAF_GIT_TOKEN_FILE`，把 token 存在一個只有自己能讀的文字檔，而不是直接寫在設定檔裡。設定檔若已有其他 `mcpServers`，把 `"overleaf": {...}` 加進去即可。

儲存後**完全關閉並重新開啟** Claude Desktop。

## 4. 驗證連線

在 Claude Desktop 新對話中輸入：

> 用 Overleaf MCP 執行 status_summary，再列出 main.tex 的所有章節

能回傳專案狀態與章節列表（I. Introduction … VI. Conclusion）即表示成功。

## 5. 可用的 MCP 工具

| 工具 | 用途 |
|---|---|
| `list_files` | 列出專案檔案 |
| `read_file` | 讀取檔案 |
| `get_sections` | 列出 LaTeX 章節 |
| `get_section_content` | 讀取某一章節 |
| `write_section` | 改寫某一章節（`newContent` 需包含章節標題） |
| `write_file` | 改寫整個檔案 |
| `status_summary` | 專案狀態摘要 |

寫入工具都需要 `commitMessage`，每次修改都會在 Overleaf 的歷史紀錄留下一筆。

## 6. 建議的寫作流程

1. 在 Claude Desktop 請 Claude 用 `get_section_content` 讀取某一節，提出修改
2. 確認後以 `write_section` 寫回 Overleaf
3. 在 Overleaf 按 Recompile 檢查 PDF
4. 告一段落時，用 `read_file` 取得最新的 `main.tex`，更新到 GitHub 的 `paper/`

## 疑難排解

| 狀況 | 處理方式 |
|---|---|
| Claude Desktop 看不到 overleaf 工具 | 檢查 JSON 格式（逗號、引號），並完全重啟 Claude Desktop |
| `npx` not found | 安裝 Node.js 18 以上；Windows 需使用 `cmd /c` 寫法 |
| Authentication failed | 重新產生 token，確認 token 檔案內容沒有多餘空白或換行 |
| 找不到專案 | 確認 Project ID 是網址 `/project/` 後面那串 |
