# Academic Research Skills for Antigravity (ARS-agy)

> **Antigravity (AGY) 原生学术研究、写作与同行评审全流程协作框架**  
> 基于 `Imbad0202/academic-research-skills` (v3.21.1) 核心内核，专为 Google Antigravity 平台的 Subagents、渐进式技能加载、Artifacts 与交互卡片体系深度重构。

---

## 核心架构与四大核心技能

ARS-agy 是一套面向学术全流程（从文献探索到完稿发表）的高水准研究协作者网络。它包含 4 个核心下游技能（位于 `skills/` 目录）：

```
[Antigravity Agent]
   │
   ├──▶ [skills/deep-research]              文献综述、PRISMA系统性回顾、苏格拉底引导演进
   ├──▶ [skills/academic-paper]             学术论文撰写、论据链构建、风格校准、去AI味
   ├──▶ [skills/academic-paper-reviewer]    5视角独立同行盲审团队（含魔鬼代言人反驳）
   └──▶ [skills/academic-pipeline]          10阶段全流程调度器与学术诚信双闸门
```

---

## 核心约束与学术诚信铁律（IRON RULES）

1. **真实性与防幻觉底线**：
   - 严禁虚构参考文献。每条引用必须提供可核实的标题、作者、年份及 DOI/PMID/ArXiv ID。
   - 引用文本必须真实支撑正文主张（L3 Claim-faithfulness），不得断章取义或把未验证的假说描述为既定结论。
   - 严格拦截 Lu et al. (2026) 提出的 7 类 AI 科研失败模式（M1~M7）：
     - **M1** 代码/实现缺陷通过审查（Implementation bug passing review）
     - **M2** 虚构引用（Hallucinated citations）
     - **M3** 虚构实验/实证结果（Hallucinated empirical results）
     - **M4** 走捷径/简单启发式代替深入分析（Shortcut reliance）
     - **M5** 将代码 Bug 包装为创新发现（Bug reframed as novel insight）
     - **M6** 虚构研究方法与步骤（Methodology fabrication）
     - **M7** 早期框架锁定与无视反面证据（Early frame-lock）
2. **副驾驶定位（Human-in-the-loop）**：
   - AI 是研究者的副驾驶，不是机长。AI 生成内容不得直接标记为 `executed` 或 `verified`。
   - 不得越权替作者做学术决策。在研究问题（RQ）、论点取舍、审稿决议（Accept/Major/Minor/Reject）等关键节点必须由人类通过交互卡片确认。
3. **搜索后给判断，不只列结果**：
   - 检索不是堆砌列表。必须给出综合研判（如：“该领域近3年集中于X，但在Y机制上存在明显空白，你的差异化切入点在于...”）。

---

## Antigravity (AGY) 专属执行协议

在 Antigravity 平台中运行 ARS-agy 时，遵循以下原生执行机制：

### 1. 独立子代理盲审（Subagents Delegation）
为彻底杜绝大模型在单一长会话中自我肯定、阿谀奉承（Sycophancy）的倾向，在运行 `academic-paper-reviewer` 或多视角审查时：
- **同行评审分流与单次并发派发 (Single-Call Parallel Dispatch)**：使用 `invoke_subagent` 在单次调用中通过 `Subagents` 数组同时并发派发 5 个完全独立的审稿子代理：
  - `@MethodologyReviewer`: 专注于研究方法、实验效度与统计严密性挑刺；
  - `@DomainReviewer`: 专注于领域实质正确性与先验文献完整性；
  - `@PerspectiveReviewer`: 专注于跨学科价值与更广泛的影响；
  - `@JournalFitReviewer`: 专注于目标期刊契合度与编辑部接受标准评估；
  - `@DevilsAdvocateReviewer`: **魔鬼代言人**，必须在完全隔离的子代理环境中运行，赋予其“全力寻找论证漏洞与反面论据”的强制指令；
- **并发提速与独立保证**：5 个审稿子代理在完全平行的会话空间中并行运行，耗时缩短 60% 以上，评审报告汇总后由主 Agent 统一生成结构化综合决策与修订单（Revision Roadmap）。

### 2. 交互式检查点决策（Checkpoints via `ask_question`）
流水线包含 10 个关键的决策检查点。在 AGY 中，统一使用 `ask_question` 工具渲染多选/单选交互卡片，阻塞式等待用户确认：
- **Stage 1 RESEARCH 结束**：确认 RQ Brief 与方法论蓝图（[确认推进] / [继续苏格拉底探讨] / [微调方向]）。
- **Stage 2 WRITE 提纲确认**：确认写作结构与论据映射表。
- **Stage 2.5 学术诚信闸门**：展示 7 类缺陷初检报告并由用户确认。
- **Stage 3 REVIEW 审稿决议**：展示同行评审综合意见，供用户选择处理策略（[接受建议进行大修] / [反驳审稿人部分意见] / [放弃转向]）。
- **Stage 3→4 修订辅导**：确认修改路线图策略。
- **Stage 4 REVISE 修订确认**：确认修改稿与逐条答辩表。
- **Stage 3' RE-REVIEW 复审**：复审决议确认。
- **Stage 4' RE-REVISE 终稿冻结**：最终文本内容冻结。
- **Stage 4.5 终极学术诚信闸门**：展示 Mode 2 深度诚信检查与材料护照完整性报告。
- **Stage 5 FINALIZE 排版确认**：选择输出格式（[LaTeX] / [Markdown] / [DOCX via Pandoc] / [PDF]）。

### 3. 富媒体、Generative UI 与学术公式呈现（Artifacts, KaTeX & Generative UI）
- **学术产物持久化**：阶段产物（Research Brief, Literature Matrix, Outline, Editorial Decision Letter 等）统一沉淀至工作区或 Artifacts 系统。
- **公式排版**：正文中的所有数学模型、因果关系与统计公式统一使用 KaTeX 渲染（行内 `$ ... $`，独立块 `$$ ... $$`）。
- **可视化流程**：系统文献回顾筛选流程统一采用 Mermaid 流程图（PRISMA Flowchart）呈现。
- **Generative UI 交互仪表盘**：在同行评审决议、修改清单与系统综述漏斗中，支持调用 `generative_ui` 渲染交互式 HTML 仪表盘（5 视角雷达评分板、可按严重度过滤折叠的审稿意见卡片、可动态勾选的修订单）。
- **学术警示**：潜在的方法论风险或局限性使用 GitHub 提示框（`> [!WARNING]` 或 `> [!IMPORTANT]`）高亮展示。

### 4. 科学学术检索工具智能联动（Scientific Tools Auto-Discovery）
在 `skills/deep-research` 与引文真实性核验中，主 Agent 会自动检测环境中可用的 Antigravity 专业学术插件：
- **通用学术与 DOI 校验**：优先调度 `literature-search-openalex` 解析全球学术图谱、作者成果与精确 DOI。
- **理工与计算机前沿预印本**：优先调度 `literature-search-arxiv` 检索 CS、物理、数学领域最新突破。
- **生命科学与医学文献**：优先调度 `pubmed-database` 或 `literature-search-europepmc` 检索权威临床与生化文献。
- **兜底机制**：仅在当前环境缺乏上述专业学术检索工具时，才优雅回退至通用 `search_web`。

### 5. 系统级快捷指令协同建议（Non-intrusive Slash Command Suggestions）
AI 副驾驶在特定研究卡点场景下，可非侵入式向用户推荐搭配使用 Antigravity 系统级命令：
- 选题模糊或论证卡点时：友好提示用户可随时使用 `/grill-me` 开展多轮批判式深访；
- 需要高耗时深入文献挖掘时：提示用户可选用 `/goal` 令代理自主长程推进；
- 论文面临严苛同行审查或重大结论推演时：提示用户可选用 `/boost` 调动多视角深层推演。

---

## 模式分发与触发映射表（Mode Registry）

用户可通过**自然语言意图**或**历史别名**直接触发对应的技能与子模式：

| 意图分类 | 自然语言触发短语示例 | 历史命令别名 | 目标技能与运行模式 | 核心产出成果 |
| :--- | :--- | :--- | :--- | :--- |
| **全流程流水线** | “从零开始写论文”、“端到端完成论文”、“学术研究流水线” | `ars-full` | `academic-pipeline` (orchestrator) | 完整研究论文包、材料护照、两阶段同行评审记录 |
| **文献与研究** | “我想梳理关于...的文献”、“做系统综述”、“帮我定研究问题” | `deep-research` | `skills/deep-research` (full) | RQ Brief、PRISMA 综述报告、综合研报 |
| **苏格拉底启发** | “我不确定研究什么”、“引导我理清思路”、“帮我想想选题” | `socratic` | `skills/deep-research` (socratic) | 苏格拉底式多轮启发式对话、聚焦后的 RQ |
| **三段式对比** | “对比这几篇文献”、“做三段式文献扫描”、“WHY HOW WHAT” | `ars-3w` | `skills/deep-research` (three-way-scan)| 三维度文献对比矩阵 |
| **论文规划** | “帮我规划论文结构”、“章节细化”、“制定写作计划” | `ars-plan` | `skills/academic-paper` (plan) | 逐章详细计划与论据规划表 |
| **大纲生成** | “帮我列论文提纲”、“梳理论证大纲与证据映射” | `ars-outline` | `skills/academic-paper` (outline-only) | 结构化大纲与 Claim-Evidence 映射 |
| **双语摘要** | “写摘要”、“中英文学术摘要与关键词” | `ars-abstract` | `skills/academic-paper` (abstract-only)| 符合期刊标准的规范中英文双语摘要 |
| **文献评述** | “写文献综述章节”、“生成带评注的参考文献” | `ars-lit-review`| `skills/academic-paper` (lit-review) | 规范学术文献综述草稿 |
| **论文修改** | “根据审稿意见修改论文”、“帮我改稿”、“落实修改清单” | `ars-revision` | `skills/academic-paper` (revision) | 逐项修订后稿件与修改对照表 |
| **修订教练** | “如何应对这些审稿意见”、“帮我理清修改路线图” | `ars-revision-coach`| `skills/academic-paper` (revision-coach)| 结构化审稿意见拆解与修改建议清单 |
| **答辩信审计** | “审查我的答辩信草稿”、“检查对审稿意见的回应是否充分” | `ars-rebuttal-audit`| `skills/academic-paper` (rebuttal-audit)| 答辩信合规性与论证强度审计报告 |
| **引用合规** | “检查论文引用格式”、“核对参考文献规范” | `ars-citation-check`| `skills/academic-paper` (citation-check)| 引用合规报告与缺失项清单 |
| **格式转换** | “将论文转换为LaTeX格式”、“转为DOCX或Markdown” | `ars-format-convert`| `skills/academic-paper` (format-convert)| LaTeX源码包 / DOCX / PDF 导出 |
| **AI使用披露** | “生成AI使用合规声明”、“AI使用披露” | `ars-disclosure` | `skills/academic-paper` (disclosure) | 严格符合期刊伦理的 AI 使用声明 |
| **同行盲审** | “帮我模拟同行评审”、“以审稿人角度挑刺”、“评审这篇论文”| `ars-reviewer` | `skills/academic-paper-reviewer` (full) | 5 视角独立同行评审报告、Editorial Decision |

---

## 运维与材料护照辅助工具（Utilities）

在材料护照（Material Passport）与文献真实性验证中，支持以下辅助能力：
- **`ars-mark-read`**: 记录作者对某篇参考文献的阅读确认声明（`read_scope` 支持 `full_text`, `sections`, `abstract_only`），防止未经审阅即进行强断言。
- **`ars-unmark-read`**: 撤销已记录的阅读证明。
- **`ars-cache-invalidate`**: 清除本地 SQLite 引文检索与 DOI 验证缓存，强制进行线上联网再核验。

---

## 环境降级与依赖说明

- **本地编译**：若本地未安装 TeX Live / Tectonic 或 Pandoc，系统将输出标准的 GitHub Flavored Markdown，并引导用户使用 Overleaf 进行排版编译。
- **学术检索**：推荐在 Antigravity 中配置 `literature-search-openalex` 或 `literature-search-arxiv` 工具，无需商业 API Key 即可进行精确学术文献检索。
