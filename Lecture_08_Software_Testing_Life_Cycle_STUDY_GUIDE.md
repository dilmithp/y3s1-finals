# LECTURE 8 — SOFTWARE TESTING LIFE CYCLE (STLC)
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **⚠️ IMPORTANT NOTE FOR THIS LECTURE**
> Lecture 8 is **pure conceptual content** — no formulas, no code, no calculations.
>
> This is one of the **highest-likelihood essay-question lectures** for the L8–L11 paper:
> - The exam will likely ask you to **list and explain the 6 STLC phases**.
> - Each phase has 4 sub-elements: **Inputs / Activities / Outputs / Tools** — memorize all four for every phase.
> - Big additional terms: **RTM, Test Plan, Test Scenario vs Case vs Script vs Data, Test Metrics, Test Environments**.
>
> **Focus: memorization, terminology, comparison tables.**

---

# SLIDE 1 — Title Slide
"Software Testing Life Cycle (STLC)" — date and lecturer. Skip.

---

# SLIDE 2 — STLC Overview

## 1. Plain English Explanation
The lecture covers **9 major topics**:
1. Introduction to STLC
2. SDLC vs STLC
3. Requirement Analysis (Phase 1)
4. Test Planning (Phase 2)
5. Test Case Development (Phase 3)
6. Test Environment Setup (Phase 4)
7. Test Execution (Phase 5)
8. Test Cycle Closure (Phase 6)
9. Challenges in STLC

## 2. PRO TIPS
- This is the **roadmap** of the lecture. Memorize the 6 phases in order.

---

# SLIDE 3 — Introduction to STLC

## 1. Plain English Explanation
The Software Testing Life Cycle (STLC) is a **structured, step-by-step process** for testing software — from understanding requirements all the way to closing the test cycle and reporting results.

## 2. Theory (Exactly as in slides)
- STLC is a **systematic approach** to testing a software application to ensure that it **meets the requirements** and is **free of defects**.
- Follows a **series of steps or phases** with specific objectives.
- **Fundamental part of SDLC**.

**Why STLC is Important?**
- Helps in **finding defects early**
- Ensures a **systematic approach** to testing
- Makes testing **measurable and repeatable**
- Supports **better planning, coverage, and quality control**

## 3. PRO TIPS
- Key essay phrase: *"STLC is a systematic approach to testing a software application to ensure it meets requirements and is free of defects."* — write verbatim.
- **A4 Sheet:** *STLC → systematic + phased + early defects + measurable + planning.*

## Quick Recap
- STLC = structured, phased testing process.
- 4 benefits: early defects / systematic / measurable / better planning.

---

# SLIDE 4 — Stages of STLC (The Cycle)

## 1. Plain English Explanation
The 6 phases form a **flow**, but it's called a **cycle** because of feedback loops, rework, and continuous improvement.

## 2. Theory (Exactly as in slides)
**The 6 stages (in order):**
```
Requirement Analysis
       ↓
Test Planning
       ↓
Test Case Development
       ↓
Test Environment Setup
       ↓
Test Execution
       ↓
Test Closure
```

**Why is it called a Cycle?**
- Because testing is rarely a **one-way street**.
- **Feedback loops, rework, iterations, and continuous improvement** make it cyclic.

## 3. PRO TIPS
- **Memory trick — "R-P-D-E-E-C"** → **R**equirement, **P**lanning, **D**evelopment (test case), **E**nvironment, **E**xecution, **C**losure.
- **Common exam question:** "Why is STLC called a cycle?" → memorize: *"Feedback loops, rework, iterations, and continuous improvement make it cyclic."*
- **A4 Sheet:** Draw the 6-phase flow vertical chart.

## Quick Recap
- 6 phases in order: Requirement → Planning → Test Cases → Environment → Execution → Closure.
- Called a "cycle" due to feedback/iteration.

---

# SLIDE 5 — Key Characteristics of SDLC

## 1. Plain English Explanation
This slide is **mislabelled in the deck** — it actually lists the key characteristics that **apply to STLC** (and SDLC by extension).

## 2. Theory (Exactly as in slides)
- Phased Approach
- Goal-Oriented
- Process-Driven
- Early Defect Detection
- Improves Quality
- Traceability
- Reusability

## 3. PRO TIPS
- **7 characteristics** — easy 7-mark essay answer if asked.
- **Memory trick:** "**P-G-P-E-I-T-R**" — Phased, Goal-oriented, Process-driven, Early defect, Improves quality, Traceability, Reusability.

## Quick Recap
- 7 key characteristics — memorize all.

---

# SLIDE 6 — STLC vs SDLC (CRITICAL EXAM TABLE)

## 1. Plain English Explanation
**SDLC** is the bigger picture (whole development cycle). **STLC** is just the testing-focused subset.

## 2. Theory (Exactly as in slides)

| Aspect | **SDLC** (Develop Software) | **STLC** (Test Software) |
|--------|-----------------------------|---------------------------|
| **Goal** | Build a functioning, high-quality application | Ensure the software works as expected and is bug-free |
| **Focus Area** | Covers entire development (requirements → deployment) | Covers only testing-related activities |
| **Who Performs It** | Developers, Architects, Business Analysts, DevOps, etc. | **Testers / QA team** |
| **Starts When** | At the beginning of the software project | **When requirements are ready** |
| **Output / Deliverables** | Working software, system architecture, code, documentation | **Test cases, bug reports, test summary reports** |
| **End Result** | A product ready for release | Verified and validated software |

## 3. PRO TIPS
- **VERY HIGH EXAM PROBABILITY:** "Compare and contrast SDLC vs STLC" → memorize this 6-row table.
- **Memory trick:** SDLC = **D**evelop. STLC = **T**est. Both have phases, but different focus.
- **A4 Sheet:** This 6-row comparison verbatim.

## Quick Recap
- SDLC = build. STLC = test.
- SDLC starts at project beginning; STLC starts when requirements are ready.
- SDLC delivers a product; STLC delivers verified/validated software.

---

# SLIDE 7 — STLC Phase Structure

## 1. Plain English Explanation
**Every STLC phase has the same 4-part structure** — this is the template you'll use for memorizing each phase.

## 2. Theory (Exactly as in slides)
```
   ┌──────────┬──────────┬──────────┐
   │  Inputs  │ Activities│ Outputs │
   └──────────┴──────────┴──────────┘
              [ Tools ]
```

## 3. PRO TIPS
- **CRITICAL FRAMEWORK:** For every phase, remember 4 things — **I-A-O-T** (Inputs, Activities, Outputs, Tools).
- **A4 Sheet:** *"Every STLC phase = Inputs + Activities + Outputs + Tools"*

## Quick Recap
- 4-part structure per phase: **I-A-O-T**.

---

# SLIDES 8–11 — PHASE 1: Requirement Analysis

## 1. Plain English Explanation
The testing team **reads and understands** the requirements so they know what to test. They turn vague stakeholder needs into clear, prioritized, testable requirements.

## 2. Theory (Exactly as in slides)

**Conceptual flow (Slide 8):**
```
Stakeholder Needs               Solution Requirements
(Unorganized, Not prioritized,   (Organized, Prioritized,
Incomplete, Unverified)    →     Complete, Verified)
            [Requirements Analysis]
```

## 3. Comparison Table — Phase 1: Requirement Analysis

| Element | Details (from slides) |
|---------|------------------------|
| **Inputs** | • Business Requirements Document (BRD) <br> • Functional Requirements (FRS) <br> • Meetings with stakeholders |
| **Activities** | • Analyze requirements for testability <br> • Identify types of testing needed <br> • Review risks and priorities <br> • Identify gaps or missing areas |
| **Outputs** | • Requirement Traceability Matrix (**RTM**) <br> • Test automation feasibility <br> • Clarification questions or assumptions |
| **Tools** | • JIRA, Confluence <br> • Excel, RTM tools (e.g., Jama Connect) <br> • Requirement analysis templates |

## 4. PRO TIPS
- **Key term to memorize:** **RTM (Requirement Traceability Matrix)** — main output of Phase 1.
- **A4 Sheet:** *Phase 1 → input: BRD/FRS → activity: analyze testability + risks → output: RTM → tools: JIRA, Confluence.*

## Quick Recap
- Phase 1 = understand WHAT to test.
- Main output: **RTM**.
- Tools: JIRA, Confluence, Excel.

---

# SLIDE 11 — Requirement Traceability Matrix (RTM)

## 1. Plain English Explanation
A **document that links** every requirement to its **design + development + test cases** — so you can prove that every requirement is being tested.

## 2. Theory (Exactly as in slides)
> A document that maps each requirement to its corresponding design, development, and testing elements.

## 3. Example Structure (from the slide)

| BR_ID | BR_User Case | FR_ID | FR_User Case | Priority | Test Case ID | Status | Comments |
|-------|---------------|-------|---------------|----------|---------------|---------|----------|
| BR_1 | Product Listing | FR_1 | Sort by | High | TC_001, TC_002, TC_004 | Finished | Dec 1: started → Dec 15: passed |
| | | FR_2 | Filters | High | TC_001, TC_002, TC_003 | Finished | Same flow |
| BR_2 | Payment Module | FR_3 | By Credit Card | High | TC_005 | In Progress | Dec 1: testing started |
| | | FR_4 | By Debit Card | High | TC_006 | In Progress | Dec 1: testing started |
| | | FR_5 | By Reward/Referral | Medium | TC_007, TC_008 | Not Started | — |

## 4. PRO TIPS
- **High-frequency MCQ target:** "What is the main output of the Requirement Analysis phase?" → **RTM**.
- RTM = links Business Requirement → Functional Requirement → Test Cases.
- **A4 Sheet:** Sketch a simple 4-column mini RTM: BR | FR | Test Case | Status.

## Quick Recap
- RTM maps Requirement → Test Case.
- Ensures **complete test coverage** of requirements.

---

# SLIDES 12 & 13 — PHASE 2: Test Planning

## 1. Plain English Explanation
Decide **HOW** to test. The lead tester writes a master plan covering scope, strategy, schedule, resources, and risk.

## 2. Comparison Table — Phase 2: Test Planning

| Element | Details (from slides) |
|---------|------------------------|
| **Inputs** | • Requirement documents <br> • RTM <br> • High-level project plan <br> • Risk assessment |
| **Activities** | • Define test **scope** <br> • Identify test **strategy and approach** <br> • Estimate **time, effort, and resources** <br> • **Assign roles and responsibilities** |
| **Outputs** | • **Test Plan** document <br> • Effort estimation sheet <br> • Resource plan |
| **Tools** | • TestRail, Xray <br> • Microsoft Project, Excel <br> • Risk analysis tools |

## 3. PRO TIPS
- **Key output:** **Test Plan Document**.
- **Memory trick:** Phase 2 = "Plan the **Scope, Strategy, Time, Roles**" → S-S-T-R.

## Quick Recap
- Phase 2 = plan HOW to test.
- Main output: Test Plan.

---

# SLIDE 14 — Test Plan Template (Important Reference)

## 1. Plain English Explanation
A typical Test Plan has **multiple standard sections**. Memorize these — exam may ask "what does a Test Plan contain?"

## 2. Theory (From slide)

| Section | Contents |
|---------|----------|
| **Features to be Tested (In-Scope)** | Sign-up/Sign-in, Forget Password, Delete Account |
| **Features NOT to be Tested** | Edit Account Information, Create Multiple Accounts |
| **Test Levels & Test Types** | Levels: System, Acceptance. Types: Functional, Usability, Regression |
| **Estimation** | Sign-up/Sign-in: 6 hours, Forget Password: 1 hour, Delete Account: 1 hour |
| **Staffing & Training** | Manual Testers, Automation Testers, TestZephyr training (16h) |
| **Assumptions** | Developers deliver code on time, license for TestZephyr |
| **Exit Criteria** | No functional bugs, low-severity bugs only, ≤10% medium-severity bugs |
| **Suspension Criteria** | Critical bugs blocking testing |
| **Test Deliverables** | Test Cases, Bug Reports, Test Summary Report |
| **Test Environment** | OS: Windows 10, Server: QA Staging, Browser: Chrome (latest), Wi-Fi |
| **Risks** | Late delivery, QA environment down, unplanned vacations, critical recurring bugs |
| **Risk Mitigation** | Risk Acceptance, Transfer, Monitoring |
| **Test References** | User Stories, Figma Design, System Design |

## 3. PRO TIPS
- **Memorize 5-6 key sections** for a partial mark essay question.
- Most-tested sections: **Features in/out of scope, Exit Criteria, Suspension Criteria, Test Deliverables**.

## Quick Recap
- A Test Plan is multi-section. Know what's in each.
- Most-tested: Scope, Exit Criteria, Test Deliverables.

---

# SLIDES 15 & 16 — PHASE 3: Test Case Development

## 1. Plain English Explanation
Write the **actual test cases, test scripts, and test data** that will be used during execution.

## 2. Comparison Table — Phase 3: Test Case Development

| Element | Details (from slides) |
|---------|------------------------|
| **Inputs** | • Requirement documents <br> • Test Plan <br> • RTM |
| **Activities** | • Write **test cases & test scripts** <br> • Review and baseline test cases <br> • Create **test data** |
| **Outputs** | • Test cases <br> • Test scripts <br> • Test data <br> • **Reviewed and approved test cases** |
| **Tools** | • TestLink, Zephyr, TestRail <br> • Excel, Word <br> • SQL (for test data), Selenium (for test scripts) |

## 3. PRO TIPS
- **Key outputs:** Test Cases, Test Scripts, Test Data.
- **Selenium** appears here — automation tool for scripts.
- **A4 Sheet:** *Phase 3 → write & review test cases + scripts + data → tools: TestRail, Selenium.*

---

# SLIDE 17 — Test Scenario vs Test Case vs Test Script vs Test Data (MAJOR EXAM TABLE)

## 1. Plain English Explanation
These 4 terms sound similar but are distinct. Confusing them is a classic MCQ trap.

## 2. Comparison Table — The 4 Definitions

| Term | Definition (from slides) | Example |
|------|--------------------------|---------|
| **Test Scenario** | A **high-level idea** of what needs to be tested | "Verify that the user can successfully log in with valid credentials." |
| **Test Case** | A **detailed set of steps and expected results** to validate a specific part of the scenario | Title: Login with valid username/password<br>Steps: 1. Navigate to login page<br>2. Enter username<br>3. Enter password<br>4. Click Login<br>Expected: User is redirected to dashboard |
| **Test Script** | An **automated or manual script** that performs the steps in the test case | Selenium Python code: `driver.get(...)`, `driver.find_element(...).send_keys(...)`, `driver.click()`, `assert "Dashboard"` |
| **Test Data** | The **input values** used during testing | Username: `testuser`, Password: `password123` |

## 3. PRO TIPS
- **MEMORY TRICK — increasing detail level:** Scenario → Case → Script → Data
  - **Scenario** = WHAT (idea)
  - **Case** = HOW (steps)
  - **Script** = code (auto-execution)
  - **Data** = inputs used in the run
- **Common MCQ trap:** "A high-level idea of what to test is called?" → **Test Scenario** (NOT Test Case).
- **A4 Sheet:** This 4-row table verbatim.

## Quick Recap
- Scenario (high-level) → Case (steps) → Script (executable) → Data (input values).

---

# SLIDES 18 & 19 — PHASE 4: Test Environment Setup

## 1. Plain English Explanation
Set up the **hardware, software, servers, and network** environment where testing will run. Configure access for testers.

## 2. Comparison Table — Phase 4: Test Environment Setup

| Element | Details (from slides) |
|---------|------------------------|
| **Inputs** | • Environment requirements document <br> • Software and hardware specs |
| **Activities** | • Set up testing hardware/software <br> • Configure test servers, networks <br> • Validate setup |
| **Outputs** | • **Environment ready for testing** <br> • Test Environment checklist <br> • Access and credentials |
| **Tools** | • Cloud platforms (AWS, Azure) <br> • Configuration management tools |

## 3. PRO TIPS
- **Key tools:** AWS, Azure (cloud) — modern QA work often runs on cloud.
- **A4 Sheet:** *Phase 4 → setup HW/SW + servers + network + access → tools: AWS, Azure.*

---

# SLIDE 20 — Different Test Environments

## 1. Plain English Explanation
There are **9 standard types** of test environments — each serves a specific testing purpose.

## 2. Theory (From slide)
1. Development Environment
2. Integration Test Environment
3. System Test Environment
4. UAT (User Acceptance Testing) Environment
5. Staging / Pre-Production Environment
6. Performance / Load Testing Environment
7. Security Testing Environment
8. Mobile / Device Test Environment
9. Sandbox Environment

## 3. Comparison Table

| # | Environment | Purpose |
|---|-------------|---------|
| 1 | Development | Devs build & unit-test |
| 2 | Integration Test | Combine and test modules |
| 3 | System Test | Test full system end-to-end |
| 4 | UAT | Customer/end-user validation |
| 5 | Staging / Pre-Production | Mirror of production for final checks |
| 6 | Performance / Load Testing | Apply heavy load to measure speed |
| 7 | Security Testing | Penetration tests, vulnerability scans |
| 8 | Mobile / Device Test | Tests on phones/tablets/devices |
| 9 | Sandbox | Isolated experimentation environment |

## 4. PRO TIPS
- **Memorize at least 5–6** for partial marks.
- **High-value:** UAT, Staging, Performance/Load environments are the most-tested.
- **A4 Sheet:** 9-environment list.

## Quick Recap
- 9 standard test environments.
- Each environment matches a stage in the testing/release flow.

---

# SLIDES 21 & 22 — PHASE 5: Test Execution

## 1. Plain English Explanation
**Actually run the tests**, log every bug found, retest after fixes, and update the test result records.

## 2. Comparison Table — Phase 5: Test Execution

| Element | Details (from slides) |
|---------|------------------------|
| **Inputs** | • Approved test cases <br> • Test data <br> • Test environment |
| **Activities** | • **Execute test cases** <br> • **Log defects/bugs** <br> • Retest after fixes <br> • Update test results |
| **Outputs** | • **Test execution report** <br> • **Defect Report** <br> • Updated RTM |
| **Tools** | • **Selenium, Appium** (automation) <br> • **JIRA, Bugzilla, Mantis** (bug tracking) <br> • TestRail, Zephyr |

## 3. PRO TIPS
- **Tools to memorize:**
  - **Automation:** Selenium (web), Appium (mobile).
  - **Bug tracking:** JIRA, Bugzilla, Mantis.
- **A4 Sheet:** *Phase 5 → execute + log bugs + retest → tools: Selenium, JIRA, Bugzilla.*

---

# SLIDE 23 — Test Execution Report

## 1. Plain English Explanation
A dashboard showing **how many tests passed, failed, are in progress, or need retest**, along with overall percentage passed.

## 2. From Slide (Example metrics shown)
- **Tests with executions:** 30
- **Executions:** 67
- **Pass:** 39
- **Fail:** 24
- **In Progress:** 2
- **Retest:** 2
- **Test Execution Results:** 58% passed

## 3. PRO TIPS
- **Tool shown:** JIRA + TestFLO plugin.
- **A4 Sheet:** Test Execution Report = pass/fail/inprogress/retest summary + % passed.

---

# SLIDES 24 & 25 — PHASE 6: Test Cycle Closure

## 1. Plain English Explanation
Wrap up the test cycle. Decide if testing is complete, record metrics, capture lessons learned, archive everything.

## 2. Comparison Table — Phase 6: Test Cycle Closure

| Element | Details (from slides) |
|---------|------------------------|
| **Inputs** | • Test execution results <br> • Defect reports |
| **Activities** | • Evaluate **test completion criteria** <br> • Analyze **test coverage, defect density** <br> • Document **lessons learned** <br> • Archive test artifacts |
| **Outputs** | • **Test Summary Report** <br> • Test metrics & closure checklist <br> • **Lessons learned document** |
| **Tools** | • Excel / Google Sheets (reporting) <br> • Reporting tools (QMetry, TestRail) <br> • Confluence, SharePoint (documentation) |

## 3. PRO TIPS
- **Key output:** **Test Summary Report**.
- **Key metrics analyzed:** test coverage + defect density.
- **A4 Sheet:** *Phase 6 → evaluate completion + metrics + lessons → output: Test Summary Report.*

## Quick Recap
- Phase 6 = wrap up + report.
- Output: Test Summary Report + Lessons Learned.

---

# SLIDE 26 — Test Metrics (Process / Product / Project)

## 1. Plain English Explanation
3 categories of metrics measured during the test cycle.

## 2. Comparison Table — 3 Metric Categories

| Category | Metrics (from slides) |
|----------|------------------------|
| **Process Metrics** | • Test Case Effectiveness <br> • Cycle Time <br> • Defect Fixing Time |
| **Product Metrics** | • Number of Defects <br> • Defect Severity <br> • Passed/Failed Test Cases |
| **Project Metrics** | • Test Coverage <br> • Cost of Testing <br> • Budget / Schedule Variance |

## 3. PRO TIPS
- **High-frequency MCQ:** "Test Coverage" → falls under **Project metrics**.
- **Memory trick:** Process = HOW we test. Product = WHAT we tested. Project = how the OVERALL effort is going.
- **A4 Sheet:** This 3-column table verbatim.

## Quick Recap
- 3 metric categories: Process, Product, Project — 3 examples each.

---

# SLIDE 27 — STLC In Summary (BIG OVERVIEW TABLE)

## 2. Theory (Exactly as in slides)

| Phase | One-line summary |
|-------|-------------------|
| **Requirement Analysis** | Understand what to test |
| **Test Planning** | Plan how to test |
| **Test Case Development** | Write test steps |
| **Test Environment Setup** | Get systems ready |
| **Test Execution** | Run tests, find bugs |
| **Test Closure** | Wrap up and report |

## 3. PRO TIPS
- **HIGH-VALUE FOR ESSAYS:** Use this as your **2-mark-per-phase** one-line answer.
- **Memory anchor:** "Understand → Plan → Write → Set up → Run → Wrap up."

## Quick Recap
- 6 phases → 6 one-line summaries.
- The order is fixed and frequently asked.

---

# SLIDE 28 — Challenges in STLC

## 2. Theory (Exactly as in slides)
- Unclear or Changing Requirements
- Time Constraints
- Lack of Collaboration
- Environment Issues
- Tooling and Automation Challenges
- Frequent Scope Creep or Last-Minute Changes
- Knowledge Gaps / Inexperienced Testers

## 3. PRO TIPS
- **7 challenges** → memorize for an easy 7-mark essay question.
- **A4 Sheet:** *Challenges: Unclear reqs, Time, Collaboration, Environment, Tools, Scope creep, Knowledge gaps.*

---

# SLIDES 29 & 30
*Quiz slide + Thank You slide. No teaching content.*

---

# 🎯 EXTRA EXAMPLES (Beyond Slides)

### Example A — Simple
**Spec:** A team is testing an e-commerce site's checkout module.

| Phase | What happens in this project |
|-------|-------------------------------|
| 1. Requirement Analysis | Read BRD/FRS. Build RTM with checkout requirements. |
| 2. Test Planning | Create Test Plan; scope = cart + payment + order confirmation. |
| 3. Test Case Development | Write test cases like "TC_001: Add to cart with valid product." |
| 4. Test Environment Setup | Set up Staging environment with test product DB. |
| 5. Test Execution | Run tests in JIRA + Selenium; log bugs. |
| 6. Test Closure | Final report: 95% pass, 3 medium bugs deferred. |

---

### Example B — Complex
**Spec:** Banking app testing across 4 modules: Login, Transfer, Statement, Notifications.

| Phase | Deliverable |
|-------|-------------|
| 1. Requirement Analysis | RTM linking each banking requirement (BR_1–BR_15) to test cases. |
| 2. Test Planning | Test Plan covering 4 modules + risks (regulatory, time, env). |
| 3. Test Case Development | 250+ test cases, 50 automated scripts in Selenium. |
| 4. Test Environment Setup | UAT environment + Performance environment for load testing. |
| 5. Test Execution | Run; log defects in JIRA; 17 critical → fixed and retested. |
| 6. Test Closure | Final report shows 98% pass; Lessons Learned: improve test data setup. |

---

# 📊 MASTER COMPARISON TABLE — ALL 6 STLC PHASES

| Phase | Inputs | Activities | Outputs | Tools |
|-------|--------|------------|---------|-------|
| **1. Req Analysis** | BRD, FRS, stakeholder meetings | Analyze testability, types, risks, gaps | **RTM**, automation feasibility, clarifications | JIRA, Confluence, Excel |
| **2. Test Planning** | Req docs, RTM, project plan, risk | Define scope, strategy, estimate, assign roles | **Test Plan**, effort estimation, resource plan | TestRail, Xray, MS Project |
| **3. Test Case Dev** | Req docs, Test Plan, RTM | Write test cases/scripts, review, create test data | Test cases, scripts, data, approved cases | TestLink, Zephyr, Selenium, SQL |
| **4. Env Setup** | Env req doc, HW/SW specs | Set up HW/SW, configure servers, validate | **Env ready**, checklist, access | AWS, Azure, config mgmt |
| **5. Test Execution** | Approved tests, test data, env | Execute, log defects, retest, update | **Test exec report**, defect report, updated RTM | Selenium, Appium, JIRA, Bugzilla |
| **6. Test Closure** | Test exec results, defect reports | Evaluate completion, analyze metrics, lessons, archive | **Test Summary Report**, lessons learned | Excel, QMetry, Confluence |

---

# 📝 MCQ PRACTICE — LECTURE 8

---

### Q1. The main output of Phase 1 (Requirement Analysis) in STLC is:
A) Test Plan
B) **Requirement Traceability Matrix (RTM)** ✅
C) Test Summary Report
D) Defect Report

**Answer: B (Slide 10)**

---

### Q2. Which STLC phase produces the Test Plan document?
A) Requirement Analysis
B) **Test Planning** ✅
C) Test Case Development
D) Test Execution

**Answer: B (Slide 13)**

---

### Q3. A high-level idea of what needs to be tested is called:
A) Test Case
B) Test Script
C) **Test Scenario** ✅
D) Test Data

**Answer: C (Slide 17)**

---

### Q4. Which of the following is NOT a phase in STLC?
A) Test Planning
B) Test Execution
C) **Deployment Testing** ✅
D) Test Closure

**Answer: C — "Deployment Testing" is not an STLC phase (Slide 4)**

---

### Q5. Selenium and Appium are most commonly used in which STLC phase?
A) Requirement Analysis
B) Test Planning
C) **Test Execution** ✅
D) Test Closure

**Answer: C (Slide 22)**

---

### Q6. "Test Coverage" is classified under which type of metrics?
A) Process Metrics
B) Product Metrics
C) **Project Metrics** ✅
D) Performance Metrics

**Answer: C (Slide 26)**

---

### Q7. STLC is called a "cycle" because:
A) It only runs once
B) **It involves feedback loops, rework, iterations, and continuous improvement** ✅
C) It is identical to SDLC
D) It only deals with closure

**Answer: B (Slide 4)**

---

### Q8. The Test Summary Report is the main output of:
A) Test Case Development
B) Test Execution
C) Test Environment Setup
D) **Test Cycle Closure** ✅

**Answer: D (Slide 25)**

---

### Q9. Which of these is the correct order of STLC phases?
A) Test Planning → Requirement Analysis → Test Execution → Closure
B) **Requirement Analysis → Test Planning → Test Case Development → Test Env Setup → Test Execution → Test Closure** ✅
C) Test Case Development → Test Planning → Execution → Closure
D) Requirement Analysis → Execution → Test Planning → Closure

**Answer: B (Slide 4)**

---

### Q10. Which environment is used by the customer/end user to validate the software?
A) Development Environment
B) Sandbox Environment
C) **UAT Environment** ✅
D) Integration Test Environment

**Answer: C (Slide 20)**

---

# 📌 LECTURE 8 — A4 REFERENCE SHEET MINI-SECTION

```
STLC OVERVIEW
  Definition: Systematic approach to testing → meets reqs + bug-free
  Called a CYCLE because: feedback loops, rework, iterations, continuous improvement

SDLC vs STLC (key contrasts):
  SDLC = Develop. Starts at project start. Devs/Architects.
        Output: Working software + code.
  STLC = Test. Starts when requirements are ready. Testers/QA.
        Output: Test cases + bug reports + test summary.

6 STLC PHASES (R-P-D-E-E-C):
  1. Requirement Analysis     → understand WHAT to test → RTM
  2. Test Planning            → plan HOW to test → Test Plan
  3. Test Case Development    → write test cases/scripts/data → Approved cases
  4. Test Environment Setup   → HW/SW/servers/network ready → Env ready
  5. Test Execution           → run + log bugs + retest → Exec report
  6. Test Cycle Closure       → metrics + lessons + archive → Test Summary Report

EVERY PHASE STRUCTURE: I-A-O-T (Inputs / Activities / Outputs / Tools)

TEST SCENARIO vs CASE vs SCRIPT vs DATA (4 levels):
  Scenario  = high-level idea ("verify login works")
  Case      = detailed steps + expected output
  Script    = automated or manual execution code (Selenium)
  Data      = input values (testuser / password123)

RTM (Requirement Traceability Matrix):
  Maps Business Req → Functional Req → Test Case
  Ensures complete coverage

TEST ENVIRONMENTS (9 types):
  Dev / Integration / System / UAT / Staging / Performance
  / Security / Mobile / Sandbox

TEST METRICS (3 categories):
  Process  → Test Case Effectiveness, Cycle Time, Defect Fix Time
  Product  → # Defects, Defect Severity, Passed/Failed Cases
  Project  → Test Coverage, Cost of Testing, Budget/Schedule Variance

7 STLC CHALLENGES:
  Unclear/Changing Reqs, Time Constraints, Lack of Collaboration,
  Env Issues, Tooling Challenges, Scope Creep, Inexperienced Testers

KEY TOOLS BY PHASE:
  P1 — JIRA, Confluence, Jama Connect
  P2 — TestRail, Xray, MS Project
  P3 — TestLink, Zephyr, Selenium, SQL
  P4 — AWS, Azure
  P5 — Selenium, Appium, JIRA, Bugzilla
  P6 — Excel, QMetry, Confluence, SharePoint
```

---

# ✅ LECTURE 8 — DONE

This lecture is **all about memorization** — phases, their components, RTM, Test Plan sections, Test Metrics categories, and tools.

**Top 3 exam-likely essay questions for this lecture:**
1. "Explain the 6 phases of STLC with Inputs, Activities, Outputs, and Tools for each."
2. "Compare SDLC vs STLC in tabular form."
3. "Differentiate between Test Scenario, Test Case, Test Script, and Test Data with examples."

Reply **"done"** to continue to **Lecture 9**.
