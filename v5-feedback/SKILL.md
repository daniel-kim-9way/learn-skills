---
name: v5-feedback
description: "사용자 피드백 루프 구축. C5 Block 1. Triggers: \"v5 feedback\", \"v5-feedback\", \"피드백\", \"사용자 의견\""
---

# C5 Block 1: 사용자 피드백 루프 구축

## 학습 목표
- 사용자 피드백이 서비스 성장에 왜 필수인지 이해한다
- 간단한 분석 도구(Ahoy 등)를 설치할 수 있다
- 피드백 폼을 만들고 ICE 프레임워크로 개선 우선순위를 정할 수 있다

## 사전 조건
- C4 LAUNCH 완료 (배포된 서비스 보유)
- 코드 에디터 + Claude Code 확장 프로그램 설치

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - 왜 피드백이 중요한가
   - 피드백 루프의 구조
   - ICE 프레임워크 소개
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - 간단한 분석 도구 설치
   - 피드백 폼 생성
   - ICE 프레임워크로 우선순위 정하기
   - my-feedback-plan.md 작성
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "피드백 루프 구축을 완료했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/v5-analytics`"

## 워밍업 태스크 (재개 시)

스킬 시작 시 프로젝트 디렉토리가 존재하면:
1. 프로젝트 상태를 기능 중심으로 요약 (기술 용어 없이)
2. 작은 수정 태스크 1개 제시 (버튼 색 변경, 텍스트 수정 등)
3. 성공 확인 후 본 학습 시작

프로젝트가 없으면 워밍업을 건너뛴다.
