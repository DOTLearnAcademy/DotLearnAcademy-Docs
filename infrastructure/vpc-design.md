# VPC & Network Architecture

## Region
ap-south-1 (Mumbai) — primary region for India-first audience.

## VPC
| Resource        | Value          | Purpose                              |
|-----------------|----------------|--------------------------------------|
| Custom VPC      | 10.0.0.0/16    | Isolated network for all DOTLearn resources |
| Public Subnet 1 | 10.0.1.0/24    | EC2 instance (public IP). Direct internet access |
| Private Subnet 1| 10.0.3.0/24    | RDS database (no public access)      |
| Internet Gateway| N/A            | Inbound internet traffic to EC2      |
| Route Table     | 0.0.0.0/0 → IGW| Routes internet traffic to EC2       |

## Notes
- Single-AZ design to keep costs under $30/month
- NAT Gateway removed (saves ~$35/mo) — not needed for dev/portfolio
- No second AZ, no Multi-AZ RDS standby