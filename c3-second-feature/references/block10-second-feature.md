## PRE-QUIZ

사전 퀴즈입니다. 지금은 정답을 알려드리지 않습니다. 학습 후 얼마나 달라졌는지 비교해봅시다.

AskUserQuestion({
  "questions": [
    {
      "question": "[사전 Q1] 두 번째 기능을 구현할 때, 첫 번째 기능보다 쉬운 이유는 무엇일까요?",
      "header": "사전 퀴즈 1/3",
      "options": [
        {"label": "두 번째 기능이 항상 더 단순하기 때문에", "description": ""},
        {"label": "첫 번째 기능 구현으로 패턴을 익히고, 프로젝트 구조가 이미 갖춰졌기 때문에", "description": ""},
        {"label": "AI가 두 번째 요청을 더 잘 이해하기 때문에", "description": ""},
        {"label": "Rails가 자동으로 만들어주기 때문에", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[사전 Q2] Hook이란 무엇인가요?",
      "header": "사전 퀴즈 2/3",
      "options": [
        {"label": "코드에서 에러가 날 때 자동으로 알려주는 알람", "description": ""},
        {"label": "특정 이벤트(파일 저장 등)가 발생할 때 자동으로 실행되는 동작", "description": ""},
        {"label": "GitHub에 코드를 올리는 방법", "description": ""},
        {"label": "AI가 코드를 검토하는 기능", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[사전 Q3] 코드를 저장할 때마다 자동으로 테스트를 실행하면 어떤 장점이 있나요?",
      "header": "사전 퀴즈 3/3",
      "options": [
        {"label": "코드 파일 크기가 줄어든다", "description": ""},
        {"label": "배포 속도가 빨라진다", "description": ""},
        {"label": "실수를 즉시 발견할 수 있어서 버그가 쌓이지 않는다", "description": ""},
        {"label": "Claude가 코드를 더 잘 이해한다", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

---

## EXPLAIN

### 두 번째 기능은 왜 쉬운가?

첫 번째 기능을 만들 때 여러 것을 동시에 배웠습니다:
- Rails 프로젝트 구조 파악
- 모델, 컨트롤러, 뷰 생성 방법
- Claude와 소통하는 패턴
- 디버깅 방법

두 번째 기능을 만들 때는 이미 이 모든 것을 알고 있습니다. 게다가:
- 프로젝트 구조가 이미 갖춰져 있습니다
- 비슷한 코드 패턴을 참고할 수 있습니다
- Claude와의 소통 방식이 익숙해졌습니다

비유: 처음 자전거를 타는 것과 두 번째 자전거를 타는 것의 차이입니다. 균형 잡는 법을 이미 알고 있으면 훨씬 빠르게 배웁니다.

### Hook = 저장 시 자동 검사관

파일을 저장할 때마다 자동으로 무언가가 실행된다면 어떨까요?

**Hook**은 특정 이벤트가 발생했을 때 자동으로 실행되는 동작입니다. 개발에서 가장 유용한 Hook은 "파일 저장 시 자동 테스트"입니다.

이점:
- 코드를 망쳤을 때 즉시 알 수 있습니다
- 버그가 쌓이지 않습니다
- "이게 왜 갑자기 안 되지?" 상황을 예방합니다

Claude Code에서 Hook을 설정하면, 파일을 저장할 때마다 Claude가 코드를 검사하고 문제가 있으면 알려줍니다.

### 반복 구현 패턴

1. "이 기능을 만들어줘" 요청
2. Claude가 구현
3. 브라우저에서 확인
4. 수정 사항 요청
5. 완성!

이 패턴을 이제 빠르게 할 수 있게 됐습니다.

## EXECUTE

### 단계 1: 두 번째 핵심 기능 구현

C2 기획서의 두 번째 핵심 기능을 Claude에게 요청합니다:

```
첫 번째 기능([기능1])에 이어서 두 번째 핵심 기능인 [기능2]를 만들어줘.

기능 설명: [사용자 관점에서 이 기능이 무엇을 하는지]
필요한 UI: [어떤 화면/버튼/폼이 필요한지]
저장할 데이터: [어떤 정보를 저장해야 하는지]
```

첫 번째 기능 때보다 더 구체적으로 요청할수록 원하는 결과가 나옵니다.

### 단계 2: Hook 설정으로 자동 검사

Claude Code의 Hook 기능을 설정합니다. Claude에게 요청합니다:

```
파일을 저장할 때마다 자동으로 코드를 검사하는 Hook을 설정해줘.
.claude/settings.json에 저장 후 자동으로 lint 검사를 실행하는 hook을 추가해줘.
```

설정 완료 후 파일을 수정하고 저장하면 자동으로 검사가 실행됩니다.

테스트:
```
이 파일에 일부러 오류를 만들어봐. 저장하면 hook이 어떻게 반응하는지 보고 싶어.
```

Hook이 오류를 감지하고 알려주면 성공입니다.

---

## MAIN-QUIZ

### 기초 (3문항)

AskUserQuestion({
  "questions": [
    {
      "question": "두 번째 기능 구현이 첫 번째보다 빠른 이유는?",
      "header": "기초 1/3",
      "options": [
        {"label": "두 번째 기능이 항상 더 단순하기 때문에", "description": ""},
        {"label": "첫 번째 기능 구현으로 패턴을 익히고, 프로젝트 구조가 이미 갖춰졌기 때문에", "description": ""},
        {"label": "AI가 두 번째 요청에 더 많은 시간을 쓰기 때문에", "description": ""},
        {"label": "Rails 버전이 자동 업데이트 되기 때문에", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "Hook의 정의로 가장 정확한 것은?",
      "header": "기초 2/3",
      "options": [
        {"label": "코드를 GitHub에 올리는 기능", "description": ""},
        {"label": "특정 이벤트 발생 시 자동으로 실행되는 동작", "description": ""},
        {"label": "MCP 서버와의 연결 방법", "description": ""},
        {"label": "CLAUDE.md에 작성하는 지시 사항", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "파일 저장 시 자동 검사 Hook의 주요 장점은?",
      "header": "기초 3/3",
      "options": [
        {"label": "파일 크기를 줄여준다", "description": ""},
        {"label": "실수를 즉시 발견하여 버그가 누적되지 않는다", "description": ""},
        {"label": "배포 속도가 자동으로 빨라진다", "description": ""},
        {"label": "다른 개발자에게 코드를 자동 공유한다", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

### 중급 (3문항)

AskUserQuestion({
  "questions": [
    {
      "question": "두 번째 기능을 Claude에게 요청할 때, 첫 번째 기능보다 더 효과적인 요청 방법은?",
      "header": "중급 1/3",
      "options": [
        {"label": "더 짧고 간단하게 요청한다", "description": ""},
        {"label": "기술 용어를 사용해서 정확하게 요청한다", "description": ""},
        {"label": "첫 번째 기능의 패턴을 참고하면서 더 구체적인 요구사항을 제시한다", "description": ""},
        {"label": "첫 번째 기능 코드를 복사해서 수정해달라고 한다", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "Hook 설정 파일의 위치는 어디인가요?",
      "header": "중급 2/3",
      "options": [
        {"label": "app/hooks/settings.json", "description": ""},
        {"label": ".claude/settings.json", "description": ""},
        {"label": "config/hook.yml", "description": ""},
        {"label": "CLAUDE.md 파일 안에 포함", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "기능 구현 후 브라우저 테스트에서 확인해야 할 것은? (모두 선택)",
      "header": "중급 3/3",
      "options": [
        {"label": "기능이 실제로 동작하는가", "description": ""},
        {"label": "데이터가 저장/조회되는가", "description": ""},
        {"label": "에러 없이 작동하는가", "description": ""},
        {"label": "코드 줄 수가 적당한가", "description": ""}
      ],
      "multiSelect": true
    }
  ]
})

### 고급 시나리오 (3문항)

AskUserQuestion({
  "questions": [
    {
      "question": "시나리오: 두 번째 기능을 구현했는데, 첫 번째 기능에서 사용하던 User 모델과 연결이 필요합니다. Claude에게 어떻게 요청하는 것이 좋을까요?",
      "header": "고급 시나리오 1/3",
      "options": [
        {"label": "\"User 모델과 연결해줘\"라고만 말한다", "description": ""},
        {"label": "\"각 [새 기능 데이터]는 특정 사용자(User)에 속해야 해. user_id로 연결하고, 한 사용자가 여러 개를 가질 수 있는 관계로 설정해줘\"라고 구체적으로 요청한다", "description": ""},
        {"label": "직접 코드를 작성해서 연결한다", "description": ""},
        {"label": "연결하지 않고 일단 구현한다", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "시나리오: Hook을 설정했는데 파일 저장 시 매번 경고가 뜹니다. 코드에 실제 문제는 없어 보이는데, 어떻게 해야 할까요?",
      "header": "고급 시나리오 2/3",
      "options": [
        {"label": "Hook을 삭제한다", "description": ""},
        {"label": "경고 메시지를 Claude에게 보여주고 \"이 경고가 왜 나오는지, 무시해도 되는지 알려줘\"라고 묻는다", "description": ""},
        {"label": "파일을 저장하지 않는다", "description": ""},
        {"label": "경고를 무시하고 계속 개발한다", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "시나리오: 두 번째 기능을 완성했습니다. 다음 단계로 무엇을 해야 할까요?",
      "header": "고급 시나리오 3/3",
      "options": [
        {"label": "바로 배포한다", "description": ""},
        {"label": "git commit으로 현재 상태를 저장하고, GitHub에 push한다", "description": ""},
        {"label": "세 번째 기능 구현을 바로 시작한다", "description": ""},
        {"label": "코드를 Claude에게 리뷰 받은 후 git commit → push한다", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

---

정답:

**사전 퀴즈:**
- Q1 → "첫 번째 기능 구현으로 패턴을 익히고, 프로젝트 구조가 이미 갖춰졌기 때문에"
- Q2 → "특정 이벤트(파일 저장 등)가 발생할 때 자동으로 실행되는 동작"
- Q3 → "실수를 즉시 발견할 수 있어서 버그가 쌓이지 않는다"

**기초:**
- 1 → "첫 번째 기능 구현으로 패턴을 익히고, 프로젝트 구조가 이미 갖춰졌기 때문에"
- 2 → "특정 이벤트 발생 시 자동으로 실행되는 동작"
- 3 → "실수를 즉시 발견하여 버그가 누적되지 않는다"

**중급:**
- 1 → "첫 번째 기능의 패턴을 참고하면서 더 구체적인 요구사항을 제시한다"
- 2 → ".claude/settings.json"
- 3 → "기능이 실제로 동작하는가", "데이터가 저장/조회되는가", "에러 없이 작동하는가" (코드 줄 수는 중요하지 않음)

**고급 시나리오:**
- 1 → 구체적으로 관계를 설명하는 방식 (has many / belongs to)
- 2 → Claude에게 경고 메시지를 보여주고 설명을 듣는다
- 3 → Claude 리뷰 후 git commit → push (안전한 마무리)

**해설:**
- 사전 퀴즈 비교: 학습 전후 답변을 비교하여 어떤 개념이 명확해졌는지 확인하세요.
- 고급 시나리오: 정답 없이 "더 좋은 접근"을 선택합니다. 개발은 상황에 따라 다양한 정답이 있습니다.
