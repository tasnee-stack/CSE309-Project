# 21 - Database Design

## Database System
**MongoDB** (NoSQL Document Database), hosted on **MongoDB Atlas** (free tier)
**ORM/ODM:** Mongoose

---

## Collections

### 1. `users` Collection

```javascript
// models/User.js
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    trim: true
  },
  email: {
    type: String,
    required: true,
    unique: true,
    lowercase: true
  },
  password: {
    type: String,
    required: true,
    minlength: 8
  },
  role: {
    type: String,
    enum: ['customer', 'admin'],
    default: 'customer'
  }
}, { timestamps: true });
```

**Sample Document:**
```json
{
  "_id": "64a1f...",
  "name": "Tanvir Ahmed",
  "email": "tanvir@example.com",
  "password": "$2b$10$hashed...",
  "role": "customer",
  "createdAt": "2024-06-01T10:00:00Z"
}
```

---

### 2. `services` Collection

```javascript
// models/Service.js
const serviceSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  description: {
    type: String,
    default: ''
  },
  duration: {
    type: Number,       // in minutes
    required: true
  },
  price: {
    type: Number,
    required: true,
    min: 0
  },
  isActive: {
    type: Boolean,
    default: true
  }
}, { timestamps: true });
```

**Sample Document:**
```json
{
  "_id": "64b2c...",
  "name": "Haircut",
  "description": "Standard haircut with wash",
  "duration": 30,
  "price": 500,
  "isActive": true
}
```

---

### 3. `timeslots` Collection

```javascript
// models/TimeSlot.js
const timeSlotSchema = new mongoose.Schema({
  service: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Service',
    required: true
  },
  date: {
    type: Date,
    required: true
  },
  startTime: {
    type: String,    // e.g. "10:00"
    required: true
  },
  endTime: {
    type: String,    // e.g. "10:30"
    required: true
  },
  isBooked: {
    type: Boolean,
    default: false
  }
}, { timestamps: true });
```

**Sample Document:**
```json
{
  "_id": "64c3d...",
  "service": "64b2c...",
  "date": "2024-06-15T00:00:00Z",
  "startTime": "10:00",
  "endTime": "10:30",
  "isBooked": false
}
```

---

### 4. `bookings` Collection

```javascript
// models/Booking.js
const bookingSchema = new mongoose.Schema({
  customer: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  service: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Service',
    required: true
  },
  timeSlot: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'TimeSlot',
    required: true
  },
  status: {
    type: String,
    enum: ['confirmed', 'cancelled'],
    default: 'confirmed'
  }
}, { timestamps: true });
```

**Sample Document:**
```json
{
  "_id": "64d4e...",
  "customer": "64a1f...",
  "service": "64b2c...",
  "timeSlot": "64c3d...",
  "status": "confirmed",
  "createdAt": "2024-06-10T09:15:00Z"
}
```

---

## Indexing Strategy

| Collection  | Field    | Index Type | Reason                          |
|-------------|----------|------------|---------------------------------|
| users       | email    | Unique     | Fast lookup, prevent duplicates |
| timeslots   | date     | Regular    | Fast date-based queries         |
| timeslots   | isBooked | Regular    | Quick slot availability filter  |
| bookings    | customer | Regular    | Fast "My Bookings" queries      |
