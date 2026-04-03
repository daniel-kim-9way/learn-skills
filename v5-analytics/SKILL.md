---
name: v5-analytics
description: "데이터 기반 의사결정. C5 Block 2. Triggers: \"v5 analytics\", \"v5-analytics\", \"분석\", \"데이터 분석\""
---

# C5 Block 2: 데이터 기반 의사결정

## 학습 목표
- 서비스 성장에 필요한 핵심 지표를 이해한다
- 분석 데이터를 읽고 패턴을 발견할 수 있다
- 데이터 기반으로 개선 우선순위를 정할 수 있다

## 사전 조건
- C4 LAUNCH 완료 (배포된 서비스 보유)
- 코드 에디터 + Claude Code 확장 프로그램 설치
- `/v5-feedback` 완료 (피드백 루프 구축)

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - 무엇을 측정해야 하는가
   - 핵심 지표(활성 사용자, 기능 사용률 등)
   - 허영 지표 vs 실행 지표
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - 분석 데이터 읽기
   - 패턴 식별
   - 개선 우선순위 리스트 작성
   - my-analytics-insights.md 작성
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "데이터 분석을 완료했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/v5-seo`"

## 워밍업 태스크 (재개 시)

스킬 시작 시 프로젝트 디렉토리가 존재하면:
1. 프로젝트 상태를 기능 중심으로 요약 (기술 용어 없이)
2. 작은 수정 태스크 1개 제시 (버튼 색 변경, 텍스트 수정 등)
3. 성공 확인 후 본 학습 시작

프로젝트가 없으면 워밍업을 건너뛴다.
