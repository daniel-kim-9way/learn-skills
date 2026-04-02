---
name: c3-second-feature
description: "핵심 기능 ② 구현 + Quiz-First 방식. C3 Block 10. Triggers: \"c3 두번째기능\", \"c3-second-feature\", \"기능 추가\", \"두 번째 기능\", \"Hook 설정\""
---

# C3 Block 10: 핵심 기능 ② + Hook으로 자동 검사

## 학습 목표
- 반복적인 기능 구현 패턴을 체득할 수 있다
- Quiz-First 방식으로 학습 효과를 높일 수 있다
- Hook을 설정하여 저장 시 자동으로 코드를 검사할 수 있다

## 사전 조건
- `/c3-database` 완료 (데이터베이스 및 모델 구현 경험)

## 기능 해금

🔓 새 기능 해금: Hook (자동 실행)
파일을 저장할 때마다 자동으로 테스트나 코드 품질 검사가 실행됩니다. "저장하면 자동으로 확인해줘" 패턴으로 실수를 줄이고 품질을 높일 수 있습니다.

## STOP PROTOCOL

이 스킬은 3-Phase STOP Protocol을 따릅니다 (Quiz-First 방식).

### Phase A (Turn 1) — Pre-Quiz
1. references/block10-second-feature.md의 PRE-QUIZ 섹션 퀴즈 출제 (3문항)
2. 답변을 받되 정답/오답 여부를 알려주지 않는다 (학습 후 비교용)
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "사전 퀴즈 완료! 학습 후 얼마나 달라지는지 확인해봅시다. '다음'을 입력하면 학습을 시작합니다."

### Phase B (Turn 2) — 학습 + 실행
1. references/block10-second-feature.md의 EXPLAIN 섹션을 읽고 설명한다
   - 반복 구현 패턴이 왜 첫 번째보다 쉬운지
   - Hook이 무엇인지 (저장 시 자동 실행되는 검사)
   - 두 번째 기능 구현 전략
2. references/block10-second-feature.md의 EXECUTE 섹션을 따라 실행한다
   - 두 번째 핵심 기능 구현
   - Hook 설정으로 자동 검사
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "두 번째 기능을 구현하고 Hook도 설정했습니다. '다음'을 입력하면 최종 퀴즈로 넘어갑니다."

### Phase C (Turn 3) — Main Quiz + Bridge
1. references/block10-second-feature.md의 MAIN-QUIZ 섹션 퀴즈 출제 (9문항: 기초 3 + 중급 3 + 고급 시나리오 3)
2. 학생 답변에 피드백한다 (Phase A의 사전 퀴즈 답변과 비교하여 성장을 보여준다)
3. Bridge 메시지 출력:
   "핵심 기능 2개가 동작합니다! 🎉 다음 주에는 예쁘게 꾸미고, AI를 붙이고, 세상에 공개합니다."
4. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "C3 과정을 완료하셨습니다! C4에서 더 고급 기능을 배워봅시다."
