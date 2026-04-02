---
name: c4-launch
description: "서비스 런치 체크리스트. C4 Block 8. 오픈 직전 최종 점검 후 LAUNCH! Triggers: \"c4 런치\", \"c4-launch\", \"launch\", \"런치\", \"서비스 오픈\", \"c4 block 8\""
---

# C4 Block 8: LAUNCH — 드디어 오픈!

## 학습 목표
- "완벽"을 기다리지 않고 적시에 오픈하는 판단력을 키운다
- 5개 필수 항목과 나중에 해도 되는 항목을 구분할 수 있다
- LAUNCH 체크리스트를 직접 실행하고 서비스를 오픈할 수 있다

## 사전 조건
- `/c4-security` 완료 (보안 체크리스트 통과)

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block8-launch.md의 EXPLAIN 섹션을 읽고 설명한다
   - "완벽은 완료의 적이다" (Done is better than perfect)
   - 5개 필수 항목 vs 나중에 해도 되는 항목
2. references/block8-launch.md의 EXECUTE 섹션을 따라 실행한다
   - templates/launch-checklist.md 체크리스트 실행
   - 런치 스킬 템플릿 생성
   - 실제 LAUNCH!
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "LAUNCH 체크리스트를 완료했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block8-launch.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c4-session-wrap`"
