# RDS Instance Plan (Cost-Optimized)

## Strategy
Single shared RDS instance (db.t3.micro) with 9 separate databases.
Saves ~$200+/month vs isolated instances.

## Engine
Microsoft SQL Server (Express Edition — free tier eligible)

## Instances

| Database       | Service      | Dev            | Production     | Multi-AZ | Read Replica |
|----------------|--------------|----------------|----------------|----------|--------------|
| UserDb         | Auth         | db.t3.micro    | db.t3.micro    | No       | No           |
| CourseDb       | Course       | shared         | db.t3.micro    | No       | No           |
| ContentDb      | Lesson       | shared         | db.t3.micro    | No       | No           |
| EnrollmentDb   | Enrollment   | shared         | db.t3.micro    | No       | No           |
| AssessmentDb   | Assessment   | shared         | db.t3.micro    | No       | No           |
| PaymentDb      | Payment      | shared         | db.t3.micro    | No       | No           |
| ProgressDb     | Progress     | shared         | db.t3.micro    | No       | No           |
| ForumDb        | Forum        | shared         | db.t3.micro    | No       | No           |
| NotificationDb | Notification | shared         | db.t3.micro    | No       | No           |

## Backup Policy
| Environment | Retention  | Method                              |
|-------------|------------|-------------------------------------|
| Dev         | 7 days     | RDS automated backup                |
| Production  | 35 days    | RDS automated backup + monthly manual snapshot |

## Notes
- Multi-AZ removed — not needed for portfolio/placement projects
- Read Replicas removed — no high-read workload at this scale
- db.r5 instances removed — overkill for dev/portfolio