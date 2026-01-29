# Product Management Exercises: SaaS Fleet Management Platform (FleetPulse)

> Exercises mapped to the Fleet Management Learning Roadmap phases.
> Reference PRD: `PRD-01-SaaS-Fleet-Management-Platform.md`

---

## Phase 1: Foundation — Business & Ecosystem Understanding

### Exercise 1.1: Market Sizing (TAM/SAM/SOM)
**Objective:** Build a bottoms-up market sizing model for a SaaS fleet management platform targeting SMB fleets.

**Task:**
1. Research and estimate the number of commercial fleets in the US by size bracket (1-9, 10-49, 50-199, 200-499, 500+ vehicles)
2. Estimate SaaS penetration rates for each bracket today
3. Define your TAM, SAM, and SOM with assumptions documented
4. Calculate the revenue opportunity at $12, $22, and $35/vehicle/month price points
5. Identify the 3 biggest assumptions that could be wrong and how they'd change your numbers

**Deliverable:** A 2-page market sizing document with a spreadsheet model. Present it as if pitching to a VC partner.

**Evaluation Criteria:**
- [ ] Uses multiple credible data sources (ATRI, IHS Markit, BLS, Census SUSB)
- [ ] Bottom-up and top-down estimates within 2x of each other
- [ ] Assumptions are explicit and testable
- [ ] Sensitivity analysis on key assumptions

---

### Exercise 1.2: Competitive Teardown
**Objective:** Deeply analyze one direct competitor to understand positioning, pricing, and product gaps.

**Task:**
1. Sign up for a free trial or demo of **Fleetio** (the closest SMB competitor)
2. Document every feature, screen, and workflow you encounter
3. Map Fleetio's features to the PRD's P0/P1/P2 priorities — what does Fleetio do well? What's missing?
4. Analyze Fleetio's pricing page: what are the tiers, what's gated, what's the implied ARPU?
5. Read 20 Fleetio reviews on G2/Capterra — categorize complaints into themes
6. Write a 1-page "Competitive Brief" summarizing: strengths, weaknesses, positioning, pricing, and the #1 opportunity FleetPulse has against Fleetio

**Deliverable:** Competitive brief + annotated screenshots of Fleetio's product.

**Evaluation Criteria:**
- [ ] Feature map is exhaustive (not surface-level)
- [ ] Review analysis identifies real patterns (not cherry-picked)
- [ ] Competitive brief is actionable (could inform roadmap decisions)
- [ ] Identifies at least one non-obvious insight

---

### Exercise 1.3: Customer Discovery Interview Script
**Objective:** Design and conduct customer discovery for SMB fleet managers.

**Task:**
1. Write a 15-question interview script for a 30-minute call with an SMB fleet manager (50-150 vehicles). Focus on:
   - Current tools and workflows (what do they use today?)
   - Time spent on fleet admin (quantify the pain)
   - Top 3 frustrations (rank order)
   - Willingness to pay (price sensitivity signals)
   - Decision-making process (who approves software purchases?)
2. Conduct 3 interviews (find fleet managers via LinkedIn, Reddit r/FleetManagement, or local business contacts)
3. Synthesize findings into a "Customer Discovery Summary" with quotes, themes, and surprises

**Deliverable:** Interview script + synthesis document with direct quotes.

**Evaluation Criteria:**
- [ ] Questions are open-ended (not leading)
- [ ] Follows Jobs-to-be-Done framework
- [ ] Avoids asking about solutions (focuses on problems)
- [ ] Synthesis identifies patterns across interviews

---

### Exercise 1.4: TCO Framework Construction
**Objective:** Build a Total Cost of Ownership model for a 75-vehicle service fleet.

**Task:**
1. Research and itemize all fleet cost categories: fuel, maintenance (preventive + unplanned), insurance, depreciation, registration/compliance, tolls/violations, driver costs (if applicable), admin overhead
2. Assign realistic dollar amounts per vehicle per year for each category (cite sources)
3. Calculate total fleet TCO and cost-per-mile
4. Identify which cost categories FleetPulse can directly impact and estimate reduction potential
5. Build an ROI calculator: "FleetPulse costs $X/year, saves $Y/year, ROI = Z months"

**Deliverable:** Spreadsheet TCO model + 1-page ROI summary suitable for a sales deck.

**Evaluation Criteria:**
- [ ] All major cost categories included
- [ ] Assumptions sourced from industry benchmarks (ATRI, NAFA, Fleetio reports)
- [ ] ROI claims are conservative and defensible
- [ ] Model is reusable (input fleet size, get output)

---

## Phase 2: Technical Stack Deep Dive

### Exercise 2.1: Data Architecture Design
**Objective:** Design the data model and ingestion pipeline for FleetPulse's vehicle tracking system.

**Task:**
1. Design a PostgreSQL database schema for:
   - Tenants (fleet accounts)
   - Vehicles (make, model, year, VIN, status, assigned driver)
   - Drivers (name, license info, certifications, assigned vehicle)
   - Location events (timestamp, lat/lng, speed, heading, vehicle_id)
   - Maintenance records (vehicle_id, service type, vendor, cost, date, mileage)
2. Explain why you chose a relational DB for core data and time-series DB (TimescaleDB) for location events
3. Design the data flow: GPS device → API → message queue → processing → storage → dashboard
4. Calculate storage requirements for 10,000 vehicles reporting every 30 seconds for 1 year
5. Identify the top 3 scalability bottlenecks and how you'd address them

**Deliverable:** ER diagram + data flow diagram + storage calculation + written analysis.

**Evaluation Criteria:**
- [ ] Schema supports multi-tenancy correctly
- [ ] Time-series data separated from transactional data with clear rationale
- [ ] Storage calculation is realistic (consider data compression)
- [ ] Scalability bottlenecks are real (not theoretical)

---

### Exercise 2.2: API Design for GPS Integration
**Objective:** Design the API contract for ingesting GPS data from third-party tracking devices.

**Task:**
1. Research 3 GPS tracker APIs (Geotab, CalAmp, Queclink) — document their data formats and push/pull mechanisms
2. Design a normalized FleetPulse ingestion API that can accept data from any GPS provider
3. Write the API specification (OpenAPI/Swagger) for:
   - `POST /api/v1/locations` (batch location upload)
   - `GET /api/v1/vehicles/{id}/location` (current location query)
   - `GET /api/v1/vehicles/{id}/trips` (trip history)
4. Define error handling, authentication (API keys vs. OAuth), and rate limiting
5. Design the "adapter pattern" for adding new GPS hardware providers without changing core code

**Deliverable:** OpenAPI spec document + adapter pattern diagram + comparison table of 3 GPS provider APIs.

**Evaluation Criteria:**
- [ ] API handles real-world data quality issues (out-of-order events, duplicates, GPS drift)
- [ ] Authentication model is appropriate for IoT devices
- [ ] Adapter pattern enables adding a new provider in <1 week of dev effort
- [ ] Rate limiting prevents abuse without blocking legitimate high-frequency data

---

### Exercise 2.3: Build a Tracking Prototype
**Objective:** Build a minimal working vehicle tracking system.

**Task:**
1. Create a simple web app that:
   - Displays a map (Mapbox or Leaflet.js)
   - Accepts location data via REST API
   - Plots vehicle positions in real-time (use WebSocket or polling)
   - Shows vehicle breadcrumb trail (last 50 positions)
2. Simulate 5 vehicles sending GPS data (write a script that generates realistic lat/lng coordinates moving along roads)
3. Add geofencing: draw a polygon on the map, alert when a vehicle enters/exits

**Deliverable:** Working prototype (GitHub repo) + README with architecture decisions.

**Evaluation Criteria:**
- [ ] Map renders correctly with real-time position updates
- [ ] Multiple vehicles displayed simultaneously
- [ ] Geofencing works with polygon intersection detection
- [ ] Code is clean, documented, and demonstrates architectural thinking

---

## Phase 3: Domain Expertise

### Exercise 3.1: Maintenance Workflow PRD Drill
**Objective:** Write a detailed feature spec for the preventive maintenance scheduling system.

**Task:**
You are the PM for FleetPulse. The CEO says: "Our customers' #1 request is better maintenance scheduling. I want this shipped in 6 weeks." Write a feature spec that includes:

1. **Problem framing:** What specific maintenance problems do SMB fleets face? (Use insights from Phase 1 interviews or research)
2. **User stories:** Write 8-10 user stories covering the full maintenance lifecycle (schedule → notify → execute → track → report)
3. **Wireframes:** Sketch (hand-drawn or Figma) the 5 key screens:
   - Maintenance calendar view
   - Create/edit maintenance schedule
   - Work order detail page
   - Driver mobile DVIR form
   - Maintenance cost dashboard
4. **Edge cases:** Document 10 edge cases (e.g., vehicle exceeds mileage interval before time interval, driver skips DVIR, vendor invoice doesn't match PO)
5. **Success metrics:** How will you measure if this feature is working?
6. **Cut list:** What did you intentionally leave out of the 6-week scope and why?

**Deliverable:** 5-page feature spec with wireframes.

**Evaluation Criteria:**
- [ ] User stories are specific and testable (clear acceptance criteria)
- [ ] Wireframes are usable (not just boxes — show real field labels, states, flows)
- [ ] Edge cases reveal deep domain understanding
- [ ] Cut list shows strategic scoping ability (knows what NOT to build)

---

### Exercise 3.2: Fuel Management Product Strategy
**Objective:** Define the product strategy for FleetPulse's fuel tracking module.

**Task:**
1. Research how SMB fleets currently track fuel (manual logs, fuel cards, nothing)
2. Analyze 3 fuel card providers (WEX, Fuelman, Comdata) — what data do their APIs provide?
3. Design a phased fuel management feature:
   - **Phase A:** Manual fuel logging + receipt OCR (2 weeks to build)
   - **Phase B:** Fuel card integration with automated import (4 weeks)
   - **Phase C:** Fuel analytics and anomaly detection (4 weeks)
4. For each phase, define: features, user stories, technical dependencies, and success metrics
5. Build a business case: if fuel tracking reduces fuel costs by 8-12%, what's the dollar impact for a 75-vehicle fleet? How does this justify the subscription price?

**Deliverable:** 3-page product strategy document with phased roadmap and business case.

---

### Exercise 3.3: Compliance Feature Prioritization (RICE Framework)
**Objective:** Prioritize compliance features using the RICE scoring framework.

**Task:**
You have 15 compliance-related feature requests from customers and the sales team. Score each using RICE (Reach, Impact, Confidence, Effort) and create a prioritized backlog.

**Feature Requests:**
1. Vehicle registration expiration tracking and alerts
2. Annual inspection scheduling
3. Driver license expiration tracking
4. ELD/HOS compliance dashboard (requires partner integration)
5. IFTA fuel tax reporting
6. DOT medical card tracking
7. Insurance certificate management
8. DVIR digital form submission
9. Toll violation management
10. OSHA compliance checklists
11. Title and plate management
12. Emissions inspection tracking
13. Automated DMV registration renewal (e-filing)
14. Drug/alcohol testing compliance tracking
15. CSA score monitoring and improvement recommendations

For each feature:
- **Reach:** How many customers request or would use this? (per quarter)
- **Impact:** How much does this move the needle? (0.25=minimal, 3=massive)
- **Confidence:** How certain are you of your estimates? (50-100%)
- **Effort:** Person-months to build

**Deliverable:** RICE scoring spreadsheet with rank-ordered backlog + 1-page rationale for your top 5.

**Evaluation Criteria:**
- [ ] Scores are justified with reasoning (not arbitrary numbers)
- [ ] Reach estimates backed by customer research or market data
- [ ] Effort estimates are realistic (consulted with engineers or used analogous features)
- [ ] Top 5 rationale tells a coherent product story (not just "highest score wins")

---

## Phase 4: Advanced Topics

### Exercise 4.1: EV Fleet Feature Design
**Objective:** Design FleetPulse's EV fleet management extension.

**Task:**
A growing number of SMB fleets are adding EVs (starting with 5-20 vehicles). Design the EV-specific features FleetPulse needs:

1. **Research:** What's different about managing EVs vs. ICE vehicles? (maintenance schedule, fuel/energy tracking, range management, charging infrastructure)
2. **Feature design:** Specify 5 EV-specific features:
   - Battery State of Health (SoH) tracking
   - Charging session logging and cost tracking
   - Range monitoring with low-range alerts
   - EV-specific maintenance schedules (simplified — no oil changes)
   - Energy cost per mile vs. fuel cost per mile comparison
3. **Data requirements:** What data do you need from EVs that's different from ICE? How do you get it?
4. **Pricing impact:** Should EV fleet management be a premium add-on or included in existing tiers? Justify.
5. **Competitive landscape:** How do Geotab, Samsara, and Fleetio handle EV fleets today?

**Deliverable:** 4-page EV feature design document.

---

### Exercise 4.2: Predictive Maintenance ML Product Spec
**Objective:** Write a product spec for an ML-powered predictive maintenance feature that a PM (not an engineer) could hand to a data science team.

**Task:**
1. Define the problem: what does "predictive maintenance" mean for an SMB fleet with basic OBD-II data (not full J1939 CAN bus)?
2. Specify the ML product requirements:
   - **Input data:** What signals are available? (mileage, fault codes, maintenance history, fuel consumption trends, driving behavior)
   - **Output:** What should the model predict? (component failure probability? Days to next unplanned repair? Maintenance urgency score?)
   - **User experience:** How should predictions be displayed? When should alerts fire? What actions should the user take?
   - **Accuracy requirements:** What false positive rate is acceptable? (Too many false alarms = alert fatigue. Too few = missed failures.)
   - **Cold start:** How does the system work for a new fleet with no historical data?
3. Define success metrics: how will you measure if predictive maintenance is working?
4. Outline the training data strategy: where does the training data come from? How much is needed?
5. Sketch the user flow: fleet manager sees a prediction → takes action → provides feedback → model improves

**Deliverable:** 4-page ML product spec (no code, no model architecture — pure product requirements).

**Evaluation Criteria:**
- [ ] Clearly separates product requirements from implementation details
- [ ] Addresses cold start problem practically
- [ ] False positive / false negative tradeoff is explicitly discussed
- [ ] Success metrics are measurable and meaningful to the business

---

### Exercise 4.3: Platform Strategy — Build vs. Partner vs. Integrate
**Objective:** Make a strategic recommendation for how FleetPulse should approach ELD/HOS compliance.

**Task:**
FleetPulse customers want ELD compliance. You have 3 options:

| Option | Description | Effort | Risk |
|--------|-----------|--------|------|
| **Build** | Build native ELD functionality, get FMCSA certified | 12+ months, $1M+ | Certification risk, regulatory complexity |
| **Partner** | White-label an existing ELD (Motive, KeepTruckin) inside FleetPulse | 3-4 months | Dependency on partner, margin sharing |
| **Integrate** | API integration with popular ELDs — pull data into FleetPulse dashboard | 4-6 weeks per integration | No native ELD, weaker experience |

Write a recommendation memo to the CEO that:
1. Analyzes all 3 options across: time-to-market, cost, user experience, competitive defensibility, revenue impact, risk
2. Recommends one option with clear rationale
3. Identifies what would need to be true for your recommendation to be wrong (reversibility analysis)
4. Proposes a decision timeline and milestones

**Deliverable:** 2-page executive memo.

**Evaluation Criteria:**
- [ ] All options analyzed fairly (not straw-manned)
- [ ] Recommendation aligns with FleetPulse's stage and strategy (early-stage SMB SaaS)
- [ ] Reversibility analysis shows intellectual honesty
- [ ] Memo is concise and decision-ready (CEO can say yes/no after reading it)

---

## Phase 5: Product & Business Strategy

### Exercise 5.1: Pricing Strategy Optimization
**Objective:** Redesign FleetPulse's pricing page to maximize conversion and revenue.

**Task:**
1. Analyze 5 SaaS pricing pages in adjacent markets (Fleetio, Samsara, HubSpot, Gusto, ServiceTitan) — what patterns do you see?
2. Critique FleetPulse's current 3-tier pricing from the PRD:
   - Is $12/vehicle too low for Starter? (anchor effect vs. margin)
   - Is the Starter→Professional jump too big? ($12 to $22)
   - What features should gate each tier? (which features drive upgrades?)
3. Design an alternative pricing model:
   - Option A: Usage-based (base fee + per-feature add-ons)
   - Option B: Tiered with different gating strategy
   - Option C: Reverse trial (start on Pro, downgrade after 30 days)
4. For your recommended model, calculate: expected ARPU, conversion rate assumptions, and projected revenue for 500 customers
5. Design the actual pricing page (wireframe or mockup)

**Deliverable:** Pricing analysis + recommended pricing model + pricing page mockup.

---

### Exercise 5.2: Go-to-Market Experiment Design
**Objective:** Design 3 experiments to test FleetPulse's go-to-market hypotheses.

**Task:**
FleetPulse has 3 key GTM hypotheses:
- **H1:** SMB fleet managers will self-serve sign up without talking to sales
- **H2:** A free fleet TCO calculator will generate qualified leads
- **H3:** LinkedIn ads targeting "Fleet Manager" title will convert at >2% CTR

For each hypothesis, design an experiment:
1. **Test design:** What specifically will you do? (landing page, ad campaign, outbound emails)
2. **Success metric:** What number tells you the hypothesis is true or false?
3. **Sample size:** How many data points do you need for statistical significance?
4. **Timeline:** How long will the experiment run?
5. **Budget:** What will it cost?
6. **Kill criteria:** At what point do you abandon the hypothesis?

**Deliverable:** 3-page experiment plan with clear pass/fail criteria.

---

### Exercise 5.3: Churn Analysis & Retention Strategy
**Objective:** Predict and prevent churn for a SaaS fleet management platform.

**Task:**
Assume FleetPulse has been live for 12 months with 200 customers. Monthly logo churn is 3.5% (target is <2%). You need to diagnose and fix this.

1. **Churn segmentation:** What dimensions would you segment churn by? (fleet size, tier, industry, tenure, feature adoption, support tickets, last login)
2. **Leading indicators:** Define 5 early warning signals that predict a customer will churn in 30-60 days
3. **Churn interview script:** Write 10 questions for churned customer exit interviews
4. **Retention playbook:** Design interventions for each churn segment:
   - "Never activated" (signed up but never configured fleet)
   - "Low engagement" (fewer than 3 logins per week)
   - "Feature-limited" (using only 1-2 of 5 core features)
   - "Support-frustrated" (3+ support tickets in 30 days)
   - "Price-sensitive" (asked about discounts or downgraded tier)
5. **Health score:** Design a customer health score (0-100) using weighted inputs

**Deliverable:** Churn analysis framework + retention playbook + health score model.

---

### Exercise 5.4: Product-Led Growth Funnel Design
**Objective:** Design the complete PLG funnel for FleetPulse.

**Task:**
Design the end-to-end product-led growth funnel:

1. **Awareness → Signup:**
   - What free tools / content attract fleet managers? (TCO calculator, maintenance template, compliance checklist)
   - Design the signup flow (what info do you collect? How few fields as possible?)

2. **Signup → Activation:**
   - What is the "aha moment" for FleetPulse? (seeing their first vehicle on the map? Getting their first maintenance alert?)
   - Design the onboarding checklist (5-7 steps)
   - What should happen in the first 10 minutes? First day? First week?

3. **Activation → Conversion:**
   - What triggers upgrade from free trial to paid?
   - Design 3 in-product prompts that nudge toward paid conversion
   - What usage-based triggers indicate readiness to upgrade?

4. **Conversion → Expansion:**
   - How do you get customers to add more vehicles? Move to a higher tier?
   - Design the expansion motion (in-product prompts, CSM outreach triggers)

**Deliverable:** PLG funnel document with wireframes for key moments (onboarding, upgrade prompts, expansion triggers).

---

## Phase 6: Hands-On Application

### Exercise 6.1: Sprint Planning Simulation
**Objective:** Plan a real 2-week sprint for FleetPulse MVP development.

**Task:**
You have a 5-person engineering team (2 backend, 1 frontend, 1 mobile, 1 QA). You're in Sprint 3 of MVP development. Sprints 1-2 delivered: basic auth, vehicle CRUD, and a static map view.

1. Break down the following MVP features into sprint-sized tickets:
   - Real-time vehicle tracking on the map
   - Maintenance schedule creation and alerts
   - Basic mobile app (driver DVIR submission)
2. For each ticket, write: title, description, acceptance criteria, story points (use Fibonacci), dependencies
3. Assign tickets to team members considering skill sets and dependencies
4. Calculate sprint velocity assumption and determine what fits in 2 weeks
5. Identify the #1 risk to this sprint and your mitigation plan

**Deliverable:** Sprint board (Notion, Jira export, or markdown table) with fully specified tickets.

---

### Exercise 6.2: Launch Readiness Checklist
**Objective:** Create a comprehensive launch checklist for FleetPulse MVP.

**Task:**
FleetPulse MVP is 4 weeks from launch. Create a launch readiness checklist covering:

1. **Product readiness:** Feature completeness, bug severity thresholds, performance benchmarks (page load <2s, API response <500ms, map rendering <3s)
2. **Operational readiness:** Customer support process, escalation path, monitoring/alerting, incident response plan, on-call rotation
3. **Sales readiness:** Sales deck, demo environment, pricing in billing system, CRM configured, first 10 target prospects identified
4. **Marketing readiness:** Website live, SEO basics, launch email to waitlist, 3 blog posts queued, social media posts scheduled
5. **Legal/compliance:** Terms of service, privacy policy, data processing agreement, SOC 2 status
6. **Success criteria:** What does "successful launch" look like at Day 7, Day 30, Day 90?

**Deliverable:** Launch checklist document with owners, due dates, and status tracking.

---

### Exercise 6.3: Post-Launch Metrics Dashboard Design
**Objective:** Design the internal metrics dashboard the FleetPulse team will use daily.

**Task:**
Design a dashboard with 3 views:

1. **Executive view** (CEO/investors check weekly):
   - ARR, MRR growth, customer count, vehicle count
   - Churn rate, NPS, net revenue retention
   - CAC, LTV, payback period
   - Cash runway

2. **Product view** (PM checks daily):
   - DAU/WAU/MAU and ratios
   - Feature adoption rates (% of accounts using each module)
   - Onboarding completion rate (step-by-step funnel)
   - Time-to-value (signup → first vehicle tracked)
   - Top 5 feature requests from support tickets
   - Error rates and performance metrics

3. **Customer success view** (CS team checks daily):
   - Customer health scores (red/yellow/green distribution)
   - Accounts approaching renewal
   - Support ticket volume and resolution time
   - Accounts with declining usage (churn risk)
   - Expansion opportunities (accounts near tier upgrade thresholds)

For each metric: define the calculation formula, data source, update frequency, and alert thresholds.

**Deliverable:** Dashboard wireframes (3 views) + metrics definition document.

---

## Bonus Exercises

### Bonus 1: Write a Product Press Release (Amazon Working Backwards)
Write a press release announcing FleetPulse's launch, dated 6 months from now. Include: headline, subheadline, problem statement, solution, customer quote (fictional), metrics achieved, and CTA. Keep it to 1 page. This forces you to clarify the product's value proposition in plain language.

### Bonus 2: Product Positioning Exercise
Using April Dunford's positioning framework, fill in:
- **Competitive alternatives:** What would customers do if FleetPulse didn't exist?
- **Unique attributes:** What does FleetPulse have that alternatives don't?
- **Value:** What does the unique attribute enable for the customer?
- **Target customer:** Who cares most about the value?
- **Market category:** What context makes the value obvious?

### Bonus 3: Stakeholder Communication
Write 3 different emails communicating the same product decision (delaying ELD feature by 2 months):
1. To the engineering team (technical, empathetic)
2. To the sales team (business impact, alternative talking points)
3. To the CEO (strategic rationale, data-backed)

Each email should be <200 words and appropriate for its audience.
