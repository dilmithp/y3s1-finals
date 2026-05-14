# LECTURE 11 — TRENDS IN SOFTWARE TESTING
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **⚠️ IMPORTANT NOTE FOR THIS LECTURE**
> Lecture 11 is **pure conceptual content** — no math, no formulas, no code. This is a **breadth-over-depth lecture**: the goal is to know **10 emerging trends** and **5 AI/ML techniques** in testing.
>
> Focus for this lecture:
> - **10 testing trends** — memorize all names and their key idea
> - **5 AI/ML techniques** with examples (NLP, Predictive Analytics, Clustering/Classification, Reinforcement Learning, Anomaly Detection)
> - Key comparison tables: **Shift-Left vs Shift-Right**, **DevOps vs QAOps**, **Crowdsourcing vs Outsourcing**, **API vs GUI Testing**
>
> **Top exam-likely essay:** "Discuss the latest trends in software testing" → list and briefly explain all 10.

---

# SLIDE 1 — Title Slide
"Trends in Software Testing." Skip.

---

# SLIDE 2 — The 10 Trends Overview

## 2. Theory (Exactly as in slides)

| # | Trend |
|---|-------|
| 1 | **Shift-Left Testing** |
| 2 | **AI and ML in Testing** |
| 3 | **Growing Use of QAOps** |
| 4 | **Crowdtesting** |
| 5 | **Enhanced Focus on Security Testing** |
| 6 | **IoT Testing** |
| 7 | **Mobile Test Automation** |
| 8 | **Enhanced API Testing and Automation** |
| 9 | **Focus on Accessibility Testing** |
| 10 | *Evolution of Test Automation* (revision of L9) |

> *Note: The slide grid shows 9 boxes — Trend #5 "Evolution of Test Automation" was treated as a revise-prior-lecture slide. We'll include it as Trend #5 in the chronological list since it's numbered that way in the slides.*

## 3. PRO TIPS
- **HIGH-FREQUENCY EXAM QUESTION:** "List and explain current trends in software testing."
- **Memory trick — "S-A-Q-C-E-S-I-M-A-A"** → **S**hift-Left, **A**I/ML, **Q**AOps, **C**rowdtesting, **E**volution, **S**ecurity, **I**oT, **M**obile, **A**PI, **A**ccessibility.

## Quick Recap
- 10 trends to memorize for exam.

---

# SLIDES 3-6 — Trend 1: Shift-Left Testing

## 1. Plain English Explanation
**Shift-Left** = move testing **earlier** in the development cycle. Don't wait for the end — start testing as soon as requirements are written.

## 2. Theory (Exactly as in slides)
- Emphasizing **early and frequent integration** of testing in the SDLC.

**Why important?**
- Identifying and addressing **issues sooner**
- **Accelerating market time**
- Enhancing software release quality
- Reducing the time spent on debugging
- Enabling teams to devote more effort to feature/functionality enhancement

**Delayed testing will result in:**
- Insufficient testing resources
- Missed design
- Architectural or requirements flaws
- Complexities in debugging and issue resolution
- Project delays

## 3. Visual (Slide 3 — Shift Left vs Shift Right Spectrum)
```
   ← SHIFT LEFT                              SHIFT RIGHT →
   Testing new   Testing new   Testing every   Testing every   Testing on
   requirements    code         build         deployment      production
```

## 4. Cost Insight (Slide 6)
- Fixing bugs **late in deployment** costs **640× more** than fixing them in **plan & design**.
- Fixing during testing = **10× cost** vs early fixes.

## 5. PRO TIPS
- **Key term:** Shift-Left = Testing **earlier**. Shift-Right = Testing **in production**.
- **Memory cue:** "Test left = test now, not later."
- **A4 Sheet:** *Shift-Left → early testing → 640× cost saving vs late fixes.*

## Quick Recap
- Shift-Left = test EARLIER in SDLC.
- Late bugs cost up to 640× more.

---

# SLIDES 7-21 — Trend 2: AI and ML in Software Testing

## 1. Plain English Explanation
AI and Machine Learning are increasingly used to **generate test cases, predict bugs, prioritize tests, and detect anomalies**.

---

## SLIDE 7 — Evolution of Testing Timeline

| Era | Period | Description |
|-----|--------|-------------|
| **Manual testing** | 1980–1990 | Waterfall methodology |
| **Bulky automation tools** | 1990–2000 | Experimentation, different dev approaches |
| **More robust automation + open source frameworks** | 2000–2010 | Agile, faster release cycles |
| **More about scale** | 2010–2018 | DevOps, continuous testing, CI/CD |
| **Autonomous testing, ML and AI** | The future | Collaborative, smart testing |

## PRO TIPS
- **Memory cue:** The 5 eras → Manual → Bulky tools → Open-source → Scale → AI/ML.

---

## SLIDE 8 — 5 AI/ML Applications in Testing

| # | Application | Description |
|---|-------------|-------------|
| 1 | **Test Case Generation** | Automatically generate test cases from requirements + historical data |
| 2 | **Test Prioritization** | Analyze code complexity, recent changes, defect data → prioritize critical tests |
| 3 | **Defect Prediction** | Predict potential failure areas using historical patterns |
| 4 | **Test Execution & Result Analysis** | Auto-execute tests, analyze results, identify defects |
| 5 | **Intelligent Feedback** | Provide context-aware feedback to testers about root cause |

## PRO TIPS
- **5 applications — "G-P-P-E-F"** → Generation, Prioritization, Prediction, Execution, Feedback.

---

## SLIDE 9 — 5 Benefits of AI/ML in Testing

| # | Benefit | Description |
|---|---------|-------------|
| 1 | **Increased Efficiency** | Automation + prioritization save time/resources |
| 2 | **Improved Accuracy** | AI identifies and fixes defects more effectively |
| 3 | **Cost Reduction** | Lower overall testing cost |
| 4 | **Enhanced Software Quality** | Fix defects early, meet quality standards |
| 5 | **Improved Developer Productivity** | Feedback on code, catches issues before bugs |

## PRO TIPS
- **5 benefits — "E-A-C-Q-P"** → Efficiency, Accuracy, Cost, Quality, Productivity.

---

## SLIDE 10 — 4 Challenges of AI/ML in Testing

| # | Challenge | Description |
|---|-----------|-------------|
| 1 | **Data Requirements** | AI/ML needs large training data |
| 2 | **Algorithm Complexity** | Requires specialized expertise |
| 3 | **Integration with Existing Tools** | Hard to integrate with current workflows |
| 4 | **Ethical Considerations** | Bias, fairness concerns |

## PRO TIPS
- **4 challenges — "D-A-I-E"** → Data, Algorithm, Integration, Ethics.

---

## SLIDE 11 — 5 AI/ML Techniques in Software Testing (MASTER TABLE)

| # | Technique | Purpose | Use Cases |
|---|-----------|---------|-----------|
| 1 | **Natural Language Processing (NLP)** | Understand human language | Test case generation, requirement traceability |
| 2 | **Predictive Analytics** | Forecast future defects | Defect prediction, test prioritization |
| 3 | **Clustering & Classification** | Group / categorize data | Test suite optimization, bug triage |
| 4 | **Reinforcement Learning** | Learn best sequence via trial/error | Intelligent exploratory testing |
| 5 | **Anomaly Detection** | Identify deviations from normal | AIOps monitoring, detecting flaky tests |

## PRO TIPS
- **5 techniques — "N-P-C-R-A"** → NLP, Predictive, Clustering, Reinforcement, Anomaly.
- **HIGH ESSAY PROBABILITY:** "Explain AI/ML techniques used in software testing."

---

## SLIDES 12-13 — Technique #1: NLP (Natural Language Processing)

### Theory
NLP helps automate testing tasks that involve **human language**.

**How NLP is used:**
- **Analyzing requirements** — Read text and auto-suggest test cases
- **Generating test cases from user stories** — Parse user stories → draft test cases
- **Analyzing bug reports** — Cluster, categorize, prioritize bugs
- **Automated testing of conversational systems** — Test chatbots/voice assistants

### Example (Slide 13)
**User story:** *"As a customer, I want to add products to my shopping cart so I can purchase them later."*

An NLP-based tool reads this and suggests:
- TC 1: Verify adding a single product to cart
- TC 2: Verify adding multiple products
- TC 3: Verify cart persists across sessions
- TC 4: Verify error handling for out-of-stock items

## PRO TIPS
- **A4 Sheet:** *NLP = reads requirements/user stories → auto-suggests test cases.*

---

## SLIDES 14-15 — Technique #2: Predictive Analytics

### Theory
Uses **historical data + statistical models + ML** to forecast outcomes.

**How it's used:**
- **Defect Prediction** — Predict modules likely to fail
- **Test Effort Estimation** — Forecast time/resources for testing
- **Test Case Prioritization** — Rank tests by defect likelihood
- **Release Readiness Prediction** — Forecast if software is stable enough

### Example (Slide 15) — Defect Prediction
**Inputs (historical data):**
- Code churn (how often code changes)
- Module complexity
- Past defect density
- Developer activity

**Output:** Model predicts that "payment" and "checkout" modules are high-risk.

**Outcome:**
- Prioritize tests for those modules
- Allocate more testers
- Prevent costly pre-release defects

## PRO TIPS
- **A4 Sheet:** *Predictive Analytics = forecast defects from history → prioritize risky modules.*

---

## SLIDES 16-17 — Technique #3: Clustering & Classification

### Theory

| Type | Learning Type | Purpose |
|------|---------------|---------|
| **Clustering** | Unsupervised | Group similar data points without labels |
| **Classification** | Supervised | Assign labels based on learned patterns |

**How Clustering is used:**
- Group similar test cases or bug reports
- Identify duplicates/overlaps/patterns
- Optimize test suites (remove redundancy)

**How Classification is used:**
- Predict outcomes (failure, severity, risk)
- Auto-filter bug reports (valid vs invalid, critical vs minor)

### Example (Slide 17) — Bug Triage System
**Clustering:** K-means or DBSCAN groups thousands of bug reports → reveals "login errors" cluster + "payment failures" cluster.
**Classification:** Decision Tree or SVM trained on historical bugs → auto-labels new reports as High/Medium/Low severity.

## PRO TIPS
- **Algorithms to memorize:**
  - Clustering: **K-means, DBSCAN**
  - Classification: **Decision Tree, SVM**
- **A4 Sheet:** *Clustering = group similar (unsupervised). Classification = label new (supervised).*

---

## SLIDES 18-19 — Technique #4: Reinforcement Learning (RL)

### Theory
An **agent** learns the best actions by interacting with an **environment**, getting **rewards/penalties**.

**How RL is used in testing:**
- Test case prioritization
- Test path exploration (UI/API)
- Automated bug discovery
- Dynamic test suite optimization
- Self-healing test automation

### Example (Slide 19) — UI Testing with RL

| Element | Description |
|---------|-------------|
| **Agent** | The RL-based automated tester |
| **Environment** | The web application's UI |
| **States** | Current screens/pages, element states |
| **Actions** | Click buttons, fill forms, navigate pages |
| **Reward** | Positive for finding bugs / coverage; penalty for dead ends |

**Workflow:**
1. Agent starts on homepage.
2. Clicks "Login" → if it leads to a new page or exposes a bug → gets reward.
3. Over many sessions, agent learns optimal exploration strategy.

## PRO TIPS
- **5 RL components: Agent, Environment, States, Actions, Reward.**
- **A4 Sheet:** *RL = agent + env + states + actions + reward → learns optimal test strategy.*

---

## SLIDES 20-21 — Technique #5: Anomaly Detection

### Theory
Identifies data/behavior that **deviates significantly** from expected/typical patterns.

**How it's used:**
- Detecting performance regressions
- Identifying unstable modules
- Spotting new/rare/unexpected bugs
- Monitoring system logs for unusual events

### Example (Slide 21) — API Response Time
- **Expected:** 100–200 ms per request
- **Observed:** 90% at ~150 ms (normal), 10% at 700 ms (anomaly)
- **Anomaly detection model** flags the 700 ms results — even though the test didn't technically "fail."

## PRO TIPS
- **A4 Sheet:** *Anomaly Detection = catch deviations from normal → flags performance regressions, flaky tests.*

---

# SLIDES 22-24 — Trend 3: Rising Significance of QAOps

## 1. Plain English Explanation
**QAOps** = QA + DevOps. Quality testing is **continuously integrated** throughout development, deployment, and delivery — not just at the end.

## 2. Theory (Exactly as in slides)
- QA is **no longer just a separate testing phase**.
- It is **embedded continuously** throughout dev, deploy, and delivery, using **automation, tools, and close collaboration** between QA, Dev, and Ops teams.

**Key Ideas:**
- **Continuous testing** across CI/CD pipeline
- **Automated test execution** after each code change/deployment
- **Shift-left testing** — QA works early
- **Monitoring in production** for ongoing quality

## 3. QAOps Cycle (Slide 23 — Infinity Loop)
QA cycle (Plan → Test Development → Automation → Trigger) + Ops cycle (Execute → Release → Report)

## 4. DevOps vs QAOps (Slide 24)

| **DevOps** | **QAOps** |
|------------|-----------|
| Operations + Developers have prime roles; QA is a subset of dev | QA specialists work collaboratively with Ops + Devs in **primary roles** |
| Importance on **deploying software rapidly** | Importance on **guaranteeing quality of software** |
| Software quality is **good** | Software quality is **excellent** |

## 5. PRO TIPS
- **Memory cue:** "QAOps = QA brought into DevOps as a first-class citizen."
- **A4 Sheet:** *QAOps → continuous QA in CI/CD, monitoring, collaboration. Better quality than DevOps alone.*

---

# SLIDES 25-28 — Trend 4: Crowdtesting

## 1. Plain English Explanation
Outsourcing testing to a **global crowd** of independent testers through platforms like Amazon Mechanical Turk, Upwork, 99designs.

## 2. Theory (Exactly as in slides)
- Involves a **large group of testers** who are **NOT part of the company's internal QA team**.
- Engage through **crowdsourcing platforms** (Amazon Mechanical Turk, Upwork, 99designs).
- Global market for crowdtesting **expected to expand**.

## 3. Crowdsourcing vs Outsourcing (Slides 26-27)

| **Crowdsourcing** | **Outsourcing** |
|--------------------|------------------|
| **Global** — workers anywhere in the world | **Single location** — center-based, offshore |
| **24/7** — flexible hours | **Set work hours** — facility shifts |
| **Flexible workforce** — on-demand, multiple languages | **Rigid workforce** — fixed staffing |
| **Output-based pricing** — pay for delivered work | **Headcount pricing** — based on hours |
| **No overhead costs** | **Fixed costs** — facility, equipment |

## 4. Benefits of Crowdtesting (Slide 28)
- **Scalable testing resources** on demand
- **More comprehensive test coverage**
- **Quicker feedback loop** with end users
- **Influx of specialized expertise**

## 5. PRO TIPS
- **4 benefits — "S-C-Q-E"** → Scalable, Coverage, Quick feedback, Expertise.
- **Memory cue:** "Crowdtesting = global, 24/7, pay-per-output, scalable."
- **A4 Sheet:** Crowdsourcing vs Outsourcing table.

---

# SLIDE 29 — Trend 5: Evolution of Test Automation

This slide is a **revision of Lecture 9 (Test Automation)**. The lecturer asks you to revise:
- Introduction to Test Automation
- Manual Vs Automated Testing
- Principles of Test Automation
- Test Automation Lifecycle
- Test Automation Frameworks
- Challenges & Myths in Test Automation

## PRO TIPS
- Refer back to **Lecture 9 study guide** for full details.

---

# SLIDES 30-32 — Trend 6: Enhanced Focus on Security Testing

## 1. Plain English Explanation
Cybersecurity threats are growing fast. Security testing must be **integrated from the start** of development.

## 2. Theory (Exactly as in slides)
- **Cybersecurity threats and data breach incidents** surged recently.
- Integrating security from **initial stages of design and development** is essential.
- **Emerging field: DevSecOps**.
- 4 security testing methodologies emphasized:
  - **Vulnerability Scanning**
  - **Penetration Testing**
  - **API Testing**
  - **Web Application Security Testing**

## 3. Cost of Cybercrime (Slide 31)
- 2024: $8.15 trillion → 2028: **$13.82 trillion** (70% increase)
- 2015: $3 trillion → 2025: $10.5 trillion (per slide chart)

## 4. DevSecOps (Slide 32)
- **DevSecOps** = methodology to provide security to application and infrastructure based on **DevOps principles**.
- Application is less vulnerable, ready for use.
- **Automated process** + security checks from the beginning of pipeline.
- Cycle: Plan → Code → Build → Test → Release → Deploy → Operate → Monitor (with **SEC** integrated throughout).

## 5. PRO TIPS
- **4 security testing methodologies — "V-P-A-W"** → Vulnerability, Penetration, API, Web app.
- **Memory cue:** "DevSecOps = Dev + Sec + Ops = security from start."
- **A4 Sheet:** *Security trend → 4 methodologies + DevSecOps + 70% cybercrime growth by 2028.*

---

# SLIDES 33-34 — Trend 7: IoT (Internet of Things) Testing

## 1. Plain English Explanation
Testing focused on **smart devices** (IoT) — security, data integrity, performance, scalability, compatibility.

## 2. Theory (Exactly as in slides)
**Significant testing trend focusing on IoT Instruments':**
- **Security**
- **Data integrity**
- **Performance**
- **Scalability**
- **Compatibility**

**Benefits:**
- Enhances system productivity by preventing unexpected glitches
- Provides greater **control over devices**
- Improves **network and device efficiency, accessibility, usage**

## 3. IoT Testing Market (Slide 34)
- Global IoT testing market is expected to grow significantly through 2028.
- Reflects increasing reliance on IoT devices + need for effective testing.

## 4. PRO TIPS
- **5 IoT focus areas — "S-D-P-S-C"** → Security, Data integrity, Performance, Scalability, Compatibility.
- **A4 Sheet:** *IoT testing → 5 focus areas: Security, Data, Perf, Scale, Compat.*

---

# SLIDES 35-36 — Trend 8: Mobile Test Automation

## 1. Plain English Explanation
With **mobile apps growing rapidly**, automated testing across devices and platforms is essential.

## 2. Theory (Exactly as in slides)
- Mobile app development is **rapidly growing** → mobile test automation will greatly help.
- Uses **software tools + scripts** to automatically test across various devices and platforms.
- **Cloud-based mobile labs** + test automation tools = next big step.

## 3. Cloud-Based Mobile Labs (Slide 36)
**Definition:** A remote testing environment where mobile apps are tested on real devices or emulators in the cloud.

**Why useful:** Test on different OS, models, screen sizes — without physical on-site lab.

**Key Features:**
- Remote Access
- Real Devices
- Virtual Devices
- Scalability
- Cost-Effectiveness
- Flexibility
- Integration

**Examples of Cloud-Based Mobile Labs:**
- Sauce Labs
- BrowserStack
- LambdaTest
- AWS Device Farm
- Perfecto.io
- Kobiton

## 4. PRO TIPS
- **MEMORIZE 3 TOOLS:** **Sauce Labs, BrowserStack, AWS Device Farm**.
- **7 features of cloud labs — "R-R-V-S-C-F-I"** → Remote, Real devices, Virtual, Scalable, Cost-effective, Flexible, Integration.
- **A4 Sheet:** *Mobile automation + Cloud labs (Sauce Labs, BrowserStack, AWS Device Farm).*

---

# SLIDES 37-38 — Trend 9: Enhanced API Testing and Automation

## 1. Plain English Explanation
**Microservices architectures** mean lots of APIs. Automating API testing is now standard practice.

## 2. Theory (Exactly as in slides)
- Rise of **microservices architectures** → significant increase in **APIs**.
- **API Test Automation** is the way to go: *"Make frequent cases faster."*
- API-driven development is more relevant than ever.
- API test automation = **higher efficiency, more tests in shorter time**.

## 3. API Testing vs GUI Testing (Slide 38 — Critical Table)

| **API** | **GUI** |
|---------|---------|
| Collection of **communication protocols & subroutines** | Software platform with **visual & audio indicators** |
| Enables interaction **between two programs** | Enables interaction **between a human and a computer program** |
| Requires **back-end storage** + logical architecture + library of scripts | Doesn't require as many resources as API |
| **High technical skills** required | Easier to use, doesn't require technical skills |
| **Easier to automate** → tested quickly | **Complicated to automate** → takes longer |
| Allows **data exchange via XML or JSON** | Doesn't allow XML/JSON data exchange |

> *Conclusion (right margin of slide): API testing is a more **efficient alternative** to extensive GUI testing in Agile/DevOps environments where speed is crucial.*

## 4. PRO TIPS
- **HIGH EXAM PROBABILITY:** "Compare API testing vs GUI testing."
- **Memory cue:** "API = fast, automatable, machine-to-machine. GUI = slow, manual, human-to-machine."
- **A4 Sheet:** 6-row API vs GUI comparison.

---

# SLIDES 39-40 — Trend 10: Focus on Accessibility Testing

## 1. Plain English Explanation
Making software **accessible to all users including those with disabilities**. Now a regulatory requirement in many jurisdictions.

## 2. Theory (Exactly as in slides)
- Era of **stringent web/mobile accessibility regulations**.
- Compliance through accessibility testing is **critical**.

**Accessibility standards to memorize:**
- **ADA** — Americans with Disabilities Act
- **Section 508**
- **WCAG 2.1** — Web Content Accessibility Guidelines

**Other points:**
- **Crowdtesting** offers valuable perspectives from users with disabilities
- For global apps, refining accessibility practices is essential to **bridge compliance gaps** and serve a **diverse user base**

## 3. Accessibility vs Usability (Slide 40 — Critical Distinction)

| **Accessibility** | **Usability** |
|-------------------|----------------|
| Validation tools | Ease of use |
| W3C standards | Broadest audience |
| Assistive technology | Satisfaction |
| Access to content | Efficiency |
| Legal requirements | User-centric design |

> Both contribute to **UX (User Experience)**.

Automation + AI can handle repetitive aspects (**screen readers, magnifiers, captions**).

## 4. PRO TIPS
- **3 standards to memorize — "ADA / Section 508 / WCAG 2.1"**.
- **5 Accessibility focus factors:** Validation tools, W3C, Assistive tech, Content access, Legal.
- **5 Usability factors:** Ease of use, Broadest audience, Satisfaction, Efficiency, User-centric.
- **Common MCQ trap:** Accessibility ≠ Usability. Accessibility = for disabled users (legal). Usability = for ease of use (general).

---

# SLIDE 41 — Quiz Time
*Mentimeter quiz instruction. No content.*

---

# SLIDE 42 — Thank You
*Closing slide. No content.*

---

# 📊 MASTER COMPARISON TABLES — LECTURE 11

## Table A — 10 Trends Summary

| # | Trend | Key Idea |
|---|-------|----------|
| 1 | Shift-Left Testing | Test EARLIER in SDLC, save 640× cost vs late fixes |
| 2 | AI/ML in Testing | 5 techniques (NLP, Predictive, Clustering, RL, Anomaly) |
| 3 | QAOps | Continuous QA integrated in DevOps (CI/CD) |
| 4 | Crowdtesting | Global crowd of external testers (Mechanical Turk, Upwork) |
| 5 | Evolution of Test Automation | Revise Lecture 9 |
| 6 | Enhanced Security Testing | DevSecOps, $13.82T cybercrime by 2028 |
| 7 | IoT Testing | Security/Data/Perf/Scale/Compat for IoT devices |
| 8 | Mobile Test Automation | Cloud labs (Sauce Labs, BrowserStack) |
| 9 | API Testing & Automation | Faster than GUI, microservices-driven |
| 10 | Accessibility Testing | ADA / Section 508 / WCAG 2.1 |

## Table B — 5 AI/ML Techniques

| # | Technique | Algorithm Examples | Test Use Case |
|---|-----------|---------------------|----------------|
| 1 | NLP | Parsing user stories | Auto test case generation from requirements |
| 2 | Predictive Analytics | Regression / forecasting models | Defect prediction, test prioritization |
| 3 | Clustering & Classification | K-means, DBSCAN / Decision Tree, SVM | Bug triage, severity labeling |
| 4 | Reinforcement Learning | Q-learning, policy gradient | UI test path exploration |
| 5 | Anomaly Detection | Statistical models, autoencoders | Performance regression, flaky test detection |

## Table C — Big Comparisons in This Lecture

| Comparison | Quick Distinction |
|------------|-------------------|
| **Shift-Left vs Shift-Right** | Test earlier vs test in production |
| **DevOps vs QAOps** | Speed of deployment vs guarantee of quality |
| **Crowdsourcing vs Outsourcing** | Global/24-7/output-paid vs Single location/hours/headcount |
| **API vs GUI Testing** | Machine-to-machine, fast, automatable vs Human-to-machine, slow, harder to automate |
| **Accessibility vs Usability** | For disabled users + legal vs Ease of use + UX |

---

# 📝 MCQ PRACTICE — LECTURE 11

---

### Q1. Shift-Left Testing emphasizes:
A) Testing only at the end of the SDLC
B) **Early and frequent integration of testing in SDLC** ✅
C) Testing only in production
D) Skipping testing for speed

**Answer: B (Slide 4)**

---

### Q2. Which AI/ML technique uses historical data to forecast which modules are likely to have defects?
A) NLP
B) **Predictive Analytics** ✅
C) Anomaly Detection
D) Clustering

**Answer: B (Slide 14)**

---

### Q3. Which AI/ML technique parses user stories to auto-generate test cases?
A) Predictive Analytics
B) **NLP** ✅
C) Reinforcement Learning
D) Anomaly Detection

**Answer: B (Slide 12)**

---

### Q4. QAOps integrates:
A) Only QA and Operations
B) **QA into the DevOps cycle** ✅
C) Only Development and Security
D) Crowdsourcing and Outsourcing

**Answer: B (Slide 23)**

---

### Q5. The combined methodology for security in DevOps is called:
A) QAOps
B) **DevSecOps** ✅
C) AIOps
D) SecOps

**Answer: B (Slide 32)**

---

### Q6. Which of the following is NOT an accessibility standard?
A) ADA (Americans with Disabilities Act)
B) Section 508
C) **WCAG 5.0** ✅
D) WCAG 2.1

**Answer: C — current standard is WCAG 2.1, not 5.0 (Slide 39)**

---

### Q7. Crowdsourcing differs from Outsourcing because Crowdsourcing is:
A) Single location, hourly paid
B) **Global, output-based pricing** ✅
C) Always more expensive
D) Restricted to internal QA

**Answer: B (Slides 26-27)**

---

### Q8. K-means and DBSCAN are algorithms used in:
A) Reinforcement Learning
B) NLP
C) **Clustering** ✅
D) Anomaly Detection

**Answer: C (Slide 17)**

---

### Q9. Which is NOT a key feature of cloud-based mobile labs?
A) Remote Access
B) Real Devices
C) Scalability
D) **Physical on-site lab requirement** ✅

**Answer: D — cloud labs eliminate the need for physical labs (Slide 36)**

---

### Q10. API testing is preferred over GUI testing in Agile/DevOps because:
A) GUI testing is more accurate
B) **API testing is more efficient, faster, and easier to automate** ✅
C) GUI testing has better tools
D) APIs don't need testing

**Answer: B (Slide 38)**

---

### Q11. The cost of fixing a bug found in production vs plan/design is approximately:
A) 10× more
B) 100× more
C) **640× more** ✅
D) The same

**Answer: C (Slide 6)**

---

### Q12. In Reinforcement Learning for testing, the "Agent":
A) Is the bug being fixed
B) **Acts as an automated tester learning by trial and error** ✅
C) Is a human QA engineer
D) Is the application's database

**Answer: B (Slide 19)**

---

# 📌 LECTURE 11 — A4 REFERENCE SHEET MINI-SECTION

```
10 TRENDS IN SOFTWARE TESTING (S-A-Q-C-E-S-I-M-A-A):

1. SHIFT-LEFT TESTING
   - Test earlier in SDLC
   - Late bugs cost 640× more than early ones

2. AI/ML IN TESTING — 5 Techniques (N-P-C-R-A):
   NLP                     → auto test case from user stories
   Predictive Analytics    → forecast defects (defect prediction)
   Clustering (unsup)      → group bugs (K-means, DBSCAN)
   Classification (sup)    → label bug severity (Decision Tree, SVM)
   Reinforcement Learning  → agent learns test paths (5 components: A-E-S-A-R)
   Anomaly Detection       → flag perf regressions, flaky tests

   5 AI/ML Applications (G-P-P-E-F):
     Generation, Prioritization, Prediction, Execution, Feedback

   5 Benefits (E-A-C-Q-P):
     Efficiency, Accuracy, Cost↓, Quality↑, Productivity↑

   4 Challenges (D-A-I-E):
     Data, Algorithm, Integration, Ethics

3. QAOPS = QA in DevOps
   - Continuous testing in CI/CD
   - QA + Ops + Dev primary roles
   - "Excellent" quality vs DevOps' "good" quality

4. CROWDTESTING
   - External global crowd of testers
   - Platforms: Mechanical Turk, Upwork, 99designs
   - Crowdsourcing vs Outsourcing: Global/24-7/Output-paid vs Single-loc/Hours/Headcount

5. EVOLUTION OF TEST AUTOMATION (revise Lec 9)

6. ENHANCED SECURITY TESTING
   - DevSecOps (DevOps + Security)
   - 4 methodologies (V-P-A-W):
       Vulnerability scanning, Penetration testing,
       API testing, Web application security
   - Cybercrime cost: $8.15T (2024) → $13.82T (2028), +70%

7. IoT TESTING — 5 focus areas (S-D-P-S-C):
   Security, Data integrity, Performance, Scalability, Compatibility

8. MOBILE TEST AUTOMATION
   - Cloud-based mobile labs (real + virtual devices)
   - Tools: Sauce Labs, BrowserStack, AWS Device Farm,
            LambdaTest, Perfecto.io, Kobiton

9. ENHANCED API TESTING & AUTOMATION
   - Microservices → many APIs
   - API vs GUI: API = fast, automatable, machine-to-machine, JSON/XML
                 GUI = slow, human-to-machine, no JSON/XML

10. ACCESSIBILITY TESTING
    - Standards: ADA, Section 508, WCAG 2.1
    - Accessibility (legal, disabled users) vs Usability (general UX)
    - Tools: screen readers, magnifiers, captions

KEY COMPARISONS:
   Shift-Left vs Shift-Right       (early vs late testing)
   DevOps vs QAOps                  (speed vs quality)
   Crowdsourcing vs Outsourcing    (global vs single-location)
   API vs GUI Testing               (machine vs human)
   Accessibility vs Usability       (legal/disabled vs general UX)
```

---

# ✅ LECTURE 11 — DONE

**Top exam-likely essay questions for this lecture:**
1. **"List and explain 10 current trends in software testing."**
2. **"Describe AI/ML techniques used in software testing."** (5 techniques)
3. **"Compare Shift-Left testing vs traditional testing approaches."**
4. **"Compare API testing vs GUI testing."**
5. **"What is DevSecOps and why is it important?"**
6. **"Differentiate Crowdsourcing from Outsourcing in testing."**

---

# 🎉 ALL LECTURES COMPLETE!

You now have study guides for:
- ✅ Lecture 1 — Introduction to Software Testing
- ✅ Lecture 2 — Specification Based Test Case Design Techniques
- ✅ Lecture 3 — Functional and Non-Functional Testing
- ✅ Lecture 8 — Software Testing Life Cycle (STLC)
- ✅ Lecture 9 — Test Automation
- ✅ Lecture 10 — Test Driven Development (TDD)
- ✅ Lecture 11 — Trends in Software Testing

**Still pending from your earlier preparation request (if needed):**
- Lecture 4 — Code Coverage Analysis (the file is available)
- Lecture 4 — Cyclomatic Complexity Measure (the file is available, **MAJOR exam topic for the CC metric calculation**)
- Lecture 5 — Cognitive Functional Size (**MAJOR exam topic for the CFS metric**)
- Lecture 6 — *Missing from your uploads*
- Lecture 7 — Weighted Composite Complexity (**MAJOR exam topic for the WCC metric — most likely metric question**)

**These are the lectures with the heavy math calculations (CC/CFS/WCC) that the exam will focus on.** Want me to prepare those next?
