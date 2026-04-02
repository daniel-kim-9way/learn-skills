---
name: c3-memory-and-skill
description: "Claude Code의 Memory(CLAUDE.md)와 Skill 기능 학습. C3 Block 2. Triggers: \"c3 메모리\", \"c3-memory-and-skill\", \"CLAUDE.md\", \"클로드 메모리\", \"커스텀 스킬\""
---

# C3 Block 2: Claude에게 기억과 스킬 주기

## 학습 목표
- CLAUDE.md를 작성하여 Claude에게 프로젝트 정보를 기억시킬 수 있다
- 반복 작업을 커스텀 스킬로 저장하고 호출할 수 있다
- Claude Code의 Memory와 Skill 기능을 활용한다

## 사전 조건
- `/c3-first-experience` 완료 (Working Backward + AI 협업 첫 체험)

## 기능 해금 타임라인

앞으로 배울 고급 기능들의 학습 순서입니다:

| 기능 | 해금 블록 | 설명 |
|------|----------|------|
| Memory (CLAUDE.md) | **지금 (Block 2)** | AI에게 프로젝트 정보 기억시키기 |
| Skill (커스텀 명령어) | **지금 (Block 2)** | 반복 작업을 명령어로 저장 |
| MCP (외부 도구 연결) | Block 3 | 데이터베이스, API 등 연결 |
| Subagent (병렬 작업) | Block 9 | 여러 AI가 동시에 작업 |
| Hook (자동 실행) | Block 10 | 특정 이벤트에 자동 반응 |
| Plugin (C4) | C4 Block 3 | 플러그인으로 기능 확장 |
| Teams (C4) | C4 Block 5 | 팀 단위 AI 협업 |

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block2-memory-skill.md의 EXPLAIN 섹션을 읽고 설명한다
   - Memory란 무엇인지 (CLAUDE.md = AI에게 명함 주기)
   - Skill이란 무엇인지 (반복 작업을 명령어로 저장)
   - 두 기능이 왜 중요한지 (매번 설명 없이 일관된 AI 협업)
2. references/block2-memory-skill.md의 EXECUTE 섹션을 따라 실행한다
   - CLAUDE.md 작성 (프로젝트 정보, AI 역할, 코드 스타일)
   - Claude가 기억하는지 새 세션에서 확인
   - `/status` 커스텀 스킬 생성
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "Memory와 Skill 설정을 마쳤습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block2-memory-skill.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c3-mcp-connect`"

## 워밍업 태스크 (재개 시)

스킬 시작 시 프로젝트 디렉토리가 존재하면:
1. 프로젝트의 현재 상태를 기능 중심으로 요약 (기술 용어 없이)
   - 예: "할 일 추가, 체크, 삭제 기능이 있는 페이지가 있습니다"
2. 작은 수정 태스크 1개 제시
   - 예: "버튼 색을 파란색으로 바꿔볼까요?"
3. 성공 확인 후 본 학습 시작

프로젝트가 없으면 워밍업을 건너뛴다.
