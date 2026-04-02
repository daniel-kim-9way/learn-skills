## EXPLAIN

### 모호한 요청이 실패하는 이유

Claude에게 "로그인 기능 만들어줘"라고 말하면 어떻게 될까요?

Claude는 만들기는 만들지만, 이런 결과가 나올 수 있습니다:
- 이메일/비밀번호 로그인을 만들었는데 나는 소셜 로그인을 원했다
- 기본 UI를 만들었는데 나는 내 브랜드 색상을 원했다
- 기능은 됐는데 내 기존 코드와 스타일이 전혀 다르다

문제는 Claude가 아닙니다. 요청이 **모호**했기 때문입니다. Claude는 여러분의 머릿속에 있는 구체적인 이미지를 볼 수 없습니다.

### Hypothesis-as-Options 패턴

좋은 지시는 모호함을 제거합니다. 가장 효과적인 방법이 **Hypothesis-as-Options** 패턴입니다.

방법: 내가 원하는 것의 **가능성들**을 선택지로 제시하고, Claude에게 가장 적합한 것을 선택하거나 더 제안하게 합니다.

❌ 나쁜 예:
```
로그인 기능 만들어줘.
```

✅ 좋은 예:
```
로그인 기능을 만들어야 해. 아래 중 어떤 방식이 내 서비스에 더 맞을까?

A. 이메일/비밀번호 로그인 (전통적, 관리 필요)
B. 카카오/구글 소셜 로그인 (간편, 외부 의존)
C. 이메일 매직 링크 (비밀번호 없음, 이메일 필요)

내 서비스는 30~40대 직장인 대상이고, 빠른 가입을 원해.
```

이 패턴의 장점:
- 내 의도를 Claude가 정확히 파악
- Claude가 각 옵션의 장단점을 분석해서 추천
- 결정이 빨라지고 재작업이 줄어듦

### 요구사항의 5가지 차원

좋은 요구사항에는 항상 이 5가지가 담겨 있습니다:

| 차원 | 질문 | 예시 |
|------|------|------|
| **Who** | 누가 쓰는가? | 30~40대 직장인 |
| **What** | 무엇을 원하는가? | 빠른 로그인 |
| **Why** | 왜 필요한가? | 재방문 시 편의성 |
| **Constraint** | 제약 조건은? | 모바일 우선 |
| **Quality** | 어느 수준? | MVP 수준이면 충분 |

### Teams: AI가 요구사항을 검토한다

Teams 기능을 쓰면 한 AI가 "개발자 역할", 다른 AI가 "기획 검토 역할"을 맡을 수 있습니다.

예를 들어:
- AI 1 (기획자): "이 요구사항에 빠진 게 뭔지 찾아줘"
- AI 2 (개발자): "이 요구사항대로 코드 짜줘"

덕분에 모호한 부분을 코딩 전에 잡아낼 수 있습니다.

## EXECUTE

### Pre-Quiz (사전 이해 측정)
본격적인 학습 전에 현재 이해를 확인합니다.

AskUserQuestion({
  "questions": [
    {
      "question": "[Pre-Quiz 1] Claude에게 '로그인 기능 만들어줘'라고 하면 왜 원하는 결과가 안 나올 수 있나요?",
      "header": "Pre-Quiz: 모호한 요청",
      "options": [
        {"label": "Claude가 로그인을 몰라서", "description": ""},
        {"label": "요청에 구체적인 정보(방식, 스타일, 제약)가 없어서", "description": ""},
        {"label": "로그인은 AI가 만들 수 없어서", "description": ""},
        {"label": "명령어가 잘못돼서", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[Pre-Quiz 2] 좋은 요구사항에 반드시 포함되어야 하는 것은? (모두 선택)",
      "header": "Pre-Quiz: 요구사항 요소",
      "options": [
        {"label": "누가 쓰는지 (Who)", "description": ""},
        {"label": "무엇을 원하는지 (What)", "description": ""},
        {"label": "개발자의 이름", "description": ""},
        {"label": "제약 조건 (Constraint)", "description": ""}
      ],
      "multiSelect": true
    },
    {
      "question": "[Pre-Quiz 3] Hypothesis-as-Options 패턴이란?",
      "header": "Pre-Quiz: 패턴 이해",
      "options": [
        {"label": "AI에게 여러 번 같은 질문을 반복하는 방법", "description": ""},
        {"label": "원하는 것의 가능성을 선택지로 제시해 AI가 최적 옵션을 추천하게 하는 방법", "description": ""},
        {"label": "AI가 생성한 코드를 가설로 보고 테스트하는 방법", "description": ""},
        {"label": "다른 서비스의 기능을 분석해서 모방하는 방법", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

---

### Clarify 패턴 체험
내 서비스에서 다음에 만들 기능을 Claude에게 **나쁜 방식**으로 요청해봅니다:

```
[기능 이름] 만들어줘.
```

Claude의 응답을 확인합니다. 그런 다음, **Hypothesis-as-Options 패턴**으로 다시 요청합니다:

```
[기능 이름]을 만들어야 해. 아래 중 어떤 방식이 내 서비스에 맞을까?

A. [옵션 1 설명]
B. [옵션 2 설명]
C. [옵션 3 설명]

내 서비스: [서비스 설명]
대상 사용자: [사용자 설명]
```

두 응답의 차이를 느껴봅니다.

### Teams로 요구사항 검토
Claude Code에서 아래와 같이 요청합니다:

```
Teams 기능을 사용해서 내 요구사항을 검토해줘.

기획자 역할 AI: 아래 요구사항에서 모호하거나 빠진 부분을 찾아줘
개발자 역할 AI: 이 요구사항이 충분히 명확한지 판단해줘

요구사항:
[내가 만들고 싶은 기능 설명]
```

## QUIZ

메인 퀴즈 (9문항: 기본 3 + 심화 3 + 시나리오 3)

AskUserQuestion({
  "questions": [
    {
      "question": "[기본 1] Clarify 패턴이 필요한 가장 근본적인 이유는?",
      "header": "기본: Clarify 필요성",
      "options": [
        {"label": "AI가 느려서 빠르게 소통해야 하기 때문에", "description": ""},
        {"label": "AI는 내 머릿속의 구체적인 의도를 알 수 없어서", "description": ""},
        {"label": "명령어가 길수록 AI가 더 잘 이해하기 때문에", "description": ""},
        {"label": "영어로 질문해야 AI가 더 잘 이해하기 때문에", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[기본 2] Hypothesis-as-Options 패턴에서 '옵션'을 제시하는 이유는?",
      "header": "기본: 옵션 제시 이유",
      "options": [
        {"label": "AI에게 선택권을 주어 자율성을 높이기 위해", "description": ""},
        {"label": "모호함을 구체화하고 AI가 의도를 정확히 파악하도록 돕기 위해", "description": ""},
        {"label": "여러 기능을 동시에 만들기 위해", "description": ""},
        {"label": "코드 작성 시간을 줄이기 위해", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[기본 3] 좋은 요구사항의 5가지 차원이 아닌 것은?",
      "header": "기본: 요구사항 차원",
      "options": [
        {"label": "Who (누가 쓰는가)", "description": ""},
        {"label": "What (무엇을 원하는가)", "description": ""},
        {"label": "When (언제 완성되는가)", "description": ""},
        {"label": "Why (왜 필요한가)", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[심화 1] 요구사항에 'Who'가 명시되어야 하는 이유는?",
      "header": "심화: Who의 중요성",
      "options": [
        {"label": "법적 책임 소재를 명확히 하기 위해", "description": ""},
        {"label": "사용자에 따라 UI, 기능, 언어가 달라지기 때문에", "description": ""},
        {"label": "개발자가 누구에게 물어볼지 알기 위해", "description": ""},
        {"label": "마케팅 자료에 사용하기 위해", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[심화 2] Teams 기능이 요구사항 검토에서 유용한 이유는?",
      "header": "심화: Teams 활용",
      "options": [
        {"label": "여러 AI가 동시에 코드를 작성하기 때문에", "description": ""},
        {"label": "한 AI가 기획 검토, 다른 AI가 개발로 역할 분담해 코딩 전에 문제를 잡을 수 있어서", "description": ""},
        {"label": "Teams는 무료라서", "description": ""},
        {"label": "AI끼리 서로 경쟁해서 더 좋은 결과가 나와서", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[심화 3] 다음 중 Constraint(제약 조건)에 해당하는 것은?",
      "header": "심화: 제약 조건 식별",
      "options": [
        {"label": "사용자가 로그인할 수 있어야 한다", "description": ""},
        {"label": "모바일 우선, 3G 환경에서도 3초 이내에 로딩되어야 한다", "description": ""},
        {"label": "사용자는 30대 직장인이다", "description": ""},
        {"label": "빠른 가입을 원한다", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[시나리오 1] 팀원이 '대시보드 만들어줘'라고 요청했습니다. Hypothesis-as-Options 패턴으로 명확화하려면?",
      "header": "시나리오: 명확화 적용",
      "options": [
        {"label": "바로 만들기 시작한다", "description": ""},
        {"label": "\"어떤 대시보드? A. 판매 통계, B. 사용자 현황, C. 시스템 모니터링 — 어떤 걸 원해?\"라고 물어본다", "description": ""},
        {"label": "대시보드 관련 문서를 먼저 읽는다", "description": ""},
        {"label": "다른 서비스의 대시보드를 복사한다", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[시나리오 2] Claude에게 '결제 기능 추가해줘'라고 했더니 원하지 않는 방식으로 구현됐습니다. 원인은?",
      "header": "시나리오: 실패 분석",
      "options": [
        {"label": "Claude가 결제를 모르기 때문에", "description": ""},
        {"label": "요청에 결제 방식(카드/간편결제), 금액 구조, 국가 등 맥락이 없었기 때문에", "description": ""},
        {"label": "결제는 AI로 구현할 수 없어서", "description": ""},
        {"label": "서버가 느려서", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[시나리오 3] 새 기능의 요구사항을 작성했습니다. 코딩 전에 Teams로 검토받는 순서는?",
      "header": "시나리오: Teams 워크플로우",
      "options": [
        {"label": "코딩 → Teams 검토 → 수정", "description": ""},
        {"label": "요구사항 작성 → Teams 기획 검토 → 명확화 → 코딩", "description": ""},
        {"label": "Teams 검토 → 요구사항 작성 → 코딩", "description": ""},
        {"label": "코딩 → 배포 → Teams 검토", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 기본 1 → "AI는 내 머릿속의 구체적인 의도를 알 수 없어서"
- 기본 2 → "모호함을 구체화하고 AI가 의도를 정확히 파악하도록 돕기 위해"
- 기본 3 → "When (언제 완성되는가)" (5가지 차원: Who, What, Why, Constraint, Quality)
- 심화 1 → "사용자에 따라 UI, 기능, 언어가 달라지기 때문에"
- 심화 2 → "한 AI가 기획 검토, 다른 AI가 개발로 역할 분담해 코딩 전에 문제를 잡을 수 있어서"
- 심화 3 → "모바일 우선, 3G 환경에서도 3초 이내에 로딩되어야 한다"
- 시나리오 1 → "'어떤 대시보드? A. 판매 통계, B. 사용자 현황, C. 시스템 모니터링 — 어떤 걸 원해?'라고 물어본다"
- 시나리오 2 → "요청에 결제 방식(카드/간편결제), 금액 구조, 국가 등 맥락이 없었기 때문에"
- 시나리오 3 → "요구사항 작성 → Teams 기획 검토 → 명확화 → 코딩"
