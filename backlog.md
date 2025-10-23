# 🧹 SpruceUp Product Backlog

## Overview
SpruceUp is a two-sided marketplace connecting homeowners with vetted local cleaners.  
This backlog outlines the **Epics**, **User Stories**, and **Acceptance Criteria** needed to launch and grow the platform.

---

## 🧩 Epic 1: User Onboarding & Authentication

### Goal
Allow customers and cleaners to easily create accounts, verify their identity, and log in securely.

---

### **User Story 1.1 — Sign Up / Login**
**As a** user,  
**I want** to create an account using my email or social login,  
**So that** I can access my SpruceUp dashboard.

**Acceptance Criteria**
- Users can register using email, Google, or Apple ID.  
- Passwords are encrypted (bcrypt).  
- Invalid credentials trigger error messages.  
- Successful login redirects to the correct dashboard (cleaner or customer).  

**Priority:** ⭐⭐⭐⭐ (High)

---

### **User Story 1.2 — Profile Setup**
**As a** new user,  
**I want** to create a personal profile,  
**So that** others can see my name, photo, and contact details.

**Acceptance Criteria**
- Cleaners and customers complete separate onboarding flows.  
- Cleaners upload a profile photo, description, and location radius.  
- Customers enter their home address and contact number.  
- Profiles can be edited at any time.

**Priority:** ⭐⭐⭐ (Medium)

---

### **User Story 1.3 — Identity Verification (Cleaners Only)**
**As a** cleaner,  
**I want** to verify my identity with a government ID and background check,  
**So that** customers trust me.

**Acceptance Criteria**
- Cleaners upload a valid ID.  
- The system tracks verification status (pending/approved/rejected).  
- Admin receives an alert when new verification requests are submitted.

**Priority:** ⭐⭐⭐⭐ (High)

---

## 🧽 Epic 2: Service Discovery & Search

### Goal
Enable customers to easily find nearby cleaners who fit their schedule, preferences, and budget.

---

### **User Story 2.1 — Location-Based Search**
**As a** customer,  
**I want** to find cleaners near my address,  
**So that** I can book someone local and available.

**Acceptance Criteria**
- Users can enter their address or enable GPS.  
- Cleaners displayed within defined service radius.  
- Results show cleaner name, rating, hourly rate, and availability.  
- Search filters: price range, rating, distance, services offered.

**Priority:** ⭐⭐⭐⭐ (High)

---

### **User Story 2.2 — View Cleaner Profile**
**As a** customer,  
**I want** to view a cleaner’s full profile,  
**So that** I can make an informed choice.

**Acceptance Criteria**
- Profiles show bio, service types, pricing, photos, and reviews.  
- "Book Now" button initiates booking flow.  
- Average rating displayed from verified reviews.  

**Priority:** ⭐⭐⭐⭐ (High)

---

## 🧹 Epic 3: Booking System

### Goal
Allow customers to book, reschedule, and cancel cleanings while enabling cleaners to manage their schedules.

---

### **User Story 3.1 — Create Booking**
**As a** customer,  
**I want** to select a service, time, and cleaner,  
**So that** I can confirm a booking.

**Acceptance Criteria**
- Booking form includes date, time, duration, and notes.  
- Availability automatically checked before confirmation.  
- Customer receives email & in-app confirmation.  
- Cleaner receives a notification to accept/reject.

**Priority:** ⭐⭐⭐⭐⭐ (Critical)

---

### **User Story 3.2 — Manage Booking Requests (Cleaner)**
**As a** cleaner,  
**I want** to view new booking requests,  
**So that** I can accept or decline jobs based on my schedule.

**Acceptance Criteria**
- Cleaner sees pending requests on dashboard.  
- Status changes to “accepted” or “declined.”  
- Customers notified of updates in real time.  

**Priority:** ⭐⭐⭐⭐ (High)

---

### **User Story 3.3 — Modify / Cancel Booking**
**As a** user,  
**I want** to cancel or reschedule my booking,  
**So that** I can adjust plans if necessary.

**Acceptance Criteria**
- Cancellation before start time allowed with refund policy.  
- Both users notified instantly.  
- Rescheduling updates cleaner availability automatically.  

**Priority:** ⭐⭐⭐ (Medium)

---

### **User Story 3.4 — Real-Time Booking Updates**
**As a** customer,  
**I want** to track my cleaner’s progress,  
**So that** I know when they’ll arrive and when cleaning begins.

**Acceptance Criteria**
- “En Route” and “In Progress” statuses visible.  
- Live location tracking optional (via Google Maps API).  
- Push notifications update both users.  

**Priority:** ⭐⭐⭐ (Medium)

---

## 💳 Epic 4: Payments & Billing

### Goal
Provide seamless, secure payment handling with automatic payouts to cleaners.

---

### **User Story 4.1 — Payment Processing**
**As a** customer,  
**I want** to pay securely within the app,  
**So that** I don’t have to handle cash.

**Acceptance Criteria**
- Payments handled via Stripe.  
- Supports cards, Apple Pay, Google Pay.  
- Receipts emailed post-payment.  
- Cleaner payout automatically triggered upon job completion.  

**Priority:** ⭐⭐⭐⭐⭐ (Critical)

---

### **User Story 4.2 — Refunds and Disputes**
**As a** customer,  
**I want** to request a refund if a service was unsatisfactory,  
**So that** I feel protected.

**Acceptance Criteria**
- Admin panel for refund requests.  
- Refund status tracked per booking.  
- Automatic updates to customer wallet or card.  

**Priority:** ⭐⭐⭐ (Medium)

---

### **User Story 4.3 — Cleaner Earnings Dashboard**
**As a** cleaner,  
**I want** to track my earnings and payouts,  
**So that** I know how much I’ve earned.

**Acceptance Criteria**
- Dashboard shows total earnings, pending payouts, and history.  
- Downloadable CSV reports.  
- Tax and fee breakdown included.  

**Priority:** ⭐⭐⭐⭐ (High)

---

## 💬 Epic 5: Communication & Notifications

### Goal
Allow smooth communication between cleaners and customers with real-time updates.

---

### **User Story 5.1 — In-App Messaging**
**As a** user,  
**I want** to message the other party,  
**So that** I can coordinate details easily.

**Acceptance Criteria**
- Secure chat using WebSocket or Firebase.  
- Messages tied to booking ID.  
- Unread message count badge shown on dashboard.  

**Priority:** ⭐⭐⭐⭐ (High)

---

### **User Story 5.2 — Notifications**
**As a** user,  
**I want** to receive updates on bookings, payments, and messages,  
**So that** I never miss an important update.

**Acceptance Criteria**
- Push and email notifications for major events.  
- Notification types: booking, payment, review, system alerts.  
- Users can toggle notification preferences.  

**Priority:** ⭐⭐⭐⭐ (High)

---

## ⭐ Epic 6: Ratings, Reviews & Trust

### Goal
Foster transparency and accountability through post-cleaning feedback.

---

### **User Story 6.1 — Leave a Review**
**As a** customer,  
**I want** to rate and review my cleaner,  
**So that** others can make better choices.

**Acceptance Criteria**
- Ratings from 1 to 5 stars.  
- Optional text review.  
- Reviews only available after “completed” booking.  

**Priority:** ⭐⭐⭐⭐ (High)

---

### **User Story 6.2 — View Reviews**
**As a** customer,  
**I want** to read reviews left by other users,  
**So that** I can gauge a cleaner’s quality.

**Acceptance Criteria**
- Display average rating and total number of reviews.  
- Sort by most recent, highest, or lowest.  

**Priority:** ⭐⭐⭐ (Medium)

---

## ⚙️ Epic 7: Admin Panel

### Goal
Provide internal tools for managing users, disputes, and system health.

---

### **User Story 7.1 — User Management**
**As an** admin,  
**I want** to view, suspend, or verify user accounts,  
**So that** I can maintain platform integrity.

**Acceptance Criteria**
- View all users and their roles.  
- Suspend/unverify accounts.  
- Filter by active/inactive.  

**Priority:** ⭐⭐⭐⭐ (High)

---

### **User Story 7.2 — Booking Oversight**
**As an** admin,  
**I want** to monitor bookings and disputes,  
**So that** I can resolve issues quickly.

**Acceptance Criteria**
- Admin dashboard with booking status filters.  
- Escalation tools for refunds or misconduct.  

**Priority:** ⭐⭐⭐⭐ (High)

---

## 🧠 Epic 8: Future Enhancements

### Goal
Prepare SpruceUp for future growth, intelligence, and premium offerings.

---

### **User Story 8.1 — AI Cleaner Recommendation**
**As a** customer,  
**I want** the app to recommend the best cleaner for me,  
**So that** I can find high-quality matches faster.

**Acceptance Criteria**
- Recommendation engine based on location, reviews, and price.  
- Shown as “Best Match” badge in search results.  

**Priority:** ⭐⭐ (Low / Future Phase)

---

### **User Story 8.2 — Subscription Plans**
**As a** customer,  
**I want** to book recurring cleanings automatically,  
**So that** I don’t need to rebook manually each week.

**Acceptance Criteria**
- Weekly/biweekly/monthly recurring bookings.  
- Auto-billing setup via Stripe.  
- Pause or cancel subscription anytime.  

**Priority:** ⭐⭐ (Low / Future Phase)

---

### **User Story 8.3 — Loyalty & Referral Program**
**As a** user,  
**I want** to earn rewards or credits,  
**So that** I’m encouraged to use SpruceUp regularly.

**Acceptance Criteria**
- Referral codes generate discounts.  
- Loyalty points for repeat bookings.  
- Redeemable credits via payment system.  

**Priority:** ⭐⭐ (Low / Future Phase)

---

# ✅ Summary

| Epic | Description | Priority |
|------|--------------|-----------|
| User Onboarding & Auth | Account creation, login, verification | ⭐⭐⭐⭐ |
| Service Discovery | Search, filtering, cleaner profiles | ⭐⭐⭐⭐ |
| Booking System | Scheduling, cancellation, tracking | ⭐⭐⭐⭐⭐ |
| Payments | Secure transactions, payouts, refunds | ⭐⭐⭐⭐⭐ |
| Communication | Chat, notifications | ⭐⭐⭐⭐ |
| Ratings & Reviews | Trust system | ⭐⭐⭐⭐ |
| Admin Panel | Internal control tools | ⭐⭐⭐⭐ |
| Future Enhancements | Subscriptions, AI, loyalty | ⭐⭐ |

---
