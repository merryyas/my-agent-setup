# my-agent-setup

여러 PC에서 쓰는 AI 에이전트 스킬 모음. 한 번 올려두고, 새 PC에서는 **URL 한 줄로** 설치합니다.

집 PC(Claude Code)와 사무실 PC(Cursor)가 같은 스킬을 쓰도록 만든 저장소입니다.

## 새 PC에서 설치하기

Cursor나 Claude Code 채팅창에 아래 한 줄을 붙여넣으세요. 나머지는 에이전트가 합니다.

```
https://github.com/merryyas/my-agent-setup 의 SETUP.md 를 읽고 그대로 설치해줘
```

인터넷이 막힌 PC라면 이 저장소를 zip으로 받아 옮긴 뒤, 압축 푼 폴더에서 이렇게 말하면 됩니다.

```
이 폴더의 SETUP.md 를 읽고 그대로 설치해줘
```

스킬 34개가 전부 파일로 들어 있어서 **인터넷 없이도 설치됩니다.** (HWP만 예외 — 원본에서 받습니다.)

## 설치 경로가 하나입니다

Cursor는 `~/.claude/skills/` 를 레거시 호환 경로로 읽습니다. 그래서 **두 PC가 같은 경로를 씁니다.**

| 도구 | 읽는 경로 |
|---|---|
| Cursor | `~/.cursor/skills/`, `~/.claude/skills/`, `<프로젝트>/.cursor/skills/` |
| Claude Code · 데스크톱 앱 | `~/.claude/skills/`, `<프로젝트>/.claude/skills/` |

## 담긴 것 — 스킬 34개

**설계·실행**

| 스킬 | 하는 일 |
|---|---|
| brainstorming | 만들기 전에 목적·제약·성공 기준부터 정리 |
| writing-plans | 작업을 잘게 쪼개고 검증 방법까지 명시 |
| executing-plans | 세운 계획을 순서대로 실행하고 진행 상황 관리 |
| using-superpowers | 나머지 스킬을 언제 쓰는지 안내하는 진입점 |
| subagent-driven-development | 계획의 각 작업을 서브에이전트로 구현·리뷰 |
| dispatching-parallel-agents | 독립적인 일을 여러 에이전트에 나눠 실행 |

**작성·검증**

| 스킬 | 하는 일 |
|---|---|
| test-driven-development | 테스트를 먼저 쓰고 그다음 구현 |
| verification-before-completion | 완료 주장 전에 실제로 확인 |
| systematic-debugging | 짐작 대신 원인 추적 |
| requesting-code-review | 리뷰받을 수 있게 변경분을 정리 |
| receiving-code-review | 받은 지적을 걸러서 반영 |
| webapp-testing | 웹앱을 실제로 띄워서 동작 확인 |

**git·도구**

| 스킬 | 하는 일 |
|---|---|
| using-git-worktrees | 작업별로 worktree 분리 |
| finishing-a-development-branch | 브랜치 정리하고 마무리 |
| mcp-builder | MCP 서버 설계·구현 |
| claude-api | Claude API 레퍼런스 (모델·가격·툴 사용) |
| writing-skills | 스킬 만드는 법 (superpowers 관점) |
| skill-creator | 스킬 만드는 법 (Anthropic 관점) |

**문서·UI**

| 스킬 | 하는 일 |
|---|---|
| frontend-design | 템플릿 같지 않은 UI 디자인 판단 |
| web-artifacts-builder | React·Tailwind 기반 복합 아티팩트 |
| theme-factory | 결과물에 일관된 테마 입히기 |
| internal-comms | 사내 공지·보고서·FAQ 작성 |

**애니메이션·모션**

| 스킬 | 하는 일 |
|---|---|
| animate | 웹 애니메이션을 판단 순서대로 설계하고 구현까지 |
| animate-expo | React Native·Expo 애니메이션 (Reanimated·제스처·햅틱) |
| animation-vocabulary | "그 통통 튀는 거" 같은 설명을 정확한 용어로 역검색 |
| apple-design | 애플식 인터페이스·물리적 모션을 웹으로 옮기기 |
| find-animation-opportunities | 움직여야 하는데 안 움직이는 곳 찾기 (제안만, 구현 안 함) |
| improve-animations | 코드베이스 모션 전체 감사 + 우선순위 실행 계획 |
| review-animations ⚠️ | 모션 코드를 높은 기준으로 리뷰. **기본이 지적이고 통과는 어렵다** |

**UI 판단·프로토타입**

| 스킬 | 하는 일 |
|---|---|
| emil-design-eng | UI 폴리시와 "느낌 좋은 소프트웨어"의 디테일 철학 |
| pick-ui-library ⚠️ | 숫자·OTP 입력, 차트, 커맨드 메뉴, 가상 스크롤, 드래그앤드롭, 토스트, 상태관리, 스타일링 등에 쓸 라이브러리를 미리 골라둔 목록에서 추천 |
| prototype ⚠️ | 설명한 UI를 **서로 확실히 다른 여러 버전으로 만들어** 비주얼 피커에 늘어놓고, 넘겨보다 마음에 드는 걸 확정 |
| ask-sonner | Sonner 토스트 라이브러리 사용·문제 해결 |
| write-swift | 모던 Swift 작성 (Swift 6 동시성·값 타입·테스팅) |

> ⚠️ 표시한 **`review-animations` · `pick-ui-library` · `prototype` 세 개는
> `disable-model-invocation: true`** 라서 에이전트가 알아서 꺼내 쓰지 않습니다.
> 사용 가능 스킬 목록에도 안 나옵니다. **이름을 직접 불러야 켜집니다** —
> 예: `prototype 스킬로 상단 메뉴바 여러 버전 만들어줘`.
> 고장이 아니라 원저자가 의도한 동작입니다.

## 목록 파일 — `sources.json`

무엇이 파일로 들어 있고, 무엇을 밖에서 받아야 하고, **무엇을 왜 뺐는지**가 적혀 있습니다.
에이전트가 SETUP.md와 같이 읽습니다.

- `bundled` — `skills/` 에 담긴 것. 출처·라이선스·내가 고친 부분까지
- `external` — HWP처럼 설치 시점에 원본에서 받는 것, 플러그인, MCP 서버
- `excluded` — 일부러 뺀 것과 **그 이유**
- `wishlist` — 아직 없어서 직접 만들어야 하는 것

## 스킬을 추가하고 싶을 때

`skills/` 아래에 폴더를 하나 만들고 그 안에 `SKILL.md`를 넣으면 끝입니다. 형식은 이렇습니다.

```markdown
---
name: 스킬이름
description: 언제 이 스킬을 써야 하는지 한 문장. 이 설명을 보고 에이전트가 발동 여부를 판단합니다.
---

# 제목

여기에 작업 지침을 씁니다.
```

그다음 `sources.json` 의 `bundled.groups` 에 이름을 추가하고 `git push` 하세요.
다른 PC에서는 `git pull` 로 따라옵니다.

담을 수 없는 것(라이선스, 용량, 별도 설치)은 `external` 에 주소와 이유를 적으세요.

## 안전에 관해

이 저장소는 에이전트에게 "읽고 실행하라"고 시키는 파일을 담고 있습니다.
**본인이 관리하는 저장소에만 이 방식을 쓰세요.** 남의 저장소 URL을 에이전트에게 그대로 넘기면
그 안의 지침이 무엇이든 실행될 수 있습니다.

스킬을 추가할 때도 같습니다. 스킬은 에이전트에게 주는 지시문이고, 에이전트는 당신의 PC에서
파일을 읽고 명령을 실행합니다. 스킬 3,000개짜리 목록 같은 걸 통째로 넣지 마세요.

## 라이선스

superpowers 계열과 emilkowalski 계열은 MIT, Anthropic 계열은 Apache 2.0입니다.
자세한 출처는 SETUP.md 맨 아래를 보세요.

`anthropics/skills` 의 **docx·pdf·pptx·xlsx 는 재배포가 금지되어 담지 않았습니다.**
이유는 `sources.json` 의 `excluded` 에 있습니다.
