---
name: c4-ai-feature
description: "Claude API로 AI 기능 추가. C4 Block 3. Triggers: \"c4 ai기능\", \"c4-ai-feature\", \"claude api\", \"클로드 api\", \"c4 block 3\""
---

# C4 Block 3: AI 기능 추가 — Claude API 연결

## 학습 목표
- API가 무엇인지 이해한다 (레스토랑 주문 비유)
- Claude API 키를 발급받고 서비스에 연결할 수 있다
- AI 기능을 Plugin으로 패키징하는 방법을 익힌다

## 사전 조건
- `/c4-landing` 완료 (랜딩 페이지 완성)
- Anthropic 계정 (Claude Pro/Max 보유)

## 기능 해금

🔓 새 기능 해금: **Plugin**

이번 블록을 완료하면 Claude Code의 Plugin 기능을 사용할 수 있습니다. Plugin은 외부 AI 서비스(Claude API, GPT 등)를 Claude Code 워크플로우에 통합하는 방법입니다.

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block3-ai-feature.md의 EXPLAIN 섹션을 읽고 설명한다
   - API가 무엇인지 (레스토랑 주문 비유)
   - Claude API의 구조 (요청 → 응답)
   - Plugin이란 무엇인지
2. references/block3-ai-feature.md의 EXECUTE 섹션을 따라 실행한다
   - API 키 발급
   - Claude가 AI 기능 추가
   - Plugin으로 패키징
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "AI 기능을 추가했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block3-ai-feature.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c4-payment`"
