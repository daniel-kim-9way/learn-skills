## EXPLAIN

### localhost vs 인터넷

지금까지 만든 서비스는 `http://localhost:3000`에서 돌아갑니다. 이 주소의 의미는 **"내 컴퓨터 안에만 있다"**입니다.

친구에게 링크를 보내도 볼 수 없습니다. 마치 집 안 TV와 같습니다. 아무리 좋은 프로그램을 틀어도 집 밖에서는 볼 수 없습니다.

**배포(Deploy)**는 서비스를 인터넷 어딘가의 컴퓨터(서버)에 올려서 전 세계 누구든 접근할 수 있게 만드는 작업입니다.

배포 후에는:
- `https://내서비스.railway.app` 같은 URL이 생깁니다
- 24시간 컴퓨터를 켜지 않아도 돌아갑니다
- 전 세계 어디서든 접근할 수 있습니다

**이 URL을 누구에게든 보내면 볼 수 있습니다.** 이것이 오늘의 순간입니다.

### Railway vs Render

| | Railway | Render |
|--|---------|--------|
| 난이도 | 쉬움 | 쉬움 |
| 무료 플랜 | 500시간/월 | 750시간/월 |
| 속도 | 빠름 | 보통 (무료는 느릴 수 있음) |
| GitHub 연동 | 자동 배포 | 자동 배포 |
| 추천 | Rails에 특히 좋음 | 다양한 프레임워크 |

**Railway 추천** — 특히 Rails 앱은 설정이 더 간단합니다.

### Production 환경

| | 개발 환경 | Production |
|--|----------|------------|
| 목적 | 빠른 수정 | 안정 운영 |
| 오류 표시 | 상세 정보 | 일반 메시지 (보안) |
| 성능 | 최적화 안 됨 | 캐싱, 압축 적용 |
| 비밀 키 | .env 파일 | 환경 변수 설정 |

## EXECUTE

### 단계 1: Production 환경 준비

```
서비스를 Railway에 배포하려고 해.
production 환경 준비를 해줘.

필요한 것:
- Procfile 또는 railway.toml 설정
- 환경 변수 목록 정리
- 데이터베이스 production 설정
- SECRET_KEY_BASE 처리
```

### 단계 2: Railway로 배포

1. https://railway.app → GitHub 로그인
2. "New Project" → "Deploy from GitHub repo"
3. 내 서비스 리포지토리 선택
4. 환경 변수 설정:
   - Variables 탭 → Add Variable
   - RAILS_ENV=production
   - RAILS_MASTER_KEY (config/master.key 값)
   - Claude가 알려준 기타 환경 변수
5. 자동 배포 시작 → 빌드 로그 확인

배포 중 오류가 나면:
```
Railway 배포 중 이 오류가 났어:
[오류 메시지 붙여넣기]
해결해줘.
```

### 단계 3: THE MOMENT

배포가 완료되면 Railway가 URL을 알려줍니다.

**이 순간이 바로 그 순간입니다.**

브라우저에서 그 URL을 열어봅니다. 내가 만든 서비스가 인터넷에 있습니다. 이 URL을 복사해서 아무에게나 보내면 볼 수 있습니다.

**폰에서도 접속해봅니다.** 포켓 속 폰에서 내가 만든 서비스가 열리는 순간을 느껴봅니다.

### 단계 4: 도메인 연결 (선택)

Railway 기본 URL(`xxx.railway.app`)을 써도 되지만, 내 도메인을 연결하면 더 전문적입니다.

도메인 구매: 가비아(gabia.com) 또는 AWS Route 53 (연간 약 만 원)

Railway에서:
1. Settings → Custom Domain
2. 도메인 입력 (예: myservice.kr)
3. CNAME 레코드 추가 (Railway 안내 따라)
4. 5~30분 후 내 도메인으로 접속 확인

## QUIZ

AskUserQuestion({
  "questions": [
    {
      "question": "localhost:3000이 다른 사람에게 보이지 않는 이유는?",
      "header": "배포 개념",
      "options": [
        {"label": "서비스에 버그가 있어서", "description": ""},
        {"label": "서비스가 내 컴퓨터에만 존재하고 인터넷에 연결되지 않아서", "description": ""},
        {"label": "비밀번호가 설정되어 있어서", "description": ""},
        {"label": "포트 번호가 잘못돼서", "description": ""}
      ],
      "multiSelect": false
    },
    {
      "question": "Production 환경에서 오류가 발생하면 어떻게 표시되어야 하나요?",
      "header": "Production 환경",
      "options": [
        {"label": "코드와 스택 트레이스 포함 상세 정보", "description": ""},
        {"label": "일반적인 오류 메시지만 (보안 위해 상세 정보 숨김)", "description": ""},
        {"label": "서버를 즉시 재시작", "description": ""},
        {"label": "오류를 무시하고 계속 진행", "description": ""}
      ],
      "multiSelect": false
    }
  ]
})

정답:
- 1번 → "서비스가 내 컴퓨터에만 존재하고 인터넷에 연결되지 않아서"
- 2번 → "일반적인 오류 메시지만 (보안 위해 상세 정보 숨김)"

해설:
- localhost: "내 컴퓨터"를 가리키는 주소입니다. 배포는 서비스를 인터넷 서버에 옮기는 작업입니다.
- Production 오류: 상세 오류를 노출하면 공격자가 시스템 구조를 파악할 수 있습니다. 일반 메시지만 표시하고 상세 정보는 로그에만 기록합니다.
