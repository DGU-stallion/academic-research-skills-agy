# Academic Research Skills for Antigravity (ARS-agy)

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Platform: Antigravity](https://img.shields.io/badge/Platform-Google%20Antigravity-4285F4.svg)](https://github.com/DGU-stallion/academic-research-skills-agy)
[![Upstream: v3.21.1](https://img.shields.io/badge/Upstream-v3.21.1-blue.svg)](https://github.com/Imbad0202/academic-research-skills)

[한국어](README.ko-KR.md) | [English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja-JP.md)

**ARS-agy**는 **Google Antigravity** 환경을 위해 네이티브로 최적화된 학술 연구, 논문 작성 및 동료 심사(Peer Review) 협업 프레임워크입니다.

본 프로젝트는 오픈소스 [Imbad0202/academic-research-skills](https://github.com/Imbad0202/academic-research-skills) (v3.21.1)을 기반으로 Antigravity에 맞게 포팅 및 재구성되었으며, [CC BY-NC 4.0 (저작자표시-비영리 4.0 국제)](https://creativecommons.org/licenses/by-nc/4.0/) 라이선스를 준수합니다. 원본 프로젝트의 상세한 역사, 학술 방법론, 업데이트 로그 및 기여자 명단은 원본 저장소를 참고해 주시기 바랍니다.

---

## Antigravity (AGY) 네이티브 주요 특징

1. **Subagents 기반 독립 동료 심사**:
   단일 세션에서 발생하기 쉬운 아첨 편향(Sycophancy)을 방지하기 위해 `invoke_subagent` 및 `define_subagent`를 사용하여 심사 패널 (Journal-Fit Reviewer + 동적 리뷰어 3명 + Devil's Advocate)을 동적으로 병렬 실행합니다. full 모드 (Journal-Fit Reviewer + R1/R2/R3 + Devil's Advocate)로 전체 심사를 진행하며, 1차 심사 패널 대 계약 기반 re-review 디스패치 경계를 엄격히 준수합니다.
2. **`ask_question` 대화형 체크포인트**:
   연구 질문(RQ) 확정, 아웃라인 검토, 심사 의견 결정(Major/Minor/Rebuttal), 연구 윤리 게이트 통과 등 중요한 분기점에서 대화형 선택 카드를 띄워 인간 연구자의 결정을 대기합니다.
3. **학술 아티팩트 영속화 및 수식 렌더링 (Artifacts & KaTeX)**:
   단계별 산출물을 Antigravity Artifacts로 체계적으로 저장하며, KaTeX 수식 및 Mermaid PRISMA 흐름도를 네이티브로 지원합니다.
4. **철저한 학술 윤리 및 허위 인용 방지**:
   존재하지 않는 문헌 위조를 엄격히 금지하며, 인용과 본문 주장 간의 정확한 뒷받침(L3 Claim-faithfulness)과 7가지 AI 연구 실패 패턴(Lu et al., 2026)을 차단합니다.

---

## 설치 및 설정 가이드

### 방법 1: 워크스페이스 모드 (권장)
연구 프로젝트 폴더 내에 스킬을 복제합니다:

```bash
cd /path/to/your/academic-project
mkdir -p skills
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git skills/academic-research-skills-agy
```

### 방법 2: 글로벌 스킬 모드
모든 Antigravity 대화에서 공통으로 사용할 수 있도록 글로벌 스킬 디렉토리에 심볼릭 링크를 생성합니다:

```bash
git clone https://github.com/DGU-stallion/academic-research-skills-agy.git ~/skills/academic-research-skills-agy
mkdir -p ~/.gemini/antigravity/skills
ln -s ~/skills/academic-research-skills-agy/deep-research ~/.gemini/antigravity/skills/deep-research
ln -s ~/skills/academic-research-skills-agy/academic-paper ~/.gemini/antigravity/skills/academic-paper
ln -s ~/skills/academic-research-skills-agy/academic-paper-reviewer ~/.gemini/antigravity/skills/academic-paper-reviewer
ln -s ~/skills/academic-research-skills-agy/academic-pipeline ~/.gemini/antigravity/skills/academic-pipeline
```

---

## 핵심 스킬 구성

| 스킬명 | 역할 | 주요 트리거 예시 |
| :--- | :--- | :--- |
| **`academic-pipeline`** | 10단계 전체 파이프라인 조율 및 연구 윤리 게이트 | "연구부터 논문까지", "Academic research pipeline" |
| **`deep-research`** | 문헌 고찰, PRISMA 체계적 문헌고찰, 소크라테스식 문답 | "문헌 조사", "체계적 문헌고찰" |
| **`academic-paper`** | 논문 작성, 아웃라인 및 주장 매핑, 스타일 교정, 심사 반영 | "논문 작성", "논문 계획을 도와줘" |
| **`academic-paper-reviewer`** | 5개 관점의 독립 블라인드 심사 및 반론 검증 | "논문 심사", "동료 심사 진행해줘" |

자세한 사용법과 설정은 [English README](README.md) 또는 [简体中文 README](README.zh-CN.md)를 참고하시기 바랍니다.
