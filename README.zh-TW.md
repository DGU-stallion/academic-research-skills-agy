# Academic Research Skills for Antigravity (ARS-agy)

[![Version](https://img.shields.io/badge/version-v3.21.1-blue)](https://github.com/DGU-stallion/academic-research-skills-agy)
[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Platform: Antigravity](https://img.shields.io/badge/Platform-Google%20Antigravity-4285F4.svg)](https://github.com/DGU-stallion/academic-research-skills-agy)
[![Upstream: v3.21.1](https://img.shields.io/badge/Upstream-v3.21.1-blue.svg)](https://github.com/Imbad0202/academic-research-skills)

[繁體中文](README.zh-TW.md) | [简体中文](README.zh-CN.md) | [English](README.md)

**ARS-agy** 是專為 **Google Antigravity** 平台打造的原生學術研究、論文寫作與同行評審全流程協作框架。

本專案基於優秀開源專案 [Imbad0202/academic-research-skills](https://github.com/Imbad0202/academic-research-skills)（v3.21.1）進行適配重構，遵循 [CC BY-NC 4.0（姓名標示-非商業性 4.0 國際）](https://creativecommons.org/licenses/by-nc/4.0/) 授權條款。關於原專案的歷史演進、通用學術方法論、詳細更新記錄及完整貢獻者名單，歡迎直接造訪上游儲存庫查閱。

---

## 核心理念與副駕駛定位

> **AI 是研究者的副駕駛，不是機長。**  
> 本工具旨在協助學者處理繁重的機械性與結構性任務：系統性文獻掃描、論據鏈條對齊、圖表數據一致性交叉核驗、排版規範適配及模擬同行盲審。而研究問題的核心價值、實驗設計的主體方向、數據意義的獨到解讀以及最終學術結論的責任，始終掌握在學者手中。

- **學術誠信與防幻覺底線**：嚴禁虛構參考文獻，每筆引用必須具備可驗證的學術識別碼（DOI、ArXiv ID、PMID 等），並在引文與正文主張之間建立精準支撐（Claim-faithfulness）。系統嚴格攔截學術界關注的 7 類 AI 研究缺陷模式（M1~M7，詳見 Lu et al., 2026）。
- **去機器感與學術規範**：不採用模糊語義的套話堆砌，而是依據規範的學術文體標準（如 APA 7.0、IEEE、GB/T 7714 等）進行篇章邏輯推導與風格校準。

---

## Antigravity (AGY) 適配特點

針對 Google Antigravity 的智慧體編排與互動生態，ARS-agy 深度融合了以下原生能力：

### 1. 獨立子代理同行盲審（Subagents Delegation）
利用 Antigravity 的 `invoke_subagent` 與 `define_subagent` 機制，在同行評審階段動態派生相互隔離的評審子代理團隊（Journal-Fit Reviewer + 3 位動態審查者 + 魔鬼代言人）：
- **期刊匹配審稿人（Journal-Fit Reviewer）**：評估論文定位與目標期刊範圍的契合度；
- **方法論審稿人（Methodology Reviewer）**：針對實驗效度、統計學嚴密性及數據邊界進行獨立評估；
- **領域審稿人（Domain Reviewer）**：審視領域理論深度與先驗文獻覆蓋完整性；
- **跨學科審稿人（Perspective Reviewer）**：審視研究的普適意義與跨學科價值；
- **魔鬼代言人（Devil's Advocate Reviewer）**：在完全隔離的子代理對話中運行，被賦予極具對抗性的挑刺指令，全力尋找邏輯斷層與反面證據。

在 full mode（Journal-Fit Reviewer + R1/R2/R3 + 魔鬼代言人）下執行完整審查流程，並嚴格確立第一輪審查面板 vs. 契約治理再審派送的分界。
各子代理獨立完成評審後，由主調度代理統一生成結構化的同行評審綜合意見書（Editorial Decision Letter），有效避免單對話自圓其說（Sycophancy）與阿諛效應。

### 2. 互動式檢查點決策卡片（Interactive Checkpoints via `ask_question`）
在學術全流程的關鍵節點，系統呼叫 Antigravity 原生的 `ask_question` 渲染互動選擇卡片，阻塞式等待人類學者決斷：
- **選題與藍圖確認**：確認研究問題（RQ Brief）與方法論方案；
- **論文提綱審查**：確認論據對齊表（Claim-Evidence Matrix）與章節結構；
- **審稿決議處理**：展示盲審綜合意見，由學者選擇大修策略、逐條答辯或方向調整；
- **誠信閘門放行**：展示 7 類學術誠信檢測報告並由作者簽署確認；
- **終稿排版匯出**：選擇最終交付格式（LaTeX、Markdown、DOCX、PDF）。

### 3. 富學術媒體呈現與排版規範（Artifacts & KaTeX）
- **學術成果持久化**：階段性產物（綜述報告、研究大綱、答辯對照表等）自動生成為規範的 Artifacts 文件；
- **數學與因果公式**：統一採用 KaTeX 渲染（行內 `$ ... $` 與獨立塊 `$$ ... $$`）；
- **系統性綜述視覺化**：PRISMA 文獻篩選流程統一採用原生 Mermaid 流程圖呈現；
- **學術風險提示**：潛在方法論漏洞與證據短板使用 GitHub 標準警示框（`> [!WARNING]` / `> [!IMPORTANT]`）顯式高亮。

### 4. 深度中文學術支援與自然語言互動
- **自然語言直接喚醒**：全面支援繁體中文與簡體中文意圖識別，無需記憶複雜參數，直接用自然學術語言表達需求（如「幫我梳理關於……的文獻」、「模擬同行評審」、「寫中英雙語摘要」）；
- **規範中文學術排版**：內建思源宋體（Source Han Serif TC/SC）版式方案與引用規範支援。

---

## 快速安裝與配置指南

在 Google Antigravity 中使用 ARS-agy 非常簡便，支援以下兩種部署方式：

### 方式一：工作區模式（推薦用於獨立科研專案）

將 ARS-agy 作為科研專案的技能擴展：

```bash
# 進入你的研究專案目錄
cd /path/to/your/academic-project

# 建立 skills 目錄並複製本儲存庫
mkdir -p skills
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git skills/academic-research-skills-agy
```

> **提示**：Antigravity 會自動發現工作區內所有 `skills/*/SKILL.md` 文件並載入其定義的能力。複製後重啟或重新整理當前 Antigravity 工作階段即可直接使用。

---

### 方式二：全域技能模式（所有工作區通用）

若希望在 Antigravity 的任何專案中均可隨時呼叫學術研究能力，可將技能掛載至使用者級全域目錄：

```bash
# 1. 複製本儲存庫至本地穩定路徑（例如 ~/.local/share/ 或 ~/skills/）
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/skills/academic-research-skills-agy

# 2. 建立符號連結將 4 個核心技能鏈接至 Antigravity 全域技能目錄
mkdir -p ~/.gemini/antigravity/skills
ln -s ~/skills/academic-research-skills-agy/deep-research ~/.gemini/antigravity/skills/deep-research
ln -s ~/skills/academic-research-skills-agy/academic-paper ~/.gemini/antigravity/skills/academic-paper
ln -s ~/skills/academic-research-skills-agy/academic-paper-reviewer ~/.gemini/antigravity/skills/academic-paper-reviewer
ln -s ~/skills/academic-research-skills-agy/academic-pipeline ~/.gemini/antigravity/skills/academic-pipeline
```

---

### 驗證安裝與環境推薦

1. **驗證技能載入**：
   在 Antigravity 對話框中發送如下任意短語：
   - `幫我規劃這篇論文的結構`
   - `做系統文獻綜述`
   - `/ars-plan`

   當 Antigravity 自動啟動對應的 `academic-paper` 或 `deep-research` 技能並以蘇格拉底式對話向你提問時，即說明安裝成功。

2. **推薦學術檢索配套工具**：
   為了獲得最佳的真實文獻檢索體驗，推薦在 Antigravity 中配合使用以下內建學術搜尋技能（無需外部商業 API Key）：
   - `literature-search-openalex`：用於查詢 OpenAlex 學術圖譜、解析 DOI 與抓取元數據；
   - `literature-search-arxiv`：用於檢索電腦科學、物理學等領域的最新 arXiv 預印本文獻。

3. **可選外部排版工具**：
   - **Pandoc**：用於將論文匯出為 `.docx` 格式；
   - **TeX Live / Tectonic**：用於在本地直接編譯 LaTeX 生成 APA 7.0 規範的 PDF。若本地未安裝 TeX 環境，系統將預設輸出完整的 Overleaf 相容原始碼包與 GitHub Flavored Markdown 供線上編譯。

---

## 四大核心技能與模式總覽

| 核心技能 (Skill) | 專注領域 | 常用觸發場景（自然語言 / 別名） | 關鍵產出物 |
| :--- | :--- | :--- | :--- |
| **`academic-pipeline`** | **全流程調度與學術誠信雙閘門** | 「從零開始寫論文」、「學術研究流水線」、「端到端完成論文」<br>`ars-full` | 完整研究論文包、材料護照（Material Passport）、兩階段盲審決策記錄 |
| **`deep-research`** | **文獻綜述與選題啟發** | 「梳理關於...的文獻」、「做系統文獻綜述」、「引導我想想選題」<br>`deep-research` / `socratic` / `ars-3w` | RQ Brief 藍圖、PRISMA 綜述報告、三段式對比矩陣 |
| **`academic-paper`** | **論文撰寫與論據對齊** | 「幫我寫論文大綱」、「寫中英雙語摘要」、「根據審稿意見修改論文」<br>`ars-plan` / `ars-outline` / `ars-abstract` / `ars-revision` | 逐章詳細計劃、Claim-Evidence 論據對齊表、雙語規範摘要、答辯對照表 |
| **`academic-paper-reviewer`** | **多視角獨立同行盲審** | 「評審這篇論文」、「以審稿人角度挑刺」、「模擬同行評審」<br>`ars-reviewer` | 5 視角獨立審稿報告（含魔鬼代言人反駁意見）、Editorial Decision 決議 |

---

## 常用工作流範例

### 場景 1：蘇格拉底式啟發選題（Socratic Ideation）

```text
使用者：「我想研究生成式 AI 在高等教育教學評估中的應用，但目前思路比較模糊，不知道如何切入研究問題。你能幫我釐清思路嗎？」
```
> **系統行為**：啟動 `deep-research` (socratic 模式)，透過多輪具有啟發性的問題與批判性反思，引導學者聚焦並明確研究問題（RQ）、理論框架與方法論假設。

---

### 場景 2：獨立同行盲審與魔鬼代言人挑刺（Peer Review）

```text
使用者：「這是我剛寫完的論文初稿（附文件連結），請幫我進行一次嚴格的同行評審，重點看看方法論嚴密性和可能的邏輯漏洞。」
```
> **系統行為**：啟動 `academic-paper-reviewer`，派生出方法論審稿人、領域審稿人與完全隔離的魔鬼代言人子代理；隨後主代理透過互動卡片向使用者呈現評審決議與修改建議清單。

---

### 場景 3：端到端論文研究流水線（Full Pipeline）

```text
使用者：「我想系統性開展關於『跨平台大模型程式碼生成一致性』的研究並撰寫完整學術論文。」
```
> **系統行為**：啟動 `academic-pipeline`，有序推進 10 個階段：研究選題 → 論文初稿撰寫 → Stage 2.5 誠信閘門 → 第一階段同行盲審 → 針對性修改 → Stage 3' 複審 → Stage 4.5 終極誠信核驗 → 排版匯出。

---

## 學術誠信鐵律（Iron Rules）

在全流程協作中，ARS-agy 嚴格遵守以下學術準則：

1. **真實引用原則**：絕不捏造任何作者、年份、期刊名稱或 DOI。遇到檢索不到的文獻時，誠實報告檢索邊界，不強行填補。
2. **L3 Claim-faithfulness 保真度**：嚴禁斷章取義，引用文獻必須在語義上真正支撐其對應的主張。
3. **人類監督確認**：在選題確認、審稿決議接納及最終文字定稿時，必須由人類學者主動確認，AI 不越權替學者做決定。

---

## 授權條款與致謝

- **授權條款**：本專案遵循 [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/) 條款發布。你可以自由分享和修改本專案，但僅限非商業性研究與個人用途，且須保留原作者及本專案的姓名標示。
- **上游專案致謝**：誠摯感謝原專案作者 [Cheng-I Wu (@Imbad0202)](https://github.com/Imbad0202) 及其開源的 [academic-research-skills](https://github.com/Imbad0202/academic-research-skills)。原專案為學術全流程嚴謹協作奠定了扎實的方法論基石。

學術引用原專案請參考：
```bibtex
@software{wu2026academic,
  author       = {Cheng-I Wu},
  title        = {Academic Research Skills: Open-Source AI Research Collaboration Framework},
  year         = {2026},
  publisher    = {Zenodo},
  version      = {v3.21.1},
  doi          = {10.5281/zenodo.20696614},
  url          = {https://github.com/Imbad0202/academic-research-skills}
}
```
