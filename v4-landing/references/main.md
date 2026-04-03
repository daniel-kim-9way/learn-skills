## EXPLAIN

### 랜딩 페이지란?

랜딩 페이지는 처음 방문한 사람이 "착지(land)"하는 페이지입니다. 광고를 클릭하거나, 링크를 공유받아서 처음 보는 그 화면입니다.

역할은 하나입니다: **낯선 사람을 고객으로 바꾸기.**

### 5섹션 구조: 설득의 여정

잘 만들어진 랜딩 페이지는 사람의 심리를 따라 설계됩니다:

```
[Hero] "이게 뭔데?" → 단 한 문장으로 서비스 설명
   ↓
[Problem] "맞아, 나 이게 불편했어" → 공감 유도
   ↓
[Solution] "이렇게 해결돼" → 해결책 제시
   ↓
[Features] "구체적으로 이런 게 돼" → 기능/혜택 나열
   ↓
[CTA] "지금 해봐" → 행동 유도
```

| 섹션 | 목적 | 핵심 질문 |
|------|------|----------|
| **Hero** | 첫인상, 한 줄 설명 | "무슨 서비스야?" |
| **Problem** | 공감, "나의 이야기"처럼 | "내 문제를 이해하는구나?" |
| **Solution** | 해결책, 희망 | "이게 내 문제를 해결해줘?" |
| **Features** | 구체적 기능, 신뢰 | "실제로 어떤 게 돼?" |
| **CTA** | 행동 촉구 | "어떻게 시작해?" |

### C1 메시징 활용하기

C1에서 정리한 `my-service-identity.md`(서비스 이름, 가치 선언문)와 `my-service-plan-v0.1.md`(기획서) 내용이 여기서 빛을 발합니다:
- **대상 사용자** (my-service-plan-v0.1.md 페르소나) → Hero 섹션의 "[누구]를 위한"
- **해결하는 문제** (my-service-plan-v0.1.md 문제 정의) → Problem 섹션
- **핵심 가치** (my-service-identity.md 가치 선언문) → Solution 섹션
- **주요 기능** (my-service-design-v1.0.md Must 기능) → Features 섹션

C1에서 "왜 만드는가"를 고민한 덕분에 랜딩 페이지 작성이 훨씬 수월합니다.

### Hero 섹션 작성 공식

Hero는 가장 중요합니다. 8초 안에 "이게 나한테 필요해"를 느끼게 해야 합니다.

공식: **[누구를] [어떤 문제에서] [어떻게 구해주는가]**

예시:
- "바쁜 1인 사업자를 위한 자동 고객 관리 도구"
- "혼자 공부하는 수험생의 학습 계획을 AI가 잡아드립니다"

## EXECUTE

### 단계 1: Hero 섹션 만들기

먼저 `my-service-identity.md`와 `my-service-plan-v0.1.md`를 읽어 메시징 소재를 파악합니다.

Claude Code에서:
```
my-service-identity.md를 읽고, 랜딩 페이지 Hero 섹션을 만들어줘.
- 서비스 한 줄 설명 (가치 선언문 기반)
- 서브타이틀로 핵심 가치 1문장
- CTA 버튼 ("시작하기" 또는 "무료로 체험하기")
- Tailwind CSS로 깔끔하게
```

### 단계 2: Problem + Solution 섹션

```
Problem 섹션과 Solution 섹션을 만들어줘.
- Problem: 타겟 사용자가 공감할 수 있는 불편함 3가지
- Solution: 우리 서비스가 그 불편함을 어떻게 해결하는지
- 아이콘이나 이모지를 활용해서 시각적으로
```

### 단계 3: Features + CTA 섹션

```
Features 섹션과 CTA 섹션을 만들어줘.
- Features: 핵심 기능 3~4개를 카드 형태로
- CTA: 마지막 행동 촉구 (가입 버튼 + 안심 문구)
- "지금 바로 시작하세요" 같은 강한 CTA
```

### 단계 4: 모바일 반응형 확인

브라우저에서 개발자 도구를 엽니다 (F12):
- Chrome: 상단 "Toggle device toolbar" (Ctrl+Shift+M)
- 화면을 좁혀서 내용이 잘 보이는지 확인

문제가 있으면:
```
모바일에서 [어떤 부분]이 깨져 보여. 반응형으로 수정해줘.
```

### 단계 5: 전체 페이지 리뷰

완성된 랜딩 페이지를 처음부터 끝까지 스크롤하며 읽어봅니다. 처음 보는 사람 입장에서 "이 서비스가 뭔지, 왜 필요한지, 어떻게 시작하는지"가 자연스럽게 전달되는지 확인합니다.

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "랜딩 페이지 5섹션 중 가장 처음에 오는 섹션은?",
      "header": "5섹션 구조",
      "options": [
        {"label": "CTA (행동 유도)", "description": ""},
        {"label": "Problem (문제 제시)", "description": ""},
        {"label": "Hero (첫인상, 한 줄 설명)", "description": ""},
        {"label": "Features (기능 나열)", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "Problem 섹션의 주요 목적은?",
      "header": "섹션 역할",
      "options": [
        {"label": "기능을 자세히 나열하기", "description": ""},
        {"label": "공감을 일으켜 '내 이야기'처럼 느끼게 하기", "description": ""},
        {"label": "가격을 안내하기", "description": ""},
        {"label": "회사를 소개하기", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번 → "Hero (첫인상, 한 줄 설명)"
- 2번 → "공감을 일으켜 '내 이야기'처럼 느끼게 하기"

해설:
- Hero: 방문자가 스크롤 없이 보는 유일한 섹션입니다. 8초 안에 "이게 내게 필요해"를 느끼게 해야 합니다.
- Problem: 기능 소개 전에 먼저 공감을 얻어야 합니다. "맞아, 나 이게 불편했어"라는 반응을 이끌어내면 그 다음 Solution이 더 설득력 있게 다가옵니다.
