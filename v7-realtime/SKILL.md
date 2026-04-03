---
name: v7-realtime
description: "실시간 기능 (Hotwire/Turbo). C7 기능 추가 개발. Triggers: \"v7 realtime\", \"v7-realtime\", \"실시간\", \"Hotwire\""
---

# V7: 실시간 기능 (Hotwire/Turbo)

## 학습 목표
- "실시간"이 사용자에게 어떤 가치를 주는지 이해한다
- Turbo Frames로 페이지 일부만 업데이트할 수 있다
- Turbo Streams로 실시간 라이브 업데이트를 구현할 수 있다
- 내 서비스에 실시간 기능 1개를 추가할 수 있다

## 사전 조건
- C4 LAUNCH 완료 (배포된 Rails 서비스)
- 코드 에디터 + Claude Code 확장 프로그램 설치
- 최소 1개 이상의 CRUD 기능 구현 완료

## 예상 소요 시간
40분

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - 실시간이란 "새로고침 없이 바뀌는 것"
   - Turbo Frames = 페이지 일부만 교체
   - Turbo Streams = 서버에서 실시간 푸시
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - Turbo Frame으로 인라인 편집 구현
   - Turbo Stream으로 실시간 목록 업데이트
   - 학생 서비스에 실시간 기능 1개 적용
3. **STOP** -- 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "실시간 기능을 완성했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 스킬: `/v7-upload`"

### 에러 대응 원칙
- Turbo Frame 미동작 시 turbo_frame_tag ID 매칭 확인
- Turbo Stream 미동작 시 broadcasts 설정 확인
- ActionCable 연결 오류 시 cable.yml 확인

### 산출물
- 최소 1개의 실시간 기능
- Turbo Frame 또는 Turbo Stream 활용
- git commit
