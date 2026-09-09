# Academic Research Skills for Antigravity (ARS-agy)

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Platform: Antigravity](https://img.shields.io/badge/Platform-Google%20Antigravity-4285F4.svg)](https://github.com/DGU-stallion/academic-research-skills-agy)
[![Upstream: v3.21.1](https://img.shields.io/badge/Upstream-v3.21.1-blue.svg)](https://github.com/Imbad0202/academic-research-skills)

[日本語](README.ja-JP.md) | [English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [한국어](README.ko-KR.md)

**ARS-agy** は、**Google Antigravity** プラットフォーム向けに最適化された学術研究・論文執筆・査読コラボレーションフレームワークです。

本プロジェクトはオープンソースプロジェクト [Imbad0202/academic-research-skills](https://github.com/Imbad0202/academic-research-skills) (v3.21.1) をベースに Antigravity 向けに再構築したフォークであり、[CC BY-NC 4.0 (表示 - 非営利 4.0 国際)](https://creativecommons.org/licenses/by-nc/4.0/) ライセンスの下で公開されています。アップストリームの歴史、学術手法の詳細、更新履歴および貢献者一覧については、元リポジトリをご参照ください。

---

## 主な特徴 (Antigravity ネイティブ)

1. **Subagents による独立ブラインド査読**:
   単一対話における阿諛追従（Sycophancy）を排除するため、Antigravity の `invoke_subagent` / `define_subagent` を活用して査読パネル（Journal-Fit Reviewer + 3 動的レビュアー + Devil's Advocate）を動的に並行展開します。full モード（Journal-Fit Reviewer + R1/R2/R3 + Devil's Advocate）で全査読を行い、初回レビューパネル vs. 契約管理された再レビューディスパッチの境界を厳格に保持します。
2. **`ask_question` による対話型チェックポイント**:
   研究課題の確定、構成案の承認、査読判定（Major/Minor/Rebuttal）、整合性ゲートの確認などの重要判断点で対話型カードを表示し、研究者による主体的判断を仰ぎます。
3. **成果物の永続化と数式表示 (Artifacts & KaTeX)**:
   レビュー結果や執筆計画を Antigravity Artifacts に構造化保存し、数式は KaTeX、系統的レビューの PRISMA フローは Mermaid で視覚化します。
4. **学術的誠実性とハルシネーション防止**:
   実在しない参考文献の捏造を厳禁とし、引用と本文主張の整合性（L3 Claim-faithfulness）および 7 つの AI 研究失敗パターン（Lu et al., 2026）を厳格に検査します。

---

## インストール手順

### 方法 1: ワークスペースモード（推奨）
研究プロジェクトのディレクトリ内でスキルをクローンします:

```bash
cd /path/to/your/academic-project
mkdir -p skills
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git skills/academic-research-skills-agy
```

### 方法 2: グローバルスキルモード
全プロジェクトで共通利用できるようにユーザーディレクトリへシンボリックリンクを作成します:

```bash
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/skills/academic-research-skills-agy
mkdir -p ~/.gemini/antigravity/skills
ln -s ~/skills/academic-research-skills-agy/deep-research ~/.gemini/antigravity/skills/deep-research
ln -s ~/skills/academic-research-skills-agy/academic-paper ~/.gemini/antigravity/skills/academic-paper
ln -s ~/skills/academic-research-skills-agy/academic-paper-reviewer ~/.gemini/antigravity/skills/academic-paper-reviewer
ln -s ~/skills/academic-research-skills-agy/academic-pipeline ~/.gemini/antigravity/skills/academic-pipeline
```

---

## コアスキル構成

| スキル名 | 役割 | 主なトリガー例 |
| :--- | :--- | :--- |
| **`academic-pipeline`** | 全 10 段階の学術パイプライン統括と誠実性ゲート | "端到端论文研究", "Academic research pipeline" |
| **`deep-research`** | 文献調査・PRISMA 系統的レビュー・ソクラテス式対話 | "文献レビュー", "Systematic review" |
| **`academic-paper`** | 論文執筆・アウトライン作成・スタイル校正・査読対応 | "論文のアウトライン作成", "Write paper" |
| **`academic-paper-reviewer`** | 5 視点からの独立ブラインド査読と反論検証 | "論文を査読して", "Review this paper" |

詳細な使用方法や設定については [English README](README.md) または [簡体中文 README](README.zh-CN.md) をご覧ください。
