# 🧹 SpruceUp Data Model

## 1. Overview
The **SpruceUp Data Model** supports a marketplace that connects **homeowners** with **verified cleaners**.  
It enables scheduling, payments, communication, and ratings through a secure, modular system.

---

## 2. Entity Relationship Diagram (Conceptual Overview)

**Users**
⬇️  
**Profiles (Cleaner / Customer)**  
⬇️  
**Bookings** ← **Services**  
⬇️  
**Payments**, **Reviews**, **Messages**

---

## 3. Core Entities and Attributes

### 3.1 `users`
Stores authentication and basic user data for all platform participants.

| Field | Type | Description |
|-------|------|-------------|
| `user_id` | UUID (PK) | Unique identifier for each user |
| `email` | VARCHAR(255) | Unique user email |
| `password_hash` | VARCHAR(255) | Hashed password |
| `role` | ENUM('customer', 'cleaner', 'admin') | Defines access level |
| `is_verified` | BOOLEAN | Indicates if user identity/background is verified |
| `created_at` | TIMESTAMP | Account creation date |
| `updated_at` | TIMESTAMP | Last update timestamp |
| `last_login` | TIMESTAMP | Last login time |

---

### 3.2 `profiles`
Stores detailed profile data for both customers and cleaners.

| Field | Type | Description |
|-------|------|-------------|
| `profile_id` | UUID (PK) | Unique profile identifier |
| `user_id` | UUID (FK → users.user_id) | Link to base user record |
| `first_name` | VARCHAR(100) | User’s first name |
| `last_name` | VARCHAR(100) | User’s last name |
| `phone` | VARCHAR(20) | Contact number |
| `profile_photo_url` | TEXT | Profile image |
| `bio` | TEXT | User introduction |
| `address` | JSON | Structured address (street, city, zip, coordinates) |
| `rating` | DECIMAL(2,1) | Average rating (for cleaners) |
| `verified_badge` | BOOLEAN | True if background check complete |
| `service_radius_km` | INTEGER | Cleaner’s coverage area (only for cleaners) |
| `created_at` | TIMESTAMP | Profile creation date |
| `updated_at` | TIMESTAMP | Profile last updated |

---

### 3.3 `services`
Defines available cleaning service types and pricing metadata.

| Field | Type | Description |
|-------|------|-------------|
| `service_id` | UUID (PK) | Unique service identifier |
| `cleaner_id` | UUID (FK → users.user_id) | The cleaner offering this service |
| `title` | VARCHAR(255) | Service name (e.g., “Deep Clean”) |
| `description` | TEXT | Detailed explanation |
| `base_price` | DECIMAL(10,2) | Starting price |
| `hourly_rate` | DECIMAL(10,2) | Hourly rate (optional) |
| `duration_estimate_min` | INTEGER | Estimated duration in minutes |
| `available` | BOOLEAN | Whether the service is currently offered |
| `created_at` | TIMESTAMP | Date added |
| `updated_at` | TIMESTAMP | Date modified |

---

### 3.4 `bookings`
Links customers with cleaners and manages appointment lifecycle.

| Field | Type | Description |
|-------|------|-------------|
| `booking_id` | UUID (PK) | Unique booking identifier |
| `customer_id` | UUID (FK → users.user_id) | The booking customer |
| `cleaner_id` | UUID (FK → users.user_id) | Assigned cleaner |
| `service_id` | UUID (FK → services.service_id) | Service being booked |
| `status` | ENUM('pending', 'accepted', 'in_progress', 'completed', 'cancelled') | Booking state |
| `scheduled_start` | TIMESTAMP | Start time |
| `scheduled_end` | TIMESTAMP | End time |
| `address` | JSON | Service address |
| `notes` | TEXT | Additional instructions |
| `total_price` | DECIMAL(10,2) | Total booking cost |
| `payment_id` | UUID (FK → payments.payment_id) | Related payment record |
| `created_at` | TIMESTAMP | Booking creation |
| `updated_at` | TIMESTAMP | Booking updates |

---

### 3.5 `payments`
Handles payment transactions and statuses.

| Field | Type | Description |
|-------|------|-------------|
| `payment_id` | UUID (PK) | Unique payment record |
| `booking_id` | UUID (FK → bookings.booking_id) | Linked booking |
| `customer_id` | UUID (FK → users.user_id) | Paying customer |
| `cleaner_id` | UUID (FK → users.user_id) | Receiving cleaner |
| `amount` | DECIMAL(10,2) | Transaction amount |
| `payment_method` | ENUM('stripe', 'apple_pay', 'google_pay') | Payment channel |
| `status` | ENUM('pending', 'completed', 'failed', 'refunded') | Payment status |
| `transaction_ref` | VARCHAR(255) | External reference ID |
| `created_at` | TIMESTAMP | Payment creation date |

---

### 3.6 `reviews`
Captures user feedback and ratings for completed bookings.

| Field | Type | Description |
|-------|------|-------------|
| `review_id` | UUID (PK) | Unique review ID |
| `booking_id` | UUID (FK → bookings.booking_id) | Associated booking |
| `customer_id` | UUID (FK → users.user_id) | Reviewer |
| `cleaner_id` | UUID (FK → users.user_id) | Reviewed cleaner |
| `rating` | INTEGER (1–5) | Star rating |
| `comment` | TEXT | Feedback text |
| `created_at` | TIMESTAMP | Review date |

---

### 3.7 `messages`
Manages in-app communication between customers and cleaners.

| Field | Type | Description |
|-------|------|-------------|
| `message_id` | UUID (PK) | Unique message identifier |
| `sender_id` | UUID (FK → users.user_id) | Message sender |
| `receiver_id` | UUID (FK → users.user_id) | Message receiver |
| `booking_id` | UUID (FK → bookings.booking_id) | Optional context |
| `content` | TEXT | Message body |
| `timestamp` | TIMESTAMP | Time sent |
| `is_read` | BOOLEAN | Read/unread status |

---

### 3.8 `notifications`
Tracks alerts and updates for both user roles.

| Field | Type | Description |
|-------|------|-------------|
| `notification_id` | UUID (PK) | Unique notification record |
| `user_id` | UUID (FK → users.user_id) | Recipient |
| `type` | ENUM('booking_update', 'payment', 'review', 'system') | Notification type |
| `message` | TEXT | Notification text |
| `is_read` | BOOLEAN | Whether user has read it |
| `created_at` | TIMESTAMP | Sent timestamp |

---

## 4. Relationships Summary

- `users` ⟶ `profiles` (1:1)  
- `users` ⟶ `services` (1:N for cleaners)  
- `users` ⟶ `bookings` (1:N as customer or cleaner)  
- `bookings` ⟶ `payments` (1:1)  
- `bookings` ⟶ `reviews` (1:1)  
- `users` ⟶ `messages` (1:N as sender/receiver)  
- `users` ⟶ `notifications` (1:N)

---

## 5. Scalability & Extensions

- **Add-ons:** Future support for “Add Extra Tasks” (e.g., laundry, oven cleaning) in a `booking_addons` table.  
- **Subscription Plans:** Introduce a `subscriptions` table for recurring cleanings.  
- **Analytics:** Track activity with a `user_metrics` table (login frequency, churn, etc.).  
- **AI Matching:** Use a `recommendations` table to store machine learning-based cleaner suggestions.

---

## 6. Example Query: Retrieve Upcoming Bookings for a Customer

```sql
SELECT b.booking_id, s.title, c.first_name AS cleaner_name, b.scheduled_start, b.status
FROM bookings b
JOIN services s ON s.service_id = b.service_id
JOIN profiles c ON c.user_id = b.cleaner_id
WHERE b.customer_id = :customer_id
AND b.status IN ('pending', 'accepted', 'in_progress')
ORDER BY b.scheduled_start ASC;

7. Data Security

All passwords stored as bcrypt hashes.

JWT authentication with refresh tokens.

Encrypted messaging with TLS.

Data access restricted via role-based permissions (RBAC).
