# 16 - Data Flow Diagram (DFD)

## What is a DFD?
A Data Flow Diagram (DFD) visually represents how data moves through the system — from inputs to processes to outputs and data storage.

---

## Level 0 DFD – Context Diagram

The Context Diagram shows the system as a single process and its interactions with external entities.

```
                        ┌──────────────────────────┐
                        │                          │
  [Customer] ──────────►│      BookEase System     │──────────► [Customer]
             ◄──────────│                          │
                        │   (Online Booking &      │
  [Admin]    ──────────►│   Reservation Platform)  │──────────► [Admin]
             ◄──────────│                          │
                        │                          │──────────► [Email Service]
                        └──────────────────────────┘
```

**External Entities:**
- **Customer** – Registers, logs in, books/cancels appointments
- **Admin** – Manages services, slots, and bookings
- **Email Service** – Receives notification requests (e.g. Nodemailer + Gmail)

---

## Level 1 DFD – Main Processes

Breaks the system into its core functional processes.

```
Customer ──► [1.0 User Authentication] ──► User DB
              │
              ▼
Customer ──► [2.0 Browse Services] ◄──► Services DB
              │
              ▼
Customer ──► [3.0 Book Appointment] ──► Bookings DB
              │                           │
              │                           ▼
              │                    [4.0 Send Email] ──► Email Service
              │
Admin    ──► [5.0 Manage Services] ──► Services DB
Admin    ──► [6.0 Manage Bookings] ──► Bookings DB
Admin    ──► [7.0 View Dashboard]  ◄── Bookings DB
```

---

## Level 2 DFD – Booking Process (Expanded)

Zooms in on Process 3.0 (Book Appointment).

```
Customer
   │
   ▼
[3.1 Select Service] ──► Read Services DB
   │
   ▼
[3.2 Select Date & Time Slot] ──► Read Availability DB
   │
   ▼
[3.3 Validate Slot Availability]
   │
   ├── Slot Available ──► [3.4 Save Booking] ──► Write Bookings DB
   │                              │
   │                              ▼
   │                      [3.5 Trigger Email] ──► Email Service
   │
   └── Slot Taken ──► [3.6 Return Error] ──► Customer
```

---

## Data Stores Summary

| Data Store        | Description                                         |
|-------------------|-----------------------------------------------------|
| User DB           | Stores user accounts (name, email, hashed password, role) |
| Services DB       | Stores services (name, description, duration, price) |
| Availability DB   | Stores time slots (date, time, service, status)     |
| Bookings DB       | Stores booking records (user, service, slot, status) |
