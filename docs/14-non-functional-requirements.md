# 14 - Non-Functional Requirements

## What are Non-Functional Requirements?
Non-functional requirements describe **how** the system performs its functions — quality attributes like speed, security, usability, and reliability.

---

## Performance

| ID    | Requirement                                                                          |
|-------|--------------------------------------------------------------------------------------|
| NFR-01 | The application shall load the home page in under 2 seconds on a standard connection. |
| NFR-02 | API responses shall return within 500ms for standard CRUD operations.                |
| NFR-03 | The booking confirmation email shall be sent within 60 seconds of booking.           |

---

## Security

| ID    | Requirement                                                                          |
|-------|--------------------------------------------------------------------------------------|
| NFR-04 | Passwords shall be hashed using bcrypt before storage.                               |
| NFR-05 | All protected API routes shall require a valid JWT token.                            |
| NFR-06 | JWT tokens shall expire after 24 hours.                                              |
| NFR-07 | The system shall prevent SQL/NoSQL injection through input validation and Mongoose sanitization. |
| NFR-08 | Admin routes shall be inaccessible to users with the Customer role.                  |

---

## Usability

| ID    | Requirement                                                                          |
|-------|--------------------------------------------------------------------------------------|
| NFR-09 | A new user shall be able to complete a booking within 3 minutes without any instructions. |
| NFR-10 | All form errors shall be displayed inline next to the relevant field.                |
| NFR-11 | The UI shall be responsive and usable on screens from 375px (mobile) to 1440px (desktop). |
| NFR-12 | The system shall provide clear feedback for every user action (success/error messages). |

---

## Reliability & Availability

| ID    | Requirement                                                                          |
|-------|--------------------------------------------------------------------------------------|
| NFR-13 | The system shall aim for 99% uptime during evaluation/demo periods.                  |
| NFR-14 | The system shall handle duplicate booking attempts gracefully without crashing.      |

---

## Maintainability

| ID    | Requirement                                                                          |
|-------|--------------------------------------------------------------------------------------|
| NFR-15 | The codebase shall follow a clear folder structure (MVC pattern on the backend).     |
| NFR-16 | All API endpoints shall be documented (in this TDD or via README).                  |
| NFR-17 | Environment variables (DB URI, JWT secret, email credentials) shall not be hardcoded. |

---

## Scalability

| ID    | Requirement                                                                          |
|-------|--------------------------------------------------------------------------------------|
| NFR-18 | The database schema shall support future addition of multiple services without restructuring. |
| NFR-19 | The backend shall be structured so additional roles (e.g. Staff) can be added in future. |
