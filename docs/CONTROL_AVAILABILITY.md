# Control Availability Matrix

This document maps integrity controls, runtime mechanisms, and degradation postures across install channels for **Academic Research Skills for Antigravity (ARS-agy)**.

---

## Install channels

| Channel | Documented in | Channel-wide limitation |
|---|---|---|
| **Plugin** — Antigravity native plugin mode | [SETUP Method 1](SETUP.md#method-1-antigravity-native-plugin-mode-recommended) | None — the reference channel. Manifest (`plugin.json`), standing rules (`rules/AGENTS.md`), and skills are all automatically wired. |
| **Workspace Skills** — Project-level skills mode | [SETUP Method 2](SETUP.md#method-2-workspace-skills-mode) | Skills operate in the local workspace directory without global plugin scope. |
| **Global Skills** — Global symlinked skills mode | [SETUP Method 3](SETUP.md#method-3-global-skills-mode-symlinks) | Skills are available globally across all sessions via symlinks in `~/.gemini/antigravity/skills/`. |

## Availability matrix

Legend: **Active** = operates as documented · **Conditional** = operates only under the noted conditions, with a defined degraded state otherwise · **Absent** = does not operate in this channel. Read down your channel's column: a claim about a mechanism holds only where its row says Active — or Conditional with the linked note's conditions met — after applying your channel's channel-wide limitation above.

| Mechanism | Plugin | Workspace Skills | Global Skills |
|---|---|---|---|
| Methodology layer (the four skills' `SKILL.md` protocols) | Active | Active | Active |
| Skill auto-routing (trigger keywords → skill activation) | Active | Active | Active |
| Antigravity subagent orchestration (`invoke_subagent` / `define_subagent`) | Active | Active | Active |
| Interactive checkpoints via `ask_question` | Active | Active | Active |
| Artifact persistence & KaTeX rendering | Active | Active | Active |
| Python-backed opt-in features (repo `scripts/`) | Conditional ⁽¹⁾ | Conditional ⁽¹⁾ | Conditional ⁽¹⁾ |
| Cross-model verification (consent-gated second model) | Conditional ⁽²⁾ | Conditional ⁽²⁾ | Conditional ⁽²⁾ |
| Prompt-level checkpoints and integrity gates | Active ⁽³⁾ | Active ⁽³⁾ | Active ⁽³⁾ |

CI-side checks (mutation-tested lints, content locks, changelog gates) run in this repository's GitHub Actions, protecting the published artifact all channels ship from, and never run on a user machine — identical for every channel. They do not all enforce at the same strength or fire on every change: the per-workflow classification is documented in [ARCHITECTURE.md](ARCHITECTURE.md). The machine-readable index of the suite's runtime graceful-degradation mechanisms is [`shared/contracts/degradation_registry.json`](../shared/contracts/degradation_registry.json).

## Notes

1. These features (e.g. the citation-verification gate CLI, the revision token-conservation checker, the submission-package verifier, the PDF read preflight, the cache commands) shell out to Python scripts at the repository root (`scripts/`, `shared/`), not inside the four skill folders. They require a Python 3.9+ environment with dependencies installed.
2. Cross-model verification requires provider API credentials and sits behind the boundary defined in [`shared/cross_model_verification.md`](../shared/cross_model_verification.md): explicit user consent per session via `ARS_CROSS_MODEL=1`. Unset, the feature makes zero external network calls.
3. The MANDATORY checkpoints, integrity gates, and IRON RULE constraints are prompt-level, trust-based controls with audit trails, executed by the session model following the skill instructions — not coercive runtime blocks. Documented overrides require recorded reasoning, and final integrity responsibility stays with the human researcher (see the [gap assessment §3](../audits/iso42001-spirit-gap-assessment-2026-08-17.md)).
4. Graceful handling of missing optional binaries and interpreters is documented in the [environment degradations](#environment-degradations-within-a-channel) table.

## Environment degradations within a channel

Independent of install channel, opt-in features and external tools gracefully degrade when optional dependencies are absent.

