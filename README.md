# Academic Research Skills for Antigravity (ARS-agy)

[![Version](https://img.shields.io/badge/version-v3.21.1-blue)](https://github.com/DGU-stallion/academic-research-skills-agy)
[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Platform: Antigravity](https://img.shields.io/badge/Platform-Google%20Antigravity-4285F4.svg)](https://github.com/DGU-stallion/academic-research-skills-agy)
[![Upstream: v3.21.1](https://img.shields.io/badge/Upstream-v3.21.1-blue.svg)](https://github.com/Imbad0202/academic-research-skills)

[简体中文](README.zh-CN.md) | [English](README.md) | [繁體中文](README.zh-TW.md)

**ARS-agy** is a native academic research, paper writing, and peer review collaboration suite designed specifically for **Google Antigravity** (with native Antigravity Plugin specification support).

Adapted and restructured from the upstream open-source project [Imbad0202/academic-research-skills](https://github.com/Imbad0202/academic-research-skills) (v3.21.1), ARS-agy is released under the [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/) license. For the upstream project's detailed evolution history, methodology background, comprehensive changelogs, and contributor list, please visit the upstream repository directly.

---

## Core Philosophy: The Human-in-the-Loop Copilot

> **AI is your research copilot, not the pilot.**  
> ARS-agy handles the structural, analytical, and formatting heavy lifting: systematic literature scans, claim-evidence alignment, cross-verification of data and figures, citation compliance, and simulated peer review. However, the core research questions, methodological formulation, interpretation of empirical findings, and ultimate scholarly responsibility always remain with the human researcher.

- **Academic Integrity & Anti-Hallucination**: Hallucinated references are strictly prohibited. Every cited reference must provide verifiable scholarly identifiers (DOI, ArXiv ID, PMID, etc.), ensuring authentic claim-faithfulness (L3 grounding) backed by a deterministic citation-existence verification gate. The framework actively guards against the 7 AI research failure modes identified by Lu et al. (2026), uses an empirical research question advisory (held-out miss rate 0.34–0.38 → 0.094 with false-fire 0/16 preserved), and incorporates a deterministic numeric/citation token-conservation checker during revision.
- **Prose Quality & Rigor**: Eliminates generic AI filler and stylistic artifacts, calibrating tone and structure against rigorous academic publishing standards (APA 7.0, IEEE, GB/T 7714, etc.).

---

## Antigravity (AGY) Native Features

ARS-agy deeply integrates with Google Antigravity's agentic orchestration and interactive capabilities:

### 1. Native Antigravity Plugin Ecosystem
- Full compliance with the Antigravity Plugin standard (`plugin.json` manifest, `rules/AGENTS.md` standing rules, and 4 bundled core skills in `skills/`), discoverable and configurable directly inside Antigravity's Plugins UI.
- Seamless coordination across literature research, writing, blind reviewing, and pipeline orchestration.

### 2. Parallel Subagents Delegation for Blind Peer Review
To prevent sycophancy and self-serving bias inherent in single-context conversations, ARS-agy dynamically spins off 5 isolated review subagents concurrently using a single-call `invoke_subagent` dispatch:
- **Journal-Fit Reviewer**: Assesses manuscript fit with target venue scope and criteria;
- **Methodology Reviewer**: Scrutinizes statistical rigor, experimental validity, and boundary conditions;
- **Domain Reviewer**: Assesses theoretical depth and breadth of prior literature coverage;
- **Perspective Reviewer**: Evaluates broader impact, interdisciplinary relevance, and practical utility;
- **Devil's Advocate Reviewer**: Operates in an isolated subagent conversation with explicit adversarial instructions to actively seek flaws, missing counter-evidence, and ungrounded assertions.

> 💡 **Concurrent Speedup & Anti-Sycophancy**: All 5 reviewer seats execute in physically isolated context windows in parallel, **reducing review turnaround time by over 60%** while guaranteeing zero cross-contamination.

Full peer review executes under full mode (Journal-Fit Reviewer + R1/R2/R3 + Devil's Advocate) with a strict First-round review panel vs. contract-governed re-review dispatch boundary. Current live reviews remain `NOT_CALIBRATED`, and the typed trajectory carrier is deferred.
The orchestrator synthesizes these independent evaluations into a structured Editorial Decision Letter and actionable Revision Roadmap.

### 3. Interactive Checkpoints via `ask_question`
At key decision milestones across the pipeline, ARS-agy invokes Antigravity's native `ask_question` card UI to block and await human confirmation:
- **Research Brief Confirmation**: Approves the Research Question (RQ) formulation and methodology blueprint;
- **Outline & Argument Review**: Confirms the Claim-Evidence Matrix and section layout;
- **Editorial Decision Handling**: Evaluates simulated peer review feedback and chooses an action strategy (Major Revision, Minor Revision, Rebuttal, or Pivot);
- **Integrity Gate Clearance**: Inspects and signs off on the 7-mode academic integrity audit report;
- **Final Packaging**: Selects preferred output formats (LaTeX, Markdown, DOCX via Pandoc, or PDF).

### 4. Rich Scholarly Media, Generative UI & KaTeX (Artifacts & UI Widgets)
- **Artifact Persistence**: Key deliverables (Research Briefs, Literature Matrices, Revision Roadmaps, Decision Letters) are automatically saved to Antigravity Artifacts;
- **Generative UI Interactive Dashboards**: In addition to standard Markdown reports, renders interactive HTML widgets (5-seat radar scoring card, filterable issue drawers by Critical/Major/Minor, author checklists, and dynamic PRISMA screening funnels);
- **KaTeX Equations**: Inline (`$ ... $`) and display (`$$ ... $$`) mathematical and causal models are cleanly formatted for KaTeX rendering;
- **PRISMA Flowcharts**: Systematic review search flows are visualized using native Mermaid diagrams;
- **Scholarly Warnings**: Methodological risks, threats to validity, and evidence gaps are highlighted using GitHub alert callouts (`> [!WARNING]` / `> [!IMPORTANT]`).

### 5. Scientific Tools Auto-Discovery
During literature discovery and claim verification, the pipeline automatically detects and prioritizes installed Antigravity scholarly plugins:
- **Global Scholarly Graph & DOI Verification**: Prioritizes `literature-search-openalex`;
- **Computer Science & Physics Preprints**: Prioritizes `literature-search-arxiv`;
- **Biomedical & Life Sciences**: Prioritizes `pubmed-database` or `literature-search-europepmc`;
- Falls back to general web search only when specialized scholarly tools are not loaded.

### 6. Bilingual & Natural Language Support
- **Zero-Friction Triggers**: Invoke skills naturally in English or Chinese without remembering esoteric command flags (e.g., "Help me structure this paper", "Conduct a systematic literature review", "Simulate a blind peer review");
- **Typography & Standards**: Built-in support for Source Han Serif (思源宋体) typography profiles and international citation styles.

---

## Installation & Setup Guide

> **Which controls are active in your install channel?** Availability varies by install channel. See the per-channel map: [docs/CONTROL_AVAILABILITY.md](docs/CONTROL_AVAILABILITY.md).  
> **Data Flows & Risk Management**: Check what leaves your machine in [docs/DATA_FLOWS.md](docs/DATA_FLOWS.md) and review existing risk controls in [docs/RISK_REGISTER.md](docs/RISK_REGISTER.md).

ARS-agy can be deployed in Google Antigravity in three ways, with Native Plugin Mode strongly recommended:

### Option 1: Native Antigravity Plugin Mode (Recommended)

Packages rules, skills, and configuration into a unified plugin unit managed directly by Antigravity:

#### 1. Global Plugin Install (Recommended across all sessions)
Clone the repository into your global Antigravity plugins directory:

```bash
mkdir -p ~/.gemini/config/plugins
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/.gemini/config/plugins/academic-research-skills-agy
```

#### 2. Project Workspace Plugin Install (Team collaboration)
Clone into your project's `.agents/plugins/` directory:

```bash
cd /path/to/your/research-project
mkdir -p .agents/plugins
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git .agents/plugins/academic-research-skills-agy
```

> **Plugin Ingestion**: Antigravity automatically detects `plugin.json`, loads `rules/AGENTS.md`, and exposes the 4 skills in `skills/`. You can view or toggle the plugin in Antigravity's Plugins settings.

---

### Option 2: Project Workspace Skills Mode

Attach ARS-agy as project-level skills:

```bash
cd /path/to/your/research-project
mkdir -p skills
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git skills/academic-research-skills-agy
```

---

### Option 3: Global Skills Mode (Symlink)

Symlink individual skills to the global skills directory:

```bash
# 1. Clone repository to a stable local path
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/skills/academic-research-skills-agy

# 2. Symlink the 4 core skills into Antigravity global skills directory
mkdir -p ~/.gemini/antigravity/skills
ln -s ~/skills/academic-research-skills-agy/deep-research ~/.gemini/antigravity/skills/deep-research
ln -s ~/skills/academic-research-skills-agy/academic-paper ~/.gemini/antigravity/skills/academic-paper
ln -s ~/skills/academic-research-skills-agy/academic-paper-reviewer ~/.gemini/antigravity/skills/academic-paper-reviewer
ln -s ~/skills/academic-research-skills-agy/academic-pipeline ~/.gemini/antigravity/skills/academic-pipeline
```

---

### Verification & Recommended Environment

1. **Verify Installation**:
   In your Antigravity chat, send any prompt such as:
   - `Help me plan the structure of my paper`
   - `Conduct a systematic literature review on...`
   - `/ars-plan`

   When Antigravity activates `academic-paper` or `deep-research` and begins a Socratic dialogue, the installation is verified.

2. **Recommended Search Skills**:
   For authentic literature discovery without proprietary API keys, pair ARS-agy with Antigravity's built-in scholarly search tools:
   - `literature-search-openalex`: Queries the OpenAlex academic graph, resolves DOIs, and retrieves metadata;
   - `literature-search-arxiv`: Searches recent preprints across CS, Physics, Math, and Quantitative Biology.

3. **Optional Export Tools**:
   - **Pandoc**: Required for converting manuscripts to `.docx`;
   - **TeX Live / Tectonic**: For local LaTeX compilation to APA 7.0 PDFs. (If unavailable, ARS-agy automatically produces clean GFM Markdown and Overleaf-ready LaTeX source bundles).

---

## Core Skills Overview

| Skill Name | Scope | Typical Triggers (Natural Language / Alias) | Key Deliverables |
| :--- | :--- | :--- | :--- |
| **`academic-pipeline`** | **End-to-end orchestrator with integrity gates** | "Write paper from scratch", "Academic research pipeline", "End-to-end paper workflow"<br>`ars-full` | Comprehensive manuscript package, Material Passport, two-stage peer review records |
| **`deep-research`** | **Literature review & Socratic inquiry** | "Conduct literature review", "Systematic review on...", "Guide my research questions"<br>`deep-research` / `socratic` / `ars-3w` | Research Question Brief, PRISMA Review Report, 3-Way Comparative Matrix |
| **`academic-paper`** | **Manuscript writing & claim alignment** | "Outline paper", "Bilingual abstract", "Revise paper according to reviewer feedback"<br>`ars-plan` / `ars-outline` / `ars-abstract` / `ars-revision` | Detailed chapter plans, Claim-Evidence Mapping, bilingual abstracts, rebuttal tables |
| **`academic-paper-reviewer`** | **Multi-perspective blind peer review** | "Review this paper", "Critique manuscript", "Devil's advocate review"<br>`ars-reviewer` | 5-seat independent review reports, Editorial Decision Letter |

---

## Academic Integrity: The Iron Rules

Across all modes and skills, ARS-agy enforces strict integrity standards:

1. **Citation Authenticity**: Fabricating citations, authors, or DOIs is strictly forbidden. When literature cannot be verified, the boundary of search is honestly reported.
2. **L3 Claim-Faithfulness**: References must substantively support the claims they are cited for. Out-of-context citation is flagged and rejected.
3. **Human Sign-Off**: AI never makes unilateral decisions on research scoping, reviewer responses, or manuscript sign-off. Human scholars retain full governance at every checkpoint.

---

## License & Attribution

- **License**: Released under the [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/) license. You are free to share and adapt for non-commercial research and academic use, provided appropriate credit is given.
- **Upstream Attribution**: Sincere gratitude to [Cheng-I Wu (@Imbad0202)](https://github.com/Imbad0202) for creating the original [academic-research-skills](https://github.com/Imbad0202/academic-research-skills) project, which established the foundational methodologies and protocols for AI research collaboration.

To cite the upstream project:
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
