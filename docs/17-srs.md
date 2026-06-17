# 17 - Software Requirements Specification (SRS)

## 1. Introduction

### 1.1 Purpose
This Software Requirements Specification (SRS) describes the complete requirements for the BookEase online booking and reservation system. It is intended to guide development, testing, and evaluation of the application.

### 1.2 Scope
BookEase is a full-stack web application that allows customers to book service appointments online and allows business admins to manage their services, schedules, and reservations from a single dashboard.

### 1.3 Definitions & Acronyms
| Term     | Definition                                              |
|----------|---------------------------------------------------------|
| JWT      | JSON Web Token – used for authentication                |
| API      | Application Programming Interface                       |
| CRUD     | Create, Read, Update, Delete                            |
| Admin    | A user with business management privileges              |
| Customer | A user who books appointments                           |
| Slot     | A specific date and time window available for booking   |

### 1.4 References
- PRD: 08-prd.md
- User Stories: 11-user-stories.md
- Use Cases: 15-use-cases.md

---

## 2. Overall Description

### 2.1 Product Perspective
BookEase is a standalone web application with a React frontend and a Node.js/Express backend, connected to a MongoDB database. It is deployed on cloud platforms using free tiers.

### 2.2 Product Functions (Summary)
- User registration and authentication (Customer and Admin roles)
- Service management by Admin
- Time slot generation and management
- Online appointment booking by Customers
- Email notifications for booking events
- Admin dashboard for schedule and booking management

### 2.3 User Classes
- **Customer:** Books and manages their own appointments
- **Admin:** Full control over services, slots, and all bookings

### 2.4 Assumptions & Dependencies
- Users have access to modern web browsers (Chrome, Firefox, Safari, Edge)
- Users have valid email addresses
- Email delivery depends on a third-party service (Nodemailer with Gmail or similar)
- Internet connectivity is required for all functions

---

## 3. Functional Requirements

*(Full list in 13-functional-requirements.md — summarized here)*

- FR-01 to FR-07: Authentication and role management
- FR-08 to FR-11: Admin service management
- FR-12 to FR-15: Time slot management
- FR-16 to FR-22: Customer booking workflow
- FR-23 to FR-26: Admin booking management
- FR-27 to FR-28: Email notifications

---

## 4. Non-Functional Requirements

*(Full list in 14-non-functional-requirements.md — summarized here)*

- **Performance:** Page load < 2s, API response < 500ms
- **Security:** bcrypt passwords, JWT auth, input validation
- **Usability:** Booking completable in < 3 minutes, responsive design
- **Reliability:** 99% uptime target, graceful error handling
- **Maintainability:** MVC structure, environment variables, documented API

---

## 5. System Constraints

- Must run entirely within free-tier hosting limits
- Solo developer — complexity must remain manageable
- No payment integration in v1.0
- No mobile native app — web only

---

## 6. External Interface Requirements

### 6.1 User Interfaces
- React SPA (Single Page Application)
- Responsive design using Tailwind CSS
- Accessible on desktop and mobile browsers

### 6.2 API Interfaces
- RESTful API built with Express.js
- JSON request/response format
- Auth via Authorization header: `Bearer <token>`

### 6.3 Email Interface
- Nodemailer library with a Gmail SMTP account
- Sends: booking confirmation, booking cancellation

### 6.4 Database Interface
- MongoDB via Mongoose ORM
- Hosted on MongoDB Atlas (free tier)
