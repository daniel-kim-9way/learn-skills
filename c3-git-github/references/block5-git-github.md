## EXPLAIN

### git = 게임 세이브 시스템

RPG 게임을 하다 보면 중요한 순간에 저장을 합니다. 보스 전 직전, 새로운 지역 진입 전… 저장 덕분에 실패해도 다시 그 지점으로 돌아올 수 있습니다.

**git**은 코드의 게임 세이브 시스템입니다.

- **커밋(commit)** = 세이브 포인트 ("로그인 기능 완성" 시점에 저장)
- **히스토리** = 세이브 목록 (언제 무엇을 저장했는지 기록)
- **브랜치** = 다른 슬롯으로 저장 (메인 게임에 영향 없이 새 기능 시도)

실수로 코드를 망쳐도 과거 커밋으로 되돌릴 수 있습니다.

### GitHub = 클라우드 세이브

게임 세이브를 클라우드에 올리면 다른 기기에서도 이어할 수 있습니다. **GitHub**은 git 저장소를 인터넷에 올려두는 클라우드 서비스입니다.

GitHub 덕분에:
- 내 컴퓨터가 고장나도 코드가 안전합니다
- 다른 컴퓨터에서 내려받아 계속 작업할 수 있습니다
- 다른 사람과 코드를 공유하고 협업할 수 있습니다

### 핵심 3개 명령어

| 명령어 | 의미 | 게임 비유 |
|--------|------|----------|
| `git add` | 저장할 파일 선택 | 저장할 항목 체크 |
| `git commit` | 세이브 포인트 생성 | 저장 버튼 클릭 |
| `git push` | 클라우드에 올리기 | 클라우드 업로드 |

## EXECUTE

### 단계 1: 로컬 git 저장소 초기화

프로젝트 폴더에서 아래 명령어를 순서대로 실행합니다:

```bash
# git 저장소 초기화
git init

# 모든 파일을 스테이징 (저장 준비)
git add .

# 첫 번째 세이브 포인트 생성
git commit -m "첫 번째 커밋: 나만의 스킬 추가"
```

Claude에게 도움을 요청할 수도 있습니다:
```
git으로 지금까지 만든 파일들을 저장해줘
```

### 단계 2: GitHub 저장소 생성

1. [github.com](https://github.com)에 로그인합니다
2. 우측 상단 `+` 버튼 → `New repository` 클릭
3. Repository name: `my-[서비스이름]-skills` (예: `my-todo-skills`)
4. Public 또는 Private 선택
5. `Create repository` 클릭

생성 후 나오는 명령어를 복사합니다 (이미 로컬 저장소가 있을 때의 명령어).

### 단계 3: GitHub에 push

GitHub에서 복사한 명령어를 실행합니다:

```bash
git remote add origin https://github.com/[내아이디]/[저장소이름].git
git branch -M main
git push -u origin main
```

GitHub 페이지를 새로고침하면 파일이 올라간 것을 확인할 수 있습니다.

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "`git commit`은 무엇을 하는 명령어인가요?",
      "header": "git commit 이해",
      "options": [
        {"label": "파일을 GitHub에 업로드한다", "description": ""},
        {"label": "저장할 파일을 선택(스테이징)한다", "description": ""},
        {"label": "현재 상태를 세이브 포인트로 저장한다", "description": ""},
        {"label": "GitHub 저장소를 새로 만든다", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "git과 GitHub의 차이는 무엇인가요?",
      "header": "git vs GitHub",
      "options": [
        {"label": "git과 GitHub는 완전히 같은 것이다", "description": ""},
        {"label": "git은 내 컴퓨터의 버전 관리 도구, GitHub는 저장소를 인터넷에 올리는 클라우드 서비스", "description": ""},
        {"label": "git은 무료, GitHub는 유료 서비스다", "description": ""},
        {"label": "git은 코드 작성 도구, GitHub는 코드 실행 서버다", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번째 질문 → "현재 상태를 세이브 포인트로 저장한다"
- 2번째 질문 → "git은 내 컴퓨터의 버전 관리 도구, GitHub는 저장소를 인터넷에 올리는 클라우드 서비스"

해설:
- git commit: 게임의 세이브처럼 현재 코드 상태를 하나의 체크포인트로 저장합니다. `git add`가 "저장할 파일 선택"이고, `git commit`이 실제 "저장 버튼 클릭"입니다.
- git vs GitHub: git은 내 컴퓨터에서 동작하는 버전 관리 도구입니다. GitHub는 그 git 저장소를 인터넷에 올려두는 서비스로, 백업과 협업을 가능하게 합니다. git 없이 GitHub만 쓸 수 없고, GitHub 없이도 git은 쓸 수 있습니다.
