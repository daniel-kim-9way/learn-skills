---
name: c4-security
description: "서비스 보안 체크리스트. C4 Block 7. 오픈 전 필수 보안 점검. Triggers: \"c4 보안\", \"c4-security\", \"보안 체크\", \"security checklist\", \"c4 block 7\""
---

# C4 Block 7: 보안 — 오픈 전 필수 점검

## 학습 목표
- 서비스 오픈 전 반드시 확인해야 할 보안 항목을 이해한다
- 일반적인 보안 위협(SQL 인젝션, XSS 등)을 시나리오로 경험한다
- 10개 보안 체크리스트를 실제로 점검할 수 있다

## 사전 조건
- `/c4-deploy` 완료 (서비스 배포 완료)

## 교수법: Quiz-First (시나리오 기반)

이 블록은 Quiz-First 방식으로 진행됩니다. 먼저 시나리오 퀴즈로 현재 보안 인식을 측정하고, 체크리스트 실행 후 메인 퀴즈로 이해를 확인합니다.

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block7-security.md의 EXPLAIN 섹션을 읽고 설명한다
   - 왜 오픈 전에 보안을 확인해야 하는가
   - 주요 보안 위협 종류 (비유로 설명)
2. references/block7-security.md의 EXECUTE 섹션을 따라 실행한다
   - Pre-Quiz (시나리오 기반)
   - 10개 보안 체크리스트 실행
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "보안 체크리스트를 완료했습니다. '다음'을 입력하면 메인 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block7-security.md의 QUIZ 섹션 메인 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c4-launch`"
