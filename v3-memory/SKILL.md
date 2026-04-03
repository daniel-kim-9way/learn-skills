---
name: v3-memory
description: "AI에게 나를 기억시키기 - CLAUDE.md 작성. C3 BUILD 세 번째 스킬. Triggers: \"v3 memory\", \"v3-memory\", \"CLAUDE.md\", \"AI 기억\""
---

# V3: Memory & Skill - AI에게 나를 기억시키기

## 학습 목표
- AI가 대화를 기억하지 못하는 문제를 직접 경험한다
- CLAUDE.md 파일의 역할과 작성법을 이해한다
- C1/C2에서 만든 내용을 활용해 CLAUDE.md를 작성한다

## 사전 조건
- `/v3-backward` 완료
- C1에서 만든 기획서 (my-service-plan-v0.1.md)
- C2에서 만든 설계서 (my-service-design-v1.0.md)
- 코드 에디터 + Claude Code 확장 프로그램에서 진행

## STOP PROTOCOL

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - AI 기억상실 문제 체험 (직접 테스트)
   - CLAUDE.md가 무엇인지 (비유: AI의 일기장)
   - 어떤 내용을 적어야 하는지
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - "내 서비스 핵심 기능이 뭐야?" 테스트 (AI 모름)
   - CLAUDE.md 함께 작성
   - 같은 질문 다시 테스트 (AI 앎!)
   - 업데이트 습관 안내
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다.
4. 멈추기 전 출력: "CLAUDE.md를 작성했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 스킬: `/v3-rails-start`"

### 에러 대응 원칙
- 파일 생성 오류 시 Claude에게 오류 메시지를 보여주도록 안내

### 산출물
- 프로젝트 루트의 CLAUDE.md 파일
