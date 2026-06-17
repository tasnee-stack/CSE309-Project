# 22 - API Design

## Overview
BookEase uses a RESTful API built with Express.js.

- **Base URL:** `https://your-api.render.com/api`
- **Format:** JSON
- **Authentication:** `Authorization: Bearer <JWT_TOKEN>` on protected routes

---

## Auth Routes `/api/auth`

### POST `/api/auth/register`
Register a new user account.

**Request Body:**
```json
{
  "name": "Tanvir Ahmed",
  "email": "tanvir@example.com",
  "password": "password123"
}
```
**Response (201):**
```json
{
  "success": true,
  "token": "eyJhbGci...",
  "user": { "_id": "...", "name": "Tanvir Ahmed", "role": "customer" }
}
```

---

### POST `/api/auth/login`
Login with email and password.

**Request Body:**
```json
{
  "email": "tanvir@example.com",
  "password": "password123"
}
```
**Response (200):**
```json
{
  "success": true,
  "token": "eyJhbGci...",
  "user": { "_id": "...", "name": "Tanvir Ahmed", "role": "customer" }
}
```

---

## Service Routes `/api/services`

### GET `/api/services`
Get all active services. *(Public)*

**Response (200):**
```json
[
  { "_id": "...", "name": "Haircut", "duration": 30, "price": 500 }
]
```

---

### POST `/api/services`
Create a new service. *(Admin only)*

**Headers:** `Authorization: Bearer <token>`
**Request Body:**
```json
{
  "name": "Beard Trim",
  "description": "Full beard styling",
  "duration": 20,
  "price": 200
}
```
**Response (201):** Created service object

---

### PUT `/api/services/:id`
Update an existing service. *(Admin only)*

---

### DELETE `/api/services/:id`
Delete a service. *(Admin only)*

---

## Time Slot Routes `/api/slots`

### GET `/api/slots?serviceId=&date=`
Get available time slots for a service on a given date. *(Customer)*

**Query Params:** `serviceId`, `date` (YYYY-MM-DD)

**Response (200):**
```json
[
  { "_id": "...", "startTime": "10:00", "endTime": "10:30", "isBooked": false },
  { "_id": "...", "startTime": "10:30", "endTime": "11:00", "isBooked": true }
]
```

---

### POST `/api/slots`
Create time slots for a date range. *(Admin only)*

**Request Body:**
```json
{
  "serviceId": "...",
  "date": "2024-06-20",
  "startHour": "09:00",
  "endHour": "17:00"
}
```

---

## Booking Routes `/api/bookings`

### POST `/api/bookings`
Book an appointment. *(Customer, auth required)*

**Request Body:**
```json
{
  "serviceId": "...",
  "timeSlotId": "..."
}
```
**Response (201):**
```json
{
  "success": true,
  "booking": { "_id": "...", "status": "confirmed", ... }
}
```

---

### GET `/api/bookings/my`
Get logged-in customer's bookings. *(Customer, auth required)*

**Response (200):** Array of booking objects (populated with service and slot data)

---

### GET `/api/bookings`
Get ALL bookings. *(Admin only)*

**Query Params (optional):** `date`, `status`

---

### PATCH `/api/bookings/:id/cancel`
Cancel a booking. *(Customer or Admin, auth required)*

**Response (200):**
```json
{ "success": true, "message": "Booking cancelled successfully" }
```

---

## Error Response Format
All errors return:
```json
{
  "success": false,
  "message": "Descriptive error message"
}
```

Common HTTP status codes:
| Code | Meaning                     |
|------|-----------------------------|
| 200  | Success                     |
| 201  | Created                     |
| 400  | Bad request / validation    |
| 401  | Unauthorized (no/bad token) |
| 403  | Forbidden (wrong role)      |
| 404  | Resource not found          |
| 409  | Conflict (slot already booked) |
| 500  | Internal server error       |
