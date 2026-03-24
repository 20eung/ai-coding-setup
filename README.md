<p align="center">
  <img src="docs/assets/banner.png" alt="AI Coding Setup Banner" width="100%">
</p>

# 🚀 AI Coding Setup

이 프로젝트는 **MacOS, Linux, Windows** 환경에서 최첨단 AI 개발 도구들을 결합하여 생산성을 극대화하는 **AI-Native 개발 환경**을 구축하는 가이드입니다.

<p align="center">
  <img src="https://img.shields.io/badge/version-1.2.1-blue.svg" alt="Version">
  <img src="https://img.shields.io/badge/Node.js-18%2B-green.svg" alt="Node.js">
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue.svg" alt="Python">
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License">
</p>

---

## ✨ Key Features

- 🧠 **Triple AI Integration**: Gemini CLI, Claude Code, Antigravity의 장점을 결합한 통합 워크플로우
- 🛡️ **Security First**: API 키 노출을 방지하는 보안 설정 가이드 (AWS Bedrock, Environment Variables)
- ⚙️ **Optimized Remote Dev**: SSH와 Remote-Explorer를 활용한 고성능 원격 서버 개발 환경
- 🤖 **PDCA Automation**: AI를 활용한 릴리즈 노트 생성 및 태그 자동화 배포 시스템
- 🔌 **bkit Powered**: `bkit.ai` 플러그인을 통한 AI 네이티브 기능 확장

## ⚡ Quick Start

가장 빠르게 환경을 구성하는 3단계 핵심 과정입니다.

1.  **기본 도구 설치**: `Node.js`, `Python`, `Git`, `gh` 설치
2.  **API 인증**: Google AI Studio, AWS Bedrock API 키 준비 및 환경 설정
3.  **에이전트 활성화**: Antigravity, Claude Code, Gemini CLI의 Interactive Shell 실행

---

## 📑 목차

1. [사전 준비 사항](#1-사전-준비-사항-prerequisites)
2. [SSH 및 Git 기본 설정](#2-ssh-및-git-기본-설정)
   - [2.1 Git 사용자 정보 설정](#21-git-사용자-정보-설정)
   - [2.2 SSH 키 생성](#22-ssh-키-생성-sshid_rsa)
   - [2.3 GitHub에 SSH 키 등록](#23-github에-ssh-키-등록)
   - [2.4 SSH 연결 확인](#24-ssh-연결-확인)
   - [2.5 SSH Config 설정](#25-ssh-config-설정-sshconfig)
   - [2.6 리모트 서버 설정](#26-리모트-서버-설정)
3. [Gemini CLI 설치 및 설정](#3-gemini-cli-설치-및-설정)
   - [3.1 설치](#31-설치)
   - [3.2 API 설정](#32-api-설정)
4. [Claude Code 설치 및 설정](#4-claude-code-설치-및-설정)
   - [4.1 설치](#41-설치)
   - [4.2 AWS Bedrock 연동](#42-aws-bedrock-연동)
     - [AWS Bedrock이란?](#aws-bedrock이란)
     - [주요 특징](#주요-특징)
     - [Claude Code에서 Bedrock을 사용하는 장점](#claude-code에서-bedrock을-사용하는-장점)
   - [4.3 프로젝트 컨텍스트 설정 (CLAUDE.md)](#43-프로젝트-컨텍스트-설정-claudemd)
5. [Antigravity 설치 및 설정](#5-antigravity-설치-및-설정)
   - [5.1 설치](#51-설치)
   - [5.2 확장 프로그램](#52-확장-프로그램)
   - [5.3 리모트 서버 접속방법](#53-리모트-서버-접속방법)
   - [5.4 터미널 활용법](#54-터미널-활용법)
   - [5.5 Claude Code 확장프로그램 사용법](#55-claude-code-확장프로그램-사용법)
6. [GitHub 연동 및 자동화](#6-github-연동-및-자동화)
   - [6.1 GitHub CLI (gh) 설치 및 설정](#61-github-cli-gh-설치-및-설정)
   - [6.2 AI를 활용한 릴리즈 자동화](#62-ai를-활용한-릴리즈-자동화)
7. [bkit 설치](#7-bkit-설치)
   - [7.1 Claude Code에서 설치](#71-claude-code에서-설치)
   - [7.2 Gemini CLI에서 설치](#72-gemini-cli에서-설치)
8. [Docker 환경 구성](#8-docker-환경-구성)
   - [8.1 Docker Desktop 설치](#81-docker-desktop-설치)
   - [8.2 docker-compose.yml 구조 이해](#82-docker-composeyml-구조-이해)
   - [8.3 .env 파일 분리 관리](#83-env-파일-분리-관리)
9. [n8n 컨테이너 설치 및 실행](#9-n8n-컨테이너-설치-및-실행)
   - [9.1 n8n이란?](#91-n8n이란)
   - [9.2 docker-compose로 n8n 실행](#92-docker-compose로-n8n-실행)
   - [9.3 웹 UI 접속 확인](#93-웹-ui-접속-확인)
   - [9.4 n8n API 설정](#94-n8n-api-설정-mcp-연동-준비)
10. [n8n-MCP + n8n-skills 설정](#10-n8n-mcp--n8n-skills-설정)
    - [10.1 n8n-MCP란?](#101-n8n-mcp란)
    - [10.2 n8n-MCP 설치](#102-n8n-mcp-설치)
    - [10.3 Claude Code에 MCP 연동](#103-claude-code에-mcp-연동)
    - [10.4 n8n-skills란?](#104-n8n-skills란)
    - [10.5 n8n-skills 설치](#105-n8n-skills-설치)
11. [Python → n8n 마이그레이션 전략](#11-python--n8n-마이그레이션-전략)
    - [11.1 마이그레이션 대상 유형 분류](#111-마이그레이션-대상-유형-분류)
    - [11.2 마이그레이션 단계별 절차](#112-마이그레이션-단계별-절차)
    - [11.3 Claude Code에게 마이그레이션 요청하는 법](#113-claude-code에게-마이그레이션-요청하는-법)
    - [11.4 마이그레이션 검증 체크리스트](#114-마이그레이션-검증-체크리스트)
12. [Claude Code로 n8n 워크플로우 개발](#12-claude-code로-n8n-워크플로우-개발)
    - [12.1 권장 개발 플로우](#121-권장-개발-플로우)
    - [12.2 워크플로우 JSON Import/Export](#122-워크플로우-json-importexport)
    - [12.3 실전 예시](#123-실전-예시-python-데몬--n8n-워크플로우)
    - [12.4 트러블슈팅](#124-트러블슈팅)

---

## 1. 사전 준비 사항 (Prerequisites)

각 도구의 설치 및 실행을 위해 다음 프로그램이 미리 설치되어 있어야 합니다.

- **Node.js & npm**: [Node.js 공식 홈페이지](https://nodejs.org/)에서 LTS 버전을 권장합니다.
- **Python**: [Python 공식 홈페이지](https://www.python.org/)에서 3.10 이상의 버전을 권장합니다.
- **Git**: [Git 공식 홈페이지](https://git-scm.com/)에서 설치 가능합니다.
- **GitHub CLI (gh)**: [GitHub CLI 공식 홈페이지](https://cli.github.com/)에서 설치 가능합니다. AI 에이전트의 PR/릴리즈 자동화에 필수입니다. (6.1절 참고)

---

## 2. SSH 및 Git 기본 설정

인증 및 사용자 식별을 위한 기본 설정입니다.

### 2.1 Git 사용자 정보 설정

로컬 환경에서 커밋 시 사용할 사용자 정보를 전역(Global)으로 설정합니다.

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"

# 설정 확인
git config --list
```

### 2.2 SSH 키 생성 (~/.ssh/id_rsa)

터미널(또는 PowerShell)에서 다음 명령어를 입력하여 키를 생성합니다.

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- 경로 요청 시 기본값(Enter)을 선택합니다.
- Passphrase(비밀번호)는 공란으로 두거나 본인이 기억할 수 있는 비밀번호를 입력합니다.

**생성되는 파일 (~/.ssh/):**

- **`id_rsa`**: 개인키 (Private Key). 절대 외부에 노출되어선 안 되며 본인 컴퓨터에만 보관합니다.
- **`id_rsa.pub`**: 공개키 (Public Key). GitHub 등 외부 서비스에 등록할 때 사용합니다.

### 2.3 GitHub에 SSH 키 등록

생성한 공개키(`id_rsa.pub`)를 GitHub 계정에 등록해야 인증이 완료됩니다.

1. **공개키 복사**:
   - **MacOS/Linux**: `cat ~/.ssh/id_rsa.pub`
   - **Windows**: `type $HOME\.ssh\id_rsa.pub`
   - 출력된 문자열(ssh-rsa...로 시작)을 모두 복사합니다.
2. **GitHub 접속**: [GitHub Settings > SSH and GPG keys](https://github.com/settings/keys)로 이동합니다.
3. **새 키 등록**: 'New SSH key' 버튼을 클릭합니다.
4. **정보 입력**: Title에 기기 이름(예: MyMacbook)을 적고, Key 필드에 복사한 내용을 붙여넣은 후 'Add SSH key'를 클릭합니다.

### 2.4 SSH 연결 확인

설정이 완료되었는지 터미널에서 다음 명령어로 확인합니다.

```bash
ssh -T git@github.com
```

- "Hi username! You've successfully authenticated..." 메시지가 나오면 성공입니다.
- 처음 접속 시 "Are you sure you want to continue connecting (yes/no/[fingerprint])?" 문구가 나오면 `yes`를 입력합니다.

### 2.5 SSH Config 설정 (~/.ssh/config)

원격 접속을 편리하게 하기 위해 파일을 생성하거나 수정합니다.

**MacOS/Linux:** `nano ~/.ssh/config`
**Windows:** `notepad $HOME\.ssh\config`

```text
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

Host server_alias
  HostName 123.456.78.90
  User your_user_id
  IdentityFile ~/.ssh/id_rsa
```

### 2.6 리모트 서버 설정

SSH Config에 등록한 리모트 서버(`server_alias`)에 비밀번호 없이 접속하려면, 로컬의 공개키를 서버에 등록해야 합니다.

1. **서버 접속**: 처음에는 비밀번호를 사용하여 서버에 접속합니다.
   ```bash
   ssh your_user_id@123.456.78.90
   ```
2. **`.ssh` 디렉토리 생성 및 권한 설정**:
   ```bash
   mkdir -p ~/.ssh
   chmod 700 ~/.ssh
   ```
3. **공개키 등록**: 로컬의 `id_rsa.pub` 내용을 서버의 `~/.ssh/authorized_keys` 파일에 추가합니다.
   ```bash
   # (서버에서 실행)
   echo "복사한_공개키_내용" >> ~/.ssh/authorized_keys
   chmod 600 ~/.ssh/authorized_keys
   ```
4. **간편 접속 확인**: 이제 로컬 터미널에서 비밀번호 없이 접속되는지 확인합니다.
   ```bash
   ssh server_alias
   ```

---

## 3. Gemini CLI 설치 및 설정

### 3.1 설치

Google의 Gemini 모델을 터미널에서 직접 사용할 수 있는 CLI 도구입니다.

```bash
# npm을 이용한 전역 설치
npm install -g @google/gemini-cli
```

> [!NOTE]
> `@google/generative-ai`는 Node.js용 클라이언트 **SDK** 패키지입니다. 터미널에서 직접 사용하는 **CLI 도구**는 `@google/gemini-cli`로 별도 패키지입니다.

### 3.2 API 설정

#### 3.2.1 Google AI Studio에서 API 발급

1. [Google AI Studio](https://aistudio.google.com/)에 접속합니다.
2. 'Get API key' 버튼을 클릭합니다.
3. 새로운 API Key를 생성하고 안전하게 복사해 둡니다.

#### 3.2.2 여러 계정 관리 및 환경변수 설정

여러 Google 계정의 API 키를 상황에 따라 변경하며 사용하려면 환경변수를 관리해야 합니다.

**MacOS/Linux (.zshrc 또는 .bashrc):**

```bash
# 계정 1
export GEMINI_API_KEY_WORK="your_work_api_key"
# 계정 2
export GEMINI_API_KEY_PERSONAL="your_personal_api_key"

# 현재 사용할 키 선택 (alias 등록)
alias set-gemini-work='export GEMINI_API_KEY=$GEMINI_API_KEY_WORK'
alias set-gemini-personal='export GEMINI_API_KEY=$GEMINI_API_KEY_PERSONAL'
```

**Windows (PowerShell Profile):**

```powershell
$env:GEMINI_API_KEY_WORK = "your_work_api_key"
$env:GEMINI_API_KEY_PERSONAL = "your_personal_api_key"

function Set-GeminiWork { $env:GEMINI_API_KEY = $env:GEMINI_API_KEY_WORK }
function Set-GeminiPersonal { $env:GEMINI_API_KEY = $env:GEMINI_API_KEY_PERSONAL }
```

---

## 4. Claude Code 설치 및 설정

### 4.1 설치

Anthropic의 Claude 4.6 기반 코딩 어시스턴트인 Claude Code를 설치합니다.

```bash
# npm을 이용한 설치
npm install -g @anthropic-ai/claude-code
```

### 4.2 AWS Bedrock 연동

#### AWS Bedrock이란?

**AWS Bedrock**은 Amazon Web Services(AWS)에서 제공하는 완전관리형 생성형 AI 서비스입니다. Anthropic(Claude), Meta(Llama), Amazon(Titan), Cohere, Stability AI 등 다양한 AI 기업의 파운데이션 모델(Foundation Model)을 **단일 API**로 접근할 수 있습니다.

#### 주요 특징

| 특징 | 설명 |
|---|---|
| **완전관리형** | 서버/인프라 관리 불필요. AWS가 모든 운영 부담을 처리 |
| **다양한 모델** | Claude, Llama, Titan, Cohere 등 여러 최신 모델을 하나의 API로 사용 |
| **데이터 보안** | 사용자 데이터가 모델 학습에 사용되지 않음. VPC 내 트래픽 유지 가능 |
| **엔터프라이즈 규정 준수** | SOC 2, HIPAA, GDPR 등 주요 보안 인증 준수 |
| **IAM 통합** | AWS IAM으로 세밀한 접근 권한 제어. 정적 API 키 대신 역할 기반 인증 |
| **사용량 기반 과금** | 호출한 만큼만 비용 발생. AWS 통합 청구로 비용 관리 편리 |
| **멀티리전 지원** | 특정 리전에 데이터를 유지해야 하는 규정 준수 요구사항 충족 |

#### Claude Code에서 Bedrock을 사용하는 장점

- **비용 관리**: AWS Organizations의 통합 청구(Consolidated Billing)를 통해 팀/기업 단위 비용 추적 용이
- **보안 강화**: Anthropic API 키를 코드나 환경변수에 노출하지 않아도 됨. IAM 역할로 인증
  - **정적 키 제거**: Anthropic 직접 API는 `sk-ant-xxxxx` 형태의 고정 키를 `.env` 파일이나 환경변수에 보관해야 하지만, Bedrock은 이런 키 자체가 없음
  - **임시 자격증명**: AWS IAM이 단기 만료 토큰(STS)을 자동 발급·갱신. 키가 탈취되어도 짧은 시간 후 무효화
  - **최소 권한 원칙**: IAM 정책으로 "Bedrock의 특정 모델만 호출 가능" 수준으로 권한을 세밀하게 제한 가능
  - **키 유출 위험 제거**: 실수로 API 키를 GitHub에 커밋하거나 로그에 출력하는 사고를 구조적으로 방지
  - **서버/컨테이너 자동 인증**: EC2 인스턴스 프로파일, ECS 태스크 역할, Lambda 실행 역할 등을 통해 코드에 자격증명을 기입하지 않아도 자동 인증
- **데이터 거주(Data Residency)**: 특정 AWS 리전 내에서만 데이터가 처리되어 국내 규정 준수 가능
- **네트워크 격리**: AWS PrivateLink를 통해 인터넷을 경유하지 않고 AWS 내부 네트워크로만 통신
- **감사 로그**: AWS CloudTrail로 모든 API 호출 기록 자동 저장
- **기존 AWS 자산 활용**: 이미 AWS 계정이 있는 조직은 별도 계정 없이 즉시 사용 가능

> [!NOTE]
> 개인 사용자나 빠른 테스트 목적이라면 [Anthropic 직접 API](https://console.anthropic.com/)가 더 간편합니다. Bedrock은 보안, 규정 준수, 비용 통합이 중요한 **팀/기업 환경**에 특히 적합합니다.

---

Claude Code에서 AWS Bedrock을 백엔드로 사용하려면 적절한 권한 설정이 필요합니다. 환경변수에 직접 키를 노출하는 대신, AWS CLI 표준 방식인 `.aws` 디렉토리의 설정 파일을 사용하는 것이 보안상 더 안전합니다.

#### 4.2.1 AWS 인증 정보 설정

**MacOS/Linux:**

```bash
mkdir -p ~/.aws
cat <<EOF > ~/.aws/config
[default]
region = ap-northeast-2
output = json
EOF

cat <<EOF > ~/.aws/credentials
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
EOF

chmod 600 ~/.aws/*
chmod 700 ~/.aws
```

**Windows (PowerShell):**

```powershell
New-Item -ItemType Directory -Force -Path $env:USERPROFILE\.aws
@'
[default]
region = ap-northeast-2
output = json
'@ | Set-Content -Path $env:USERPROFILE\.aws\config

@'
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
'@ | Set-Content -Path $env:USERPROFILE\.aws\credentials
```

#### 4.2.2 Claude 환경변수 및 실행

Claude Code가 Bedrock을 사용하도록 필수 환경변수를 설정하고 실행합니다.

**MacOS/Linux:**

```bash
# Bedrock 활성화 및 리전 설정 (필수)
export CLAUDE_CODE_USE_BEDROCK=1
export AWS_REGION="ap-northeast-2" # Bedrock 모델 권한을 받은 리전

# (선택) 사용할 모델 명시적 지정
# AWS Bedrock 모델 ID 형식은 사용 방식에 따라 다릅니다:
#   일반 리전:            anthropic.claude-sonnet-4-5-20251001-v1:0
#   Cross-Region (미국):  us.anthropic.claude-sonnet-4-5-20251001-v1:0
#   글로벌 (커스텀 설정): global.anthropic.claude-sonnet-4-6
# export ANTHROPIC_MODEL="us.anthropic.claude-sonnet-4-5-20251001-v1:0"

# Claude Code 실행
claude
```

**Windows (PowerShell):**

```powershell
setx CLAUDE_CODE_USE_BEDROCK "1"
setx AWS_REGION "ap-northeast-2"

# (선택) 사용할 모델 명시적 지정 (형식은 위 MacOS/Linux 주석 참고)
# setx ANTHROPIC_MODEL "us.anthropic.claude-sonnet-4-5-20251001-v1:0"
```


> [!TIP]
> 더 자세한 설정 방법은 [claude-code-use-bedrock](https://github.com/20eung/claude-code-use-bedrock) 문서를 참고하세요.

### 4.3 프로젝트 컨텍스트 설정 (CLAUDE.md)

Claude Code는 프로젝트 루트의 `CLAUDE.md` 파일을 자동으로 읽어 프로젝트 특화 컨텍스트를 AI에게 제공합니다. 세션이 바뀌어도 일관된 작업 방식을 유지할 수 있습니다.

```bash
# 프로젝트 루트에 CLAUDE.md 생성 후 아래 샘플 내용을 붙여넣고 환경에 맞게 수정하세요
touch CLAUDE.md
```

> [!TIP]
> 전역 설정은 `~/.claude/CLAUDE.md`에, 프로젝트별 설정은 프로젝트 루트의 `CLAUDE.md`에 작성합니다. 프로젝트 파일이 전역 파일보다 우선 적용됩니다.

**Python → n8n 마이그레이션 프로젝트용 `CLAUDE.md` 샘플:**

```markdown
# Python → n8n 마이그레이션 프로젝트

## 미션 개요
기존 바이브 코딩으로 작성된 Python 데몬/스크립트를 n8n 워크플로우로 전면 이전합니다.
코드의 품질보다 **동작의 동일성**을 최우선 목표로 합니다.

## 환경 정보
- n8n 버전: 1.x (self-hosted)
- n8n 접속 주소: http://localhost:5678  ← 실제 주소로 수정
- n8n API Key: (`.env` 파일의 `N8N_API_KEY` 참고)
- Python 소스 위치: `./scripts/`  ← 실제 경로로 수정
- 완료된 워크플로우 JSON 저장 위치: `./workflows/`

## 사용 가능한 MCP 도구
n8n-MCP가 활성화되어 있습니다. 워크플로우 생성 시 반드시 아래 순서로 진행하세요:
1. `search_nodes`로 필요한 노드를 검색
2. `get_node` 또는 `get_node_details`로 노드 속성을 정확히 확인
3. `validate_workflow`로 생성된 JSON 유효성 검사
4. `create_workflow` 또는 `update_workflow`로 n8n에 직접 배포

## 마이그레이션 규칙
- Python 코드를 분석할 때: 바이브 코딩 특성상 중복/불필요 코드가 있을 수 있습니다.
  로직의 **핵심 흐름(트리거 → 처리 → 출력)**만 파악해서 n8n으로 옮기세요.
- 외부 라이브러리 의존성(`requests`, `pandas` 등)은 n8n 내장 노드로 대체합니다.
- 복잡한 로직은 n8n Code 노드(JavaScript)로 이식합니다. Python 외부 라이브러리는 사용 불가합니다.
- 오류 처리: 모든 워크플로우에 Error Trigger 노드를 연결하고 Slack `#errors` 채널로 알림을 보냅니다.

## 워크플로우 네이밍 규칙
`[트리거유형] 원본파일명 - 설명`
예시:
- `[SCHEDULE] check_api_status - API 상태 10분마다 확인`
- `[WEBHOOK] receive_order - 주문 수신 처리`
- `[MANUAL] data_cleanup - 수동 데이터 정리`

## 완료 기준 체크리스트
마이그레이션이 완료되었다고 판단하려면 다음을 모두 충족해야 합니다:
- [ ] n8n 웹 UI에서 테스트 실행 성공
- [ ] 기존 Python 결과값과 n8n 결과값 일치 확인
- [ ] 오류 발생 시 Slack 알림 정상 작동 확인
- [ ] 워크플로우 JSON을 `./workflows/` 에 저장하고 Git 커밋

## 작업 시 주의사항
- n8n에 워크플로우를 배포하기 전 반드시 `validate_workflow`를 실행하세요.
- Python 데몬을 비활성화하기 전, n8n 워크플로우를 Active 상태로 먼저 전환하세요.
- 기존 Python 스크립트는 삭제하지 말고 `./scripts/archived/`로 이동하세요.

## 답변 언어
모든 설명과 주석은 한국어로 작성합니다.
```

---

## 5. Antigravity 설치 및 설정

### 5.1 설치

Antigravity는 강력한 AI 코딩 에이전트 환경입니다. 별도의 설치 과정 없이 지원되는 환경에서 즉시 사용 가능하거나, 전용 클라이언트를 통해 구동됩니다.

### 5.2 확장 프로그램

VS Code와 함께 사용하면 효과가 극대화됩니다.

| 확장 프로그램 | 마켓플레이스 ID | 용도 |
|---|---|---|
| **Remote-SSH** | `ms-vscode-remote.remote-ssh` | 리모트 서버 접속 및 파일 편집 (원격 탐색기 포함) |
| **Claude Code for VS Code** | `anthropic.claude-code` | VS Code 내에서 Claude 기능 직접 사용 |
| **Korean Language Pack** | `ms-ceintl.vscode-language-pack-ko` | 한국어 메뉴 구성 |

VS Code 확장 마켓플레이스에서 ID로 검색하거나, 터미널에서 다음과 같이 설치할 수 있습니다:
```bash
code --install-extension ms-vscode-remote.remote-ssh
code --install-extension anthropic.claude-code
code --install-extension ms-ceintl.vscode-language-pack-ko
```

### 5.3 리모트 서버 접속방법

VS Code의 **Remote-SSH** 확장 프로그램을 사용하면 GUI 환경에서 리모트 서버에 간편하게 접속할 수 있습니다.

1.  **설정 연동**: Remote-SSH는 이전에 작성한 `~/.ssh/config` 파일을 자동으로 읽어와 목록을 표시합니다.
2.  **접속 방법**: 왼쪽 패널의 '원격 탐색기' 아이콘을 클릭하면 등록된 서버 목록(`server_alias` 등)이 나타납니다. 접속하려는 서버 옆의 '새 창에서 연결' 아이콘을 클릭합니다.
3.  **효과**: 터미널 명령어 없이 클릭만으로 원격 서버의 파일 구조를 탐색하고 직접 편집할 수 있습니다.

### 5.4 터미널 활용법 (대화형 CLI)

터미널에서 명령어를 입력하여 각 AI 모델의 대화형(Interactive) 셸을 즉시 실행할 수 있습니다.

#### 5.4.1 Gemini CLI 실행

```bash
# Gemini CLI 대화창으로 진입
gemini

# 또는 단발성 질문 (명령어 뒤에 질문 추가)
gemini "현재 디렉토리의 파일 구조를 분석해줘"
```

#### 5.4.2 Claude Code 실행

```bash
# Claude Code 대화형 셸 실행
claude

# 이후 대화창(>)에서 명령 입력
> /fix "src/index.js의 버그를 수정해줘"
```

> [!NOTE]
> **Antigravity**는 터미널 명령어가 아닌, 프로그램 상단의 **'Toggle Agent'** 버튼을 클릭하여 에이전트 모드를 활성화한 후 자연어로 직접 소통하며 사용합니다.

### 5.5 Claude Code 확장프로그램 사용법

5.2에서 설치한 **Claude Code for VS Code** 확장 프로그램을 활용하는 방법입니다.

1.  **파일 오픈**: 탐색기에서 작업할 파일을 아무거나 하나 오픈합니다.
2.  **버튼 클릭**: 편집기 창의 우측 상단 또는 파일 탭 근처에 표시되는 **'Claude Code: Open'** 버튼을 클릭합니다.
3.  **대화창 활성화**: 클릭 시 Antigravity 대화창과 유사한 형태의 Claude Code 전용 대화창이 나타나며, 이를 통해 현재 파일과 관련된 질문이나 코드 수정을 요청할 수 있습니다.

---

## 6. GitHub 연동 및 자동화

### 6.1 GitHub CLI (gh) 설치 및 설정

GitHub CLI(`gh`)를 설치하면 터미널을 벗어나지 않고 GitHub의 기능을 제어할 수 있으며, AI 에이전트가 직접 PR 생성, 이슈 관리, 릴리즈 작성을 수행하는 데 필수적입니다.

#### 설치 방법

- **MacOS**: `brew install gh`
- **Linux**: `sudo apt install gh` (또는 해당 배포판 패키지 매니저)
- **Windows**: `winget install --id GitHub.cli`

#### 인증 및 확인

```bash
# GitHub 로그인 (웹 브라우저 인증 방식)
gh auth login

# 로그인 상태 확인
gh auth status
```

### 6.2 AI를 활용한 릴리즈 자동화

`gh` CLI가 설치된 상태에서 AI(Antigravity/Claude/Gemini)에게 자연어로 릴리즈를 요청하는 방법입니다.

1.  **AI에게 요청**: 복잡하게 지시할 필요 없이 **"v1.2.0 버전으로 릴리즈해줘"**라고만 요청해도 충분합니다.
2.  **AI의 동작 흐름**:
    - `git log`를 분석하여 변경 사항 요약(릴리즈 노트 작성)
    - `gh release create v1.2.0 --generate-notes` 등의 명령어 수행
    - **자동 처리**: 태그가 없으면 AI가 내부적으로 사용하는 `gh` 명령어가 **태그 생성 -> 서버 푸쉬 -> 릴리즈 페이지 생성** 과정을 한 번에 완료합니다.
3.  **수동 실행 시 예시**:
    ```bash
    # 태그 생성부터 릴리즈까지 한 번에 처리
    gh release create v1.2.0 --generate-notes
    ```


---

## 7. bkit 설치

**bkit (Vibecoding Kit)**은 PDCA 방법론을 기반으로 설계된 AI 네이티브 개발 도구로, Claude Code와 Gemini CLI의 기능을 보강하는 플러그인 형태로 제공됩니다.

### 7.1 Claude Code에서 설치

Claude Code 터미널(Interactive Shell) 내에서 아래 명령어를 순서대로 실행합니다.

> [!NOTE]
> 아래 `/plugin` 명령어는 **bkit 전용 슬래시 커맨드**입니다. Claude Code 기본 명령어가 아니며, bkit 설치 후에만 사용 가능합니다.

```
# Claude Code 대화창(>) 내에서 실행
# 1. 플러그인 마켓플레이스 추가
/plugin marketplace add popup-studio-ai/bkit-claude-code

# 2. bkit 플러그인 설치
/plugin install bkit
```

### 7.2 Gemini CLI에서 설치

터미널에서 아래 명령어를 실행하여 Gemini CLI용 bkit 익스텐션을 설치합니다.

**방법 1: 자동 설치 (권장)**
```bash
gemini extensions install https://github.com/popup-studio-ai/bkit-gemini.git
```

**방법 2: 수동 설치 (GitHub Clone)**
자동 설치가 원활하지 않을 경우, 아래 경로에 직접 프로젝트를 복제합니다.
```bash
git clone https://github.com/popup-studio-ai/bkit-gemini.git ~/.gemini/extensions/bkit
```

---

## 8. Docker 환경 구성

n8n을 컨테이너로 실행하기 위한 Docker 환경을 준비합니다.

### 8.1 Docker Desktop 설치

**MacOS:**
```bash
brew install --cask docker
```
설치 후 Docker Desktop 앱을 실행하여 엔진을 시작합니다.

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install -y docker.io docker-compose-plugin
sudo usermod -aG docker $USER  # 재로그인 필요
```

**Windows:**
[Docker Desktop 공식 페이지](https://www.docker.com/products/docker-desktop/)에서 설치 파일을 다운로드합니다.

**설치 확인:**
```bash
docker --version
docker compose version
```

### 8.2 docker-compose.yml 구조 이해

n8n 실행에 사용할 `docker-compose.yml` 예시와 각 항목 설명입니다.

```yaml
services:
  n8n:
    image: n8nio/n8n:latest      # n8n 공식 Docker 이미지
    container_name: n8n
    restart: unless-stopped      # 서버 재시작 시 자동으로 컨테이너 재시작
    ports:
      - "5678:5678"              # 호스트포트:컨테이너포트
    environment:
      - N8N_HOST=${N8N_HOST}     # 접속 호스트 (예: localhost 또는 서버IP)
      - N8N_PORT=5678
      - N8N_PROTOCOL=${N8N_PROTOCOL}  # http 또는 https
      - WEBHOOK_URL=${WEBHOOK_URL}    # 외부 Webhook 수신 URL
      - N8N_ENCRYPTION_KEY=${N8N_ENCRYPTION_KEY}  # 자격증명 암호화 키
    volumes:
      - n8n_data:/home/node/.n8n  # 워크플로우/데이터 영속성 보장
    env_file:
      - .env                      # 환경변수 파일 분리

volumes:
  n8n_data:                       # Docker 관리 볼륨 (데이터 보존)
```

### 8.3 .env 파일 분리 관리

API 키, 비밀번호 등 민감한 정보는 `.env` 파일로 분리하여 관리합니다.

**`.env` 파일 예시:**
```bash
N8N_HOST=localhost
N8N_PORT=5678
N8N_PROTOCOL=http
WEBHOOK_URL=http://localhost:5678
N8N_ENCRYPTION_KEY=your_random_32char_key_here
N8N_API_KEY=                  # 9.4에서 발급 후 입력
```

> [!CAUTION]
> `.env` 파일에는 민감한 정보가 포함되어 있습니다. 반드시 `.gitignore`에 추가하세요.

```bash
# .gitignore에 추가
echo ".env" >> .gitignore
```

---

## 9. n8n 컨테이너 설치 및 실행

### 9.1 n8n이란?

n8n은 **오픈소스 워크플로우 자동화 툴**입니다. Zapier/Make와 유사하지만 셀프호스팅이 가능합니다.

**왜 Python 데몬 대신 n8n인가?**

| 기존 Python 데몬 | n8n 워크플로우 |
|---|---|
| 코드 읽기 전까지 로직 파악 불가 | GUI로 전체 흐름을 시각적으로 파악 |
| 오류 시 로그 파일 직접 확인 | 웹 UI에서 실행 이력/오류 즉시 확인 |
| 재실행하려면 SSH 접속 필요 | 웹 UI에서 클릭 한 번으로 재실행 |
| 슬랙/메일 알림 직접 구현 | 내장 노드로 즉시 연동 |
| 수정 후 배포 프로세스 필요 | Claude Code가 JSON 직접 생성/수정 |

### 9.2 docker-compose로 n8n 실행

8.2에서 작성한 `docker-compose.yml`이 있는 디렉토리에서 실행합니다.

```bash
docker compose up -d          # 백그라운드 실행
docker compose down           # 중지 (데이터 보존)
docker compose logs -f n8n    # 실시간 로그 확인
docker compose restart n8n    # n8n 컨테이너만 재시작
docker compose pull && docker compose up -d  # 최신 버전으로 업데이트
```

### 9.3 웹 UI 접속 확인

```
로컬 환경:  http://localhost:5678
원격 서버:  http://<서버IP>:5678
```

1. 웹 브라우저에서 위 주소로 접속합니다.
2. 최초 접속 시 관리자 계정(이메일/비밀번호)을 설정합니다.
3. 대시보드가 보이면 정상 실행 완료입니다.

### 9.4 n8n API 설정 (MCP 연동 준비)

n8n-MCP가 워크플로우를 직접 배포하려면 n8n API Key가 필요합니다.

1. n8n 웹 UI → 우측 상단 프로필 → **Settings**
2. **API** 메뉴 → **Create API Key**
3. 생성된 키를 `.env` 파일의 `N8N_API_KEY`에 저장

**API 동작 확인:**
```bash
curl -H "X-N8N-API-KEY: your_api_key" http://localhost:5678/api/v1/workflows
```

---

## 10. n8n-MCP + n8n-skills 설정

Claude Code가 n8n 노드를 **정확히** 알고 워크플로우를 생성하도록 AI 지식을 주입하는 단계입니다.

> [!NOTE]
> n8n-MCP 없이 Claude Code에게 워크플로우 생성을 요청하면 노드 속성을 '추측'으로 작성하여 오류가 빈번합니다. 반드시 설정하세요.

### 10.1 n8n-MCP란?

[n8n-MCP](https://github.com/czlonkowski/n8n-mcp)는 AI 어시스턴트에게 n8n **1,239개 노드**의 정확한 문서를 제공하는 MCP 서버입니다.

- Claude Code가 `search_nodes`, `get_node_info` 등 도구를 통해 노드 속성을 실시간 조회
- n8n API 연동 시 워크플로우 생성/수정/배포까지 자동화
- 지원 IDE: Claude Code, Antigravity, Cursor, Windsurf, VS Code

### 10.2 n8n-MCP 설치

**Option A: Hosted Service (팀 공용 권장)**
1. [dashboard.n8n-mcp.com](https://dashboard.n8n-mcp.com) 가입
2. API Key 발급 (무료: 100 calls/day)
3. 아래 10.3에서 API Key 설정

**Option B: npx 로컬 실행 (개인 개발용)**
```bash
npx n8n-mcp
```

**Option C: Docker 자체 호스팅**
```bash
docker run -d --name n8n-mcp -e N8N_MCP_MODE=hosted czlonkowski/n8n-mcp
```

### 10.3 Claude Code에 MCP 연동

프로젝트 루트 또는 홈 디렉토리에 `.mcp.json` 파일을 생성합니다.

> [!CAUTION]
> `.mcp.json` 파일에는 API 키가 포함됩니다. 반드시 `.gitignore`에 추가하세요.
> ```bash
> echo ".mcp.json" >> .gitignore
> ```

**Hosted Service 연동:**
```json
{
  "mcpServers": {
    "n8n": {
      "command": "npx",
      "args": ["-y", "n8n-mcp"],
      "env": {
        "N8N_MCP_MODE": "hosted",
        "N8N_MCP_API_KEY": "your_hosted_api_key"
      }
    }
  }
}
```

**로컬 n8n 인스턴스 연동 (워크플로우 자동 배포):**
```json
{
  "mcpServers": {
    "n8n": {
      "command": "npx",
      "args": ["-y", "n8n-mcp"],
      "env": {
        "N8N_MCP_MODE": "hosted",
        "N8N_MCP_API_KEY": "your_hosted_api_key",
        "N8N_API_URL": "http://localhost:5678",
        "N8N_API_KEY": "your_n8n_api_key"
      }
    }
  }
}
```

### 10.4 n8n-skills란?

[n8n-skills](https://github.com/czlonkowski/n8n-skills)는 Claude Code에 설치하는 **7가지 전문 스킬**로, n8n-MCP를 더 정확하게 활용하도록 AI를 훈련시킵니다.

| # | 스킬명 | 역할 |
|---|--------|------|
| 1 | Expression Syntax | `{{$json.body}}` 등 표현식 정확히 작성 |
| 2 | **MCP Tools Expert** (최우선) | 어떤 MCP 도구를 언제 써야 하는지 판단 |
| 3 | Workflow Patterns | 5가지 검증된 워크플로우 설계 패턴 |
| 4 | Validation Expert | 유효성 오류 해석 및 수정 방법 |
| 5 | Node Configuration | 노드 속성 간 의존성 설정 |
| 6 | Code JavaScript | Code 노드에서 JS 올바르게 작성 |
| 7 | Code Python | Code 노드에서 Python 작성법 및 제한사항 |

### 10.5 n8n-skills 설치

```bash
# Claude Code 터미널에서 실행

# 방법 1: 플러그인 명령어 (권장)
/plugin install czlonkowski/n8n-skills

# 방법 2: 수동 설치
git clone https://github.com/czlonkowski/n8n-skills.git
cp -r n8n-skills/skills/* ~/.claude/skills/
```

---

## 11. Python → n8n 마이그레이션 전략

기존 Python 코드/서비스 데몬을 n8n 워크플로우로 체계적으로 이전하는 방법입니다.

### 11.1 마이그레이션 대상 유형 분류

| Python 패턴 | n8n 대응 노드 | 난이도 |
|---|---|---|
| `schedule` / `cron` 데몬 | Schedule Trigger | 🟢 쉬움 |
| `requests.get/post()` | HTTP Request | 🟢 쉬움 |
| Slack/메일 알림 | Slack / Gmail / Email 노드 | 🟢 쉬움 |
| `if / for` 조건·반복 로직 | IF / Switch / Loop Over Items | 🟡 보통 |
| `json` 파싱 / 데이터 변환 | Set, Code (JS) | 🟡 보통 |
| `subprocess` / 쉘 명령 | Execute Command | 🟡 보통 |
| DB 쿼리 (`psycopg2`, `pymysql`) | Postgres / MySQL 노드 | 🟡 보통 |
| 파일 읽기/쓰기 | Read/Write Binary File | 🟡 보통 |
| Webhook 수신 (`Flask`, `FastAPI`) | Webhook Trigger | 🔴 주의 필요 |
| 복잡한 비즈니스 로직 | Code 노드 (JS/Python) | 🔴 주의 필요 |

### 11.2 마이그레이션 단계별 절차

```
1단계. Python 코드 분석
   → 트리거 (언제 실행?) / 처리 로직 / 출력 (어디로 보냄?) 으로 분해

2단계. 트리거 유형 파악
   → 스케줄 실행? / Webhook 수신? / 수동 실행?

3단계. Claude Code에 마이그레이션 요청 (11.3 참고)

4단계. 생성된 JSON을 n8n 웹 UI에서 Import 후 테스트 실행

5단계. 기존 Python 결과 vs n8n 결과 비교 검증 (11.4 체크리스트)

6단계. 검증 완료 시 Python 데몬(systemd) 비활성화
        n8n 워크플로우 Active 상태로 전환
```

### 11.3 Claude Code에게 마이그레이션 요청하는 법

아래 프롬프트 패턴을 복사하여 Claude Code에 붙여넣고, Python 코드를 첨부하세요.

```
아래 Python 스크립트를 n8n 워크플로우 JSON으로 변환해줘.
n8n-MCP 도구를 사용해서 정확한 노드 속성을 조회한 후 생성해.

[Python 코드 붙여넣기]

요구사항:
- 트리거: (예: 매일 오전 9시 / Webhook 수신 / 수동 실행)
- n8n 버전: 1.x (self-hosted, localhost:5678)
- 출력: (예: 슬랙 #알림 채널로 전송 / DB 저장 / 파일 저장)
- 오류 발생 시: 슬랙 #에러 채널로 알림
```

> [!TIP]
> Python 코드 전체를 붙여넣는 것보다, 파일을 `@[파일명]` 형태로 참조하면 더 정확합니다.

### 11.4 마이그레이션 검증 체크리스트

- [ ] 트리거 타이밍이 기존과 동일한가?
- [ ] HTTP 요청의 URL, 헤더, 바디가 동일한가?
- [ ] 데이터 변환 결과값이 동일한가?
- [ ] DB 저장 데이터가 동일한가?
- [ ] 오류 발생 시 알림이 정상적으로 오는가?
- [ ] n8n 실행 로그에 오류가 없는가?
- [ ] Python 데몬과 n8n이 동시에 실행되어 중복 처리되지 않는가?

---

## 12. Claude Code로 n8n 워크플로우 개발

### 12.1 권장 개발 플로우

```
Python 코드 분석
    ↓
Claude Code에 마이그레이션 요청
(n8n-MCP + n8n-skills 활성화 상태)
    ↓
생성된 JSON을 n8n 웹 UI에서 Import
    ↓
테스트 실행
    ↓ (오류 발생 시)
Claude Code에 오류 로그 전달 → 수정 → 재Import
    ↓ (정상 확인)
기존 Python 데몬 비활성화
n8n 워크플로우 Active 전환
```

### 12.2 워크플로우 JSON Import/Export

**Export (워크플로우 백업/공유):**
1. n8n 웹 UI → 워크플로우 목록
2. 대상 워크플로우 우측 `⋮` 클릭 → **Download**
3. `.json` 파일로 저장됨

**Import (Claude Code가 생성한 JSON 적용):**
1. n8n 웹 UI → 좌측 상단 **+** 버튼 → **Import from File**
2. Claude Code가 생성한 `.json` 파일 선택
3. Import 후 **Save**

> [!NOTE]
> 워크플로우 JSON을 Git으로 버전 관리하면 팀원 간 공유 및 롤백이 쉬워집니다.

### 12.3 실전 예시: Python 데몬 → n8n 워크플로우

**Before (Python 스크립트 예시):**
```python
import schedule
import requests
import time

def check_api_and_notify():
    response = requests.get("https://api.example.com/status")
    data = response.json()
    if data["status"] != "ok":
        requests.post("https://hooks.slack.com/...",
            json={"text": f"⚠️ 서비스 이상 감지: {data['message']}"})

schedule.every(10).minutes.do(check_api_and_notify)
while True:
    schedule.run_pending()
    time.sleep(1)
```

**Claude Code 요청:**
```
위 Python 데몬을 n8n 워크플로우 JSON으로 변환해줘.
n8n-MCP로 HTTP Request, Schedule Trigger, Slack 노드 속성을 확인 후 생성해.
- 트리거: 10분마다 실행
- API 상태가 'ok'가 아닐 때만 슬랙 알림
- 오류 발생 시 별도 슬랙 채널(#errors)로 알림
```

**After (n8n 워크플로우 구성):**
```
[Schedule Trigger: 10분마다]
    → [HTTP Request: GET api.example.com/status]
    → [IF: status != 'ok']
        → True:  [Slack: #알림 채널 메시지 전송]
        → False: [No Operation]
```

### 12.4 트러블슈팅

| 오류 상황 | 원인 | 해결 방법 |
|---|---|---|
| `$json.body` undefined | Webhook 데이터 구조 미스매치 | Webhook 노드에서 `$json.body`로 접근 확인 |
| Code 노드에서 `import` 오류 | Python 외부 라이브러리 미지원 | JS로 전환하거나 HTTP Request 노드 활용 |
| Loop 노드 배치 오류 | 반환 형식 불일치 | `[{json: {...}}]` 형식으로 반환 확인 |
| 인증 토큰 만료 | 액세스 토큰 미갱신 | Credentials 노드로 OAuth 자동 갱신 설정 |
| 워크플로우 실행 안 됨 | Active 상태 미확인 | 웹 UI에서 워크플로우 Active 토글 ON 확인 |

---

## 📄 License

이 프로젝트는 **MIT License**에 따라 배포됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

**문의 사항 및 피드백**: 20eung@gmail.com
