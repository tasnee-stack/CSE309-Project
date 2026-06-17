# 18 - Entity Relationship Diagram (ERD)

## Overview
The BookEase system uses MongoDB (a NoSQL document database), but we model the data relationships using ERD concepts for clarity.

---

## Entities & Attributes

### User
| Field       | Type     | Description                     |
|-------------|----------|---------------------------------|
| _id         | ObjectId | Primary key (auto-generated)    |
| name        | String   | Full name of the user           |
| email       | String   | Unique email address            |
| password    | String   | Hashed password                 |
| role        | String   | "customer" or "admin"           |
| createdAt   | Date     | Account creation timestamp      |

### Service
| Field       | Type     | Description                     |
|-------------|----------|---------------------------------|
| _id         | ObjectId | Primary key                     |
| name        | String   | Service name (e.g. "Haircut")   |
| description | String   | Short description                |
| duration    | Number   | Duration in minutes              |
| price       | Number   | Price in BDT/USD                |
| isActive    | Boolean  | Whether service is available     |
| createdAt   | Date     | Creation timestamp               |

### TimeSlot
| Field       | Type     | Description                      |
|-------------|----------|----------------------------------|
| _id         | ObjectId | Primary key                      |
| service     | ObjectId | Reference to Service             |
| date        | Date     | Date of the slot                  |
| startTime   | String   | Start time (e.g. "10:00")        |
| endTime     | String   | End time (e.g. "10:30")          |
| isBooked    | Boolean  | Whether this slot is taken        |
| createdAt   | Date     | Creation timestamp                |

### Booking
| Field       | Type     | Description                      |
|-------------|----------|----------------------------------|
| _id         | ObjectId | Primary key                      |
| customer    | ObjectId | Reference to User (customer)     |
| service     | ObjectId | Reference to Service             |
| timeSlot    | ObjectId | Reference to TimeSlot            |
| status      | String   | "confirmed", "cancelled"         |
| createdAt   | Date     | Booking creation timestamp       |

---

## Relationships

```
User (Customer) ──────────< Booking >────────── TimeSlot
                                │
                                │
                            Service
                                │
                                │
                          TimeSlot (generated per service)
```

- One **User** (Customer) can have many **Bookings**
- One **Booking** belongs to one **Service**
- One **Booking** references one **TimeSlot**
- One **Service** has many **TimeSlots**
- One **TimeSlot** can have at most one **Booking** (enforced by `isBooked`)

---

## ERD (Text Representation)

```
┌──────────────┐         ┌──────────────────┐         ┌──────────────┐
│     USER     │         │     BOOKING       │         │   TIMESLOT   │
│──────────────│         │──────────────────│         │──────────────│
│ _id (PK)     │ 1     N │ _id (PK)         │ N     1 │ _id (PK)     │
│ name         ├─────────┤ customer (FK)    ├─────────┤ service (FK) │
│ email        │         │ service (FK)     │         │ date         │
│ password     │         │ timeSlot (FK)    │         │ startTime    │
│ role         │         │ status           │         │ endTime      │
│ createdAt    │         │ createdAt        │         │ isBooked     │
└──────────────┘         └────────┬─────────┘         └──────────────┘
                                  │ N                        
                                  │ 1                        
                          ┌───────▼──────┐
                          │   SERVICE    │
                          │──────────────│
                          │ _id (PK)     │
                          │ name         │
                          │ description  │
                          │ duration     │
                          │ price        │
                          │ isActive     │
                          └──────────────┘
```
