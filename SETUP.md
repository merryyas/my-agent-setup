# SETUP — AI 에이전트용 설치 지침

> **이 문서는 사람이 아니라 AI 에이전트가 읽고 실행하는 지침서입니다.**
> 사용자는 에이전트에게 이 파일의 URL만 주면 됩니다.

---

## 에이전트에게 (Instructions for the agent)

당신은 지금부터 이 저장소의 스킬과 플러그인을 사용자의 환경에 설치합니다.

**지켜야 할 원칙**

1. 아래 단계를 **순서대로** 진행합니다.
2. **⚠️ 표시된 단계는 당신이 대신 할 수 없습니다.** 사용자에게 정확히 무엇을 하라고 안내만 하고, 완료했는지 확인한 뒤 다음으로 넘어가세요.
3. 각 단계가 끝나면 결과를 **한 줄로** 보고합니다. 장황한 설명은 하지 마세요.
4. 실패하면 멈추고, 무엇이 왜 실패했는지 알린 뒤 사용자의 판단을 기다립니다. 임의로 우회하지 마세요.
5. 마지막에 검증 단계(5번)를 반드시 수행합니다.

---

## 0단계 — 환경 파악

먼저 다음을 확인하고 사용자에게 한 줄로 보고하세요.

- **어떤 도구에서 실행 중인가**: Cursor / Claude Code / Claude Desktop(Cowork) / 그 외
- **Node.js 18 이상** 설치 여부 — `node --version`
- **Python 3.9 이상** 설치 여부 — `python3 --version` 또는 `python --version`
- **git** 설치 여부 — `git --version`

Node나 Python이 없으면 그 사실만 알리세요. 3단계(HWP)에서만 필요하고 나머지는 없어도 됩니다.

확인한 도구에 따라 아래 표의 설치 경로를 사용합니다.

| 실행 중인 도구 | 스킬 설치 위치 |
|---|---|
| Cursor | `<프로젝트 루트>/.cursor/skills/` (프로젝트 단위만 지원) |
| Claude Code | `~/.claude/skills/` (전역) 또는 `<프로젝트 루트>/.claude/skills/` |
| Claude Desktop (Cowork) | 파일 복사 불가 — 3단계 방식 참조 |

---

## 1단계 — 스킬 5개 설치

이 저장소의 `skills/` 아래에 다섯 개 폴더가 있습니다. 각각 `SKILL.md`를 담고 있는 완결된 스킬입니다.

| 스킬 | 하는 일 |
|---|---|
| `brainstorming` | 만들기 전에 목적·제약·성공 기준을 먼저 파악하고 설계안을 비교 제시 |
| `writing-plans` | 설계를 2~5분 단위 작업으로 분해하고 각 단계에 검증 방법을 붙임 |
| `verification-before-completion` | "완료했다"고 말하기 전에 실제로 돌려보고 근거를 확인 |
| `systematic-debugging` | 짐작으로 고치지 않고 원인을 단계적으로 추적 |
| `frontend-design` | UI를 만들 때 템플릿 같지 않은 의도적 디자인 판단 |

**설치 방법**

0단계에서 정한 경로로 폴더째 복사하세요.

```bash
# Cursor — 프로젝트 루트에서 실행
mkdir -p .cursor/skills
cp -r skills/* .cursor/skills/

# Claude Code — 전역 설치
mkdir -p ~/.claude/skills
cp -r skills/* ~/.claude/skills/
```

Windows PowerShell:

```powershell
# Cursor
New-Item -ItemType Directory -Force .cursor\skills
Copy-Item -Recurse -Force skills\* .cursor\skills\

# Claude Code
New-Item -ItemType Directory -Force $HOME\.claude\skills
Copy-Item -Recurse -Force skills\* $HOME\.claude\skills\
```

복사 후 **몇 개 폴더가 들어갔는지 세어서** 보고하세요. 5개여야 합니다.

⚠️ 복사가 끝나면 사용자에게 **도구를 완전히 껐다가 다시 켜라고** 안내하세요. 재시작 전에는 인식되지 않습니다.

---

## 2단계 — Superpowers 플러그인 ⚠️

이건 슬래시 명령이라 **에이전트가 대신 칠 수 없습니다.** 사용자에게 안내만 하세요.

실행 중인 도구에 맞는 것 하나만 알려주세요:

| 도구 | 사용자가 채팅창에 칠 명령 |
|---|---|
| Cursor | `/add-plugin superpowers` |
| Claude Code | `/plugin install superpowers@claude-plugins-official` |
| Gemini CLI | `gemini extensions install https://github.com/obra/superpowers` |
| Codex CLI | `/plugins` → superpowers 검색 → Install |

**함께 전달할 내용**

- Superpowers는 세션 시작 훅으로 **매번 자동으로 걸립니다.** 따로 부를 필요가 없습니다.
- 대신 간단한 요청에도 설계 절차가 끼어들 수 있습니다. 건너뛰려면 "설계 단계 생략하고 바로 해줘"라고 말하면 됩니다.
- 기관·회사 환경이라면 외부 통신을 끄는 편이 낫습니다: 환경변수 `SUPERPOWERS_DISABLE_TELEMETRY=1`

> 참고: 1단계에서 설치한 brainstorming, writing-plans, verification-before-completion, systematic-debugging은 Superpowers에서 가져온 것입니다. 2단계로 Superpowers 본체를 설치하면 **중복**됩니다.
> Cursor·Claude Code를 쓰면 2단계만 하고 1단계의 그 네 개는 지워도 됩니다. 1단계는 Superpowers를 설치할 수 없는 환경(Claude Desktop 등)을 위한 것입니다.
> 어느 쪽으로 할지 **사용자에게 물어보고** 진행하세요.

---

## 3단계 — HWP 스킬 (선택)

한글 문서(.hwp / .hwpx)를 읽고 만들고 편집합니다. 한컴오피스 없이 동작합니다.
**Node 18+ 와 Python 3.9+ 가 필요합니다.** 없으면 이 단계를 건너뛰고 그 사실을 알리세요.

**Cursor / Claude Code인 경우** — 직접 설치 가능합니다:

```bash
git clone --depth 1 https://github.com/DoHyun468/claw-hwp /tmp/claw-hwp
cp -r /tmp/claw-hwp/plugins/claw-hwp/skills/hwp .cursor/skills/     # Cursor
# 또는
cp -r /tmp/claw-hwp/plugins/claw-hwp/skills/hwp ~/.claude/skills/   # Claude Code
rm -rf /tmp/claw-hwp
```

Claude Code는 플러그인 방식이 더 깔끔합니다 (⚠️ 사용자가 직접 입력):

```
/plugin marketplace add https://github.com/DoHyun468/claw-hwp
/plugin install claw-hwp@claw-hwp
```

**Claude Desktop (Cowork)인 경우** ⚠️ — 파일 복사가 안 됩니다. 다음을 대신 해주세요:

1. 위 저장소를 받아 `plugins/claw-hwp/skills/hwp` 폴더를 `hwp.skill` 이라는 이름의 zip으로 압축
2. 그 파일을 사용자에게 전달
3. 사용자가 **Settings → Skills → Upload skill** 에서 업로드하도록 안내

**알아둘 제약** — 사용자에게 함께 전달하세요:

- 기존 `.hwp` 파일을 편집하면 **문서 안의 표가 사라질 수 있습니다.**
- 표를 지켜야 하면 한컴오피스에서 `.hwpx`로 한 번 저장한 뒤 그 파일로 작업하세요.
- 결과물은 반드시 한컴오피스에서 열어 확인해야 합니다.
- PDF·DOCX 변환은 아직 지원하지 않습니다.

---

## 4단계 — git 동기화 설정 (선택, 권장)

사용자가 여러 PC(집/회사)를 오간다면 스킬을 저장소에 커밋해두라고 안내하세요.

```bash
git add .cursor/skills
git commit -m "add agent skills"
git push
```

다른 PC에서는 `git pull` 한 번이면 스킬까지 따라옵니다. 이후 파일을 들고 다닐 필요가 없어집니다.

---

## 5단계 — 검증 (건너뛰지 말 것)

설치했다고 말하기 전에 **실제로 확인**하세요.

1. **파일 확인** — 설치 경로에 각 스킬 폴더와 그 안의 `SKILL.md`가 실제로 존재하는지 확인합니다. 개수를 셉니다.
2. **인식 확인** — ⚠️ 사용자에게 도구를 재시작한 뒤 채팅에 *"지금 쓸 수 있는 스킬 알려줘"* 라고 물어보게 하세요. 설치한 스킬 이름이 목록에 나와야 합니다.
3. **동작 확인** — 다음 중 실제로 시켜보게 안내합니다:
   - `frontend-design` → "간단한 소개 페이지 디자인 방향을 잡아줘"
   - `brainstorming` → "새 기능 하나 만들려고 하는데 같이 정리하자"
   - `hwp` → 아무 .hwp 파일을 올리고 "표 구조 그대로 읽어줘"

**최종 보고 형식** — 설치된 것 / 건너뛴 것 / 사용자가 아직 해야 할 것, 세 줄로 정리해서 알리세요. 확인하지 않은 것을 "완료"라고 말하지 마세요.

---

## 출처와 라이선스

여기 담긴 것은 모두 공개 프로젝트에서 가져왔습니다. 원본은 아래를 보세요.

| 스킬 | 출처 | 라이선스 |
|---|---|---|
| brainstorming, writing-plans, verification-before-completion, systematic-debugging | [obra/superpowers](https://github.com/obra/superpowers) | MIT |
| frontend-design | Anthropic | Apache 2.0 (`skills/frontend-design/LICENSE.txt`) |
| hwp (3단계) | [DoHyun468/claw-hwp](https://github.com/DoHyun468/claw-hwp) | MIT |

`brainstorming`은 원본에서 로컬 브라우저 서버가 필요한 시각 도우미 기능을 제거했습니다(외부 통신 포함). `systematic-debugging`은 개발용 테스트 파일을 정리했습니다. 그 외 내용은 원본 그대로입니다.
