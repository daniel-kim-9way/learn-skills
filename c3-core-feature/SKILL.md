---
name: c3-core-feature
description: "C2 기획서를 바탕으로 핵심 기능 구현. C3 Block 8. Triggers: \"c3 핵심기능\", \"c3-core-feature\", \"기능 구현\", \"첫 기능 만들기\", \"서비스 기능 개발\""
---

# C3 Block 8: 핵심 기능 ① 구현하기

## 학습 목표
- C2에서 만든 기획서를 Claude에게 전달하여 실제 기능을 구현할 수 있다
- "Claude에게 무엇을 만들지 말하는" 패턴을 익힌다
- 브라우저에서 구현된 기능을 확인하고 피드백을 줄 수 있다

## 사전 조건
- `/c3-first-page` 완료 (홈페이지 + 인증 구현 경험)
- C2에서 작성한 기획 문서 (기능 명세)

## 기능 해금 (외부 API가 필요한 경우)

🔓 새 기능 해금: MCP (외부 API 연결)
핵심 기능이 외부 서비스(날씨 API, 지도, 결제 등)와 연결이 필요하다면 MCP로 연결할 수 있습니다. Block 3에서 배운 `claude mcp add` 명령을 활용하세요.

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block8-core-feature.md의 EXPLAIN 섹션을 읽고 설명한다
   - C2 기획서 → 동작하는 코드로 가는 흐름
   - "Claude에게 무엇을 만들지 말하는" 패턴
   - 구현 후 테스트하고 피드백 주는 사이클
2. references/block8-core-feature.md의 EXECUTE 섹션을 따라 실행한다
   - C2 기획서를 Claude에게 공유
   - Claude가 핵심 기능 구현
   - 브라우저에서 테스트
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "첫 번째 핵심 기능을 구현했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block8-core-feature.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c3-database`"
