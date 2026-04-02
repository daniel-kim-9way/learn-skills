---
name: c4-warmup
description: "C4 시작 워밍업. C4 Block 0. 쉬고 나서 다시 서비스와 연결하기. Triggers: \"c4 워밍업\", \"c4-warmup\", \"c4 시작\", \"c4 block 0\""
---

# C4 Block 0: 워밍업 — 다시 연결하기

## 학습 목표
- 쉬고 나서 내가 만든 서비스를 다시 기억하고 실행할 수 있다
- Claude에게 서비스를 기능 중심으로 설명시키는 방법을 익힌다
- 작은 변경 한 가지를 직접 해보며 손을 푼다

## 사전 조건
- C3 전 과정 완료 (Claude Code 설치, Memory, Skill, MCP, 서비스 개발 기본)
- 만들던 서비스 프로젝트 폴더 존재

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block0-warmup.md의 EXPLAIN 섹션을 읽고 설명한다
   - 왜 워밍업이 필요한지 (기억 리셋 현상)
   - 컨텍스트 회복 개념 (내 서비스를 다시 '느끼기')
2. references/block0-warmup.md의 EXECUTE 섹션을 따라 실행한다
   - 서비스 실행
   - Claude가 서비스를 기능 중심으로 요약
   - 버튼 색 변경 (손 풀기)
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "서비스를 다시 실행하고 워밍업을 마쳤습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block0-warmup.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (모든 답변이 유효하므로 경험을 격려하고 다음 단계로 안내)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c4-design`"
