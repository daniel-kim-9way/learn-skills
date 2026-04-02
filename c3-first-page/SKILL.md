---
name: c3-first-page
description: "홈페이지 + 회원가입/로그인 구현. C3 Block 7. Triggers: \"c3 홈페이지\", \"c3-first-page\", \"회원가입 로그인\", \"첫 페이지 만들기\", \"인증 구현\""
---

# C3 Block 7: 홈페이지 + 회원가입/로그인 만들기

## 학습 목표
- 완성된 예시를 먼저 보고 수정하는 Scaffolding 방식을 경험할 수 있다
- 홈페이지와 인증 기능이 왜 필요한지 이해할 수 있다
- Claude의 도움으로 텍스트/색상 수정 및 회원가입/로그인 기능을 추가할 수 있다

## 사전 조건
- `/c3-rails-init` 완료 (Rails 프로젝트 생성 및 실행 경험)

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block7-first-page.md의 EXPLAIN 섹션을 읽고 설명한다
   - 홈페이지 = 서비스의 현관문 (왜 중요한지)
   - 인증 = 누가 들어올 수 있는지 (회원가입/로그인의 역할)
   - Scaffolding 방식 소개 (완성된 예시 먼저 → 수정)
2. references/block7-first-page.md의 EXECUTE 섹션을 따라 실행한다
   - Claude가 완성된 예시 페이지를 보여줌
   - 텍스트/색상 수정
   - Claude의 도움으로 인증 기능 추가
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "홈페이지와 회원가입/로그인을 만들었습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block7-first-page.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c3-core-feature`"
