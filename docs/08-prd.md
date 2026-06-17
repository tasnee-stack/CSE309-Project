# 08 - Product Requirement Document (PRD)

## Product Name
**BookEase** – Online Appointment & Reservation System

## Version
1.0 (Initial Release)

## Product Vision
To empower small service businesses with a simple, free, and reliable online booking tool — eliminating manual scheduling and improving the customer experience.

---

## Goals & Objectives

| Goal                          | Objective                                                                 |
|-------------------------------|---------------------------------------------------------------------------|
| Reduce manual booking effort  | Customers can self-book without contacting the business                   |
| Prevent double-bookings       | System enforces slot availability before confirming                       |
| Improve customer experience   | Booking completes in under 2 minutes with email confirmation               |
| Give admin full control       | Admin can manage services, time slots, and all bookings from one dashboard |

---

## Target Users
1. **Customers** – People booking appointments with a business
2. **Admins** – Business owners or managers managing the schedule

---

## Core Features (MVP)

### For Customers
- Register and log in to an account
- View all available services offered by the business
- Browse available time slots for a service
- Book an appointment (select service → select date/time → confirm)
- View upcoming and past bookings
- Cancel an upcoming booking
- Receive email confirmation after booking

### For Admins
- Log in to the admin dashboard
- Add, edit, or delete services (name, description, duration, price)
- Define available working hours / time slots
- View all upcoming bookings
- Confirm or cancel any booking
- View a daily/weekly schedule overview

---

## Non-Goals (Out of Scope for v1.0)
- Payment processing or invoicing
- Customer reviews or ratings
- Multi-branch or multi-staff support
- SMS/WhatsApp notifications
- Mobile app (iOS/Android)

---

## Success Metrics
| Metric                     | Target                           |
|----------------------------|----------------------------------|
| Booking completion rate    | > 80% of started bookings finish |
| Admin task time            | Booking management < 5 min/day   |
| Email confirmation delivery | 100% on booking                  |
| Page load time             | < 2 seconds                      |

---

## Assumptions
- The business has a single location and a single admin
- All services have fixed durations (no variable-length appointments)
- Users have access to email for confirmation

## Constraints
- Solo developer — scope must remain achievable
- No budget for paid APIs or hosting (free tiers only)
- Must be completed within the course timeline
