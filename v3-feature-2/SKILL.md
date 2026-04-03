---
name: v3-feature-2
description: "핵심 기능 2 - 반복 빌드. C3 BUILD 아홉 번째 스킬. Triggers: \"v3 feature-2\", \"v3-feature-2\", \"두번째 기능\", \"반복 빌드\""
---

# V3: 핵심 기능 2 - 반복 빌드

## 학습 목표
- v3-feature-1에서 배운 패턴을 스스로 적용한다
- 안내 없이 기능을 계획하고 Claude에게 지시하는 자율성을 경험한다
- "이 패턴을 알면 뭐든 만든다"는 깨달음을 얻는다

## 사전 조건
- `/v3-feature-1` 완료 (첫 번째 핵심 기능 구현 경험)
- C2에서 작성한 핵심 기능 목록 (my-service-design-v1.0.md의 2번째 기능)
- 코드 에디터 + Claude Code 확장 프로그램에서 진행

## STOP PROTOCOL

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - v3-feature-1 패턴 복습
   - 이번에는 학생이 직접 계획을 세운다
   - "도움이 필요하면 언제든 물어보세요" (점진적 자율성)
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - 학생이 직접 기능 분해
   - 학생이 Claude에게 직접 지시
   - 막히면 도움 제공
   - 기능 1과 통합 테스트
   - git commit
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다.
4. 멈추기 전 출력: "두 번째 핵심 기능까지 완성했습니다! '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 스킬: `/v3-checkpoint`"

### 에러 대응 원칙
- 이번에는 학생이 먼저 시도하도록 유도
- 막히면 힌트 → 그래도 안 되면 구체적 안내 (단계적 도움)

### 산출물
- 동작하는 핵심 기능 2
- 기능 1과 통합 확인
- git commit
