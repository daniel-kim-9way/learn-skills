## EXPLAIN

### 자동화란? — "내가 안 해도 되는 일"을 찾는 것

매일 아침 출근해서 하는 일을 떠올려보세요:

- 어제 만료된 게시글을 닫아야 합니다
- 7일 동안 로그인하지 않은 사용자에게 이메일을 보내야 합니다
- 매주 월요일마다 지난주 통계를 정리해야 합니다

이런 일들의 공통점이 있습니다:

1. **반복적입니다** — 매일/매주 같은 일
2. **규칙이 명확합니다** — "만약 7일 지났으면 이메일 보내기"
3. **데이터 기반입니다** — 날짜, 숫자, 상태를 확인하고 처리

사람이 할 필요가 없습니다. **컴퓨터가 훨씬 잘합니다.** 빠뜨리지 않고, 잊지 않고, 새벽 3시에도 정확히 실행합니다.

### 자동화 대상 찾기 체크리스트

아래 질문에 "네"라고 답하면 자동화 대상입니다:

- "이 일을 매일/매주 하고 있나요?" → **반복 작업**
- "할 때마다 같은 순서로 하나요?" → **규칙적 작업**
- "이 일을 깜빡하면 문제가 생기나요?" → **중요하지만 잊기 쉬운 작업**
- "컴퓨터가 판단할 수 있는 기준이 있나요?" → **자동 판단 가능**

서비스별 자동화 예시:

| 서비스 유형 | 자동화할 일 | 빈도 |
|-----------|-----------|------|
| 중고거래 | 30일 지난 게시글 자동 만료 | 매일 |
| 예약 서비스 | 내일 예약 리마인더 발송 | 매일 오후 6시 |
| 커뮤니티 | 비활성 사용자 알림 | 매주 |
| 쇼핑몰 | 장바구니 리마인더 | 매일 |
| 모든 서비스 | 주간 통계 정리 | 매주 월요일 |

### Rails의 자동화 도구 — Job

Rails에서 자동화는 **Job**으로 만듭니다. Job은 "할 일 목록"에 적어두면 알아서 실행되는 작업입니다.

```ruby
# app/jobs/cleanup_expired_posts_job.rb
class CleanupExpiredPostsJob < ApplicationJob
  def perform
    expired_count = Post.where("expires_at < ?", Time.current)
                        .update_all(status: "closed")

    Rails.logger.info "[자동화] 만료 게시글 #{expired_count}건 정리 완료"
  end
end
```

이 Job이 하는 일:
1. 만료 날짜가 지난 게시글을 찾는다
2. 상태를 "closed"로 바꾼다
3. 몇 건 처리했는지 기록한다

사람이 직접 하면 게시글을 하나씩 확인해야 합니다. Job이 하면 **1초에 수천 건**을 처리합니다.

### Solid Queue = Rails 8의 내장 작업 관리자

**Solid Queue**는 Rails 8에 내장된 작업 큐 시스템입니다. 별도 설치가 필요 없습니다.

하는 일:
- Job을 **대기열**에 넣는다 (줄 세우기)
- 정해진 시간에 **자동 실행**한다 (알람 시계)
- 실패하면 **다시 시도**한다 (자동 재시도)
- 실행 기록을 **저장**한다 (로그)

비유하면:
- **Job** = 해야 할 일 (ex: 만료 게시글 정리)
- **Solid Queue** = 비서 ("내일 아침 9시에 이 일 해주세요" → 정확히 실행)

### Recurring Tasks = 반복 예약

"매일 새벽 3시에 실행해줘"를 설정하는 방법입니다:

```yaml
# config/recurring.yml
production:
  cleanup_expired:
    class: CleanupExpiredPostsJob
    schedule: every day at 3am
    description: "매일 새벽 3시 만료 게시글 정리"

  send_reminders:
    class: SendReminderEmailsJob
    schedule: every day at 6pm
    description: "매일 오후 6시 내일 예약 리마인더"

  weekly_stats:
    class: WeeklyStatsJob
    schedule: every monday at 9am
    description: "매주 월요일 오전 9시 주간 통계"
```

스케줄 문법은 자연스러운 영어입니다:
- `every day at 3am` — 매일 새벽 3시
- `every hour` — 매시간
- `every monday at 10am` — 매주 월요일 오전 10시
- `every 30 minutes` — 30분마다
- `every day at 9am, 6pm` — 매일 오전 9시, 오후 6시

### 모니터링 — 자동화가 잘 돌고 있는지 확인

자동화의 함정: **한 번 설정하면 신경을 안 쓰게 됩니다.** 어느 날 갑자기 안 돌고 있었는데 몰랐다면? 큰 문제입니다.

확인 방법:
1. **로그 확인**: `Rails.logger.info`로 기록한 것을 확인
2. **Solid Queue 대시보드**: Mission Control 설치로 웹에서 확인
3. **에러 알림**: 실패 시 이메일 알림 받기

---

## EXECUTE

### Step 1: 자동화 대상 선정 (5분)

> "서비스 운영 시 매일/매주 반복해야 할 작업이 있나요? 일상 업무 중 '이건 매번 내가 하기 귀찮다'고 느끼는 것은?"

Claude와 함께 자동화 대상 리스트를 만듭니다:

```
[자동화 후보 목록]
1. _________________ (매일 / 매주)
2. _________________ (매일 / 매주)
3. _________________ (매일 / 매주)
```

가장 단순하고 효과가 큰 **1개**를 선택합니다. 첫 번째 자동화는 단순할수록 좋습니다.

추천 시작점:
- 만료 데이터 정리 (가장 단순)
- 리마인더 이메일 발송 (사용자에게 가치)
- 통계 요약 생성 (운영에 도움)

### Step 2: Job 클래스 작성 (10분)

```bash
bin/rails generate job CleanupExpired
```

생성된 파일: `app/jobs/cleanup_expired_job.rb`

학생 서비스에 맞게 Job을 작성합니다. 핵심은 **로깅**입니다:

```ruby
# app/jobs/cleanup_expired_job.rb
class CleanupExpiredJob < ApplicationJob
  queue_as :default

  def perform
    # 1. 처리할 대상 찾기
    expired_posts = Post.where("expires_at < ?", Time.current)
                        .where.not(status: "closed")

    # 2. 처리하기
    count = expired_posts.update_all(status: "closed")

    # 3. 기록 남기기 (중요!)
    Rails.logger.info "[자동화] CleanupExpiredJob: #{count}건 처리 완료 (#{Time.current})"
  end
end
```

> "모든 Job에는 반드시 로그를 남기세요. '몇 건 처리했는지'를 기록하면 나중에 '잘 돌고 있는지' 확인할 수 있습니다."

더 복잡한 Job 예시 — 리마인더 발송:

```ruby
# app/jobs/send_reminder_emails_job.rb
class SendReminderEmailsJob < ApplicationJob
  queue_as :default

  def perform
    # 내일 예약이 있는 사용자 찾기
    tomorrow = Date.tomorrow
    reservations = Reservation.where(date: tomorrow)
                              .where(reminder_sent: false)

    reservations.find_each do |reservation|
      # 이메일 발송
      ReservationMailer.reminder(reservation).deliver_later

      # 발송 기록
      reservation.update(reminder_sent: true)
    end

    Rails.logger.info "[자동화] SendReminderEmailsJob: #{reservations.count}건 리마인더 발송"
  end
end
```

### Step 3: 수동 테스트 — 콘솔에서 먼저 확인 (5분)

스케줄링 전에 **반드시** 수동으로 테스트합니다:

```bash
bin/rails console
```

```ruby
# 즉시 실행 (큐를 거치지 않고 바로)
CleanupExpiredJob.perform_now

# 로그에 "[자동화] CleanupExpiredJob: N건 처리 완료"가 뜨면 성공!
```

에러가 나면 고치고, 정상 동작하면 다음 단계로.

> "perform_now는 큐를 거치지 않고 즉시 실행합니다. 결과를 바로 확인할 수 있어 테스트에 적합합니다. 정상 동작을 확인한 후에 스케줄링으로 전환합니다."

### Step 4: Solid Queue 스케줄링 설정 (10분)

테스트가 끝났으면 자동 실행을 설정합니다:

```yaml
# config/recurring.yml
production:
  cleanup_expired:
    class: CleanupExpiredJob
    schedule: every day at 3am
    description: "매일 새벽 3시 만료 데이터 정리"
```

> "새벽 3시로 설정하는 이유가 있습니다. 사용자가 가장 적은 시간이라 서버 부하가 적고, 하루가 시작되기 전에 정리가 끝납니다."

두 번째 Job도 추가하려면:

```yaml
production:
  cleanup_expired:
    class: CleanupExpiredJob
    schedule: every day at 3am
    description: "매일 새벽 3시 만료 데이터 정리"

  send_reminders:
    class: SendReminderEmailsJob
    schedule: every day at 6pm
    description: "매일 오후 6시 내일 예약 리마인더 발송"
```

개발 환경에서 테스트하려면:

```yaml
# development 환경에서도 테스트하고 싶다면
development:
  cleanup_expired:
    class: CleanupExpiredJob
    schedule: every 5 minutes  # 개발용: 5분마다 실행해서 확인
```

### Step 5: 에러 핸들링 — 실패해도 괜찮게 (5분)

자동화는 무인으로 돌아가므로 **에러 처리가 필수**입니다:

```ruby
class CleanupExpiredJob < ApplicationJob
  queue_as :default

  # 실패 시 자동 재시도 (최대 3번, 간격을 늘려가며)
  retry_on StandardError, wait: :polynomially_longer, attempts: 3

  def perform
    expired_posts = Post.where("expires_at < ?", Time.current)
                        .where.not(status: "closed")

    count = expired_posts.update_all(status: "closed")
    Rails.logger.info "[자동화] CleanupExpiredJob: #{count}건 처리 완료"
  rescue => e
    Rails.logger.error "[자동화 오류] CleanupExpiredJob 실패: #{e.message}"
    raise  # 다시 던져서 retry_on이 처리하게 함
  end
end
```

`retry_on`의 동작:
- 1차 실패 → 3초 후 재시도
- 2차 실패 → 18초 후 재시도
- 3차 실패 → 최종 실패 기록

> "retry_on을 추가하면 네트워크 일시 장애 같은 일시적 오류에서 자동 복구됩니다. 3번 시도해도 실패하면 그때 기록을 남깁니다."

### Step 6: 모니터링 — Mission Control 설치 (선택, 5분)

Solid Queue의 상태를 웹 대시보드에서 확인할 수 있습니다:

```ruby
# Gemfile
gem "mission_control-jobs"
```

```bash
bundle install
```

```ruby
# config/routes.rb
Rails.application.routes.draw do
  mount MissionControl::Jobs::Engine, at: "/jobs"
  # ...
end
```

브라우저에서 `/jobs`에 접속하면:
- 대기 중인 작업 수
- 최근 실행된 작업 목록
- 실패한 작업과 에러 메시지
- 예약된 반복 작업 스케줄

> "배포 후에는 이 대시보드를 가끔 확인하세요. '자동화가 잘 돌고 있는지' 한눈에 볼 수 있습니다."

주의: 프로덕션에서는 대시보드에 인증을 추가해야 합니다 (아무나 접근하면 안 됩니다).

### Step 7: git commit (2분)

```bash
git add -A && git commit -m "자동화 추가: 반복 작업 Job + Solid Queue 스케줄링"
```

> "축하합니다! 이제 서비스가 여러분이 자고 있는 동안에도 스스로 일합니다."

---

## QUIZ

### Q1: 자동화 대상 판별
> "다음 중 자동화에 가장 적합한 업무는?"

1. 새로운 기능 기획하기
2. 고객 불만에 개인적으로 답변하기
3. 매일 밤 만료된 데이터 정리하기
4. 서비스 디자인 변경하기

정답: 3번
해설: 반복적이고 규칙이 명확한 작업이 자동화에 적합합니다. "만료 날짜가 지났으면 상태를 변경한다" — 이것은 명확한 규칙이므로 컴퓨터가 매일 정확히 실행할 수 있습니다.

### Q2: perform_now vs perform_later
> "처음 테스트할 때 perform_now를 쓰는 이유는?"

1. perform_later보다 빠르기 때문에
2. 즉시 실행해서 결과를 바로 확인할 수 있으니까
3. perform_later는 개발 환경에서 동작하지 않아서
4. 데이터베이스 연결이 필요 없어서

정답: 2번
해설: perform_now는 큐를 거치지 않고 즉시 실행합니다. 에러가 나면 바로 보이고, 로그도 바로 확인됩니다. 정상 동작을 확인한 후에 스케줄링으로 전환하면 안전합니다.

### Q3: recurring.yml의 역할
> "config/recurring.yml 파일은 무엇을 설정하나요?"

1. 데이터베이스 연결 정보
2. Job이 자동으로 실행되는 시간과 빈도
3. 서버 재시작 스케줄
4. 이메일 발송 설정

정답: 2번
해설: recurring.yml은 "어떤 Job을 언제 실행할지" 정의합니다. `every day at 3am`처럼 자연스러운 영어로 스케줄을 적으면 Solid Queue가 그 시간에 자동으로 실행합니다.

### Q4: 에러 핸들링의 중요성
> "Job에 retry_on을 추가하는 이유는?"

1. Job을 더 빠르게 실행하기 위해
2. 일시적 오류(네트워크 등) 시 자동으로 재시도하기 위해
3. 코드를 더 깔끔하게 만들기 위해
4. 로그를 더 자세하게 남기기 위해

정답: 2번
해설: 네트워크 일시 장애, 데이터베이스 잠시 느려짐 같은 일시적 오류는 잠시 후 재시도하면 성공하는 경우가 많습니다. retry_on을 추가하면 이런 일시적 오류에서 자동으로 복구됩니다.
