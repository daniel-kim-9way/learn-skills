## EXPLAIN

### 크롬 익스텐션이란?

브라우저 오른쪽 위의 작은 아이콘들 -- 광고 차단기, 번역기 등이 전부 크롬 익스텐션입니다. **HTML + CSS + JavaScript**로만 만들어집니다.

### Manifest V3 = 익스텐션의 신분증

```json
{
  "manifest_version": 3,
  "name": "나의 첫 익스텐션",
  "version": "1.0",
  "description": "간단한 설명",
  "action": { "default_popup": "popup.html" },
  "permissions": ["activeTab"]
}
```

### 익스텐션의 세 가지 유형

| 유형 | 설명 | 예시 |
|------|------|------|
| **Popup** | 아이콘 클릭 시 작은 창 | 메모장, 할 일 목록 |
| **Content Script** | 웹 페이지 내용 수정 | 광고 숨기기 |
| **Background** | 백그라운드 동작 | 알림 |

초보자에게는 **Popup**이 가장 쉽고 결과가 바로 보입니다.

---

## EXECUTE

### Step 1: 아이디어 선정 (5분)

> "브라우저에서 '이런 기능이 있으면 좋겠다'고 생각한 적 있나요?"

예시: 새 탭에 할 일 표시, 텍스트 글자 수 세기, 색상 코드 복사, 서비스 바로가기

### Step 2: 프로젝트 폴더 생성 (3분)

```bash
mkdir -p ~/chrome-extensions/my-first-extension
```

파일 구조: `manifest.json`, `popup.html`, `popup.css`, `popup.js`

### Step 3: manifest.json 작성 (3분)

```json
{
  "manifest_version": 3,
  "name": "학생의 익스텐션 이름",
  "version": "1.0",
  "action": { "default_popup": "popup.html" },
  "permissions": ["activeTab", "storage"]
}
```

### Step 4: Popup UI 만들기 (10분)

Claude와 함께 popup.html, popup.css, popup.js를 작성한다. 학생 아이디어에 맞게 Claude가 코드를 생성하도록 한다.

팝업 크기는 width: 300px 정도가 적당.

### Step 5: 크롬에 로드하기 (5분)

1. `chrome://extensions` 접속
2. "개발자 모드" 토글 켜기
3. "압축해제된 확장 프로그램을 로드합니다" 클릭
4. 만든 폴더 선택

> "아이콘이 브라우저에 나타났나요? 클릭해보세요!"

오류 시 "오류" 버튼으로 메시지 확인 후 수정.

### Step 6: 테스트 및 수정 (5분)

팝업이 열리는지, 기능이 동작하는지 확인. 수정 후 `chrome://extensions`에서 새로고침 아이콘 클릭.

### Step 7: 기능 확장 (7분)

하나 더 추가: 데이터 저장(chrome.storage), 디자인 개선, 기능 추가 등.

```javascript
// 데이터 저장 예시
chrome.storage.local.set({ todos: todoArray });
chrome.storage.local.get(['todos'], (result) => {
  if (result.todos) loadTodos(result.todos);
});
```

> "chrome.storage를 사용하면 브라우저를 닫았다 열어도 데이터가 유지됩니다."

git commit (선택).

---

## QUIZ

### Q1: manifest.json의 역할
> "manifest.json이 없으면 어떻게 될까요?"

1. 익스텐션이 느리게 동작한다
2. 크롬이 이 폴더를 익스텐션으로 인식하지 못한다
3. 팝업 디자인이 깨진다
4. 아무 영향 없다

정답: 2번
해설: manifest.json은 익스텐션의 신분증입니다. 이 파일이 없으면 크롬은 폴더를 익스텐션으로 인식할 수 없습니다.

### Q2: 개발자 모드
> "크롬에서 '개발자 모드'를 켜야 하는 이유는?"

1. 코드를 더 빠르게 실행하기 위해
2. 스토어에 등록하지 않은 로컬 익스텐션을 로드하기 위해
3. JavaScript를 사용하기 위해
4. 인터넷 연결 없이 사용하기 위해

정답: 2번
해설: 개발자 모드를 켜면 로컬 폴더에서 직접 익스텐션을 로드할 수 있어 개발과 테스트가 가능합니다.
