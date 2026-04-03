---
name: v7-email
description: "이메일 알림/예약 자동화. C7 기능 추가 개발. Triggers: \"v7 email\", \"v7-email\", \"이메일\", \"알림 자동화\""
---

# V7: 이메일 알림/예약 자동화

## 학습 목표
- 서비스에서 이메일을 보내야 하는 시점을 판단할 수 있다
- Action Mailer로 이메일 기능을 구현할 수 있다
- Resend를 연동해 실제 이메일을 발송할 수 있다
- Solid Queue로 이메일 예약 발송을 구현할 수 있다

## 사전 조건
- C4 LAUNCH 완료 (배포된 Rails 서비스)
- 코드 에디터 + Claude Code 확장 프로그램 설치
- 기본적인 모델과 인증 기능 구현 완료

## 예상 소요 시간
30분

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - 이메일을 보내야 하는 시점 (회원가입 환영, 알림 등)
   - Action Mailer = Rails의 이메일 시스템
   - Resend = 이메일 전송 서비스
   - Solid Queue = 예약/지연 발송
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - 학생 서비스에 맞는 이메일 시나리오 선정
   - Action Mailer 설정
   - Resend 연동
   - 테스트 이메일 발송
   - Solid Queue로 예약 발송 구현
3. **STOP** -- 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "이메일 시스템을 완성했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 스킬: `/v7-realtime`"

### 에러 대응 원칙
- Resend API 키 오류 시 환경변수 설정 확인
- 개발 환경에서는 letter_opener로 이메일 미리보기 활용
- Solid Queue 설정 오류 시 config/queue.yml 확인

### 산출물
- 최소 1개의 Mailer 클래스
- 실제 동작하는 이메일 발송 기능
- git commit
