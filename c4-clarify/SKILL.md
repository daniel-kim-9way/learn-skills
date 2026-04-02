---
name: c4-clarify
description: "Claude에게 명확하게 지시하는 Clarify 패턴. C4 Block 5. Triggers: \"c4 clarify\", \"c4-clarify\", \"clarify 패턴\", \"명확한 지시\", \"c4 block 5\""
---

# C4 Block 5: Clarify 패턴 — 명확한 지시의 기술

## 학습 목표
- 모호한 요청이 왜 실패하는지 이해한다
- Hypothesis-as-Options 패턴으로 요구사항을 명확히 할 수 있다
- Teams 기능을 활용해 AI가 요구사항을 검토하는 방법을 익힌다

## 사전 조건
- `/c4-payment` 완료 (결제 연동 경험)

## 기능 해금

🔓 새 기능 해금: **Teams**

이번 블록을 완료하면 Claude Code의 Teams 기능을 사용할 수 있습니다. Teams는 여러 AI 에이전트가 팀으로 일하게 하는 기능입니다. 한 에이전트가 기획을 검토하고, 다른 에이전트가 코딩하는 방식으로 협업합니다.

## 교수법: Quiz-First

이 블록은 Quiz-First 방식으로 진행됩니다. 먼저 퀴즈로 현재 이해를 측정하고, 학습 후 더 깊은 퀴즈로 이해를 확인합니다.

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block5-clarify.md의 EXPLAIN 섹션을 읽고 설명한다
   - 모호한 요청이 실패하는 이유
   - Hypothesis-as-Options 패턴
   - Teams 기능 소개
2. references/block5-clarify.md의 EXECUTE 섹션을 따라 실행한다
   - Pre-Quiz (3문항) — 사전 이해 측정
   - Clarify 패턴 직접 체험
   - Teams로 요구사항 검토
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "Clarify 패턴을 체험했습니다. '다음'을 입력하면 메인 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block5-clarify.md의 QUIZ 섹션 메인 퀴즈 출제 (9문항)
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 브릿지 메시지 출력:
   - "서비스가 결제까지 되고, AI에게 명확히 지시할 수 있습니다! 🎉 남은 건 세상에 내보내는 것뿐입니다."
4. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c4-deploy`"
