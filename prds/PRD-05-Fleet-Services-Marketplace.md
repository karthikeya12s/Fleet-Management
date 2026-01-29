# PRD-05: Fleet Services Marketplace

**Product Name:** FleetBay
**Document Version:** 1.0
**Date:** January 29, 2026
**Author:** Product Management
**Status:** Draft

---

## 1. Overview

FleetBay is a two-sided marketplace connecting fleet operators (demand side) with fleet service providers (supply side) — maintenance shops, tire dealers, towing companies, parts suppliers, body shops, mobile mechanics, fuel vendors, and driver staffing agencies. FleetBay enables fleet managers to discover, compare, book, and pay for fleet services through a single platform with transparent pricing, verified quality ratings, and integrated invoicing.

**Business Model:** Transaction fees on completed services + vendor subscription tiers + payment processing margins + SaaS upsell for fleet management tools.

---

## 2. Problem Statement

### The Vendor Chaos Problem in Fleet Operations

Fleet operators waste enormous time and money sourcing and managing service vendors:

- **12-18 hours per week** spent by fleet managers on vendor-related tasks (NAFA fleet manager surveys): finding shops, getting quotes, scheduling appointments, tracking repairs, processing invoices, resolving disputes.

- **15-25 separate vendors** managed by a typical 100-vehicle fleet: 3-5 maintenance shops, 2-3 tire dealers, 1-2 body shops, a towing service, glass repair, fuel card company, parts suppliers, a registration service, and insurance brokers. Each vendor has different ordering processes, invoicing formats, and payment terms.

- **2-4 hours of extra downtime per breakdown** due to vendor sourcing friction. When a truck breaks down on the road (especially outside the home market), dispatchers scramble through phone lists and Google searches to find a nearby shop that: (a) works on their vehicle type, (b) is open, (c) has capacity, (d) can provide an estimate. This delay costs **$150-$400 per hour in lost productivity** per vehicle.

- **No pricing transparency:** Fleet operators have no way to know if a $2,800 brake job is fair or $1,000 overpriced. Unlike consumer auto repair (where RepairPal and Kelley Blue Book provide price guides), commercial fleet repair has zero pricing transparency. Shops price based on "what the fleet will pay," not market rates.

- **Small shops are invisible:** Over **60% of commercial vehicle repairs** are performed by independent shops (not dealer networks), according to the Commercial Vehicle Solutions Network. These shops have zero digital presence for fleet customers — no online booking, no reviews from fleet managers, no way to advertise specialized capabilities (refrigeration systems, hydraulic lifts, PTO repairs).

- **Invoice chaos:** A fleet manager processing invoices from 20 vendors receives paper invoices, emailed PDFs, and online portal receipts — each in different formats. Reconciliation against POs, validation of line items, and coding to the correct vehicle takes **2-3 full days per month** for a 200-vehicle fleet.

### Market Opportunity

- **US fleet maintenance and repair market:** $300B+ annually
- **Commercial vehicle parts market:** $70B+ (US)
- **Fleet towing and roadside assistance:** $12B (US)
- **Total addressable services market:** $380B+
- **Marketplace take-rate potential (5-12% of GMV):** $19B-$45B
- **Initial target market (fleets of 20-500 vehicles, metro areas):** $50B in services spend
- **Year 5 GMV target:** $500M (0.13% of addressable market)
- **Year 5 marketplace revenue (8% avg take-rate):** $40M

---

## 3. Target Users & Personas

### Demand Side: Fleet Operators

#### Persona 1: Fleet Manager (Primary Buyer)

**Name:** Tony Russo
**Role:** Fleet Manager, regional food distribution company
**Fleet Size:** 150 refrigerated trucks + 40 delivery vans
**Age:** 45

**Current Pain:**
- Has a "shop spreadsheet" with 22 vendors — phone numbers, contacts, specialties — maintained in his head and a shared Google Sheet
- When a truck breaks down on I-95 (outside home market), he spends 45 minutes calling shops to find one that can handle a reefer unit
- Received 3 invoices this month with charges he's pretty sure are inflated but has no benchmark data to challenge
- Spends every Friday afternoon processing vendor invoices and matching to POs
- Has no visibility into which shops consistently do quality work vs. which ones cause repeat repairs

**Goals:**
- Find and book qualified shops in any market in <10 minutes
- Know the fair price for any repair before approving it
- One consolidated invoice and payment workflow
- Quality ratings based on other fleet managers' real experiences
- Reduce vendor management time by 60%

#### Persona 2: Dispatcher (Urgent Buyer)

**Name:** Kim Patel
**Role:** Dispatch Supervisor, long-haul trucking company
**Fleet Size:** 400 Class 8 trucks, nationwide operations

**Current Pain:**
- Handles 5-8 breakdowns per week, many in unfamiliar markets
- Current process: driver calls → dispatcher calls TMC (fleet roadside service) → TMC finds a shop → 1-3 hour delay
- Has zero control over shop selection or pricing in emergency situations
- After-hours breakdowns are the worst — limited options, premium pricing, no quality assurance
- CEO is pushing for faster "driver back on road" times

**Goals:**
- One-tap breakdown assistance: find nearest qualified, available shop instantly
- Real-time shop availability (who can take my truck right now?)
- Price estimates before committing to a shop
- Track repair progress remotely (like Uber tracking but for truck repair)

### Supply Side: Service Providers

#### Persona 3: Independent Repair Shop Owner

**Name:** Hector Ramirez
**Role:** Owner, Ramirez Diesel Repair (independent heavy-duty truck shop)
**Location:** Dallas, TX metro area
**Staff:** 6 mechanics, 4 bays
**Annual Revenue:** $1.2M

**Current Pain:**
- 80% of business comes from 5 fleet accounts — if he loses one, revenue drops 15%
- Zero digital presence — no website, listed on Google Maps but with consumer reviews only
- Cannot compete with dealer networks for new fleet business — no marketing budget, no sales staff
- Idle bays during mid-week; overbooked on Mondays and Fridays
- Invoicing is manual: handwritten on carbon copy, then typed into QuickBooks

**Goals:**
- New fleet customers without a sales team
- Fill idle bay capacity (20-30% of weekly capacity goes unused)
- Digital invoicing and payments (faster than 30-day checks)
- Showcase specialties (reefer units, Cummins engines, hydraulic systems) to relevant fleets

#### Persona 4: National Tire Dealer

**Name:** Lisa Chen
**Role:** Fleet Sales Manager, regional tire dealer (15 locations)
**Brands:** Michelin, BFGoodrich, Continental, Goodyear

**Current Pain:**
- Fleet tire business is relationship-driven — hard to win new accounts without cold-calling
- Each fleet account has negotiated pricing — managing price books across 200 fleet accounts is complex
- Emergency tire calls (blowouts) require phone coordination — no digital platform for urgent service requests
- Mobile tire service trucks are underutilized — only dispatched to known fleet accounts

**Goals:**
- Marketplace visibility to fleets she doesn't currently serve
- Digital service requests (scheduled and emergency)
- Streamlined fleet pricing management
- Better utilization of mobile service units

---

## 4. Business Model Details

### Revenue Streams

#### Stream 1: Transaction Fees (Core)

| Service Category | Transaction Fee (% of invoice) | Rationale |
|-----------------|------------------------------|-----------|
| **Preventive maintenance** (oil change, PM service) | 8% | High volume, standardized pricing |
| **Mechanical repair** (brakes, engine, transmission) | 10% | Higher value, FleetBay provides significant matching value |
| **Tire service** (replacement, rotation, alignment) | 7% | Lower margin category; compete with existing tire programs |
| **Body/collision repair** | 10% | Insurance involvement often; high ticket value |
| **Towing/roadside** | 12% | Highest urgency = highest willingness to pay for speed |
| **Parts only** | 5% | Lower-margin pass-through; volume play |

**Blended average take-rate:** ~8-9% of GMV

**Fee structure:** Charged to the **service provider** (not the fleet operator) — providers pay for customer acquisition, similar to DoorDash/Uber model. Fleet operators see transparent pricing with no platform markup.

#### Stream 2: Vendor Subscription (Visibility + Tools)

| Tier | Monthly Fee | Features |
|------|-----------|----------|
| **Basic** (free) | $0 | Listed on marketplace, receive service requests, basic profile |
| **Pro** | $99/month | Priority listing in search, analytics dashboard, digital invoicing tools, marketing badges ("FleetBay Verified") |
| **Premium** | $249/month | Top placement, featured in FleetBay recommendations, dedicated account manager, API access, lead notifications |

#### Stream 3: Payment Processing

- **Payment facilitation:** FleetBay processes all payments between fleet operators and vendors
- **Processing margin:** 2.9% + $0.30 per transaction (standard card processing) — FleetBay retains 0.5-1.0% after payment processor fees
- **Fleet billing:** Consolidated monthly billing for fleet operators (net-30 terms) — FleetBay pays vendors within 3-5 business days, improving vendor cash flow

#### Stream 4: SaaS Upsell (Fleet Management Lite)

- Fleets using FleetBay for vendor services are offered lightweight fleet management tools:
  - Maintenance scheduling and tracking: $5/vehicle/month
  - Vehicle cost tracking: $3/vehicle/month
  - Bundled: $7/vehicle/month
- Cross-sell target: 20% of active fleet accounts within 12 months

### Unit Economics

| Metric | Value |
|--------|-------|
| Average service transaction value | $650 |
| Average take-rate | 8.5% |
| Revenue per transaction | $55 |
| Transactions per fleet operator/month | 8-12 (100-vehicle fleet) |
| Monthly revenue per active fleet operator | $440-$660 |
| Annual revenue per active fleet operator | $5,300-$7,900 |
| CAC (fleet operator) | $500-$1,000 |
| CAC (vendor) | $200-$400 |
| LTV (fleet operator, 2-year avg) | $12,000 |
| LTV:CAC (fleet operator) | ~15:1 |
| Gross margin (after vendor payouts, payment processing) | 65-70% |

### Revenue Projections

| Year | Active Fleets | Active Vendors | Monthly GMV | Annual GMV | Platform Revenue (8.5%) | Vendor Subs | SaaS Upsell | Total Revenue |
|------|--------------|---------------|------------|-----------|----------------------|------------|------------|---------------|
| Y1 | 150 | 500 | $2.5M | $30M | $2.6M | $0.3M | $0.1M | $3.0M |
| Y2 | 600 | 2,000 | $10M | $120M | $10.2M | $1.2M | $0.8M | $12.2M |
| Y3 | 1,800 | 5,000 | $30M | $360M | $30.6M | $3.0M | $3.0M | $36.6M |

---

## 5. Core Features & Requirements

### P0 — MVP (Must Have for Launch)

**5.1 Vendor Discovery & Search**
- Search by: service type, vehicle type/class, location (radius), availability, rating, certifications
- Map view: vendors plotted with distance, rating, and availability indicator
- Filter by: specialty (reefer, hydraulics, electrical, Cummins/Detroit/Paccar engine brands), hours of operation, mobile service available, certifications (ASE, OEM-certified)
- Vendor profile page: services offered, pricing (ranges or fixed for common services), photos, ratings, certifications, hours, accepted fleet accounts

**5.2 Service Request & Booking**
- **Scheduled service:** Fleet manager selects service type → receives quotes from 2-3 nearby vendors → compares price/availability/rating → books preferred vendor → confirms appointment
- **Emergency/breakdown:** One-tap "Breakdown Assist" → system finds nearest available, qualified vendor → provides ETA and estimated cost → fleet approves → vendor dispatched
- **Service request details:** Vehicle info (year/make/model, VIN), service needed (dropdown + free text), preferred date/time, vehicle location (GPS or address), photos of issue (optional)

**5.3 Pricing Transparency**
- **Price guide:** FleetBay Fair Price range for 50 most common services, by vehicle class and metro area (built from historical transaction data)
- **Quote comparison:** Side-by-side vendor quotes for same service
- **Price flag:** Alert fleet manager when a quote exceeds FleetBay Fair Price by >20%

**5.4 Ratings & Reviews**
- Fleet managers rate vendors after each service: 1-5 stars + written review
- Rating dimensions: quality of work, turnaround time, communication, pricing fairness
- Vendor response capability (reply to reviews)
- Minimum 5 reviews before rating is publicly displayed
- Review verification: only fleet operators with completed transactions can review

**5.5 Payment Processing**
- Fleet operator: net-30 consolidated billing (one invoice per month for all services)
- Vendor: payment within 3-5 business days of service completion and fleet approval
- Payment methods: ACH (primary), credit card, fleet card
- Invoice line items: service description, parts, labor hours, shop supplies, tax — standardized format
- Dispute resolution: 10-day dispute window after invoice delivery

**5.6 Vendor Profile & Onboarding**
- Self-service vendor registration: business info, services offered, certifications, photos, pricing
- Verification: business license validation, insurance verification (GL + garage liability), ASE/OEM certifications
- "FleetBay Verified" badge for vendors completing full verification
- Profile management: update services, pricing, availability, hours

**5.7 Mobile App**
- **Fleet manager app:** Search vendors, create service requests, approve quotes, track repair status, process payments
- **Driver app:** Report breakdown with GPS location + photos, view assigned vendor and ETA, rate service
- **Vendor app:** Receive service requests, send quotes, update repair status, upload invoices, manage availability

### P1 — Post-Launch (3-6 months)

**5.8 Repair Tracking**
- Real-time status updates from vendor: received, diagnosed, parts ordered, in progress, quality check, ready for pickup
- Estimated completion time with updates
- Photo documentation: before, during, after repair
- Fleet manager push notifications for status changes

**5.9 Fleet Account Pricing**
- Vendors can offer fleet-specific pricing for repeat customers (negotiated rates)
- Fleet pricing visible only to that fleet account
- Volume discount tiers: automatic discounts based on monthly/annual spend volume
- Price book management for vendors with multiple fleet accounts

**5.10 Parts Procurement**
- Parts search and ordering through FleetBay (integrated with parts distributors)
- Cross-reference: OEM part number → aftermarket equivalents with price comparison
- Ship-to-shop: order parts delivered directly to the repair shop
- Parts warranty tracking

**5.11 Analytics Dashboard**
- **Fleet operators:** Spend by vendor, category, vehicle; avg cost per service type vs. FleetBay benchmark; vendor performance scorecard
- **Vendors:** Revenue trends, customer acquisition metrics, service mix, capacity utilization, rating trends

### P2 — Growth Features (6-12 months)

**5.12 Vendor Financing**
- Offer vendors early payment (next-day payment) for a fee (1-2% of invoice)
- Working capital loans for shop equipment upgrades (FleetBay Capital, partner with fintech lender)
- Revenue-based financing: repay as a percentage of FleetBay transactions

**5.13 Predictive Service Matching**
- ML model recommends: "Vehicle #2847 is due for brake service in ~2 weeks. Here are 3 available shops near your depot with their pricing."
- Proactive service scheduling based on fleet vehicle data (if telematics connected)

**5.14 National Account Programs**
- Fleet operators designate preferred vendors for specific services across all locations
- Centralized pricing agreements managed through FleetBay
- Compliance tracking: ensure drivers use approved vendors

**5.15 Mobile Mechanic Marketplace**
- On-demand mobile mechanics dispatched to vehicle location (depot or breakdown site)
- Gig-economy model: certified mechanics sign up for shifts
- Best for: oil changes, minor repairs, diagnostics, tire changes at fleet depots

---

## 6. User Stories & Acceptance Criteria

### US-01: Emergency Breakdown Vendor Finding
**As a** dispatcher, **I want to** find a qualified repair shop near my broken-down truck within 5 minutes **so that** the driver gets back on the road faster.

**Acceptance Criteria:**
- "Breakdown Assist" button prominently on home screen of dispatcher app
- Input: vehicle type, issue description (dropdown: engine, tire, electrical, brakes, reefer, other), current GPS location
- System returns 3-5 nearest qualified, currently-open shops within 30-mile radius within 15 seconds
- Results show: shop name, distance, ETA, estimated cost range, rating, phone number, current availability status
- One-tap to request service from preferred shop
- Shop receives push notification and responds within 15 minutes (accept/decline)
- If shop accepts: driver receives shop name, address, ETA, and turn-by-turn directions

### US-02: Scheduled Maintenance Booking
**As a** fleet manager, **I want to** schedule a PM service for 5 vehicles at a shop near my depot **so that** I can keep vehicles on schedule without phone tag.

**Acceptance Criteria:**
- Select service type (e.g., "PM Service - Oil Change + Filter + Inspection") and vehicles (multi-select)
- System shows nearby shops with: available appointment slots this week, price per vehicle, estimated time per vehicle, rating
- Can book multiple vehicles at same shop with staggered drop-off times
- Booking confirmation sent to fleet manager + driver(s) + vendor
- Calendar integration (Google Calendar, Outlook) for appointment reminders
- Automated reminder to driver 24 hours before appointment

### US-03: Vendor Service Request
**As a** repair shop owner, **I want to** receive and respond to service requests digitally **so that** I can fill my idle bays without a sales team.

**Acceptance Criteria:**
- New service request notification: push notification + email + in-app badge
- Request details: fleet name, vehicle info, service needed, preferred timing, vehicle location, photos
- Respond with: estimated cost (parts + labor), estimated completion time, available appointment slots
- Accept or decline with one tap
- Can counter-propose timing or pricing
- Response must be submitted within configurable SLA (default: 2 hours for scheduled, 15 minutes for emergency)

### US-04: Invoice Processing
**As a** fleet manager, **I want** all vendor invoices in a single standardized format on one monthly bill **so that** I can process payments in 30 minutes instead of 3 days.

**Acceptance Criteria:**
- Monthly consolidated invoice: all services across all vendors for the billing period
- Line items: date, vehicle (unit #/VIN), vendor name, service description, parts cost, labor cost, total
- Sortable/filterable by: vehicle, vendor, service category, date
- Each line item links to detailed vendor invoice (parts list, labor hours, photos)
- Export to CSV, QuickBooks, and PDF
- One-click payment approval for entire invoice or line-by-line approval
- Disputed items flagged for resolution (excluded from payment until resolved)

### US-05: Vendor Rating and Feedback
**As a** fleet manager, **I want to** see verified ratings from other fleet managers before choosing a shop **so that** I don't waste time and money on low-quality vendors.

**Acceptance Criteria:**
- Rating appears on vendor profile: overall score (1-5), number of reviews, score by dimension (quality, speed, communication, price)
- Only verified fleet operators with completed transactions can leave reviews
- Reviews include: star rating, written feedback, service type, vehicle type, date of service
- Vendor can respond to reviews publicly
- "FleetBay Top Rated" badge for vendors with 4.5+ rating and 20+ reviews
- Filter search results by minimum rating

---

## 7. Technical Architecture

```
┌───────────────────────────────────────────────────────────────┐
│                     CLIENT APPLICATIONS                        │
│                                                                │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐               │
│  │ Fleet Mgr  │  │ Driver     │  │ Vendor     │               │
│  │ Web + App  │  │ Mobile App │  │ Web + App  │               │
│  │ (React +   │  │ (React     │  │ (React +   │               │
│  │  RN)       │  │  Native)   │  │  RN)       │               │
│  └─────┬──────┘  └─────┬──────┘  └─────┬──────┘               │
└────────┼────────────────┼────────────────┼─────────────────────┘
         └────────────────┼────────────────┘
                          ▼
┌───────────────────────────────────────────────────────────────┐
│                      API GATEWAY                               │
│              (Authentication, Rate Limiting)                   │
└─────────────────────────┬─────────────────────────────────────┘
                          │
         ┌────────────────┼────────────────┐
         ▼                ▼                ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Marketplace │  │  Payments    │  │ Communication│
│  Service     │  │  Service     │  │ Service      │
│ (search,     │  │ (Stripe      │  │ (notifs,     │
│  matching,   │  │  Connect,    │  │  SMS, email, │
│  booking,    │  │  invoicing,  │  │  in-app)     │
│  reviews)    │  │  payouts)    │  │              │
└──────┬───────┘  └──────┬───────┘  └──────────────┘
       │                 │
       ▼                 ▼
┌──────────────┐  ┌──────────────┐
│ PostgreSQL   │  │ Stripe       │
│ (marketplace │  │ (payments,   │
│  data)       │  │  payouts,    │
│              │  │  billing)    │
└──────────────┘  └──────────────┘

Additional Services:
├── Search Engine (Elasticsearch — vendor search, geo-queries)
├── Pricing Engine (fair price calculation from transaction history)
├── Matching Algorithm (emergency: nearest + available + qualified)
├── Analytics (Snowflake — spend analytics, vendor performance)
├── Maps (Mapbox — vendor locations, directions, ETA)
├── File Storage (S3 — photos, invoices, documents)
└── Background Jobs (SQS + Lambda — reminders, status checks)
```

**Key Technical Decisions:**

- **Marketplace framework:** Custom-built on PostgreSQL + Elasticsearch (vendor search requires geo-spatial queries + faceted filtering that existing marketplace platforms handle poorly for this vertical)
- **Payments:** Stripe Connect for marketplace payments (handles split payments, vendor payouts, fleet billing, tax reporting)
- **Real-time matching (emergency):** Custom algorithm considering: distance, vendor availability (real-time), vehicle type match, certification match, rating, price history
- **Pricing engine:** Statistical model built from completed transaction data — calculates fair price ranges by service type, vehicle class, and metro area (requires ~10,000 transactions per service category for statistical significance)
- **Mobile-first:** React Native for all mobile apps; React for web dashboards

---

## 8. Network Effects & Liquidity Strategy

### The Chicken-and-Egg Problem

Marketplaces require both supply (vendors) and demand (fleet operators) to deliver value. Neither side joins without the other.

### Liquidity Strategy

**Phase 1: Supply Seeding (Months 1-3)**

1. **Geo-focused launch:** Start in ONE metro area (Dallas-Fort Worth — large commercial fleet market, many independent shops)
2. **Manual vendor onboarding:** FleetBay team physically visits top 50 repair shops, tire dealers, and towing companies in DFW. Offer:
   - Free listing and first 6 months of Pro subscription
   - Professional profile photos and description (done by FleetBay)
   - Guarantee: minimum 5 service requests per month or FleetBay refunds Pro subscription
3. **Anchor vendor recruitment:** Sign 2-3 national/regional chains (Firestone, Love's Truck Care, TravelCenters of America) — provides instant coverage and credibility

**Phase 2: Demand Seeding (Months 2-4)**

1. **Target 20 fleets in DFW** with 50-300 vehicles (food distribution, construction, field service)
2. **Fleet onboarding incentive:** First $1,000 in services transacted through FleetBay = zero transaction fee (FleetBay absorbs vendor fee)
3. **"Bring your vendor" program:** Fleets invite their existing preferred shops to join FleetBay — both fleet and vendor get $200 credit
4. **Pain point entry:** Start with the highest-pain use case — **emergency breakdown service**. Even fleets that don't want to change their regular shops will use FleetBay for breakdowns in unfamiliar areas.

**Phase 3: Organic Growth (Months 4-12)**

1. **Marketplace flywheel kicks in:** More fleets → more transactions → more revenue for vendors → more vendors join → better selection → more fleets join
2. **Expand to metro #2 and #3:** Houston, Atlanta (similar fleet density to DFW)
3. **Data network effects:** As transaction volume grows, FleetBay Fair Price data becomes more accurate and valuable — a moat competitors can't replicate without transaction history

**Phase 4: Geographic Expansion (Months 12-24)**

- Expand to top 20 US metro areas
- Focus on interstate corridor coverage (I-95, I-10, I-40, I-80) for long-haul fleets
- Self-service vendor onboarding (vendors sign up without FleetBay team visit)

### Liquidity Metrics

| Metric | Target |
|--------|--------|
| Service request fill rate (% of requests matched to vendor) | >80% within 30 min (emergency), >95% within 24 hrs (scheduled) |
| Vendor response rate | >70% of requests receive response |
| Average time to first vendor response (scheduled) | <2 hours |
| Average time to vendor dispatch (emergency) | <30 minutes |
| Repeat transaction rate (fleet uses FleetBay again) | >60% within 30 days |

---

## 9. Success Metrics & KPIs

### Marketplace Health Metrics

| Metric | Y1 Target | Y2 Target |
|--------|-----------|-----------|
| Monthly GMV | $2.5M | $10M |
| Monthly transactions | 3,800 | 15,400 |
| Active fleet operators (monthly) | 150 | 600 |
| Active vendors (monthly) | 500 | 2,000 |
| Service request fill rate | 75% | 88% |
| Avg vendor response time (scheduled) | <3 hours | <1.5 hours |
| Avg vendor response time (emergency) | <20 minutes | <12 minutes |

### Quality Metrics

| Metric | Target |
|--------|--------|
| Average vendor rating | 4.2+ / 5.0 |
| Repeat fleet operator rate (monthly) | 60%+ |
| Service complaint rate | <3% of transactions |
| Payment dispute rate | <1.5% of transactions |
| Vendor churn (monthly) | <5% |
| Fleet operator churn (monthly) | <8% |

### Financial Metrics

| Metric | Y1 Target | Y2 Target |
|--------|-----------|-----------|
| Net revenue | $3.0M | $12.2M |
| Gross margin | 65% | 70% |
| CAC (fleet operator) | $800 | $500 |
| CAC (vendor) | $300 | $150 |
| Unit economics positive per metro | Month 8 | All active metros |

---

## 10. Competitive Analysis

| Capability | FleetBay | Fleetio (Vendor Network) | Openbay | RepairPal | FinditParts | FleetPride | TruckPark |
|-----------|---------|------------------------|---------|-----------|-------------|-----------|-----------|
| **Focus** | Commercial fleet marketplace | Fleet maintenance software with vendor directory | Consumer auto repair marketplace | Consumer auto repair estimates | Commercial truck parts marketplace | Commercial truck parts distributor | Truck parking/services |
| **Transactional marketplace** | Yes (core) | No (directory only) | Yes (consumer) | No (referral) | Yes (parts only) | E-commerce | Limited |
| **Commercial fleet focus** | Yes | Yes | No (consumer) | No (consumer) | Yes (parts) | Yes (parts) | Trucking |
| **Service booking** | Yes (scheduled + emergency) | No | Yes (consumer) | No | No | No | No |
| **Pricing transparency** | Yes (FleetBay Fair Price) | No | Yes (consumer estimates) | Yes (consumer) | Yes (parts pricing) | Yes (parts) | No |
| **Ratings/reviews (fleet-specific)** | Yes | Basic | Yes (consumer) | Yes (consumer) | No | No | Yes |
| **Payment processing** | Yes (consolidated billing) | No | Yes | No | Yes | Yes | No |
| **Emergency/breakdown** | Yes (real-time matching) | No | No | No | No | No | No |
| **Mobile mechanic** | Yes (P2) | No | No | No | No | No | No |
| **Vendor tools (invoicing, etc.)** | Yes | No | Limited | No | Yes | Yes | No |

### Competitive Positioning

**"The commercial fleet's operating system for outside services."**

FleetBay has no direct competitor. Fleetio has a vendor directory but no transactional marketplace. Openbay and RepairPal serve consumer auto, not commercial fleets. FinditParts and FleetPride are parts marketplaces, not service marketplaces. No existing platform enables fleet operators to discover, book, pay, and rate fleet service providers in a transactional marketplace with pricing transparency.

**Defensibility:**
1. **Transaction data moat:** FleetBay Fair Price data improves with every transaction — impossible to replicate without marketplace volume
2. **Two-sided network effects:** More vendors attract more fleets, which attract more vendors
3. **Vendor relationship lock-in:** Vendors build their reputation (ratings, reviews) on FleetBay — switching cost increases with review count
4. **Fleet workflow integration:** Consolidated billing and vehicle cost tracking create operational dependency

---

## 11. Go-to-Market Strategy

### Phase 1: DFW Metro Launch (Months 1-4)

**Supply Development (Vendors):**
- 3-person "vendor success" team physically visits 200 shops in DFW metro
- Target: 50 verified vendors at launch (mix of general repair, tire, towing, body shop)
- Onboarding includes: profile setup, professional photos, pricing configuration, app training
- Sign 2 national chain partners (e.g., Love's Truck Care, TA Petro)

**Demand Development (Fleets):**
- Target 30 fleets in DFW with 50-300 vehicles
- Industries: food/beverage distribution, construction, HVAC/plumbing, courier
- Lead with emergency breakdown use case (lowest switching cost — fleets try FleetBay for breakdowns without changing regular shop relationships)
- Fleet onboarding: import vehicle list, configure notification preferences, add dispatchers and drivers

**Marketing:**
- LinkedIn Ads targeting fleet managers in DFW
- Local fleet association sponsorships (NTFMA — North Texas Fleet Management Association)
- "FleetBay Launch Partner" designation for first 20 fleets and 30 vendors (testimonials, case studies)
- Truck stop signage and brochures (drivers are influencers for shop selection)

### Phase 2: Multi-Metro Expansion (Months 5-10)

- **Metro #2: Houston** (Month 5) — similar market dynamics, close to DFW for operational support
- **Metro #3: Atlanta** (Month 7) — major Southeast hub, strong fleet density
- **Metro #4-5: Chicago, Phoenix** (Month 9-10)
- Replicate DFW playbook with lighter touch (50% physical + 50% digital vendor onboarding)
- Cross-metro fleets: DFW fleet with Houston operations gets Houston coverage automatically

### Phase 3: National Expansion + Self-Serve (Months 11-18)

- Self-serve vendor onboarding (digital verification, no physical visit required for verified businesses)
- Interstate corridor coverage: I-95 (East Coast), I-10 (Southern), I-40, I-80 corridors
- Partnerships with fleet management companies (FleetBay as vendor procurement layer)
- "FleetBay Verified" marketing campaign at industry conferences (NTEA Work Truck Show, TMC Annual Meeting)

### Phase 4: Platform Maturity (Months 18-24)

- Mobile mechanic marketplace launch (top 10 metros)
- Parts procurement integration
- National account program for multi-location fleets
- API for fleet management software integration (Fleetio, Samsara, Motive)
- Canada expansion (similar fleet landscape)

---

## 12. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| **Low vendor adoption** (shops won't join/use platform) | High (early) | Critical | Physical onboarding, free Pro tier for 6 months, guaranteed minimum leads, extremely simple UX (should be easier than answering a phone call) |
| **Low transaction volume** (fleets browse but don't transact) | High (early) | Critical | Start with emergency use case (highest pain = highest adoption); $1,000 zero-fee onboarding; fleet manager time savings >12 hrs/week as value prop |
| **Service quality issues** (bad vendor experience reflects on FleetBay) | Medium | High | Verification process; rating system with low-rating vendor removal (below 3.0 after 10 reviews); service guarantee (FleetBay covers cost of rework if vendor quality issue verified) |
| **Vendor disintermediation** (fleet and vendor go direct after first transaction) | Medium | High | Consolidated billing value (fleet doesn't want 25 vendor invoices again); continued fair pricing data; vendor payment speed (3-5 days vs. net-30+); ongoing service tracking |
| **Pricing pushback from vendors** (8-10% take-rate too high) | Medium | Medium | Position as customer acquisition cost (vendors currently spend 15-20% on customer acquisition through sales staff); offer lower take-rate for higher-volume vendors; compare to HomeAdvisor/Angi (20-30% take-rate) |
| **Fleet managers resistant to change** from existing vendor relationships | High | Medium | "Bring your vendor" program (don't ask fleets to switch — ask them to digitize existing relationships); start with breakdown use case (no existing vendor for out-of-market breakdowns) |
| **Payment fraud / disputes** | Low | Medium | Stripe Connect's fraud protection; require service completion photos; 10-day dispute window; escrow hold for first-time vendor transactions |

---

## 13. Roadmap

### MVP (Months 0-4)
- Vendor discovery and search (geo-based, filtered by service type and vehicle class)
- Vendor profiles with photos, services, hours, certifications
- Service request submission (scheduled + emergency)
- Vendor quoting and booking workflow
- Basic ratings and reviews (1-5 stars + text)
- Payment processing (Stripe Connect — fleet billing, vendor payouts)
- Mobile apps: fleet manager, driver (breakdown report), vendor (receive/respond to requests)
- DFW metro launch: 50 vendors, 20 fleet operators

### V1.0 (Months 5-8)
- FleetBay Fair Price engine (price benchmarks for top 20 service types)
- Repair tracking (real-time status updates from vendor)
- Fleet account pricing (negotiated rates per fleet-vendor pair)
- Analytics dashboards (fleet: spend analytics; vendor: performance metrics)
- Consolidated monthly billing for fleets (one invoice, all vendors)
- Expand to Houston + Atlanta
- Target: 200 vendors, 80 fleet operators

### V1.5 (Months 9-14)
- Parts procurement integration (search + order through marketplace)
- Volume discount tiers (automatic discounts at spend thresholds)
- National account program (multi-location fleet support)
- Vendor Pro and Premium subscription tiers with analytics
- FleetBay Verified certification program
- Expand to top 10 US metros
- Target: 1,500 vendors, 400 fleet operators

### V2.0 (Months 15-24)
- Mobile mechanic marketplace (on-demand at depot/roadside)
- Predictive service matching (proactive recommendations based on fleet data)
- Vendor financing (early payment, working capital)
- SaaS fleet management upsell (maintenance scheduling, vehicle cost tracking)
- API for integration with fleet management platforms
- Interstate corridor coverage
- Target: 5,000 vendors, 1,500 fleet operators, $30M GMV/month

---

## Appendix A: Key Assumptions

1. Fleet operators will transact through FleetBay (rather than going direct) for the value of pricing transparency, consolidated billing, and rating data
2. Independent repair shops will adopt a digital platform if onboarding is free and leads are guaranteed
3. 8-10% take-rate is acceptable to vendors when positioned as customer acquisition cost
4. Emergency breakdown is the highest-pain entry point that drives initial adoption
5. "Bring your vendor" strategy reduces fleet switching cost to near-zero
6. FleetBay Fair Price requires ~10,000 transactions per service category per metro for statistical significance
7. Geographic density of 50+ vendors per metro provides adequate coverage for most service needs

## Appendix B: Open Questions

1. Should FleetBay offer a service quality guarantee (rework coverage) from day one, or wait until review data is sufficient to identify quality vendors?
2. What is the right take-rate for different service categories — should emergency services command a higher fee due to urgency value?
3. Should FleetBay build its own towing dispatch capability (high-frequency, high-pain use case) or partner with existing dispatch platforms (Agero, Urgently)?
4. How do we handle fleet operators who want to use FleetBay for vendor discovery but process payments outside the platform (losing transaction fee revenue)?
5. Should vendors be able to set their own prices, or should FleetBay enforce "fair price" ceilings to prevent price gouging?
6. Is DFW the optimal launch metro, or should we consider a smaller market where we can achieve density faster?
