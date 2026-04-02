---
name: c3-first-experience
description: "AI와 함께 첫 서비스 체험. C3 Block 1. Triggers: \"c3 체험\", \"working backward\", \"c3-first-experience\", \"워킹백워드\""
---

# C3 Block 1: AI와 함께 첫 서비스 체험

## 학습 목표
- 완성된 서비스를 먼저 보고 역방향으로 이해하는 Working Backward 방식을 익힌다
- Claude에게 "무언가를 만들어줘"라고 말하는 첫 경험을 한다
- AI와 협업하는 감각을 키운다

## 사전 조건
- `/c3-setup` 완료 (Claude Code 설치 및 첫 대화 경험)

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block1-experience.md의 EXPLAIN 섹션을 읽고 설명한다
   - Working Backward란 무엇인지 (완성품을 먼저 보고 이해하는 방식)
   - 왜 이 방식이 비개발자에게 효과적인지
2. references/block1-experience.md의 EXECUTE 섹션을 따라 실행한다
   - Claude에게 투두 웹앱 만들기 요청
   - 완성된 앱의 코드를 Claude에게 설명 요청 (역방향 이해)
   - 자신의 서비스 아이디어에 맞게 수정 요청
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "AI와 첫 협업을 마쳤습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block1-experience.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (모든 답변이 유효하므로 경험을 격려하고 다음 단계로 안내)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c3-memory-and-skill`"

## 워밍업 태스크 (재개 시)

스킬 시작 시 프로젝트 디렉토리가 존재하면:
1. 어제 Claude와 만든 것이 무엇인지 Claude에게 물어본다
   - `CLAUDE.md`가 있으면 Claude가 자동으로 기억합니다
   - 없으면 학생에게 "어제 뭘 만들었나요?"라고 물어봅니다
2. 작은 수정 태스크 1개 제시 (버튼 색 변경, 텍스트 수정 등)
3. 성공 확인 후 본 학습 시작

프로젝트가 없으면 워밍업을 건너뛴다.
