---
name: v7-chrome-ext
description: "크롬 익스텐션 만들기. C7 기능 추가 개발. Triggers: \"v7 chrome-ext\", \"v7-chrome-ext\", \"크롬 확장\", \"브라우저 확장\""
---

# V7: 크롬 익스텐션 만들기

## 학습 목표
- 크롬 익스텐션의 구조(Manifest V3)를 이해한다
- Claude와 함께 간단한 익스텐션을 만들 수 있다
- 로컬에서 익스텐션을 로드하고 테스트할 수 있다
- 기본 기능을 확장하여 개선할 수 있다

## 사전 조건
- C4 LAUNCH 완료 (배포된 Rails 서비스)
- 코드 에디터 + Claude Code 확장 프로그램 설치
- Chrome 브라우저 사용
- 기본적인 HTML/CSS/JavaScript 이해 (몰라도 Claude가 도와줌)

## 예상 소요 시간
40분

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - 크롬 익스텐션이란
   - Manifest V3 구조
   - 익스텐션으로 할 수 있는 것들
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - 익스텐션 아이디어 선정
   - 기본 파일 구조 생성
   - Claude와 함께 기능 구현
   - 로컬 로드 및 테스트
   - 기능 확장
3. **STOP** -- 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "크롬 익스텐션을 완성했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "C7 기능 추가 개발을 모두 완료했습니다!"

### 에러 대응 원칙
- manifest.json 문법 오류 시 JSON 검증
- 권한(permissions) 부족 시 manifest.json에 추가
- content script 미동작 시 matches 패턴 확인

### 산출물
- 동작하는 크롬 익스텐션 1개
- manifest.json + popup 또는 content script
- git commit (선택)
