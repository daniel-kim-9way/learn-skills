## EXPLAIN

### "실시간"이 뭔가요?

일반 웹: 버튼 클릭 → 페이지 전체 새로고침 → 변경 내용 표시
실시간 웹: 버튼 클릭 → **바뀌어야 할 부분만** 즉시 변경. 카카오톡처럼.

### Turbo Frames = 액자 교체

벽 전체를 허물지 않고 **액자 안의 그림만 교체**하는 것.

```erb
<%%= turbo_frame_tag "post_1" do %>
  <h2>게시글 제목</h2>
  <%%= link_to "수정", edit_post_path(@post) %>
<%% end %>
```

"수정" 클릭 시 `turbo_frame_tag "post_1"` 영역만 수정 폼으로 바뀝니다.

### Turbo Streams = 실시간 방송

Turbo Frames는 클릭해야 바뀌고, **Turbo Streams**는 서버에서 알아서 밀어줍니다.

```ruby
class Comment < ApplicationRecord
  broadcasts_to :post
end
```

이 한 줄이면, 댓글 추가 시 모든 사용자에게 실시간 반영됩니다.

| 상황 | 도구 | 예시 |
|------|------|------|
| 클릭하면 일부만 바뀌기 | Turbo Frame | 인라인 편집, 탭 전환 |
| 자동으로 실시간 반영 | Turbo Stream | 댓글, 알림, 채팅 |

---

## EXECUTE

### Step 1: 실시간 기능 선정 (3분)

> "서비스에서 '새로고침 없이 바로 바뀌면 좋겠다'고 생각한 부분이 있나요?"

권장: 목록에 새 항목 추가, 인라인 편집, 삭제 시 즉시 사라짐

### Step 2: Turbo Frame -- 인라인 편집 (10분)

show 뷰에서 편집할 영역을 `turbo_frame_tag`로 감싸고, edit 뷰의 폼도 같은 ID로 감싼다. 브라우저에서 "수정" 클릭 시 새로고침 없이 폼이 나타나는지 확인.

> "turbo_frame_tag의 ID가 같으면, Rails가 자동으로 그 영역만 교체합니다."

### Step 3: Turbo Stream -- 실시간 목록 업데이트 (15분)

1. 모델에 `broadcasts_to` 추가
2. show 뷰에 `turbo_stream_from @post` 추가
3. comments partial을 `dom_id(comment)`로 감싸기
4. 컨트롤러에서 `respond_to { |format| format.turbo_stream }` 추가
5. 브라우저 두 개 열어 테스트: 탭 A에서 댓글 작성 → 탭 B에서 실시간 반영 확인

### Step 4: 학생 서비스에 적용 (7분)

Step 2-3 패턴을 학생 서비스에 적용. 가장 효과적인 곳 선택:
- 기존 CRUD에 인라인 편집 추가
- 목록에 실시간 추가/삭제 반영

### Step 5: git commit (2분)

> "이제 서비스에 실시간 기능이 추가되었습니다."

---

## QUIZ

### Q1: Turbo Frame의 핵심 원리
> "Turbo Frame이 하는 일을 한 마디로 설명하면?"

1. 페이지 전체를 더 빠르게 로딩한다
2. 페이지의 특정 영역만 교체한다
3. JavaScript를 자동으로 작성해준다
4. 데이터베이스 쿼리를 최적화한다

정답: 2번
해설: Turbo Frame은 같은 ID를 가진 영역끼리 교체합니다. 전체 페이지가 아닌 해당 부분만 바뀝니다.

### Q2: Turbo Frame vs Turbo Stream
> "Turbo Stream이 Turbo Frame과 다른 점은?"

1. Turbo Stream이 더 예쁘다
2. Turbo Stream은 서버에서 자동으로 변경사항을 밀어준다
3. Turbo Frame이 더 빠르다
4. 둘은 같은 기능이다

정답: 2번
해설: Turbo Frame은 클릭해야 바뀌고, Turbo Stream은 서버에서 변경 시 자동으로 모든 사용자에게 실시간 반영합니다.
