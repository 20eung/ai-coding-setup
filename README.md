# AI Coding 개발환경 구성 가이드

이 문서는 MacOS/Linux 및 Windows 환경에서 **Gemini CLI**, **Claude Code**, 그리고 **Antigravity**를 활용한 최적의 AI 코딩 개발환경을 구성하는 방법을 안내합니다.

---

## 목차

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

---

## 1. 사전 준비 사항 (Prerequisites)

각 도구의 설치 및 실행을 위해 다음 프로그램이 미리 설치되어 있어야 합니다.

- **Node.js & npm**: [Node.js 공식 홈페이지](https://nodejs.org/)에서 LTS 버전을 권장합니다.
- **Python**: [Python 공식 홈페이지](https://www.python.org/)에서 3.10 이상의 버전을 권장합니다.
- **Git**: [Git 공식 홈페이지](https://git-scm.com/)에서 설치 가능합니다.

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
npm install -g @google/generative-ai
```

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

```bash
# Bedrock 활성화 및 리전 설정 (필수)
export CLAUDE_CODE_USE_BEDROCK=1
export AWS_REGION="ap-northeast-2" # Bedrock 모델 권한을 받은 리전

# (선택) Anthropic Model 지정
# export ANTHROPIC_MODEL="global.anthropic.claude-sonnet-4-6"

# Claude Code 실행
claude
```

> [!TIP]
> 더 자세한 설정 방법은 [claude-code-use-bedrock](https://github.com/20eung/claude-code-use-bedrock) 문서를 참고하세요.

---

## 5. Antigravity 설치 및 설정

### 5.1 설치

Antigravity는 강력한 AI 코딩 에이전트 환경입니다. 별도의 설치 과정 없이 지원되는 환경에서 즉시 사용 가능하거나, 전용 클라이언트를 통해 구동됩니다.

### 5.2 확장 프로그램

VS Code와 함께 사용하면 효과가 극대화됩니다.

- **Remote-SSH**: 리모트 서버에 접속하여 파일을 편집하기 위해 필수입니다. (원격 탐색기 기능 포함)
- **Claude Code for VS Code**: VS Code 내에서 Claude 기능을 직접 사용합니다.
- **Korean Language Pack for Visual Studio Code**: 한국어 메뉴 구성을 위해 필수입니다.

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

Claude Code 터미널(Interactive Shell) 내에서 아래 플러그인 명령어를 순서대로 실행합니다.

```bash
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

**문의 사항 및 피드백**: 20eung@gmail.com
