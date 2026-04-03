---
name: v3-rails-start
description: "Rails 프로젝트 시작 + Hello World. C3 BUILD 네 번째 스킬. Triggers: \"v3 rails-start\", \"v3-rails-start\", \"Rails 시작\", \"프로젝트 생성\""
---

# V3: Rails 프로젝트 시작 + Hello World

## 학습 목표
- Ruby와 Rails가 설치되어 있는지 확인하고, 없으면 설치한다
- rails new 명령으로 내 서비스 프로젝트를 생성한다
- localhost:3000에서 내 서비스가 돌아가는 것을 직접 확인한다
- 기본 페이지를 내 서비스 홈페이지로 교체한다

## 사전 조건
- `/v3-memory` 완료 (CLAUDE.md 작성 경험)
- 코드 에디터 + Claude Code 확장 프로그램에서 진행

## STOP PROTOCOL

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - Rails가 무엇인지 (비유: 건물의 골조)
   - localhost란? (비유: 내 컴퓨터에서만 보이는 비밀 주소)
   - 프로젝트 생성이 왜 중요한 마일스톤인지
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - Ruby/Rails 설치 확인
   - rails new [서비스이름]
   - 서버 시작 + localhost:3000 확인
   - 기본 페이지 → 내 서비스 홈페이지로 교체
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다.
4. 멈추기 전 출력: "축하합니다! 내 서비스가 처음으로 브라우저에 나타났습니다! '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 스킬: `/v3-git-save`"

### 에러 대응 원칙
- Ruby/Rails 설치 오류는 OS별로 대응 (rbenv, asdf 등)
- 포트 충돌 시 다른 포트 사용 안내
- "오류 메시지를 Claude에게 보여주세요"가 만능 해결책

### 산출물
- Rails 프로젝트 디렉토리
- localhost:3000에서 동작하는 내 서비스 홈페이지
