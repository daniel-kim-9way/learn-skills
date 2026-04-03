## EXPLAIN

### 이메일은 서비스의 "목소리"입니다

서비스가 사용자에게 직접 말을 거는 유일한 방법이 이메일입니다.

카카오톡 알림? 앱이 있어야 합니다. 푸시 알림? 허용해야 합니다. 하지만 이메일은 **가입할 때 이미 받았습니다.** 별도 설치도, 허락도 필요 없습니다.

잘 보낸 이메일 한 통이 사용자를 다시 불러옵니다:
- "환영합니다!" → 가입 직후 안심감
- "새 댓글이 달렸어요" → 다시 서비스로 돌아옴
- "이번 주 요약 리포트" → 서비스의 가치를 상기

반대로 잘못 보내면? **스팸함**으로 직행합니다. 핵심은 **사용자에게 가치가 있는 순간에만** 보내는 것입니다.

### Action Mailer = Rails의 "우체부"

우체국을 생각해보세요.

1. **편지를 쓴다** — 내용을 작성합니다
2. **봉투에 넣는다** — 받는 사람, 제목을 적습니다
3. **우체통에 넣는다** — 발송을 요청합니다
4. **우체부가 배달한다** — 실제로 전달합니다

Rails의 Action Mailer가 바로 이 **1~3번** 과정을 담당합니다:

```ruby
class UserMailer < ApplicationMailer
  # 1. 편지를 쓴다 (메서드 정의)
  def welcome_email(user)
    @user = user  # 편지에 쓸 내용 준비

    # 2. 봉투에 넣는다 (받는 사람, 제목)
    mail(
      to: @user.email,
      subject: "#{@user.name}님, 환영합니다!"
    )
  end
end
```

이메일의 실제 내용(HTML)은 별도 파일에 작성합니다:

```erb
<%# app/views/user_mailer/welcome_email.html.erb %>
<h1><%= @user.name %>님, 환영합니다!</h1>
<p>서비스에 가입해주셔서 감사합니다.</p>
<p>궁금한 점이 있으면 언제든 문의해주세요.</p>
```

호출은 단 한 줄입니다:

```ruby
UserMailer.welcome_email(user).deliver_later
```

편지를 쓰고(welcome_email), 우체통에 넣는다(deliver_later). 끝입니다.

### Resend = 실제 배달을 맡는 "택배 회사"

Action Mailer가 편지를 작성하면, **누군가**가 실제로 배달해야 합니다. 혼자서 우체국을 운영할 수는 없으니까요.

**Resend**는 현대적인 이메일 배달 서비스입니다:
- 무료 월 3,000통 (시작하기에 충분)
- API 키 하나로 5분 만에 연동
- 이메일이 잘 도착했는지 대시보드에서 확인 가능
- Gmail, 네이버 메일 등에 스팸으로 분류되지 않도록 처리

비유하면 이렇습니다:
- **Action Mailer** = 편지를 쓰고 봉투에 넣는 사람 (여러분)
- **Resend** = 편지를 실제로 배달하는 택배 회사

왜 직접 보내지 않고 Resend를 쓸까요? 직접 이메일 서버를 운영하면 스팸으로 분류되기 쉽고, 관리가 복잡합니다. Resend 같은 전문 서비스를 쓰면 **보내는 것에만 집중**할 수 있습니다.

### 3종 이메일: 서비스에 꼭 필요한 이메일들

대부분의 서비스에는 이 3가지 이메일이면 충분합니다:

| 종류 | 언제 보내나요? | 목적 |
|------|---------------|------|
| **가입 환영** | 회원가입 직후 | "잘 가입되었어요" 안심 + 첫인상 |
| **알림** | 중요한 이벤트 발생 시 | "새 댓글", "예약 확정" 등 |
| **주간 리포트** | 매주 월요일 아침 | "이번 주 활동 요약" → 재방문 유도 |

환영 이메일은 **자동 발송** (가입하면 바로), 알림은 **이벤트 기반** (뭔가 일어나면), 주간 리포트는 **예약 발송** (정해진 시간에). 각각 다른 방식으로 보내지만, Action Mailer로 전부 처리할 수 있습니다.

### deliver_now vs deliver_later — 큰 차이

```ruby
# 즉시 발송: 이메일 보내는 동안 사용자가 기다림
UserMailer.welcome_email(user).deliver_now

# 백그라운드 발송: 사용자는 바로 다음 페이지로
UserMailer.welcome_email(user).deliver_later
```

`deliver_now`는 우체국에 직접 가서 줄 서는 것입니다. 줄이 길면 한참 기다립니다.
`deliver_later`는 우체통에 넣는 것입니다. 넣고 바로 다른 일을 합니다.

**항상 `deliver_later`를 쓰세요.** Solid Queue가 백그라운드에서 알아서 보내줍니다. Rails 8에 내장되어 있으니 별도 설치도 필요 없습니다.

예약 발송도 가능합니다:

```ruby
# 1시간 후에 보내기
UserMailer.tips_email(user).deliver_later(wait: 1.hour)

# 내일 오전 9시에 보내기
UserMailer.weekly_report(user).deliver_later(
  wait_until: Date.tomorrow.beginning_of_day + 9.hours
)
```

### letter_opener = 개발 중 이메일 확인 도구

개발할 때 진짜 이메일을 보내면 안 됩니다. 실수로 테스트 메일이 고객에게 갈 수 있습니다.

**letter_opener** gem을 쓰면 이메일을 보내는 대신 **브라우저에서 열어줍니다.** 실제 이메일과 똑같이 생긴 화면이 브라우저에 뜹니다. 이메일이 어떻게 보이는지 바로 확인할 수 있습니다.

---

## EXECUTE

### Step 1: 이메일 시나리오 선정 (3분)

> "서비스에서 사용자에게 이메일을 보내면 좋을 상황 3가지를 떠올려보세요."

예시:
- 쇼핑몰: 주문 확인, 배송 시작, 리뷰 요청
- 예약 서비스: 예약 확인, 리마인더, 후기 요청
- 커뮤니티: 가입 환영, 새 댓글 알림, 주간 인기글

가장 단순한 **가입 환영 이메일**부터 시작합니다.

### Step 2: letter_opener 설치 — 이메일 미리보기 환경 (3분)

개발 중 이메일을 브라우저로 확인할 수 있게 설정합니다:

```ruby
# Gemfile의 development 그룹에 추가
group :development do
  gem "letter_opener"
end
```

```bash
bundle install
```

```ruby
# config/environments/development.rb 에 추가
config.action_mailer.delivery_method = :letter_opener
config.action_mailer.perform_deliveries = true
config.action_mailer.default_url_options = { host: "localhost", port: 3000 }
```

> "이제 개발 환경에서 이메일을 보내면, 진짜 발송되는 대신 브라우저 새 탭에서 열립니다. 안심하고 테스트하세요."

### Step 3: Action Mailer 생성 — 첫 번째 이메일 (5분)

```bash
bin/rails generate mailer User welcome notification weekly_report
```

생성되는 파일들:
- `app/mailers/user_mailer.rb` — 이메일 작성 로직
- `app/views/user_mailer/welcome.html.erb` — 환영 이메일 내용
- `app/views/user_mailer/notification.html.erb` — 알림 이메일 내용
- `app/views/user_mailer/weekly_report.html.erb` — 주간 리포트 내용

Mailer 파일을 서비스에 맞게 수정합니다:

```ruby
# app/mailers/user_mailer.rb
class UserMailer < ApplicationMailer
  default from: "noreply@myservice.com"

  def welcome(user)
    @user = user
    mail(to: @user.email, subject: "#{@user.name}님, 환영합니다!")
  end

  def notification(user, message)
    @user = user
    @message = message
    mail(to: @user.email, subject: "새로운 알림이 있습니다")
  end

  def weekly_report(user)
    @user = user
    @stats = calculate_weekly_stats(user)
    mail(to: @user.email, subject: "#{@user.name}님의 이번 주 활동 요약")
  end

  private

  def calculate_weekly_stats(user)
    # 학생 서비스에 맞는 통계 — Claude와 함께 작성
    {
      total_actions: 0,  # 예: 이번 주 작성한 글 수
      new_items: 0       # 예: 이번 주 새로 추가된 항목 수
    }
  end
end
```

### Step 4: 이메일 템플릿 작성 — 예쁜 편지지 (5분)

환영 이메일 템플릿을 서비스에 맞게 작성합니다:

```erb
<%# app/views/user_mailer/welcome.html.erb %>
<div style="max-width: 600px; margin: 0 auto; font-family: 'Apple SD Gothic Neo', sans-serif;">
  <div style="background-color: #4F46E5; padding: 30px; text-align: center;">
    <h1 style="color: white; margin: 0;">환영합니다!</h1>
  </div>

  <div style="padding: 30px; background-color: #ffffff;">
    <p style="font-size: 18px; color: #1F2937;">
      안녕하세요, <strong><%= @user.name %></strong>님!
    </p>

    <p style="color: #4B5563; line-height: 1.8;">
      서비스에 가입해주셔서 감사합니다.
      지금 바로 시작해보세요.
    </p>

    <div style="text-align: center; margin: 30px 0;">
      <a href="<%= root_url %>"
         style="background-color: #4F46E5; color: white; padding: 12px 30px;
                text-decoration: none; border-radius: 6px; font-size: 16px;">
        서비스 시작하기
      </a>
    </div>

    <p style="color: #9CA3AF; font-size: 14px;">
      궁금한 점이 있으면 이 메일에 답장해주세요.
    </p>
  </div>
</div>
```

> "이메일 HTML은 웹페이지와 다릅니다. Tailwind CSS를 쓸 수 없고, **인라인 스타일(style 속성)**을 직접 써야 합니다. 이메일 앱들이 외부 CSS를 지원하지 않기 때문입니다."

### Step 5: 개발 환경 테스트 — letter_opener로 확인 (3분)

Rails 콘솔에서 직접 테스트합니다:

```bash
bin/rails console
```

```ruby
# 콘솔에서 실행
UserMailer.welcome(User.first).deliver_now
```

> "브라우저 새 탭이 열리면서 이메일이 표시됩니다. 디자인이 마음에 드나요? 수정하고 싶은 부분이 있으면 템플릿을 고치고 다시 실행해보세요."

알림 이메일과 주간 리포트도 같은 방법으로 테스트합니다:

```ruby
UserMailer.notification(User.first, "테스트 알림입니다").deliver_now
UserMailer.weekly_report(User.first).deliver_now
```

### Step 6: 자동 발송 트리거 연결 (5분)

이메일은 수동으로 보내는 게 아닙니다. **이벤트가 발생하면 자동으로** 보냅니다:

```ruby
# app/models/user.rb
class User < ApplicationRecord
  # 회원가입하면 자동으로 환영 이메일
  after_create_commit :send_welcome_email

  private

  def send_welcome_email
    UserMailer.welcome(self).deliver_later
  end
end
```

> "after_create_commit은 '새 사용자가 데이터베이스에 저장된 후'를 의미합니다. deliver_later를 썼으므로 사용자는 기다리지 않습니다."

알림 이메일은 해당 이벤트가 발생하는 곳에서 보냅니다:

```ruby
# 예: 댓글이 달리면 글쓴이에게 알림
# app/models/comment.rb
class Comment < ApplicationRecord
  after_create_commit :notify_post_author

  private

  def notify_post_author
    return if user == post.user  # 자기 글에 자기가 댓글 달면 안 보냄
    UserMailer.notification(post.user, "#{user.name}님이 댓글을 남겼습니다").deliver_later
  end
end
```

### Step 7: Resend 연동 — 실제 이메일 발송 (7분)

개발 환경에서 확인이 끝났으면, 실제로 이메일을 보낼 수 있게 Resend를 연동합니다.

**1단계: Resend 가입 및 API 키 발급**

1. [resend.com](https://resend.com) 가입 (GitHub 로그인 가능)
2. 대시보드 → API Keys → Create API Key
3. 키를 복사해둡니다 (re_로 시작하는 문자열)

**2단계: gem 설치**

```ruby
# Gemfile
gem "resend"
```

```bash
bundle install
```

**3단계: API 키 저장 (보안)**

```bash
bin/rails credentials:edit
```

```yaml
# credentials에 추가
resend:
  api_key: re_여기에_API_키_붙여넣기
```

**4단계: Resend 초기화**

```ruby
# config/initializers/resend.rb
Resend.api_key = Rails.application.credentials.dig(:resend, :api_key)
```

**5단계: production 환경 설정**

```ruby
# config/environments/production.rb
config.action_mailer.delivery_method = :resend
config.action_mailer.default_url_options = { host: "myservice.com" }
```

> "개발 환경은 letter_opener, 프로덕션은 Resend. 코드는 동일하고 배달 방법만 다릅니다. 택배 회사만 바뀌는 것이지 편지 내용은 같습니다."

### Step 8: 주간 리포트 — Solid Queue 예약 발송 (5분)

주간 리포트는 매주 정해진 시간에 보내야 합니다. Solid Queue의 recurring 기능을 사용합니다:

```ruby
# app/jobs/weekly_report_job.rb
class WeeklyReportJob < ApplicationJob
  queue_as :default

  def perform
    User.find_each do |user|
      UserMailer.weekly_report(user).deliver_later
    end
    Rails.logger.info "[주간리포트] #{User.count}명에게 발송 예약 완료"
  end
end
```

```yaml
# config/recurring.yml
production:
  weekly_report:
    class: WeeklyReportJob
    schedule: every monday at 9am
    description: "매주 월요일 오전 9시 주간 리포트 발송"
```

> "find_each는 사용자가 많아도 메모리를 아끼면서 한 명씩 처리합니다. 1000명이든 10000명이든 안전합니다."

git commit으로 마무리합니다.

```bash
git add -A && git commit -m "이메일 기능 추가: 환영/알림/주간리포트 + Resend 연동"
```

---

## QUIZ

### Q1: 이메일 발송 시점
> "다음 중 이메일을 보내기에 가장 적절한 시점은?"

1. 사용자가 페이지를 방문할 때마다
2. 사용자에게 중요한 변화가 있을 때 (가입, 예약 확정 등)
3. 서비스에 새 기능이 추가될 때마다
4. 매시간 자동으로

정답: 2번
해설: 이메일은 사용자에게 가치가 있는 순간에만 보내야 합니다. 너무 자주 보내면 스팸이 됩니다. "이 이메일을 받으면 사용자가 기쁠까?"를 기준으로 판단하세요.

### Q2: deliver_now vs deliver_later
> "deliver_later를 사용하는 이유는?"

1. 이메일을 더 예쁘게 만들기 위해
2. 이메일 발송을 백그라운드에서 처리해 서비스가 느려지지 않게 하려고
3. 이메일을 여러 명에게 보내기 위해
4. 이메일 내용을 나중에 수정하기 위해

정답: 2번
해설: deliver_now는 이메일 발송이 완료될 때까지 사용자가 기다려야 합니다. 회원가입 버튼을 눌렀는데 3초 동안 멈춰있으면 "고장났나?" 생각하겠죠. deliver_later는 Solid Queue가 백그라운드에서 처리하므로 사용자는 바로 다음 화면으로 넘어갑니다.

### Q3: Action Mailer와 Resend의 관계
> "Action Mailer와 Resend의 역할 차이는?"

1. Action Mailer는 텍스트 이메일, Resend는 HTML 이메일을 담당한다
2. Action Mailer는 이메일을 작성하고, Resend는 실제 배달을 담당한다
3. Action Mailer는 개발용, Resend는 테스트용이다
4. 둘은 같은 기능의 다른 이름이다

정답: 2번
해설: Action Mailer는 편지를 쓰는 사람, Resend는 배달하는 택배 회사입니다. 편지 내용은 Action Mailer가 담당하고, 그 편지를 실제 사용자 메일함까지 전달하는 것은 Resend가 합니다.

### Q4: letter_opener의 용도
> "개발 환경에서 letter_opener를 사용하는 이유는?"

1. 이메일을 더 빠르게 보내기 위해
2. 이메일 디자인을 꾸미기 위해
3. 실제 발송 없이 브라우저에서 이메일 내용을 확인하기 위해
4. 이메일 수신자 목록을 관리하기 위해

정답: 3번
해설: 개발 중에 진짜 이메일을 보내면 테스트 메일이 고객에게 갈 수 있습니다. letter_opener는 이메일을 발송하는 대신 브라우저에서 보여줍니다. 디자인과 내용을 안전하게 확인할 수 있습니다.
