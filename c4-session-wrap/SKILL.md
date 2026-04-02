---
name: c4-session-wrap
description: "Multi-Agent 패턴으로 세션 마무리 자동화. C4 Block 9. Triggers: \"c4 세션마무리\", \"c4-session-wrap\", \"multi-agent\", \"멀티에이전트\", \"c4 block 9\""
---

# C4 Block 9: Multi-Agent — 여러 AI가 함께 일하기

## 학습 목표
- Multi-Agent 패턴(병렬 → 순차)의 개념을 이해한다
- 2-Phase 패턴으로 세션 마무리 스킬을 만들 수 있다
- 4-에이전트 패턴으로 실제 병렬 작업을 실행할 수 있다

## 사전 조건
- `/c4-launch` 완료 (서비스 오픈 완료)

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block9-session-wrap.md의 EXPLAIN 섹션을 읽고 설명한다
   - Multi-Agent 패턴이란 (병렬 vs 순차)
   - 2-Phase 패턴 구조
   - 언제 Multi-Agent가 유용한가
2. references/block9-session-wrap.md의 EXECUTE 섹션을 따라 실행한다
   - 4-에이전트 패턴 학습
   - 세션 마무리 스킬 만들기
   - 병렬 에이전트 실행 체험
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "Multi-Agent 패턴을 익혔습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block9-session-wrap.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c4-compound`"
