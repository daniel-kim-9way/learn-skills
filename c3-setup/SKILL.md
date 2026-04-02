---
name: c3-setup
description: "Claude Code 설치와 첫 대화. C3 Block 0. Triggers: \"c3 설치\", \"c3 setup\", \"c3-setup\", \"클로드코드 설치\""
---

# C3 Block 0: Claude Code 설치 + 첫 대화

## 학습 목표
- Claude Code를 설치하고 실행할 수 있다
- 터미널에서 AI와 첫 대화를 나눌 수 있다
- 오류 메시지를 Claude에게 붙여넣어 해결하는 패턴을 익힌다

## 사전 조건
- C1(VALUE)과 C2(PLAN) 완료
- 인터넷 연결
- Claude Pro/Max/Teams 계정

## STOP PROTOCOL

### Phase A (Turn 1)
1. references/block0-setup.md의 EXPLAIN 섹션을 읽고 설명한다
   - Claude Code가 무엇인지 (한 줄 설명)
   - 설치 방법 (OS별 명령어)
   - "오류→Claude에 붙여넣기" 패턴
2. references/block0-setup.md의 EXECUTE 섹션을 따라 실행한다
   - 설치 명령어 실행
   - `claude` 입력으로 첫 대화
   - 의도적 오류 → 붙여넣기 체험
3. **STOP** — 멈추고 기다린다
4. 출력: "설치와 첫 대화를 마쳤습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block0-setup.md의 QUIZ 섹션 퀴즈 출제
2. 피드백 후 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c3-first-experience`"
