---
name: v7-automation
description: "업무 자동화 도전. C7 기능 추가 개발. Triggers: \"v7 automation\", \"v7-automation\", \"업무 자동화\", \"자동화\""
---

# V7: 업무 자동화 도전

## 학습 목표
- 일상에서 반복되는 작업을 자동화 대상으로 식별할 수 있다
- Claude와 함께 자동화 로직을 설계할 수 있다
- Rails의 Solid Queue로 반복 작업을 스케줄링할 수 있다
- 하나의 자동화를 처음부터 끝까지 완성할 수 있다

## 사전 조건
- C4 LAUNCH 완료 (배포된 Rails 서비스)
- 코드 에디터 + Claude Code 확장 프로그램 설치
- 기본적인 Rails 구조 이해 (모델, 컨트롤러)

## 예상 소요 시간
35분

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - 자동화란 "반복 작업을 코드에게 맡기는 것"
   - 어떤 업무가 자동화에 적합한가
   - Rake Task + Solid Queue 패턴
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - 자동화 대상 업무 선정
   - Rake Task 또는 Job으로 구현
   - Solid Queue로 스케줄링
   - 테스트 실행
3. **STOP** -- 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "자동화 기능을 완성했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 스킬: `/v7-chrome-ext`"

### 에러 대응 원칙
- Job 실행 오류 시 Rails 로그 확인
- 스케줄링 설정 오류 시 config/recurring.yml 확인
- 외부 API 연동 시 에러 핸들링 필수

### 산출물
- 1개의 자동화된 작업 (Job 또는 Rake Task)
- Solid Queue 스케줄링 설정
- git commit
