# ARS-agy 安裝與設定指南

適用於 Google Antigravity 平台的 **Academic Research Skills for Antigravity (ARS-agy)** 安裝與環境設定說明。

---

## 最小可行設定

1. 確保已安裝並啟動 Google Antigravity。
2. 將本專案複製（clone）至研究專案工作區（或建立符號連結至全域技能目錄）。
3. 在 Antigravity 對話框中提出你的學術研究需求。

核心提示詞驅動技能（deep-research、academic-paper、academic-paper-reviewer、academic-pipeline）無需專有商業 API Key 或額外 Python 相依即可完整運作。

---

## 在 Antigravity 中的安裝方式

Antigravity 會自動探索 `<workspaceRoot>/skills/<skill-name>/SKILL.md` 或使用者全域目錄 `~/.gemini/antigravity/skills/<skill-name>/SKILL.md` 下的技能。

### 方法一：專案工作區模式（推薦用於獨立研究專案）

適合個別論文、畢業設計或研究團隊專案：

```bash
# 進入你的研究工作區目錄：
cd /path/to/your/research-workspace
mkdir -p skills
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git skills/academic-research-skills-agy
```

因 `skills/academic-research-skills-agy/skills/` 內包含 4 個核心技能的軟連結，Antigravity 會自動載入：
- `deep-research`
- `academic-paper`
- `academic-paper-reviewer`
- `academic-pipeline`

### 方法二：全域技能模式（所有工作區通用）

將技能安裝至使用者目錄，使所有 Antigravity 對話皆可隨時呼叫學術技能：

```bash
# 複製至本地存放路徑：
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/skills/academic-research-skills-agy

# 建立符號連結至 Antigravity 全域技能目錄：
mkdir -p ~/.gemini/antigravity/skills
ln -s ~/skills/academic-research-skills-agy/deep-research ~/.gemini/antigravity/skills/deep-research
ln -s ~/skills/academic-research-skills-agy/academic-paper ~/.gemini/antigravity/skills/academic-paper
ln -s ~/skills/academic-research-skills-agy/academic-paper-reviewer ~/.gemini/antigravity/skills/academic-paper-reviewer
ln -s ~/skills/academic-research-skills-agy/academic-pipeline ~/.gemini/antigravity/skills/academic-pipeline
```

---

## 透過 `GEMINI.md` 設定常設偏好

Antigravity 在工作階段啟動時會自動載入工作區根目錄下的 `GEMINI.md`。你可以在其中設定學術偏好：

```markdown
## ARS 常設偏好設定

- 引用格式：優先採用 APA 7th（或期刊要求之格式）。
- 文獻搜尋：預設排除未同儕審查的預印本，優先檢索領域核心期刊。
- 語言規範：生成中英雙語摘要，符合正式學術規範。
- 開放取用：優先引用具有 Open Access 版本的文獻，並附帶 DOI / OpenAlex 連結。
```

---

### 跨模型驗證設定（選用）

```bash
# 選擇跨模型驗證模型：
export ARS_CROSS_MODEL="gpt-5.5"
# or: export ARS_CROSS_MODEL="gemini-3.1-pro-preview"
# or: export ARS_CROSS_MODEL="gpt-5.6-sol"
```

---

### 1. 學術檢索技能（無外部金鑰）
- **`literature-search-openalex`**：檢索 OpenAlex 全球學術圖譜、解析 DOI 與詮釋資料。
- **`literature-search-arxiv`**：快速檢索與分析電腦科學、物理、數學領域之 arXiv 論文。

### 2. 文件匯出與排版工具（選用）
- **Pandoc**（匯出為 `.docx`）：
  ```bash
  # macOS
  brew install pandoc
  ```
- **TeX Live / Tectonic**（本地編譯 LaTeX 產出 PDF）：
  ```bash
  # macOS
  brew install tectonic
  ```
  若未安裝 TeX 環境，系統將預設輸出可在 Overleaf 線上編譯的完整原始碼包。

### 3. 跨模型驗證設定（選用）

```bash
# 選擇跨模型驗證目標：
export ARS_CROSS_MODEL="gpt-5.5"
# 或：export ARS_CROSS_MODEL="gemini-3.1-pro-preview"
# 或：export ARS_CROSS_MODEL="gpt-5.6-sol"
# 或使用訂閱傳輸：export ARS_CROSS_MODEL_TRANSPORT="codex"
```

---

## 驗證安裝

在 Antigravity 對話框中輸入：
`幫我規劃論文寫作大綱` 或 `Help me plan my research paper`。
若 Antigravity 成功啟用 `academic-paper` 並以結構化引導回應，即表示設定成功。
