# SQS Queue & SNS Topic Design

**Naming Convention:** `dotlearn-{event}-{env}`  
**Environments:** dev | staging | prod

---

## Queues

| Queue Name | Type | Producer | Consumer | Notes |
|------------|------|----------|----------|-------|
| dotlearn-payment-succeeded-{env} | SQS Standard | Payment Service | Enrollment Service | Visibility timeout: 30s. Max receive count: 3 |
| dotlearn-payment-failed-{env} | SQS Standard | Payment Service | Notification Service | DLQ: dotlearn-payment-failed-dlq-{env} |
| dotlearn-lesson-completed-{env} | SQS Standard | Progress Service | Enrollment Service | High throughput. Batch size: 10 |
| dotlearn-enrollment-completed-{env} | SQS Standard | Enrollment Service | Certificate + Notification | Fan-out via SNS Topic (2 consumers) |
| dotlearn-course-access-revoked-{env} | SQS Standard | Payment Service | Enrollment Service | Triggered by refund webhook |
| dotlearn-new-reply-{env} | SQS Standard | Forum Service | Notification Service | Throttle: 10 msg/sec (SES rate limit) |
| dotlearn-password-reset-{env} | SQS Standard | Auth Service | Notification Service | DLQ: dotlearn-password-reset-dlq-{env} |

---

## SNS Topics

| Topic Name | Type | Producer | Consumer | Notes |
|------------|------|----------|----------|-------|
| dotlearn-notifications-sns-{env} | SNS Topic | Any service | Notification Service | Fan-out for multi-consumer events |

---

## Dead Letter Queues (DLQ)

| DLQ Name | Parent Queue | CloudWatch Alarm |
|----------|-------------|-----------------|
| dotlearn-payment-succeeded-dlq-{env} | dotlearn-payment-succeeded-{env} | Alarm if depth > 0 |
| dotlearn-payment-failed-dlq-{env} | dotlearn-payment-failed-{env} | Alarm if depth > 0 |
| dotlearn-lesson-completed-dlq-{env} | dotlearn-lesson-completed-{env} | Alarm if depth > 0 |
| dotlearn-enrollment-completed-dlq-{env} | dotlearn-enrollment-completed-{env} | Alarm if depth > 0 |
| dotlearn-course-access-revoked-dlq-{env} | dotlearn-course-access-revoked-{env} | Alarm if depth > 0 |
| dotlearn-new-reply-dlq-{env} | dotlearn-new-reply-{env} | Alarm if depth > 0 |
| dotlearn-password-reset-dlq-{env} | dotlearn-password-reset-{env} | Alarm if depth > 0 |

---

## Rules

- Every SQS queue MUST have a DLQ
- A non-empty DLQ means a consumer is failing silently
- CloudWatch alarm must fire immediately when DLQ depth > 0
- All queue names use lowercase with hyphens only
- Never hardcode queue URLs — always resolve from env variable or Secrets Manager