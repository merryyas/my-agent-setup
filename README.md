# my-agent-setup

여러 PC에서 쓰는 AI 에이전트 스킬 모음. 한 번 올려두고, 새 PC에서는 URL 하나로 설치합니다.

## 새 PC에서 설치하기

Cursor나 Claude Code 채팅창에 아래 한 줄을 붙여넣으세요. 나머지는 에이전트가 합니다.

```
https://github.com/merryyas/my-agent-setup 의 SETUP.md 를 읽고 그대로 설치해줘
```

인터넷이 막힌 PC라면 이 저장소를 zip으로 받아 옮긴 뒤, 압축 푼 폴더에서 이렇게 말하면 됩니다.

```
이 폴더의 SETUP.md 를 읽고 그대로 설치해줘
```

## 담긴 것

스킬 15개. Superpowers 14개 전부와 Anthropic의 frontend-design 하나입니다.

**설계·계획**

| 스킬 | 하는 일 |
|---|---|
| brainstorming | 만들기 전에 목적·제약·성공 기준부터 정리 |
| writing-plans | 작업을 잘게 쪼개고 검증 방법까지 명시 |
| executing-plans | 세운 계획을 순서대로 실행하고 진행 상황을 관리 |
| using-superpowers | 나머지 스킬을 언제 쓰는지 안내하는 진입점 |

**작성·검증**

| 스킬 | 하는 일 |
|---|---|
| test-driven-development | 테스트를 먼저 쓰고 그다음 구현 |
| verification-before-completion | 완료 주장 전에 실제로 확인 |
| systematic-debugging | 짐작 대신 원인 추적 |
| requesting-code-review | 코드 리뷰를 받을 수 있게 변경분을 정리 |
| receiving-code-review | 받은 리뷰 지적을 걸러서 반영 |

**협업·git**

| 스킬 | 하는 일 |
|---|---|
| using-git-worktrees | 작업별로 worktree를 분리 |
| finishing-a-development-branch | 브랜치를 정리하고 마무리 |
| dispatching-parallel-agents | 독립적인 일을 여러 에이전트에 나눠 실행 |
| subagent-driven-development | 계획의 각 작업을 서브에이전트로 구현·리뷰 |

**기타**

| 스킬 | 하는 일 |
|---|---|
| frontend-design | 템플릿 같지 않은 UI 디자인 판단 |
| writing-skills | 스킬 자체를 만드는 법 |

HWP 문서 스킬은 용량 때문에 파일로 담지 않았습니다. SETUP.md가 설치 방법을 안내합니다.

## 이 저장소를 처음 만들 때

```bash
git init
git add .
git commit -m "initial: agent skills setup"
git branch -M main
git remote add origin https://github.com/merryyas/my-agent-setup.git
git push -u origin main
```

GitHub에서 저장소를 먼저 하나 만들어야 합니다(New repository → 이름 `my-agent-setup` → Public 또는 Private).
Private으로 두면 새 PC에서 설치할 때 로그인이 필요합니다. 민감한 내용이 없으니 Public이 편합니다.

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

넣고 나서 `git push` 하면 다른 PC에서도 `git pull` 로 따라옵니다.

## 안전에 관해

이 저장소는 에이전트에게 "읽고 실행하라"고 시키는 파일을 담고 있습니다.
**본인이 관리하는 저장소에만 이 방식을 쓰세요.** 남의 저장소 URL을 에이전트에게 그대로 넘기면
그 안의 지침이 무엇이든 실행될 수 있습니다.

## 라이선스

각 스킬의 원래 라이선스를 따릅니다. 자세한 출처는 SETUP.md 맨 아래를 보세요.
