# Quick Start Guide: Academic Research Skills for Antigravity (ARS-agy)

Get from zero to your first AI-assisted research in 3 simple steps on Google Antigravity.

---

## Step 1: Install Plugin / Skills in Antigravity

Choose one of the following installation methods:

### Option A: Antigravity Native Plugin Mode (Recommended)
Install as a complete Antigravity plugin with rules and skills automatically managed:

```bash
# Global plugin (recommended across all projects)
mkdir -p ~/.gemini/config/plugins
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/.gemini/config/plugins/academic-research-skills-agy
```

### Option B: Workspace Skills Mode (Per-project)
Add ARS-agy to your current research project folder:

```bash
cd /path/to/your/research-project
mkdir -p skills
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git skills/academic-research-skills-agy
```

### Option C: Global Skills Mode (Symlink)
Install globally via symlink:

```bash
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/skills/academic-research-skills-agy
mkdir -p ~/.gemini/antigravity/skills
ln -s ~/skills/academic-research-skills-agy/deep-research ~/.gemini/antigravity/skills/deep-research
ln -s ~/skills/academic-research-skills-agy/academic-paper ~/.gemini/antigravity/skills/academic-paper
ln -s ~/skills/academic-research-skills-agy/academic-paper-reviewer ~/.gemini/antigravity/skills/academic-paper-reviewer
ln -s ~/skills/academic-research-skills-agy/academic-pipeline ~/.gemini/antigravity/skills/academic-pipeline
```

---

## Step 2: Open Antigravity

Open your research project workspace in Antigravity (via Antigravity IDE, CLI, or web interface). Antigravity automatically detects the plugin or skills.

---

## Step 3: Start Researching

Simply express what you need in natural language (English or Chinese). Antigravity will automatically route to the right skill and mode.

### Example 1: Socratic Guided Inquiry (Brainstorming & RQ Definition)

```text
You: "I have a broad idea about evaluating code generation consistency across LLM architectures, but I am not sure how to frame the research question. Can you guide me?"
```
> Antigravity activates `deep-research` (socratic mode), guiding you through critical questions to narrow down variables, hypotheses, and scope.

### Example 2: Plan a Paper Chapter-by-Chapter

```text
You: "Help me outline and plan a research paper investigating reinforcement learning from human feedback in robotics."
```
> Antigravity activates `academic-paper` (plan / outline mode), mapping claims to supporting evidence.

### Example 3: Multi-Perspective Blind Peer Review

```text
You: "Review this draft paper [attached document] as an academic reviewer team. Focus on methodology rigor and potential counterarguments."
```
> Antigravity activates `academic-paper-reviewer`, delegating to independent reviewer subagents and an isolated Devil's Advocate.

### Example 4: Full End-to-End Pipeline

```text
You: "I want to conduct an end-to-end research project on multi-agent consensus protocols, from literature search to publication draft."
```
> Antigravity activates `academic-pipeline`, orchestrating the 10-stage process with interactive `ask_question` decision cards at each gate.

---

## Which Mode Should I Use?

| I want to... | Skill & Mode | Natural Prompt / Alias |
| :--- | :--- | :--- |
| Clarify or refine a vague idea | `deep-research` (socratic) | "Guide my research questions" / `socratic` |
| Fast literature overview | `deep-research` (quick) | "Literature overview on [topic]" |
| PRISMA systematic review | `deep-research` (systematic-review) | "Conduct systematic review on [topic]" |
| 3-way literature comparison | `deep-research` (three-way-scan) | "Compare these papers" / `ars-3w` |
| Draft a complete paper | `academic-paper` (full) | "Help me write a research paper" |
| Create structured outline & claim map | `academic-paper` (outline) | "Outline this paper" / `ars-outline` |
| Generate bilingual abstract | `academic-paper` (abstract) | "Generate bilingual abstract" / `ars-abstract` |
| Address reviewer comments | `academic-paper` (revision) | "Revise paper based on review comments" / `ars-revision` |
| Independent blind peer review | `academic-paper-reviewer` (full) | "Review this paper" / `ars-reviewer` |
| Complete 10-stage research pipeline | `academic-pipeline` (orchestrator) | "End-to-end research pipeline" / `ars-full` |

---

## What's Next?

- [Full Readme (Simplified Chinese)](README.zh-CN.md)
- [Full Readme (English)](README.md)
- [Upstream Repository](https://github.com/Imbad0202/academic-research-skills)
