# Academic Research Skills for Antigravity (ARS-agy)

> **Antigravity (AGY) 原生学术研究、写作与同行评审全流程协作框架**  
> 基于 `Imbad0202/academic-research-skills` (v3.21.1) 官方核心内核，针对 Google Antigravity 平台的 Subagents、渐进式技能加载、Artifacts 与交互卡片体系深度定制。

---

## 核心架构与四大技能

ARS-agy 是一套面向学术全流程（从文献探索到完稿发表）的高水准研究协作者网络。它包含 4 个核心下游技能（位于 `skills/` 目录）：

```
[Antigravity Agent]
   │
   ├──▶ [deep-research]              文献综述、PRISMA系统性回顾、苏格拉底引导演进
   ├──▶ [academic-paper]             学术论文撰写、论据链构建、风格校准、去AI味
   ├──▶ [academic-paper-reviewer]    5视角独立同行盲审团队（含魔鬼代言人反驳）
   └──▶ [academic-pipeline]          10阶段全流程调度器与学术诚信闸门
```

---

## 核心约束与学术诚信铁律（IRON RULES）

1. **真实性与防幻觉底线**：
   - 严禁虚构参考文献。每条引用必须提供可核实的标题、作者、年份及 DOI/PMID/ArXiv ID。
   - 引用文本必须真实支撑正文主张（L3 Claim-faithfulness），不得断章取义或把未验证的假说描述为既定结论。
   - 严格拦截 Lu et al. (2026) 提出的 7 类 AI 科研失败模式（M1~M7），包括代码 bug 包装为创新发现、虚构引用、走捷径与框架锁定。
2. **副驾驶定位（Human-in-the-loop）**：
   - AI 是研究者的副驾驶，不是机长。AI 生成内容不得直接标记为 `executed` 或 `verified`。
   - 不得越权替作者做学术决策。在研究问题（RQ）、论点取舍、审稿决议（Accept/Major/Minor/Reject）等关键节点必须由人类确认。
3. **搜索后给判断，不只列结果**：
   - 检索不是堆砌列表。必须给出综合研判（如：“该领域近3年集中于X，但在Y机制上存在明显空白，你的差异化切入点在于...”）。

---

## Antigravity (AGY) 专属执行协议

在 Antigravity 平台中运行 ARS 时，遵循以下原生执行机制：

### 1. 独立子代理盲审（Subagents Delegation）
为彻底杜绝大模型在单一长会话中自我肯定、阿谀奉承（Sycophancy）的倾向，在运行 `academic-paper-reviewer` 时：
- **同行评审分流**：使用 `invoke_subagent` 派生独立的审稿子代理（如 `@MethodologyReviewer`、`@DomainReviewer`）；
- **魔鬼代言人（Devil's Advocate）**：必须在完全隔离的子代理环境中运行，赋予其“全力寻找论证漏洞与反面论据”的强制指令；
- 评审报告汇总后，由主 Agent 综合生成结构化决策与修订单（Revision Roadmap）。

### 2. 交互式检查点决策（Checkpoints via `ask_question`）
原版流水线中包含 10 个关键的决策检查点。在 AGY 中，请使用 `ask_question` 工具渲染多选卡片：
- **Stage 1 RESEARCH 结束**：确认 RQ Brief 与方法论蓝图（[确认推进] / [继续苏格拉底探讨] / [微调方向]）。
- **Stage 2 WRITE 提纲确认**：确认写作结构与论据映射表。
- **Stage 3 REVIEW 审稿决议**：展示同行评审综合意见，供用户选择处理策略（[接受建议进行大修] / [反驳审稿人部分意见] / [放弃转向]）。
- **Stage 2.5 / 4.5 学术诚信闸门**：展示 7 类缺陷检查报告并由用户确认。

### 3. 富媒体与学术公式呈现（Artifacts & KaTeX）
- **公式排版**：正文中的所有数学模型、因果关系与统计公式统一使用 KaTeX 渲染（行内 `$ ... $`，独立块 `$$ ... $$`）；
- **可视化流程**：系统文献回顾筛选流程统一采用 Mermaid 流程图（PRISMA Flowchart）呈现；
- **学术警示**：潜在的方法论风险或局限性使用 GitHub 提示框（`> [!WARNING]` 或 `> [!IMPORTANT]`）高亮展示。

---

## 快速调用与触发指引

| 用户需求 | 推荐调用的 Skill | 产出成果 |
| :--- | :--- | :--- |
| “我想梳理关于...的文献”、“做系统综述”、“帮我定研究问题” | `skills/deep-research` | RQ Brief、PRISMA 文献矩阵、综合研报 |
| “帮我起草论文导论”、“把这段论点写得更有学术味”、“去AI感” | `skills/academic-paper` | 规范章节草稿、论据映射图、BibTeX |
| “帮我模拟盲审这篇论文”、“以审稿人角度挑刺”、“准备答辩” | `skills/academic-paper-reviewer` | 5视角同行评审报告、修改路线图、魔鬼代言人质疑 |
| “全流程写一篇学术论文”、“从零开始搞定论文” | `skills/academic-pipeline` | 跨阶段材料护照（Material Passport）、完稿包 |

---

## 环境降级与配置说明

- **本地编译**：若本地未安装 TeX Live / Tectonic 或 Pandoc，系统将输出标准的 GitHub Flavored Markdown，并引导用户使用 Overleaf 快速排版。
- **学术检索**：推荐配置 `literature-search-openalex` 或 `paper-search-mcp`，无需昂贵的商业 API Key 即可进行精确学术检索。
