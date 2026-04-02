---
name: c4-payment
description: "Toss Payments 결제 연동. C4 Block 4. Triggers: \"c4 결제\", \"c4-payment\", \"토스페이먼츠\", \"toss payments\", \"결제 연동\", \"c4 block 4\""
---

# C4 Block 4: 결제 연동 — Toss Payments

## 학습 목표
- 결제 흐름 전체를 이해한다 (고객 → 게이트웨이 → 내 통장)
- Toss Payments 테스트 모드로 결제 기능을 구현할 수 있다
- 실제 결제 전 안전하게 테스트하는 방법을 익힌다

## 사전 조건
- `/c4-ai-feature` 완료 (Claude API 연결 경험)
- 사업자 등록번호 또는 개인 계좌 정보 (실제 연동 시)

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block4-payment.md의 EXPLAIN 섹션을 읽고 설명한다
   - 결제 흐름 전체 (고객 → 게이트웨이 → 내 통장)
   - 테스트 모드와 실제 모드의 차이
   - Toss Payments 선택 이유
2. references/block4-payment.md의 EXECUTE 섹션을 따라 실행한다
   - Toss Payments 테스트 계정 등록
   - Claude가 결제 기능 연동
   - 테스트 결제 실행
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "결제 연동을 완료했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block4-payment.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c4-clarify`"
