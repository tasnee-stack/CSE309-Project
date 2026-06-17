# 15 - Use Cases

## What is a Use Case?
A use case describes a specific interaction between a user (actor) and the system to achieve a goal.

---

## Actors
- **Customer** – A registered user who books appointments
- **Admin** – The business owner/manager who manages the system
- **System** – The BookEase application itself (automated actions)

---

## Use Case 1: Register Account

| Field          | Detail                                                      |
|----------------|-------------------------------------------------------------|
| **ID**         | UC-01                                                       |
| **Name**       | Register Account                                            |
| **Actor**      | Customer                                                    |
| **Precondition** | User is not logged in and does not have an account        |
| **Main Flow**  | 1. User navigates to the registration page                  |
|                | 2. User enters name, email, and password                    |
|                | 3. User clicks "Register"                                   |
|                | 4. System validates input (unique email, password length)   |
|                | 5. System creates account and redirects to dashboard        |
| **Alternative Flow** | If email already exists → System shows error message  |
| **Postcondition** | User has an active account and is logged in              |

---

## Use Case 2: Book an Appointment

| Field          | Detail                                                       |
|----------------|--------------------------------------------------------------|
| **ID**         | UC-02                                                        |
| **Name**       | Book an Appointment                                          |
| **Actor**      | Customer                                                     |
| **Precondition** | Customer is logged in                                      |
| **Main Flow**  | 1. Customer views the service listing                        |
|                | 2. Customer selects a service                                |
|                | 3. Customer selects a date from the calendar                 |
|                | 4. System displays available time slots                      |
|                | 5. Customer selects a time slot                              |
|                | 6. Customer clicks "Confirm Booking"                         |
|                | 7. System saves the booking and marks slot as unavailable    |
|                | 8. System sends confirmation email to customer               |
| **Alternative Flow** | If slot is taken → System shows error "Slot no longer available" |
| **Postcondition** | Booking is saved; customer receives email confirmation    |

---

## Use Case 3: Cancel a Booking

| Field          | Detail                                                       |
|----------------|--------------------------------------------------------------|
| **ID**         | UC-03                                                        |
| **Name**       | Cancel a Booking                                             |
| **Actor**      | Customer                                                     |
| **Precondition** | Customer is logged in and has an upcoming booking          |
| **Main Flow**  | 1. Customer visits "My Bookings"                             |
|                | 2. Customer selects an upcoming booking                      |
|                | 3. Customer clicks "Cancel Booking"                          |
|                | 4. System shows a confirmation prompt                        |
|                | 5. Customer confirms                                         |
|                | 6. System cancels booking and frees the slot                 |
|                | 7. System sends cancellation email                           |
| **Alternative Flow** | Customer cancels the prompt → No action taken        |
| **Postcondition** | Booking is cancelled; slot is available for others       |

---

## Use Case 4: Admin Manages Services

| Field          | Detail                                                       |
|----------------|--------------------------------------------------------------|
| **ID**         | UC-04                                                        |
| **Name**       | Manage Services                                              |
| **Actor**      | Admin                                                        |
| **Precondition** | Admin is logged in                                         |
| **Main Flow**  | 1. Admin navigates to "Services" in the dashboard            |
|                | 2. Admin clicks "Add Service"                                |
|                | 3. Admin fills in name, duration, price, description         |
|                | 4. Admin clicks "Save"                                       |
|                | 5. System saves and displays service in the public listing   |
| **Alternative Flow** | Admin edits or deletes an existing service            |
| **Postcondition** | Service is live and bookable by customers               |

---

## Use Case 5: Admin Cancels a Booking

| Field          | Detail                                                       |
|----------------|--------------------------------------------------------------|
| **ID**         | UC-05                                                        |
| **Name**       | Admin Cancels a Booking                                      |
| **Actor**      | Admin                                                        |
| **Precondition** | Admin is logged in; booking exists                         |
| **Main Flow**  | 1. Admin opens the Bookings list                             |
|                | 2. Admin finds the target booking                            |
|                | 3. Admin clicks "Cancel"                                     |
|                | 4. System cancels booking and notifies customer by email     |
| **Postcondition** | Booking is cancelled; slot is freed                      |
