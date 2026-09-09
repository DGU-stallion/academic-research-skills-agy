# Academic Research Skills for Antigravity (ARS-agy)

[![Version](https://img.shields.io/badge/version-v3.21.1-blue)](https://github.com/DGU-stallion/academic-research-skills-agy)
[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Platform: Antigravity](https://img.shields.io/badge/Platform-Google%20Antigravity-4285F4.svg)](https://github.com/DGU-stallion/academic-research-skills-agy)
[![Upstream: v3.21.1](https://img.shields.io/badge/Upstream-v3.21.1-blue.svg)](https://github.com/Imbad0202/academic-research-skills)

[简体中文](README.zh-CN.md) | [English](README.md) | [繁體中文](README.zh-TW.md)

**ARS-agy** 是专为 **Google Antigravity** 平台打造的原生学术研究、论文写作与同行评审全流程协作框架（原生支持 Antigravity Plugin 插件规范）。

本项目基于优秀开源项目 [Imbad0202/academic-research-skills](https://github.com/Imbad0202/academic-research-skills)（v3.21.1）进行适配重构，遵循 [CC BY-NC 4.0（署名-非商业性使用 4.0 国际）](https://creativecommons.org/licenses/by-nc/4.0/) 授权协议。关于原项目的历史演进、通用学术方法论、详细更新记录及完整贡献者名单，欢迎直接访问上游仓库查阅。

---

## 核心理念与副驾驶定位

> **AI 是研究者的副驾驶，不是机长。**  
> 本工具旨在协助学者处理繁重的机械性与结构性任务：系统性文献扫描、论据链条对齐、图表数据一致性交叉核验、排版规范适配及模拟同行盲审。而研究问题的核心价值、实验设计的主体方向、数据意义的独到解读以及最终学术结论的责任，始终掌握在学者手中。

- **学术诚信与防幻觉底线**：严禁虚构参考文献，每条引用必须具备可验证的学术标识（DOI、ArXiv ID、PMID 等），并在引文与正文主张之间建立精准支撑（Claim-faithfulness）。系统严格拦截学术界关注的 7 类 AI 研究缺陷模式（M1~M7，详见 Lu et al., 2026）。
- **去机器感与学术规范**：不采用模糊语义的套话堆砌，而是依据规范的学术文体标准（如 APA 7.0、IEEE、GB/T 7714 等）进行篇章逻辑推导与风格校准。

---

## Antigravity (AGY) 适配特点

针对 Google Antigravity 的智能体编排与交互生态，ARS-agy 深度融合了以下原生能力：

### 1. 原生 Antigravity 插件架构（Native Plugin Ecosystem）
- 完全契合 Antigravity 插件规范（含 `plugin.json` 清单、`rules/AGENTS.md` 规则与 `skills/` 四大技能包），支持在 Antigravity 的插件面板中统一启用、停用与配置。
- 自动注册完整的学术规则体系，各模式（研究、写作、审稿、流水线）协同运作且互不干扰。

### 2. 独立子代理同行并发盲审（Parallel Subagents Delegation）
利用 Antigravity 的 `invoke_subagent` 机制，在同行评审阶段**单次并发派发**相互隔离的 5 视角独立审稿子代理团队：
- **期刊匹配审稿人（Journal-Fit Reviewer）**：评估论文定位与目标期刊范围的契合度；
- **方法论审稿人（Methodology Reviewer）**：针对实验效度、统计学严密性及数据边界进行独立评估；
- **领域审稿人（Domain Reviewer）**：审视领域理论深度与先验文献覆盖完整性；
- **跨学科审稿人（Perspective Reviewer）**：审视研究的普适意义与跨学科价值；
- **魔鬼代言人（Devil's Advocate Reviewer）**：在完全隔离的独立子代理环境中运行，被赋予极具对抗性的挑刺指令，全力寻找逻辑断层与反面证据。

> 💡 **并发提速与反阿谀奉承**：5 位审稿子代理在物理隔离的上下文空间中并行生成评审报告，**整体审稿耗时缩短 60% 以上**，彻底杜绝单模型长会话中的阿谀奉承效应（Anti-Sycophancy）。

### 3. 交互式检查点决策卡片（Interactive Checkpoints via `ask_question`）
在学术全流程的关键节点，系统调用 Antigravity 原生的 `ask_question` 渲染交互选择卡片，阻塞式等待人类学者决断：
- **选题与蓝图确认**：确认研究问题（RQ Brief）与方法论方案；
- **论文提纲审查**：确认论据映射表（Claim-Evidence Matrix）与章节结构；
- **审稿决议处理**：展示盲审综合意见，由学者选择大修策略、逐条答辩或方向调整；
- **诚信闸门放行**：展示 7 类学术诚信检测报告并由作者签署确认；
- **终稿排版导出**：选择最终交付格式（LaTeX、Markdown、DOCX、PDF）。

### 4. 富媒体、Generative UI 与学术排版规范（Artifacts, KaTeX & UI Widgets）
- **学术成果持久化**：阶段性产物（综述报告、研究大纲、答辩对照表等）自动沉淀为右侧独立展示的 Artifacts 成果文档；
- **Generative UI 交互仪表盘**：除标准 Markdown 报告外，支持渲染交互式 HTML 仪表盘（5 视角综合雷达评分板、可按严重度折叠的审稿意见卡片、可交互勾选的修订清单，以及 PRISMA 动态文献筛选漏斗）；
- **数学与因果公式**：统一采用 KaTeX 渲染（行内 `$ ... $` 与独立块 `$$ ... $$`）；
- **系统性综述可视化**：PRISMA 文献筛选流程统一采用原生 Mermaid 流程图呈现；
- **学术风险提示**：潜在方法论漏洞与证据短板使用 GitHub 标准警示框（`> [!WARNING]` / `> [!IMPORTANT]`）显式高亮。

### 5. 科学学术检索工具智能联动（Scientific Tools Auto-Discovery）
在文献调研与引文核验环节，系统会自动嗅探 Antigravity 当前环境中已加载的专业学术插件并优先分流：
- **全球综合文献与 DOI 真实性**：优先调度 `literature-search-openalex`；
- **计算机与理工前沿预印本**：优先调度 `literature-search-arxiv`；
- **生物医药与临床实证研究**：优先调度 `pubmed-database` 或 `literature-search-europepmc`；
- 仅在缺乏专业学术工具时优雅回退至通用网页搜索，从源头确保学术引文的真实可考。

### 6. 深度中文学术支持与自然语言交互
- **自然语言直接唤醒**：全面支持简体中文与繁体中文意图识别，无需记忆复杂参数，直接用自然学术语言表达需求（如“帮我梳理关于……的文献”、“模拟同行评审”、“写中英双语摘要”）；
- **规范中文学术排版**：内置思源宋体（Source Han Serif SC/TC）版式方案与 GB/T 7714 参考文献样式支持。

---

## 快速安装与配置指南

在 Google Antigravity 中使用 ARS-agy 提供三种部署方式，首选原生插件安装：

### 方式一：Antigravity 原生插件安装（推荐，最优雅完整）

Antigravity 原生支持将规则、技能、配置一体化打包为插件进行统一管理：

#### 1. 全局插件安装（推荐，对所有会话生效）
直接将本仓库作为插件克隆至 Antigravity 的全局插件目录：

```bash
# 创建全局插件目录并克隆本插件
mkdir -p ~/.gemini/config/plugins
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/.gemini/config/plugins/academic-research-skills-agy
```

#### 2. 工作区插件安装（适合团队协同与特定科研项目）
在具体科研项目的根目录下作为工作区专属插件安装：

```bash
# 进入你的科研项目目录
cd /path/to/your/research-project

# 克隆至项目插件目录
mkdir -p .agents/plugins
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git .agents/plugins/academic-research-skills-agy
```

> **插件生效说明**：安装后，Antigravity 会自动识别 `plugin.json` 清单，加载 `rules/AGENTS.md` 规则，并同时暴露 `skills/` 下的四大技能。可在 Antigravity 设置的“插件（Plugins）”面板中随时查看、开启或停用。

---

### 方式二：项目工作区技能模式（轻量化引入）

若仅需将技能作为当前工作区的扩展能力：

```bash
cd /path/to/your/academic-project
mkdir -p skills
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git skills/academic-research-skills-agy
```
Antigravity 会自动发现工作区内所有 `skills/*/SKILL.md` 文件并载入能力。

---

### 方式三：全局技能模式（Symbolic Link）

若希望直接以技能形式挂载至用户全局技能目录：

```bash
# 1. 克隆本仓库至本地稳定路径
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/skills/academic-research-skills-agy

# 2. 软链接 4 个核心技能至 Antigravity 全局技能目录
mkdir -p ~/.gemini/antigravity/skills
ln -s ~/skills/academic-research-skills-agy/deep-research ~/.gemini/antigravity/skills/deep-research
ln -s ~/skills/academic-research-skills-agy/academic-paper ~/.gemini/antigravity/skills/academic-paper
ln -s ~/skills/academic-research-skills-agy/academic-paper-reviewer ~/.gemini/antigravity/skills/academic-paper-reviewer
ln -s ~/skills/academic-research-skills-agy/academic-pipeline ~/.gemini/antigravity/skills/academic-pipeline
```

---

### 验证安装与环境推荐

1. **验证插件/技能加载**：
   在 Antigravity 对话框中发送如下任意短语：
   - `帮我规划这篇论文的结构`
   - `做系统文献综述`
   - `/ars-plan`

   当 Antigravity 自动激活对应的 `academic-paper` 或 `deep-research` 技能并以苏格拉底式对话向你提问时，即说明安装成功。

2. **推荐学术检索配套工具**：
   为了获得最佳的真实文献检索体验，推荐在 Antigravity 中配合使用以下内置学术搜索技能（无需外部商业 API Key）：
   - `literature-search-openalex`：用于查询 OpenAlex 学术图谱、解析 DOI 与抓取元数据；
   - `literature-search-arxiv`：用于检索计算机科学、物理学等领域的最新 arXiv 预印本文献。

3. **可选外部排版工具**：
   - **Pandoc**：用于将论文导出为 `.docx` 格式；
   - **TeX Live / Tectonic**：用于在本地直接编译 LaTeX 生成 APA 7.0 规范的 PDF。若本地未安装 TeX 环境，系统将默认输出完整的 Overleaf 兼容源码包与 GitHub Flavored Markdown 供在线编译。

---

## 四大核心技能与模式总览

| 核心技能 (Skill) | 专注领域 | 常用触发场景（自然语言 / 别名） | 关键产出物 |
| :--- | :--- | :--- | :--- |
| **`academic-pipeline`** | **全流程调度与学术诚信双闸门** | “从零开始写论文”、“学术研究流水线”、“端到端完成论文”<br>`ars-full` | 完整研究论文包、材料护照（Material Passport）、两阶段盲审决策记录 |
| **`deep-research`** | **文献综述与选题启发** | “梳理关于...的文献”、“做系统文献综述”、“引导我想想选题”<br>`deep-research` / `socratic` / `ars-3w` | RQ Brief 蓝图、PRISMA 综述报告、三段式对比矩阵 |
| **`academic-paper`** | **论文撰写与论据对齐** | “帮我写论文大纲”、“写中英双语摘要”、“根据审稿意见修改论文”<br>`ars-plan` / `ars-outline` / `ars-abstract` / `ars-revision` | 逐章详细计划、Claim-Evidence 论据映射表、双语规范摘要、答辩对照表 |
| **`academic-paper-reviewer`** | **多视角独立同行盲审** | “评审这篇论文”、“以审稿人角度挑刺”、“模拟同行评审”<br>`ars-reviewer` | 5 视角独立审稿报告（含魔鬼代言人反驳意见）、Editorial Decision 决议 |

---

## 常用工作流示例

### 场景 1：苏格拉底式启发选题（Socratic Ideation）

```text
用户：“我想研究生成式 AI 在高等教育教学评估中的应用，但目前思路比较模糊，不知道如何切入研究问题。你能帮我理清思路吗？”
```
> **系统行为**：激活 `deep-research` (socratic 模式)，通过多轮具有启发性的问题与批判性反思，引导学者聚焦并明确研究问题（RQ）、理论框架与方法论假设。

---

### 场景 2：独立同行盲审与魔鬼代言人挑刺（Peer Review）

```text
用户：“这是我刚写完的论文初稿（附文档链接），请帮我进行一次严格的同行评审，重点看看方法论严密性和可能的逻辑漏洞。”
```
> **系统行为**：激活 `academic-paper-reviewer`，派生出方法论审稿人、领域审稿人与完全隔离的魔鬼代言人子代理；随后主代理通过交互卡片向用户呈现评审决议与修改建议清单。

---

### 场景 3：端到端论文研究流水线（Full Pipeline）

```text
用户：“我想系统性开展关于‘跨平台大模型代码生成一致性’的研究并撰写完整学术论文。”
```
> **系统行为**：激活 `academic-pipeline`，有序推进 10 个阶段：研究选题 → 论文初稿撰写 → Stage 2.5 诚信闸门 → 第一阶段同行盲审 → 针对性修改 → Stage 3' 复审 → Stage 4.5 终极诚信核验 → 排版导出。

---

## 学术诚信铁律（Iron Rules）

在全流程协作中，ARS-agy 严格遵守以下学术准则：

1. **真实引用原则**：绝不捏造任何作者、年份、期刊名称或 DOI。遇到检索不到的文献时，诚实报告检索边界，不强行填补。
2. **L3 Claim-faithfulness 保真度**：严禁断章取义，引用文献必须在语义上真正支撑其对应的主张。
3. **人类监督确认**：在选题确认、审稿决议接纳及最终文本定稿时，必须由人类学者主动确认，AI 不越权替学者做决定。

---

## 许可证与致谢

- **许可证**：本项目遵循 [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/) 协议发布。你可以自由分享和修改本项目，但仅限非商业性研究与个人用途，且须保留原作者及本项目的署名。
- **上游项目致谢**：诚挚感谢原项目作者 [Cheng-I Wu (@Imbad0202)](https://github.com/Imbad0202) 及其开源的 [academic-research-skills](https://github.com/Imbad0202/academic-research-skills)。原项目为学术全流程严谨协作奠定了扎实的方法论基石。

学术引用原项目请参考：
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
