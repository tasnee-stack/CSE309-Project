# 20 - Technical Design Document (TDD)

## 1. Introduction
This Technical Design Document describes the implementation details of the BookEase system — how the components are built, how they interact, and the key technical decisions made during design.

---

## 2. Technology Stack

| Component     | Technology           | Reason                                             |
|---------------|----------------------|----------------------------------------------------|
| Frontend      | React.js (Vite)      | Component-based, fast dev server, large ecosystem  |
| Styling       | Tailwind CSS         | Utility-first, fast UI development                 |
| HTTP Client   | Axios                | Clean API for REST calls, interceptor support      |
| Backend       | Node.js + Express    | Lightweight, fast, JavaScript throughout           |
| Auth          | JWT + bcrypt         | Stateless auth; bcrypt for secure password hashing |
| Database      | MongoDB + Mongoose   | Flexible schema fits the booking data model        |
| Email         | Nodemailer (Gmail)   | Simple, no-cost email sending                      |
| Deployment    | Vercel + Render      | Free tiers suitable for course project             |

---

## 3. Key Technical Decisions

### 3.1 JWT for Authentication
Chose stateless JWT over sessions because:
- No server-side session storage needed
- Works naturally with a REST API
- Easy to implement role checks by decoding the token payload

### 3.2 MongoDB over SQL
Chose MongoDB because:
- Flexible schema — bookings/services don't need rigid relationships
- Native JSON format matches the Node.js stack
- MongoDB Atlas free tier is generous enough for this project

### 3.3 React Context for Auth State
Used React Context + useState instead of Redux because:
- Project is small — Redux would be overkill
- AuthContext provides user data and login/logout functions app-wide

---

## 4. API Design Summary
*(Full API details in 22-api-design.md)*

- Base URL: `https://your-api.render.com/api`
- Format: JSON
- Auth: `Authorization: Bearer <token>` on protected routes

Key route groups:
- `/api/auth` — register, login
- `/api/services` — CRUD for services
- `/api/slots` — view and manage time slots
- `/api/bookings` — create, view, cancel bookings

---

## 5. Data Validation Strategy

**Backend:**
- Mongoose schema-level validation (required, type, minlength)
- Custom validation in controllers (e.g. slot availability check before booking)

**Frontend:**
- Controlled React form inputs
- Client-side validation before API call (empty fields, email format)
- Display API error messages from responses

---

## 6. Error Handling

**Backend:**
- All controllers wrapped in try/catch
- Central error handler middleware returns consistent error format:
```json
{
  "success": false,
  "message": "Descriptive error message"
}
```

**Frontend:**
- Axios response interceptor catches 401 (unauthorized) → redirects to login
- All API calls show error toast/message to user

---

## 7. Email Notification Design

**Library:** Nodemailer
**Transport:** Gmail SMTP (via app password)

**Booking Confirmation Email:**
- To: customer email
- Subject: "Your booking is confirmed – BookEase"
- Body: Service name, date, time, cancellation instructions

**Cancellation Email:**
- To: customer email
- Subject: "Your booking has been cancelled – BookEase"
- Body: Service name, original date/time, invitation to rebook

---

## 8. Security Considerations

| Risk                        | Mitigation                                         |
|-----------------------------|-----------------------------------------------------|
| Password exposure           | bcrypt hashing (salt rounds: 10)                   |
| Unauthorized API access     | JWT middleware on all protected routes             |
| Role escalation             | roleMiddleware checks `user.role === 'admin'`      |
| NoSQL injection             | Mongoose sanitization + `express-mongo-sanitize`   |
| Sensitive config exposure   | All secrets in `.env`, never committed to Git      |
