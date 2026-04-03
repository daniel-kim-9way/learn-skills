---
name: v4-ai-feature
description: "[선택] Claude API로 AI 기능 추가. Triggers: \"v4 ai-feature\", \"v4-ai-feature\", \"AI 기능\", \"Claude API\""
---

# [선택] Claude API로 AI 기능 추가

## 학습 목표
- API가 무엇인지 이해한다 (레스토랑 주문 비유)
- .env로 비밀을 관리하는 원칙을 익힌다 ("비밀은 코드에 안 쓴다")
- 내 서비스에 AI 기능 하나를 추가하고 테스트한다

## 사전 조건
- `/v4-landing` 완료 (랜딩 페이지 완성)
- Anthropic 계정 (API 키 발급용)
- 코드 에디터 + Claude Code 확장 프로그램에서 진행

## 대화형 학습 프로토콜

### 진행 방식
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - 내 서비스에 AI가 추가되면 어떤 가치가 생기는지
   - API 개념 (레스토랑 비유)
   - API 비용에 대한 불안 해소
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - API 키 발급
   - .env 설정 ("비밀은 코드에 안 쓴다")
   - AI 기능 하나 구현
   - 테스트
3. **STOP** — 학생 응답 대기
4. references/main.md의 QUIZ 섹션 퀴즈 출제
5. 다음 안내: `/v4-payment` (선택) 또는 `/v4-security`

### 산출물
- Claude API 연동된 AI 기능 1개
- .env 파일에 API 키 안전하게 보관
