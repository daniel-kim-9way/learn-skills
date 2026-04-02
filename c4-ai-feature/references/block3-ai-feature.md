## EXPLAIN

### API란? 레스토랑 주문 비유

API(Application Programming Interface)는 어렵게 들리지만 사실 우리가 매일 하는 행동과 같습니다.

레스토랑을 상상해보세요:
- **손님(나의 서비스)**: "파스타 하나 주세요"
- **웨이터(API)**: 주문을 받아 주방에 전달
- **주방(Claude AI)**: 요리해서 다시 전달
- **웨이터(API)**: 음식을 손님에게 전달

내 서비스가 직접 AI를 만들 필요 없이, Claude에게 "이 질문에 답해줘"라고 요청하면 Claude가 답을 돌려주는 것입니다. 그 연결 통로가 API입니다.

### Claude API 구조

Claude API는 이런 방식으로 동작합니다:

```
나의 서비스 → (API 키로 인증) → Claude AI → 답변 반환 → 나의 서비스
```

**API 키**는 마치 회원 카드 같습니다. "이 요청은 내가 보내는 거야"라고 증명하는 비밀 번호입니다. API 키가 있어야 Claude를 사용할 수 있고, 사용량에 따라 요금이 부과됩니다.

### 서비스에 AI를 추가하면?

내 서비스에 AI가 붙으면 사용자 경험이 완전히 달라집니다.

예시:
- 독서 기록 앱 → "이 책의 핵심 메시지가 뭐야?" 물어볼 수 있음
- 할 일 관리 앱 → "오늘 할 일 중 우선순위를 AI가 정해줘"
- 식단 관리 앱 → "이 재료로 만들 수 있는 레시피 추천해줘"

AI는 단순한 기능이 아니라 **서비스의 두뇌**가 됩니다.

### Plugin이란?

Plugin은 자주 쓰는 AI 기능을 패키징해서 **한 줄 명령어**로 재사용할 수 있게 만드는 도구입니다.

예를 들어, `claude --plugin my-ai-feature`처럼 실행하거나, Claude Code 워크플로우에서 플러그인을 호출할 수 있습니다. 복잡한 AI 연동 코드를 매번 작성하지 않아도 됩니다.

## EXECUTE

### 단계 1: API 키 발급
1. https://console.anthropic.com 접속 (Anthropic 계정으로 로그인)
2. 왼쪽 메뉴 → "API Keys" 클릭
3. "Create Key" 버튼 클릭
4. 이름 입력 (예: "my-service-key") → 생성
5. **발급된 키를 안전한 곳에 복사** (다시 볼 수 없습니다!)

⚠️ API 키는 절대 소스 코드에 직접 넣지 마세요. 환경 변수로 관리합니다.

### 단계 2: Claude가 AI 기능 추가
Claude Code에서 아래와 같이 요청합니다:

```
내 서비스에 AI 기능을 추가해줘.
Claude API를 사용해서 [원하는 AI 기능]을 구현해줘.

예시:
- 사용자가 텍스트를 입력하면 Claude가 분석/조언해주는 기능
- 입력된 데이터를 바탕으로 Claude가 제안을 해주는 기능

API 키는 환경 변수로 관리해줘:
- 환경 변수 이름: ANTHROPIC_API_KEY
- .env 파일에 저장하고, .gitignore에 추가해줘
```

Claude가 코드를 작성하면:
1. `.env` 파일을 열어서 `ANTHROPIC_API_KEY=발급받은키` 입력
2. 서버를 재시작하고 AI 기능 테스트

### 단계 3: Plugin으로 패키징
AI 기능이 잘 동작하면 Plugin으로 만들어서 재사용하기 쉽게 합니다:

```
방금 만든 AI 기능을 Plugin으로 패키징해줘.
플러그인 이름: [서비스명]-ai
설명: [이 플러그인이 하는 일]
나중에 다른 프로젝트에서도 쉽게 재사용할 수 있게 만들어줘.
```

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "API 키를 관리하는 올바른 방법은 무엇인가요?",
      "header": "API 키 보안",
      "options": [
        {"label": "소스 코드에 직접 넣어서 편하게 사용한다", "description": ""},
        {"label": "환경 변수(.env 파일)에 저장하고 .gitignore에 추가한다", "description": ""},
        {"label": "README 파일에 써두어 팀원이 쉽게 볼 수 있게 한다", "description": ""},
        {"label": "매번 새로 발급받아서 사용한다", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "API가 하는 역할을 가장 잘 설명한 것은 무엇인가요?",
      "header": "API 개념",
      "options": [
        {"label": "서비스의 디자인을 담당하는 도구", "description": ""},
        {"label": "두 서비스가 대화할 수 있게 연결해주는 통로 (웨이터 역할)", "description": ""},
        {"label": "데이터베이스에 데이터를 저장하는 방법", "description": ""},
        {"label": "웹사이트를 배포하는 도구", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번째 질문 → "환경 변수(.env 파일)에 저장하고 .gitignore에 추가한다"
- 2번째 질문 → "두 서비스가 대화할 수 있게 연결해주는 통로 (웨이터 역할)"

해설:
- API 키 보안: 소스 코드에 API 키를 직접 넣으면 GitHub에 올릴 때 공개될 수 있습니다. .env 파일은 로컬에만 존재하고 .gitignore로 업로드를 막아 보안을 유지합니다.
- API 역할: API는 내 서비스와 외부 서비스(Claude AI 등) 사이를 연결하는 표준화된 통로입니다. 레스토랑의 웨이터처럼 요청을 전달하고 결과를 가져옵니다. 덕분에 AI를 직접 만들지 않아도 AI 기능을 사용할 수 있습니다.
