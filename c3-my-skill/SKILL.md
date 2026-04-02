---
name: c3-my-skill
description: "Template과 STUB으로 나만의 스킬 만들기. C3 Block 4. Triggers: \"c3 스킬 만들기\", \"c3-my-skill\", \"커스텀 스킬 생성\", \"나만의 스킬\""
---

# C3 Block 4: Template + STUB으로 나만의 스킬 만들기

## 학습 목표
- 스킬 파일의 구조(YAML frontmatter, 섹션)를 이해할 수 있다
- STUB 플레이스홀더를 채워서 나만의 스킬을 완성할 수 있다
- 완성된 스킬을 `/명령어`로 호출하여 동작을 확인할 수 있다

## 사전 조건
- `/c3-mcp-connect` 완료 (MCP 개념 및 외부 도구 연결 경험)

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/block4-my-skill.md의 EXPLAIN 섹션을 읽고 설명한다
   - 스킬 파일의 구조 설명 (YAML frontmatter, 지시 섹션)
   - STUB이 무엇인지 (채워야 할 빈칸 플레이스홀더)
   - templates/my-tool-skill.md 파일 안내
2. references/block4-my-skill.md의 EXECUTE 섹션을 따라 실행한다
   - 스킬 뼈대 생성
   - STUB 하나씩 채우기
   - 완성된 스킬 테스트
3. **STOP** — 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "나만의 스킬을 만들었습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/block4-my-skill.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. Bridge 메시지 출력:
   "AI가 당신의 Slack에 연결됐습니다! 🎉 다음 시간에는 이걸 GitHub에 올려서 어디서든 쓸 수 있게 만들어봅시다."
4. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 블록: `/c3-git-github`"
