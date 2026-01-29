# Product Management Exercises: Fleet Services Marketplace (FleetBay)

> Exercises mapped to the Fleet Management Learning Roadmap phases.
> Reference PRD: `PRD-05-Fleet-Services-Marketplace.md`

---

## Phase 1: Foundation — Business & Ecosystem Understanding

### Exercise 1.1: Marketplace Economics — GMV, Take-Rate, and Liquidity
**Objective:** Model the marketplace economics and understand the metrics that matter.

**Task:**
1. **GMV modeling:** Build a bottoms-up GMV model for FleetBay in year 1:
   - Estimate: average fleet (100 vehicles) uses how many external services per month? What's the average transaction value by category?

   | Service Category | Frequency (per 100 vehicles/month) | Avg Transaction Value | Monthly GMV (100-vehicle fleet) |
   |-----------------|-----------------------------------|----------------------|-------------------------------|
   | Oil change / PM service | ? | ? | ? |
   | Tire replacement/repair | ? | ? | ? |
   | Brake service | ? | ? | ? |
   | Body/collision repair | ? | ? | ? |
   | Towing/roadside | ? | ? | ? |
   | Other mechanical repair | ? | ? | ? |
   | **Total** | | | **?** |

   Now multiply by target fleet count to get monthly/annual GMV.

2. **Take-rate sensitivity:** Model revenue at 5%, 8%, 10%, and 12% take-rates. At what take-rate do vendors refuse to participate? (Research: what do DoorDash, Uber, HomeAdvisor, Angi charge?)

3. **Liquidity metrics:** Define and calculate:
   - **Supply liquidity:** If a fleet manager posts a service request, what's the probability a vendor responds within 2 hours? (Depends on vendor density in that metro)
   - **Demand liquidity:** If a vendor is on FleetBay, how many service requests do they receive per week? (Below a threshold, they'll leave)
   - What's the minimum marketplace size (vendors x fleets) per metro for viable liquidity?

4. **Marketplace leakage:** What percentage of transactions will happen "off-platform" (fleet contacts vendor found on FleetBay but transacts directly)? How do you minimize this?

**Deliverable:** GMV model spreadsheet + take-rate analysis + liquidity threshold calculations + leakage assessment.

**Evaluation Criteria:**
- [ ] Service frequencies are realistic (research-backed, not guessed)
- [ ] Take-rate analysis references real marketplace precedents
- [ ] Liquidity thresholds are specific (e.g., "3+ vendor responses per service request")
- [ ] Leakage problem is addressed with concrete countermeasures

---

### Exercise 1.2: Two-Sided Customer Discovery
**Objective:** Conduct customer discovery on BOTH sides of the marketplace.

**Task:**
FleetBay needs to understand both fleet operators (demand) and service providers (supply). Design and ideally conduct discovery for both:

**Demand Side — Fleet Managers:**
1. Write an 8-question interview script focused on:
   - How they find repair shops today (especially in unfamiliar markets)
   - Their worst breakdown experience (how long? how much? how stressful?)
   - How they evaluate vendor quality (word of mouth? trial and error?)
   - Invoice processing pain (how many vendors, how long does reconciliation take?)
   - What would make them try a new platform? (What's the switching cost?)

**Supply Side — Independent Repair Shop Owners:**
1. Write an 8-question interview script focused on:
   - How they acquire new fleet customers today (referrals? cold calling? walk-ins?)
   - What percentage of their bay capacity goes unused? (Idle time)
   - How they handle pricing for fleet accounts (negotiated rates vs. menu pricing)
   - What technology they use (QuickBooks? Paper? Nothing?)
   - What would make them join a marketplace? (What do they fear?)

2. Conduct at least 2 interviews per side (find fleet managers via LinkedIn; find shop owners by visiting local commercial vehicle repair shops)

3. Synthesize findings: What are the top 3 pain points per side? Do they align? Where is the "intersection of pain" that FleetBay solves?

**Deliverable:** Both interview scripts + synthesis document with quotes and pattern analysis.

---

### Exercise 1.3: Marketplace Benchmarking — Lessons from Adjacent Markets
**Objective:** Extract lessons from successful marketplace businesses in adjacent verticals.

**Task:**
Research 4 marketplace businesses and extract lessons applicable to FleetBay:

1. **Angi (HomeAdvisor)** — Home services marketplace
   - How did they solve the cold start problem?
   - What's their take-rate and fee structure? (Lead fee vs. transaction fee)
   - What's their vendor quality enforcement mechanism?
   - Why did the HomeAdvisor/Angi merger struggle?

2. **Uber Freight** — Freight brokerage marketplace
   - How does load matching work? (Parallels to FleetBay's service matching)
   - How did they onboard carriers (supply side)?
   - What pricing transparency features do they offer?
   - What network effects exist in freight matching?

3. **OpenTable** — Restaurant reservation marketplace
   - How did they seed supply? (They gave restaurants free software to manage reservations)
   - What's the business model? (Per-seated-diner fee + subscription for tools)
   - What's their vendor retention strategy?
   - Lesson for FleetBay: should FleetBay give vendors free shop management tools?

4. **Faire** — B2B wholesale marketplace
   - How did they build trust between buyers and sellers who don't know each other?
   - What financial products (payment terms, returns) did they offer to reduce friction?
   - How did they handle geographic expansion?
   - What's their net revenue retention?

For each marketplace: 3 key lessons for FleetBay + 1 warning (what to avoid).

**Deliverable:** 4-marketplace benchmarking report with actionable lessons.

---

## Phase 2: Technical Stack Deep Dive

### Exercise 2.1: Search & Matching Algorithm Design
**Objective:** Design the vendor matching algorithm for both scheduled and emergency service requests.

**Task:**
FleetBay needs two matching modes:

**Mode 1: Scheduled service** (fleet manager has time to compare options)
- Design the search/ranking algorithm. When a fleet manager searches for "brake service, Class 8 truck, within 20 miles":
  1. Define the filter criteria: service type, vehicle compatibility, distance, hours of operation, certifications
  2. Define the ranking formula. Candidates that pass filters are ranked by: distance (closer = better), rating (higher = better), price (lower = better), response time history (faster = better), repeat customer (bonus if fleet has used this vendor before)
  3. Assign weights to each factor. Should distance matter more than rating? Should price matter more than speed?
  4. Design the search results page: what info does the fleet manager see for each vendor? How many results?

**Mode 2: Emergency breakdown** (dispatcher needs help NOW)
- Design the emergency matching algorithm:
  1. Priority changes: availability NOW is #1 (a 5-star shop 30 miles away that's closed is useless)
  2. Push notification to qualified vendors: "Emergency brake repair needed, 2021 Peterbilt 579, I-85 mile marker 142, trailer loaded. Can you help?"
  3. First vendor to accept wins (like Uber driver acceptance)
  4. What if no vendor accepts within 15 minutes? Expand radius? Call vendors directly?
  5. Design the dispatcher's emergency flow (wireframe: 4 key screens)

**Deliverable:** Matching algorithm specification + ranking formula + emergency flow wireframes.

**Evaluation Criteria:**
- [ ] Scheduled ranking balances multiple factors with justified weights
- [ ] Emergency mode prioritizes availability and speed over price/rating
- [ ] Algorithm handles edge cases (no vendors available, vendor accepts then cancels)
- [ ] Search results page shows information that enables decisions

---

### Exercise 2.2: Payment & Invoicing System Design
**Objective:** Design the financial infrastructure for a B2B services marketplace.

**Task:**
FleetBay processes payments between fleet operators and vendors — both businesses with specific financial requirements.

1. **Payment flow design:**
   - Vendor completes service → uploads invoice → fleet approves (or disputes) → FleetBay processes payment → vendor receives funds
   - Design this flow with timing: when does each step happen? What's the maximum time for each?
   - What happens if the fleet operator doesn't approve within 10 days? Auto-approve? Escalate?

2. **Consolidated billing:**
   - Fleet operator wants ONE monthly invoice, not 15 vendor invoices
   - Design the consolidated invoice: line items, subtotals by vendor, subtotals by vehicle, subtotals by service category
   - Payment terms: net-30 for fleet operators (industry standard). FleetBay pays vendors in 3-5 days. This means FleetBay floats ~25 days of cash. Calculate the cash float requirement at $10M monthly GMV.

3. **Vendor payout:**
   - Standard: payment 3-5 business days after fleet approval
   - Early payment option: next-day payment for 1.5% fee (embedded finance revenue)
   - Design the vendor payout dashboard: pending payments, completed payments, upcoming payments, early payment option

4. **Dispute resolution:**
   - Fleet operator says invoice is wrong (wrong parts, overcharges, work not performed)
   - Design the dispute workflow: fleet marks line item disputed → vendor notified → vendor provides evidence → FleetBay mediates → resolution
   - Who holds the funds during a dispute? (Escrow)
   - What's the average dispute rate to plan for? (Research: commercial services industry typically 2-5%)

5. **Stripe Connect implementation:** Research Stripe Connect's "marketplace" model. Map FleetBay's requirements to Stripe Connect features: connected accounts, split payments, delayed payouts, refunds.

**Deliverable:** Payment flow diagram + consolidated invoice wireframe + dispute workflow + Stripe Connect mapping.

---

### Exercise 2.3: "FleetBay Fair Price" Engine Design
**Objective:** Design the pricing transparency engine that calculates fair market prices for fleet services.

**Task:**
FleetBay's pricing transparency is a key differentiator. Fleet managers should know: "A brake job on a 2021 Freightliner Cascadia should cost $1,800-$2,400 in the Dallas metro."

1. **Data requirements:** What transaction data do you need to calculate fair prices?
   - Service type (standardized taxonomy: how do you categorize 1,000+ possible repairs?)
   - Vehicle class and make/model
   - Geography (metro area or zip code level)
   - Parts cost vs. labor cost breakdown
   - Vendor type (independent shop vs. dealer vs. chain)

2. **Methodology:**
   - How do you calculate the "fair price range"? (25th-75th percentile of historical transactions?)
   - How many transactions do you need per service-vehicle-geography combination for statistical significance?
   - How do you handle rare services with few data points? (Extrapolate from similar services? Show "insufficient data"?)
   - How often do you update prices? (Monthly? Rolling 90-day window?)

3. **Cold start:** When FleetBay launches in a new metro with zero transaction data, how do you bootstrap fair prices?
   - Option A: Import data from repair estimating guides (Mitchell, CCC, Audatex)
   - Option B: Survey local shops for rate cards
   - Option C: Use national averages with geographic cost-of-living adjustment
   - Recommend an approach with trade-offs

4. **User experience:** Design how Fair Price appears in the FleetBay interface:
   - On the search results page (price range next to each vendor)
   - On the quote comparison page (flag if quote is above/below fair range)
   - As a standalone tool ("What should X service cost in my area?")

**Deliverable:** Fair Price methodology + cold start strategy + UX integration wireframes.

---

## Phase 3: Domain Expertise

### Exercise 3.1: Service Taxonomy Design
**Objective:** Create a standardized taxonomy of fleet services for the marketplace.

**Task:**
FleetBay needs a structured taxonomy of all fleet services to enable search, matching, pricing, and analytics. This is harder than it sounds — "brake service" means different things to different people.

1. **Level 1: Service categories** (8-12 top-level categories)
   - Example: Preventive Maintenance, Brakes, Engine, Transmission, Electrical, Tires, Body/Paint, Glass, HVAC, Exhaust/Emissions, Towing, Other

2. **Level 2: Service types** (3-8 per category)
   - Example under "Brakes": Brake pad replacement, Brake rotor replacement, Brake drum replacement, Brake adjustment, Brake fluid flush, Complete brake job, Air brake system service, ABS diagnostic

3. **Level 3: Service variants** (by vehicle class)
   - "Brake pad replacement — Light duty (Class 1-3)" vs. "Brake pad replacement — Heavy duty (Class 7-8)"
   - How does vehicle class affect the taxonomy?

4. **Mapping challenges:**
   - How do you handle when a vendor's description doesn't match the taxonomy? ("Fixed the brakes" vs. "Replaced front brake pads and rotors")
   - How do you handle multi-service work orders? (Oil change + tire rotation + brake inspection as one visit)
   - How do you handle diagnostic services? ("Find out why the check engine light is on" doesn't fit a neat category)

5. **Taxonomy maintenance:** Who updates the taxonomy? How do you add new services? (Electric vehicles will need new categories)

**Deliverable:** Complete 3-level service taxonomy + mapping guidelines + maintenance process.

---

### Exercise 3.2: Vendor Quality Assurance Program
**Objective:** Design the quality assurance system that ensures FleetBay vendors deliver good work.

**Task:**
FleetBay's reputation depends on vendor quality. A bad repair experience reflects on FleetBay, not just the vendor. Design the QA program:

1. **Pre-onboarding verification:**
   - What credentials must a vendor have to list on FleetBay? (Business license, insurance, ASE certifications, EPA compliance, specific OEM certifications)
   - How do you verify these? (Document upload + automated verification service? Manual review?)
   - How long should verification take? (Target: <48 hours)
   - What percentage of applicants should be rejected? (Too low = poor quality; too high = insufficient supply)

2. **Ongoing quality monitoring:**
   - Rating-based: What happens at 3.5 stars? 3.0 stars? Below 2.5?
   - Comeback rate: If a fleet returns the same vehicle for the same issue within 30 days, that's a quality failure. Track per vendor.
   - Invoice accuracy: Do invoices match quoted prices? Track markup frequency.
   - Timeliness: Did the vendor complete service within quoted timeframe?

3. **Quality enforcement ladder:**
   - Warning (3.0-3.5 rating after 10+ reviews): notification sent, quality improvement plan
   - Probation (below 3.0 or comeback rate >10%): reduced visibility in search results, loss of "Verified" badge
   - Suspension (below 2.5 or pattern of complaints): temporarily removed from marketplace
   - Removal (persistent quality issues): permanently banned
   - Define the appeal process for each level

4. **Service guarantee:** Should FleetBay offer a quality guarantee?
   - "If your repair needs to be redone within 30 days due to vendor error, FleetBay covers the cost"
   - What's the projected cost of this guarantee? (1-3% of GMV?)
   - Is it worth it for trust-building and competitive differentiation?

**Deliverable:** QA program document + quality scorecard + enforcement ladder + guarantee cost model.

---

### Exercise 3.3: Emergency Breakdown Experience Design
**Objective:** Design the end-to-end emergency breakdown experience — FleetBay's "hero use case."

**Task:**
Emergency breakdown is FleetBay's wedge into the market — the highest-pain moment where fleet managers have no good options today.

**Design the experience from the driver's first call to the truck back on the road:**

1. **Minute 0 — Driver initiates:** The driver's truck won't start in a parking lot in Memphis, TN. The fleet is based in Atlanta.
   - Driver opens FleetBay app → taps "Breakdown Assist"
   - App captures: GPS location, vehicle info (pre-populated from profile), issue category (dropdown: won't start, flat tire, engine warning, accident, reefer failure, other)
   - Driver adds: photo of dashboard, voice note describing the issue
   - **Wireframe this screen.**

2. **Minute 1-5 — FleetBay matching:**
   - System finds qualified vendors within 30-mile radius with current availability
   - Push notification sent to 5 nearest shops: "Emergency: 2021 Kenworth T680, won't start, Memphis TN — can you help?"
   - First shop to accept gets the job
   - **What if no shop responds in 10 minutes?** (Auto-expand radius? FleetBay calls shops manually? Dispatch towing as fallback?)

3. **Minute 5-15 — Vendor accepted:**
   - Driver notified: "Ramirez Diesel Repair accepted your request. Tow truck ETA: 35 minutes. Shop address: [map]."
   - Dispatcher notified with same info via their dashboard
   - **Wireframe the driver's tracking screen** (like Uber: shows tow truck approaching)

4. **During repair:**
   - Vendor updates status: received → diagnosing → parts needed → repairing → quality check → ready
   - Each status change → push notification to driver + dispatcher
   - Vendor sends estimate before major work: "Starter motor replacement — $850 parts + $400 labor = $1,250. Approve?"
   - Dispatcher approves/declines from dashboard

5. **Post-repair:**
   - Driver picks up vehicle, confirms functional
   - Rating prompt: "How was your experience with Ramirez Diesel Repair?"
   - Invoice auto-generated and added to fleet's monthly consolidated bill
   - FleetBay sends fleet manager a breakdown summary report

**Deliverable:** Complete experience map + wireframes for 6 key screens (driver: initiate, tracking, status updates; dispatcher: notification, approval, summary) + edge case handling.

---

## Phase 4: Advanced Topics

### Exercise 4.1: Marketplace Network Effects and Competitive Moats
**Objective:** Analyze the types and strength of network effects in FleetBay.

**Task:**
1. **Classify FleetBay's network effects:**
   - **Same-side effects (supply):** Does having more vendors attract more vendors? (Usually no — vendors compete with each other)
   - **Same-side effects (demand):** Does having more fleet operators attract more fleet operators? (Only if data/reviews improve)
   - **Cross-side effects (supply → demand):** More vendors → better coverage → more fleets join
   - **Cross-side effects (demand → supply):** More fleets → more orders → more revenue → more vendors join
   - **Data network effects:** More transactions → better Fair Price data → more trust → more transactions

2. **Network effect strength assessment:**
   - Rate each network effect: strong, moderate, or weak
   - Compare to other marketplaces: is FleetBay's network effect stronger or weaker than Uber's? Than Airbnb's? Than Amazon Marketplace? Why?
   - What's the "tipping point" where network effects become self-sustaining?

3. **Multi-homing risk:**
   - Can vendors list on multiple marketplaces simultaneously? (Yes — low switching cost)
   - Can fleet operators use multiple vendor-finding methods? (Yes — FleetBay + Google + phone book)
   - How do you make FleetBay the "default" despite multi-homing?

4. **Winner-take-all assessment:** Is the fleet services marketplace likely to be winner-take-all, or will multiple platforms coexist? Why? (Research: which marketplace categories tend toward monopoly vs. oligopoly?)

**Deliverable:** Network effects analysis + competitive moat assessment + multi-homing mitigation strategy.

---

### Exercise 4.2: Predictive Service Matching
**Objective:** Design an ML-powered feature that proactively matches fleet vehicles with upcoming service needs to available vendors.

**Task:**
Instead of waiting for breakdowns, FleetBay can predict when vehicles need service and proactively suggest vendors.

1. **Prediction model:**
   - Input: vehicle make/model/year, current mileage, last service dates per category, driving conditions (mileage per month, road type), historical DTC codes (if telematics connected)
   - Output: "Vehicle #2847 likely needs brake service within 2-4 weeks" (confidence: 75%)
   - How do you train this model? (Historical service data from FleetBay transactions + OEM maintenance schedules)

2. **Proactive recommendation:**
   - When should FleetBay surface a recommendation? (In-app notification? Email? Dashboard card?)
   - What does the recommendation look like? "Your 2021 Kenworth T680 is due for brake service. Here are 3 shops near your depot with availability this week. Best price: $1,850 at TruckPro Memphis."
   - How is this different from a maintenance management tool? (FleetBay's value is the vendor match, not just the reminder)

3. **Business impact:**
   - Predictive matching shifts reactive service (breakdowns, emergency) to proactive service (scheduled PM). Why is this better for:
     - Fleet operators? (Less downtime, lower cost)
     - Vendors? (Predictable workload, scheduled appointments)
     - FleetBay? (Higher GMV — preventive services are more frequent)

4. **Data flywheel:** How does more transaction data improve prediction accuracy? Design the feedback loop.

**Deliverable:** Predictive matching product spec + recommendation UX wireframe + business impact model.

---

### Exercise 4.3: Geographic Expansion Playbook
**Objective:** Design the repeatable process for launching FleetBay in a new metro area.

**Task:**
FleetBay is live in DFW and expanding. Design the playbook for launching in metro #2 (Houston):

1. **Pre-launch (T-8 weeks to launch):**
   - Vendor target list: How do you identify the top 50 repair shops in Houston? (Google Maps scraping? Commercial vehicle shop directories? Industry association member lists?)
   - Fleet target list: How do you identify 30 fleet operators in Houston with 50-300 vehicles?
   - Cross-metro demand: How many existing DFW fleet customers also operate vehicles in Houston?

2. **Vendor onboarding (T-6 to T-2 weeks):**
   - Physical visits or remote onboarding? (First market was physical. Can Houston be remote?)
   - Target: 40 verified vendors at launch. What's the category mix? (20 general repair, 8 tire, 5 towing, 4 body shop, 3 glass)
   - Vendor incentive: first 3 months free Pro listing

3. **Fleet onboarding (T-4 to T-0):**
   - "Houston is now live" campaign to existing DFW fleets with Houston operations
   - Local fleet outreach: 15 Houston-only fleets onboarded before launch
   - Launch event? (Joint event with a Houston fleet association?)

4. **Post-launch (T+0 to T+12 weeks):**
   - Weekly metrics check: service request volume, fill rate, vendor response time, fleet repeat rate
   - "Unhealthy market" triggers: what numbers tell you Houston isn't working? (Fill rate <50% at week 4 = problem)
   - Course correction: if demand is low, what do you do? If supply is low?

5. **Template creation:** Turn this playbook into a checklist template that any FleetBay market launcher can follow for metros #3-#30.

**Deliverable:** Launch playbook document + weekly metrics dashboard + health check triggers + checklist template.

---

## Phase 5: Product & Business Strategy

### Exercise 5.1: Platform Strategy — Vertical vs. Horizontal
**Objective:** Decide FleetBay's long-term platform strategy.

**Task:**
FleetBay starts as a maintenance and repair marketplace. But should it expand horizontally (more service categories) or vertically (deeper into maintenance)?

**Option A: Horizontal expansion** — Add more fleet service categories:
- Parts procurement marketplace
- Driver staffing / temp driver marketplace
- Fleet vehicle sales marketplace (buy/sell used fleet vehicles)
- Fleet insurance marketplace (compare quotes from carriers)
- Fleet fuel card marketplace

**Option B: Vertical deepening** — Become the complete maintenance solution:
- Add SaaS fleet maintenance management (scheduling, tracking, vehicle health)
- Add parts inventory management
- Add predictive maintenance (telematics integration)
- Become the "Shopify for fleet maintenance shops" (give vendors a full shop management system)

**Option C: Hybrid** — Do both, but sequenced

For each option:
1. Revenue potential (estimate TAM for each new category)
2. Competitive moat impact (does this strengthen or dilute FleetBay's network effects?)
3. Execution complexity (engineering effort, operational effort, new domain expertise needed)
4. Customer value impact (do fleet managers want a broader marketplace or a deeper solution?)

Make a strategic recommendation with a 3-year sequencing plan.

**Deliverable:** Strategic options analysis + recommended sequencing + 3-year product vision.

---

### Exercise 5.2: Vendor Engagement & Retention Strategy
**Objective:** Design the strategy to keep vendors active and engaged on FleetBay.

**Task:**
Vendor retention is FleetBay's lifeline. If vendors leave, the marketplace dies.

1. **Vendor lifecycle mapping:** Define the stages of a vendor's life on FleetBay:
   - Onboarding → First service request → First completed transaction → Regular user → Power user → At-risk → Churned
   - For each stage: define the key metric, target timeframe, and intervention

2. **Vendor value proposition audit:** Vendors join for leads and revenue. But what makes them stay?
   - Lead volume: How many service requests per week does a vendor need to find FleetBay worthwhile? (Research: what's the minimum for HomeAdvisor/Angi vendors?)
   - Revenue impact: What percentage of a shop's revenue should come from FleetBay? (Too low = irrelevant; too high = dependency risk)
   - Tools value: Digital invoicing, payment speed (3-5 days vs. 30-60 day checks from fleet accounts), analytics

3. **Vendor success program:**
   - Design the "FleetBay Partner Success" program:
     - Profile optimization service (help vendors write better descriptions, take better photos)
     - Pricing guidance ("Shops in your area charge $X-$Y for brake jobs — consider adjusting")
     - Review solicitation tools (help vendors ask satisfied customers for reviews)
     - Marketing badge: "FleetBay Top Rated" and "FleetBay Verified" — how do vendors earn these?

4. **Vendor churn analysis framework:**
   - Leading indicators of vendor churn: declining response rate, increasing decline rate, fewer logins, negative reviews
   - Intervention playbook: what does FleetBay do when a vendor shows churn signals?
   - Win-back campaign: re-engage churned vendors — what offer brings them back?

**Deliverable:** Vendor lifecycle map + success program design + churn prevention playbook.

---

### Exercise 5.3: Marketplace Pricing Strategy Optimization
**Objective:** Optimize FleetBay's fee structure to maximize GMV growth while maintaining take-rate.

**Task:**
1. **Dynamic take-rate exploration:** Should FleetBay's take-rate vary based on:
   - Service category? (Higher take for emergency towing where FleetBay provides most value?)
   - Transaction size? (Lower take for $5,000+ repairs to encourage big transactions on-platform?)
   - Vendor tenure? (Lower take for loyal vendors who've been on platform 12+ months?)
   - Geographic market maturity? (Lower take in new markets to seed supply; higher in established markets?)

2. **Fee structure A/B test design:**
   - Test: 8% flat fee vs. 6% base + $25 fixed fee per transaction
   - Hypothesis: fixed fee component increases FleetBay revenue on small transactions without hurting large transaction volume
   - Calculate: which model generates more revenue at $500, $1,000, $2,500, and $5,000 transaction values?
   - Design the test: how do you split test this without confusing vendors?

3. **Competitive pricing pressure:**
   - What if a competitor launches with 3% take-rate (undercutting FleetBay)? At what point does FleetBay need to respond?
   - Design the response playbook: when to hold pricing, when to selectively discount, when to match
   - What non-price value justifies FleetBay's take-rate? (Payment speed, consolidated billing, quality guarantee)

4. **Vendor subscription pricing optimization:**
   - Free / $99 Pro / $249 Premium — is this right?
   - What features justify the step-up? Design the feature gating strategy.
   - What percentage of vendors should be on each tier? (Target: 60% free, 30% Pro, 10% Premium?)

**Deliverable:** Dynamic pricing model + A/B test design + competitive response playbook + subscription optimization.

---

## Phase 6: Hands-On Application

### Exercise 6.1: Launch Week Simulation
**Objective:** Simulate FleetBay's first week live in Dallas-Fort Worth.

**Task:**
It's Monday morning, Week 1. FleetBay is live in DFW with 45 vendors and 18 fleet operator accounts (representing ~1,200 vehicles).

**Day-by-day scenarios — handle each:**

**Monday:**
- 3 service requests submitted by fleet operators (2 scheduled PM services, 1 tire replacement)
- Only 1 vendor responds within 2 hours (the other 2 requests get no response)
- Fleet manager calls: "Nobody is responding. Is this platform broken?"
- **What do you do?**

**Tuesday:**
- A vendor completes a brake job. Uploads invoice for $3,200. Fleet manager says: "That's way too high. I usually pay $2,000 for this."
- FleetBay doesn't have enough transaction data for "Fair Price" yet.
- **How do you handle the dispute? How do you build Fair Price data faster?**

**Wednesday:**
- BREAKTHROUGH: A dispatcher uses FleetBay's breakdown assist. Truck broke down on I-35. FleetBay finds a shop 8 miles away in 4 minutes. Shop accepts, truck towed and repaired in 5 hours. Dispatcher says: "This is amazing."
- **How do you amplify this success? (Case study? Testimonial? Use it in sales?)**

**Thursday:**
- A vendor calls: "I signed up a week ago and haven't received a single service request. This is a waste of time."
- **How do you retain this vendor? What data do you share? What expectation did you set wrong?**

**Friday:**
- Week 1 metrics: 12 service requests submitted, 7 matched to vendors, 4 completed transactions. GMV: $4,800.
- **Write the Week 1 internal recap email to the team.** Include: wins, concerns, actions for Week 2.

**Deliverable:** Response plan for each day + Week 1 recap email + Week 2 action plan.

---

### Exercise 6.2: Vendor Onboarding Experience Design
**Objective:** Design the end-to-end vendor onboarding flow for self-serve signup.

**Task:**
As FleetBay scales beyond physical vendor visits, you need a self-serve onboarding flow that results in high-quality vendor profiles.

1. **Signup flow (target: <15 minutes):**
   - Step 1: Business basics (name, address, phone, email, website)
   - Step 2: Services offered (multi-select from taxonomy + "other")
   - Step 3: Vehicle types serviced (light-duty, medium-duty, heavy-duty, specialty)
   - Step 4: Credentials upload (business license, insurance certificate, certifications)
   - Step 5: Photos (shop exterior, interior, bays — explain why photos matter for trust)
   - Step 6: Pricing (rate card or "request quote" per service)
   - Step 7: Availability/hours
   - **Wireframe each step.**

2. **Verification process (target: <48 hours):**
   - Automated checks: business license validation (API?), insurance certificate verification (API?), Google Maps confirmation (address exists and matches a commercial property)
   - Manual review: photo quality check, certification validation, completeness review
   - Rejection handling: what if credentials are expired or business is not found?

3. **Profile optimization:**
   - After verification, prompt vendor to add: detailed service descriptions, specialties, certifications, response time commitment, gallery photos of completed work
   - "Profile strength meter" (LinkedIn-style): "Your profile is 60% complete. Add photos to reach 80% and get more visibility."

4. **First week experience:**
   - Day 1: Welcome email + "How FleetBay works" video (2 minutes)
   - Day 3: "Complete your profile" reminder if <80% complete
   - Day 5: First service request match (even if simulated/test — let them experience the notification flow)
   - Day 7: Check-in call or chat: "How's your first week? Any questions?"

**Deliverable:** Onboarding wireframes (7 screens) + verification process flow + first-week engagement plan.

---

### Exercise 6.3: Marketplace Health Dashboard
**Objective:** Design the internal dashboard that the FleetBay team uses to monitor marketplace health.

**Task:**
A marketplace has unique health metrics beyond typical SaaS. Design the dashboard:

1. **Liquidity metrics** (most important — is the marketplace working?):
   - Service request fill rate (% of requests matched to a vendor within 24 hours)
   - Average vendor response time (target: <2 hours scheduled, <15 minutes emergency)
   - Average time to first response (are multiple vendors competing for each request?)
   - Supply-demand ratio by metro by category (are there enough tire shops? Too many body shops?)

2. **Engagement metrics:**
   - Active fleet operators (submitted ≥1 request in last 30 days) / total registered
   - Active vendors (completed ≥1 transaction in last 30 days) / total registered
   - Repeat transaction rate (fleet operator uses FleetBay again within 30 days)
   - Average transactions per fleet operator per month

3. **Quality metrics:**
   - Average vendor rating (overall + by category)
   - Dispute rate (% of transactions with disputes)
   - Comeback rate (same vehicle, same issue, within 30 days)
   - Service guarantee claims (frequency + cost)

4. **Financial metrics:**
   - GMV (daily, weekly, monthly)
   - Net revenue (GMV x take-rate)
   - Average transaction value
   - Payment processing volume + margin
   - Vendor subscription revenue

5. **Alert conditions:** Define 5 alerts that indicate marketplace health problems:
   - Example: "DFW fill rate dropped below 60% — investigate supply shortage"

**Deliverable:** Dashboard wireframe with 4 sections + alert definitions + data source mapping.

---

## Bonus Exercises

### Bonus 1: "FleetBay for Vendors" Product Vision
Write a 1-page product vision for giving vendors a free shop management system (appointment scheduling, digital invoicing, customer CRM, inventory tracking) — similar to how Toast gives restaurants a free POS system. How does this lock in supply-side vendors?

### Bonus 2: Disintermediation Defense
FleetBay's biggest risk is disintermediation (fleets and vendors go direct after meeting on FleetBay). Design 5 specific features that make transacting ON FleetBay better than going direct. For each: what value does it provide that disappears if they go off-platform?

### Bonus 3: International Expansion Assessment
Should FleetBay expand internationally? Analyze 3 markets (UK, Germany, Brazil): fleet landscape, vendor landscape, competitive environment, regulatory complexity, and market size. Recommend: expand, don't expand, or wait.
