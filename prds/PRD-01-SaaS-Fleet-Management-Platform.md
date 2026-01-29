# PRD-01: SaaS Fleet Management Platform for SMB Fleets

**Product Name:** FleetPulse
**Document Version:** 1.0
**Date:** January 29, 2026
**Author:** Product Management
**Status:** Draft

---

## 1. Overview

FleetPulse is a cloud-native, SaaS fleet management platform designed specifically for small-to-medium business (SMB) fleets of 10-200 vehicles. It consolidates vehicle tracking, maintenance scheduling, compliance management, fuel tracking, and driver management into a single affordable subscription — replacing the patchwork of spreadsheets, paper logs, and disconnected point solutions that SMB fleet operators rely on today.

**Business Model:** Monthly per-vehicle subscription pricing with tiered feature access.

---

## 2. Problem Statement

### The SMB Fleet Management Gap

Small-to-medium fleet operators face a systemic efficiency crisis driven by tool fragmentation:

- **Fragmented workflows:** A typical 50-vehicle fleet uses 4-7 disconnected tools — Google Sheets for maintenance logs, a standalone GPS app (Life360 or consumer-grade trackers), paper-based DVIR forms, manual fuel receipt collection, and email/phone for dispatch. No single source of truth exists.

- **Cost pressure:** The American Transportation Research Institute (ATRI) reported fleet operating costs at **$2.27/mile in 2023**, with marginal costs continuing to rise. Small fleets pay an estimated **15-20% premium** over larger operators due to lack of optimization tooling, bulk purchasing power, and operational visibility.

- **Compliance risk:** FMCSA penalties for Hours of Service (HOS) violations range from **$1,000-$16,000 per violation**. Small fleets without automated compliance tracking are disproportionately cited — FMCSA data shows fleets with <50 vehicles account for 60%+ of out-of-service violations.

- **Maintenance inefficiency:** Without predictive or even structured preventive maintenance, SMB fleets experience **30-40% higher unplanned downtime** versus fleets using management software (Fleetio benchmark data). Average unplanned repair costs are 3-5x planned maintenance costs.

- **Enterprise solutions are priced out of reach:** Geotab starts at ~$25-40/vehicle/month, Samsara at ~$30-45/vehicle/month with hardware requirements and multi-year contracts. A 50-vehicle fleet faces $15,000-$27,000/year before hardware — prohibitive for businesses operating on thin margins.

### Market Opportunity

- **US commercial fleet market:** 15.5 million registered commercial vehicles (IHS Markit)
- **SMB segment (10-200 vehicles):** ~500,000 fleet operators, ~8 million vehicles
- **Current SaaS penetration in SMB fleets:** Estimated <15%
- **Serviceable addressable market:** $2.4B annually (8M vehicles x $25/vehicle/month average)

---

## 3. Target Users & Personas

### Primary Persona: Owner-Operator / Fleet Manager (SMB)

**Name:** Mike Torres
**Role:** Operations Manager at a regional HVAC company
**Fleet Size:** 42 service vans
**Age:** 38
**Tech Comfort:** Moderate — uses QuickBooks, Google Workspace

**Pain Points:**
- Tracks maintenance in a shared Google Sheet that's always outdated
- Drivers text photos of fuel receipts; he manually enters them weekly
- Has been fined twice for expired vehicle registrations ($500 each)
- Spends 10+ hours/week on fleet admin instead of growing the business
- No visibility into driver behavior or route efficiency

**Goals:**
- Reduce fleet admin time to <3 hours/week
- Eliminate compliance surprises
- Cut fuel costs by 10%
- Extend vehicle lifespan through better maintenance

### Secondary Persona: Small Trucking Company Owner

**Name:** Linda Chen
**Role:** Owner of a 25-truck regional freight carrier
**Fleet Size:** 25 Class 8 trucks + 30 trailers
**Age:** 52
**Tech Comfort:** Low-moderate — relies on dispatch software but struggles with new tools

**Pain Points:**
- ELD compliance is a constant worry
- Fuel costs are her #1 expense and she has no analytics
- Manually tracks HOS using paper backup logs
- Insurance premiums increased 30% last renewal due to lack of safety data

**Goals:**
- Automated ELD/HOS compliance
- Fuel cost visibility and theft detection
- Safety data to negotiate lower insurance premiums
- Simple interface her drivers won't resist

### Tertiary Persona: Finance Controller / CFO

**Name:** Rachel Kim
**Role:** Controller at a plumbing company with 80 vehicles
**Pain Points:**
- Cannot get accurate fleet TCO numbers
- Fuel card reconciliation takes 2 days/month
- No depreciation or lifecycle cost tracking
- Audit readiness is poor

**Goals:**
- Consolidated fleet cost reporting
- Automated fuel card reconciliation
- Budget forecasting for fleet expenses

---

## 4. Business Model Details

### Pricing Tiers

| Tier | Price/Vehicle/Month | Target Fleet Size | Key Features |
|------|-------------------|-------------------|--------------|
| **Starter** | $12/vehicle | 10-30 vehicles | GPS tracking, basic maintenance scheduling, fuel log, mobile app |
| **Professional** | $22/vehicle | 20-100 vehicles | Everything in Starter + compliance management, driver scoring, route history, reporting dashboard, fuel card integration |
| **Business** | $35/vehicle | 50-200 vehicles | Everything in Pro + predictive maintenance alerts, API access, advanced analytics, custom reports, priority support, multi-location |

**Contract Terms:**
- Monthly billing (no long-term contracts required — key SMB differentiator)
- Annual prepay discount: 15% off
- Free 14-day trial on Professional tier
- No hardware required (BYOD GPS tracker support + optional hardware partnerships)

### Unit Economics

| Metric | Value |
|--------|-------|
| **Blended ARPU** | $22/vehicle/month |
| **Gross margin** | 78-82% (pure SaaS, no hardware) |
| **CAC (SMB)** | $800-$1,200 per account (digital marketing + inside sales) |
| **Average fleet size** | 45 vehicles |
| **Average ACV** | $11,880 (45 x $22 x 12) |
| **LTV (3-year avg retention)** | $35,640 |
| **LTV:CAC ratio** | ~30:1 |
| **Payback period** | 1-2 months |
| **Monthly churn target** | <2% logo churn |

### Revenue Projections (Year 1-3)

| Year | Customers | Avg Vehicles/Customer | Total Vehicles | ARR |
|------|-----------|----------------------|----------------|-----|
| Y1 | 200 | 40 | 8,000 | $2.1M |
| Y2 | 800 | 45 | 36,000 | $9.5M |
| Y3 | 2,000 | 50 | 100,000 | $26.4M |

---

## 5. Core Features & Requirements

### P0 — MVP (Must Have for Launch)

**5.1 Real-Time Vehicle Tracking**
- Live map view with all vehicles plotted
- 30-second position update frequency
- Vehicle status indicators (moving, idle, stopped, offline)
- Last known location for offline vehicles
- Support for 10+ GPS hardware providers via API integration (or smartphone-based tracking as fallback)

**5.2 Maintenance Management**
- Service schedule templates (oil change, tire rotation, brake inspection, etc.)
- Mileage-based and time-based maintenance triggers
- Work order creation and tracking (open, in-progress, completed)
- Maintenance cost logging per vehicle
- Upcoming maintenance dashboard with alerts (email + push notification)
- Digital vehicle inspection reports (DVIR) via mobile app

**5.3 Fuel Tracking**
- Manual fuel entry via mobile app (receipt photo capture + OCR)
- Fuel card integration (WEX, Fuelman, Comdata) for automated import
- MPG/L-per-100km tracking per vehicle
- Fuel cost reporting by vehicle, driver, time period
- Anomaly flagging (unusually high fuel consumption)

**5.4 Driver Management**
- Driver profiles with license info, certifications, assigned vehicles
- License/certification expiration tracking and alerts
- Basic driver scorecards (speeding events, hard braking, idle time — from GPS data)

**5.5 Mobile App (iOS + Android)**
- Driver-facing: DVIR submission, fuel logging, navigation, messaging
- Manager-facing: vehicle location, alerts, approval workflows

**5.6 Dashboard & Reporting**
- Fleet overview dashboard (utilization, costs, alerts)
- Pre-built reports: maintenance costs, fuel costs, vehicle utilization, compliance status
- Export to CSV/PDF

### P1 — Post-Launch (3-6 months)

**5.7 Compliance Management**
- Registration and insurance expiration tracking
- ELD integration for HOS compliance (partner integration with Motive, KeepTruckin)
- IFTA fuel tax reporting
- DOT inspection readiness checklist
- Automated renewal reminders (90/60/30 days)

**5.8 Route History & Analysis**
- Historical route playback
- Geofence creation and alerts (enter/exit)
- Idle time reporting with location context
- Unauthorized use detection (after-hours, off-route)

**5.9 Advanced Reporting & Analytics**
- Total Cost of Ownership (TCO) per vehicle
- Fleet benchmarking (your fleet vs. industry averages)
- Custom report builder
- Scheduled report delivery via email

**5.10 Integrations**
- QuickBooks / Xero accounting sync
- Fuel card auto-reconciliation
- Zapier connector for custom workflows

### P2 — Growth Features (6-12 months)

**5.11 Predictive Maintenance**
- OBD-II fault code monitoring (via compatible hardware)
- Pattern-based maintenance predictions (e.g., brake wear trending)
- Recommended service alerts based on vehicle make/model/mileage

**5.12 Dispatch & Scheduling**
- Job assignment and dispatch board
- Estimated arrival time calculation
- Customer notification integration
- Workload balancing across drivers

**5.13 Fleet Optimization Intelligence**
- Vehicle replacement recommendations (TCO-based)
- Right-sizing analysis (underutilized vehicles)
- Fuel efficiency optimization suggestions
- Insurance data export for premium negotiation

---

## 6. User Stories & Acceptance Criteria

### US-01: Vehicle Location Tracking
**As a** fleet manager, **I want to** see all my vehicles on a live map **so that** I can monitor operations in real-time.

**Acceptance Criteria:**
- Map loads within 3 seconds showing all active vehicles
- Vehicle positions update every 30 seconds
- Clicking a vehicle shows: driver name, speed, heading, last stop time, status
- Map supports satellite and street view
- Search/filter by vehicle name, driver, or status

### US-02: Maintenance Scheduling
**As a** fleet manager, **I want to** set up recurring maintenance schedules **so that** vehicles are serviced on time without manual tracking.

**Acceptance Criteria:**
- Can create maintenance tasks triggered by mileage interval OR calendar interval (whichever comes first)
- System sends email + push notification at configurable thresholds (e.g., 500 miles before due, 7 days before due)
- Overdue maintenance items display in red on dashboard
- Completing a work order automatically resets the next due trigger
- Maintenance history is viewable per vehicle with full cost records

### US-03: Fuel Receipt Capture
**As a** driver, **I want to** photograph my fuel receipt and have it automatically logged **so that** I don't have to manually enter fuel data.

**Acceptance Criteria:**
- Camera opens within mobile app with receipt capture mode
- OCR extracts: gallons/liters, total cost, station name, date
- Driver confirms/corrects extracted data before submission
- Fuel entry appears in manager's dashboard within 60 seconds
- Receipt image stored and viewable from fuel log entry

### US-04: Compliance Alerts
**As a** fleet manager, **I want to** receive automatic alerts when vehicle registrations, inspections, or driver licenses are expiring **so that** I never face compliance fines.

**Acceptance Criteria:**
- Alerts sent at 90, 60, 30, 14, and 7 days before expiration
- Dashboard shows compliance status with red/yellow/green indicators
- Expired items block vehicle from being dispatched (configurable)
- Renewal completion can be logged with document upload

### US-05: Fleet Cost Reporting
**As a** CFO, **I want to** see total fleet costs broken down by category and vehicle **so that** I can manage budgets and identify savings.

**Acceptance Criteria:**
- Report shows: fuel, maintenance, insurance, depreciation, tolls, fines per vehicle
- Filter by date range, vehicle group, cost category
- Compare month-over-month and year-over-year
- Export to CSV and PDF
- Cost-per-mile calculation per vehicle and fleet-wide

---

## 7. Technical Architecture Overview

```
┌─────────────────────────────────────────────────────┐
│                    CLIENT LAYER                       │
│  ┌──────────┐  ┌──────────┐  ┌───────────────────┐  │
│  │ Web App  │  │ iOS App  │  │   Android App     │  │
│  │ (React)  │  │ (Swift)  │  │   (Kotlin)        │  │
│  └────┬─────┘  └────┬─────┘  └────────┬──────────┘  │
└───────┼──────────────┼─────────────────┼─────────────┘
        │              │                 │
        ▼              ▼                 ▼
┌─────────────────────────────────────────────────────┐
│                   API GATEWAY                        │
│            (AWS API Gateway / Kong)                  │
│         Rate limiting, auth, routing                 │
└──────────────────────┬──────────────────────────────┘
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
┌──────────────┐ ┌──────────┐ ┌──────────────┐
│  Fleet Core  │ │ Tracking │ │ Notification │
│  Service     │ │ Service  │ │ Service      │
│ (vehicles,   │ │ (ingest, │ │ (email,push, │
│  drivers,    │ │  store,  │ │  SMS)        │
│  maint,fuel) │ │  query)  │ │              │
└──────┬───────┘ └────┬─────┘ └──────────────┘
       │              │
       ▼              ▼
┌──────────────┐ ┌──────────────┐
│ PostgreSQL   │ │ TimescaleDB  │
│ (core data)  │ │ (location    │
│              │ │  time-series)│
└──────────────┘ └──────────────┘

External Integrations:
├── GPS Hardware APIs (Geotab, CalAmp, Queclink)
├── Fuel Card APIs (WEX, Fuelman, Comdata)
├── OCR Service (Google Vision / AWS Textract)
├── Mapping (Mapbox / Google Maps)
├── Accounting (QuickBooks, Xero)
└── ELD Providers (Motive, Samsara - partner API)
```

**Key Technical Decisions:**
- **Multi-tenant SaaS** with tenant isolation at the database row level (RLS in PostgreSQL)
- **No proprietary hardware required** — integrate with existing GPS trackers via API, or use smartphone GPS as entry-level option
- **Event-driven architecture** using Kafka/SQS for real-time tracking data ingestion
- **Infrastructure:** AWS (ECS/Fargate for services, RDS for PostgreSQL, S3 for documents/images)
- **Mobile:** React Native for cross-platform with native modules where needed

---

## 8. Success Metrics & KPIs

### Product Metrics

| Metric | Target (Y1) | Target (Y2) |
|--------|-------------|-------------|
| Monthly Active Users (MAU) | 70% of registered users | 75% |
| Daily Active Users (DAU) | 40% of MAU | 50% |
| Feature adoption (maintenance module) | 60% of accounts | 80% |
| Feature adoption (fuel tracking) | 50% of accounts | 70% |
| Mobile app daily opens (drivers) | 1.5x per driver/day | 2x |
| NPS | 40+ | 50+ |
| Support tickets per account/month | <2 | <1.5 |

### Business Metrics

| Metric | Target (Y1) | Target (Y2) |
|--------|-------------|-------------|
| New customers/month | 15-20 | 50-70 |
| Monthly logo churn | <2.5% | <1.5% |
| Net revenue retention | 105% | 115% |
| ARPU growth | $22 → $24 | $24 → $28 |
| Gross margin | 78% | 82% |

### Customer Outcome Metrics

| Metric | Target |
|--------|--------|
| Fleet admin time reduction | 50%+ (from ~12 hrs/week to <6) |
| Compliance violation reduction | 80%+ |
| Maintenance cost reduction | 15-20% (through preventive scheduling) |
| Fuel cost reduction | 8-12% (through visibility + driver behavior) |

---

## 9. Competitive Analysis

| Feature | FleetPulse | Samsara | Geotab | Fleetio | Motive |
|---------|-----------|---------|--------|---------|--------|
| **Target segment** | SMB (10-200) | Mid-Enterprise | Enterprise | SMB-Mid | Mid-Enterprise |
| **Pricing** | $12-35/veh/mo | $30-45/veh/mo | $25-40/veh/mo | $5-17/veh/mo | $25-40/veh/mo |
| **Hardware required** | No (BYOD) | Yes (proprietary) | Yes (proprietary) | No | Yes (proprietary) |
| **Contract** | Month-to-month | 3-5 year | 3-5 year | Month-to-month | 3-year |
| **GPS tracking** | Yes (integrated) | Yes | Yes | Via integrations | Yes |
| **Maintenance** | Built-in | Basic | Via marketplace | Core strength | Basic |
| **Fuel tracking** | Built-in + OCR | Yes | Yes | Via integrations | Yes |
| **Compliance** | Built-in | Yes | Yes | Basic | Core strength (ELD) |
| **Mobile app** | Full-featured | Good | Basic | Good | Good |
| **Setup time** | <1 hour | Days-weeks | Days-weeks | <1 hour | Days-weeks |
| **Free trial** | 14 days | Demo only | Demo only | Free tier | Demo only |

### Competitive Positioning

**FleetPulse vs. Samsara/Geotab/Motive:** These are hardware-first platforms requiring proprietary devices, multi-year contracts, and professional installation. They're designed for 200+ vehicle enterprise fleets. FleetPulse wins on: no hardware lock-in, no long-term contracts, faster setup, lower price point, and SMB-optimized UX.

**FleetPulse vs. Fleetio:** Fleetio is the closest competitor in the SMB space with strong maintenance management. However, Fleetio lacks native GPS tracking (requires third-party integration), has limited fuel management, and no built-in compliance module. FleetPulse wins on: all-in-one platform (no integrations needed for core use cases), built-in tracking, superior mobile experience for drivers.

**Key Differentiator:** The only all-in-one fleet platform for SMBs that requires zero hardware investment, no long-term contract, and can be operational within one hour of signup.

---

## 10. Go-to-Market Strategy

### Phase 1: Digital-Led Acquisition (Months 1-6)

**Channels:**
- **SEO/Content:** Target long-tail keywords: "fleet management for small business," "track company vehicles free," "fleet maintenance spreadsheet template" (convert free template users)
- **Google Ads:** Target high-intent searches: "fleet tracking software," "vehicle maintenance software"
- **LinkedIn Ads:** Target: Operations Manager, Fleet Manager, Owner at companies with 20-500 employees in target industries
- **Free tools:** Offer free fleet TCO calculator, maintenance schedule template, compliance checklist — capture leads

**Target Industries (Initial):**
1. HVAC / Plumbing / Electrical (service fleets)
2. Construction (mixed fleets)
3. Courier / Local delivery
4. Property management / Landscaping

### Phase 2: Channel Partnerships (Months 6-12)

- **GPS hardware resellers:** Partner with Queclink, CalAmp dealers — they sell hardware, bundle FleetPulse subscription
- **Insurance agents:** Commercial auto insurance brokers recommend FleetPulse for fleet visibility (we provide data for premium discounts)
- **Accounting firms:** QuickBooks ProAdvisors and accountants serving SMBs with fleet expenses
- **Industry associations:** NAFA, local fleet manager associations — sponsorships and webinars

### Phase 3: Product-Led Growth (Months 9-18)

- **Freemium tier:** Free for up to 5 vehicles (tracking + basic maintenance only) — convert to paid as fleets grow
- **Referral program:** $200 credit per referred customer who activates
- **Self-serve onboarding:** Video tutorials, guided setup wizard, sample data import

---

## 11. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| **GPS hardware fragmentation** — supporting many device APIs is complex | High | Medium | Start with 3-5 most popular SMB trackers + smartphone fallback; build abstraction layer |
| **Low switching costs** — SMBs may churn to cheaper alternatives | Medium | High | Focus on data gravity (years of maintenance history), workflow lock-in, and continuous value delivery |
| **Samsara/Geotab move downmarket** — enterprise players launch SMB tiers | Medium | High | Move fast to build brand and community in SMB; they'll struggle with SMB economics and support |
| **Smartphone GPS accuracy** — insufficient for geofencing/route tracking | Medium | Medium | Use smartphone as entry-level only; recommend hardware upgrade path for precision use cases |
| **Fuel card API reliability** — third-party integrations break | Medium | Low | Build robust error handling, manual entry fallback, monitor API health |
| **Driver adoption resistance** — drivers refuse to use mobile app | High | Medium | Minimal required actions for drivers; gamification; show driver benefit (simplified DVIRs, navigation) |

---

## 12. Roadmap

### MVP (Months 0-4)
- Core: Vehicle tracking (3 GPS providers + smartphone), live map dashboard
- Core: Maintenance scheduling with alerts and work orders
- Core: Fuel logging (manual + receipt OCR)
- Core: Driver profiles with license/cert tracking
- Core: Mobile app (iOS + Android) for drivers
- Core: Basic dashboard and 5 pre-built reports
- Infrastructure: Multi-tenant SaaS, auth, billing (Stripe)

### V1.0 (Months 5-8)
- Compliance module (registration, inspection, insurance tracking)
- Fuel card integrations (WEX, Fuelman)
- Geofencing and route history
- Advanced reporting and TCO calculator
- QuickBooks integration
- Driver behavior scoring
- API for custom integrations

### V1.5 (Months 9-12)
- ELD partner integrations (HOS compliance)
- IFTA reporting
- Predictive maintenance alerts (OBD-II integration)
- Custom report builder
- Zapier connector
- Freemium tier launch
- White-label option for GPS hardware resellers

### V2.0 (Months 13-18)
- Dispatch and scheduling module
- Fleet optimization intelligence (right-sizing, replacement recommendations)
- AI-powered insights ("Your fleet's fuel costs are 12% above industry average — here's why")
- Insurance data export and broker partnerships
- Multi-language support (Spanish priority)
- EV fleet support (charging tracking, range monitoring)

---

## Appendix A: Key Assumptions

1. SMB fleet operators are willing to pay $12-35/vehicle/month for an all-in-one solution
2. Smartphone GPS is accurate enough for basic tracking use cases (within 10-15m)
3. 70%+ of target SMB fleets already have some form of GPS hardware installed
4. Driver adoption can reach 60%+ within 90 days of account activation
5. Fuel card providers will grant API access for integration
6. Average customer will expand from Starter to Professional tier within 6 months

## Appendix B: Open Questions

1. Should we build our own low-cost GPS tracker ($50-80 hardware) for fleets with no existing devices?
2. What is the minimum viable compliance feature set to differentiate from Fleetio?
3. Should the freemium tier be available at launch or post-PMF?
4. How do we handle fleets that span multiple countries (Canada + US border fleets)?
5. What is the right level of driver behavior monitoring without being perceived as "surveillance"?
