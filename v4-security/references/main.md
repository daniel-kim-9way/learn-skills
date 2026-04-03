## EXPLAIN

### 내 사용자를 보호하는 방패

보안이라고 하면 "해킹", "유출" 같은 무서운 단어가 떠오릅니다. 하지만 관점을 바꿔봅시다.

보안은 **내가 만든 서비스를 사용하는 사람들을 보호하는 방패**입니다. 내 서비스를 믿고 가입한 사용자의 이름, 이메일, 비밀번호를 지키는 것입니다. 이것은 기술 문제가 아니라 **책임**입니다.

좋은 소식: Rails 같은 현대 프레임워크는 대부분의 기본 보안을 자동으로 처리합니다. 우리가 할 일은 **실수하지 않는 것**과 **기본 설정을 올바르게 유지하는 것**입니다.

### 주요 보안 위협 (일상 비유)

**환경 변수 노출 — 열쇠를 문 앞에 두기**
API 키나 비밀번호를 소스 코드에 직접 넣으면 GitHub에 올릴 때 전 세계에 공개됩니다.

**인증 우회 — 자물쇠 없는 문**
"관리자 페이지에 로그인 체크를 깜빡했다." 누구든 /admin에 접근하면 모든 데이터를 볼 수 있습니다.

**XSS (Cross-Site Scripting) — 댓글에 악성 코드 심기**
사용자가 입력한 텍스트에 JavaScript 코드가 포함되면, 다른 사용자의 브라우저에서 실행될 수 있습니다.

**SQL 인젝션 — 빈칸에 악의적인 명령어 넣기**
입력 양식에 SQL 명령어를 넣어 데이터베이스를 조작하려는 공격입니다. Rails의 ActiveRecord가 자동으로 막아줍니다.

**CSRF (사이트 간 요청 위조) — 위조 편지**
다른 사이트에서 사용자 몰래 우리 서비스에 요청을 보내는 공격입니다. Rails가 자동으로 CSRF 토큰으로 방어합니다.

### 10개 체크리스트 미리 보기

1. .env 파일이 .gitignore에 있는가
2. 인증 보호: 로그인 필요한 페이지가 보호되는가
3. HTTPS 강제 적용 (production)
4. 관리자 페이지 접근 제한
5. Strong Parameters 설정
6. XSS 방어 (이스케이프 처리)
7. CSRF 방어 (토큰 확인)
8. Raw SQL 사용 여부
9. 비밀번호 암호화
10. Production 오류 메시지 숨김

## EXECUTE

### 단계 1: Claude에게 10개 보안 체크리스트 실행 요청

```
내 서비스의 보안 체크리스트를 실행해줘.
아래 10가지 항목을 하나씩 확인하고 결과를 알려줘:

1. 환경 변수: .env 파일이 .gitignore에 있는지
2. 인증 보호: 로그인 없이 접근하면 안 되는 페이지가 보호되는지
3. HTTPS: Production에서 HTTPS가 강제 적용되는지
4. 관리자 페이지: /admin 접근이 인증으로 보호되는지
5. 파라미터 검증: Strong Parameters가 올바르게 설정됐는지
6. XSS 방어: 사용자 입력을 HTML에 출력할 때 이스케이프 처리되는지
7. CSRF 방어: form에 CSRF 토큰이 포함되는지
8. SQL 인젝션: Raw SQL 쿼리를 직접 쓰는 곳이 없는지
9. 비밀번호 암호화: 비밀번호가 평문 저장되지 않는지
10. 에러 메시지: Production에서 상세 오류가 노출되지 않는지

각 항목: ✅ 통과 / ⚠️ 주의 / ❌ 즉시 수정 필요
```

### 단계 2: 문제 항목 즉시 수정

❌ 또는 ⚠️ 항목이 있으면 즉시 수정합니다:

```
[항목 번호] 항목이 ❌야. 수정해줘.
```

모든 항목이 ✅가 될 때까지 반복합니다.

### 단계 3: 보안 Sign-off

모든 항목 통과 후:

```
보안 체크리스트 결과를 요약해줘.
10개 항목 모두 통과했으면 "보안 점검 완료" 확인서를 만들어줘.
날짜와 점검 항목 목록 포함.
```

이 확인서는 "나는 기본 보안을 점검하고 서비스를 오픈한다"는 자기 자신과의 약속입니다.

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "폼에 SQL 명령어를 입력해서 데이터베이스를 조작하려는 공격은?",
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
      "question": "다음 중 즉각적인 보안 위험에 해당하는 것은?",
      "header": "보안 위험 식별",
      "options": [
        {"label": "서비스 이름이 길다", "description": ""},
        {"label": "API 키가 소스 코드에 포함되어 있다", "description": ""},
        {"label": "페이지 로딩이 느리다", "description": ""},
        {"label": "도메인이 연결되지 않았다", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "Rails에서 사용자 입력을 안전하게 처리하는 핵심 메커니즘은?",
      "header": "Rails 보안 기능",
      "options": [
        {"label": "모든 입력을 거부한다", "description": ""},
        {"label": "Strong Parameters로 허용할 파라미터를 명시적으로 지정한다", "description": ""},
        {"label": "입력 길이를 10자로 제한한다", "description": ""},
        {"label": "사용자에게 보안 교육을 한다", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번 → "SQL 인젝션"
- 2번 → "API 키가 소스 코드에 포함되어 있다"
- 3번 → "Strong Parameters로 허용할 파라미터를 명시적으로 지정한다"

해설:
- SQL 인젝션: 사용자 입력을 그대로 SQL에 삽입하면 DB를 조작할 수 있습니다. Rails ActiveRecord가 자동 방어합니다.
- API 키 노출: 소스 코드에 API 키가 있으면 GitHub에서 공개됩니다. 봇들이 24시간 스캔합니다. 발견 즉시 재발급해야 합니다.
- Strong Parameters: 폼 데이터 중 허용할 필드를 명시적으로 지정합니다. permit(:name, :email)로 지정하면 나머지는 무시됩니다.
