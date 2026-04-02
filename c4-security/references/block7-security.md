## EXPLAIN

### 왜 오픈 전에 보안을 확인해야 하나?

집을 짓고 나서 문에 자물쇠를 달지 않고 살겠다는 사람은 없습니다. 서비스도 마찬가지입니다.

서비스를 인터넷에 올리는 순간, 전 세계 수억 명이 접근할 수 있습니다. 그 중 일부는 악의를 가진 사람들입니다. 봇(자동화 프로그램)들은 24시간 새로운 서비스를 찾아 취약점을 스캔합니다.

보안 문제가 발생하면:
- 고객 데이터가 유출됩니다
- 서비스가 마비됩니다
- 법적 책임이 생깁니다 (개인정보보호법)
- 신뢰를 잃습니다 (회복이 매우 어려움)

좋은 소식: Rails와 같은 현대 프레임워크는 대부분의 기본 보안을 자동으로 처리합니다. 우리가 할 일은 **실수하지 않는 것**과 **기본 설정을 올바르게 유지하는 것**입니다.

### 주요 보안 위협 (일상 비유로)

**SQL 인젝션** — 빈칸에 악의적인 명령어 넣기

은행 창구에서 이름을 입력하는 양식에 "'; DROP TABLE accounts;--"라고 쓰면? 만약 시스템이 이를 그대로 실행하면 계좌 정보가 모두 삭제됩니다. Rails의 ActiveRecord는 이를 자동으로 막아줍니다.

**XSS (Cross-Site Scripting)** — 댓글에 악성 코드 심기

다른 사용자가 볼 수 있는 댓글에 JavaScript 코드를 심으면, 댓글을 읽는 모든 사람의 브라우저에서 그 코드가 실행됩니다. 쿠키(로그인 정보)를 탈취하는 데 사용됩니다.

**인증 우회** — 자물쇠 없는 문

"관리자 페이지는 /admin에 있는데 로그인 체크를 깜빡했다." 누구든 /admin에 접근하면 모든 데이터를 볼 수 있습니다.

**환경 변수 노출** — 열쇠를 문 앞에 두기

API 키나 비밀번호를 소스 코드에 직접 넣으면, GitHub에 올릴 때 전 세계에 공개됩니다.

## EXECUTE

### Pre-Quiz (시나리오 기반 사전 점검)

AskUserQuestion({
  "questions": [
    {
      "question": "[시나리오 A] 사용자가 폼에 '이름' 대신 <script>alert('해킹!')</script>을 입력했습니다. 어떤 보안 위협인가요?",
      "header": "Pre-Quiz: 보안 위협 식별",
      "options": [
        {"label": "SQL 인젝션", "description": ""},
        {"label": "XSS (Cross-Site Scripting)", "description": ""},
        {"label": "CSRF (사이트 간 요청 위조)", "description": ""},
        {"label": "서버 과부하 공격 (DDoS)", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "[시나리오 B] 개발자가 실수로 .env 파일을 GitHub에 올렸습니다. 즉시 해야 할 행동은?",
      "header": "Pre-Quiz: 키 노출 대응",
      "options": [
        {"label": "커밋을 삭제하고 기다린다", "description": ""},
        {"label": "모든 API 키와 비밀번호를 즉시 재발급한다", "description": ""},
        {"label": "리포지토리를 private으로 변경한다", "description": ""},
        {"label": "아무것도 안 해도 된다 (나만 보는 리포지토리라서)", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

---

### 10개 보안 체크리스트 실행
Claude에게 아래를 요청합니다:

```
내 Rails 서비스의 보안 체크리스트를 실행해줘.
아래 10가지 항목을 하나씩 확인하고 결과를 알려줘:

1. 환경 변수: .env 파일이 .gitignore에 있는지 확인
2. 인증 보호: 로그인 없이 접근하면 안 되는 페이지가 보호되는지 확인
3. HTTPS: Production에서 HTTPS가 강제 적용되는지 확인
4. 관리자 페이지: /admin 접근이 인증으로 보호되는지 확인
5. 파라미터 검증: Strong Parameters가 올바르게 설정됐는지 확인
6. XSS 방어: 사용자 입력을 HTML에 출력할 때 이스케이프 처리되는지 확인
7. CSRF 방어: form에 CSRF 토큰이 포함되는지 확인
8. SQL 인젝션: Raw SQL 쿼리를 직접 쓰는 곳이 없는지 확인
9. 비밀번호 암호화: 비밀번호가 평문으로 저장되지 않는지 확인
10. 에러 메시지: Production에서 상세한 오류 정보가 노출되지 않는지 확인

각 항목 상태: ✅ 통과 / ⚠️ 주의 / ❌ 즉시 수정 필요
```

❌ 항목이 있으면 즉시 수정합니다:
```
[항목 번호] 항목이 ❌야. 수정해줘.
```

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "사용자가 폼에 SQL 명령어를 입력해서 데이터베이스를 조작하려는 공격은?",
      "header": "보안 위협 유형",
      "options": [
        {"label": "XSS (Cross-Site Scripting)", "description": ""},
        {"label": "SQL 인젝션", "description": ""},
        {"label": "CSRF", "description": ""},
        {"label": "DDoS", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "Rails에서 사용자 입력을 안전하게 처리하기 위한 핵심 메커니즘은?",
      "header": "Rails 보안 기능",
      "options": [
        {"label": "모든 입력을 거부한다", "description": ""},
        {"label": "Strong Parameters로 허용할 파라미터를 명시적으로 지정한다", "description": ""},
        {"label": "입력 길이를 10자로 제한한다", "description": ""},
        {"label": "사용자에게 보안 교육을 한다", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "다음 중 즉각적인 보안 위험에 해당하는 것은?",
      "header": "보안 위험 식별",
      "options": [
        {"label": "서비스 이름이 길다", "description": ""},
        {"label": "API 키가 소스 코드에 직접 포함되어 있다", "description": ""},
        {"label": "페이지 로딩이 느리다", "description": ""},
        {"label": "도메인이 아직 연결되지 않았다", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번째 질문 → "SQL 인젝션"
- 2번째 질문 → "Strong Parameters로 허용할 파라미터를 명시적으로 지정한다"
- 3번째 질문 → "API 키가 소스 코드에 직접 포함되어 있다"

해설:
- SQL 인젝션: 사용자 입력을 그대로 SQL 쿼리에 삽입하면 데이터베이스를 조작할 수 있습니다. Rails의 ActiveRecord는 파라미터를 자동으로 이스케이프해서 기본적으로 방어합니다.
- Strong Parameters: Rails에서 폼으로 받은 데이터 중 허용할 필드를 명시적으로 지정하는 메커니즘입니다. permit(:name, :email)처럼 지정하면 그 외의 필드는 무시됩니다.
- API 키 노출: 소스 코드에 API 키가 있으면 GitHub 등에 올릴 때 공개될 수 있습니다. 악의적인 봇들은 GitHub를 스캔해서 노출된 키를 자동으로 수집합니다. 발견 즉시 키를 재발급해야 합니다.
