## EXPLAIN

### 파일 업로드, 왜 필요한가요?

텍스트만 있는 서비스를 떠올려보세요. 프로필 사진이 없는 카카오톡, 상품 이미지가 없는 쇼핑몰, 사진이 없는 인스타그램. 뭔가 빠진 느낌이 들죠?

**이미지 하나**가 추가되면 서비스의 완성도가 확 올라갑니다:
- 프로필 사진 → 사용자 신뢰도 상승
- 상품/게시글 이미지 → 한눈에 파악 가능
- 첨부파일 → 실무 활용도 상승

### Active Storage = Rails의 "창고 관리인"

파일 업로드를 직접 구현하려면 생각보다 할 일이 많습니다:

1. 파일을 받아서 어디에 저장할지 결정
2. 파일명이 겹치지 않게 관리
3. 이미지 크기를 줄여 썸네일 만들기
4. 나중에 클라우드로 옮기기
5. 삭제 시 파일도 같이 정리

**Active Storage**가 이 모든 것을 대신 해줍니다. Rails에 내장되어 있어 별도 gem 설치도 필요 없습니다.

비유하면 이렇습니다:
- **여러분** = 물건을 맡기는 손님 ("이 사진 보관해주세요")
- **Active Storage** = 창고 관리인 ("네, 여기 번호표요. 나중에 이 번호로 찾으세요")

여러분은 "보관해줘", "꺼내줘"만 하면 됩니다. 어디에 어떻게 저장되는지는 **창고 관리인이 알아서** 합니다.

### 모델에 연결하기 — 단 한 줄

```ruby
class User < ApplicationRecord
  has_one_attached :avatar       # 프로필 사진 1장
end

class Post < ApplicationRecord
  has_one_attached :cover_image  # 대표 이미지 1장
  has_many_attached :photos      # 사진 여러 장
end
```

`has_one_attached`는 "이 모델에 파일 1개를 붙인다", `has_many_attached`는 "파일 여러 개를 붙인다"는 뜻입니다.

놀라운 점: **모델 테이블에 컬럼을 추가할 필요가 없습니다.** Active Storage가 별도 테이블(`active_storage_blobs`, `active_storage_attachments`)에서 관리합니다. 기존 테이블을 건드리지 않으니 안전합니다.

### 이미지 변환 (Variant) = 자동 크기 조절

원본 사진이 5MB짜리 고화질 이미지라면? 목록 페이지에서 50개를 한꺼번에 불러오면 페이지가 느려집니다.

**Variant**가 이 문제를 해결합니다:

```erb
<%# 원본 그대로 표시 (상세 페이지) %>
<%= image_tag @post.cover_image %>

<%# 썸네일로 줄여서 표시 (목록 페이지) %>
<%= image_tag @post.cover_image.variant(resize_to_limit: [150, 150]) %>

<%# 정사각형으로 잘라서 표시 (프로필) %>
<%= image_tag @user.avatar.variant(resize_to_fill: [100, 100]) %>
```

- `resize_to_limit` = 비율 유지하면서 최대 크기 제한 (사진 찌그러지지 않음)
- `resize_to_fill` = 지정 크기에 맞게 자르기 (프로필 사진처럼 정사각형)

원본은 그대로 보관하고, **크기가 줄어든 복사본**을 따로 만듭니다. 한 번 만들면 캐시되어 다음에는 빠르게 불러옵니다.

### 저장 위치 — 지금은 로컬, 나중에 클라우드

| 환경 | 저장 위치 | 설정 | 비고 |
|------|----------|------|------|
| 개발(local) | 내 컴퓨터 디스크 | 기본값, 설정 불필요 | `storage/` 폴더에 저장됨 |
| 프로덕션 | 클라우드 (S3, GCS 등) | 나중에 설정 | 배포 시 변경 |

코드는 **하나도 안 바꿔도 됩니다.** 설정 파일(`config/storage.yml`)만 변경하면 저장 위치가 바뀝니다. Active Storage(창고 관리인)가 어디에 저장할지 알아서 판단합니다.

### 파일 검증 — 아무 파일이나 받으면 안 됩니다

사용자가 1GB 동영상을 업로드하면? 서버가 터집니다. 실행 파일(.exe)을 올리면? 보안 위험입니다.

**반드시 제한을 걸어야 합니다:**

```ruby
class Post < ApplicationRecord
  has_one_attached :cover_image

  validate :acceptable_image

  private

  def acceptable_image
    return unless cover_image.attached?

    # 크기 제한: 10MB 이하
    unless cover_image.blob.byte_size <= 10.megabytes
      errors.add(:cover_image, "10MB 이하의 파일만 업로드할 수 있습니다")
    end

    # 형식 제한: 이미지만 허용
    acceptable_types = ["image/jpeg", "image/png", "image/webp", "image/gif"]
    unless acceptable_types.include?(cover_image.content_type)
      errors.add(:cover_image, "JPEG, PNG, WebP, GIF 형식만 가능합니다")
    end
  end
end
```

이 검증이 없으면 서비스가 위험해집니다. **항상 크기와 형식을 제한하세요.**

---

## EXECUTE

### Step 1: 업로드 대상 선정 (2분)

> "서비스에서 이미지나 파일을 첨부하면 좋을 곳이 어디인가요?"

예시:
- 사용자 프로필 사진 → `has_one_attached :avatar`
- 게시글 대표 이미지 → `has_one_attached :cover_image`
- 상품 사진 여러 장 → `has_many_attached :photos`
- 리뷰에 첨부 사진 → `has_many_attached :images`

가장 효과가 큰 곳 **1개**를 선택합니다. 프로필 사진이나 게시글 이미지를 권장합니다.

### Step 2: Active Storage 설치 (3분)

```bash
bin/rails active_storage:install
bin/rails db:migrate
```

> "이 명령어는 Active Storage가 사용하는 테이블 2개를 만듭니다. 여러분의 기존 테이블은 건드리지 않습니다."

이미지 크기 조절을 위해 **libvips**도 필요합니다:

```bash
# Ubuntu/WSL
sudo apt install libvips

# Mac
brew install vips
```

설치 확인:

```bash
vips --version
```

### Step 3: 모델에 첨부 기능 추가 (3분)

```ruby
# 예: 게시글에 이미지 추가
class Post < ApplicationRecord
  has_one_attached :cover_image
end
```

> "마이그레이션이 필요 없습니다! Active Storage가 별도 테이블에서 관리하니까요. 모델 파일에 한 줄만 추가하면 끝입니다."

### Step 4: 폼에 파일 업로드 필드 추가 (5분)

```erb
<%# app/views/posts/_form.html.erb %>
<%= form_with(model: post, class: "space-y-4") do |f| %>
  <%# 기존 필드들... %>

  <div>
    <%= f.label :cover_image, "대표 이미지", class: "block font-semibold mb-1" %>
    <%= f.file_field :cover_image, accept: "image/*",
        class: "block w-full text-sm text-gray-500
               file:mr-4 file:py-2 file:px-4 file:rounded
               file:border-0 file:bg-blue-50 file:text-blue-700
               hover:file:bg-blue-100" %>

    <%# 이미 이미지가 있으면 미리보기 표시 %>
    <% if post.cover_image.attached? %>
      <div class="mt-2">
        <p class="text-sm text-gray-500">현재 이미지:</p>
        <%= image_tag post.cover_image.variant(resize_to_limit: [200, 200]),
            class: "mt-1 rounded shadow-sm" %>
      </div>
    <% end %>
  </div>

  <%= f.submit "저장", class: "bg-blue-600 text-white px-6 py-2 rounded" %>
<% end %>
```

컨트롤러의 strong parameters에 `:cover_image`를 추가합니다:

```ruby
# app/controllers/posts_controller.rb
def post_params
  params.require(:post).permit(:title, :body, :cover_image)
end
```

> "`accept: 'image/*'`는 파일 선택 창에서 이미지 파일만 보여주는 힌트입니다. 하지만 이것만으로는 부족합니다 — 사용자가 개발자 도구로 우회할 수 있으니 모델에서도 검증해야 합니다."

### Step 5: 이미지 표시하기 (5분)

```erb
<%# app/views/posts/show.html.erb — 상세 페이지: 큰 이미지 %>
<% if @post.cover_image.attached? %>
  <div class="mb-6">
    <%= image_tag @post.cover_image.variant(resize_to_limit: [800, 600]),
        class: "rounded-lg shadow-md w-full object-cover" %>
  </div>
<% end %>

<h1 class="text-3xl font-bold"><%= @post.title %></h1>
<p class="mt-4 text-gray-700"><%= @post.body %></p>
```

```erb
<%# app/views/posts/_post.html.erb 또는 index — 목록 페이지: 썸네일 %>
<div class="flex gap-4 p-4 border-b">
  <% if post.cover_image.attached? %>
    <%= image_tag post.cover_image.variant(resize_to_fill: [120, 120]),
        class: "w-[120px] h-[120px] rounded object-cover flex-shrink-0" %>
  <% else %>
    <div class="w-[120px] h-[120px] rounded bg-gray-100 flex items-center justify-center flex-shrink-0">
      <span class="text-gray-400 text-sm">이미지 없음</span>
    </div>
  <% end %>

  <div>
    <h3 class="font-semibold"><%= post.title %></h3>
    <p class="text-sm text-gray-600 mt-1"><%= truncate(post.body, length: 80) %></p>
  </div>
</div>
```

> "`attached?`로 이미지 존재 여부를 확인하는 것이 중요합니다. 이미지가 없는 게시글에서 에러가 나지 않도록 합니다."

### Step 6: 파일 검증 추가 — 보안의 기본 (3분)

```ruby
# app/models/post.rb
class Post < ApplicationRecord
  has_one_attached :cover_image

  validate :acceptable_image

  private

  def acceptable_image
    return unless cover_image.attached?

    # 10MB 이하만 허용
    if cover_image.blob.byte_size > 10.megabytes
      errors.add(:cover_image, "10MB 이하의 파일만 업로드할 수 있습니다")
    end

    # 이미지 형식만 허용
    acceptable_types = ["image/jpeg", "image/png", "image/webp", "image/gif"]
    unless acceptable_types.include?(cover_image.content_type)
      errors.add(:cover_image, "JPEG, PNG, WebP, GIF 형식만 가능합니다")
    end
  end
end
```

> "이 검증은 반드시 넣으세요. 없으면 누군가 1GB 파일을 올려서 서버를 다운시킬 수 있습니다."

### Step 7: 여러 파일 업로드 (선택, 5분)

이미지를 여러 장 올릴 수 있게 하려면:

```ruby
# 모델
class Post < ApplicationRecord
  has_many_attached :photos
end
```

```erb
<%# 폼 — multiple: true 추가 %>
<%= f.file_field :photos, accept: "image/*", multiple: true,
    class: "block w-full text-sm" %>

<%# 표시 — 갤러리 형태 %>
<% if @post.photos.attached? %>
  <div class="grid grid-cols-3 gap-2 mt-4">
    <% @post.photos.each do |photo| %>
      <%= image_tag photo.variant(resize_to_fill: [200, 200]),
          class: "rounded object-cover w-full aspect-square" %>
    <% end %>
  </div>
<% end %>
```

컨트롤러 params에도 배열로 추가:

```ruby
def post_params
  params.require(:post).permit(:title, :body, :cover_image, photos: [])
end
```

### Step 8: 클라우드 스토리지 연결 (선택, 5분)

배포 시 클라우드 저장소를 사용해야 합니다. 로컬 디스크는 서버를 재배포하면 파일이 사라지기 때문입니다.

```yaml
# config/storage.yml
amazon:
  service: S3
  access_key_id: <%= Rails.application.credentials.dig(:aws, :access_key_id) %>
  secret_access_key: <%= Rails.application.credentials.dig(:aws, :secret_access_key) %>
  region: ap-northeast-2
  bucket: my-service-uploads
```

```ruby
# config/environments/production.rb
config.active_storage.service = :amazon
```

> "지금 당장은 하지 않아도 됩니다. 배포할 때 설정하면 됩니다. 중요한 것은 코드를 하나도 바꾸지 않고 설정만 바꾸면 된다는 점입니다."

git commit으로 마무리합니다.

```bash
git add -A && git commit -m "이미지 업로드 기능 추가: Active Storage + 썸네일 + 검증"
```

---

## QUIZ

### Q1: Active Storage의 장점
> "Active Storage 사용 시 모델 테이블에 컬럼을 추가해야 하나요?"

1. 네, image_url 컬럼이 필요합니다
2. 아니오, Active Storage가 별도 테이블에서 관리합니다
3. 네, file_path와 file_size 컬럼이 필요합니다
4. 모델마다 다릅니다

정답: 2번
해설: Active Storage는 `active_storage_blobs`와 `active_storage_attachments`라는 별도 테이블에서 파일 정보를 관리합니다. 기존 모델 테이블을 건드리지 않으므로 안전합니다.

### Q2: variant의 역할
> "image.variant(resize_to_limit: [100, 100])이 하는 일은?"

1. 원본 이미지를 100x100으로 영구 변경한다
2. 원본은 유지하고 100x100 크기의 사본을 생성한다
3. 이미지를 삭제하고 새로 만든다
4. 이미지 파일명을 바꾼다

정답: 2번
해설: variant는 원본을 절대 건드리지 않습니다. 지정한 크기의 복사본을 만들고 캐시합니다. 다음에 같은 크기를 요청하면 캐시된 이미지를 바로 보여줍니다.

### Q3: 파일 검증의 필요성
> "파일 업로드에 크기/형식 제한을 거는 이유는?"

1. 이미지를 더 예쁘게 만들기 위해
2. 서버를 보호하고 보안 위험을 방지하기 위해
3. 업로드 속도를 높이기 위해
4. 브라우저 호환성을 위해

정답: 2번
해설: 제한이 없으면 누군가 1GB 파일을 올려 서버 저장 공간을 가득 채우거나, 실행 파일을 올려 보안 위협이 될 수 있습니다. 크기와 형식 제한은 서비스 보호의 기본입니다.

### Q4: has_one_attached vs has_many_attached
> "프로필 사진에 적합한 것은?"

1. has_many_attached — 사진을 많이 올릴 수 있으니까
2. has_one_attached — 프로필 사진은 1장이니까
3. 둘 다 가능하고 차이 없다
4. 둘 다 아니고 별도 gem이 필요하다

정답: 2번
해설: 프로필 사진은 1장이므로 `has_one_attached`가 적합합니다. 새 사진을 올리면 자동으로 이전 사진을 대체합니다. 갤러리처럼 여러 장이 필요한 경우에만 `has_many_attached`를 씁니다.
