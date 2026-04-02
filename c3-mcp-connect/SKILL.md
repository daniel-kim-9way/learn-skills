---
name: c3-mcp-connect
description: "MCP 개념 이해 및 외부 도구 연결. C3 Block 3. Triggers: \"c3 mcp\", \"c3-mcp-connect\", \"MCP 연결\", \"외부 도구 연결\", \"슬랙 연결\""
---

# C3 Block 3: MCP — AI에게 도구 연결하기

## 학습 목표
- MCP가 무엇인지 설명할 수 있다
- `claude mcp add` 명령어로 외부 도구를 연결할 수 있다
- 연결된 도구를 Claude에게 요청하여 사용할 수 있다

## 사전 조건
- `/c3-memory-and-skill` 완료 (Memory + Skill 기능 이해)

## 기능 해금

🔓 새 기능 해금: MCP (Model Context Protocol)
Claude Code에 Slack, Notion, GitHub 등 외부 서비스를 연결하는 표준 프로토콜입니다. 연결하면 Claude가 그 서비스를 직접 읽고 쓸 수 있습니다.

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block3-mcp-connect.md의 EXPLAIN 섹션을 읽고 설명한다
   - MCP가 무엇인지 (USB-C 비유로 설명)
   - Host / Client / Server 모델을 간단하게 설명
   - 왜 MCP가 필요한지 (AI가 외부 세계와 연결되는 방법)
2. references/block3-mcp-connect.md의 EXECUTE 섹션을 따라 실행한다
   - `claude mcp add`로 도구 연결
   - 연결된 도구에 자연어로 요청
   - `/mcp` 명령어 탐색
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "MCP 연결을 마쳤습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block3-mcp-connect.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c3-my-skill`"
