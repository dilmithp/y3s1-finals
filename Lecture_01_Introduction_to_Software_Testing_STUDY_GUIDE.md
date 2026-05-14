# LECTURE 1 — INTRODUCTION TO SOFTWARE TESTING
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **⚠️ IMPORTANT NOTE FOR THIS LECTURE**
> Lecture 1 is a **conceptual/theory lecture only**. It contains **NO mathematical formulas, NO code analysis, and NO software metrics (CC / CFS / WCC)**. Those topics appear in Lectures 4, 5, and 7. So in this guide you will not see LaTeX formulas, token tables, or weight tables — those will appear in the respective metric lectures.
>
> For Lecture 1, your exam preparation focus is **MCQs and Essay-style definitions**.

---

# SLIDE 1 — Title Slide

**Content of slide:** "Software Engineering Process and Quality Management — Lecture 1 – Introduction to Software Testing"

No content to teach here. Move on.

---

# SLIDE 2 — What is Software Quality?

## 1. Plain English Explanation
Software Quality means *how good* a piece of software is. But "good" depends on **who you ask** — the person who builds the software has one view, and the person who uses it has another view.

## 2. Theory (Exactly as in slides)

> **Quality is conformance to requirements (Producer View)** — *Philip Crosby*
>
> **Quality is fit for use (Customer View)** — *Joseph Juran & Edwards Deming*

## 3. Comparison Table

| View | Definition | Author(s) | Focus | Example |
|------|------------|-----------|-------|---------|
| **Producer View** | Quality is **conformance to requirements** | Philip Crosby | Did we build what the spec said? | The SRS said "login must take < 2 seconds." If it does, quality is met. |
| **Customer View** | Quality is **fit for use** | Joseph Juran & Edwards Deming | Does it actually solve the user's problem? | A user can log in fast — but if they can't find the logout button, it's not "fit for use." |

## 4. Real-World Application
A bank app may technically conform to every requirement (Producer View: ✅) but customers still hate it because navigation is confusing (Customer View: ❌). Modern teams aim to satisfy **both views** simultaneously.

## 5. Extra Examples (Beyond the slides)

**Example A — Simple:**
A calculator app's requirement: *"Must perform addition, subtraction, multiplication, division."*
- Producer View: All four operations work → Quality met.
- Customer View: But the buttons are tiny and hard to tap on mobile → Not fit for use.

**Example B — Complex:**
A hospital management system passes all 1,200 written requirements (Crosby happy), yet nurses cannot enter a patient's blood pressure in under 30 seconds during emergencies (Juran/Deming unhappy). **Both viewpoints must be satisfied for true quality.**

## 6. PRO TIPS
- **Memory trick:** "Crosby = Conformance" (both start with **C**). "Juran = Use" (Juran sounds like "Use-an").
- **Common exam trap:** Don't mix up the authors. Crosby ≠ Juran/Deming.
- **A4 Sheet:** Write: *Crosby → Producer → Conformance to Requirements | Juran & Deming → Customer → Fit for Use*

## Quick Recap
- Producer View (Crosby) = meets the **spec**.
- Customer View (Juran & Deming) = meets the **need**.
- Both definitions together = true software quality.

---

# SLIDE 3 — What is Software Testing?

## 1. Plain English Explanation
Software testing is the process of **checking** a piece of software to find bugs and make sure it works the way it's supposed to.

## 2. Theory (Exactly as in slides)
> Software testing is the process of evaluating a software application to identify defects and ensure it meets quality standards.

## 3. Key Phrases to Memorize
| Phrase | Why It Matters |
|--------|----------------|
| **Process of evaluating** | Testing is systematic, not random. |
| **Identify defects** | Goal #1: find bugs. |
| **Ensure it meets quality standards** | Goal #2: confirm quality. |

## 4. Real-World Application
Before WhatsApp ships a new version, hundreds of testers click every button, send every emoji, try every device — to "evaluate" the app and "identify defects" before it reaches 2 billion users.

## 5. PRO TIPS
- This is a **direct definition question** — write it word-for-word in your essay if asked "Define software testing."
- **A4 Sheet:** *Software Testing = process of evaluating software to identify defects and ensure it meets quality standards.*

## Quick Recap
- Testing = evaluation activity.
- Two goals: find defects, confirm quality.
- Memorize the definition verbatim.

---

# SLIDE 4 — Importance of Software Testing for Quality

## 1. Plain English Explanation
Why bother testing? Because testing catches problems **early**, makes sure users actually get what they need, makes the product safer and more reliable, and saves money long-term.

## 2. Theory (Exactly as in slides)
- Helps detect defects early
- Ensures software meets business and user needs
- Improves reliability, security, and maintainability
- Reduces post-release failures and maintenance costs

## 3. Comparison Table — The Four Benefits

| # | Benefit | What it means | Why it matters |
|---|---------|---------------|----------------|
| 1 | Detect defects early | Find bugs during development, not after release | A bug found in design costs 100× less than one found after release |
| 2 | Meets business & user needs | Validates the right thing was built | Wrong product = wasted money even if bug-free |
| 3 | Improves reliability, security, maintainability | Software stays up, stays safe, stays editable | Long-term product health |
| 4 | Reduces post-release failures & costs | Fewer bugs reach customers | Saves support cost, brand damage, lawsuits |

## 4. Real-World Application
Banks invest 30–40% of project budget in testing because **one undetected bug** (like Knight Capital's, next slide) can wipe out hundreds of millions of dollars in minutes.

## 5. PRO TIPS
- **Memory trick:** "DEMR" → **D**etect early, **E**nsure needs, **M**aintain (reliability/security/maintainability), **R**educe costs.
- Exam tip: If asked "Why is testing important?" — list all **four points** for full marks.

## Quick Recap
- Early defect detection saves cost.
- Testing confirms business + user needs.
- Improves three "-ities": reliability, security, maintainability.
- Lowers post-release maintenance.

---

# SLIDE 5 — What Happens When Testing Is Not Done Properly?

## 1. Plain English Explanation
The slide lists **three famous real-world disasters** that happened because of poor or missing software testing.

## 2. Theory (Exactly as in slides)
- **Windows 10 Update Deletes User Files (2018)**
- **Knight Capital Trading Glitch (2012) — $440 Million Loss in 45 Minutes**
- **NASA's Mars Climate Orbiter (1999) — $327 Million Lost**

## 3. Comparison Table — Three Famous Testing Failures

| Year | System | What Went Wrong | Cost / Impact |
|------|--------|-----------------|----------------|
| 1999 | NASA Mars Climate Orbiter | Software unit-conversion failure | $327 Million lost |
| 2012 | Knight Capital Trading Platform | Trading glitch in deployed code | $440 Million lost in 45 minutes |
| 2018 | Windows 10 Update | Update deleted user files | Reputation damage; users lost personal data |

## 4. Real-World Application
These are the **classic exam case studies**. The exam may ask: *"Give an example where lack of testing caused major loss."* Memorize at least two of the three with year + cost.

## 5. PRO TIPS
- **Memory trick (year order):** "1999 NASA, 2012 Knight, 2018 Windows" → ascending years.
- **Cost order trick:** "Knight > NASA" ($440M > $327M).
- **A4 Sheet:** Write the table above — clean, short, scoreable.

## Quick Recap
- 3 famous failures: Mars Orbiter (1999), Knight Capital (2012), Windows 10 (2018).
- All caused by inadequate software testing.
- These are go-to examples for essay questions.

---

# SLIDE 6 — Quiz 1
*Slide contains a QR-code quiz only — no teaching content. Skip.*

---

# SLIDE 7 — How is Software Testing Done?

## 1. Plain English Explanation
There are **four main ways** to do testing. Two compare *how* tests are run (by hand or by tool), and two compare *whether* the code is actually executed (only read, or actually run).

## 2. Theory (Exactly as in slides)
- **Manual Testing:** Performed without automation tools
- **Automated Testing:** Uses scripts and tools
- **Static Testing:** Reviews and inspections
- **Dynamic Testing:** Executing test cases

## 3. Comparison Table — The Four Approaches

| Type | Definition (from slides) | Code is executed? | Tool used? | Example |
|------|--------------------------|-------------------|-------------|---------|
| **Manual Testing** | Performed without automation tools | Yes | No | Tester clicks through a login form by hand |
| **Automated Testing** | Uses scripts and tools | Yes | Yes | Selenium script runs 500 test cases overnight |
| **Static Testing** | Reviews and inspections | **No** | Optional | Code review of a Java file before running it |
| **Dynamic Testing** | Executing test cases | **Yes** | Either | Running the program with test inputs |

## 4. Real-World Application
- **Manual + Static** → Used for new, exploratory areas (UX checking, requirements review).
- **Automated + Dynamic** → Used for regression testing (re-running 1,000s of tests on every code change).

## 5. PRO TIPS
- **Memory trick:**
  - **Manual ↔ Automated** = *Who runs the test?* (human vs script)
  - **Static ↔ Dynamic** = *Is the code running?* (no vs yes)
- **Common confusion:** Static testing is **NOT** the same as Manual testing. A code review is static AND manual. A unit test is dynamic AND automated.
- **A4 Sheet:** Draw a 2×2 grid → Manual/Automated × Static/Dynamic.

## Quick Recap
- 4 approaches in 2 pairs.
- Manual vs Automated = human vs tool.
- Static vs Dynamic = not-running vs running.

---

# SLIDE 8 — Quiz 2
*QR-code quiz slide — no teaching content. Skip.*

---

# SLIDE 9 — Basic Terminology in Software Testing

## 1. Plain English Explanation
Five core words every tester must know. **These are extremely common MCQ targets**.

## 2. Theory (Exactly as in slides)
- **Bug/Defect:** A flaw causing incorrect results
- **Test Case:** Set of conditions for testing
- **Test Plan:** Strategy for testing
- **Validation:** Ensures software meets user needs
- **Verification:** Ensures software meets requirements

## 3. Comparison Table — The Five Terms

| Term | Definition (from slides) | Quick-Recall Example |
|------|--------------------------|----------------------|
| **Bug / Defect** | A flaw causing incorrect results | 2 + 2 returns 5 |
| **Test Case** | Set of conditions for testing | "Input: 2 and 2 → Expected output: 4" |
| **Test Plan** | Strategy for testing | The document listing what/when/how to test |
| **Validation** | Ensures software meets **user needs** | "Did we build the right product?" |
| **Verification** | Ensures software meets **requirements** | "Did we build the product right?" |

## 4. Validation vs Verification — Critical Exam Distinction

| Aspect | Verification | Validation |
|--------|---------------|------------|
| Question it answers | "Are we building the product **right**?" | "Are we building the **right** product?" |
| Reference point | **Requirements / Spec** | **User needs / Real use** |
| When | During development | Near the end / at release |
| Examples | Code reviews, walkthroughs, inspections | User acceptance testing, beta testing |

## 5. Real-World Application
A WhatsApp build can pass verification (every spec'd feature works) but fail validation (users wanted a feature like "edit message" that wasn't in the spec).

## 6. PRO TIPS
- **The most-tested MCQ in this course:** Verification vs Validation.
- **Memory trick:**
  - **V**erification = **V**s the spec (matches requirements doc).
  - V**a**lidation = vs the user (**a**ctual user need).
- **A4 Sheet — must include:**
  *Verification → "Are we building product right?" → vs Requirements*
  *Validation → "Are we building the right product?" → vs User needs*

## Quick Recap
- 5 must-know terms: Bug, Test Case, Test Plan, Validation, Verification.
- V&V is the highest-frequency exam concept.
- Verification = spec match; Validation = user-need match.

---

# SLIDES 10 & 11 — Types of Software Testing

## 1. Plain English Explanation
Testing splits into **two big families**:
1. **Functional** = checks *what the software does*.
2. **Non-Functional** = checks *how the software does it*.

## 2. Theory (Exactly as in slides)

**Functional Testing:**
- Unit Testing
- Integration Testing
- System Testing
- User Acceptance Testing (UAT)

**Non-Functional Testing:**
- Performance Testing
- Security Testing
- Usability Testing
- Compatibility Testing

## 3. Comparison Table — Functional Sub-Types

| Sub-Type | What it tests | Example | Who performs it? |
|----------|---------------|---------|------------------|
| **Unit Testing** | Smallest piece of code (a single method/function) | Test that `add(2,2)` returns 4 | Developer |
| **Integration Testing** | How modules talk to each other | Login module + Database module work together | Developer / Tester |
| **System Testing** | Whole product end-to-end | Full e-commerce site checkout flow | QA team |
| **User Acceptance Testing (UAT)** | Real users verify the software | Customer tries app before sign-off | Real end users |

## 4. Comparison Table — Non-Functional Sub-Types

| Sub-Type | What it tests | Example |
|----------|---------------|---------|
| **Performance Testing** | Speed, response time, load | 10,000 users hit the site at once |
| **Security Testing** | Resistance to attacks | SQL injection on login form |
| **Usability Testing** | Ease of use / UX | Can a 60-year-old user place an order? |
| **Compatibility Testing** | Works on different OS/browsers/devices | App on Chrome, Firefox, Safari, iOS, Android |

## 5. Real-World Application
- A bank: **Performance + Security** are top priorities.
- An e-learning app: **Usability + Compatibility** matter most.
- A small embedded device: **Unit + Integration** are heavy.

## 6. PRO TIPS
- **Memory trick — Functional levels (small → big):** "**U-I-S-U**" = **U**nit, **I**ntegration, **S**ystem, **UAT**.
- **Memory trick — Non-Functional 4:** "**P-S-U-C**" = **P**erformance, **S**ecurity, **U**sability, **C**ompatibility.
- **A4 Sheet:** Two side-by-side columns: Functional (4) | Non-Functional (4).

## Quick Recap
- 2 families: Functional (what) and Non-Functional (how).
- 4 sub-types each → memorize all 8.
- Levels increase in scope: Unit < Integration < System < UAT.

---

# SLIDE 12 — Quiz 3
*QR-code quiz — skip.*

---

# SLIDE 13 — Software Testing Principles

## 1. Plain English Explanation
The **7 fundamental rules** every tester lives by. Each one is small but profound. These are **frequent essay/MCQ targets**.

## 2. Theory (Exactly as in slides)
1. Testing shows presence of defects, not absence
2. Exhaustive testing is impossible
3. Early testing saves time & cost
4. Defect clustering
5. Pesticide paradox
6. Testing is context-dependent
7. Absence of errors is a fallacy

## 3. Comparison Table — The 7 Principles Explained

| # | Principle | Meaning | Easy Example |
|---|-----------|---------|---------------|
| 1 | Testing shows presence of defects, not absence | Tests can find bugs but cannot prove there are NO bugs left | Finding no rats in 1 trap ≠ no rats in the house |
| 2 | Exhaustive testing is impossible | You can't test every possible input/path | A field accepting "any text" has infinite values |
| 3 | Early testing saves time & cost | Find bugs ASAP — cheaper to fix | Bug in design = fix the doc; bug in production = patch + customer support cost |
| 4 | Defect clustering | A small % of modules contain the most bugs | 20% of features hold 80% of defects (Pareto) |
| 5 | Pesticide paradox | Repeating the same tests stops finding new bugs | Need new test cases over time |
| 6 | Testing is context-dependent | Test a game ≠ test a bank app | Different domains need different strategies |
| 7 | Absence of errors is a fallacy | Bug-free ≠ useful | App can be bug-free but useless if it doesn't meet user needs |

## 4. Real-World Application
- **Principle 5 (Pesticide Paradox):** Netflix rotates its test cases regularly so new bugs in old features get caught.
- **Principle 4 (Defect Clustering):** A bank focuses 80% of QA effort on the 20% of modules (e.g., payments) that historically hold most defects.

## 5. PRO TIPS
- **Memory trick (acronym): "T-E-E-D-P-C-A"** → **T**esting shows defects, **E**xhaustive impossible, **E**arly saves cost, **D**efect clustering, **P**esticide paradox, **C**ontext dependent, **A**bsence of errors is fallacy.
- **High-value exam quote:** *"Testing shows the presence of defects, not their absence"* — write this verbatim.
- **A4 Sheet:** All 7 principles in a 7-line list with one example each.

## Quick Recap
- 7 principles → memorize all in order using "T-E-E-D-P-C-A".
- Principles 1 & 7 are most likely to be MCQ-tested (subtle wording).
- Defect Clustering ↔ Pareto Principle in real life.

---

# SLIDE 14 — Software Testing Process

## 1. Plain English Explanation
The testing **lifecycle** — 6 stages, in this exact order, that every testing team goes through.

## 2. Theory (Exactly as in slides)
1. Requirement Analysis
2. Test Planning
3. Test Case Development
4. Test Execution
5. Defect Reporting
6. Test Closure

## 3. Comparison Table — The 6 Stages

| # | Stage | What Happens | Deliverable |
|---|-------|---------------|-------------|
| 1 | **Requirement Analysis** | Read & understand the SRS / specs | List of testable requirements |
| 2 | **Test Planning** | Decide approach, tools, schedule | Test Plan document |
| 3 | **Test Case Development** | Write the actual test cases | Test Case repository |
| 4 | **Test Execution** | Run the tests | Test execution report |
| 5 | **Defect Reporting** | Log every bug found | Bug / defect log |
| 6 | **Test Closure** | Wrap up, summarize, archive | Test closure report |

## 4. Real-World Application
In agile sprints, this 6-step process runs **every sprint** in miniature — testers go from analysis to closure in 1–2 weeks per sprint.

## 5. PRO TIPS
- **Memory trick:** "**R**eal **P**eople **D**evelop **E**xcellent **D**efect-free **C**ode" → R-P-D-E-D-C → matches the 6 stages.
- **Common exam question:** "List the steps of the software testing process in order." → write all 6, in order, for full marks.
- **A4 Sheet:** 6 stages in a vertical flow.

## Quick Recap
- 6 ordered stages: Req. Analysis → Test Planning → Test Case Dev → Test Execution → Defect Reporting → Test Closure.
- Order matters in exams.

---

# SLIDE 15 — Common Challenges in Software Testing

## 1. Plain English Explanation
Five real-world headaches that testing teams face daily.

## 2. Theory (Exactly as in slides)
- Changing requirements
- Time constraints
- Complexity in large software systems
- Defect leakage
- Need for skilled testers

## 3. Comparison Table — The 5 Challenges

| # | Challenge | What it means | Real Example |
|---|-----------|----------------|---------------|
| 1 | Changing requirements | Client keeps tweaking the spec | "Now add dark mode" 3 days before release |
| 2 | Time constraints | Tight deadlines → rushed testing | Sprint ends Friday, testing only got 1 day |
| 3 | Complexity in large software | Millions of lines, many integrations | Banking systems with 100+ microservices |
| 4 | Defect leakage | Bugs slip past QA into production | Customers find a bug the team missed |
| 5 | Need for skilled testers | Good testers are hard to find | Domain knowledge + tools + analytical mindset |

## 4. Real-World Application
"Defect Leakage" is a common KPI tracked at companies — number of bugs caught by customers vs by QA. Low leakage = mature testing process.

## 5. PRO TIPS
- **Memory trick:** "**C-T-C-D-S**" → **C**hanging, **T**ime, **C**omplexity, **D**efect leakage, **S**killed testers needed.
- **Essay tip:** If asked to list challenges, give all 5 + a 1-line explanation each → easy full marks.
- **A4 Sheet:** 5-line bullet list.

## Quick Recap
- 5 challenges to memorize.
- "Defect Leakage" is a specific term — don't forget it.

---

# SLIDE 16 — Quiz 4
*QR-code quiz — skip.*

---

# SLIDE 17 — Conclusion

## 1. Plain English Explanation
The wrap-up: testing is essential. You need to know **principles, types, and processes** to be effective.

## 2. Theory (Exactly as in slides)
> Software testing is critical for ensuring quality, reliability, and security. Understanding principles, types, and processes helps teams build better software.

## 3. PRO TIPS
- Use this exact sentence as the **conclusion of your essay answer** for any "Why is testing important?" type question.
- **A4 Sheet:** Already covered by previous slides — no new items needed.

## Quick Recap
- Testing ensures quality, reliability, security.
- Master 3 pillars: **principles, types, processes**.

---

# SLIDE 18 — Feedback
*QR-code feedback slide — skip.*

---

# 📝 MCQ PRACTICE — LECTURE 1
*All questions based strictly on the slide content above.*

---

### Q1. Who defined quality as "conformance to requirements"?
A) Joseph Juran
B) **Philip Crosby** ✅
C) Edwards Deming
D) Tim Berners-Lee

**Correct Answer: B — Philip Crosby (Producer View, Slide 2)**

---

### Q2. Which testing principle states that running the same tests repeatedly stops finding new bugs?
A) Defect clustering
B) **Pesticide paradox** ✅
C) Absence of errors is a fallacy
D) Early testing saves cost

**Correct Answer: B — Pesticide paradox (Slide 13)**

---

### Q3. Which of the following is NOT a Non-Functional Testing type?
A) Performance Testing
B) Security Testing
C) **Unit Testing** ✅
D) Usability Testing

**Correct Answer: C — Unit Testing (it is FUNCTIONAL, not non-functional, Slides 10–11)**

---

### Q4. In the software testing process, which step comes immediately after Test Case Development?
A) Test Planning
B) **Test Execution** ✅
C) Defect Reporting
D) Test Closure

**Correct Answer: B — Test Execution (Slide 14)**

---

### Q5. "Are we building the product right?" refers to:
A) Validation
B) **Verification** ✅
C) UAT
D) Test Planning

**Correct Answer: B — Verification (matches requirements / spec, Slide 9)**

---

### Q6. Which famous failure caused a $440 million loss in 45 minutes?
A) NASA Mars Climate Orbiter
B) **Knight Capital Trading Glitch** ✅
C) Windows 10 update
D) Ariane 5 rocket

**Correct Answer: B — Knight Capital (2012, Slide 5)**

---

### Q7. Static Testing is best described as:
A) Executing test cases
B) Performance load test
C) **Reviews and inspections** ✅
D) Running automated scripts

**Correct Answer: C — Reviews and inspections (Slide 7)**

---

# 📌 LECTURE 1 — A4 REFERENCE SHEET MINI-SECTION

Suggested compact entries (final A4 sheet will combine all 11 lectures):

```
SOFTWARE QUALITY:
  Crosby (Producer)   = Conformance to requirements
  Juran/Deming (Cust) = Fit for use

SOFTWARE TESTING DEF:
  Process of evaluating software → identify defects + ensure quality

TESTING APPROACHES:
  Manual / Automated  (who runs it)
  Static / Dynamic    (is code running?)

V & V:
  Verification = product right?  → vs Requirements
  Validation   = right product?  → vs User needs

5 BASIC TERMS:
  Bug, Test Case, Test Plan, Validation, Verification

FUNCTIONAL TYPES (U-I-S-U):
  Unit → Integration → System → UAT

NON-FUNCTIONAL TYPES (P-S-U-C):
  Performance, Security, Usability, Compatibility

7 PRINCIPLES (T-E-E-D-P-C-A):
  1. Defects, not absence
  2. Exhaustive impossible
  3. Early testing saves cost
  4. Defect clustering
  5. Pesticide paradox
  6. Context dependent
  7. Absence of errors = fallacy

6-STEP PROCESS:
  Req Analysis → Test Plan → Test Cases →
  Execution → Defect Report → Closure

5 CHALLENGES (C-T-C-D-S):
  Changing reqs, Time, Complexity, Defect leakage, Skilled testers

3 FAMOUS FAILURES:
  1999 NASA Mars Orbiter   ($327M)
  2012 Knight Capital       ($440M)
  2018 Windows 10 update    (deleted files)
```

---

# ✅ LECTURE 1 — DONE

This lecture is **purely conceptual** — no formulas, no code, no metrics. Your effort here is **memorization + understanding**, not calculation.

Next up after you reply **"done"** → **Lecture 2: Specification Based Test Case Design Techniques.**
