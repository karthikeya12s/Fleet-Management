# Product Management Exercises: Hardware + Software Bundle (FleetNode)

> Exercises mapped to the Fleet Management Learning Roadmap phases.
> Reference PRD: `PRD-02-Hardware-Software-Bundle-Telematics.md`

---

## Phase 1: Foundation — Business & Ecosystem Understanding

### Exercise 1.1: Hardware Business Model Economics
**Objective:** Model the financial dynamics of a hardware + subscription business vs. pure SaaS.

**Task:**
1. Build a spreadsheet comparing 3 hardware go-to-market models over 36 months for a 200-vehicle fleet deal:
   - **Model A:** Full hardware purchase ($349/device) + $40/month subscription
   - **Model B:** Subsidized hardware ($175/device) + $45/month subscription (3-year contract)
   - **Model C:** Hardware-as-a-Service ($0 upfront) + $55/month subscription (3-year contract)
2. For each model, calculate: total revenue, cash flow by quarter, break-even point, customer lifetime value, gross margin
3. Model the impact of 10% annual hardware failure rate on unit economics (warranty replacements)
4. Answer: Which model should FleetNode offer as the default? Which is best for customers? Which is best for FleetNode's cash position?
5. Research how Samsara and Geotab structure their hardware pricing and compare

**Deliverable:** Financial model spreadsheet + 1-page recommendation memo with trade-off analysis.

**Evaluation Criteria:**
- [ ] All 3 models calculated correctly with consistent assumptions
- [ ] Cash flow timing is modeled (hardware upfront cost vs. subscription over time)
- [ ] Hardware failure/warranty impact is quantified
- [ ] Recommendation considers both company and customer perspective

---

### Exercise 1.2: Bill of Materials (BOM) Analysis
**Objective:** Understand the cost structure and trade-offs in telematics hardware.

**Task:**
1. Research the actual retail prices and estimated COGS for the key components in a telematics device:
   - SoC/processor (Qualcomm QCS6490 vs. MediaTek Genio vs. NXP i.MX8)
   - 4G LTE modem (Quectel EG25-G vs. Sierra Wireless HL7812)
   - Camera sensor (Sony IMX462 vs. OmniVision OV2735)
   - GPS module (u-blox M10 vs. Quectel L86)
2. Create an alternative BOM at 3 price points:
   - **Budget ($80 COGS):** What do you sacrifice?
   - **Standard ($130 COGS):** The baseline FleetNode Pro
   - **Premium ($200 COGS):** What do you add?
3. For each price point, map which features are enabled/disabled
4. Make a recommendation: should FleetNode ship 1 SKU, 2 SKUs, or 3 SKUs at launch? Why?

**Deliverable:** BOM comparison table + SKU strategy recommendation.

---

### Exercise 1.3: Total Cost of Ownership — Multi-Vendor vs. FleetNode
**Objective:** Build a compelling TCO comparison that the sales team can use.

**Task:**
A 200-truck fleet currently uses:
- Geotab GO9 for GPS tracking: $28/vehicle/month
- Lytx DriveCam for dashcam + driver camera: $45/vehicle/month
- Motive ELD for HOS compliance: $25/vehicle/month
- Manual diagnostic checks at each PM service: $50/vehicle/quarter

Build a 3-year TCO comparison:
1. **Current state:** Total cost of all 4 vendors (subscriptions + hardware + installation + IT management time + data integration effort)
2. **FleetNode state:** Single device, single subscription
3. Quantify "soft costs" that are real but often ignored: IT staff time managing 4 vendors, data integration projects, driver training on multiple devices, dashboard switching productivity loss
4. Calculate net savings and payback period

**Deliverable:** TCO comparison document formatted as a sales-ready 1-pager.

---

## Phase 2: Technical Stack Deep Dive

### Exercise 2.1: Edge AI Model Prioritization
**Objective:** Decide which AI models should run on-device vs. in the cloud.

**Task:**
FleetNode's edge processor can run 5 concurrent ML models. There are 10 potential models:

| Model | Latency Requirement | Data Volume | Safety-Critical? |
|-------|-------------------|-------------|-----------------|
| Forward collision warning | <50ms | High (video stream) | Yes |
| Drowsiness detection | <100ms | High (video) | Yes |
| Phone distraction | <200ms | High (video) | Yes |
| Lane departure warning | <100ms | High (video) | Yes |
| Tailgating detection | <200ms | High (video) | Moderate |
| Hard brake classification | <500ms | Low (accelerometer) | No |
| Fault code severity scoring | <5s | Low (CAN data) | No |
| Fuel theft detection | <60s | Low (fuel level sensor) | No |
| Driver identification (face) | <1s | Medium (video) | No |
| Road surface quality | <1s | Medium (accelerometer + video) | No |

1. Rank all 10 models for on-device priority
2. Select 5 for the initial device firmware — justify your choices
3. For the 5 not selected, define whether they should: (a) run in the cloud, (b) be deferred to V2 hardware, or (c) be dropped entirely
4. Consider: customer value, safety impact, compute cost, bandwidth savings, and competitive differentiation

**Deliverable:** Prioritized model list with decision rationale for each.

**Evaluation Criteria:**
- [ ] Safety-critical models prioritized correctly
- [ ] Latency requirements drive edge vs. cloud decision
- [ ] Bandwidth savings from edge processing are quantified
- [ ] Trade-offs between models that share compute resources are discussed

---

### Exercise 2.2: OTA Update Strategy Design
**Objective:** Design the Over-the-Air firmware update system for 50,000+ deployed devices.

**Task:**
FleetNode needs to safely update firmware on devices installed in moving trucks across the country. Design the OTA system:

1. **Update types:**
   - Critical safety patch (must deploy within 24 hours)
   - Feature update (deploy within 1 week)
   - AI model weight update (deploy within 2 weeks)
2. **Staged rollout strategy:** What percentage of devices get each stage? How long between stages? What metrics trigger go/no-go for the next stage?
3. **Failure handling:** What happens if an update fails mid-install? (Device is in a truck on I-80 with poor cellular connectivity)
4. **Rollback mechanism:** How does the device revert to the previous firmware if the new version causes issues?
5. **Scheduling constraints:** Updates should not interrupt active driving or recording. When is it safe to update?
6. **Fleet manager controls:** Can fleet managers delay updates? Opt out of non-critical updates? Schedule update windows?

**Deliverable:** OTA update system design document (3 pages) with rollout strategy flowchart.

---

### Exercise 2.3: Data Bandwidth Optimization
**Objective:** Calculate and optimize the cellular data usage per device.

**Task:**
FleetNode sends data from multiple sensors. Calculate monthly cellular data usage:

| Data Type | Raw Data Rate | Current Approach |
|-----------|-------------|-----------------|
| GPS location | 1 ping/30 sec, 100 bytes each | Send all |
| CAN bus parameters | 20 PIDs/sec, 50 bytes each | Send all |
| Accelerometer | 100 samples/sec, 12 bytes each | Send all |
| Dashcam video | 1080p @ 30fps, ~5 Mbps | Send all |
| Driver camera | 720p @ 15fps, ~2 Mbps | Send all |

1. Calculate raw monthly data volume if everything is sent over cellular (assume 8 hours of driving per day, 22 days per month)
2. That number is impossibly high. Design optimization strategies:
   - GPS: Send only on movement change or at reduced frequency when idle
   - CAN bus: Edge aggregation (send 1-minute summaries, not raw)
   - Accelerometer: Edge processing (only send detected events, not raw stream)
   - Video: Event-triggered upload only (not continuous streaming)
   - Wi-Fi offload: What percentage of data can wait for depot Wi-Fi?
3. Calculate optimized monthly cellular data usage
4. Estimate monthly cellular cost per device at pooled fleet data plan rates ($2-5/GB)

**Deliverable:** Data budget spreadsheet + optimization strategy document.

---

## Phase 3: Domain Expertise

### Exercise 3.1: Predictive Maintenance Feature Design
**Objective:** Design the user experience for predictive maintenance alerts.

**Task:**
FleetNode's edge processor monitors CAN bus data and detects patterns indicating component wear. You need to design how these predictions reach the right person at the right time.

**Scenario:** FleetNode's ML model has detected that Vehicle #2847 (2021 Freightliner Cascadia) has a 78% probability of battery failure within 30 days, based on voltage drop patterns over the last 6 weeks.

Design the complete experience:
1. **Alert hierarchy:** How is this alert different from a critical fault code alert vs. a minor efficiency suggestion? Design a 4-level alert severity framework.
2. **Notification flow:** Who gets notified? (Maintenance manager? Fleet manager? Driver?) Through what channels? When?
3. **Alert detail screen:** Wireframe the screen showing this prediction. What information does the maintenance manager need to take action?
4. **Action workflow:** What happens after the manager sees the alert? (Convert to work order → schedule appointment → track completion)
5. **Feedback loop:** How does the system learn if the prediction was correct? (Manager marks: "Replaced battery — model was right" or "Inspected — battery was fine, false alarm")
6. **False positive tolerance:** What's the maximum acceptable false positive rate before fleet managers start ignoring alerts? How do you measure this?

**Deliverable:** Alert framework + wireframes + notification flow diagram + feedback loop design.

---

### Exercise 3.2: Driver Safety Coaching Program Design
**Objective:** Design a driver safety program powered by FleetNode's AI dashcam and behavior data.

**Task:**
Fleet insurance carriers increasingly require evidence of "active driver coaching" for premium discounts. Design FleetNode's coaching program:

1. **Driver scoring model:** Design a composite safety score (0-100) with weighted components:
   - What events factor in? (hard brake, speeding, following distance, phone use, drowsiness, lane departure, seatbelt)
   - How are events weighted? (a phone-use event is worse than a hard brake?)
   - How does the score decay over time? (a perfect week should improve the score — how fast?)
   - What's the benchmark? (What score is "good"? "Needs improvement"? "Unacceptable"?)

2. **Real-time coaching:** Design in-cab alerts that are:
   - Helpful (driver knows what to do differently)
   - Not distracting (ironic if a safety alert causes a crash)
   - Not annoying (driver doesn't rip the device off the windshield)
   - Configurable (fleet manager can enable/disable specific alerts)

3. **Review workflow:** Design the safety manager's weekly workflow:
   - Which events need human review?
   - How is video evidence presented alongside behavior data?
   - How does the manager deliver coaching? (in-app message, in-person conversation triggered by the system)

4. **Insurance report:** Design the quarterly report FleetNode generates for the insurance carrier. What data do insurers need to justify premium discounts?

**Deliverable:** Scoring model design + in-cab alert UX spec + review workflow wireframes + insurance report template.

---

### Exercise 3.3: ELD Compliance — Product Requirements vs. Regulatory Requirements
**Objective:** Translate FMCSA regulatory requirements into product specifications.

**Task:**
1. Read the FMCSA ELD Technical Specifications (49 CFR Part 395 Subpart B Appendix A) — focus on:
   - Required data elements per driving event
   - Display requirements for roadside inspection
   - Data transfer requirements (Bluetooth + Web service)
   - Malfunction and data diagnostic event handling
   - Driver edit and annotation requirements
2. Translate 10 regulatory requirements into user stories with acceptance criteria
3. Identify 5 areas where the regulatory requirement is ambiguous and you need a product decision
4. Design the driver's ELD experience: status changes, daily log view, edit workflow, roadside inspection mode
5. Map the FMCSA certification process: what testing is required? How long does it take? What are the risks?

**Deliverable:** Regulatory-to-product requirements mapping + 10 user stories + ELD UX wireframes.

---

## Phase 4: Advanced Topics

### Exercise 4.1: Connected Vehicle Security Threat Model
**Objective:** Conduct a threat modeling exercise for a fleet telematics device.

**Task:**
FleetNode is a connected device installed in vehicles, communicating over cellular networks, with remote firmware update capability. This is a serious attack surface.

1. Using the STRIDE framework (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege), identify 12 threats against FleetNode
2. For each threat, assess: likelihood (1-5), impact (1-5), and current mitigation
3. Identify the top 5 threats and design mitigations:
   - **Device authentication:** How does the cloud know a request is from a legitimate FleetNode device?
   - **Data in transit:** How is telemetry data protected from interception?
   - **OTA update integrity:** How do you prevent malicious firmware from being installed?
   - **Physical tampering:** What if someone plugs into the device's debug port?
   - **Privacy:** What if a device is stolen and data is extracted from local storage?
4. Write a 1-page security brief for the fleet manager: "How FleetNode protects your data" (non-technical language)

**Deliverable:** STRIDE threat model + mitigation designs + customer-facing security brief.

---

### Exercise 4.2: Device Lifecycle & Warranty Strategy
**Objective:** Design the end-to-end device lifecycle management strategy.

**Task:**
FleetNode devices are deployed in harsh environments (extreme temperatures, vibration, power surges) for 3-5 years. Design the lifecycle:

1. **Provisioning:** How does a new device get configured for a specific fleet? (Zero-touch provisioning? QR code scan? Serial number entry?)
2. **Health monitoring:** What telemetry from the device itself (not the vehicle) should you monitor? (CPU temp, memory usage, cellular signal strength, camera health, accelerometer calibration)
3. **Failure detection:** How do you know a device has failed before the customer reports it? (Define "device health score" and alerting thresholds)
4. **RMA process:** Design the return/replacement process. How do you minimize customer downtime? (Advance replacement? Cross-shipping?)
5. **End-of-life:** When and how do you end-of-life a hardware generation? How do you migrate customers to new hardware?
6. **Warranty economics:** Model the cost of a 2-year vs. 3-year warranty at 3%, 5%, and 8% annual failure rates. What warranty term should FleetNode offer?

**Deliverable:** Device lifecycle management plan + warranty cost model + RMA process flowchart.

---

### Exercise 4.3: Multi-Product Portfolio Strategy
**Objective:** Define FleetNode's product portfolio strategy across customer segments.

**Task:**
FleetNode is considering 3 device SKUs (Core, Pro, Max) and 3 software tiers (Track, Protect, Predict). That's 9 possible bundles. This is too many.

1. Design a simplified product matrix: which device + software combinations should FleetNode sell? (Maximum 4-5 bundles)
2. For each bundle, define: target customer, use case, pricing, and positioning
3. Create a "Good-Better-Best" framework that guides customers to the right bundle
4. Design a product comparison page (wireframe) that makes the choice clear
5. Model the expected revenue mix: what percentage of customers buy each bundle?
6. Define the upgrade paths: how does a customer on Track + Core upgrade to Protect + Pro? (Hardware swap logistics + subscription change)

**Deliverable:** Product matrix + comparison page wireframe + revenue mix model + upgrade path design.

---

## Phase 5: Product & Business Strategy

### Exercise 5.1: Sales Process Design for Hardware + Software
**Objective:** Design the sales motion for a product that requires hardware installation.

**Task:**
Selling FleetNode is more complex than selling pure SaaS — the customer must also install physical devices on their vehicles. Design the sales and onboarding process:

1. **Sales stages:** Define the sales pipeline stages from first contact to fleet-wide deployment:
   - Lead → Qualified → Demo → Pilot → Procurement → Deployment → Active
   - For each stage: entry criteria, exit criteria, average duration, key activities
2. **Pilot program design:** Design a 10-vehicle, 30-day pilot that proves FleetNode's value:
   - What does the fleet get? (Free devices, free subscription)
   - What success metrics prove the pilot worked? (Be specific)
   - How do you convert a successful pilot to a full fleet deal?
3. **Deployment planning:** A 300-vehicle fleet just signed. How do you deploy FleetNode?
   - Self-install vs. professional installation — when to use each
   - Deployment schedule (50 vehicles/week? All at once? By location?)
   - Driver training plan
   - Go-live checklist per vehicle
4. **Sales compensation:** How do you compensate sales reps for hardware + subscription deals? (One-time commission on hardware? Monthly recurring commission? Blended?)

**Deliverable:** Sales process document + pilot program design + deployment playbook + comp plan outline.

---

### Exercise 5.2: Channel Partner Strategy
**Objective:** Design the channel partner program for FleetNode distribution.

**Task:**
FleetNode cannot reach 120,000 target vehicles through direct sales alone. Design a channel strategy:

1. **Identify 4 channel partner types** and for each: value proposition to the partner, revenue share model, support responsibilities, minimum requirements
   - Truck dealerships (Peterbilt, Kenworth, Freightliner dealers)
   - Leasing companies (Penske, Ryder)
   - Insurance carriers/brokers
   - IT/telematics VARs (value-added resellers)
2. For each channel, answer:
   - Why would they sell FleetNode? (What's in it for them?)
   - How do they sell it? (Pre-installed on new trucks? Recommended at insurance renewal? Bundled with lease?)
   - Who owns the customer relationship?
   - What training/enablement do they need?
3. Model the unit economics for each channel: revenue share, CAC reduction, LTV impact
4. Prioritize: which channel do you launch first and why?

**Deliverable:** Channel partner program design + economic model + launch priority recommendation.

---

### Exercise 5.3: Competitive War Game
**Objective:** Simulate Samsara's competitive response to FleetNode's launch.

**Task:**
You launched FleetNode 6 months ago and are gaining traction in the 50-500 vehicle segment. Samsara (the market leader with $800M+ ARR) notices.

1. **Red team (play Samsara):** What are 5 competitive responses Samsara could execute?
   - Price reduction? New SKU? Feature acceleration? Partnership? Acquisition?
   - For each: how quickly could they execute it? How effective would it be?
2. **Blue team (play FleetNode):** For each Samsara response, what is FleetNode's counter-strategy?
3. **Moat assessment:** What advantages does FleetNode have that Samsara cannot easily replicate?
4. **Moat assessment (reverse):** What advantages does Samsara have that FleetNode cannot easily overcome?
5. **Strategic recommendation:** Based on this war game, what should FleetNode's competitive strategy be? (Avoid head-to-head? Out-niche? Out-innovate? Race to different segment?)

**Deliverable:** 3-page competitive war game analysis with strategic recommendations.

---

## Phase 6: Hands-On Application

### Exercise 6.1: Hardware Product Launch Checklist
**Objective:** Create the launch checklist for a hardware + software product.

**Task:**
FleetNode Pro is 6 weeks from launch. Unlike SaaS, hardware launches are irreversible — you can't "patch" a physical device once shipped. Create a comprehensive launch checklist:

1. **Hardware readiness:**
   - Manufacturing quality validation (first production run acceptance criteria)
   - Environmental testing sign-off (temperature, vibration, drop)
   - Certification status (FCC, PTCRB, carrier approval)
   - Packaging and unboxing experience (what's in the box?)
   - Installation guide (printed + video)
   - Inventory levels (how many units for launch?)

2. **Software readiness:**
   - Firmware stability criteria (crash rate, memory leaks, watchdog timer incidents)
   - Cloud platform load testing (can it handle 10,000 devices connecting simultaneously?)
   - Mobile app store submission timeline (Apple review = 1-2 weeks)
   - OTA update system tested end-to-end

3. **Operations readiness:**
   - Device provisioning workflow tested
   - RMA/return process documented
   - Shipping/fulfillment partner configured (where are devices shipped from?)
   - Customer support trained on hardware troubleshooting

4. **Go-to-market readiness:**
   - First 10 pilot customers identified and committed
   - Sales team trained on hardware demo + installation story
   - Website with product specs, pricing, and order flow

**Deliverable:** Launch checklist with owners and timelines.

---

### Exercise 6.2: Post-Launch Device Quality Dashboard
**Objective:** Design the internal dashboard that monitors FleetNode device health after deployment.

**Task:**
You have 5,000 FleetNode devices deployed. Design a real-time device health dashboard:

1. **Fleet-level metrics:**
   - Devices online vs. offline (connectivity rate target: >99%)
   - Average daily data upload volume per device
   - Firmware version distribution (% on latest vs. older versions)
   - Device failure rate (devices requiring RMA, rolling 30-day)

2. **Individual device diagnostics:**
   - Last seen timestamp
   - Cellular signal strength history
   - CPU temperature trend
   - Storage utilization (128GB — how full?)
   - Camera health check (last successful image capture)
   - GPS fix quality (satellite count, HDOP)

3. **Alert design:** Define alerts for:
   - Device offline >4 hours during expected driving hours
   - Storage >90% full (video buffer not clearing)
   - Camera producing black/corrupt frames
   - Battery voltage below threshold (device may lose power)
   - Firmware update failed after 3 retry attempts

4. **Batch issue detection:** How do you detect a systemic issue (e.g., firmware bug affecting 5% of devices)? Design the anomaly detection logic.

**Deliverable:** Dashboard wireframes + alert rules + batch issue detection design.

---

### Exercise 6.3: Customer Advisory Board Design
**Objective:** Design a customer advisory board to guide FleetNode's product roadmap.

**Task:**
1. Define the purpose and scope of the advisory board (what decisions does it influence?)
2. Recruit criteria: How do you select 8-12 customers? (Fleet size mix, industry mix, technical sophistication, geographic diversity, friendly vs. demanding)
3. Meeting cadence and format: quarterly in-person vs. monthly virtual?
4. Agenda design: What do you show them? What do you ask them? How do you avoid groupthink?
5. Input mechanisms: How do advisory board feedback flow into the product roadmap? (Advisory board says "we need tire pressure monitoring" — what happens next?)
6. Incentive structure: What do advisory board members get? (Early access? Discounts? Conference invitations? Direct PM access?)

**Deliverable:** Advisory board charter + selection criteria + sample agenda for first meeting.

---

## Bonus Exercises

### Bonus 1: Hardware Teardown
Find a teardown video or article for an existing telematics device (Geotab GO9 or Samsara AG46). Document:
- Every component you can identify
- Estimated BOM cost
- Design decisions you agree/disagree with
- What you would change for FleetNode

### Bonus 2: Supply Chain Risk Assessment
Identify the top 5 supply chain risks for FleetNode hardware and design mitigation strategies. Consider: chip shortages, single-source components, geopolitical risk (China manufacturing), shipping delays, and quality control at contract manufacturers.

### Bonus 3: Pricing Page A/B Test
Design 2 versions of the FleetNode pricing page with different framing (hardware + subscription vs. all-inclusive monthly). Define the A/B test: hypothesis, sample size, success metric, and expected runtime. Mock up both versions.
