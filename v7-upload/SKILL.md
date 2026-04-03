---
name: v7-upload
description: "파일 업로드 (Active Storage). C7 기능 추가 개발. Triggers: \"v7 upload\", \"v7-upload\", \"파일 업로드\", \"이미지 업로드\""
---

# V7: 파일 업로드 (Active Storage)

## 학습 목표
- Active Storage가 무엇인지 이해한다
- 기존 모델에 이미지 업로드 기능을 추가할 수 있다
- 업로드된 이미지를 화면에 표시할 수 있다
- 이미지 변환(썸네일)을 사용할 수 있다

## 사전 조건
- C4 LAUNCH 완료 (배포된 Rails 서비스)
- 코드 에디터 + Claude Code 확장 프로그램 설치
- 최소 1개 이상의 모델과 CRUD 기능 구현 완료

## 예상 소요 시간
30분

## STOP PROTOCOL

이 스킬은 2-Phase STOP Protocol을 따릅니다.

### Phase A (Turn 1)
1. references/main.md의 EXPLAIN 섹션을 읽고 설명한다
   - Active Storage = Rails의 파일 관리 시스템
   - 로컬 저장 vs 클라우드 저장
   - 이미지 변환(variant)이란
2. references/main.md의 EXECUTE 섹션을 따라 실행한다
   - Active Storage 설치
   - 모델에 이미지 첨부 기능 추가
   - 폼에 파일 업로드 필드 추가
   - 이미지 표시 및 썸네일 생성
3. **STOP** -- 여기서 멈추고 학생의 응답을 기다린다. AskUserQuestion을 사용하지 않는다.
4. 멈추기 전 출력: "파일 업로드 기능을 완성했습니다. '다음'을 입력하면 퀴즈로 넘어갑니다."

### Phase B (Turn 2)
1. references/main.md의 QUIZ 섹션 퀴즈 출제
2. 학생 답변에 피드백한다 (오답 해설 포함)
3. 다음 안내:
   - "웹에서 '완료' 버튼을 눌러주세요."
   - "다음 스킬: `/v7-automation`"

### 에러 대응 원칙
- libvips 미설치 시 `sudo apt install libvips` 안내
- 파일 크기 제한 설정 권장 (10MB 이하)
- S3 연동은 이 스킬에서 다루지 않음 (로컬 저장으로 충분)

### 산출물
- Active Storage가 설치된 상태
- 최소 1개 모델에 이미지 업로드 기능
- 업로드된 이미지가 화면에 표시됨
- git commit
