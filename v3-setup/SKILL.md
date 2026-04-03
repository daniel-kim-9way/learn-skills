---
name: v3-setup
description: "코드 에디터 + Claude Code 설치. C3 BUILD 첫 번째 스킬. Triggers: \"v3 setup\", \"v3-setup\", \"에디터 설치\", \"코드 에디터\""
---

# V3: 코드 에디터 + Claude Code 설치

## 학습 목표
- VS Code(코드 에디터)를 설치하고 기본 화면을 이해한다
- Claude Code 확장 프로그램을 설치하고 에디터 안에서 AI와 대화한다
- Claude Code Desktop과 에디터의 차이를 체감한다 ("Claude가 이제 직접 파일을 만들어줍니다")

## 사전 조건
- C1(VALUE)과 C2(PLAN) 완료 (my-service-plan-v0.1.md, my-service-design-v1.0.md 파일 존재)
- 인터넷 연결
- Claude Pro/Max/Teams 계정
- **도구 전환**: C1~C2에서 사용한 Claude Code Desktop에서 → 코드 에디터 + Claude Code 확장 프로그램으로 전환합니다

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. 학생의 OS를 확인한다 (Windows / macOS / Linux)
2. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - 데스크탑 → 에디터 전환의 의미
   - VS Code가 무엇인지 (비유: 워드 프로세서 → 코드 전용 워드)
   - Claude Code 확장이 하는 일
3. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - OS에 맞는 에디터 설치
   - Claude Code 확장 설치
   - 에디터 안에서 첫 대화
   - 파일 생성 데모 (Desktop vs Editor 차이 체험)
4. **STOP** — 여기서 멈추고 학생의 응답을 기다린다.
5. 멈추기 전 출력: "에디터와 Claude Code 설치를 마쳤습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 스킬: `/v3-backward`"

### 에러 대응 원칙
- 설치 오류가 나면 당황하지 말고 오류 메시지를 그대로 공유하도록 안내
- "오류는 실패가 아니라 대화의 시작입니다"

### 산출물
- VS Code + Claude Code 확장 설치 완료
- 에디터에서 AI가 만든 첫 파일 확인
