## EXPLAIN

### "실시간"이 왜 중요한가요?

카카오톡에서 메시지를 보내면 어떻게 되나요? 상대방 화면에 **바로** 뜹니다. 새로고침 버튼 같은 건 없습니다.

이것이 사용자가 기대하는 "현대적인" 웹입니다.

일반 웹과 실시간 웹의 차이:

| | 일반 웹 | 실시간 웹 |
|---|---------|----------|
| 새 댓글 확인 | F5 눌러서 새로고침 | 자동으로 나타남 |
| 게시글 수정 | 수정 페이지로 이동 | 그 자리에서 바로 수정 |
| 알림 확인 | 페이지 이동해서 확인 | 화면 위에 바로 표시 |
| 느낌 | 2000년대 홈페이지 | 카카오톡/인스타그램 |

Rails 8에는 이것을 쉽게 만드는 도구가 **이미 포함**되어 있습니다. 별도 설치가 필요 없습니다.

### Hotwire = TV 리모컨

Hotwire를 이해하는 가장 좋은 비유는 **TV 리모컨**입니다.

리모컨 없던 시절: TV 앞까지 걸어가서 → 채널 돌리고 → 다시 소파로 돌아옴
리모컨이 생긴 후: 소파에 앉아서 → 버튼 하나로 채널 변경

**페이지 새로고침** = TV 앞까지 걸어가는 것
**Hotwire** = 리모컨 버튼 하나로 바꾸는 것

Hotwire는 두 가지 도구로 이루어져 있습니다:

### Turbo Frame = "액자 교체"

벽에 그림 액자가 5개 걸려있다고 상상해보세요. 한 그림만 바꾸고 싶으면 어떻게 하나요? 벽 전체를 허물 필요 없이, **그 액자만 빼고 새 그림을 넣으면** 됩니다.

Turbo Frame이 정확히 이것입니다. 페이지 전체를 다시 불러오지 않고, **특정 영역만 교체**합니다.

```erb
<%# 이 영역이 하나의 "액자"입니다 %>
<%= turbo_frame_tag "post_1" do %>
  <h2>게시글 제목</h2>
  <p>게시글 내용입니다...</p>
  <%= link_to "수정", edit_post_path(@post) %>
<% end %>
```

"수정" 링크를 클릭하면? 페이지 전체가 바뀌는 대신, `post_1`이라는 **액자 안의 내용만** 수정 폼으로 바뀝니다. 나머지 페이지는 그대로입니다.

비밀은 **같은 ID**입니다. 현재 페이지의 `turbo_frame_tag "post_1"`과 수정 페이지의 `turbo_frame_tag "post_1"`이 같은 ID를 가지면, Rails가 자동으로 그 영역만 교체합니다.

적합한 곳:
- **인라인 편집**: 게시글 클릭하면 그 자리에서 수정
- **탭 전환**: 탭을 클릭하면 내용 영역만 바뀜
- **더보기**: "더보기" 버튼 누르면 그 자리에 추가 내용 표시

### Turbo Stream = "실시간 방송"

Turbo Frame은 사용자가 **클릭해야** 바뀝니다. 하지만 카카오톡 메시지는 클릭 안 해도 알아서 옵니다.

Turbo Stream이 이 역할을 합니다. 서버에서 변경이 생기면 **알아서 모든 사용자에게 전달**합니다.

비유하면:
- **Turbo Frame** = 리모컨 (내가 버튼을 눌러야 바뀜)
- **Turbo Stream** = TV 방송 (방송국에서 보내면 모든 TV에 나옴)

놀라운 것은 코드가 매우 짧다는 것입니다:

```ruby
# app/models/comment.rb
class Comment < ApplicationRecord
  belongs_to :post
  broadcasts_to :post  # 이 한 줄이 전부!
end
```

`broadcasts_to :post` 한 줄이면, 댓글이 추가/수정/삭제될 때 **해당 게시글을 보고 있는 모든 사용자**에게 실시간으로 반영됩니다.

뷰에서는 "채널 수신" 설정만 합니다:

```erb
<%# 이 게시글의 실시간 업데이트를 수신합니다 %>
<%= turbo_stream_from @post %>

<div id="comments">
  <%= render @post.comments %>
</div>
```

이제 탭 A에서 댓글을 작성하면, 탭 B에서 새로고침 없이 댓글이 나타납니다.

### 정리: 언제 뭘 쓰나요?

| 상황 | 도구 | 작동 방식 | 예시 |
|------|------|----------|------|
| 클릭하면 일부만 바뀌기 | **Turbo Frame** | 사용자 클릭 → 해당 영역 교체 | 인라인 편집, 탭 전환 |
| 자동으로 실시간 반영 | **Turbo Stream** | 서버 변경 → 모든 사용자에게 전송 | 댓글, 알림, 채팅 |
| 둘 다 쓰기 | Frame + Stream | 입력은 Frame, 결과는 Stream | 댓글 입력 폼 + 실시간 목록 |

대부분의 경우 **Turbo Frame부터 시작**합니다. 클릭 시 부분 교체만으로도 사용자 경험이 크게 좋아집니다. 그 다음 필요한 곳에 Turbo Stream을 추가합니다.

---

## EXECUTE

### Step 1: 실시간 기능 선정 (3분)

> "서비스에서 '새로고침 없이 바로 바뀌면 좋겠다'고 생각한 부분이 있나요?"

실시간화하면 효과가 큰 곳:
- 목록에 새 항목 추가하면 바로 나타남
- 수정 버튼 누르면 그 자리에서 바로 수정
- 삭제하면 즉시 사라짐
- 다른 사람의 변경이 실시간으로 반영

권장: 기존 기능 중 **가장 자주 사용하는 CRUD 하나**를 선택합니다.

### Step 2: Turbo Frame으로 인라인 편집 만들기 (10분)

기존 show 페이지에서 "수정" 클릭 시 그 자리에서 바로 편집할 수 있게 만듭니다.

**2-1. show 뷰에 Turbo Frame 추가**

```erb
<%# app/views/posts/show.html.erb %>
<%= turbo_frame_tag dom_id(@post) do %>
  <div class="bg-white rounded-lg shadow p-6">
    <h1 class="text-2xl font-bold"><%= @post.title %></h1>
    <p class="mt-4 text-gray-700"><%= @post.body %></p>

    <div class="mt-4">
      <%= link_to "수정", edit_post_path(@post), class: "text-blue-600 hover:underline" %>
    </div>
  </div>
<% end %>
```

**2-2. edit 뷰도 같은 Frame ID로 감싸기**

```erb
<%# app/views/posts/edit.html.erb %>
<%= turbo_frame_tag dom_id(@post) do %>
  <div class="bg-white rounded-lg shadow p-6">
    <%= form_with(model: @post, class: "space-y-4") do |f| %>
      <div>
        <%= f.label :title, "제목", class: "block font-semibold" %>
        <%= f.text_field :title, class: "w-full border rounded px-3 py-2" %>
      </div>
      <div>
        <%= f.label :body, "내용", class: "block font-semibold" %>
        <%= f.text_area :body, rows: 5, class: "w-full border rounded px-3 py-2" %>
      </div>
      <div class="flex gap-2">
        <%= f.submit "저장", class: "bg-blue-600 text-white px-4 py-2 rounded" %>
        <%= link_to "취소", post_path(@post), class: "px-4 py-2 text-gray-600" %>
      </div>
    <% end %>
  </div>
<% end %>
```

> "핵심은 두 뷰의 turbo_frame_tag ID가 같다는 것입니다. `dom_id(@post)`는 `post_1`처럼 자동으로 고유 ID를 만들어줍니다. ID가 같으면 Rails가 그 영역만 교체합니다."

브라우저에서 확인: "수정" 클릭 → 페이지 새로고침 없이 폼이 나타남 → 저장하면 다시 원래 내용으로.

### Step 3: Turbo Stream으로 실시간 목록 업데이트 (15분)

이제 진짜 실시간입니다. 한 사용자가 변경하면 다른 사용자에게도 바로 반영됩니다.

**3-1. 모델에 broadcasts 추가**

```ruby
# app/models/comment.rb (또는 학생 서비스의 모델)
class Comment < ApplicationRecord
  belongs_to :post
  belongs_to :user

  broadcasts_to :post
end
```

> "broadcasts_to :post 한 줄이 마법의 주문입니다. 댓글이 생성/수정/삭제될 때마다, 해당 게시글 페이지를 보고 있는 모든 사용자에게 자동으로 변경사항을 전달합니다."

**3-2. 뷰에서 실시간 수신 설정**

```erb
<%# app/views/posts/show.html.erb %>
<%= turbo_stream_from @post %>

<h1><%= @post.title %></h1>

<div id="comments">
  <%= render @post.comments %>
</div>

<%= form_with(model: [@post, Comment.new], class: "mt-6") do |f| %>
  <div class="flex gap-2">
    <%= f.text_field :body, placeholder: "댓글을 입력하세요...",
        class: "flex-1 border rounded px-3 py-2" %>
    <%= f.submit "작성", class: "bg-blue-600 text-white px-4 py-2 rounded" %>
  </div>
<% end %>
```

**3-3. 댓글 partial 작성**

```erb
<%# app/views/comments/_comment.html.erb %>
<div id="<%= dom_id(comment) %>" class="py-3 border-b">
  <div class="flex justify-between items-center">
    <span class="font-semibold"><%= comment.user.name %></span>
    <span class="text-sm text-gray-500"><%= time_ago_in_words(comment.created_at) %> 전</span>
  </div>
  <p class="mt-1 text-gray-700"><%= comment.body %></p>
</div>
```

> "partial의 최상위 div에 `dom_id(comment)`를 넣는 것이 중요합니다. Turbo Stream이 이 ID를 기준으로 어디에 추가/수정/삭제할지 판단합니다."

**3-4. 컨트롤러 설정**

```ruby
# app/controllers/comments_controller.rb
class CommentsController < ApplicationController
  def create
    @post = Post.find(params[:post_id])
    @comment = @post.comments.build(comment_params)
    @comment.user = current_user

    if @comment.save
      # broadcasts_to가 자동으로 Turbo Stream을 보내므로
      # 별도 응답이 필요 없습니다
      respond_to do |format|
        format.turbo_stream  # 빈 응답 OK — broadcasts가 처리
        format.html { redirect_to @post }
      end
    else
      redirect_to @post, alert: "댓글 작성에 실패했습니다."
    end
  end

  private

  def comment_params
    params.require(:comment).permit(:body)
  end
end
```

**3-5. 실시간 테스트 — 와우 모먼트!**

1. 브라우저 창 두 개를 나란히 엽니다 (같은 게시글 페이지)
2. 왼쪽 창에서 댓글을 작성합니다
3. **오른쪽 창에서 새로고침 없이 댓글이 나타나는지 확인합니다**

> "새로고침 없이 댓글이 나타나는 순간, 실시간 웹의 위력을 체감하게 됩니다. 카카오톡과 같은 원리입니다. 이것이 단 한 줄(broadcasts_to)로 구현되었다는 것이 Rails 8의 힘입니다."

### Step 4: 학생 서비스에 적용 (7분)

Step 2-3에서 배운 패턴을 학생 서비스의 기존 기능에 적용합니다.

가장 효과적인 곳을 선택하세요:

**옵션 A: 인라인 편집 (Turbo Frame)**
- 기존 CRUD의 수정 기능을 인라인으로 변경
- 목록에서 항목 클릭 → 그 자리에서 수정 → 저장

**옵션 B: 실시간 목록 (Turbo Stream)**
- 새 항목 추가 시 목록에 자동 반영
- 삭제 시 즉시 사라짐
- 여러 사용자가 동시에 보고 있어도 동기화

**옵션 C: 실시간 알림 (Turbo Stream)**
- 새 이벤트 발생 시 화면 상단에 알림 표시
- 읽지 않은 알림 수 자동 업데이트

> "Claude에게 '내 서비스의 [기능]을 Turbo Frame/Stream으로 실시간화해줘'라고 요청하세요. 구체적으로 어떤 화면의 어떤 부분을 바꾸고 싶은지 설명하면 됩니다."

### Step 5: 삭제도 실시간으로 (3분)

항목을 삭제했을 때 즉시 사라지게 만듭니다:

```ruby
# 컨트롤러 destroy 액션
def destroy
  @comment = @post.comments.find(params[:id])
  @comment.destroy

  respond_to do |format|
    format.turbo_stream { render turbo_stream: turbo_stream.remove(@comment) }
    format.html { redirect_to @post }
  end
end
```

삭제 버튼:

```erb
<%= button_to "삭제", [@post, comment], method: :delete,
    class: "text-red-500 text-sm",
    data: { turbo_confirm: "정말 삭제하시겠습니까?" } %>
```

> "`turbo_confirm`을 추가하면 삭제 전 확인 팝업이 뜹니다. 실수로 삭제하는 것을 방지합니다."

### Step 6: git commit (2분)

```bash
git add -A && git commit -m "실시간 기능 추가: Turbo Frame 인라인 편집 + Turbo Stream 실시간 업데이트"
```

> "축하합니다! 이제 서비스가 새로고침 없이 동작합니다. 사용자 경험이 완전히 달라졌습니다."

---

## QUIZ

### Q1: Turbo Frame의 핵심 원리
> "Turbo Frame이 하는 일을 한 마디로 설명하면?"

1. 페이지 전체를 더 빠르게 로딩한다
2. 페이지의 특정 영역만 교체한다
3. JavaScript를 자동으로 작성해준다
4. 데이터베이스 쿼리를 최적화한다

정답: 2번
해설: Turbo Frame은 같은 ID를 가진 영역끼리 교체합니다. 벽에 걸린 액자 중 하나만 바꾸는 것처럼, 페이지 전체가 아닌 해당 부분만 바뀝니다.

### Q2: Turbo Frame vs Turbo Stream
> "Turbo Stream이 Turbo Frame과 다른 점은?"

1. Turbo Stream이 더 예쁘다
2. Turbo Stream은 서버에서 자동으로 변경사항을 밀어준다
3. Turbo Frame이 더 빠르다
4. 둘은 같은 기능이다

정답: 2번
해설: Turbo Frame은 사용자가 클릭해야 바뀝니다 (리모컨). Turbo Stream은 서버에서 변경이 생기면 자동으로 모든 사용자에게 전달합니다 (TV 방송). 카카오톡 메시지가 클릭 안 해도 오는 것과 같습니다.

### Q3: broadcasts_to의 역할
> "모델에 `broadcasts_to :post`를 추가하면 무엇이 일어나나요?"

1. 게시글이 자동으로 저장된다
2. 댓글이 변경될 때마다 해당 게시글을 보는 사용자에게 실시간 반영된다
3. 게시글의 조회수가 올라간다
4. 이메일 알림이 전송된다

정답: 2번
해설: broadcasts_to는 "이 모델이 변경되면, 관련된 게시글 페이지를 보고 있는 모든 사용자에게 변경사항을 실시간으로 보내라"는 뜻입니다. 댓글이 추가/수정/삭제될 때 자동으로 동작합니다.

### Q4: dom_id의 중요성
> "partial에서 dom_id(comment)를 사용하는 이유는?"

1. CSS 스타일을 적용하기 위해
2. Turbo Stream이 어떤 요소를 추가/수정/삭제할지 식별하기 위해
3. JavaScript에서 사용하기 위해
4. 데이터베이스 ID를 표시하기 위해

정답: 2번
해설: dom_id는 `comment_1`, `comment_2` 같은 고유 ID를 만듭니다. Turbo Stream은 이 ID를 기준으로 "새 댓글을 어디에 추가할지", "어떤 댓글을 삭제할지"를 판단합니다. ID가 없으면 Turbo Stream이 무엇을 바꿔야 할지 모릅니다.
