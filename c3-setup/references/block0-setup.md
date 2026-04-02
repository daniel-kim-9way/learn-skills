## EXPLAIN

Claude Code는 터미널(또는 에디터)에서 AI와 대화하면서 코딩하는 도구입니다. "이거 만들어줘"라고 말하면 AI가 코드를 작성하고, 파일을 만들고, 서버를 실행합니다.

### 설치 방법

| OS | 명령어 |
|----|--------|
| macOS / Linux / WSL | `curl -fsSL https://claude.ai/install.sh \| bash` |
| Windows (PowerShell) | `irm https://claude.ai/install.ps1 \| iex` |

### 오류 대응 패턴

코딩을 하다 보면 반드시 오류가 납니다. 비개발자에게 오류 메시지는 외계어처럼 보이지만, Claude Code에게는 해결의 실마리입니다.

패턴은 간단합니다:
1. 오류 메시지가 나타나면 **전체 복사**
2. Claude Code에 **붙여넣기**
3. "이 오류 해결해줘" 입력
4. Claude가 원인을 설명하고 해결

이 패턴 하나면 앞으로 만날 대부분의 오류를 넘길 수 있습니다.

## EXECUTE

### 단계 1: Claude Code 설치
터미널을 열고 아래 명령어를 입력합니다:

macOS/Linux:
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Windows (PowerShell):
```powershell
irm https://claude.ai/install.ps1 | iex
```

### 단계 2: 첫 실행과 로그인
```bash
claude
```
Claude가 인사하면 성공입니다. 계정 인증 안내가 나오면 따라 진행합니다.

### 단계 3: 첫 대화
Claude에게 이렇게 말해봅니다:
```
안녕! 나는 [내 서비스 이름]을 만들 거야. 반가워!
```

### 단계 4: 오류 체험 (의도적)
일부러 존재하지 않는 명령어를 입력합니다:
```
existnotcommand
```
오류가 나면 그 오류 메시지를 Claude에게 붙여넣고 "이게 뭐야?" 라고 물어봅니다.

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "Claude Code를 성공적으로 설치하고 첫 대화를 나눴나요?",
      "header": "설치 확인",
      "options": [
        {"label": "네, 모두 완료했습니다!", "description": "설치 + 첫 대화 + 오류 체험 모두 끝"},
        {"label": "설치는 했지만 오류 체험은 아직이에요", "description": "단계 4를 해보세요"},
        {"label": "설치에서 막혔어요", "description": "어떤 오류인지 알려주세요, 함께 해결합니다"}
      ],
      "multiSelect": false
    },
    {
      "question": "오류가 났을 때 가장 먼저 해야 할 행동은?",
      "header": "오류 대응 패턴",
      "options": [
        {"label": "구글에 검색한다", "description": ""},
        {"label": "오류 메시지를 Claude에 붙여넣는다", "description": ""},
        {"label": "프로그램을 껐다 켠다", "description": ""},
        {"label": "포기한다", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답: 2번째 질문 → "오류 메시지를 Claude에 붙여넣는다"
해설: 오류 메시지에는 무엇이 잘못됐는지 정보가 담겨 있습니다. Claude는 이 정보를 읽고 해결 방법을 알려줍니다. 구글 검색보다 빠르고 정확합니다.
