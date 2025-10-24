# 🧹 SpruceUp Sprint Plan (Windsurf Single-Agent Implementation)

## Overview
SpruceUp is a two-sided cleaning marketplace built to connect homeowners with local, verified cleaners.  
This sprint plan assumes **one Windsurf agent** operating as both **developer** and **QA**, using the previously defined PRD, data model, and backlog.

---

## 🧭 Project Setup & Technical Context

- **Stack:** React Native (Expo) + Node.js (Express/FastAPI alternative)  
- **Database:** PostgreSQL  
- **Auth:** JWT + bcrypt  
- **Hosting:** AWS / Vercel  
- **Payments:** Stripe SDK  
- **Mapping:** Google Maps API  
- **Build Environment:** Windsurf single-agent mode, with iterative code refinement and in-context memory enabled.

---

## 🏁 Sprint 0 – Environment & Scaffolding (Week 0)

**Goal:** Set up the foundational architecture, environments, and CI/CD pipeline.

### Tasks
- [ ] Initialize monorepo: `/frontend`, `/backend`, `/database`.  
- [ ] Configure environment variables (DB, Stripe, Google Maps).  
- [ ] Set up PostgreSQL schema using Prisma or SQLAlchemy based on data model.  
- [ ] Initialize GitHub repo connected to Windsurf project workspace.  
- [ ] Configure automated testing (Jest or Pytest).  
- [ ] Deploy base “Hello World” app to verify build pipeline.

### Acceptance Criteria
- ✅ Backend & frontend servers run independently.  
- ✅ CI/CD pipeline passes basic build test.  
- ✅ Database migrations run successfully.  

### Deliverables
- `/backend/app.py` or `/backend/server.js` scaffolded.  
- `/frontend/App.tsx` base layout ready.  
- `.env` and deployment scripts committed.

---

## 🧩 Sprint 1 – Authentication & User Onboarding (Week 1–2)

**Goal:** Allow users to register, log in, and set up initial profiles.

### Tasks
- [ ] Implement JWT-based authentication (signup/login/logout).  
- [ ] Create `users` and `profiles` tables per data model.  
- [ ] Build onboarding UI for both roles (customer / cleaner).  
- [ ] Integrate profile photo upload (AWS S3 / Firebase).  
- [ ] Add basic validation and error handling.  

### Windsurf Prompts
- “Generate signup and login flows with JWT auth and bcrypt password hashing.”  
- “Create React Native forms for cleaner and customer onboarding.”  
- “Implement backend endpoints for POST /signup, POST /login, GET /profile.”  

### Acceptance Criteria
- ✅ Users can create accounts and log in.  
- ✅ Profile setup flow completes without errors.  
- ✅ Basic role routing works (customer → booking dashboard, cleaner → jobs dashboard).  

### Deliverables
- `POST /signup`, `POST /login`, `GET /profile` routes live.  
- Onboarding screens functional in the mobile app.

---

## 🧽 Sprint 2 – Service Discovery & Cleaner Profiles (Week 3)

**Goal:** Enable customers to search for cleaners nearby and view their profiles.

### Tasks
- [ ] Implement `services` table and API.  
- [ ] Integrate Google Maps API for location-based cleaner search.  
- [ ] Build search filters (rating, distance, price).  
- [ ] Create cleaner profile page UI with rating, pricing, and “Book Now” button.  
- [ ] Add dummy data seeding for test accounts.  

### Windsurf Prompts
- “Build REST endpoint GET /cleaners?lat=&lng=&radius= for location-based search.”  
- “Create React Native list and profile view components for cleaners.”  

### Acceptance Criteria
- ✅ Customers can view nearby cleaners.  
- ✅ Cleaner profiles display complete information.  
- ✅ Search filters operate correctly.  

### Deliverables
- Functional search page with mock data.  
- Cleaner profile screen integrated.

---

## 🧹 Sprint 3 – Booking & Scheduling System (Week 4–5)

**Goal:** Implement booking lifecycle between customers and cleaners.

### Tasks
- [ ] Create `bookings` table with relationships (customer_id, cleaner_id, service_id).  
- [ ] Build booking form (service type, date/time, notes).  
- [ ] Implement cleaner-side booking approval flow.  
- [ ] Enable cancellation and rescheduling.  
- [ ] Add booking status tracking (“pending”, “accepted”, “in_progress”, “completed”).  

### Windsurf Prompts
- “Generate backend routes for bookings: POST /bookings, PATCH /bookings/:id/status.”  
- “Create React Native calendar view for cleaner schedule management.”  

### Acceptance Criteria
- ✅ Users can request and confirm bookings.  
- ✅ Cleaners can accept or reject requests.  
- ✅ Status transitions update both users’ dashboards.  

### Deliverables
- Bookings fully functional end-to-end.  
- Notifications triggered via simple webhook or polling.

---

## 💳 Sprint 4 – Payments Integration (Week 6)

**Goal:** Enable secure in-app payments and automated payouts.

### Tasks
- [ ] Set up Stripe integration (customer payments, cleaner payouts).  
- [ ] Build payment confirmation screen.  
- [ ] Add refund/dispute logic in admin layer.  
- [ ] Link booking total to payment amount dynamically.  

### Windsurf Prompts
- “Integrate Stripe Checkout for bookings with dynamic pricing from backend.”  
- “Implement payout webhook for cleaner accounts.”  

### Acceptance Criteria
- ✅ Customer can pay via card or mobile wallet.  
- ✅ Cleaner receives payout upon completion.  
- ✅ Payment records stored in `payments` table.  

### Deliverables
- Fully functional Stripe flow (sandbox).  
- Payment logs visible in admin dashboard.

---

## 💬 Sprint 5 – Messaging & Notifications (Week 7)

**Goal:** Implement real-time chat and event notifications.

### Tasks
- [ ] Create `messages` table with sender_id, receiver_id, booking_id.  
- [ ] Use WebSockets or Firebase Realtime Database for chat.  
- [ ] Add push notifications for booking updates and payments.  
- [ ] Build simple notifications list view in app.  

### Windsurf Prompts
- “Generate WebSocket server for chat tied to booking_id.”  
- “Implement push notifications for booking status changes using Expo Notifications.”  

### Acceptance Criteria
- ✅ Real-time chat works between users.  
- ✅ Notifications trigger on booking updates and payments.  
- ✅ Messages persist to DB and reload on refresh.  

### Deliverables
- Chat UI and backend live.  
- Notifications panel functional.

---

## ⭐ Sprint 6 – Ratings, Reviews & Trust (Week 8)

**Goal:** Build customer feedback and reputation system.

### Tasks
- [ ] Implement `reviews` table with booking_id, rating, comment.  
- [ ] Add rating input modal post-cleaning.  
- [ ] Update cleaner profile with average rating.  
- [ ] Moderate offensive content in admin panel.  

### Windsurf Prompts
- “Create POST /reviews endpoint and frontend review submission modal.”  
- “Calculate average cleaner rating dynamically and cache in profile.”  

### Acceptance Criteria
- ✅ Customers can rate completed bookings.  
- ✅ Cleaners’ ratings update automatically.  
- ✅ Review data appears in search and profile screens.  

### Deliverables
- Ratings and reviews flow fully integrated.

---

## ⚙️ Sprint 7 – Admin Dashboard & QA (Week 9)

**Goal:** Provide administrative oversight tools and finalize MVP stability.

### Tasks
- [ ] Build web-based admin panel (Next.js or simple React).  
- [ ] Manage users, bookings, and disputes.  
- [ ] Monitor transactions and cleaner verification.  
- [ ] Conduct QA and load testing.  
- [ ] Prepare documentation for MVP release.  

### Windsurf Prompts
- “Generate simple admin dashboard with user/booking/payment lists.”  
- “Run integration tests across all major flows.”  

### Acceptance Criteria
- ✅ Admin can verify, suspend, and review users.  
- ✅ System stable under simulated traffic.  
- ✅ All core flows tested and documented.  

### Deliverables
- MVP ready for beta release.  
- Docs and test scripts available in `/docs`.

---

## 🚀 Sprint 8 – MVP Launch & Feedback Loop (Week 10)

**Goal:** Launch SpruceUp MVP to pilot users and collect feedback.

### Tasks
- [ ] Deploy backend and mobile app to production environment.  
- [ ] Create onboarding email templates and notification flows.  
- [ ] Launch beta with test users in one metro area.  
- [ ] Capture analytics (Mixpanel / Firebase).  
- [ ] Collect user feedback for Sprint 9+ improvements.  

### Acceptance Criteria
- ✅ App live and functional in production.  
- ✅ Payment and booking flow verified in real-world test.  
- ✅ Analytics tracking user retention and engagement.  

### Deliverables
- Live MVP accessible to real users.  
- Feedback summarized in product report.

---

## 🧠 Future Sprints (Beyond MVP)

| Sprint | Goal | Key Features |
|--------|------|---------------|
| Sprint 9 | Subscriptions | Recurring bookings & auto billing |
| Sprint 10 | AI Recommendations | Personalized cleaner matching |
| Sprint 11 | Loyalty & Referrals | Rewards, credits, and retention |
| Sprint 12 | Smart Integrations | Alexa/Google Home voice commands |

---

## 🧾 Summary Timeline

| Sprint | Duration | Focus | Deliverable |
|---------|-----------|--------|--------------|
| 0 | Week 0 | Setup & scaffolding | Infra ready |
| 1 | Week 1–2 | Auth & Onboarding | Login + Profile |
| 2 | Week 3 | Discovery & Search | Cleaner listing |
| 3 | Week 4–5 | Booking System | Core workflow |
| 4 | Week 6 | Payments | Stripe integration |
| 5 | Week 7 | Messaging | Real-time chat |
| 6 | Week 8 | Reviews | Rating engine |
| 7 | Week 9 | Admin + QA | Stable MVP |
| 8 | Week 10 | Launch | Production release |

---

## 🧰 Agent Setup in Windsurf

**Agent Role:** `SpruceUp_Builder`  
**Goal:** Build and maintain the SpruceUp MVP autonomously through iterative development loops.  

**Agent Responsibilities:**
- Generate code for each sprint milestone.  
- Run integration tests and self-debug.  
- Commit versioned changes to repo.  
- Write test documentation per sprint.

**Prompt Template:**
