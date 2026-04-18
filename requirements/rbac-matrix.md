## 0.1.3 Role-Based Access Control (RBAC) Matrix

Each API endpoint is mapped to access levels to enforce authorization before backend implementation.

Legend:
- Y = Allowed
- Own only = Only resource owner
- Own course = Instructor who owns the course
- Enrolled = Student enrolled in the course

---

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| POST /auth/register | Y | - | - | - | - |
| POST /auth/login | Y | - | - | - | - |
| POST /auth/refresh | Y | - | - | - | - |
| GET /auth/.well-known/jwks.json | Y | - | - | - | - |
| POST /auth/password-reset | Y | - | - | - | - |

---

### 👤 Profile

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| GET /auth/profile/:id | - | Own only | Own only | Y | - |
| PUT /auth/profile/:id | - | Own only | Own only | Y | - |

---

### 📚 Courses

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| GET /courses (browse/search) | Y | Y | Y | Y | - |
| POST /courses (create) | - | - | Y | Y | - |
| PUT /courses/:id (edit) | - | - | Own course | Y | - |
| DELETE /courses/:id (archive) | - | - | Own course | Y | - |
| GET /internal/courses/:id/price | - | - | - | - | Y |

---

### 🎥 Lessons

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| GET /lessons/:id/content | - | Enrolled | Own course | Y | - |
| POST /lessons (create) | - | - | Own course | Y | - |

---

### 💳 Payments

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| POST /payments/checkout | - | Y | - | - | - |
| POST /payments/webhook/* | Y (signature verified) | - | - | - | - |
| POST /payments/refund | - | - | - | Y | - |
| GET /payments/student/:id | - | Own only | - | Y | - |

---

### 📦 Enrollments

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| POST /enrollments/free | - | Y | - | - | - |
| GET /internal/enrollments/check | - | - | - | - | Y |

---

### 🧠 Quizzes & Progress

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| POST /quizzes (create) | - | - | Own course | Y | - |
| POST /quizzes/:id/attempts/start | - | Enrolled | - | - | - |
| PUT /progress/track | - | Own only | - | - | - |

---

### 🎓 Certificates

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| GET /certificates/verify/:code | Y | - | - | - | - |

---

### 💬 Forum & Notifications

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| POST /forum/threads | - | Enrolled | Own course | Y | - |
| GET /notifications/:userId | - | Own only | Own only | Y | - |

---

### 🛠️ Admin

| Endpoint | Public | Student | Instructor | Admin | Internal |
|----------|--------|---------|------------|--------|----------|
| PUT /admin/users/:id/suspend | - | - | - | Y | - |
| PUT /admin/courses/:id/approve | - | - | - | Y | - |