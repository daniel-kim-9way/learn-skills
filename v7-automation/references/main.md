## EXPLAIN

### 자동화란?

매일 반복하는 일 중 **"규칙만 있으면 컴퓨터가 할 수 있는 일"**을 코드에게 맡기는 것.

자동화에 적합한 업무:
1. **반복적이다**: 매일/매주 같은 작업
2. **규칙이 명확하다**: "만약 A이면 B를 한다"
3. **데이터 기반이다**: 숫자, 날짜, 상태를 확인하고 처리

예시: 만료 게시글 정리, 비활성 계정 알림, 일일 통계 요약

### Rails에서 자동화하는 방법

```ruby
# app/jobs/cleanup_expired_posts_job.rb
class CleanupExpiredPostsJob < ApplicationJob
  def perform
    Post.where("expires_at < ?", Time.current).update_all(status: "closed")
  end
end
```

### Solid Queue로 스케줄링

```yaml
# config/recurring.yml
cleanup_posts:
  class: CleanupExpiredPostsJob
  schedule: every day at 3am
```

Rails 8에 내장되어 별도 설치 불필요.

---

## EXECUTE

### Step 1: 자동화 대상 선정 (5분)

> "서비스 운영 시 매일/매주 반복해야 할 작업이 있나요? 일상 업무 중 자동화하고 싶은 것은?"

예시: 만료 데이터 정리, 통계 요약, 리마인더 발송, 데이터 백업

### Step 2: Job 클래스 작성 (10분)

```bash
bin/rails generate job [자동화이름]
```

학생 서비스에 맞는 Job을 Claude와 함께 작성한다. 로깅을 포함:

```ruby
class CleanupExpiredPostsJob < ApplicationJob
  def perform
    count = Post.where("expires_at < ?", Time.current).update_all(status: "closed")
    Rails.logger.info "[자동화] #{count}건 처리 완료"
  end
end
```

### Step 3: 수동 테스트 (5분)

Rails 콘솔에서 직접 실행:
```ruby
CleanupExpiredPostsJob.perform_now
```

> "콘솔에서 먼저 테스트하는 것은 좋은 습관입니다."

### Step 4: Solid Queue 스케줄링 (10분)

`config/recurring.yml` 작성:
```yaml
production:
  cleanup_posts:
    class: CleanupExpiredPostsJob
    schedule: every day at 3am
```

스케줄 예시: `every day at 9am`, `every hour`, `every monday at 10am`, `every 30 minutes`

### Step 5: 에러 핸들링 (3분)

```ruby
def perform
  # 작업 로직
rescue => e
  Rails.logger.error "[Job 오류] #{e.message}"
  raise
end
```

git commit으로 마무리.

---

## QUIZ

### Q1: 자동화 대상 판별
> "다음 중 자동화에 가장 적합한 업무는?"

1. 새로운 기능 기획하기
2. 고객 불만에 개인적으로 답변하기
3. 매일 밤 만료된 데이터 정리하기
4. 서비스 디자인 변경하기

정답: 3번
해설: 반복적이고 규칙이 명확한 작업이 자동화에 적합합니다.

### Q2: perform_now vs perform_later
> "처음 테스트할 때 perform_now를 쓰는 이유는?"

1. perform_later보다 빠르기 때문에
2. 즉시 실행해서 결과를 바로 확인할 수 있으니까
3. perform_later는 개발 환경에서 동작하지 않아서
4. 데이터베이스 연결이 필요 없어서

정답: 2번
해설: perform_now는 큐를 거치지 않고 즉시 실행합니다. 정상 동작 확인 후 스케줄링으로 전환하면 됩니다.
