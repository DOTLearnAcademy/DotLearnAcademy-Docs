# Security Groups

## EC2-SG
Attached to: EC2 instance

| Direction | Protocol | Port | Source         | Purpose              |
|-----------|----------|------|----------------|----------------------|
| Inbound   | TCP      | 80   | 0.0.0.0/0      | HTTP traffic         |
| Inbound   | TCP      | 443  | 0.0.0.0/0      | HTTPS traffic        |
| Inbound   | TCP      | 22   | Your IP only   | SSH access           |
| Outbound  | All      | All  | 0.0.0.0/0      | All outbound allowed |

## RDS-SG
Attached to: RDS instance

| Direction | Protocol | Port | Source   | Purpose                        |
|-----------|----------|------|----------|--------------------------------|
| Inbound   | TCP      | 1433 | EC2-SG   | MSSQL access from EC2 only     |
| Outbound  | None     | -    | -        | No outbound allowed            |

## Notes
- ALB Security Group removed — no load balancer needed for dev/portfolio
- EC2 handles all traffic directly