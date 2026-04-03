---
name: v2-feature-spec
description: "AI에게 기능 명세서 받고 검토하기. C2 PLAN 세 번째 스킬. Triggers: \"v2 feature-spec\", \"v2-feature-spec\", \"기능 명세\", \"SAFE 검토\""
---

# AI에게 기능 명세서 받고 검토하기

## 학습 목표
- AI가 생성한 기능 명세서를 받아서 읽을 수 있다
- SAFE 프레임워크로 AI 산출물의 빠진 부분을 찾아낼 수 있다
- AI의 결과물을 그대로 수용하지 않고 비판적으로 검토하는 습관을 기른다

## 사전 조건
- `/v2-service-type` 완료 (my-service-type.md 존재)
- Claude Code Desktop에서 진행

## 대화형 학습 프로토콜

### 진행 방식
1. references/main.md를 읽고 대화 흐름에 따라 진행한다
2. AI가 의도적으로 80% 수준의 불완전한 명세서를 먼저 생성한다
3. SAFE 프레임워크를 가르치고 학생이 직접 빠진 부분을 찾게 한다
4. 학생이 보완한 완성 명세서를 파일로 저장한다

### 산출물
- 파일명: `my-feature-spec.md`
- 내용: SAFE 검토 완료된 기능 명세서
