# PROMPT for AI Coding Environment Setup

이 프롬프트는 어떤 AI 어시스턴트를 사용하여도 일관된 PDCA AI 코딩 개발환경 구성 가이드를 생성하도록 설계되었습니다.

---

### AI 프롬프트 원문

```text
역할: 시니어 데브옵스 엔지니어 및 테크니컬 라이터

목표: MacOS, Linux, Windows 사용자를 위한 'AI Coding 개발환경 구성' README.md 문서를 작성하라.
      AI 코딩을 처음 접하는 초보자(터미널 친숙, 코딩 경험 적음)도 따라 할 수 있도록 친절하게 구성하라.

문서 구조 (3-PART 2단계 구조):
  PART 1 — 첫 AI 코딩 (모두 대상, ~20분):
    Antigravity를 진입점으로 배치하여 설치 후 바로 AI와 대화할 수 있게 안내한다.
    PART 1 끝에 "여기서 멈춰도 됩니다" 체크포인트를 명시한다.
  PART 2 — AI 코딩 환경 완성 (심화):
    Gemini CLI, Claude Code (AWS Bedrock / Azure AI Foundry / GCP Vertex AI 포함), GitHub 자동화, bkit
  PART 3 — n8n 자동화 (고급):
    Docker, n8n, n8n-MCP+Skills, Python→n8n 마이그레이션, Claude Code n8n 개발

제약 조건:
1. 언어는 한국어로 작성하되, 전문 용어는 영어 원문을 병기하라.
2. 모든 명령어는 복사하여 붙여넣기 가능한 코드 블록으로 제공하라.
3. 운영체제별 설정 차이를 명확히 구분하여 설명하라.
4. **시각적 요소 강화**: 상단에 프로젝트 배너(`docs/assets/banner.png`)와 Shields.io 뱃지(Version, Node, Python, License)를 포함하라.
5. **가독성 최적화**: Quick Start에 PART 1 직접 링크와 예상 시간(~20분)을 안내하고, PART 1/2/3 구분선이 포함된 목차(TOC)를 제공하라.
6. 섹션 2.6 리모트 서버 설정에는 "네트워크 엔지니어라면 건너뛰어도 됩니다" 주석을 추가하라.
7. 클라우드 AI 서비스(AWS Bedrock, Azure AI Foundry, GCP Vertex AI) 비교 테이블을 제공하고, 상세 설명은 1개의 NOTE로 요약하며 각 공식 문서 링크를 제공하라.

포함 내용 (섹션 순서):
PART 1:
1. 사전 준비 사항 (Node.js, Git; Python은 PART 2부터 필요임을 명시)
2. SSH 및 Git 기본 설정 (Git config, SSH 키 생성/등록, SSH Config, 리모트 서버)
3. Antigravity 설치 및 설정 (VS Code 확장, 리모트 서버 접속)
   → PART 1 완료 체크포인트

PART 2:
4. Gemini CLI 설치 및 설정 (npm 설치, Google AI Studio API 발급, 멀티 계정 환경변수)
5. Claude Code 설치 및 설정 (npm 설치, 클라우드 AI 서비스 연동 (AWS / Azure / GCP), 터미널 활용법, CLAUDE.md 설정)
6. GitHub 연동 및 자동화 (gh 설치/인증, AI 릴리즈 자동화)
7. bkit 설치 (Claude Code 플러그인, Gemini CLI 익스텐션)

PART 3:
8. Docker 환경 구성 (MacOS/Linux/Windows 설치, docker-compose.yml 해설, .env 보안 관리)
9. n8n 컨테이너 설치 및 실행 (n8n 소개 및 Python 데몬 대비 장점, docker compose 명령어, API Key 발급)
10. n8n-MCP + n8n-skills 설정 (MCP 서버 연동, 7가지 스킬 설치 및 역할)
11. Python → n8n 마이그레이션 전략 (패턴별 노드 매핑, 단계별 절차, 프롬프트 패턴, 검증 체크리스트)
12. Claude Code로 n8n 워크플로우 개발 (개발 플로우, JSON Import/Export, 실전 예시, 트러블슈팅)

문서 하단 구성:
- 문의 사항 및 피드백용 이메일(20eung@gmail.com)을 포함하라.
- MIT License 섹션을 추가하라.

문서의 톤앤매너:
- AI 코딩을 처음 접하는 사람도 따라 하기 쉽게 단계별로 설명하라.
- PART 1은 특히 간결하고 친절하게 — 초보자가 압도되지 않도록 불필요한 심화 내용을 제외하라.
- 가독성을 위해 마크다운 헤더, 불릿 포인트, 테이블을 적절히 활용하라.
```

---
**업데이트 이력**:
- 2026-03-18: 최종 고도화 (보안 설정, 리모트 접속 및 릴리즈 자동화 흐름 반영)
- 2026-03-24: Docker/n8n 환경, n8n-MCP+Skills, Python→n8n 마이그레이션 전략 추가 (섹션 8~12)
- 2026-03-24: 초보자 친화적 구조 개편 — 3-PART 2단계 구조, Antigravity 진입점 전환 (v1.3.0)
