# Creative Market BD - Graphic Design Marketplace

A modern, professional Graphic Design Marketplace Android application crafted for Bangladesh, enabling graphic designers to showcase portfolios, package design services in BDT (৳), and collaborate with clients through secure order placement, real-time messaging, revision tracking, and administrative governance.

## User Review & Critical Decisions

> [!IMPORTANT]
> The clarifying questions were completed with recommended marketplace defaults. Please review the confirmed architectural choices below:

- **Role Management & Testing**: Built-in interactive role switcher supporting seamless switching between **Client**, **Graphic Designer / Seller**, and **Platform Admin**, alongside individual credential login/registration so each role's dedicated dashboards, permissions, and workflows can be thoroughly explored.
- **Bilingual Interface (Bengali + English)**: Live language toggle (বাংলা / English) accessible from the top app bar and user profile, paired with localized typography (Hind Siliguri for Bengali, Poppins for English) and native Bangladeshi currency formatting (BDT ৳).
- **Payment Verification Flow**: Real-world Bangladeshi mobile financial service checkout (bKash, Nagad, Rocket) and direct bank transfer with merchant wallet instructions, copyable numbers, and mandatory Transaction ID (TrxID) submission verified through Admin/Designer order processing.
- **Architecture & Persistence**: Local reactive SQLite database powered by Room with pre-populated rich seed data (top Bangladeshi designers, 12 marketplace categories, packages, reviews, active orders, and chat threads) guaranteeing immediate, offline-capable usability and full end-to-end CRUD persistence.

---

## 1. Overview & Core Concept

**Creative Market BD** addresses the growing creative freelance economy in Bangladesh by offering a localized, high-trust digital marketplace. Clients can effortlessly discover vetted Bangladeshi graphic designers, compare tiered packages (Basic, Standard, Premium), place orders with project briefs, and communicate directly. Designers gain an intuitive mobile business suite to publish services, track milestone deliverables, request revisions, and monitor their BDT earnings.

### Key Personas
1. **Client / Buyer**: Small businesses, startups, content creators, and agencies in Bangladesh seeking logo design, social media banners, packaging, and UI/UX assets.
2. **Graphic Designer / Seller**: Freelance creative professionals creating packages, managing revisions, uploading design previews, and withdrawing earnings.
3. **Platform Admin**: System auditor managing designer verifications, disputes, categories, commission rates, and platform transactions.

---

## 2. User Experience & Visual Design

### Visual Identity & Theme Tokens
- **Primary Color**: Deep Navy Blue (`#0A192F` / `#0D2140`) — conveys institutional trust, premium craftsmanship, and authority.
- **Secondary Color**: Electric Blue (`#0066FF` / `#2575FC`) — dynamic visual accents, call-to-actions, and active tab highlights.
- **Background**: Soft Canvas Gray (`#F7F9FC`) with crisp pure white elevated cards (`#FFFFFF`).
- **Accent Color**: Creative Purple (`#7C3AED` / `#8B5CF6`) — highlights badges, verified tags, and premium package chips.
- **Text & Surface**: Dark Charcoal (`#1E293B`) for high contrast readability and Slate Gray (`#64748B`) for secondary metadata.
- **Typography Pairing**:
  - English: **Poppins** (Bold titles, clean metrics, package tags).
  - Bengali: **Hind Siliguri** (Natural Bengali script legibility).

### 18 Main App Screens & Navigation
```
┌────────────────────────────────────────────────────────────────────────┐
│                        App Navigation Flow                             │
├────────────────────────────────────────────────────────────────────────┤
│  [1. Splash] ──► [2. Onboarding] ──► [3. Auth (Login / Register)]     │
│                                                │                       │
│                           ┌────────────────────┴────────────────────┐  │
│                           ▼                                         ▼  │
│                  [Client Perspective]                     [Role Switch]│
│                  ├─ 4. Home Marketplace                              │ │
│                  ├─ 5. Categories Grid (12 domains)                  │ │
│                  ├─ 6. Search & Multi-Filter                         │ │
│                  ├─ 7. Service Details (Tiered Packages)             │ │
│                  ├─ 8. Designer Profile & Badges                     │ │
│                  ├─ 9. Portfolio Lightbox Gallery                    │ │
│                  ├─ 10. Order Checkout (bKash/Nagad/Rocket)          │ │
│                  ├─ 11. Real-time Order Chat                         │ │
│                  ├─ 12. Order Tracking & Delivery Review             │ │
│                  ├─ 16. User Profile & Favorites                     │ │
│                  └─ 17. Notifications Center                         │ │
│                                                                      │ │
│                  [Designer Perspective]                              │ │
│                  ├─ 13. Designer Dashboard (Live Orders & Stats)     │ │
│                  ├─ 14. Add / Edit Design Service                    │ │
│                  └─ 15. Earnings & Payout Analytics                  │ │
│                                                                      │ │
│                  [Admin Perspective]                                 │ │
│                  └─ 18. Admin Control Center (Users, Orders, Verif.) │ │
└────────────────────────────────────────────────────────────────────────┘
```

### Screen Breakdown
1. **Splash Screen**: Animated branding with logo mark, tagline, and instant role session restoration.
2. **Onboarding Screen**: 3-step carousel showcasing creative gig discovery, secure bKash escrow, and fast delivery.
3. **Login / Register Screen**: Clean tabbed form with role selection (Client vs. Designer), validation, and quick-demo accounts.
4. **Home Marketplace**: Hero banner, live role badge, search bar, category pills, featured designers, and trending gigs.
5. **Categories Screen**: Visual grid of all 12 design categories with icon badges and active gig count.
6. **Search & Filter Modal**: Real-time keyword search, category filter, price slider (BDT 500 – ৳50,000), rating, and delivery speed.
7. **Service Details**: Multi-image slider, seller avatar, ratings, package selector (Basic, Standard, Premium), FAQ, and reviews.
8. **Designer Profile**: Bio, verification badge, rating summary, response time, portfolio grid, and active services.
9. **Portfolio Gallery**: Visual masonry grid with full-screen preview lightbox and design specifications.
10. **Order Checkout**: Package summary, project brief/instructions input, delivery timeline, and MFS payment selection (bKash/Nagad/Rocket/Bank).
11. **Order Chat & Collaboration**: Real-time messaging between client and designer, requirement attachments, and revision notes.
12. **Order Progress & Delivery**: Step-by-step progress tracker (Placed -> Accepted -> Designing -> In Revision -> Delivered -> Completed) with rating modal.
13. **Designer Dashboard**: Active orders queue, pending requests, acceptance actions, quick metrics, and service management.
14. **Add New Service**: Form for creating new gigs with thumbnail selector, category picker, delivery duration, and 3-tier pricing in BDT.
15. **Earnings & Payout Dashboard**: Monthly revenue graph, net profit, pending clearance, and bKash/Nagad withdrawal requests.
16. **User Profile & Favorites**: User details, language toggle (EN/BN), role switcher, wishlist, and help center.
17. **Notifications Hub**: Alerts for order milestones, chat messages, payment confirmations, and admin verifications.
18. **Admin Dashboard**: System metrics (total gross merchandise value, orders, users), pending designer approvals, order dispute resolution, and category controls.

---

## 3. Key Product Decisions & Trade-Offs

- **Local Room Database with Preloaded Market Data**:
  - *Chosen Approach*: Fully relational SQLite database with Room entities (`User`, `Service`, `Order`, `Message`, `Review`, `Category`, `Favorite`).
  - *Why*: Provides instant, blazing-fast local responsiveness, survives app restarts, allows realistic multi-user role interactions without network timeouts or external auth barriers, and fulfills the prompt requirement for complete operational integrity.
- **Bangladeshi Payment Verification Paradigm**:
  - *Chosen Approach*: Official merchant wallet instruction sheets for bKash, Nagad, Rocket, and Bank Wire. Client enters the unique 10-character Transaction ID (`TrxID`) and payment phone number. The order transitions to `PAYMENT_PENDING` and is immediately verifiable by Admin/Designer.
  - *Why*: Complies with Google Play policy by strictly adhering to safe verified flows without simulated dummy webviews, matching standard e-commerce practices in Bangladesh.
- **In-App Role Switcher Utility**:
  - *Chosen Approach*: Floating quick-switch avatar badge accessible in the top bar to immediately switch between "Rakibul Hasan (Client)", "Sumaiya Akter (Designer)", and "Admin HQ".
  - *Why*: Enables seamless testing of all 3 distinct user interfaces (Client ordering -> Designer accepting & delivering -> Admin approving) in one cohesive app session.

---

## 4. Technical Architecture & Data Strategy

### System Architecture Diagram
```
┌────────────────────────────────────────────────────────────────────────┐
│                        Presentation Layer (Jetpack Compose)            │
│  ┌───────────────────────┐  ┌──────────────────────┐  ┌─────────────┐  │
│  │   Client Screens      │  │   Designer Screens   │  │ Admin Screen│  │
│  │ (Home, Order, Chat)   │  │ (Dashboard, Add Gig) │  │  (Auditing) │  │
│  └───────────┬───────────┘  └──────────┬───────────┘  └──────┬──────┘  │
│              └─────────────────────────┼─────────────────────┘         │
│                                        ▼                               │
│                         MarketplaceViewModel (StateFlow)               │
│                                        │                               │
│  ┌─────────────────────────────────────┴────────────────────────────┐  │
│  │              AppRepository (Unified Data Orchestrator)           │  │
│  └─────────────────────────────────────┬────────────────────────────┘  │
│                                        ▼                               │
│                         MarketplaceDatabase (Room SQLite)              │
│  ┌───────────┬─────────────┬───────────┬───────────┬────────────────┐  │
│  │ UserEntity│ServiceEntity│OrderEntity│ ChatEntity│ ReviewEntity   │  │
│  └───────────┴─────────────┴───────────┴───────────┴────────────────┘  │
└────────────────────────────────────────────────────────────────────────┘
```

### Core Data Entities & Schema
- `User`: `id`, `name`, `email`, `role` (CLIENT, DESIGNER, ADMIN), `avatarUrl`, `bio`, `rating`, `completedOrders`, `isVerified`, `phone`.
- `Service`: `id`, `designerId`, `designerName`, `designerAvatar`, `titleEn`, `titleBn`, `category`, `thumbnailUrl`, `rating`, `reviewCount`, `basicPrice`, `basicDays`, `standardPrice`, `standardDays`, `premiumPrice`, `premiumDays`, `description`.
- `Order`: `id`, `serviceId`, `serviceTitle`, `clientId`, `clientName`, `designerId`, `designerName`, `packageTier`, `amountBdt`, `status` (`PENDING`, `IN_PROGRESS`, `DELIVERED`, `REVISION`, `COMPLETED`, `CANCELLED`), `paymentMethod`, `trxId`, `requirements`, `createdAt`, `deliveredWorkUrl`.
- `ChatMessage`: `id`, `orderId`, `senderId`, `senderName`, `senderRole`, `message`, `timestamp`, `attachmentUrl`.
- `Review`: `id`, `serviceId`, `clientId`, `clientName`, `rating`, `comment`, `date`.

---

## 5. Execution Plan & Implementation Steps

1. **Dependencies & Typography**:
   - Update `build.gradle.kts` to uncomment `androidx.room`, `coil.compose`, and `material.icons.extended`.
   - Install **Poppins** and **Hind Siliguri** local static TTF fonts via `font-util` into `res/font/`.
2. **Theme, Localized Strings & Data Models**:
   - Configure M3 theme tokens (Navy, Electric Blue, Purple, Canvas Background) and centralized dual-language dictionary (`strings.xml` and Compose localization helper).
   - Set up Room entities, TypeConverters, DAOs, and database initialization with rich Bangladeshi seed data.
3. **Repository & State Management**:
   - Implement `MarketplaceRepository` with reactive coroutine flows.
   - Build `MarketplaceViewModel` managing current active user role, search queries, active orders, live chat threads, and statistics.
4. **Screen Implementations**:
   - Build TopBar with Language Toggle and Role Switcher.
   - Implement Client workflows: Marketplace Feed, 12 Category explorer, Service Details with 3-tier pricing, Order Checkout with bKash/Nagad/Rocket verification.
   - Implement Designer workflows: Dashboard, Order Acceptance/Delivery, Add New Gig, and Earnings.
   - Implement Admin workflows: User verification queue, commission adjustments, and dispute audits.
   - Implement Shared components: Order tracking timeline, real-time messaging screen, and ratings.
5. **Verification & Polish**:
   - Compile and verify with `compile_applet`.
   - Ensure touch targets adhere to M3 48dp minimums, edge-to-edge insets, and proper testTags.
