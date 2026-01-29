# Product Management Exercises: Fleet Data Monetization Platform (FleetSignal)

> Exercises mapped to the Fleet Management Learning Roadmap phases.
> Reference PRD: `PRD-04-Fleet-Data-Monetization-Platform.md`

---

## Phase 1: Foundation — Business & Ecosystem Understanding

### Exercise 1.1: Two-Sided Data Marketplace Economics
**Objective:** Model the economics of a platform where one side produces data and the other buys it.

**Task:**
FleetSignal has two customer types: fleet operators (data sellers) and data buyers (insurers, cities, OEMs). Each side requires different acquisition, pricing, and retention strategies.

1. **Supply-side economics:** Model the cost to acquire and maintain 100,000 contributing vehicles:
   - Fleet operator acquisition: 50 fleet operators averaging 2,000 vehicles each
   - Cost per fleet integration: engineering time ($5K-$15K per integration based on telematics platform)
   - Revenue share payout: $1-4/vehicle/month
   - Total annual supply-side cost at 100K vehicles

2. **Demand-side economics:** Model the revenue from 3 buyer segments:
   - 5 insurance carriers at $150K ACV each
   - 3 municipalities at $100K ACV each
   - 2 OEMs at $300K ACV each
   - Total annual demand-side revenue

3. **Marketplace liquidity model:** At what vehicle count does FleetSignal have statistically significant data for:
   - Metro-level traffic analytics (need X vehicles per metro area)
   - Insurance risk scoring (need X vehicles per risk category)
   - Vehicle reliability benchmarking (need X vehicles per make/model/year)

4. **Network effects analysis:** Draw the reinforcement loop: more fleet data → better products → more buyers → more revenue share → more fleets contribute. Where is this loop weakest?

**Deliverable:** Two-sided marketplace financial model + liquidity analysis + network effects diagram.

**Evaluation Criteria:**
- [ ] Supply and demand economics modeled independently
- [ ] Liquidity thresholds are specific and justified (not hand-waved)
- [ ] Network effects diagram identifies the weakest link
- [ ] Break-even analysis considers both sides of the marketplace

---

### Exercise 1.2: Data Buyer Discovery — Insurance Carriers
**Objective:** Understand what commercial auto insurers actually need and would pay for.

**Task:**
1. Research the commercial auto insurance underwriting process:
   - What data do underwriters currently use to price commercial fleet policies?
   - What is a "loss ratio" and why has commercial auto been unprofitable (loss ratios >100%) for many carriers?
   - How does Usage-Based Insurance (UBI) work in personal auto? Why hasn't it penetrated commercial?
   - What regulations govern the use of telematics data in insurance underwriting? (State-level rate filings)

2. Build an underwriter persona based on your research (role, daily workflow, data they wish they had, decision-making process)

3. Design a 10-question interview script for a commercial auto underwriter focused on:
   - What data would change their pricing decisions?
   - How much would they pay for per-fleet risk scores?
   - What integration format do they need? (API? Batch file? Dashboard?)
   - What actuarial validation would they require before using the data?

4. Identify 5 specific commercial auto insurance carriers to target and why (company size, market position, innovation history)

**Deliverable:** Insurance industry research summary + underwriter persona + interview script + target list.

---

### Exercise 1.3: Competitive Landscape — Data Platforms
**Objective:** Map the commercial vehicle data monetization landscape.

**Task:**
1. Research each competitor in the data monetization space:
   - **Wejo** (acquired by GM): What data do they sell? To whom? What was their revenue at acquisition?
   - **Otonomo**: What's their data marketplace model? Why did they struggle financially?
   - **Arity** (Allstate subsidiary): What's their driving behavior scoring model? How is it used?
   - **Cambridge Mobile Telematics (CMT)**: Smartphone-based scoring — how does it work? What are its limitations?
   - **Verisk**: The incumbent — what data products do they offer for commercial auto?

2. For each competitor, fill in:
   - Data source (OEM, telematics, smartphone, insurance claims)
   - Primary buyer segment
   - Revenue model
   - Strength vs. FleetSignal
   - Weakness vs. FleetSignal

3. Answer: What is FleetSignal's defensible advantage? Is it the data source (commercial fleet telematics)? The buyer focus (commercial auto insurance)? The fleet revenue-sharing model?

**Deliverable:** Competitive landscape map + positioning analysis.

---

## Phase 2: Technical Stack Deep Dive

### Exercise 2.1: Anonymization Pipeline Design
**Objective:** Design a data anonymization pipeline that protects individual fleet and driver identity while preserving analytical value.

**Task:**
FleetSignal receives raw telemetry: vehicle ID, timestamp, GPS coordinates (lat/lng to 6 decimal places), speed, heading, CAN bus parameters, fault codes.

Design the anonymization pipeline that transforms raw data into publishable data products:

1. **ID anonymization:**
   - Replace vehicle IDs with rotating cryptographic tokens. Why rotate? How often?
   - Hash driver IDs. Why hash instead of simply removing?
   - Strip fleet operator identity from all output products

2. **Spatial anonymization:**
   - Snap GPS coordinates to road segments (OpenStreetMap way IDs). Why is this safer than raw coordinates?
   - Suppress trip endpoints (first/last 500m). Why? What attack does this prevent?
   - What minimum aggregation level prevents location-based re-identification? (5 vehicles per road segment? 10?)

3. **Temporal anonymization:**
   - Minimum time bucket: 1 hour for traffic products. Why not 15 minutes?
   - Timestamp noise injection: add ±5 minute jitter to event timestamps. When does this matter?

4. **Differential privacy:**
   - Explain ε (epsilon) in plain language for a PM audience
   - What ε value is appropriate for FleetSignal's products? (Research what Apple, Google, US Census Bureau use)
   - What is the trade-off between privacy (lower ε) and data utility (higher ε)?

5. **Validation:**
   - Design 3 re-identification attacks a motivated adversary might attempt
   - For each attack, explain how your anonymization pipeline prevents it
   - What third-party audit should FleetSignal commission to validate the pipeline?

**Deliverable:** Anonymization pipeline design document + re-identification risk assessment.

**Evaluation Criteria:**
- [ ] All anonymization techniques serve a specific purpose (not just "best practice")
- [ ] Re-identification attacks are realistic (not strawmen)
- [ ] Trade-off between privacy and utility is explicitly discussed
- [ ] Differential privacy explanation is accessible to non-technical stakeholders

---

### Exercise 2.2: Data Ingestion Architecture
**Objective:** Design the system that ingests data from multiple telematics providers.

**Task:**
FleetSignal must pull data from 5+ telematics platforms, each with different APIs, data formats, and rate limits.

1. Research the APIs for 3 telematics platforms:
   - Geotab (Data Feed API / myGeotab SDK)
   - Samsara (REST API)
   - Motive (REST API)

   For each: data format, update frequency, rate limits, authentication, available data fields

2. Design a normalized data schema that can accept data from any provider:
   - What fields are universally available? (Timestamp, lat/lng, speed)
   - What fields are provider-specific? (CAN bus parameters vary by provider)
   - How do you handle data quality differences? (One provider reports speed every 5 seconds, another every 60 seconds)

3. Design the ingestion pipeline:
   - Pull vs. push: which is better for each provider? Why?
   - Error handling: what happens when a provider's API is down? (Data gap handling)
   - Back-fill: how do you handle late-arriving data?
   - Monitoring: how do you detect data quality degradation?

4. Calculate ingestion volume at 200,000 vehicles:
   - Events per second at peak
   - Daily storage volume
   - Infrastructure sizing (Kafka partitions, consumer groups)

**Deliverable:** Normalized schema + ingestion pipeline design + volume calculations.

---

### Exercise 2.3: ML Model Design — Fleet Risk Scoring
**Objective:** Write the product specification for the Fleet Risk Score ML model.

**Task:**
The Fleet Risk Score is FleetSignal's flagship product — a 0-100 score predicting the accident risk of a commercial fleet or individual vehicle.

Write the product spec (not the technical ML design):

1. **Model inputs:** What driving behavior features should the model use?
   - List 15-20 candidate features (speeding frequency, hard braking rate, time-of-day distribution, mileage, road type mix, etc.)
   - For each feature, note: data source, availability across providers, expected predictive power

2. **Model output:** What exactly does the score represent?
   - Option A: Probability of an at-fault accident in next 12 months
   - Option B: Relative risk compared to industry average (percentile)
   - Option C: Expected claims cost per vehicle per year
   - Recommend one and justify. What do insurance underwriters prefer?

3. **Score calibration:** How do you validate the score actually predicts risk?
   - What labeled training data do you need? (Actual accident/claims data — where does this come from?)
   - How do you handle the class imbalance problem? (Most vehicles don't have accidents)
   - What validation metric do you use? (AUC? Gini coefficient? — research what's standard in insurance)

4. **Model fairness:** Could the model discriminate based on protected characteristics?
   - Geographic features could correlate with race/income — how do you audit for this?
   - What fairness metrics should FleetSignal report?

5. **User experience:** How do underwriters consume the score?
   - Dashboard view for fleet portfolio analysis
   - API response for real-time quoting
   - Score explainability: "This fleet's top risk factors are: X, Y, Z"

**Deliverable:** ML product spec (4 pages) covering inputs, outputs, validation, fairness, and UX.

---

## Phase 3: Domain Expertise

### Exercise 3.1: Insurance Product Partnership Design
**Objective:** Design the integration between FleetSignal and an insurance carrier's underwriting workflow.

**Task:**
A Top-20 commercial auto insurer wants to use FleetSignal data to improve their pricing. Design the partnership:

1. **Integration workflow:** Map the underwriting process and where FleetSignal data fits:
   - Broker submits new business application → Underwriter reviews → Rates the risk → Issues quote → Binds policy → Monitors during policy term → Renewal
   - At which stages does FleetSignal data add value? Design the data flow.

2. **Data delivery formats:** Insurers use specific systems and formats:
   - Research ACORD data standards (insurance industry standard). Can FleetSignal output scores in ACORD format?
   - Integration options: API (real-time), SFTP batch file (nightly), portal (manual lookup)
   - Which format does the underwriter's daily workflow prefer?

3. **Actuarial validation:** Insurers can't use pricing factors without actuarial justification:
   - What does "actuarial validation" mean? (The score must statistically predict losses)
   - Design the validation study: FleetSignal provides historical scores, insurer provides historical claims, statistician measures correlation
   - How long does validation take? (Typically 12-24 months of claims development)

4. **Regulatory filing:** State insurance departments must approve new rating factors:
   - Research the rate filing process in 3 states (Texas, California, New York)
   - What documentation must the insurer submit to use FleetSignal data in pricing?
   - Which states are "file and use" (easier) vs. "prior approval" (harder)?

5. **Revenue model:** Design the pricing for this insurance partnership:
   - Per-policy scored? Per-vehicle monitored? Annual license? Hybrid?
   - What's the ROI for the insurer? (If FleetSignal improves loss ratio by 2 points, what's that worth?)

**Deliverable:** Partnership design document + integration architecture + actuarial validation plan + revenue model.

---

### Exercise 3.2: Municipal Data Product Design
**Objective:** Design the traffic analytics product for city transportation departments.

**Task:**
A mid-size US city (population 600K) wants to use FleetSignal's commercial vehicle data for infrastructure planning.

1. **Use case discovery:** Interview (or research) what city DOTs actually need. Common use cases:
   - Truck route compliance monitoring
   - Road pavement wear analysis (by vehicle weight class)
   - Intersection safety analysis (commercial vehicle crash risk)
   - Freight corridor planning
   - School zone commercial traffic analysis
   - Construction zone traffic diversion monitoring

2. **Data product design:** For the top 3 use cases, design the data product:
   - What data is needed?
   - What visualization / format does the city planner prefer? (Map layers? GIS files? PDF reports?)
   - What update frequency? (Real-time? Monthly?)
   - What geographic resolution is useful? (Road segment? Intersection? Zone?)

3. **Coverage assessment:** FleetSignal only has data from fleet operators who opt in. How do you ensure coverage?
   - In a city with 50,000 daily commercial vehicle trips, FleetSignal captures data from 5,000 (10%). Is this sufficient?
   - How do you extrapolate from sampled data to estimate total traffic? (Statistical methods)
   - What coverage percentage is the minimum for credible traffic analytics?

4. **Procurement process:** Selling to government is different from selling to companies:
   - Research the typical city procurement process (RFP, evaluation criteria, budget cycles)
   - What department has the budget? (DOT? Planning? Public works?)
   - What's the typical contract value and term for transportation data services?

**Deliverable:** Municipal product design + 3 use case specifications + coverage analysis + procurement strategy.

---

### Exercise 3.3: OEM Reliability Data Product Design
**Objective:** Design the vehicle reliability benchmarking product for truck OEMs.

**Task:**
A major truck OEM (e.g., Daimler Truck / Freightliner) wants real-world reliability data on their vehicles vs. competitors.

1. **Data product concept:** "Vehicle Reliability Index" — component-level reliability rankings based on real-world fleet data.

2. **Design the data methodology:**
   - How do you measure reliability? (DTC frequency? Mean miles between failures? Maintenance cost per mile?)
   - How do you normalize for operating conditions? (A truck in Minnesota winters vs. Arizona summers will have different failure patterns)
   - How do you ensure statistical significance? (Minimum sample size per make/model/year/component)

3. **Sensitive data handling:** OEMs want competitive intelligence but no OEM wants their data used against them:
   - An OEM subscribing can see: "Your model's brake system failure rate is 2.3x the class average"
   - But competitors are anonymized: "Competitor A" not "Freightliner"
   - How do you handle the scenario where an OEM demands to know who "Competitor A" is?
   - What if FleetSignal's data shows a safety defect that hasn't been recalled?

4. **Revenue model design:** OEMs are willing to pay a lot for this data. Design tiered pricing:
   - Tier 1: Annual reliability report (PDF) for their own vehicles — $X
   - Tier 2: Dashboard with quarterly updates + competitor benchmarks — $X
   - Tier 3: Custom queries + raw anonymized data access + API — $X
   - What's the right pricing for each tier?

**Deliverable:** Reliability methodology + sensitive data policy + tiered pricing model.

---

## Phase 4: Advanced Topics

### Exercise 4.1: Privacy-Preserving Analytics — Differential Privacy Implementation
**Objective:** Make a product decision about differential privacy parameters.

**Task:**
Differential privacy adds mathematical noise to data to prevent re-identification. As PM, you need to decide how much noise is appropriate.

1. **Research differential privacy basics:**
   - What is ε (epsilon) and what does it control?
   - What values of ε are considered "strong privacy" vs. "weak privacy"?
   - What did Apple use for iOS analytics? What did the US Census use for 2020?

2. **Privacy-utility trade-off experiment:**
   Imagine a traffic heatmap showing commercial vehicles per road segment per hour. Model what happens at different ε values:
   - ε = 0.1 (very private): How much noise? Is the heatmap still useful?
   - ε = 1.0 (moderate): How much noise? Can you distinguish high-traffic from low-traffic segments?
   - ε = 10.0 (weak privacy): Minimal noise. Any re-identification risk?

   Create a visual or table showing data quality at each privacy level.

3. **Product decision:** Recommend an ε value for each FleetSignal product:
   - Insurance risk scores (aggregated per fleet): ε = ?
   - Traffic heatmaps (aggregated per road segment): ε = ?
   - Vehicle reliability benchmarks (aggregated per make/model): ε = ?
   - Justify why different products might need different ε values

4. **Communication challenge:** Write a 200-word explanation of differential privacy for:
   - Fleet operators (data contributors): "Your data is protected because..."
   - Insurance buyers: "The accuracy of our scores is maintained because..."
   - Privacy regulators: "Our anonymization methodology ensures..."

**Deliverable:** Privacy parameter recommendations + trade-off analysis + 3 stakeholder communications.

---

### Exercise 4.2: Data Ethics Framework
**Objective:** Design the ethical guidelines for FleetSignal's data products.

**Task:**
Data monetization raises ethical questions beyond legal compliance. Design FleetSignal's ethical framework:

1. **Ethical dilemmas exercise:** For each scenario, decide: should FleetSignal do this?

   a. A law enforcement agency wants to purchase commercial vehicle route data to track suspected drug smuggling routes. The data would be anonymized at the road-segment level.

   b. A hedge fund wants to buy real-time freight flow data to predict retail earnings before quarterly reports. This is legal (alternative data for investing).

   c. An insurance carrier wants to use FleetSignal data to deny coverage (not just price it) to high-risk fleets. This could leave some fleets unable to operate.

   d. A competitor of one of FleetSignal's fleet operator data contributors wants to buy data. The data is anonymized, but patterns might reveal competitive intelligence.

   e. A journalist wants access to FleetSignal data for an investigation into a trucking company's safety record. The request is for anonymized aggregate data about the industry.

2. **Ethics policy:** Based on these dilemmas, write FleetSignal's data ethics policy (1 page):
   - Who can buy data? (Approved use cases vs. prohibited use cases)
   - Who cannot buy data? (Blacklisted buyer types)
   - What review process applies to borderline cases?
   - Who makes the final decision?

3. **Ethics board:** Should FleetSignal have an external data ethics advisory board? Who should be on it?

**Deliverable:** Dilemma analysis + data ethics policy + ethics governance recommendation.

---

### Exercise 4.3: International Data Expansion — GDPR Compliance
**Objective:** Assess the feasibility and design of expanding FleetSignal to EU markets.

**Task:**
FleetSignal wants to include European fleet data. GDPR applies.

1. **Legal analysis:** Research how GDPR applies to FleetSignal's model:
   - Is anonymized fleet telemetry data "personal data" under GDPR? (Article 4, Recital 26)
   - At what point in FleetSignal's pipeline does data become anonymized (and thus outside GDPR scope)?
   - What GDPR basis applies to the data before anonymization? (Consent? Legitimate interest?)
   - What is a Data Protection Impact Assessment (DPIA) and does FleetSignal need one?

2. **Technical requirements:** What changes does the anonymization pipeline need for GDPR?
   - Stricter anonymization thresholds? (k=10 instead of k=5?)
   - Data residency requirements? (EU data stored in EU?)
   - Right to erasure: if a fleet operator exercises their right to deletion, what happens to data already in FleetSignal's products?

3. **Business model impact:**
   - Does GDPR change the fleet operator consent model? (Explicit opt-in required — how does this affect onboarding?)
   - Are EU data buyers willing to use data derived from fleets operating under GDPR?
   - Does FleetSignal need a Data Protection Officer (DPO)?

4. **Go/no-go recommendation:** Should FleetSignal expand to the EU? What's the cost, risk, and opportunity?

**Deliverable:** GDPR compliance assessment + technical requirements + go/no-go recommendation.

---

## Phase 5: Product & Business Strategy

### Exercise 5.1: Data Network Effects Strategy
**Objective:** Design the strategy to build and defend FleetSignal's data network effects.

**Task:**
FleetSignal's moat is data network effects: more fleet data → better products → more buyers → more revenue share → more fleet data. Design the strategy to accelerate this flywheel:

1. **Cold start problem:** You need 50,000 vehicles before data products are statistically significant. But fleet operators won't join without revenue share (which requires buyers). Design the cold start strategy:
   - What subsidies/incentives break the chicken-and-egg deadlock?
   - Can you use synthetic data or public data to bootstrap early products?
   - Which comes first: supply (fleets) or demand (buyers)? Why?

2. **Data quality scoring:** Not all fleet data is equally valuable. Design a data quality score:
   - What makes fleet data high-quality? (Data freshness, field completeness, GPS accuracy, CAN bus coverage, driving hours per day)
   - How do you incentivize fleet operators to contribute higher-quality data? (Higher revenue share for higher quality?)
   - Scoring rubric: 0-100 data quality score

3. **Exclusivity strategy:** Should FleetSignal seek exclusive data agreements with fleet operators? (If Fleet X only shares data with FleetSignal, competitors can't replicate it)
   - Pros and cons of exclusivity
   - What would FleetSignal offer in exchange for exclusivity? (Higher revenue share? Free telematics? Premium analytics?)
   - Is exclusivity enforceable?

4. **Competitive defense:** A well-funded competitor (backed by a major insurer) launches a copycat platform. They offer fleet operators 50% revenue share (vs. FleetSignal's 30-40%). What do you do?

**Deliverable:** Data network effects strategy + cold start plan + competitive defense playbook.

---

### Exercise 5.2: Pricing Strategy for Data Products
**Objective:** Design the pricing model for FleetSignal's diverse data products.

**Task:**
FleetSignal sells to very different buyers (insurers, cities, OEMs) with very different willingness-to-pay. Design the pricing:

1. **Value-based pricing exercise:** For each buyer segment, calculate the value FleetSignal delivers:
   - **Insurer:** If FleetSignal improves commercial auto loss ratios by 2 points on a $500M book, that's $10M in value. What's fair pricing?
   - **Municipality:** If FleetSignal helps a city optimize $50M in road maintenance spending by 5%, that's $2.5M in value. What's fair pricing?
   - **OEM:** If FleetSignal helps reduce warranty costs by 3% on $500M in annual warranty spend, that's $15M in value. What's fair pricing?

2. **Pricing models comparison:** For each segment, evaluate:
   - Flat annual license fee
   - Per-query/per-API-call pricing
   - Per-vehicle-scored pricing (insurance)
   - Revenue-share/outcome-based pricing
   - Recommend one model per segment with rationale

3. **Self-serve tier design:** For smaller buyers (startups, researchers, analysts), design a self-serve pricing page:
   - Free tier: What do you offer for free? (Limited geography, historical data only, rate-limited API)
   - Starter: $X/month for Y API calls
   - Growth: $X/month for Y API calls + dashboard
   - How does self-serve pricing compare to enterprise contracts?

4. **Price discrimination ethics:** Is it ethical to charge an insurer $200K/year for essentially the same data you charge a city $80K/year for? Justify.

**Deliverable:** Pricing model per segment + self-serve tier design + pricing ethics analysis.

---

### Exercise 5.3: Investor Pitch Deck
**Objective:** Build the seed-stage pitch deck for FleetSignal.

**Task:**
FleetSignal is raising a $5M seed round. Build a 12-slide pitch deck:

1. **Problem** (1 slide): The commercial fleet data opportunity — data generated but wasted
2. **Solution** (1 slide): FleetSignal's data platform (one visual, one sentence)
3. **Market size** (1 slide): TAM/SAM/SOM for fleet data monetization
4. **Business model** (1 slide): Two-sided marketplace — how money flows
5. **Product** (2 slides): Core data products with mockup screenshots
6. **Traction** (1 slide): What have you achieved? (LOIs, pilot commitments, fleet data partnerships)
7. **Go-to-market** (1 slide): Supply-first strategy, buyer acquisition plan
8. **Competition** (1 slide): Landscape map showing FleetSignal's unique position
9. **Team** (1 slide): Why this team? (domain expertise + technical capability)
10. **Financials** (1 slide): Revenue projections (3 years), key assumptions
11. **Ask** (1 slide): $5M for 18 months — key milestones

For each slide, write the content and design the key visual/chart.

**Deliverable:** Full pitch deck outline with content for each slide + key visuals described.

---

## Phase 6: Hands-On Application

### Exercise 6.1: Design Partner Engagement
**Objective:** Run the first insurance carrier design partnership.

**Task:**
FleetSignal has signed a design partnership with a mid-size commercial auto insurer. They'll collaborate on the risk scoring product for 6 months before commercial launch.

1. **Partnership structure:**
   - What does the insurer provide? (Claims data for model validation, underwriter time for feedback, actuarial review)
   - What does FleetSignal provide? (Risk scores on insurer's existing fleet policyholders, dashboard access, weekly check-ins)
   - What are the deliverables at Month 3 and Month 6?
   - Is the partnership exclusive? (Can FleetSignal work with a competing insurer simultaneously?)

2. **Validation study design:**
   - FleetSignal scores 5,000 of the insurer's fleet policyholders
   - Insurer provides 3 years of claims history for those fleets
   - Actuary correlates FleetSignal scores with actual claims
   - Define: what correlation strength validates the model? (Research Gini coefficients in insurance)

3. **Feedback loop design:**
   - Weekly product review sessions: what do you show? What do you ask?
   - How do you prioritize insurer feedback vs. FleetSignal's product vision? (They want custom features — how much do you build for one partner?)
   - How do you prevent the product from being over-fitted to one insurer's needs?

4. **Commercial transition:**
   - At what point does the design partnership become a commercial contract?
   - What pricing discount (if any) does the design partner get for early adoption?
   - How do you use the design partner as a reference for acquiring the next 5 insurers?

**Deliverable:** Design partnership plan + validation study design + commercial transition strategy.

---

### Exercise 6.2: Data Product Quality Monitoring
**Objective:** Design the internal monitoring system for FleetSignal's data products.

**Task:**
FleetSignal's data products must be accurate, fresh, and unbiased. Design the monitoring system:

1. **Risk score monitoring:**
   - Distribution monitoring: is the score distribution stable month-to-month? (Alert if mean shifts >5 points)
   - Feature drift: are input features changing in unexpected ways? (e.g., a telematics provider changes their speed calculation)
   - Prediction calibration: does a score of 80 actually mean 80th percentile risk? (Calibration plot)

2. **Traffic heatmap monitoring:**
   - Coverage monitoring: what percentage of road segments have sufficient data? (Track over time)
   - Consistency check: does traffic volume make sense? (A road showing 10,000 daily traversals last month and 50 this month = data problem)
   - Freshness: alert if data for a metro is >48 hours stale

3. **Privacy monitoring:**
   - k-anonymity validator: confirm every data point in every product meets k≥5
   - Quasi-identifier scan: regularly check for combinations of fields that could enable re-identification
   - Alert: data point with k<5 detected → automatically suppress until more data available

4. **Incident response:** Design the playbook for:
   - Bad data shipped to a buyer (incorrect risk scores sent via API)
   - Privacy breach detected (re-identification possible in published product)
   - Data source goes offline (telematics provider API down for 48+ hours)

**Deliverable:** Monitoring dashboard design + alert rules + incident response playbook.

---

### Exercise 6.3: Fleet Operator Revenue Dashboard
**Objective:** Design the experience that keeps fleet operators engaged and contributing data.

**Task:**
Fleet operators need a reason to continue sharing data. The revenue dashboard is FleetSignal's retention tool.

1. **Dashboard design:** Wireframe the fleet operator's FleetSignal dashboard:
   - Revenue earned this month / this quarter / all-time
   - Vehicles contributing data (active vs. inactive)
   - Data quality score with improvement suggestions
   - Revenue breakdown by data product (which products earn the most?)
   - Payment history and upcoming payment schedule

2. **Engagement features:**
   - "Increase your revenue" recommendations: "Enable CAN bus data sharing to unlock vehicle reliability products — estimated +40% revenue"
   - Fleet insights: "Your fleet's safety score is in the top 20% nationally" (gives fleet operators value from their own data)
   - Benchmark comparisons: "Your fleet's fuel efficiency is 8% above industry average" (useful for fleet operators even without monetization)

3. **Revenue optimization:**
   - Which data types are most valuable? (Design the pricing matrix: GPS data = $0.50/vehicle/month, CAN bus data = additional $1.00, behavior events = additional $0.75)
   - How do you upsell fleet operators from GPS-only to full telemetry sharing?

4. **Churn prevention:**
   - What signals indicate a fleet operator is about to stop sharing data?
   - Design 3 automated interventions for at-risk fleet operators

**Deliverable:** Dashboard wireframes + engagement feature designs + churn prevention playbook.

---

## Bonus Exercises

### Bonus 1: "Data as a Service" Product Hunt Launch
Write the Product Hunt launch copy for FleetSignal's self-serve API. Include: tagline, description, 3 key features, and the "first comment" from the founder. Target audience: startup founders and data analysts who need commercial vehicle data.

### Bonus 2: Academic Research Partnership
Design a program to provide FleetSignal data (at heavy discount) to university transportation research programs. What data do you share? What restrictions apply? How does this generate PR and credibility?

### Bonus 3: M&A Target Assessment
FleetSignal is approached by a major insurance company (like Allstate or Progressive) about an acquisition. Write a 1-page analysis: what is FleetSignal worth? What are the strategic synergies? What are the risks of selling to an insurer (other insurer buyers may defect)?
