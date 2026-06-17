# 19 - System Design

## Architecture Overview
BookEase follows a classic **3-tier web architecture**:

```
┌─────────────────────────────────────────────────────────┐
│                      Client Layer                        │
│              React.js SPA (Vercel)                       │
└───────────────────────────┬─────────────────────────────┘
                            │ HTTPS / REST API
┌───────────────────────────▼─────────────────────────────┐
│                    Application Layer                     │
│           Node.js + Express.js (Railway/Render)          │
│                                                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌────────┐  │
│  │  Auth    │  │ Services │  │  Slots   │  │Bookings│  │
│  │  Router  │  │  Router  │  │  Router  │  │ Router │  │
│  └──────────┘  └──────────┘  └──────────┘  └────────┘  │
│                                                          │
│  ┌──────────────────────────────────────────────────┐   │
│  │              Middleware Layer                    │   │
│  │  authMiddleware | roleCheck | errorHandler       │   │
│  └──────────────────────────────────────────────────┘   │
└───────────────────────────┬─────────────────────────────┘
                            │ Mongoose ODM
┌───────────────────────────▼─────────────────────────────┐
│                      Data Layer                          │
│              MongoDB Atlas (Free Tier)                   │
│     Collections: users, services, timeslots, bookings   │
└─────────────────────────────────────────────────────────┘
                            │
              ┌─────────────▼──────────────┐
              │     Email Service           │
              │  Nodemailer + Gmail SMTP    │
              └────────────────────────────┘
```

---

## Folder Structure

### Backend (Node.js + Express)
```
server/
├── config/
│   └── db.js               # MongoDB connection
├── controllers/
│   ├── authController.js
│   ├── serviceController.js
│   ├── slotController.js
│   └── bookingController.js
├── middleware/
│   ├── authMiddleware.js    # JWT verification
│   └── roleMiddleware.js    # Admin-only route guard
├── models/
│   ├── User.js
│   ├── Service.js
│   ├── TimeSlot.js
│   └── Booking.js
├── routes/
│   ├── authRoutes.js
│   ├── serviceRoutes.js
│   ├── slotRoutes.js
│   └── bookingRoutes.js
├── utils/
│   └── emailService.js      # Nodemailer setup
├── .env
└── server.js
```

### Frontend (React)
```
client/
├── public/
├── src/
│   ├── api/
│   │   └── axios.js         # Axios instance with base URL + token
│   ├── components/
│   │   ├── Navbar.jsx
│   │   ├── ServiceCard.jsx
│   │   ├── BookingForm.jsx
│   │   └── BookingList.jsx
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── Login.jsx
│   │   ├── Register.jsx
│   │   ├── Services.jsx
│   │   ├── BookAppointment.jsx
│   │   ├── MyBookings.jsx
│   │   └── admin/
│   │       ├── Dashboard.jsx
│   │       ├── ManageServices.jsx
│   │       └── ManageBookings.jsx
│   ├── context/
│   │   └── AuthContext.jsx  # Global auth state
│   ├── App.jsx
│   └── main.jsx
└── package.json
```

---

## Authentication Flow

```
1. User submits login form
2. POST /api/auth/login
3. Server verifies credentials
4. Server issues JWT (expires in 24h)
5. Client stores JWT in localStorage
6. All subsequent API calls include: Authorization: Bearer <token>
7. authMiddleware validates token on each protected request
```

---

## Deployment Plan

| Component | Platform       | Free Tier |
|-----------|----------------|-----------|
| Frontend  | Vercel         | Yes       |
| Backend   | Render/Railway | Yes       |
| Database  | MongoDB Atlas  | Yes       |
| Email     | Gmail SMTP     | Yes       |
