# SETUP — AI 에이전트용 설치 지침

> **이 문서는 사람이 아니라 AI 에이전트가 읽고 실행하는 지침서입니다.**
> 사용자는 에이전트에게 이 파일의 URL만 주면 됩니다.

---

## 에이전트에게 (Instructions for the agent)

당신은 지금부터 이 저장소의 스킬을 사용자의 환경에 설치합니다.

**지켜야 할 원칙**

1. 아래 단계를 **순서대로** 진행합니다.
2. **⚠️ 표시된 단계는 당신이 대신 할 수 없습니다.** 사용자에게 정확히 무엇을 하라고 안내만 하고, 완료했는지 확인한 뒤 다음으로 넘어가세요.
3. 각 단계가 끝나면 결과를 **한 줄로** 보고합니다. 장황한 설명은 하지 마세요.
4. 실패하면 멈추고, 무엇이 왜 실패했는지 알린 뒤 사용자의 판단을 기다립니다. 임의로 우회하지 마세요.
5. 마지막에 검증 단계를 반드시 수행합니다. **확인하지 않은 것을 완료라고 말하지 마세요.**

**같이 읽을 파일:** [`sources.json`](sources.json) — 무엇이 파일로 들어 있고, 무엇을 밖에서 받아야 하고, 무엇을 왜 뺐는지가 기계가 읽을 수 있는 형태로 적혀 있습니다.

---

## 0단계 — 환경 파악

다음을 확인하고 사용자에게 **한 줄로** 보고하세요.

- **어떤 도구인가**: Cursor / Claude Code (터미널 CLI) / Claude 데스크톱 앱·Cowork / 그 외
- `node --version` — 18 이상? (3단계 HWP에만 필요)
- `python --version` 또는 `python3 --version` — 3.9 이상? (3단계 HWP에만 필요)
- `git --version`

Node·Python이 없으면 그 사실만 알리세요. 1단계는 없어도 됩니다.

### 설치 경로

**Cursor와 Claude Code는 `~/.claude/skills/` 를 둘 다 읽습니다.** Cursor가 이 경로를 레거시 호환으로 지원하기 때문입니다. 그러니 **PC가 여러 대여도 경로는 하나로 통일하세요.**

| 도구 | 읽는 경로 | 이 지침이 쓸 경로 |
|---|---|---|
| Cursor | `~/.cursor/skills/`, `~/.claude/skills/`, `<프로젝트>/.cursor/skills/`, `<프로젝트>/.agents/skills/` | **`~/.claude/skills/`** |
| Claude Code (CLI) | `~/.claude/skills/`, `<프로젝트>/.claude/skills/` | **`~/.claude/skills/`** |
| Claude 데스크톱 앱 | `~/.claude/skills/` | **`~/.claude/skills/`** |

전역 경로를 쓸 수 없는 사정이 있으면 프로젝트 경로로 대체하고, 그 사실을 보고하세요.

---

## 1단계 — 스킬 22개 설치 (핵심)

이 저장소의 `skills/` 아래 스물두 개 폴더를 **통째로** 설치 경로에 복사합니다.
전부 파일로 들어 있으므로 **인터넷 없이도 됩니다.**

```bash
# macOS / Linux / Git Bash
mkdir -p ~/.claude/skills
cp -r skills/* ~/.claude/skills/
```

```powershell
# Windows PowerShell
New-Item -ItemType Directory -Force $HOME\.claude\skills
Copy-Item -Recurse -Force skills\* $HOME\.claude\skills\
```

**설치 후 반드시 확인하고 숫자를 보고하세요:**

1. 폴더가 **22개**인지 세기
2. 각 폴더에 `SKILL.md`가 실제로 있는지 확인 (하나라도 없으면 실패로 보고)

담긴 스킬 목록은 [`sources.json`](sources.json)의 `bundled.groups`에 있습니다. 크게 세 갈래입니다.

| 갈래 | 내용 |
|---|---|
| 설계·실행 | brainstorming, writing-plans, executing-plans, using-superpowers, subagent-driven-development, dispatching-parallel-agents |
| 작성·검증 | test-driven-development, verification-before-completion, systematic-debugging, requesting-code-review, receiving-code-review, webapp-testing |
| git·도구 | using-git-worktrees, finishing-a-development-branch, mcp-builder, claude-api, writing-skills, skill-creator |
| 문서·UI | frontend-design, web-artifacts-builder, theme-factory, internal-comms |

⚠️ 복사가 끝나면 사용자에게 안내하세요:
- **Claude Code / 데스크톱 앱** — 완전히 껐다가 다시 켜야 인식됩니다.
- **Cursor** — 재시작 불필요합니다. 열려 있는 상태에서 추가해도 다음 세션에 잡힙니다.

---

## 2단계 — HWP 스킬 (선택, 한국어 문서용)

한글 문서(.hwp / .hwpx)를 읽고 만들고 편집합니다. 한컴오피스 없이 동작합니다.
**Node 18+ 와 Python 3.9+ 가 필요합니다.** 없으면 건너뛰고 그 사실을 알리세요.

라이선스(MIT)상 담아도 되지만 용량 때문에 파일로 넣지 않았습니다. 원본에서 받으세요.

```bash
git clone --depth 1 https://github.com/DoHyun468/claw-hwp /tmp/claw-hwp
cp -r /tmp/claw-hwp/plugins/claw-hwp/skills/hwp ~/.claude/skills/
rm -rf /tmp/claw-hwp
```

```powershell
# Windows PowerShell
$t = "$env:TEMP\claw-hwp"
git clone --depth 1 https://github.com/DoHyun468/claw-hwp $t
Copy-Item -Recurse -Force "$t\plugins\claw-hwp\skills\hwp" "$HOME\.claude\skills\"
Remove-Item -Recurse -Force $t
```

> **Claude 데스크톱 앱에서는 이 단계를 건너뛰세요.** `anthropic-skills` 플러그인으로 이미 들어 있습니다. 목록에 `hwp`가 보이는지 먼저 확인하세요.

**제약 — 사용자에게 반드시 함께 전달하세요:**

- 기존 `.hwp` 파일을 편집하면 **문서 안의 표가 사라질 수 있습니다.**
- 표를 지켜야 하면 한컴오피스에서 `.hwpx`로 한 번 저장한 뒤 그 파일로 작업하세요.
- 결과물은 반드시 한컴오피스에서 열어 확인해야 합니다.
- PDF·DOCX 변환은 아직 지원하지 않습니다.

---

## 3단계 — Superpowers 플러그인 (선택, 대개 건너뜀)

**1단계로 이미 끝났습니다.** Superpowers 스킬 14개가 전부 파일로 들어가 있습니다.
플러그인으로 깔면 얻는 건 **자동 업데이트**와 **세션 시작 훅** 두 가지뿐입니다.

### ⚠️ 안 되는 환경이 많습니다 (2026-08 확인)

- **Claude 데스크톱 앱 / Cowork** — `/plugin` 명령 자체가 없습니다. 마켓플레이스 검색에도 안 나옵니다.
- **Claude Code (터미널 CLI)** — 됩니다: `/plugin install superpowers@claude-plugins-official`
- **Cursor** — `/add-plugin superpowers`

**`/plugin`이 안 되면 그냥 건너뛰세요.** 잃는 게 거의 없습니다.
"플러그인은 이 환경에서 안 되지만 스킬은 전부 설치됐다"고 한 줄 보고하고 넘어가면 됩니다.

### 훅이 없으면 뭐가 달라지나

훅은 매 대화마다 `using-superpowers`를 자동으로 띄웁니다. 파일 설치만 하면 그게 없으므로
스킬은 **설명이 맞을 때만** 걸립니다. 손해가 아닙니다 — 훅이 있으면 간단한 요청에도
설계 절차가 끼어듭니다. 명시적으로 쓰고 싶으면 이렇게 부르면 됩니다:

```
using-superpowers 스킬 보고 이 작업에 뭐가 맞는지 골라줘
```

설치하기로 했다면: 1단계의 superpowers 14개와 **중복**되므로 설치 경로에서 그 14개를 지우세요.
기관·회사 환경이면 외부 통신을 끄세요 — 환경변수 `SUPERPOWERS_DISABLE_TELEMETRY=1`

---

## 4단계 — MCP 서버 (해당될 때만)

MCP 서버는 파일 복사가 아니라 **설정**으로 붙습니다. [`sources.json`](sources.json)의
`external.mcp_servers.servers` 목록을 보고, 비어 있으면 이 단계를 건너뛰세요.

| 도구 | 방법 |
|---|---|
| Cursor | `~/.cursor/mcp.json` 에 항목 추가 |
| Claude Code (CLI) | `claude mcp add <이름> -- <명령>` |

**API 키는 절대 파일에 적지 마세요.** 환경변수로 처리하고, 사용자에게 직접 넣게 안내하세요.

---

## 5단계 — 검증 (건너뛰지 말 것)

설치했다고 말하기 전에 **실제로 확인**하세요.

1. **파일 확인** — 설치 경로의 폴더 수를 세고, 각 폴더에 `SKILL.md`가 있는지 확인합니다. 1단계만 했으면 22개, HWP까지면 23개입니다.
2. **인식 확인** ⚠️ — 사용자에게 (Claude Code면 재시작 후) *"지금 쓸 수 있는 스킬 알려줘"* 라고 물어보게 하세요. 설치한 이름이 목록에 나와야 합니다.
3. **동작 확인** — 다음 중 하나를 실제로 시켜보게 안내합니다:
   - `frontend-design` → "간단한 소개 페이지 디자인 방향을 잡아줘"
   - `brainstorming` → "새 기능 하나 만들려고 하는데 같이 정리하자"
   - `mcp-builder` → "MCP 서버 하나 만들려는데 구조 잡아줘"
   - `hwp` → 아무 .hwp 파일을 주고 "표 구조 그대로 읽어줘"

**최종 보고 형식** — 설치된 것 / 건너뛴 것 / 사용자가 아직 해야 할 것, 세 줄로 정리하세요.

---

## 스킬을 추가하고 싶을 때

`skills/` 아래에 폴더를 만들고 `SKILL.md`를 넣은 뒤, [`sources.json`](sources.json)의
`bundled.groups`에 이름을 추가하세요. 그리고 `git push` 하면 다른 PC에서 `git pull`로 따라옵니다.

담을 수 없는 것(라이선스 제한, 용량, 별도 설치 필요)은 파일 대신 `external` 아래에
주소와 이유를 적어두세요. **일부러 뺀 것은 `excluded` 에 이유와 함께 남기세요** —
그래야 나중에 모르고 다시 넣지 않습니다.

---

## 출처와 라이선스

| 스킬 | 출처 | 라이선스 |
|---|---|---|
| superpowers 계열 14개 | [obra/superpowers](https://github.com/obra/superpowers) | MIT |
| frontend-design, mcp-builder, claude-api, webapp-testing, web-artifacts-builder, skill-creator, theme-factory, internal-comms | [anthropics/skills](https://github.com/anthropics/skills) | Apache 2.0 (각 폴더 `LICENSE.txt`) |
| hwp (2단계) | [DoHyun468/claw-hwp](https://github.com/DoHyun468/claw-hwp) | MIT |

**원본과 다른 점** — 두 스킬만 손댔고 나머지는 원본 그대로입니다.

- `brainstorming` — 로컬 브라우저 서버가 필요한 시각 도우미를 제거했습니다(`scripts/`, `visual-companion.md`). 외부 통신이 포함돼 있어 기관 환경에 맞지 않았습니다. SKILL.md의 해당 절은 "인라인으로 그려서 보여주라"로 바꿨습니다.
- `systematic-debugging` — 원본에 섞여 있던 개발용 테스트 파일(`CREATION-LOG.md`, `test-*.md`)을 뺐습니다. SKILL.md는 원본과 동일합니다.

> 원본을 최신으로 따라갈 때 이 두 개는 그냥 덮어쓰지 말고 위 변경을 다시 적용하세요.

### ⚠️ 일부러 담지 않은 것

`anthropics/skills`의 **docx · pdf · pptx · xlsx**는 Apache 2.0이 **아닙니다.**
라이선스가 서비스 밖 복제·2차저작물·제3자 배포를 명시적으로 금지합니다
(© Anthropic, All rights reserved). 저장소에 담는 것도, 받아가게 하는 것도 위반입니다.

Claude 데스크톱 앱에는 플러그인으로 기본 제공됩니다. Cursor에서 문서 작업이 필요하면
`python-docx` / `openpyxl` 을 직접 쓰거나 다른 오픈소스 스킬을 찾으세요.

나머지 제외 항목과 이유는 [`sources.json`](sources.json)의 `excluded` 에 있습니다.

---

## 안전에 관해

이 저장소는 에이전트에게 "읽고 실행하라"고 시키는 파일을 담고 있습니다.
**본인이 관리하는 저장소에만 이 방식을 쓰세요.** 남의 저장소 URL을 에이전트에게 그대로 넘기면
그 안의 지침이 무엇이든 실행될 수 있습니다.

스킬을 추가할 때도 같습니다. 스킬은 에이전트에게 주는 지시문이고, 에이전트는 당신의 PC에서
파일을 읽고 명령을 실행합니다. 출처가 확인되지 않은 스킬을 대량으로 넣지 마세요.
