# 📘 Use Cases – DotLearnAcademy LMS

This document defines the core use cases for the DotLearnAcademy Learning Management System.

---

## 🎓 Student Use Cases

### 1. Student Registration & Login
- **Actor:** Student  
- **Priority:** Must-Have  
- **Description:** Students can register and log in using email or OAuth providers.  
- **Notes:** Auth Service, OAuth (Google, GitHub)

---

### 2. Browse & Search Course Catalog
- **Actor:** Student  
- **Priority:** Must-Have  
- **Description:** Students can search and filter courses.  
- **Notes:** Full-text search, filters, pagination

---

### 3. View Course Details & Free Preview
- **Actor:** Student  
- **Priority:** Must-Have  
- **Description:** Students can view course info and preview lessons.  
- **Notes:** `isPreview` flag on lessons

---

### 4. Enroll in Free Course
- **Actor:** Student  
- **Priority:** Must-Have  
- **Description:** Students can enroll in free courses directly.  
- **Notes:** No payment flow required

---

### 5. Purchase Paid Course
- **Actor:** Student  
- **Priority:** Must-Have  
- **Description:** Students can purchase courses.  
- **Notes:** Stripe / Razorpay integration (PCI-compliant)

---

### 6. Watch Lessons & Track Progress
- **Actor:** Student  
- **Priority:** Must-Have  
- **Description:** Students can watch videos and track progress.  
- **Notes:** Progress heartbeat every 30 seconds

---

### 7. Take Quiz & View Results
- **Actor:** Student  
- **Priority:** Must-Have  
- **Description:** Students can attempt quizzes and view scores.  
- **Notes:** Auto-grading, attempt history

---

### 8. Download Certificate
- **Actor:** Student  
- **Priority:** Must-Have  
- **Description:** Students can download completion certificates.  
- **Notes:** PDF with QR verification

---

### 9. Participate in Discussion Forum
- **Actor:** Student  
- **Priority:** Should-Have  
- **Description:** Students can post and reply in discussions.  
- **Notes:** Linked to course/lesson

---

### 10. Manage Profile & Avatar
- **Actor:** Student  
- **Priority:** Should-Have  
- **Description:** Students can update profile and upload avatar.  
- **Notes:** Presigned S3 upload

---

### 11. View Purchase History & Subscriptions
- **Actor:** Student  
- **Priority:** Should-Have  
- **Description:** Students can view payment history and subscriptions.  
- **Notes:** Payment Service API

---

### 12. Subscription Plan Management
- **Actor:** Student / Admin  
- **Priority:** Should-Have  
- **Description:** Manage subscription lifecycle.  
- **Notes:** Stripe subscription flow

---

## 👨‍🏫 Instructor Use Cases

### 13. Create & Publish Course
- **Actor:** Instructor  
- **Priority:** Must-Have  
- **Description:** Instructors can create and publish courses.  
- **Notes:** Draft → Published → Archived states

---

### 14. Upload Videos & Resources
- **Actor:** Instructor  
- **Priority:** Must-Have  
- **Description:** Upload course content like videos and PDFs.  
- **Notes:** Presigned S3 upload

---

### 15. Build Quizzes
- **Actor:** Instructor  
- **Priority:** Must-Have  
- **Description:** Create quizzes with different question types.  
- **Notes:** Marks configuration, auto-grading

---

### 16. View Analytics
- **Actor:** Instructor  
- **Priority:** Must-Have  
- **Description:** View enrollment and revenue analytics.  
- **Notes:** Dashboard KPIs

---

### 17. Moderate Discussions
- **Actor:** Instructor  
- **Priority:** Should-Have  
- **Description:** Manage Q&A discussions.  
- **Notes:** Pin, close, delete, mark answers

---

### 18. Manage Students
- **Actor:** Instructor  
- **Priority:** Should-Have  
- **Description:** View student progress and performance.  
- **Notes:** Filter by progress segments

---

## 🛠️ Admin Use Cases

### 19. Approve / Reject Courses
- **Actor:** Admin  
- **Priority:** Must-Have  
- **Description:** Review and approve submitted courses.  
- **Notes:** Notify instructors

---

### 20. Manage Users
- **Actor:** Admin  
- **Priority:** Must-Have  
- **Description:** Manage all platform users.  
- **Notes:** Role-based actions (suspend, delete)

---

### 21. View Platform Analytics
- **Actor:** Admin  
- **Priority:** Must-Have  
- **Description:** View system-wide metrics.  
- **Notes:** Revenue, MAU, course stats

---

### 22. Send System Notifications
- **Actor:** Admin  
- **Priority:** Should-Have  
- **Description:** Broadcast notifications to users.  
- **Notes:** Target by role

---

### 23. Audit Logs
- **Actor:** Admin  
- **Priority:** Nice-to-Have  
- **Description:** Track admin actions.  
- **Notes:** Paginated logs