# 13 - Functional Requirements

## What are Functional Requirements?
Functional requirements describe **what the system must do** — the specific behaviors and functions it must provide.

---

## Authentication & User Management

| ID   | Requirement                                                                 |
|------|-----------------------------------------------------------------------------|
| FR-01 | The system shall allow new users to register with a name, email, and password. |
| FR-02 | The system shall validate that the email is unique during registration.        |
| FR-03 | The system shall hash passwords before storing them in the database.           |
| FR-04 | The system shall allow registered users to log in with email and password.     |
| FR-05 | The system shall issue a JWT token upon successful login.                       |
| FR-06 | The system shall distinguish between two roles: Customer and Admin.            |
| FR-07 | The system shall restrict admin routes to users with the Admin role.           |

---

## Service Management (Admin)

| ID   | Requirement                                                                 |
|------|-----------------------------------------------------------------------------|
| FR-08 | The system shall allow admins to create a service with name, description, duration, and price. |
| FR-09 | The system shall allow admins to edit any service.                           |
| FR-10 | The system shall allow admins to delete a service (and cascade-cancel related bookings). |
| FR-11 | The system shall display all active services on the public service listing page. |

---

## Availability & Time Slot Management (Admin)

| ID   | Requirement                                                                 |
|------|-----------------------------------------------------------------------------|
| FR-12 | The system shall allow admins to define working days and hours.              |
| FR-13 | The system shall auto-generate time slots based on service duration and working hours. |
| FR-14 | The system shall mark a slot as "booked" when a reservation is confirmed.    |
| FR-15 | The system shall free a slot when a booking is cancelled.                    |

---

## Booking (Customer)

| ID   | Requirement                                                                 |
|------|-----------------------------------------------------------------------------|
| FR-16 | The system shall allow a logged-in customer to browse available services.    |
| FR-17 | The system shall allow a customer to select a date and view available slots. |
| FR-18 | The system shall allow a customer to book an appointment by selecting a service and slot. |
| FR-19 | The system shall prevent double-booking of the same slot.                    |
| FR-20 | The system shall send a confirmation email upon successful booking.           |
| FR-21 | The system shall display a customer's upcoming and past bookings.             |
| FR-22 | The system shall allow a customer to cancel an upcoming booking.              |

---

## Admin Booking Management

| ID   | Requirement                                                                 |
|------|-----------------------------------------------------------------------------|
| FR-23 | The system shall display all bookings to the admin, sorted by date.          |
| FR-24 | The system shall allow admins to cancel any booking.                          |
| FR-25 | The system shall allow admins to filter bookings by date.                     |
| FR-26 | The system shall show a daily/weekly schedule view on the admin dashboard.    |

---

## Notifications

| ID   | Requirement                                                                 |
|------|-----------------------------------------------------------------------------|
| FR-27 | The system shall send an email confirmation when a booking is created.        |
| FR-28 | The system shall send an email notification when a booking is cancelled.      |
