---
name: c3-database
description: "데이터베이스와 모델 개념 이해 및 구현. C3 Block 9. Triggers: \"c3 데이터베이스\", \"c3-database\", \"DB 설계\", \"모델 만들기\", \"데이터 저장\""
---

# C3 Block 9: 데이터베이스 + 모델 만들기

## 학습 목표
- 데이터베이스의 개념을 비개발자 언어로 이해할 수 있다
- Claude에게 모델 생성을 요청할 수 있다
- 마이그레이션이 무엇인지 기본적으로 설명할 수 있다

## 사전 조건
- `/c3-core-feature` 완료 (핵심 기능 구현 경험)

## 기능 해금

🔓 새 기능 해금: Subagent (병렬 작업)
DB 설계를 서브에이전트가 동시에 검토할 수 있습니다. Claude에게 "서브에이전트로 이 DB 설계를 검토해줘"라고 요청하면 두 번째 AI가 병렬로 검토를 수행합니다.

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block9-database.md의 EXPLAIN 섹션을 읽고 설명한다
   - 데이터베이스 = "엑셀 스프레드시트" 비유
   - 테이블 = 시트, 컬럼 = 헤더, 관계 = VLOOKUP
   - 마이그레이션이 무엇인지 (DB 변경 이력서)
2. references/block9-database.md의 EXECUTE 섹션을 따라 실행한다
   - Claude에게 모델 생성 요청
   - 마이그레이션 내용 확인
   - 서브에이전트로 DB 설계 검토
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "데이터베이스와 모델을 만들었습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block9-database.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c3-second-feature`"
