## EXPLAIN

### 스킬 파일의 구조

Block 2에서 `/status` 스킬을 만들어봤습니다. 그 파일을 열어보면 두 부분으로 나뉩니다:

**1. YAML frontmatter (파일 상단 `---` 사이):**
```yaml
---
name: status
description: "프로젝트 현황을 요약합니다. Triggers: /status"
---
```
이 부분은 스킬의 "이름표"입니다. Claude가 이 파일을 어떤 스킬인지 인식하는 데 사용합니다.

**2. 본문 (지시 섹션):**
```markdown
# 현황 요약

지금 프로젝트의 파일 목록을 확인하고...
```
이 부분은 스킬이 호출됐을 때 Claude에게 내려갈 지시입니다.

### STUB이란?

**STUB**은 "아직 채워지지 않은 플레이스홀더"입니다. 마치 계약서에 `[성명]`, `[날짜]` 처럼 비어 있어서 채워야 하는 칸입니다.

스킬 템플릿에서는 이렇게 생겼습니다:
```
[STUB: 이 스킬이 하는 일을 한 문장으로 설명]
[STUB: 어떤 정보를 가져올지]
[STUB: 결과를 어떤 형식으로 보여줄지]
```

STUB을 하나씩 채우면 나만의 스킬이 완성됩니다.

### 왜 Template + STUB 방식인가?

처음부터 빈 파일에 스킬을 쓰는 것은 막막합니다. 하지만 "이 부분만 채우면 돼"라고 안내받으면 훨씬 쉽습니다. STUB 방식은 스킬 작성을 **빈칸 채우기 문제**로 바꿔줍니다.

## EXECUTE

### 단계 1: 스킬 뼈대 생성

`templates/my-tool-skill.md` 파일을 참고하여 나만의 스킬 뼈대를 만듭니다. Claude에게 요청합니다:

```
.claude/skills/my-tool/ 폴더를 만들고 SKILL.md를 만들어줘.
내 서비스의 핵심 기능은 [내 서비스 핵심 기능]이야.
이 기능을 AI에게 시키는 스킬을 만들고 싶어.
templates/my-tool-skill.md를 참고해서 STUB이 있는 뼈대부터 만들어줘.
```

### 단계 2: STUB 하나씩 채우기

생성된 파일에서 `[STUB: ...]` 부분을 순서대로 채웁니다. Claude에게 도움을 요청해도 좋습니다:

```
SKILL.md의 첫 번째 STUB을 채워줘.
이 스킬은 [내가 원하는 동작]을 해야 해.
```

모든 STUB이 채워질 때까지 반복합니다.

### 단계 3: 완성된 스킬 테스트

STUB을 모두 채웠으면 스킬을 호출해봅니다:

```
/my-tool
```

스킬이 의도한 대로 동작하는지 확인합니다. 다르게 동작한다면 Claude에게 수정을 요청합니다:

```
/my-tool을 실행했는데 [예상한 것]이 아니라 [실제 결과]가 나왔어.
SKILL.md를 수정해줘.
```

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "스킬 파일의 YAML frontmatter (--- 사이 내용)의 역할은 무엇인가요?",
      "header": "스킬 구조 이해",
      "options": [
        {"label": "스킬이 실행될 때 Claude에게 전달되는 지시 내용", "description": ""},
        {"label": "스킬의 이름과 설명 등 메타정보 (Claude가 스킬을 인식하는 데 사용)", "description": ""},
        {"label": "스킬의 버전과 업데이트 날짜 기록", "description": ""},
        {"label": "스킬에서 사용할 외부 서비스 연결 설정", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "스킬 템플릿에서 STUB이란 무엇인가요?",
      "header": "STUB 개념 이해",
      "options": [
        {"label": "스킬 실행 시 자동으로 삭제되는 임시 코드", "description": ""},
        {"label": "Claude가 채워주는 자동 완성 섹션", "description": ""},
        {"label": "나중에 직접 채워야 하는 빈칸 플레이스홀더", "description": ""},
        {"label": "오류 처리를 위한 예외 처리 코드", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번째 질문 → "스킬의 이름과 설명 등 메타정보 (Claude가 스킬을 인식하는 데 사용)"
- 2번째 질문 → "나중에 직접 채워야 하는 빈칸 플레이스홀더"

해설:
- YAML frontmatter: `---`로 둘러싸인 영역에는 `name`, `description` 등 스킬의 메타정보가 들어갑니다. Claude Code는 이 정보를 보고 `/my-tool`처럼 명령어를 입력했을 때 어떤 파일을 실행할지 결정합니다.
- STUB: 계약서의 `[성명]`처럼, 스킬 템플릿에서 여러분이 자신의 상황에 맞게 채워야 하는 빈칸입니다. 모든 STUB을 채우면 나만의 스킬이 완성됩니다.
