## 0.1.2 Non-Functional Requirements (NFRs)

NFRs define the operational quality bar for the system. Each requirement includes a measurable SLA.

---

### 🚀 Performance

| Requirement | Target / SLA | Implementation Notes |
|------------|-------------|---------------------|
| API response time (p95) | < 200 ms | Measured at API Gateway / backend logs |
| Page load (First Contentful Paint) | < 1.5 s | Angular lazy loading + CDN caching (CloudFront) |
| Video stream start latency | < 2 s | CloudFront signed URLs + S3 optimization |

---

### ⚙️ Availability

| Requirement | Target / SLA | Implementation Notes |
|------------|-------------|---------------------|
| Platform uptime | 99.9% | Single-AZ deployment (EC2/ECS + RDS). Manual failover strategy |

---

### 📈 Scalability

| Requirement | Target / SLA | Implementation Notes |
|------------|-------------|---------------------|
| Concurrent users (browsing) | 500 users | Single instance/service. Manual scaling when required |
| Concurrent video streaming | 100 users | Handled via CDN (CloudFront), no backend load |

---

### 🔐 Security

| Requirement | Target / SLA | Implementation Notes |
|------------|-------------|---------------------|
| Access token expiry | 15 minutes | JWT (RS256), stateless authentication |
| Refresh token expiry | 7 days | Rotation enabled, single-use tokens |
| Password hashing | BCrypt (cost factor 12) | Industry-standard secure hashing |

---

### 🧾 Data Integrity

| Requirement | Target / SLA | Implementation Notes |
|------------|-------------|---------------------|
| Payment idempotency | 100% (no double charges) | Unique Transaction ID enforced |

---

### 💾 Data Retention

| Requirement | Target / SLA | Implementation Notes |
|------------|-------------|---------------------|
| DB backup (dev) | 7 days | Automated backups enabled |
| DB backup (prod) | 35 days | Automated + periodic manual snapshots |

---

### ⚖️ Compliance

| Requirement | Target / SLA | Implementation Notes |
|------------|-------------|---------------------|
| PCI DSS | SAQ A level | Stripe/Razorpay handles all card data |
| Data privacy (GDPR) | User deletion supported | Soft delete + permanent purge endpoint |