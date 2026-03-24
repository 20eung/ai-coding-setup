# PROMPT for AI Coding Environment Setup

이 프롬프트는 어떤 AI 어시스턴트를 사용하여도 일관된 PDCA AI 코딩 개발환경 구성 가이드를 생성하도록 설계되었습니다.

---

### AI 프롬프트 원문

```text
역할: 시니어 데브옵스 엔지니어 및 테크니컬 라이터

목표: MacOS, Linux, Windows 사용자를 위한 **Professional Standard** 'AI Coding 개발환경 구성' README.md 문서를 작성하라.

제약 조건:
1. 언어는 한국어로 작성하되, 전문 용어는 영어 원문을 병기하라.
2. 모든 명령어는 복사하여 붙여넣기 가능한 코드 블록으로 제공하라.
3. 운영체제별 설정 차이를 명확히 구분하여 설명하라.
4. **시각적 요소 강화**: 상단에 프로젝트 배너(`docs/assets/banner.png`)와 Shields.io 뱃지(Version, Node, Python, License)를 포함하라.
5. **가독성 최적화**: Key Features와 Quick Start 섹션을 상단에 배치하고, 클릭 가능한 목차(TOC)를 제공하라.

포함 내용:
1. 사전 준비 사항 (Node.js, Python, Git 등 기본 요구사항)
2. SSH 및 Git 기본 설정 가이드 (Git config global 설정/확인, id_rsa 생성 및 파일 설명, GitHub SSH 키 등록 및 연결 확인 방법, ~/.ssh/config 및 리모트 서버 authorized_keys 설정법)
3. Gemini CLI 설치 및 설정 방법 (npm 설치, Google AI Studio API 발급 및 멀티 계정 환경변수 관리 방법 포함)
4. Claude Code 설치 및 설정 방법 (npm 설치, .aws 디렉토리 기반 보안 인증 설정, 필수 환경변수(CLAUDE_CODE_USE_BEDROCK, AWS_REGION 등) 및 선택적 모델 지정 포함)
5. Antigravity 설치 및 설정 (설치 가이드, 필수 VS Code 확장 프로그램(Remote-SSH, Claude Code for VS Code 등), 리모트 서버 접속 방법, 터미널 대화형 CLI(Gemini/Claude) 활용 및 확장 프로그램 UI 사용법 포함)
6. GitHub 연동 및 자동화 (GitHub CLI(gh) 설치 및 인증, AI 기반 자동화 릴리즈 가이드)
7. bkit 설치 (Claude Code 플러그인 마켓플레이스 활용 및 Gemini CLI 익스텐션 설치 방법 포함)
8. Docker 환경 구성 (MacOS/Linux/Windows Docker Desktop 설치, docker-compose.yml 구조 해설, .env 파일 분리 보안 관리)
9. n8n 컨테이너 설치 및 실행 ('n8n이란' 및 Python 데몬 대비 n8n의 장점 설명, docker compose 명령어 모음, n8n API Key 발급 및 MCP 연동 준비)
10. n8n-MCP + n8n-skills 설정 (AI에 n8n 1,239개 노드 지식 주입, .mcp.json 설정, 7가지 스킬 설치 및 역할 소개)
11. Python → n8n 마이그레이션 전략 (Python 패턴별 n8n 노드 매핑 테이블, 단계별 절차, Claude Code 활용 프롬프트 패턴, 마이그레이션 검증 체크리스트)
12. Claude Code로 n8n 워크플로우 개발 (권장 개발 플로우, JSON Import/Export 방법, Python 데몬 → n8n 실전 예시, 트러블슈팅 가이드)

문서 하단 구성:
- 문의 사항 및 피드백용 이메일(20eung@gmail.com)을 포함하라.
- MIT License 섹션을 추가하라.

문서의 톤앤매너:
- 전문적이면서도 초보자가 따라 하기 쉽게 단계별로 설명하라.
- 가독성을 위해 마크다운 헤더, 불릿 포인트, 테이블을 적절히 활용하라.
```

---
**업데이트 이력**:
- 2026-03-18: 최종 고도화 (보안 설정, 리모트 접속 및 릴리즈 자동화 흐름 반영)
- 2026-03-24: Docker/n8n 환경, n8n-MCP+Skills, Python→n8n 마이그레이션 전략 추가 (섹션 8~12)
