# Product Management Exercises: Managed Fleet Services Platform (FleetBridge)

> Exercises mapped to the Fleet Management Learning Roadmap phases.
> Reference PRD: `PRD-03-Managed-Fleet-Services-Platform.md`

---

## Phase 1: Foundation — Business & Ecosystem Understanding

### Exercise 1.1: Service Business Unit Economics
**Objective:** Model the unit economics of a services business where humans are the product.

**Task:**
FleetBridge's cost structure is fundamentally different from SaaS — the primary cost is people (Fleet Operations Specialists), not servers.

1. Model the economics of a single Fleet Operations Specialist (FOS):
   - Fully-loaded annual cost: salary ($65K) + benefits (30%) + tools/software ($3K) + training ($2K) + management overhead allocation
   - Vehicle capacity: model at 250, 300, 350, and 400 vehicles per FOS
   - Revenue per vehicle: $80/month management fee
   - At what vehicle-per-FOS ratio does the unit economics turn profitable? What's the margin at each level?

2. Model the ramp-up economics for a new FOS:
   - Week 1-3: Training (zero revenue-generating capacity)
   - Week 4-8: Ramp-up (50% capacity — managing 150 vehicles while learning)
   - Week 9+: Full capacity (300-400 vehicles)
   - What's the "payback period" for investing in hiring + training a new FOS?

3. Model the gain-sharing economics:
   - Baseline fleet spend: $15,000/vehicle/year
   - FleetBridge achieves 15% savings = $2,250/vehicle/year
   - 30% gain-share to FleetBridge = $675/vehicle/year
   - How does gain-sharing change the total revenue per vehicle? Per FOS?

4. Answer: What is the maximum management fee you can charge before customers say "I'll just hire a fleet manager myself"? (Compare: fleet manager salary ÷ vehicles managed)

**Deliverable:** Financial model spreadsheet + break-even analysis + competitive pricing analysis.

**Evaluation Criteria:**
- [ ] Correctly accounts for FOS ramp-up time (not immediately profitable)
- [ ] Gain-sharing revenue modeled separately from base management fee
- [ ] Compares build-vs-buy for the customer (hire fleet manager vs. outsource)
- [ ] Sensitivity analysis on FOS capacity ratio

---

### Exercise 1.2: Service-Level Agreement (SLA) Design
**Objective:** Design SLAs that are meaningful to customers and achievable by FleetBridge.

**Task:**
SLAs define the quality of service FleetBridge promises. Design the SLA framework:

1. For each core service, define measurable SLAs:

| Service | SLA Metric | Target | Measurement Method | Penalty for Breach |
|---------|-----------|--------|-------------------|-------------------|
| Compliance management | ? | ? | ? | ? |
| Maintenance scheduling | ? | ? | ? | ? |
| Emergency breakdown response | ? | ? | ? | ? |
| Monthly reporting | ? | ? | ? | ? |
| Service request response | ? | ? | ? | ? |

2. For each SLA:
   - What's the cost to FleetBridge if they breach it? (Financial penalty, service credit, or reputational only?)
   - What's the internal monitoring mechanism? (How does FleetBridge know they're about to breach an SLA?)
   - What's the escalation process when an SLA is at risk?

3. Design the SLA dashboard that the client sees in the portal

4. Tricky question: Should SLAs be tighter for higher-paying clients? Or the same for all? Justify.

**Deliverable:** SLA framework document + client-facing SLA dashboard wireframe.

---

### Exercise 1.3: Customer Discovery — "Reluctant Fleet Managers"
**Objective:** Understand the mindset of people who manage fleets but don't want to.

**Task:**
FleetBridge's primary persona is the "reluctant fleet manager" — someone whose real job is VP of Operations, Office Manager, or CFO, but who has fleet responsibilities dumped on them.

1. Write a 12-question interview script specifically for "reluctant fleet managers" (people who manage fleets as a secondary responsibility). Focus on:
   - How they ended up managing the fleet (was it gradual or sudden?)
   - What percentage of their time goes to fleet tasks
   - What they wish they could delegate entirely
   - What keeps them from outsourcing (trust? cost? control?)
   - Decision-making: who would approve outsourcing fleet management?

2. Identify 5 channels to find these personas (they won't be in "fleet manager" LinkedIn groups)

3. Design a survey (10 questions, <5 minutes) to quantify the problem at scale:
   - How many hours per week on fleet tasks?
   - What's your confidence level that your fleet is fully compliant? (1-10)
   - Have you ever been surprised by a fleet expense or violation?
   - Would you consider outsourcing fleet management if cost-neutral?

**Deliverable:** Interview script + survey design + 5 recruitment channels.

---

## Phase 2: Technical Stack Deep Dive

### Exercise 2.1: Operations Platform Architecture
**Objective:** Design the internal operations management system that FleetBridge staff use daily.

**Task:**
The FOS needs a purpose-built tool to manage 300-400 vehicles efficiently. Design the system:

1. **Task queue engine:**
   - Tasks auto-generate from: compliance deadlines approaching, maintenance schedules due, client service requests, vendor follow-ups, monthly report deadlines
   - Priority scoring: how do you rank a compliance deadline (urgent, no flex) vs. a routine PM scheduling (important, flexible)?
   - Design the FOS's daily task queue view (wireframe)

2. **Compliance engine:**
   - Data model: for each vehicle, track N compliance items with different renewal cycles, different state requirements, different processing workflows
   - Automation: what compliance workflows can be fully automated? (Registration renewal auto-filing in states that support e-services)
   - Alerts: design a 3-tier alert system (90/60/30 days) with escalation if not acted upon

3. **Vendor management CRM:**
   - Vendor profiles: services, pricing, quality scores, contact info, geographic coverage
   - PO generation: when FOS schedules a service, auto-generate a PO to the vendor with fleet rates
   - Invoice matching: auto-match vendor invoice to PO and flag discrepancies

4. **Client communication hub:**
   - How does the FOS communicate with 2-3 client contacts per account?
   - What's automated (status updates, report delivery) vs. manual (escalations, QBRs)?

**Deliverable:** Operations platform design document with wireframes for 4 key screens.

---

### Exercise 2.2: Automation Opportunity Assessment
**Objective:** Identify which FOS tasks can be automated to increase the vehicle-per-FOS ratio.

**Task:**
If FleetBridge can increase FOS capacity from 300 to 400 vehicles through automation, gross margin improves dramatically. Analyze each FOS task:

| Task | Weekly Time | Automation Potential | How to Automate |
|------|-----------|---------------------|----------------|
| Schedule preventive maintenance | 3 hrs | ? | ? |
| Track compliance deadlines | 2 hrs | ? | ? |
| Coordinate with vendors (calls/emails) | 5 hrs | ? | ? |
| Process/validate vendor invoices | 3 hrs | ? | ? |
| Generate client reports | 2 hrs | ? | ? |
| Handle breakdown calls | 2 hrs | ? | ? |
| Client communication (proactive) | 3 hrs | ? | ? |
| Vehicle acquisition/disposition | 2 hrs | ? | ? |

1. Rate each task: Fully automatable / Partially automatable / Requires human judgment
2. For partially automatable tasks, design the human-in-the-loop workflow
3. Estimate the total hours saved per week per FOS through automation
4. Calculate the impact on unit economics (more vehicles per FOS = higher margin)
5. Prioritize the automation backlog: what do you build first?

**Deliverable:** Automation assessment + priority roadmap + unit economics impact model.

---

### Exercise 2.3: Multi-State Compliance Data Architecture
**Objective:** Design the data model for tracking vehicle compliance across all 50 US states.

**Task:**
Vehicle registration, inspection, and insurance requirements vary by state. A fleet operating in 15 states must comply with 15 different sets of rules.

1. Research compliance requirements for 5 states (Texas, California, New York, Florida, Illinois):
   - Vehicle registration renewal: frequency, fees, online renewal available?
   - Safety inspection: required? Frequency? What's checked?
   - Emissions inspection: required? Which vehicles? Frequency?
   - Insurance minimums: liability, cargo, UM/UIM requirements
2. Design a flexible data model that handles state-level variation without hardcoding state-specific logic
3. How do you handle a vehicle that changes states? (Fleet moves a truck from Texas to California)
4. How do you keep the compliance rules database up-to-date as states change requirements?

**Deliverable:** Compliance data model + state comparison table + rules maintenance strategy.

---

## Phase 3: Domain Expertise

### Exercise 3.1: Vendor Network Strategy
**Objective:** Design the vendor network strategy for a new FleetBridge market.

**Task:**
FleetBridge is launching in the Atlanta metro area. You need to build a vendor network from scratch.

1. **Vendor category mapping:** List every vendor type a 200-vehicle mixed fleet needs:
   - Routine maintenance (oil change, tires, brakes, alignment)
   - Heavy repair (engine, transmission, electrical)
   - Body/collision repair
   - Glass repair
   - Towing/roadside
   - Detailing/cleaning
   - Registration services
   - Parts suppliers
2. For each category, determine: How many vendors do you need in the Atlanta metro? What's the geographic coverage requirement? (Every vehicle within 15 miles of a vendor?)
3. Design the vendor vetting process: What qualifications, certifications, insurance, and references do you require?
4. Create the vendor rate negotiation strategy: How do you negotiate fleet rates without volume on day 1? What leverage do you have?
5. Design the vendor scorecard: 5 metrics you track quarterly to evaluate vendor performance

**Deliverable:** Vendor network plan for Atlanta + vetting criteria + scorecard template.

---

### Exercise 3.2: Gain-Sharing Model Design
**Objective:** Design a fair, transparent gain-sharing model that aligns FleetBridge and client incentives.

**Task:**
Gain-sharing is FleetBridge's key differentiator — the company earns more when it saves the client more. But designing it fairly is complex.

1. **Baseline establishment:** How do you calculate the "before FleetBridge" baseline?
   - What data do you need from the client? (12 months of invoices? Vehicle list? Fuel card data?)
   - How do you handle: new vehicles added, vehicles removed, inflation, fuel price changes, mileage changes?
   - What if the client's data is incomplete or inaccurate?

2. **Savings categories:** Define which savings count toward gain-sharing:
   - Maintenance cost reduction (yes/no?)
   - Fuel cost reduction (yes/no? — FleetBridge doesn't control fuel prices)
   - Insurance premium reduction (yes/no? — long feedback loop)
   - Compliance fine avoidance (yes/no? — hard to prove a negative)
   - Admin time savings (yes/no? — soft cost, hard to quantify)

3. **Calculation mechanics:** Design the quarterly gain-sharing calculation:
   - Formula for calculating savings
   - Adjustments for fleet size changes, mileage changes, fuel price index
   - Split ratio: 70/30 (client/FleetBridge) — is this fair? What if savings are huge? What if savings are negative?

4. **Edge cases:**
   - What if there are no savings in a quarter? (FleetBridge gets $0 gain-share)
   - What if the client adds 50 new vehicles mid-quarter? (New vehicles have no baseline)
   - What if external factors (fuel price spike) overwhelm FleetBridge's savings?

5. **Client reporting:** Design the quarterly gain-sharing report that shows exactly how savings were calculated

**Deliverable:** Gain-sharing model design + calculation example + quarterly report template.

**Evaluation Criteria:**
- [ ] Baseline methodology is robust against gaming and noise
- [ ] Savings categories are defensible and measurable
- [ ] Edge cases are handled (not ignored)
- [ ] Report is transparent enough that the CFO trusts it

---

### Exercise 3.3: Fleet Lifecycle Replacement Analysis
**Objective:** Build a vehicle replacement decision model.

**Task:**
One of FleetBridge's highest-value services is telling clients WHEN to replace vehicles. Too early = unnecessary capital expense. Too late = maintenance costs exceed vehicle value.

1. Build a replacement analysis model for a 2020 Ford Transit 250 cargo van:
   - Input: purchase price, current mileage, maintenance cost history (monthly), fuel cost/mile, current resale value, projected resale value curve, insurance cost, depreciation schedule
   - Output: "Replace at X miles/Y years" based on minimum total cost of ownership
   - Graph: plot TCO per mile over time — the inflection point where keeping the vehicle costs more than replacing it

2. Apply the model to 3 different scenarios:
   - Light use (15,000 miles/year, city driving, HVAC service fleet)
   - Medium use (25,000 miles/year, mixed driving, delivery fleet)
   - Heavy use (40,000 miles/year, highway, courier fleet)

3. What data does FleetBridge need to build this model for each client vehicle? How do you get it?

4. Design the "Fleet Aging Report" dashboard showing: vehicles approaching optimal replacement, estimated replacement cost, projected savings from replacing vs. keeping

**Deliverable:** Replacement analysis model (spreadsheet) + 3 scenario outputs + dashboard wireframe.

---

## Phase 4: Advanced Topics

### Exercise 4.1: AI-Powered Operations Assistant
**Objective:** Design an AI assistant for Fleet Operations Specialists.

**Task:**
FleetBridge wants to build an AI assistant (think internal co-pilot) that helps FOS teams work faster and make better decisions.

1. **Use case identification:** List 10 tasks where AI can assist the FOS:
   - Example: "Read vendor invoice, extract line items, match to PO, flag discrepancies"
   - Example: "Analyze vehicle maintenance history, recommend optimal PM schedule"
   - Rate each: feasibility (easy/medium/hard), impact (time saved per week), data availability

2. **Top 3 AI features — detailed design:**
   For your top 3 use cases, design the AI feature:
   - Input: What data does the AI receive?
   - Processing: What does it do with the data?
   - Output: What does the FOS see?
   - Confidence: How does the AI express uncertainty?
   - Override: How does the FOS correct the AI when it's wrong?
   - Learning: How does the AI improve from FOS corrections?

3. **Build vs. buy:** Should FleetBridge build custom AI or use an existing LLM API (Claude, GPT-4)? For each use case, what's the right approach?

**Deliverable:** AI use case assessment + detailed designs for top 3 features.

---

### Exercise 4.2: EV Transition Advisory Service Design
**Objective:** Design FleetBridge's EV transition consulting service for mid-market fleets.

**Task:**
A 150-vehicle HVAC company asks FleetBridge: "Should we start replacing our Ford Transit vans with the Ford E-Transit? We're curious but nervous."

Design the consulting engagement:

1. **Assessment phase (Week 1-2):**
   - What data do you collect? (Vehicle usage patterns, daily mileage, route types, depot locations, utility rates)
   - What analysis do you perform? (Which vehicles are "EV-ready" based on daily mileage < EV range?)
   - What's the output? (Vehicle-by-vehicle EV suitability score)

2. **Financial modeling (Week 3):**
   - TCO comparison: Ford Transit ($35K purchase, $0.15/mile fuel, $2,500/year maintenance) vs. Ford E-Transit ($55K purchase - $7,500 tax credit, $0.04/mile energy, $1,200/year maintenance)
   - Payback period calculation
   - Incentive identification (federal, state, utility programs)

3. **Infrastructure planning (Week 4):**
   - Depot charging requirements (how many chargers? What capacity? What utility upgrades?)
   - Charging schedule optimization (charge overnight during off-peak rates)
   - Public charging contingency (for vehicles that exceed range)

4. **Pilot program design:**
   - Recommend: start with 10-15 vehicles that have the best EV fit
   - 6-month pilot metrics: actual vs. projected range, energy cost, maintenance cost, driver satisfaction, operational disruptions
   - Go/no-go criteria for expanding to full fleet

**Deliverable:** EV transition advisory playbook + TCO model + pilot program design.

---

### Exercise 4.3: Scaling from Regional to National Operations
**Objective:** Design the operational playbook for scaling FleetBridge from 3 metros to 30.

**Task:**
FleetBridge is operating in Atlanta, Dallas, and Houston with 25 clients. The CEO wants to be in 30 metros within 18 months. Design the expansion plan:

1. **Metro selection criteria:** Rank the next 27 metros by attractiveness:
   - Fleet density (how many target companies with 50-500 vehicles?)
   - Competitive presence (are Element/Merchants Fleet already strong here?)
   - Vendor availability (are there enough quality shops?)
   - FleetBridge customer demand (do existing customers operate in this metro?)

2. **Vendor network playbook:** How do you build a vendor network in a new metro without physical presence?
   - Remote vendor vetting process
   - National account coverage (Firestone, etc.) vs. local independents
   - Minimum vendor count to launch (what's the threshold?)

3. **FOS hiring and training:**
   - Can FOS work remotely? (They don't need to be in the metro they manage)
   - Training program: 6-week curriculum design (week-by-week outline)
   - Mentorship model: how does a new FOS shadow an experienced one?

4. **Quality consistency:** How do you maintain service quality as you scale from 25 to 180 clients?
   - Standardized operating procedures (what must be documented?)
   - Quality audits (how often? What do you check?)
   - Client satisfaction monitoring (beyond NPS)

**Deliverable:** National expansion playbook + metro prioritization model + FOS training curriculum outline.

---

## Phase 5: Product & Business Strategy

### Exercise 5.1: Managed Services vs. SaaS — Strategic Positioning
**Objective:** Articulate why managed services wins over self-service SaaS for the mid-market segment.

**Task:**
A VC asks: "Why not just build a SaaS tool and let customers self-serve? Managed services don't scale."

Write a response that:
1. Explains why mid-market fleet management is a poor fit for self-service SaaS (hint: the buyer doesn't have fleet expertise, doesn't want to learn, and can't implement software without guidance)
2. Quantifies the value gap: SaaS tool saves 30% of admin time; managed services saves 80% AND delivers expert decisions
3. Addresses the scalability concern: how does FleetBridge scale beyond linear FOS hiring? (Automation, AI, platform leverage, vendor network leverage)
4. Provides 3 examples of successful managed services businesses that achieved venture-scale outcomes (hint: ADP, Rippling PEO, Pilot bookkeeping)
5. Defines FleetBridge's long-term vision: Does it stay managed services forever, or does the platform eventually enable self-service for some segments?

**Deliverable:** 2-page strategic memo suitable for a VC partner meeting.

---

### Exercise 5.2: Quarterly Business Review (QBR) Design
**Objective:** Design the quarterly business review that FleetBridge presents to each client.

**Task:**
The QBR is FleetBridge's primary retention and expansion tool. Design it:

1. **QBR deck structure** (12-15 slides):
   - Fleet overview: vehicle count, additions/removals, utilization
   - Compliance scorecard: deadlines met, items processed, compliance rate
   - Maintenance summary: services performed, spend vs. budget, preventive vs. unplanned ratio
   - Cost analysis: TCO per vehicle, cost per mile, YoY trend
   - Gain-sharing report: savings achieved, gain-share payment
   - Vendor performance: top/bottom vendors by quality and cost
   - Recommendations: vehicle replacements, vendor changes, process improvements
   - Next quarter priorities

2. **For each section:** Define the data sources, calculation methodology, and visualization format

3. **QBR preparation workflow:** How does the FOS prepare for a QBR? (What data gathering, what analysis, what review?) How much time should QBR prep take?

4. **Expansion opportunities:** How do you use the QBR to sell additional services? (Example: "Your fleet's fuel costs are 12% above benchmark — our fuel management service could save $X")

5. **Difficult conversations:** How do you present a quarter where savings were below target? Where a compliance deadline was missed?

**Deliverable:** QBR deck template (slide outlines) + preparation checklist + expansion playbook.

---

### Exercise 5.3: Client Acquisition Funnel — Services Business
**Objective:** Design the sales and marketing funnel for a managed services business.

**Task:**
Selling managed services is different from selling SaaS — longer sales cycle, higher ACV, more trust required.

1. **Funnel design:**
   - **Top of funnel:** How do you find companies with 50-500 vehicles whose operations person is drowning in fleet admin? (They're not searching for "managed fleet services")
   - **Middle of funnel:** "Free fleet assessment" — design the 2-week assessment process that demonstrates FleetBridge's value before the contract
   - **Bottom of funnel:** Proposal, negotiation, contract — what's in the proposal? How do you handle objections?

2. **Content marketing for trust:**
   - Design 5 content pieces that establish FleetBridge as the fleet management authority:
     - "The True Cost of Managing Your Own Fleet" (calculator/tool)
     - "10 Compliance Violations That Could Shut Down Your Fleet" (fear-based)
     - "Case Study: How [Company] Reduced Fleet Costs 18% in 6 Months" (proof)
     - [Design 2 more]

3. **Referral partnerships:** Design the insurance broker referral program (insurance brokers see fleet risk data and can recommend FleetBridge)

4. **Conversion metrics:** Define target conversion rates at each stage and identify the #1 bottleneck

**Deliverable:** Full funnel design + content plan + referral program + conversion model.

---

## Phase 6: Hands-On Application

### Exercise 6.1: Day-in-the-Life Simulation
**Objective:** Simulate a day as a Fleet Operations Specialist managing 350 vehicles.

**Task:**
It's 8:00 AM Monday. You are a FleetBridge FOS managing 3 client accounts (120 + 130 + 100 vehicles). Here's your inbox:

**Urgent:**
1. Client A: Driver reports breakdown on I-85 southbound, reefer truck, perishable cargo, driver needs towing + repair ASAP
2. Client B: Registration for vehicle #2847 expired yesterday — driver was pulled over, $250 ticket, vehicle impounded

**Today's Queue:**
3. Schedule PM services for 8 vehicles across Client A and C (oil change + tire rotation)
4. Review and approve 6 vendor invoices (total: $14,200)
5. Follow up with body shop on Client B's collision repair (been 3 weeks, originally estimated 2 weeks)
6. Client C's controller is asking for the monthly cost report — it's 2 days late
7. Compliance calendar: 4 vehicles across all accounts have registrations expiring in 30 days

**By end of day:**
8. Prepare talking points for Client A's QBR tomorrow

**For each item:**
- Prioritize (what order do you handle these?)
- Describe the actions you take (who do you call, what do you look up, what do you tell the client?)
- Estimate time spent
- Identify what went wrong (the expired registration is a FleetBridge failure — how do you handle it with the client?)
- Identify what could be automated

**Deliverable:** Day simulation walkthrough with prioritization, actions, time estimates, and improvement recommendations.

---

### Exercise 6.2: Crisis Management — Compliance Failure
**Objective:** Handle a major service failure with a client.

**Task:**
FleetBridge missed a DOT annual inspection deadline for 12 vehicles in Client B's fleet. A DOT roadside inspection caught it — 3 vehicles were placed out-of-service, $4,800 in fines, and Client B's COO is furious.

1. **Immediate response (first 2 hours):**
   - What do you communicate to the client? When? Through what channel? Who delivers the message?
   - What actions do you take to resolve the immediate issue? (Get inspections scheduled ASAP)
   - Draft the client communication (email or call script)

2. **Root cause analysis:**
   - How did 12 vehicles get missed? (System failure? Human error? Onboarding gap?)
   - Design the RCA process: who's involved, what data is reviewed, what's the timeline?

3. **Remediation plan:**
   - What does FleetBridge owe the client? (Cover the fines? Service credit? Both?)
   - What systemic fix prevents this from happening again? (Process change? System change? Staffing change?)

4. **Client retention:**
   - The COO says "I'm considering canceling the contract." How do you save the account?
   - Design the recovery plan: what actions over the next 90 days rebuild trust?

**Deliverable:** Crisis communication draft + RCA framework + remediation plan + 90-day recovery plan.

---

### Exercise 6.3: Build the FleetBridge Financial Model
**Objective:** Build a 3-year financial model for FleetBridge suitable for investor conversations.

**Task:**
Build a bottoms-up financial model in a spreadsheet:

**Revenue:**
- New clients per month (assumption) x average vehicles per client x management fee per vehicle
- Gain-sharing revenue: (total vehicles) x (avg fleet spend/vehicle) x (savings rate) x (FleetBridge share)
- Ancillary revenue: procurement advisory, remarketing, fuel card commissions

**Costs:**
- FOS team: headcount = total vehicles / vehicles-per-FOS ratio
- Sales team: headcount based on new client acquisition targets
- Technology: platform development team + hosting + tools
- G&A: office, insurance, legal, accounting
- Vendor network development: initial investment per new metro

**Key metrics to output:**
- Monthly/quarterly/annual revenue, gross margin, EBITDA
- Customer acquisition cost, LTV, LTV:CAC
- Revenue per FOS, margin per FOS
- Cash flow and runway (assuming $3M seed funding)

**Sensitivity analysis:** Model 3 scenarios (conservative, base, aggressive) varying: new clients/month, vehicle-per-FOS ratio, and churn rate.

**Deliverable:** Financial model spreadsheet with assumptions tab, P&L tab, cash flow tab, and sensitivity analysis.

---

## Bonus Exercises

### Bonus 1: Competitive Win/Loss Analysis Framework
Design the process for tracking why FleetBridge wins or loses deals. What data do you collect from sales? How do you categorize loss reasons? How does this data feed back into product and service improvements?

### Bonus 2: Employee Onboarding Curriculum
Design the 6-week training curriculum for a new Fleet Operations Specialist. Week-by-week, what do they learn? Who trains them? What's the certification test at the end? How do you ensure quality consistency across FOS team members?

### Bonus 3: Partnership Proposal — Insurance Broker
Write a 2-page partnership proposal to a commercial auto insurance brokerage. Explain: why their clients need FleetBridge, how FleetBridge improves the broker's book of business (lower claims = happier carriers = better commissions), and what the economics look like for the broker (referral fee per client).
