## EXPLAIN

### Active Storage = Rails의 파일 관리 시스템

파일 저장, 크기 조절, 모델 연결을 Rails 내장 기능으로 해결합니다.

```ruby
class User < ApplicationRecord
  has_one_attached :avatar       # 사진 1장
  has_many_attached :documents   # 파일 여러 개
end
```

### 이미지 변환 (Variant)

원본은 유지하면서 자동으로 크기를 줄여줍니다:

```erb
<%%= image_tag @user.avatar.variant(resize_to_limit: [100, 100]) %>
```

한 번 생성하면 캐시되어 재사용됩니다.

### 저장 위치

| 환경 | 저장소 | 비고 |
|------|--------|------|
| 개발 | 로컬 디스크 | 기본값, 설정 불필요 |
| 프로덕션 | 클라우드 (S3 등) | 나중에 변경 가능 |

---

## EXECUTE

### Step 1: 업로드 대상 선정 (2분)

> "서비스에서 이미지나 파일을 첨부하면 좋을 곳이 어디인가요?"

1장: `has_one_attached` / 여러 장: `has_many_attached`

### Step 2: Active Storage 설치 (3분)

```bash
bin/rails active_storage:install
bin/rails db:migrate
```

### Step 3: 모델에 첨부 기능 추가 (3분)

```ruby
class Post < ApplicationRecord
  has_one_attached :image
end
```

> "별도 마이그레이션이 필요 없습니다. Active Storage가 별도 테이블에서 관리해요."

### Step 4: 폼에 파일 업로드 필드 추가 (5분)

```erb
<%%= f.file_field :image, accept: "image/*" %>
<%% if @post.image.attached? %>
  <%%= image_tag @post.image, style: "max-width: 200px" %>
<%% end %>
```

컨트롤러 strong parameters에 `:image` 추가.

### Step 5: 이미지 표시 (5분)

```erb
<%# show - 큰 이미지 %>
<%% if @post.image.attached? %>
  <%%= image_tag @post.image, style: "max-width: 600px" %>
<%% end %>

<%# index - 썸네일 %>
<%%= image_tag post.image.variant(resize_to_limit: [150, 150]) %>
```

### Step 6: 이미지 변환 설정 (5분)

libvips 설치 확인: `vips --version` (없으면 `sudo apt install libvips`)

다양한 variant:
```ruby
post.image.variant(resize_to_limit: [100, 100])   # 썸네일
post.image.variant(resize_to_fill: [200, 200])     # 정사각형 크롭
```

### Step 7: 검증 추가 (2분)

```ruby
validate :acceptable_image
private
def acceptable_image
  return unless image.attached?
  errors.add(:image, "10MB 이하만 가능") unless image.blob.byte_size <= 10.megabyte
end
```

git commit으로 마무리.

---

## QUIZ

### Q1: Active Storage의 장점
> "Active Storage 사용 시 모델 테이블에 컬럼을 추가해야 하나요?"

1. 네, image_url 컬럼이 필요합니다
2. 아니오, Active Storage가 별도 테이블에서 관리합니다
3. 네, file_path와 file_size 컬럼이 필요합니다
4. 모델마다 다릅니다

정답: 2번
해설: Active Storage는 별도 테이블(active_storage_blobs, active_storage_attachments)에서 관리합니다.

### Q2: variant의 역할
> "image.variant(resize_to_limit: [100, 100])이 하는 일은?"

1. 원본 이미지를 100x100으로 영구 변경한다
2. 원본은 유지하고 100x100 크기의 사본을 생성한다
3. 이미지를 삭제하고 새로 만든다
4. 이미지 파일명을 바꾼다

정답: 2번
해설: variant는 원본을 그대로 두고 지정한 크기의 사본을 생성합니다. 캐시되어 다음에는 빠르게 불러옵니다.
