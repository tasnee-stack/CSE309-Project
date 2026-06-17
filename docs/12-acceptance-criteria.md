# 12 - Acceptance Criteria

## What is Acceptance Criteria?
Acceptance criteria define the specific conditions that must be true for a user story to be considered complete and working correctly.

---

## US-01: Customer Registration

**Given** I am a new visitor on the site  
**When** I fill in a valid name, email, and password and click "Register"  
**Then** my account is created and I am redirected to the service listing page

**Additional conditions:**
- Email must be unique (duplicate email shows error: "Email already in use")
- Password must be at least 8 characters
- All fields are required; empty fields show inline validation messages

---

## US-02: Customer Login

**Given** I have a registered account  
**When** I enter my correct email and password and click "Login"  
**Then** I am logged in and redirected to my dashboard

**Additional conditions:**
- Incorrect credentials show: "Invalid email or password"
- Logged-in session persists across page refreshes (JWT stored in localStorage)

---

## US-04: View Available Time Slots

**Given** I have selected a service  
**When** I choose a date on the calendar  
**Then** I see only the available (unbooked) time slots for that date

**Additional conditions:**
- Already-booked slots are shown as greyed-out/disabled
- Past dates are not selectable
- If no slots are available, message shows: "No available slots for this date"

---

## US-05: Book an Appointment

**Given** I have selected a service and a time slot  
**When** I click "Confirm Booking"  
**Then** the booking is saved and I am shown a success message

**Additional conditions:**
- System prevents booking the same slot twice (race condition protection)
- Booking appears immediately in "My Bookings"
- Confirmation email is sent within 60 seconds

---

## US-06: Email Confirmation

**Given** I have successfully booked an appointment  
**When** the booking is confirmed  
**Then** I receive an email with the service name, date, time, and a cancellation option

---

## US-08: Cancel a Booking

**Given** I have an upcoming booking  
**When** I click "Cancel" and confirm the prompt  
**Then** the booking is removed and the time slot becomes available again

**Additional conditions:**
- Cancellation only allowed for future bookings (past bookings cannot be cancelled)
- A cancellation confirmation email is sent to the customer

---

## US-11: Admin Adds a Service

**Given** I am logged in as an admin  
**When** I fill in service name, duration (in minutes), and price and click "Save"  
**Then** the new service appears on the public service listing immediately

**Additional conditions:**
- All fields (name, duration, price) are required
- Duration must be a positive number
- Price must be zero or positive

---

## US-14: Admin Views All Bookings

**Given** I am logged in as an admin  
**When** I visit the "Bookings" section of the dashboard  
**Then** I see a list of all bookings sorted by date, with customer name, service, date, and time

**Additional conditions:**
- Filter by date is available
- Booking status (Confirmed / Cancelled) is shown
