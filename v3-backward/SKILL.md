---
name: v3-backward
description: "Working Backward - 완성부터 거꾸로. C3 BUILD 두 번째 스킬. Triggers: \"v3 backward\", \"v3-backward\", \"워킹 백워드\", \"완성부터\""
---

# V3: Working Backward - 완성부터 거꾸로

## 학습 목표
- 완성된 샘플 앱을 직접 사용해보고 "내 서비스도 이렇게 되겠구나"를 체감한다
- 코드 구조(models/views/controllers)를 지도처럼 훑어본다
- C2 기획서의 내용이 코드의 어디에 해당하는지 연결한다

## 사전 조건
- `/v3-setup` 완료 (에디터 + Claude Code 설치)
- C2 설계서 참고 (my-service-design-v1.0.md)
- 코드 에디터 + Claude Code 확장 프로그램에서 진행

## STOP PROTOCOL

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - "레고 완성 사진" 비유: 완성품을 먼저 보면 조립이 쉬워진다
   - 샘플 앱(sample-bookclub)이 무엇인지
   - 코드 구조를 지도로 비유
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - 샘플 앱 clone + 실행
   - 브라우저에서 사용해보기
   - 코드 구조 탐색
   - 내 서비스와 매핑
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다.
4. 멈추기 전 출력: "샘플 앱 탐색을 마쳤습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 스킬: `/v3-memory`"

### 에러 대응 원칙
- clone이나 서버 실행에서 오류가 나면 오류 메시지를 Claude에게 보여주도록 안내
- Ruby/Rails 설치가 안 되어 있으면 설치부터 진행

### 산출물
- 샘플 앱 실행 경험
- "내 서비스 → 코드 구조" 매핑 메모
