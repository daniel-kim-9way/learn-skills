## EXPLAIN

### 크롬 익스텐션이란?

브라우저 오른쪽 위에 작은 아이콘들이 있죠? 광고 차단기, 번역기, 다크 모드, 스크린 캡처 — 이것들이 전부 **크롬 익스텐션(확장 프로그램)**입니다.

놀라운 사실: 이것들은 **HTML + CSS + JavaScript**로만 만들어집니다. 여러분이 이미 알고 있는 웹 기술과 동일합니다. 특별한 프로그래밍 언어가 필요 없습니다.

왜 크롬 익스텐션을 만들까요?

- **내 서비스와 연결**: 서비스 바로가기, 알림 확인
- **업무 효율화**: 자주 하는 작업을 버튼 하나로
- **웹 개선**: 특정 사이트에 기능 추가
- **포트폴리오**: "저는 크롬 익스텐션도 만들어봤습니다"

### Manifest V3 = 익스텐션의 "설계도"

모든 크롬 익스텐션에는 `manifest.json`이라는 파일이 있어야 합니다. 이것은 익스텐션의 **신분증이자 설계도**입니다.

크롬이 이 파일을 읽고 판단합니다:
- "이 익스텐션 이름이 뭐지?" → `name`
- "버전은?" → `version`
- "아이콘 클릭하면 뭐 보여줘?" → `action.default_popup`
- "어떤 권한이 필요해?" → `permissions`

```json
{
  "manifest_version": 3,
  "name": "나의 첫 익스텐션",
  "version": "1.0",
  "description": "서비스 바로가기 & 간단 메모",
  "action": {
    "default_popup": "popup.html",
    "default_icon": "icon.png"
  },
  "permissions": ["activeTab", "storage"]
}
```

`manifest_version: 3`은 최신 규격입니다. 구글이 보안과 성능을 위해 V2에서 V3로 업그레이드했습니다. 새로 만드는 익스텐션은 반드시 V3를 사용해야 합니다.

### 익스텐션의 세 가지 구성 요소

크롬 익스텐션은 용도에 따라 세 가지 방식으로 동작합니다:

| 구성 요소 | 비유 | 하는 일 | 예시 |
|----------|------|--------|------|
| **Popup** | 메모 포스트잇 | 아이콘 클릭 시 작은 창을 띄움 | 할 일 목록, 계산기, 바로가기 |
| **Content Script** | 마술사의 손 | 현재 보고 있는 웹페이지를 수정 | 광고 숨기기, 글자 크기 변경, 번역 |
| **Background (Service Worker)** | 경비원 | 보이지 않는 곳에서 백그라운드 동작 | 알림, 데이터 동기화 |

초보자에게 가장 추천하는 것은 **Popup**입니다. 이유:
- 결과가 **바로** 보입니다 (아이콘 클릭 → 창이 뜸)
- 일반 웹페이지 만드는 것과 **똑같습니다** (HTML + CSS)
- 다른 사이트에 영향을 **주지 않습니다** (안전)

### Popup = 작은 웹페이지

Popup은 그냥 **작은 HTML 페이지**입니다. 브라우저 아이콘을 클릭하면 300~400px 너비의 작은 창에 표시됩니다.

```html
<!-- popup.html -->
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="popup.css">
</head>
<body>
  <h1>내 메모장</h1>
  <textarea id="memo" placeholder="메모를 입력하세요..."></textarea>
  <button id="saveBtn">저장</button>
  <script src="popup.js"></script>
</body>
</html>
```

일반 웹페이지와 다른 점 딱 **2가지**:
1. **크기가 작다** — 팝업이니까 300px 정도
2. **chrome API를 쓸 수 있다** — `chrome.storage`, `chrome.tabs` 등

### Content Script = 웹페이지에 기능 추가

Content Script는 **다른 사람의 웹사이트에 코드를 주입**하는 것입니다.

예를 들어 "모든 웹사이트에서 선택한 텍스트의 글자 수를 보여주는 익스텐션"을 만들 수 있습니다:

```javascript
// content.js — 사용자가 방문하는 웹페이지에서 실행됩니다
document.addEventListener("mouseup", () => {
  const selectedText = window.getSelection().toString();
  if (selectedText.length > 0) {
    // 선택한 텍스트의 글자 수를 표시
    showBadge(selectedText.length);
  }
});
```

manifest.json에서 어떤 사이트에서 실행할지 지정합니다:

```json
{
  "content_scripts": [
    {
      "matches": ["<all_urls>"],
      "js": ["content.js"]
    }
  ]
}
```

`<all_urls>`는 모든 웹사이트에서 실행한다는 뜻입니다. 특정 사이트만 대상으로 하려면 `["https://www.google.com/*"]`처럼 지정할 수 있습니다.

### chrome.storage = 브라우저에 데이터 저장

일반 웹에서는 데이터를 서버에 저장합니다. 크롬 익스텐션에서는 **브라우저 자체에** 저장할 수 있습니다:

```javascript
// 저장
chrome.storage.local.set({ memo: "오늘 할 일: 보고서 작성" });

// 불러오기
chrome.storage.local.get(["memo"], (result) => {
  console.log(result.memo);  // "오늘 할 일: 보고서 작성"
});
```

서버 없이도 데이터가 유지됩니다. 브라우저를 닫았다 열어도, 컴퓨터를 재시작해도 남아있습니다.

---

## EXECUTE

### Step 1: 아이디어 선정 (5분)

> "브라우저에서 '이런 기능이 있으면 좋겠다'고 생각한 적 있나요? 또는 내 서비스와 연결되는 익스텐션이 있으면 유용할까요?"

아이디어 예시:
- **서비스 바로가기** — 아이콘 클릭 → 내 서비스 빠른 접근 + 알림 확인
- **메모장** — 간단한 메모 저장, 브라우저 닫아도 유지
- **글자 수 세기** — 텍스트 선택하면 글자 수 표시
- **색상 코드 복사** — 웹페이지에서 색상을 클릭하면 코드 복사
- **새 탭 커스텀** — 새 탭 열면 할 일 목록 표시
- **번역 도우미** — 선택한 텍스트를 번역

첫 익스텐션은 **Popup 형태**를 추천합니다. 가장 간단하고 결과가 바로 보입니다.

### Step 2: 프로젝트 폴더 생성 (3분)

```bash
mkdir -p ~/chrome-extensions/my-first-extension
```

필요한 파일 4개를 만듭니다:

```
my-first-extension/
  manifest.json    ← 설계도 (필수)
  popup.html       ← 화면 (필수)
  popup.css        ← 디자인
  popup.js         ← 동작
```

> "이 4개 파일이 전부입니다. 서버도, 데이터베이스도, 빌드 도구도 필요 없습니다."

### Step 3: manifest.json 작성 — 설계도 만들기 (3분)

```json
{
  "manifest_version": 3,
  "name": "나의 메모장",
  "version": "1.0",
  "description": "간단한 메모를 저장하는 크롬 익스텐션",
  "action": {
    "default_popup": "popup.html"
  },
  "permissions": ["storage"]
}
```

각 항목 설명:
- `manifest_version`: 3 — 최신 규격, 반드시 3
- `name` — 크롬에 표시될 익스텐션 이름
- `version` — 버전 번호, 업데이트 시 올림
- `action.default_popup` — 아이콘 클릭 시 보여줄 HTML 파일
- `permissions` — 필요한 권한 (storage = 데이터 저장)

> "Claude에게 '내 아이디어에 맞는 manifest.json을 만들어줘'라고 요청하세요. 아이디어에 따라 permissions가 달라집니다."

### Step 4: Popup UI 만들기 — HTML+CSS+JS (10분)

Claude와 함께 학생 아이디어에 맞는 popup을 만듭니다.

메모장 예시:

```html
<!-- popup.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="popup.css">
</head>
<body>
  <div class="container">
    <h1>메모장</h1>
    <textarea id="memo" placeholder="메모를 입력하세요..."></textarea>
    <div class="button-group">
      <button id="saveBtn" class="btn btn-primary">저장</button>
      <button id="clearBtn" class="btn btn-secondary">지우기</button>
    </div>
    <p id="status" class="status"></p>
  </div>
  <script src="popup.js"></script>
</body>
</html>
```

```css
/* popup.css */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  width: 320px;
  font-family: 'Apple SD Gothic Neo', 'Malgun Gothic', sans-serif;
}

.container {
  padding: 16px;
}

h1 {
  font-size: 18px;
  color: #1F2937;
  margin-bottom: 12px;
}

textarea {
  width: 100%;
  height: 120px;
  padding: 10px;
  border: 1px solid #D1D5DB;
  border-radius: 8px;
  font-size: 14px;
  resize: none;
  outline: none;
}

textarea:focus {
  border-color: #4F46E5;
  box-shadow: 0 0 0 2px rgba(79, 70, 229, 0.1);
}

.button-group {
  display: flex;
  gap: 8px;
  margin-top: 10px;
}

.btn {
  flex: 1;
  padding: 8px 0;
  border: none;
  border-radius: 6px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.btn-primary {
  background-color: #4F46E5;
  color: white;
}

.btn-primary:hover {
  background-color: #4338CA;
}

.btn-secondary {
  background-color: #F3F4F6;
  color: #374151;
}

.btn-secondary:hover {
  background-color: #E5E7EB;
}

.status {
  margin-top: 8px;
  font-size: 12px;
  color: #10B981;
  text-align: center;
  min-height: 18px;
}
```

```javascript
// popup.js
document.addEventListener("DOMContentLoaded", () => {
  const memo = document.getElementById("memo");
  const saveBtn = document.getElementById("saveBtn");
  const clearBtn = document.getElementById("clearBtn");
  const status = document.getElementById("status");

  // 저장된 메모 불러오기
  chrome.storage.local.get(["memo"], (result) => {
    if (result.memo) {
      memo.value = result.memo;
    }
  });

  // 저장 버튼
  saveBtn.addEventListener("click", () => {
    chrome.storage.local.set({ memo: memo.value }, () => {
      status.textContent = "저장되었습니다!";
      setTimeout(() => { status.textContent = ""; }, 2000);
    });
  });

  // 지우기 버튼
  clearBtn.addEventListener("click", () => {
    memo.value = "";
    chrome.storage.local.remove("memo", () => {
      status.textContent = "삭제되었습니다.";
      setTimeout(() => { status.textContent = ""; }, 2000);
    });
  });
});
```

> "팝업의 너비는 body에서 설정합니다. 320px 정도가 가장 자연스럽습니다. 너무 크면 불편하고, 너무 작으면 내용이 안 들어갑니다."

### Step 5: 크롬에 로드하기 — 내 익스텐션 설치 (5분)

1. 크롬 주소창에 `chrome://extensions` 입력
2. 오른쪽 상단 **"개발자 모드"** 토글을 켭니다
3. **"압축해제된 확장 프로그램을 로드합니다"** 버튼 클릭
4. 만든 폴더(`my-first-extension`)를 선택

> "아이콘이 브라우저 오른쪽 위에 나타났나요? 퍼즐 모양 아이콘을 클릭하면 내 익스텐션이 목록에 있습니다. 핀 아이콘을 누르면 항상 보이게 고정됩니다."

**오류가 나면?**
- 빨간 "오류" 버튼이 나타납니다
- 클릭하면 에러 메시지가 보입니다
- 대부분 manifest.json의 오타이거나 파일 경로 문제입니다
- Claude에게 에러 메시지를 보여주면 바로 해결됩니다

### Step 6: 테스트 및 수정 반복 (5분)

1. 익스텐션 아이콘을 클릭합니다
2. 팝업이 열리는지 확인합니다
3. 메모를 입력하고 "저장" 버튼을 클릭합니다
4. 팝업을 닫았다가 다시 엽니다 — **메모가 유지되는지** 확인합니다

수정 후 반영하기:
1. 코드를 수정합니다
2. `chrome://extensions`에서 익스텐션의 **새로고침 아이콘(원형 화살표)**을 클릭합니다
3. 팝업을 다시 열어 확인합니다

> "코드를 수정할 때마다 '새로고침 아이콘'을 클릭해야 합니다. 웹페이지의 F5와 같은 역할입니다."

### Step 7: Content Script 추가 — 웹페이지에 기능 넣기 (7분)

Popup만으로도 훌륭하지만, Content Script를 추가하면 **다른 웹사이트에서도** 기능이 동작합니다.

예: 텍스트를 선택하면 글자 수를 보여주는 기능

```javascript
// content.js
document.addEventListener("mouseup", () => {
  const selectedText = window.getSelection().toString().trim();

  // 기존 배지 제거
  const existingBadge = document.getElementById("char-count-badge");
  if (existingBadge) existingBadge.remove();

  if (selectedText.length > 0) {
    const badge = document.createElement("div");
    badge.id = "char-count-badge";
    badge.textContent = `${selectedText.length}자`;
    badge.style.cssText = `
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: #4F46E5;
      color: white;
      padding: 8px 16px;
      border-radius: 20px;
      font-size: 14px;
      z-index: 999999;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
    `;
    document.body.appendChild(badge);

    // 3초 후 자동 사라짐
    setTimeout(() => badge.remove(), 3000);
  }
});
```

manifest.json에 Content Script를 등록합니다:

```json
{
  "manifest_version": 3,
  "name": "나의 메모장 + 글자수",
  "version": "1.1",
  "description": "메모 저장 + 선택 텍스트 글자 수 표시",
  "action": {
    "default_popup": "popup.html"
  },
  "permissions": ["storage"],
  "content_scripts": [
    {
      "matches": ["<all_urls>"],
      "js": ["content.js"]
    }
  ]
}
```

> "content_scripts의 matches에 `<all_urls>`를 넣으면 모든 웹사이트에서 동작합니다. 아무 웹사이트에서 텍스트를 드래그해보세요. 오른쪽 아래에 글자 수가 뜹니다."

### Step 8: 기능 확장 — 하나 더 추가 (5분)

기본 기능이 동작하면, Claude와 함께 하나를 더 추가합니다:

아이디어:
- **단축키 추가**: 키보드 단축키로 메모 저장 (Ctrl+Shift+S)
- **다크 모드**: 시스템 테마에 맞춰 팝업 색상 변경
- **메모 목록**: 여러 메모를 저장하고 선택
- **내 서비스 연결**: 팝업에서 내 Rails 서비스의 API 호출

```javascript
// 예: 저장된 메모에 날짜/시간 추가
saveBtn.addEventListener("click", () => {
  const now = new Date().toLocaleString("ko-KR");
  const entry = {
    text: memo.value,
    savedAt: now
  };
  chrome.storage.local.set({ memo: entry }, () => {
    status.textContent = `${now}에 저장됨`;
  });
});
```

### Step 9: 크롬 웹스토어 등록 과정 소개 (2분)

만든 익스텐션을 세상에 공개하고 싶다면:

**등록 절차:**
1. **개발자 계정 등록** — [Chrome Web Store Developer Dashboard](https://chrome.google.com/webstore/devconsole)
2. **등록비 결제** — 일회성 $5 (약 6,500원)
3. **익스텐션 패키징** — 폴더를 ZIP 파일로 압축
4. **스토어 정보 작성** — 설명, 스크린샷, 카테고리
5. **제출 및 심사** — 구글이 검토 (보통 1~3일)
6. **승인 후 공개** — 누구나 검색해서 설치 가능

> "당장 등록하지 않아도 됩니다. 하지만 '등록할 수 있다'는 것을 아는 것이 중요합니다. 내가 만든 도구를 다른 사람들도 쓸 수 있다는 뜻이니까요."

**등록 시 필요한 것:**
- ZIP 파일 (익스텐션 폴더 압축)
- 아이콘 이미지 (128x128px)
- 스크린샷 (1280x800px 권장, 최소 1장)
- 짧은 설명 (132자 이내)
- 상세 설명

git commit (선택):

```bash
cd ~/chrome-extensions/my-first-extension
git init && git add -A && git commit -m "나의 첫 크롬 익스텐션: 메모장 + 글자수 세기"
```

---

## QUIZ

### Q1: manifest.json의 역할
> "manifest.json이 없으면 어떻게 될까요?"

1. 익스텐션이 느리게 동작한다
2. 크롬이 이 폴더를 익스텐션으로 인식하지 못한다
3. 팝업 디자인이 깨진다
4. 아무 영향 없다

정답: 2번
해설: manifest.json은 익스텐션의 신분증이자 설계도입니다. "이 폴더가 크롬 익스텐션입니다"라고 크롬에게 알려주는 파일입니다. 이것 없이는 크롬이 폴더를 익스텐션으로 인식할 수 없습니다.

### Q2: 개발자 모드
> "크롬에서 '개발자 모드'를 켜야 하는 이유는?"

1. 코드를 더 빠르게 실행하기 위해
2. 스토어에 등록하지 않은 로컬 익스텐션을 로드하기 위해
3. JavaScript를 사용하기 위해
4. 인터넷 연결 없이 사용하기 위해

정답: 2번
해설: 보통 크롬 익스텐션은 웹 스토어에서 설치합니다. 개발 중인 익스텐션은 스토어에 없으므로, 개발자 모드를 켜서 로컬 폴더에서 직접 로드해야 합니다.

### Q3: Popup과 Content Script의 차이
> "Popup과 Content Script의 가장 큰 차이는?"

1. Popup이 더 어렵다
2. Popup은 아이콘 클릭 시 창을 띄우고, Content Script는 웹페이지 자체를 수정한다
3. Content Script가 더 예쁘다
4. 둘 다 같은 방식으로 동작한다

정답: 2번
해설: Popup은 익스텐션 아이콘을 클릭하면 나타나는 독립된 작은 창입니다. Content Script는 사용자가 방문하는 웹페이지에 코드를 주입해서 페이지 내용을 변경합니다. 용도가 다릅니다.

### Q4: chrome.storage의 특징
> "chrome.storage에 저장한 데이터는 언제 사라지나요?"

1. 팝업을 닫으면 사라진다
2. 브라우저를 재시작하면 사라진다
3. 익스텐션을 삭제하거나 직접 지울 때까지 유지된다
4. 1시간 후 자동으로 사라진다

정답: 3번
해설: chrome.storage는 브라우저에 영구적으로 저장됩니다. 팝업을 닫아도, 브라우저를 재시작해도 데이터가 남아있습니다. 익스텐션을 삭제하거나 코드에서 `chrome.storage.local.remove()`를 호출해야 사라집니다.

### Q5: manifest_version: 3
> "manifest_version을 3으로 설정하는 이유는?"

1. 3이 가장 빠르기 때문에
2. 구글이 보안과 성능을 위해 최신 규격으로 지정한 것이기 때문에
3. 2는 모바일용이고 3이 데스크톱용이기 때문에
4. 특별한 이유 없이 관례적으로 쓰는 것이다

정답: 2번
해설: Manifest V3는 구글이 보안과 성능 향상을 위해 도입한 최신 규격입니다. V2는 2024년부터 단계적으로 지원이 중단되고 있으므로, 새로 만드는 익스텐션은 반드시 V3를 사용해야 합니다.
