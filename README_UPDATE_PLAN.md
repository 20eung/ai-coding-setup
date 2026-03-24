# 📋 README.md 업데이트 계획서

> **상태**: ✅ Do 단계 완료 (2026-03-24)

## 미션 요약

> **기존에 바이브 코딩으로 만들어진 Python 코드 및 서비스 데몬들을 n8n 워크플로우로 마이그레이션한다.**
> 팀원들이 이 문서를 따라 환경을 구성하고, Claude Code + n8n-MCP + n8n-skills를 활용하여
> Python 서비스를 n8n으로 옮길 수 있도록 가이드한다.

---

## 추가 섹션 목록 (기존 7개 → 12개)

| 섹션 | 제목 | 상태 |
|------|------|------|
| 8 | Docker 환경 구성 | ⬜ 작성 예정 |
| 9 | n8n 컨테이너 설치 및 실행 | ⬜ 작성 예정 |
| 10 | n8n-MCP + n8n-skills 설정 | ⬜ 작성 예정 |
| 11 | Python → n8n 마이그레이션 전략 | ⬜ 작성 예정 |
| 12 | Claude Code로 n8n 워크플로우 개발 | ⬜ 작성 예정 |

---

## 섹션별 상세 계획

### 섹션 8. Docker 환경 구성

**목적**: n8n을 컨테이너로 실행하기 위한 Docker 환경 기반 마련

**8.1 Docker Desktop 설치**
- MacOS: `brew install --cask docker`
- Linux: `apt install docker.io docker-compose`
- Windows: Docker Desktop 공식 설치 파일 링크
- 설치 확인: `docker --version`, `docker compose version`

**8.2 docker-compose.yml 구조 이해**
- 핵심 구성 요소 설명 (services, volumes, networks, ports, environment)
- n8n용 `docker-compose.yml` 예시 전문 제공
- 각 항목 주석 설명

**8.3 .env 파일 분리 관리**
- `.env` 파일 생성 (N8N_HOST, N8N_PORT, WEBHOOK_URL, DB 설정 등)
- `.gitignore`에 `.env` 추가 (보안 필수)
- `docker-compose.yml`에서 `env_file` 또는 `${VAR}` 참조 방법

---

### 섹션 9. n8n 컨테이너 설치 및 실행

**목적**: n8n을 실제로 실행하고 팀이 접근 가능한 상태로 만들기

**9.1 n8n이란?**
- 오픈소스 워크플로우 자동화 툴 (Zapier/Make의 셀프호스팅 대안)
- **왜 Python 데몬 대신 n8n인가?** → 핵심 설득 포인트
  - GUI 기반 시각화로 유지보수 편의성 극대화
  - 오류 발생 시 웹 UI에서 즉시 재실행/디버깅 가능
  - 알림(슬랙/메일), API 연동 노드 내장
  - Claude Code가 JSON으로 직접 워크플로우 생성 가능

**9.2 docker-compose로 n8n 실행**
```bash
docker compose up -d         # 백그라운드 실행
docker compose down          # 중지
docker compose logs -f n8n   # 실시간 로그
docker compose restart n8n   # 재시작
```

**9.3 웹 UI 접속 확인**
- 로컬: `http://localhost:5678`
- 원격 서버: `http://<서버IP>:5678`
- 초기 계정 설정 방법

**9.4 n8n API 설정 (MCP 연동 준비)**
- n8n 웹 UI에서 API Key 발급 방법
- `N8N_API_KEY` 환경변수에 저장
- API 동작 확인: `curl http://localhost:5678/api/v1/workflows`

---

### 섹션 10. n8n-MCP + n8n-skills 설정

**목적**: Claude Code가 n8n 노드를 정확히 알고 워크플로우를 생성하도록 AI 지식 주입

**참고 링크**:
- n8n-MCP: https://github.com/czlonkowski/n8n-mcp
- n8n-skills: https://github.com/czlonkowski/n8n-skills

**10.1 n8n-MCP란?**
- AI 어시스턴트에게 n8n 1,239개 노드 문서를 제공하는 MCP 서버
- 이것 없이는 Claude Code가 n8n 노드 속성을 '추측'으로 생성 → 오류 빈발
- n8n 관리 API 연동 시 워크플로우 직접 생성/수정/배포까지 자동화 가능

**10.2 n8n-MCP 설치 방법 3가지**
- **Option A (권장, 팀 공용)**: Hosted Service — `dashboard.n8n-mcp.com` 가입 후 API Key 발급 (무료 100 calls/day)
- **Option B (개인 로컬)**: npx 실행
  ```bash
  npx n8n-mcp
  ```
- **Option C (자체 호스팅)**: Docker로 n8n과 함께 실행

**10.3 Claude Code에 MCP 연동**
- `.mcp.json` 파일 생성 위치 및 설정 예시
- Hosted Service 연동 예시:
  ```json
  {
    "mcpServers": {
      "n8n": {
        "command": "npx",
        "args": ["-y", "n8n-mcp"],
        "env": {
          "N8N_MCP_API_KEY": "your_hosted_api_key"
        }
      }
    }
  }
  ```
- 동작 확인 방법

**10.4 n8n-skills란? (7가지 스킬)**

| # | 스킬명 | 역할 |
|---|--------|------|
| 1 | Expression Syntax | `{{$json.body}}` 등 표현식 작성법 |
| 2 | MCP Tools Expert (최우선) | 어떤 MCP 도구를 언제 쓸지 판단 |
| 3 | Workflow Patterns | 5가지 검증된 워크플로우 패턴 |
| 4 | Validation Expert | 오류 해석 및 수정 가이드 |
| 5 | Node Configuration | 노드 속성 의존성 설정 |
| 6 | Code JavaScript | Code 노드에서 JS 작성법 |
| 7 | Code Python | Code 노드에서 Python 작성법 (제한사항 포함) |

**10.5 n8n-skills Claude Code 설치**
```bash
# 방법 1: 플러그인 명령어 (권장)
/plugin install czlonkowski/n8n-skills

# 방법 2: 수동 설치
git clone https://github.com/czlonkowski/n8n-skills.git
cp -r n8n-skills/skills/* ~/.claude/skills/
```

---

### 섹션 11. Python → n8n 마이그레이션 전략

**목적**: Python 서비스를 n8n으로 옮기기 위한 체계적 접근법 제공

**11.1 마이그레이션 대상 유형 분류**

| Python 패턴 | n8n 대응 노드 | 난이도 |
|---|---|---|
| `schedule` / `cron` 데몬 | Schedule Trigger | 🟢 쉬움 |
| `requests.get/post()` | HTTP Request | 🟢 쉬움 |
| `if / for` 로직 | IF / Switch / Loop Over Items | 🟡 보통 |
| `json` 파싱 / 데이터 변환 | Set, Code (JS) | 🟡 보통 |
| `subprocess` / 쉘 명령 | Execute Command | 🟡 보통 |
| DB 쿼리 (`psycopg2`, `pymysql`) | Postgres / MySQL 노드 | 🟡 보통 |
| 슬랙/메일 알림 | Slack / Gmail / Email 노드 | 🟢 쉬움 |
| 파일 읽기/쓰기 | Read/Write Binary File | 🟡 보통 |
| Webhook 수신 서버 (`Flask`, `FastAPI`) | Webhook Trigger | 🔴 주의 필요 |
| 복잡한 비즈니스 로직 | Code 노드 (JS/Python) | 🔴 주의 필요 |

**11.2 마이그레이션 단계별 절차**
1. Python 코드 분석 → 트리거/처리/출력 3단계로 분해
2. 트리거 유형 파악 (스케줄? Webhook? 수동?)
3. Claude Code에게 마이그레이션 요청
4. n8n 웹 UI에서 JSON Import 후 테스트
5. 기존 Python 결과와 n8n 결과 비교 검증
6. Python 데몬(systemd) 비활성화 및 n8n 워크플로우 활성화

**11.3 Claude Code에게 마이그레이션 요청하는 법**

효과적인 프롬프트 패턴:
```
다음 Python 스크립트를 n8n 워크플로우 JSON으로 변환해줘.

[Python 코드 붙여넣기]

요구사항:
- 트리거: 매일 오전 9시 실행
- n8n-MCP 도구를 사용해서 정확한 노드 속성으로 생성
- n8n 버전: 1.x (self-hosted)
- 결과를 슬랙 #알림 채널로 전송
```

**11.4 마이그레이션 검증 체크리스트**
- [ ] 트리거 타이밍이 동일한가?
- [ ] HTTP 요청 헤더/바디가 동일한가?
- [ ] 데이터 변환 결과가 동일한가?
- [ ] 오류 발생 시 알림이 오는가?
- [ ] n8n 실행 로그에 오류 없음 확인

---

### 섹션 12. Claude Code로 n8n 워크플로우 개발

**목적**: MCP + Skills를 결합한 실전 개발 워크플로우 가이드

**12.1 권장 개발 플로우**
```
Python 코드 파악
    ↓
Claude Code에 마이그레이션 요청 (n8n-MCP + skills 활성화 상태)
    ↓
생성된 JSON을 n8n 웹 UI에서 Import
    ↓
테스트 실행 → 오류 발생 시 Claude Code에 오류 로그 전달
    ↓
수정 → 재Import → 검증
    ↓
기존 Python 데몬 비활성화 → n8n 워크플로우 활성화
```

**12.2 워크플로우 JSON Import/Export**
- Export: n8n 웹 UI → 워크플로우 → ⋮ → Download
- Import: n8n 웹 UI → 워크플로우 → Import from File

**12.3 실전 예시: Python 데몬 → n8n 워크플로우**
- 예시 선정: 매 시간 특정 API를 호출하여 결과를 DB에 저장하고 Slack 알림 전송하는 Python 스크립트
- Before: Python 코드 전문
- After: n8n 워크플로우 JSON (Claude Code 생성)
- 비교 분석

**12.4 트러블슈팅**
- `$json.body`와 `$json` 혼용 오류
- 인증 토큰 만료 처리
- Loop 노드에서 배치 처리 오류
- Code 노드 Python 외부 라이브러리 미지원 우회법

---

## 작업 순서 (체크리스트)

- [x] 목차 업데이트 (기존 README 내 `## 📑 목차` 섹션에 8~12 추가)
- [x] 섹션 8 작성 및 추가
- [x] 섹션 9 작성 및 추가
- [x] 섹션 10 작성 및 추가
- [x] 섹션 11 작성 및 추가
- [x] 섹션 12 작성 및 추가
- [x] PROMPT.md 업데이트
- [x] GitHub 업로드 (v1.2.0 릴리즈 완료)

---

## 참고 링크

- [n8n-MCP GitHub](https://github.com/czlonkowski/n8n-mcp)
- [n8n-skills GitHub](https://github.com/czlonkowski/n8n-skills)
- [n8n 공식 문서](https://docs.n8n.io)
- [n8n Docker 설치 가이드](https://docs.n8n.io/hosting/installation/docker/)
