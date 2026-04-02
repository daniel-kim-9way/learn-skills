---
name: c4-deploy
description: "서비스 배포하기. C4 Block 6. localhost에서 인터넷으로. Triggers: \"c4 배포\", \"c4-deploy\", \"배포\", \"deploy\", \"railway\", \"render\", \"c4 block 6\""
---

# C4 Block 6: 배포 — 세상에 내보내기

## 학습 목표
- localhost와 인터넷 배포의 차이를 이해한다
- Railway 또는 Render로 서비스를 배포할 수 있다
- 도메인을 연결하는 방법을 익힌다

## 사전 조건
- `/c4-clarify` 완료 (Clarify 패턴 + Teams 기능 해금)

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block6-deploy.md의 EXPLAIN 섹션을 읽고 설명한다
   - localhost vs 인터넷 배포 차이
   - 왜 배포가 필요한가 (내 컴퓨터만 보임)
   - Railway vs Render 비교
2. references/block6-deploy.md의 EXECUTE 섹션을 따라 실행한다
   - Production 환경 준비
   - Railway 또는 Render로 배포
   - 도메인 연결
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "배포를 완료했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block6-deploy.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c4-security`"
