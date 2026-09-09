# ARS-agy Setup Guide

Prerequisites and setup instructions for **Academic Research Skills for Antigravity (ARS-agy)** on Google Antigravity.

---

## Minimum Viable Setup

1. Have Google Antigravity installed and running.
2. Clone this repository into your project workspace (or symlink to global skills).
3. Start an Antigravity conversation and ask your research question.

No proprietary API keys or external Python dependencies are strictly required for the core prompt-driven skills (deep-research, academic-paper, academic-paper-reviewer, academic-pipeline).

---

## Installation Methods in Antigravity

Before relying on any of those mechanisms, check the per-channel map: [CONTROL_AVAILABILITY.md](CONTROL_AVAILABILITY.md) and data flows: [DATA_FLOWS.md](DATA_FLOWS.md).

Antigravity supports customizations via Plugins, Workspace Skills, or Global Skills.

### Method 1: Antigravity Native Plugin Mode (Recommended)

Installs ARS-agy as a managed Antigravity Plugin, automatically activating its rules (`rules/AGENTS.md`), plugin manifest (`plugin.json`), and bundled skills (`skills/`).

```bash
# Global plugin installation (accessible in all sessions):
mkdir -p ~/.gemini/config/plugins
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/.gemini/config/plugins/academic-research-skills-agy

# Or project-level plugin installation (in your project repository):
cd /path/to/your/research-project
mkdir -p .agents/plugins
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git .agents/plugins/academic-research-skills-agy
```

### Method 2: Workspace Skills Mode

Ideal for dedicated research projects or thesis workspaces where you only want the skills loaded without plugin namespacing.

```bash
# In your research workspace directory:
cd /path/to/your/research-workspace
mkdir -p skills
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git skills/academic-research-skills-agy
```

Because `skills/academic-research-skills-agy/skills/` contains symlinks to the 4 core skills, Antigravity will discover:
- `skills/academic-research-skills-agy/skills/deep-research/SKILL.md`
- `skills/academic-research-skills-agy/skills/academic-paper/SKILL.md`
- `skills/academic-research-skills-agy/skills/academic-paper-reviewer/SKILL.md`
- `skills/academic-research-skills-agy/skills/academic-pipeline/SKILL.md`

### Method 3: Global Skills Mode (Symlinks)

Allows ARS-agy skills to be invoked across all Antigravity projects and sessions:

```bash
# Clone to a permanent local path:
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/skills/academic-research-skills-agy

# Create symlinks to the Antigravity global skills directory:
mkdir -p ~/.gemini/antigravity/skills
ln -s ~/skills/academic-research-skills-agy/deep-research ~/.gemini/antigravity/skills/deep-research
ln -s ~/skills/academic-research-skills-agy/academic-paper ~/.gemini/antigravity/skills/academic-paper
ln -s ~/skills/academic-research-skills-agy/academic-paper-reviewer ~/.gemini/antigravity/skills/academic-paper-reviewer
ln -s ~/skills/academic-research-skills-agy/academic-pipeline ~/.gemini/antigravity/skills/academic-pipeline
```

---

## Standing Preferences via `GEMINI.md`

Antigravity automatically loads `GEMINI.md` from your workspace root. You can specify standing research preferences that all agents will respect:

```markdown
## ARS Standing Preferences

- Citation style: APA 7th (or GB/T 7714 for Chinese manuscripts) unless venue template specifies otherwise.
- Literature search: Exclude unverified preprints unless explicitly requested; prioritize peer-reviewed Q1/Q2 journal articles.
- Language preference: Output bilingual abstracts (English and Simplified Chinese) conforming to academic standards.
- Open Access: Prefer Open Access copies when citing, and provide verifiable DOI / OpenAlex links.
```

---

## Recommended Tooling & Dependencies

### 1. Scholarly Search Skills (Zero-API Setup)
ARS-agy works seamlessly with Antigravity's built-in scholarly search skills:
- **`literature-search-openalex`**: Performs DOI resolution, bibliographic metadata retrieval, and citation graph exploration against the open OpenAlex corpus.
- **`literature-search-arxiv`**: Pre-retrieves full-text abstracts and PDF metadata for recent computer science, physics, mathematics, and quantitative biology preprints.

### 2. Document Export Tools (Optional)
- **Pandoc** (for `.docx` export):
  ```bash
  # macOS
  brew install pandoc

  # Ubuntu / Debian
  sudo apt-get install pandoc
  ```
- **TeX Live / Tectonic** (for local `.pdf` compilation):
  ```bash
  # macOS
  brew install tectonic

  # Linux
  curl --proto '=https' --tlsv1.2 -fsSL https://drop-sh.fullyjustified.net | sh
  ```
  *Recommended fonts for CJK PDF rendering*: Source Han Serif SC/TC (思源宋体). If local TeX is unavailable, ARS outputs clean GFM Markdown and Overleaf-ready LaTeX archives.

---

## Optional Environment Flags

| Flag | Purpose | Reference |
| :--- | :--- | :--- |
| `ARS_PASSPORT_RESET=1` | Promotes FULL checkpoints to context-reset boundaries, saving tokens in long research pipelines. | `academic-pipeline/references/passport_as_reset_boundary.md` |
| `ARS_CROSS_MODEL=1` | Cross-model generates a blind, separately executed critique via subagents or external provider. | `shared/cross_model_verification.md` |
| `ARS_CLAIM_AUDIT=1` | Activates citation-level Claim-Faithfulness (L3) verification gate. | `docs/design/` |
| `ARS_SOCRATIC_READING_PROBE=1` | Activates reading-probe verification during Socratic ideation. | `deep-research/agents/socratic_mentor_agent.md` |

### Cross-Model Verification Setup (Optional)

```bash
# Choose your cross-verification model:
export ARS_CROSS_MODEL="gpt-5.5"
# or: export ARS_CROSS_MODEL="gemini-3.1-pro-preview"
# or: export ARS_CROSS_MODEL="gpt-5.6-sol"
# or use subscription transport: export ARS_CROSS_MODEL_TRANSPORT="codex"
```

---

## Verification

To verify that ARS-agy is active in your Antigravity environment:
1. Start an Antigravity conversation in your workspace.
2. Type: `帮我规划论文写作提纲` or `Help me plan my research paper`.
3. If Antigravity activates `academic-paper` and responds with a structured research planning prompt, setup is complete!
