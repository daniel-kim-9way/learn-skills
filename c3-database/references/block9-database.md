## EXPLAIN

### 데이터베이스 = 엑셀 스프레드시트

데이터베이스를 처음 들으면 어렵게 느껴지지만, 사실 엑셀과 아주 비슷합니다.

| 엑셀 | 데이터베이스 |
|------|------------|
| 파일 (Book) | 데이터베이스 (Database) |
| 시트 (Sheet) | 테이블 (Table) |
| 행 (Row) | 레코드 (Record) |
| 열/헤더 (Column) | 컬럼 (Column) |
| VLOOKUP | 관계 (Relation) |

예시: 독서 목록 앱이라면
- `books` 테이블: id, title, author, read_date
- `users` 테이블: id, email, name, created_at

### 테이블 간 관계 = VLOOKUP

엑셀에서 다른 시트의 데이터를 가져올 때 VLOOKUP을 씁니다. 데이터베이스에서는 "관계"로 연결합니다.

예시: "이 책은 어떤 사용자 거야?" → `books` 테이블에 `user_id` 컬럼으로 연결

### 마이그레이션 = DB 변경 이력서

팀에서 일하면 누군가 DB 구조를 바꿀 때 다른 사람들도 같이 바꿔야 합니다. **마이그레이션**은 이 변경 사항을 파일로 기록해서 팀 전체가 같은 DB 구조를 유지하게 합니다.

비유: 마이그레이션은 "2024-01-15: books 테이블에 page_count 컬럼 추가" 같은 이력서입니다.

혼자 개발해도 마이그레이션은 중요합니다 — 나중에 배포할 때 서버 DB도 같이 바뀌기 때문입니다.

## EXECUTE

### 단계 1: Claude에게 모델 생성 요청

Claude에게 요청합니다:

```
내 서비스에 필요한 데이터 모델을 만들어줘.

필요한 데이터:
- [데이터 항목 1]: [설명]
- [데이터 항목 2]: [설명]

예를 들어 독서 목록 앱이면:
"책 정보를 저장하는 Book 모델을 만들어줘.
저장할 내용: 제목, 저자, 읽기 시작한 날짜, 완독 여부"
```

Claude가 아래와 비슷한 명령어를 실행합니다:
```bash
bin/rails generate model Book title:string author:string started_at:date completed:boolean
bin/rails db:migrate
```

### 단계 2: 마이그레이션 내용 확인

생성된 마이그레이션 파일을 Claude에게 설명 요청합니다:

```
방금 만들어진 마이그레이션 파일이 뭘 하는 건지 설명해줘.
db/migrate/ 폴더에 있는 파일 내용을 보여주고, 비개발자가 이해할 수 있게 설명해줘.
```

Claude의 설명을 들으면서 "아, 이렇게 DB 구조가 정의되는구나"를 이해하는 것이 목표입니다.

### 단계 3: Subagent로 DB 설계 검토

DB 설계를 서브에이전트에게 검토 요청합니다:

```
서브에이전트를 사용해서 지금 DB 설계를 검토해줘.
체크할 내용:
- 나중에 필요할 수 있는 컬럼이 빠진 게 있나?
- 데이터 타입이 적절한가?
- 테이블 간 관계가 맞는가?
```

서브에이전트의 검토 결과를 바탕으로 설계를 보완합니다.

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "데이터베이스의 '테이블'은 엑셀의 무엇에 해당하나요?",
      "header": "DB 개념 이해",
      "options": [
        {"label": "엑셀 파일 전체", "description": ""},
        {"label": "하나의 시트(Sheet)", "description": ""},
        {"label": "셀 하나", "description": ""},
        {"label": "행 하나", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "Rails에서 '마이그레이션(migration)'이란 무엇인가요?",
      "header": "마이그레이션 이해",
      "options": [
        {"label": "서버를 다른 컴퓨터로 이전하는 작업", "description": ""},
        {"label": "DB 구조 변경 사항을 파일로 기록하여 팀 전체가 같은 구조를 유지하게 하는 것", "description": ""},
        {"label": "오래된 데이터를 새 형식으로 변환하는 것", "description": ""},
        {"label": "데이터베이스를 백업하는 방법", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번째 질문 → "하나의 시트(Sheet)"
- 2번째 질문 → "DB 구조 변경 사항을 파일로 기록하여 팀 전체가 같은 구조를 유지하게 하는 것"

해설:
- 테이블 vs 시트: 엑셀에서 한 파일 안에 여러 시트가 있듯, 데이터베이스 안에 여러 테이블이 있습니다. `users` 테이블, `books` 테이블처럼 데이터 종류별로 테이블이 분리됩니다.
- 마이그레이션: DB 구조를 코드 파일로 기록합니다. 덕분에 팀원이 `bin/rails db:migrate`만 실행하면 내가 바꾼 DB 구조와 똑같이 맞춰집니다. 혼자 개발해도 배포 서버에서 같은 명령어로 서버 DB를 업데이트할 수 있습니다.
