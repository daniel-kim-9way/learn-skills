## EXPLAIN

### MCP란? — USB-C 비유

예전에는 폰마다 충전기가 달랐습니다. 삼성 폰, 아이폰, 갤럭시 탭… 각각 다른 케이블이 필요했죠. 그런데 USB-C가 나오면서 **하나의 표준 포트**로 모든 기기를 연결할 수 있게 됐습니다.

**MCP(Model Context Protocol)**는 AI 세계의 USB-C입니다.

Slack, Notion, GitHub, 데이터베이스… 각각 AI와 연결하려면 원래 전부 다른 방식이 필요했습니다. MCP는 이 모든 연결을 **하나의 표준 방식**으로 통일합니다.

### Host / Client / Server 모델

MCP를 이해하는 세 개의 역할:

| 역할 | 의미 | 예시 |
|------|------|------|
| **Host** | AI가 실행되는 환경 | Claude Code (여러분의 터미널) |
| **Client** | 연결을 요청하는 쪽 | Claude 자체 |
| **Server** | 연결되는 서비스 | Slack MCP 서버, Notion MCP 서버 |

쉽게 말하면: Claude Code(Host)가 Claude(Client)를 통해 Slack(Server)에 연결하는 것입니다.

### 왜 MCP가 필요한가?

MCP 없이는 Claude가 여러분의 컴퓨터 파일만 볼 수 있습니다. MCP를 연결하면:
- Slack 메시지를 읽고 쓸 수 있다
- Notion 문서를 업데이트할 수 있다
- GitHub 이슈를 확인하고 PR을 만들 수 있다
- 데이터베이스를 직접 조회할 수 있다

AI가 여러분의 업무 도구와 **직접 연결**되는 것입니다.

## EXECUTE

### 단계 1: MCP 서버 추가

Claude Code에서 아래 명령어로 Slack 또는 Notion을 연결합니다.

**Slack 연결:**
```bash
claude mcp add slack -- npx -y @modelcontextprotocol/server-slack
```

**Notion 연결 (Slack이 없다면):**
```bash
claude mcp add notion -- npx -y @modelcontextprotocol/server-notion
```

연결 후 Claude Code를 재시작합니다:
```bash
# Claude Code 종료 후 재시작
claude
```

### 단계 2: 연결 확인 및 자연어 요청

Claude에게 자연어로 요청해봅니다:

**Slack 연결 시:**
```
내 슬랙 채널 목록 보여줘
```

**Notion 연결 시:**
```
내 Notion 워크스페이스에 있는 페이지 목록 보여줘
```

Claude가 실제 데이터를 가져오면 MCP 연결이 성공한 것입니다.

### 단계 3: /mcp 명령어 탐색

Claude Code에서 `/mcp`를 입력하면 현재 연결된 MCP 서버 목록을 볼 수 있습니다:

```
/mcp
```

연결된 서버 이름과 사용 가능한 도구 목록이 표시됩니다. 어떤 것들을 할 수 있는지 탐색해보세요.

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "MCP(Model Context Protocol)란 무엇인가요?",
      "header": "MCP 개념 이해",
      "options": [
        {"label": "AI가 코드를 작성할 때 사용하는 프로그래밍 언어", "description": ""},
        {"label": "AI와 외부 서비스(Slack, Notion 등)를 연결하는 표준 프로토콜", "description": ""},
        {"label": "코드의 오류를 자동으로 검사하는 도구", "description": ""},
        {"label": "GitHub에 코드를 올리는 방법", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "Claude Code에서 새로운 MCP 서버를 추가하는 명령어는?",
      "header": "MCP 명령어",
      "options": [
        {"label": "claude install [서비스명]", "description": ""},
        {"label": "claude connect [서비스명]", "description": ""},
        {"label": "claude mcp add [서비스명]", "description": ""},
        {"label": "claude plugin [서비스명]", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번째 질문 → "AI와 외부 서비스(Slack, Notion 등)를 연결하는 표준 프로토콜"
- 2번째 질문 → "claude mcp add [서비스명]"

해설:
- MCP: USB-C처럼 하나의 표준 방식으로 AI와 다양한 서비스를 연결합니다. 덕분에 Claude가 Slack, Notion, GitHub 등을 직접 읽고 쓸 수 있게 됩니다.
- 명령어: `claude mcp add`는 새 MCP 서버를 Claude Code에 등록하는 명령어입니다. 등록 후 Claude Code를 재시작하면 Claude가 해당 서비스에 접근할 수 있습니다.
