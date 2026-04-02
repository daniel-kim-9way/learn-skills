---
name: SKILL_NAME
description: "SKILL_DESCRIPTION. Triggers: \"TRIGGER_1\", \"TRIGGER_2\""
---

# SKILL_TITLE

## 학습 목표
LEARNING_OBJECTIVES

## 사전 조건
PREREQUISITES

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/BLOCK_REF.md의 EXPLAIN 섹션을 읽고 설명한다
2. references/BLOCK_REF.md의 EXECUTE 섹션의 단계를 실행한다
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "다음을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/BLOCK_REF.md의 QUIZ 섹션의 퀴즈를 출제한다
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/NEXT_SKILL_COMMAND`"

## 워밍업 태스크 (재개 시)

스킬 시작 시 프로젝트 디렉토리가 존재하면:
1. 프로젝트 상태를 기능 중심으로 요약 (기술 용어 없이)
2. 작은 수정 태스크 1개 제시 (버튼 색 변경, 텍스트 수정 등)
3. 성공 확인 후 본 학습 시작

프로젝트가 없으면 워밍업을 건너뛴다.
