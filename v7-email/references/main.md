## EXPLAIN

### 이메일, 언제 보내야 할까?

사용자에게 이메일이 오면 좋은 순간:
- **회원가입 직후**: "환영합니다!" -- 사용자는 안심합니다
- **중요한 변화**: "새 댓글이 달렸어요", "예약이 확정되었어요"
- **리마인더**: "내일 예약이 있습니다"

핵심은 **사용자에게 가치가 있는 순간**에만 보내는 것입니다.

### Action Mailer = Rails의 우체부

```ruby
class UserMailer < ApplicationMailer
  def welcome_email(user)
    @user = user
    mail(to: @user.email, subject: "환영합니다!")
  end
end
```

호출: `UserMailer.welcome_email(user).deliver_later`

### Resend = 실제 배달 서비스

Action Mailer가 편지를 작성하면, **Resend**가 실제로 배달합니다. 무료 월 3,000통, API 키 하나면 바로 사용 가능.

### Solid Queue = 예약 배송

```ruby
UserMailer.reminder_email(user).deliver_later(wait: 1.hour)
UserMailer.daily_digest.deliver_later(wait_until: Date.tomorrow.beginning_of_day + 9.hours)
```

---

## EXECUTE

### Step 1: 이메일 시나리오 선정 (3분)

> "서비스에서 사용자에게 이메일을 보내면 좋을 상황 2가지를 생각해보세요."

가장 단순한 시나리오 1개를 선택한다 (회원가입 환영 메일 권장).

### Step 2: Action Mailer 생성 (5분)

```bash
bin/rails generate mailer User welcome
```

생성 파일: `app/mailers/user_mailer.rb`, `app/views/user_mailer/welcome.html.erb`
학생 서비스에 맞게 Mailer와 뷰 템플릿을 수정한다.

### Step 3: 개발 환경 테스트 (5분)

letter_opener gem으로 브라우저에서 이메일 확인:
```ruby
# Gemfile (development 그룹)
gem "letter_opener"
# config/environments/development.rb
config.action_mailer.delivery_method = :letter_opener
```

Rails 콘솔에서: `UserMailer.welcome(User.first).deliver_now`

### Step 4: Resend 연동 (7분)

1. resend.com 가입 → API 키 발급
2. `gem "resend"` 추가, `config/initializers/resend.rb` 설정
3. credentials에 API 키 저장: `bin/rails credentials:edit`
4. production 환경: `config.action_mailer.delivery_method = :resend`

### Step 5: 발송 트리거 연결 (5분)

```ruby
# app/models/user.rb
after_create_commit :send_welcome_email
private
def send_welcome_email
  UserMailer.welcome(self).deliver_later
end
```

### Step 6: Solid Queue 예약 발송 (5분)

```ruby
UserMailer.tips_email(@user).deliver_later(wait: 1.hour)
```

> "deliver_later를 사용하면 Solid Queue가 이메일을 대기열에 넣고, 지정한 시간에 자동으로 보냅니다."

git commit으로 마무리.

---

## QUIZ

### Q1: 이메일 발송 시점
> "다음 중 이메일을 보내기에 가장 적절한 시점은?"

1. 사용자가 페이지를 방문할 때마다
2. 사용자에게 중요한 변화가 있을 때 (가입, 예약 확정 등)
3. 서비스에 새 기능이 추가될 때마다
4. 매시간 자동으로

정답: 2번
해설: 이메일은 사용자에게 가치가 있는 순간에만 보내야 합니다. 너무 자주 보내면 스팸이 됩니다.

### Q2: deliver_now vs deliver_later
> "deliver_later를 사용하는 이유는?"

1. 이메일을 더 예쁘게 만들기 위해
2. 이메일 발송을 백그라운드에서 처리해 서비스가 느려지지 않게 하려고
3. 이메일을 여러 명에게 보내기 위해
4. 이메일 내용을 나중에 수정하기 위해

정답: 2번
해설: deliver_now는 발송 완료까지 사용자가 기다려야 합니다. deliver_later는 Solid Queue가 백그라운드에서 처리합니다.
