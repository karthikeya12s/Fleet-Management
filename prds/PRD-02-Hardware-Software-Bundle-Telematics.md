# PRD-02: Unified Hardware + Software Telematics Platform

**Product Name:** FleetNode
**Document Version:** 1.0
**Date:** January 29, 2026
**Author:** Product Management
**Status:** Draft

---

## 1. Overview

FleetNode is an all-in-one telematics hardware device bundled with a cloud software platform that eliminates "device fatigue" in commercial fleets. A single ruggedized unit replaces the 3-5 separate devices (GPS tracker, dashcam, ELD, OBD-II scanner, driver behavior monitor) currently installed in most commercial trucks, providing unified data collection, edge AI processing, and a single dashboard for fleet operators.

**Business Model:** Hardware sold at cost or subsidized + monthly per-vehicle software subscription generating recurring revenue.

---

## 2. Problem Statement

### The Device Fatigue Crisis in Commercial Trucking

Commercial trucking fleets face compounding costs and complexity from fragmented telematics hardware:

- **$74 billion annual cost of vehicle downtime** across the US trucking industry (American Trucking Associations). The average cost of a single truck breakdown is **$448-$760 per incident**, with fleets averaging 1-2 unplanned breakdowns per truck per year.

- **Device proliferation:** A typical Class 8 truck has **3-5 separate aftermarket devices** installed:
  - GPS tracker (fleet visibility)
  - Forward-facing dashcam (liability protection)
  - ELD device (HOS compliance — federally mandated since 2019)
  - OBD-II/J1939 diagnostic reader (maintenance)
  - Driver-facing camera or behavior monitor (insurance requirements)

- **Cost multiplication:** Each device carries its own subscription ($15-45/month each), totaling **$75-225/vehicle/month** for full coverage. A 200-truck fleet spends **$180,000-$540,000/year** on telematics subscriptions alone, across 3-5 separate vendors.

- **Data silos destroy insight:** GPS data in one system, video in another, diagnostics in a third. Fleet managers cannot correlate a hard-braking event (behavior system) with dashcam footage (video system) with the vehicle's brake pad wear data (diagnostic system). This correlation is exactly what prevents accidents and predicts failures.

- **Driver frustration:** Drivers deal with multiple screens, multiple apps, multiple login credentials. The Owner-Operator Independent Drivers Association (OOIDA) surveys show device clutter is a top-5 driver complaint. Each device has different mounting requirements, power draws, and failure modes.

- **IT burden:** Fleet IT teams manage firmware updates, troubleshoot connectivity issues, and handle warranty claims across multiple vendors with different support models. Average fleet IT spending on telematics device management is **$150-$300 per vehicle per year** (Frost & Sullivan).

- **Predictive diagnostics gap:** Current telematics devices collect location data well but poorly integrate vehicle health data. Only 12% of commercial fleets use predictive maintenance effectively (McKinsey), despite the technology being available. The missing link is unified hardware that captures both operational and diagnostic data streams simultaneously.

### Market Opportunity

- **US commercial vehicle telematics market:** $8.2B in 2024, projected $14.5B by 2028 (MarketsandMarkets)
- **Total addressable vehicles:** 15.5M commercial vehicles in the US, 37M in North America
- **Hardware replacement cycle:** 3-5 years — current generation of first-wave ELD devices (2017-2019) are reaching end-of-life
- **Target market:** 3.5M Class 3-8 vehicles in fleets of 20-2,000 vehicles
- **Revenue opportunity:** $3.5M vehicles x $45/month average = $1.89B ARR at maturity

---

## 3. Target Users & Personas

### Primary Persona: Fleet Operations Director

**Name:** James Walker
**Role:** VP of Operations, regional LTL carrier
**Fleet Size:** 350 Class 8 trucks + 200 trailers
**Age:** 47

**Current Pain:**
- Managing 4 telematics vendors (Geotab for GPS, Lytx for cameras, Motive for ELD, Cummins for engine diagnostics)
- Paying $165/truck/month across all subscriptions
- Cannot correlate driver behavior events with vehicle diagnostic data
- 2 full-time IT staff dedicated to telematics device management
- Average of 8% device failure rate requiring truck visits to swap hardware

**Goals:**
- Single vendor, single device, single dashboard
- Reduce telematics cost to <$80/truck/month
- Predictive maintenance to reduce breakdowns by 30%
- AI-powered safety coaching from combined camera + behavior data
- Self-installing device (reduce installation cost from $200 to $0)

### Secondary Persona: Safety Manager

**Name:** Diane Morales
**Role:** Director of Safety, food distribution company
**Fleet Size:** 180 refrigerated trucks

**Current Pain:**
- Cannot get unified safety scores combining driving behavior + video evidence
- Insurance carrier demands video proof of driver coaching — requires manual export from Lytx and cross-referencing with behavior scores from a different system
- FMCSA CSA scores are borderline; needs better data to improve
- Accident reconstruction requires pulling data from 3 systems

**Goals:**
- Single safety score per driver combining all data sources
- Automated video clip extraction tied to safety events
- Insurance-ready safety reports in one click
- Real-time coaching alerts to drivers in cab

### Tertiary Persona: Maintenance Manager

**Name:** Carlos Reyes
**Role:** Fleet Maintenance Manager, utility company
**Fleet Size:** 400 mixed vehicles (trucks, vans, bucket trucks)

**Current Pain:**
- Diagnostic data only available when vehicle is in the shop (no remote monitoring)
- Unplanned breakdowns cost his fleet $2.1M last year
- Fault codes generate too many alerts — 80% are false positives without context
- Cannot prioritize which vehicles need immediate attention

**Goals:**
- Remote vehicle health monitoring in real-time
- Intelligent fault code analysis (severity ranking, not just raw codes)
- Predictive failure alerts with confidence scores
- Maintenance scheduling integrated with vehicle health data

---

## 4. Business Model Details

### Pricing Structure

**Hardware:**

| Device | MSRP | Cost to Build (COGS) | Margin | Strategy |
|--------|------|---------------------|--------|----------|
| **FleetNode Core** (GPS + OBD/J1939 + accelerometer + cellular) | $199 | $120 | 40% | Entry-level, self-install |
| **FleetNode Pro** (Core + forward-facing AI dashcam) | $349 | $210 | 40% | Most popular SKU |
| **FleetNode Max** (Pro + driver-facing camera + cabin sensor) | $499 | $300 | 40% | Full safety suite |

**Hardware Acquisition Options:**
- **Purchase outright:** Full MSRP
- **Subsidized with 3-year contract:** Device at 50% MSRP (recovered through subscription margin)
- **Hardware-as-a-Service:** $0 upfront, $10-15/month hardware fee added to subscription (36-month commitment)

**Software Subscription:**

| Tier | Price/Vehicle/Month | Includes |
|------|-------------------|----------|
| **Track** | $25 | GPS tracking, geofencing, basic alerts, trip history, mobile app |
| **Protect** | $40 | Track + dashcam management, AI safety events, driver scoring, ELD/HOS compliance |
| **Predict** | $55 | Protect + predictive maintenance, fault code intelligence, vehicle health scoring, advanced analytics, API access |

### Unit Economics Per Vehicle (Predict Tier, 3-Year Contract)

| Item | Value |
|------|-------|
| Hardware revenue (subsidized Pro device) | $175 (one-time) |
| Hardware COGS | $210 |
| **Hardware margin** | **-$35 (subsidized)** |
| Monthly subscription | $55 |
| Hosting/data costs per vehicle | ~$5/month |
| **Monthly gross margin** | **$50/month (91%)** |
| **36-month subscription revenue** | **$1,980** |
| **36-month gross profit per vehicle** | **$1,765** |
| **Blended 3-year margin** | **82%** |

### Revenue Model Summary

| Revenue Stream | % of Revenue (Steady State) |
|---------------|---------------------------|
| Software subscriptions | 75% |
| Hardware sales | 15% |
| Professional services (installation, training) | 5% |
| Data services (insurance APIs, benchmarking) | 5% |

### Revenue Projections

| Year | Vehicles Deployed | Hardware Revenue | Subscription ARR | Total Revenue |
|------|------------------|-----------------|-----------------|---------------|
| Y1 | 15,000 | $4.5M | $7.2M | $11.7M |
| Y2 | 50,000 | $10.5M | $24.0M | $34.5M |
| Y3 | 120,000 | $21.0M | $57.6M | $78.6M |

---

## 5. Hardware Specifications & Requirements

### FleetNode Pro (Primary SKU)

**Physical:**
- Dimensions: 130mm x 90mm x 35mm
- Weight: <250g
- Operating temperature: -30C to +70C
- IP67 rated (dust/water resistant)
- Mounting: Windshield mount (dashcam) + OBD/J1939 cable to vehicle port
- LED indicators: Power, GPS, cellular, recording status

**Connectivity:**
- Cellular: 4G LTE Cat-4 with 3G/2G fallback; 5G-ready antenna design
- Wi-Fi: 802.11ac for bulk video offload at depot
- Bluetooth 5.0: For driver ID (phone proximity), peripheral sensors
- GPS/GNSS: Multi-constellation (GPS + GLONASS + Galileo), <2.5m accuracy

**Processing:**
- SoC: Qualcomm QCS6490 or equivalent (8-core, NPU for edge AI)
- RAM: 4GB LPDDR4X
- Storage: 128GB eMMC (local video buffer — ~72 hours of event-triggered recording)
- Edge AI: Capable of running 3-5 concurrent ML models (drowsiness, distraction, tailgating, lane departure, forward collision)

**Camera (Forward-Facing):**
- Resolution: 1080p @ 30fps (recording), 4K stills for events
- FoV: 140 horizontal
- Night vision: IR illumination + low-light sensor (Sony IMX462 or equivalent)
- HDR: Multi-exposure HDR for tunnel/bright transitions

**Vehicle Interface:**
- OBD-II (passenger/light-duty) and J1939/J1708 (heavy-duty) support
- CAN bus reader: 500kbps + 250kbps
- Fault code reading: Full DTC library
- PID monitoring: RPM, coolant temp, oil pressure, fuel level, battery voltage, throttle position, turbo boost, transmission temp, exhaust temp, DEF level

**Power:**
- Vehicle power: 12V/24V DC input with surge protection
- Internal battery: 500mAh LiPo (graceful shutdown, theft alert if disconnected)
- Power consumption: <3W typical, <6W peak (video recording + cellular upload)

**Driver-Facing Camera (FleetNode Max Add-On):**
- Resolution: 720p @ 15fps
- IR illumination for nighttime monitoring
- AI models: Drowsiness detection, phone use, seatbelt detection, smoking
- Privacy mode: Audio recording disabled by default, video only processed on-device (events only uploaded)

---

## 6. Software Platform Requirements

### P0 — MVP Features

**6.1 Real-Time Tracking & Map**
- Live fleet map with <10 second latency
- Vehicle breadcrumb trail (configurable density: 1-60 second intervals)
- Geofencing: polygon and circular, unlimited fences
- Alerts: speeding, geofence enter/exit, after-hours use, idle time
- Trip replay with speed graph overlay

**6.2 Dashcam & Video Management**
- Event-triggered recording: hard brake, collision, speeding, manual trigger
- 30-second pre-event + 30-second post-event video clips
- Cloud storage: 90 days of event clips included
- Live video streaming (on-demand, manager-initiated)
- AI event classification: severity scoring (critical, moderate, low)
- Video request queue: request specific time ranges from device buffer

**6.3 ELD / HOS Compliance**
- FMCSA-registered ELD (compliance certification required)
- Automatic driving time detection from vehicle movement
- Driver log editing with audit trail
- Roadside inspection mode (display logs to officers)
- HOS violation alerts (approaching limits)
- Unidentified driving event management

**6.4 Vehicle Diagnostics**
- Real-time fault code monitoring with plain-English descriptions
- Severity classification: critical (stop driving), warning (schedule service), informational
- Battery voltage monitoring with failure prediction
- Engine performance trending (fuel consumption, coolant temp, oil pressure)
- Diagnostic dashboard per vehicle

**6.5 Device Management**
- Remote firmware updates (OTA)
- Device health monitoring (connectivity status, GPS signal, camera function)
- Self-diagnostic mode for troubleshooting
- Remote reboot capability
- Automatic configuration push (new device activates with fleet settings)

**6.6 Driver Scoring**
- Composite safety score (0-100) per driver per week
- Event categories: hard braking, rapid acceleration, speeding, cornering, phone distraction, drowsiness
- Trend tracking: improving/declining over time
- Leaderboard: fleet ranking (optional, configurable)
- Coaching workflows: review event → assign coaching → track improvement

### P1 — Post-Launch (3-6 months)

**6.7 Predictive Maintenance Engine**
- ML models for component failure prediction:
  - Battery failure (12V/24V starting battery)
  - Brake wear estimation (from deceleration patterns)
  - Tire condition (from vibration patterns)
  - Engine anomaly detection (from CAN bus parameter trending)
  - DPF/aftertreatment system issues
- Confidence scoring: percentage likelihood of failure within 30/60/90 days
- Recommended action: severity + suggested repair + estimated cost
- Integration with maintenance work order systems (Fleetio, TMT Fleet, etc.)

**6.8 Advanced Safety Analytics**
- AI-powered near-miss detection (forward collision warning events)
- Following distance monitoring and coaching
- Accident reconstruction report (GPS + video + g-force + speed data combined)
- Insurance report generation (FNOL automation)
- FMCSA CSA score improvement tracking

**6.9 Fuel Management**
- Fuel consumption tracking from CAN bus data
- MPG trending per vehicle and driver
- Idle fuel waste calculation
- Fuel theft detection (level drops without engine running / GPS at fuel station)
- Fuel card reconciliation (WEX, Comdata integration)

### P2 — Growth Features (6-12 months)

**6.10 AI Coaching**
- In-cab audio coaching for safety events (real-time: "Following distance alert")
- Post-trip safety summary delivered to driver app
- Personalized coaching plans based on individual risk patterns
- Gamification: badges, streaks, team competitions

**6.11 Fleet Benchmarking**
- Anonymous benchmarking against industry peers (same vehicle class, region, fleet size)
- Metrics: fuel efficiency, safety scores, maintenance costs, downtime
- Quarterly benchmark reports

**6.12 Trailer & Asset Tracking**
- Bluetooth asset tags for trailers, equipment, containers
- FleetNode device acts as gateway for nearby BLE sensors
- Cargo temperature monitoring (reefer integration)
- Door open/close sensors
- Trailer GPS position (when connected to tractor)

---

## 7. User Stories & Acceptance Criteria

### US-01: Single Device Installation
**As a** fleet IT manager, **I want to** install one device per vehicle that replaces all existing telematics hardware **so that** I reduce device management overhead by 80%.

**Acceptance Criteria:**
- FleetNode Pro installs in <15 minutes per vehicle with no professional tools
- Windshield mount adhesive + OBD/J1939 cable connection only
- Device auto-provisions upon power-on (detects vehicle type, downloads configuration)
- All features functional within 5 minutes of installation
- Installation guide available via QR code on device packaging

### US-02: Unified Safety Event Review
**As a** safety manager, **I want to** review a safety event with synchronized video, g-force data, speed, and location on a single screen **so that** I can make accurate coaching decisions.

**Acceptance Criteria:**
- Event detail page shows: video clip, map with location, speed graph, g-force graph, driver score impact — all time-synchronized
- Can play forward and road-facing camera side-by-side (FleetNode Max)
- One-click "Coach Driver" action creates a coaching task with event attached
- Can mark event as: valid (coaching needed), false positive (dismiss), or disputed (needs review)
- Event available for review within 5 minutes of occurrence

### US-03: Predictive Breakdown Alert
**As a** maintenance manager, **I want to** receive an alert when a vehicle is likely to break down within 30 days **so that** I can schedule preventive repair before a roadside failure.

**Acceptance Criteria:**
- Alert includes: vehicle ID, predicted component, confidence percentage, estimated time to failure, recommended action, estimated repair cost
- Alert sent via dashboard notification, email, and push notification
- Can convert alert to work order in one click
- Historical accuracy: >70% true positive rate for critical alerts within first year, improving to >85% by year 2
- Alert suppression logic: no repeat alerts for same issue within 7 days unless severity increases

### US-04: ELD Compliance
**As a** driver, **I want** my driving hours to be automatically tracked and my logs to always be compliant **so that** I don't face personal fines or put my CDL at risk.

**Acceptance Criteria:**
- Driving time auto-records when vehicle moves >5 mph for >60 seconds
- Duty status changes (On-Duty, Off-Duty, Sleeper, Driving) editable via mobile app
- HOS clock visible on mobile app: remaining drive time, on-duty time, cycle time
- Warning at 30-minute and 15-minute remaining thresholds
- Roadside inspection mode displays logs per FMCSA format on tablet/phone
- Unidentified driving events flagged to manager within 24 hours

---

## 8. Technical Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                     FLEETNODE DEVICE (EDGE)                    │
│                                                                │
│  ┌─────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────┐   │
│  │ GPS/GNSS│  │ Camera(s)│  │ CAN Bus  │  │ Accelerometer│   │
│  │ Module  │  │ Module   │  │ Interface│  │ / Gyro       │   │
│  └────┬────┘  └────┬─────┘  └────┬─────┘  └──────┬───────┘   │
│       │            │             │                │            │
│       ▼            ▼             ▼                ▼            │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │              EDGE AI PROCESSOR (Qualcomm SoC)           │  │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌───────────┐  │  │
│  │  │ Location │ │ Video AI │ │ Vehicle  │ │ Behavior  │  │  │
│  │  │ Engine   │ │ Pipeline │ │ Health   │ │ Scoring   │  │  │
│  │  │          │ │ (5 models│ │ Monitor  │ │ Engine    │  │  │
│  │  │          │ │  on-chip)│ │          │ │           │  │  │
│  │  └──────────┘ └──────────┘ └──────────┘ └───────────┘  │  │
│  └─────────────────────────────────────────────────────────┘  │
│       │                                                        │
│  ┌────▼────────────────────────────────────────┐              │
│  │  Local Storage (128GB) — Video buffer,      │              │
│  │  offline data queue, model weights           │              │
│  └────┬────────────────────────────────────────┘              │
│       │                                                        │
│  ┌────▼─────┐    ┌───────────┐                                │
│  │ 4G/5G   │    │ Wi-Fi     │ (bulk upload at depot)          │
│  │ Modem   │    │ Module    │                                  │
│  └────┬─────┘    └─────┬─────┘                                │
└───────┼────────────────┼──────────────────────────────────────┘
        │                │
        ▼                ▼
┌──────────────────────────────────────────────────────────────┐
│                        CLOUD PLATFORM                         │
│                                                                │
│  ┌───────────────┐    ┌─────────────────┐                     │
│  │ Data Ingestion│    │  Video Pipeline  │                     │
│  │ (MQTT/Kafka)  │    │  (S3 + Lambda)   │                     │
│  └───────┬───────┘    └────────┬────────┘                     │
│          │                     │                               │
│          ▼                     ▼                               │
│  ┌───────────────────────────────────────┐                    │
│  │         Streaming Processor            │                    │
│  │     (Flink / Kinesis Analytics)        │                    │
│  └───────┬───────────────┬───────────────┘                    │
│          │               │                                     │
│     ┌────▼────┐    ┌────▼──────────┐                          │
│     │TimescaleDB   │ PostgreSQL    │                          │
│     │(telemetry)│  │(fleet config) │                          │
│     └─────────┘    └──────────────┘                           │
│          │               │                                     │
│     ┌────▼───────────────▼──────┐                             │
│     │    ML / Analytics Engine   │                             │
│     │  (Predictive Maintenance,  │                             │
│     │   Fleet Benchmarking,      │                             │
│     │   Anomaly Detection)       │                             │
│     └────────────┬──────────────┘                             │
│                  │                                             │
│     ┌────────────▼──────────────┐                             │
│     │        API Layer           │                             │
│     │   (REST + GraphQL + WS)    │                             │
│     └────────────┬──────────────┘                             │
│                  │                                             │
│     ┌────────────▼──────────────┐                             │
│     │  Web Dashboard + Mobile   │                             │
│     │  Apps + Admin Console     │                             │
│     └───────────────────────────┘                             │
└──────────────────────────────────────────────────────────────┘
```

**Key Architecture Decisions:**

- **Edge-first AI:** All safety-critical ML models run on-device for <100ms latency. Cloud only receives events and metadata, not raw sensor streams (reduces bandwidth 95%).
- **Store-and-forward:** Device buffers all data locally when cellular is unavailable. Automatic sync upon reconnection with priority queue (safety events first).
- **Wi-Fi offload:** High-bandwidth data (requested video clips, firmware updates) transfers over Wi-Fi when vehicle returns to depot, reducing cellular costs 60%.
- **OTA updates:** Device firmware, AI model weights, and configuration all updatable remotely. Staged rollouts with automatic rollback on failure detection.
- **Multi-tenant cloud:** Shared infrastructure with tenant-level data isolation. Regional data residency support for compliance (US, Canada, EU).

---

## 9. Success Metrics & KPIs

### Hardware Metrics

| Metric | Target |
|--------|--------|
| Device failure rate (annual) | <3% |
| Mean time between failures | >36 months |
| Installation time (self-install) | <15 minutes |
| GPS fix time (cold start) | <45 seconds |
| Cellular uptime | >99.5% |
| Edge AI inference latency | <100ms per model |
| Video event upload time | <3 minutes (4G) |

### Software / Business Metrics

| Metric | Target (Y1) | Target (Y2) |
|--------|-------------|-------------|
| Vehicles deployed | 15,000 | 50,000 |
| Subscription ARR | $7.2M | $24M |
| Blended ARPU | $40/veh/mo | $44/veh/mo |
| Monthly churn | <1.5% | <1.0% |
| NPS | 45+ | 55+ |
| Device return rate | <5% | <3% |
| Support tickets per 100 devices/month | <8 | <5 |

### Customer Outcome Metrics

| Metric | Target |
|--------|--------|
| Unplanned breakdown reduction | 25-35% within 12 months |
| Safety event rate reduction | 30-50% within 6 months |
| Telematics cost reduction (vs. multi-vendor) | 40-60% |
| Fleet manager time saved on device management | 70%+ |
| Insurance premium reduction (with safety data) | 10-15% |
| Predictive maintenance true positive rate | >70% (Y1), >85% (Y2) |

---

## 10. Competitive Analysis

| Capability | FleetNode | Geotab GO9 | Samsara AG46 | Motive AI Dashcam | Lytx DriveCam |
|-----------|----------|-----------|-------------|-------------------|---------------|
| **GPS Tracking** | Yes | Yes | Yes | Yes | No |
| **Forward Dashcam** | Yes (Pro/Max) | No (third-party) | Yes | Yes | Yes |
| **Driver-Facing Camera** | Yes (Max) | No | Yes | Yes | Yes |
| **ELD Compliance** | Yes | Via partner | Yes | Yes | No |
| **Vehicle Diagnostics (CAN/J1939)** | Full suite | Full suite | Basic | Basic | No |
| **Edge AI** | Yes (5 models) | Limited | Yes (3 models) | Yes (2 models) | Yes (4 models) |
| **Predictive Maintenance** | Yes (core feature) | Basic (via marketplace) | No | No | No |
| **Self-Install** | Yes | Yes | Yes | Yes | Professional |
| **Single Device** | Yes (all-in-one) | No (camera separate) | Partial (no diagnostics depth) | No (no deep diagnostics) | Camera only |
| **Avg Monthly Cost (all features)** | $55 | $90+ (multi-device) | $70+ | $60+ (no diagnostics) | $45 (camera only) |

### Competitive Positioning

**"One device. One subscription. Complete fleet intelligence."**

FleetNode is the only hardware platform that combines full vehicle diagnostics (CAN bus/J1939), AI dashcam, ELD compliance, and predictive maintenance in a single self-install device. Competitors require 2-4 devices to match this functionality at 40-80% higher total cost.

---

## 11. Manufacturing & Supply Chain

### Manufacturing Strategy

- **Phase 1 (Y1):** Contract manufacturing with a Shenzhen-based OEM (Quectel/Fibocom partner factory). Minimum order quantity: 5,000 units per production run.
- **Phase 2 (Y2):** Dual-source manufacturing (China + Mexico) for supply chain resilience and US-market proximity.
- **Phase 3 (Y3):** Evaluate US-based assembly for "Made in America" positioning (government fleet contracts).

### Bill of Materials (FleetNode Pro)

| Component | Supplier | Unit Cost |
|-----------|----------|-----------|
| Qualcomm QCS6490 SoC | Qualcomm (via distributor) | $35 |
| 4G LTE modem (Quectel EG25-G) | Quectel | $18 |
| Camera module (Sony IMX462) | Sony | $12 |
| GPS module (u-blox M10) | u-blox | $8 |
| Memory (4GB LPDDR4X) | Samsung/Micron | $6 |
| Storage (128GB eMMC) | Samsung/SK Hynix | $10 |
| PCB + passive components | Contract MFG | $8 |
| Enclosure + mount hardware | Injection mold | $5 |
| Cables (OBD/J1939 + power) | Cable assembly | $4 |
| Battery (500mAh LiPo) | BYD/CATL | $3 |
| Assembly + testing + packaging | Contract MFG | $12 |
| Shipping + logistics | Flexport | $4 |
| **Total COGS** | | **~$125** |
| Certifications amortized (FCC, PTCRB, FMCSA ELD) | — | $5/unit (at 50K volume) |
| **Landed Cost** | | **~$130** |

### Quality & Certification Requirements

- FCC Part 15 (US radio emissions)
- PTCRB (cellular carrier certification — AT&T, T-Mobile, Verizon)
- FMCSA ELD certification (if offering ELD feature)
- CE marking (for future EU market)
- SAE J1939 compliance testing
- IP67 environmental testing
- Automotive-grade thermal testing (-30C to +70C, 1000-hour HALT testing)
- Drop test: 1.5m onto concrete, 6 faces

---

## 12. Go-to-Market Strategy

### Phase 1: Direct Sales to Mid-Size Fleets (Months 1-8)

**Target:** Fleets of 50-500 vehicles currently using 3+ telematics vendors
**Value Prop:** "Cut your telematics bill in half while getting better data"

**Sales Motion:**
1. Identify fleets with known multi-vendor setups (trade show leads, LinkedIn targeting)
2. TCO comparison: current multi-vendor cost vs. FleetNode all-in-one
3. 10-vehicle pilot (30 days free) — prove device reliability and data quality
4. Fleet-wide rollout with phased deployment (50 vehicles/week)

**Pricing for pilots:** Free hardware + free 30-day subscription for up to 10 vehicles

### Phase 2: Channel Partners (Months 6-14)

- **Truck dealerships:** Peterbilt, Kenworth, Freightliner dealers as installation + resale partners
- **Leasing companies:** Penske, Ryder — pre-install FleetNode on leased vehicles
- **Insurance carriers:** Recommend FleetNode for premium discounts — we share safety data via API
- **Fleet management companies:** White-label FleetNode for managed fleet service providers

### Phase 3: Self-Serve + SMB (Months 12-18)

- E-commerce store for fleets <50 vehicles
- "Buy device, activate online" model
- Shopify-powered hardware store with subscription activation
- Amazon Business listing for procurement teams

---

## 13. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| **Hardware quality issues at scale** | Medium | Critical | Extensive pre-production testing (HALT/HASS), phased rollout, 2-year warranty with advance replacement |
| **Cellular cost overruns** | Medium | High | Edge AI processing reduces upload volume 95%; Wi-Fi offload for video; negotiate pooled data plans |
| **FMCSA ELD certification delays** | Medium | High | Begin certification process 9 months before launch; hire ELD compliance consultant; offer ELD as Phase 2 feature if delayed |
| **Supply chain disruption** (chip shortage) | Medium | High | 6-month component buffer stock; dual-source critical components; redesign flexibility for alternate SoCs |
| **Competitor price war** | Medium | Medium | Differentiate on predictive maintenance (unique capability); focus on total cost savings vs. per-unit price |
| **Driver privacy backlash** (driver-facing camera) | High | Medium | Privacy-by-design: on-device AI only, events-only upload, no continuous recording to cloud, clear driver communication |
| **Long sales cycle** (6-12 months for mid-fleet) | High | Medium | Offer easy pilot program; build self-serve channel for smaller fleets; case study content marketing |

---

## 14. Roadmap

### MVP (Months 0-6)
- FleetNode Core + Pro hardware (manufactured, certified, shippable)
- GPS tracking, geofencing, trip history
- Forward dashcam with AI event detection (3 models: hard brake, collision, speeding context)
- Basic vehicle diagnostics (fault codes, battery voltage, engine parameters)
- Driver behavior scoring (accelerometer-based)
- Web dashboard + mobile app
- Device management (OTA updates, health monitoring)

### V1.0 (Months 7-12)
- ELD/HOS compliance (FMCSA certified)
- FleetNode Max (driver-facing camera) launch
- Predictive maintenance engine (battery + brake wear + engine anomaly)
- Fuel management (CAN bus consumption tracking)
- Advanced safety analytics + coaching workflows
- Insurance report generation
- Wi-Fi bulk video offload

### V1.5 (Months 13-18)
- Fleet benchmarking (anonymous peer comparison)
- In-cab audio coaching (real-time safety alerts)
- Trailer tracking via BLE gateway
- Integration marketplace (Fleetio, TMT, QuickBooks)
- ADAS-grade features: forward collision warning, lane departure warning
- API for third-party developers

### V2.0 (Months 19-24)
- 5G connectivity option
- V2X communication readiness
- Advanced predictive models: transmission, turbo, aftertreatment, tire
- AI accident reconstruction (automated FNOL report)
- White-label program for leasing companies and fleet management providers
- International expansion (Canada, UK, EU)

---

## Appendix A: Key Assumptions

1. Commercial fleets averaging 3+ telematics devices per vehicle will consolidate to a single device given equivalent functionality at lower cost
2. Qualcomm QCS6490 or equivalent SoC provides sufficient edge AI compute for 5 concurrent models
3. 128GB local storage provides adequate video buffer for 72+ hours of event recording
4. FMCSA ELD certification is achievable within 9-12 months
5. Cellular data costs will average <$3/vehicle/month with edge processing and Wi-Fi offload
6. Self-installation by fleet maintenance staff is viable for 90%+ of vehicle types
7. Predictive maintenance ML models can achieve >70% true positive rate within 12 months with sufficient training data

## Appendix B: Open Questions

1. Should we offer a camera-less SKU (Core only) for fleets that only need tracking + diagnostics?
2. What is the right warranty period — 2 years standard or 3 years to match contract length?
3. Should we pursue FMCSA ELD certification in-house or partner with a certified ELD provider?
4. How do we handle the chicken-and-egg problem for predictive maintenance ML models (need data to train, need devices deployed to get data)?
5. Should cellular connectivity be included in subscription price or billed separately?
