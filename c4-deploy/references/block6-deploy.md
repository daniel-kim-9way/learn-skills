## EXPLAIN

### localhost vs 인터넷: 무슨 차이?

지금까지 만든 서비스는 `http://localhost:3000`에서 돌아가고 있습니다. 이 주소의 의미는 "**내 컴퓨터 안에 있다**"입니다.

친구에게 "내 서비스 써봐"라고 링크를 보내면 친구는 볼 수 없습니다. 왜냐하면 그 서비스가 내 컴퓨터에만 존재하기 때문입니다.

마치 집 안에 있는 TV와 같습니다. 아무리 좋은 프로그램을 틀어도 집 밖에서는 볼 수 없습니다.

**배포(Deploy)**는 내 서비스를 **인터넷 어딘가의 컴퓨터(서버)**에 올려서 전 세계 누구든 접근할 수 있게 만드는 작업입니다.

배포 후에는:
- `https://내서비스이름.railway.app` 같은 주소가 생깁니다
- 24시간 컴퓨터를 켜지 않아도 서비스가 돌아갑니다
- 전 세계 어디서든 접근 가능합니다

### Railway vs Render: 어떤 걸 쓸까?

비개발자에게 친화적인 배포 플랫폼 두 가지:

| | Railway | Render |
|--|---------|--------|
| 시작 난이도 | ★★☆ (쉬움) | ★★☆ (쉬움) |
| 무료 플랜 | 500시간/월 | 750시간/월 |
| 속도 | 빠름 | 보통 (무료는 느릴 수 있음) |
| 한국어 지원 | 일부 | 일부 |
| GitHub 연동 | 자동 배포 지원 | 자동 배포 지원 |
| 추천 상황 | Rails, Node.js | 다양한 프레임워크 |

**Railway 추천** — 특히 Rails 앱은 Railway가 설정이 더 간단합니다.

### Production 환경이란?

개발 환경(development)과 실제 서비스 환경(production)은 다르게 동작합니다.

| | 개발 환경 | Production 환경 |
|--|----------|----------------|
| 목적 | 빠른 수정, 디버깅 | 안정적 운영, 보안 |
| 오류 표시 | 상세한 오류 정보 | 일반 오류 메시지 (보안) |
| 성능 | 최적화 안 됨 | 캐싱, 압축 적용 |
| 비밀 키 | .env 파일 | 환경 변수 설정 필요 |

## EXECUTE

### 단계 1: Production 환경 준비
배포 전에 Claude에게 준비를 요청합니다:

```
서비스를 Railway에 배포하려고 해.
production 환경으로 배포할 수 있게 준비해줘.

필요한 것:
- Procfile 또는 railway.toml 설정
- 환경 변수 목록 정리 (어떤 환경 변수가 필요한지)
- 데이터베이스 production 설정 확인
- SECRET_KEY_BASE 같은 보안 키 처리 방법
```

### 단계 2: Railway로 배포
1. https://railway.app 접속 → GitHub로 로그인
2. "New Project" → "Deploy from GitHub repo" 클릭
3. 내 서비스 리포지토리 선택
4. 환경 변수 설정:
   - Variables 탭 → Add Variable
   - RAILS_ENV=production
   - RAILS_MASTER_KEY (config/master.key 값)
   - 기타 Claude가 알려준 환경 변수들
5. 자동 배포 시작 → 완료되면 URL 확인

만약 배포 중 오류가 나면:
```
Railway 배포 중 이런 오류가 났어:
[오류 메시지 붙여넣기]
해결해줘.
```

### 단계 3: 도메인 연결 (선택)
Railway가 제공하는 기본 URL(`xxx.railway.app`)을 사용해도 되지만, 내 도메인을 연결하면 더 전문적으로 보입니다.

도메인 구매: 가비아(gabia.com) 또는 AWS Route 53 (~만 원/년)

Railway에서:
1. Settings → Custom Domain
2. 도메인 입력 (예: myservice.kr)
3. CNAME 레코드를 도메인 등록업체에 추가 (Railway가 안내해줌)
4. 5~30분 후 내 도메인으로 접속 확인

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "localhost:3000 주소가 다른 사람에게 보이지 않는 이유는?",
      "header": "배포 개념",
      "options": [
        {"label": "서비스에 버그가 있어서", "description": ""},
        {"label": "서비스가 내 컴퓨터 안에만 존재하고 인터넷에 연결되지 않아서", "description": ""},
        {"label": "비밀번호가 설정되어 있어서", "description": ""},
        {"label": "포트 번호가 잘못되어서", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "Production 환경에서 오류가 발생하면 어떻게 표시되어야 하나요?",
      "header": "Production 환경",
      "options": [
        {"label": "코드와 스택 트레이스를 포함한 상세한 오류 정보", "description": ""},
        {"label": "일반적인 오류 메시지만 표시 (보안을 위해 상세 정보 숨김)", "description": ""},
        {"label": "오류가 발생하면 서버를 즉시 재시작", "description": ""},
        {"label": "오류를 무시하고 계속 진행", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번째 질문 → "서비스가 내 컴퓨터 안에만 존재하고 인터넷에 연결되지 않아서"
- 2번째 질문 → "일반적인 오류 메시지만 표시 (보안을 위해 상세 정보 숨김)"

해설:
- localhost: localhost는 "내 컴퓨터"를 가리키는 주소입니다. 이 주소에서 돌아가는 서비스는 내 컴퓨터에서만 접근 가능합니다. 배포는 이 서비스를 인터넷 서버에 옮기는 작업입니다.
- Production 오류 표시: 개발 환경에서는 빠른 디버깅을 위해 상세한 오류 정보가 필요합니다. 하지만 Production에서 상세한 오류를 노출하면 악의적인 사용자가 시스템 구조를 파악해 공격할 수 있습니다. 따라서 "문제가 발생했습니다" 같은 일반 메시지만 표시하고 상세 정보는 로그에만 기록합니다.
