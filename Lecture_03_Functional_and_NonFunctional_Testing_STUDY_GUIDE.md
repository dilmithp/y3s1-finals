# LECTURE 3 — FUNCTIONAL AND NON-FUNCTIONAL TESTING
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **⚠️ IMPORTANT NOTE FOR THIS LECTURE**
> Lecture 3 is **pure conceptual content** — there are **NO formulas, NO code, NO calculations**. This is a high-volume terminology lecture: lots of testing types and sub-types to memorize.
>
> Focus for this lecture:
> - **6 Functional Testing types**
> - **5 Non-Functional Testing types** (with **6 Performance sub-types**)
> - The **Star Truck Café example** (used throughout the slides — likely exam scenario)
> - Heavy on MCQs and definition-based essay questions.

---

# SLIDE 1 — Title Slide
"Lecture 3 – Functional and Non-Functional Testing." Skip.

---

# SLIDE 2 — Software Testing (Overview Diagram)

## 1. Plain English Explanation
A simple flowchart of how testing works:
- **Test Inputs** → Testing Software → **Test Outputs** → Acceptability Check → either **Pass** ✅ or **Fail** ❌.

## 2. Theory (From slide)
```
Test Inputs → [Testing Software] → Test Outputs → Acceptability Check
                                                         ├── Test Case Pass ✅
                                                         └── Test Case Fail ❌
```

## 3. PRO TIPS
- **A4 Sheet:** Draw this 4-box flow once — useful as a visual answer in essays.
- **Common exam question:** "What is the basic flow of software testing?" → use this diagram in your answer.

## Quick Recap
- Inputs → Software → Outputs → Check → Pass/Fail.

---

# SLIDE 3 — Software Testing Types (Main Branches)

## 1. Plain English Explanation
At the highest level, software testing splits into **2 branches**.

## 2. Theory (Exactly as in slides)
```
              [Software Testing]
                /            \
   [Functional Testing]   [Non-Functional Testing]
```

## 3. Comparison Table — The Two Branches

| Branch | Tests | Sample Question |
|--------|-------|------------------|
| **Functional Testing** | What the system does (features) | "Does the login button work?" |
| **Non-Functional Testing** | How the system performs (quality attributes) | "How fast does login respond under 1,000 users?" |

## 4. PRO TIPS
- **Memory trick:**
  - **Functional** = **F**unctions / **F**eatures (WHAT).
  - **Non-Functional** = qualities / characteristics (HOW WELL).
- **A4 Sheet:** Two boxes side-by-side; under each, the sub-types.

## Quick Recap
- 2 high-level testing categories.
- Functional = WHAT. Non-Functional = HOW WELL.

---

# SLIDE 4 — Functional Testing (Definition)

## 1. Plain English Explanation
Functional testing checks whether each **function** of the system does what it's supposed to do — input goes in, output comes out, and the actual output matches the expected output.

## 2. Theory (Exactly as in slides)
- A type of testing that verifies that **each function of the software application operates in conformance with the requirement specification**.
- Each functionality of the system is tested by providing **appropriate input, verifying the output, and comparing the actual results with the expected results**.

## 3. PRO TIPS
- Memorize this definition **verbatim** — high-likelihood essay/MCQ target.
- **A4 Sheet:** *Functional testing → verifies each function conforms to requirement spec → input/expected output/actual output comparison.*

## Quick Recap
- Functional = "Does this feature work correctly?"
- Test by comparing **actual** vs **expected** results.

---

# SLIDE 5 — Types of Functional Testing

## 1. Plain English Explanation
**6 sub-types of Functional Testing** to memorize.

## 2. Theory (Exactly as in slides)
1. Unit Testing
2. Smoke Testing
3. Regression Testing
4. Sanity Testing
5. System Testing
6. User Acceptance Testing

## 3. Comparison Table — The 6 Functional Sub-Types

| # | Type | Tested by | When | Scope |
|---|------|-----------|------|-------|
| 1 | **Unit Testing** | Developer | During coding | Individual function/method/class |
| 2 | **Smoke Testing** | QA team | After new build | Core/critical functionality |
| 3 | **Regression Testing** | QA team (often automated) | After any change | Re-runs old scripted tests |
| 4 | **Sanity Testing** | QA team (non-scripted) | After minor change | Targeted small area |
| 5 | **System Testing** | QA team | Before release | Entire integrated system |
| 6 | **User Acceptance Testing (UAT)** | Customer/end user | Before sign-off | End-user perspective |

## 4. PRO TIPS
- **Memory trick — acronym "U-S-R-S-S-U"** → Unit, Smoke, Regression, Sanity, System, UAT.
- **A4 Sheet:** 6 sub-types listed vertically with one-line definitions each.

## Quick Recap
- 6 sub-types → memorize.
- Order roughly from smallest scope (Unit) to largest (UAT).

---

# SLIDE 6 — Unit Testing (Definition)

## 1. Plain English Explanation
Test **the smallest pieces of code** in isolation — single methods, functions, or classes — to make sure each works correctly **on its own**.

## 2. Theory (Exactly as in slides)
- A process of testing the **individual subprograms, subroutines, classes, or procedures** in a program.
- Unit testing is a way of **managing the combined elements of testing**.
- Unit testing **eases the task of debugging**.

## 3. Real-World Application
A developer writes a method `calculateOvertime()` and immediately writes a test that calls it with 5 hours → expects $50. If the test fails, the bug is contained to one method — easy to debug.

## 4. PRO TIPS
- **Common exam keywords:** "individual," "subroutines/classes/procedures," "eases debugging."
- **Memory trick:** Unit = **U**ndivided **N**ode **I**nspection **T**est.
- **A4 Sheet:** *Unit = smallest unit (method/class) → done by dev → eases debugging.*

## Quick Recap
- Smallest testing unit.
- Done by developer.
- Easier to debug small failures.

---

# SLIDE 7 — Unit Testing Diagram

The slide shows: **Unit Specification + Unit Source Code → Unit Testing**.

In other words, you take the **specification** (what the unit should do) plus the **code** (what was written) and verify the code meets the spec.

---

# SLIDES 8 & 9 — Smoke Testing

## 1. Plain English Explanation
After a new build is delivered, run a **quick set of tests on the core features** — if the basics fail ("the build catches fire / smokes"), there's no point doing deeper testing.

## 2. Theory (Exactly as in slides)
- Testing the **core functionality** of a program.
- The term smoke test in technology is broadly used to **test product features in a limited time**.
- Smoke testing is a **subset of all defined test cases** that cover the main functionality.

**Examples of capabilities tested:**
- Access to the application
- Logging in with a set of users
- Main modules of a particular application

## 3. PRO TIPS
- **Origin of name:** From hardware — if you turn on a device and smoke appears, it's broken. Same idea for software.
- **A4 Sheet:** *Smoke = quick core-functionality check on new build → subset of full tests.*

## Quick Recap
- Quick test of core features after build.
- Subset of total test cases.
- "If smoke comes out, stop testing further."

---

# SLIDE 10 — Regression Testing (Definition)

## 1. Plain English Explanation
After making any change to existing software, **re-run the old tests** to make sure the change didn't break anything that used to work.

## 2. Theory (Exactly as in slides)
- Regression testing is testing an existing software application to ensure that a **change or addition has not caused any errors** with existing functionality.
- Regression testing **re-runs the testing scenarios that were originally scripted**.
- Regression testing **typically requires an automated testing tool**.

## 3. Real-World Application
After adding a "dark mode" toggle to Facebook, the QA team runs the entire regression test suite to confirm posting, commenting, friend requests, etc. all still work.

## 4. PRO TIPS
- **Common exam keywords:** "existing," "change or addition," "re-runs," "automated tool."
- **A4 Sheet:** *Regression = re-run old tests after change → catches breakages → usually automated.*

## Quick Recap
- Re-runs old test scripts.
- Triggered by ANY change to code.
- Typically automated.

---

# SLIDE 11 — Selecting Regression Tests

## 1. Plain English Explanation
You usually can't run **all** regression tests every time (too many). So you pick smart ones.

## 2. Theory (Exactly as in slides)
- Requires knowledge about the system and how it is affected by the existing functionalities.
- Select tests based on the **area of frequent defects**.
- Tests include the areas which have undergone **code changes several times**.
- Tests are selected based on the **criticality of the features**.

## 3. Comparison Table — How to Pick Regression Tests

| Criterion | Why |
|-----------|-----|
| Frequent defect areas | Bugs cluster there (recall **Defect Clustering** from L1) |
| Areas with multiple code changes | More change = more risk |
| Critical features | High user/business impact |

## 4. PRO TIPS
- **A4 Sheet:** *Select regression tests: frequent-defect areas + frequently-changed code + critical features.*

---

# SLIDE 12 — Sanity Testing

## 1. Plain English Explanation
A **quick, narrow check** after a **minor change** — "does the planned change actually work?" It's not exhaustive, just a sanity check.

## 2. Theory (Exactly as in slides)
- Performed **after receiving a software build, with minor changes** in code or functionality.
- Checks whether the **planned functionality is working as expected**.
- Sanity testing is **typically non-scripted**.
- Sanity testing is a **subset of regression testing**.

## 3. Comparison Table — Smoke vs Sanity (Very High Exam Frequency!)

| Feature | Smoke Testing | Sanity Testing |
|---------|---------------|-----------------|
| Trigger | After **new build** | After **minor change** |
| Scope | Core features (broad, shallow) | Specific changed area (narrow, focused) |
| Subset of | Full test suite | **Regression testing** |
| Scripted? | Usually scripted | **Non-scripted** |
| Goal | "Can we even start testing?" | "Did this small change work?" |

## 4. PRO TIPS
- **Memory trick:**
  - Smoke = "Is the build alive?"
  - Sanity = "Is the developer sane? Did the fix work?"
- **Highest-likelihood MCQ:** Smoke vs Sanity differences.
- **A4 Sheet:** Smoke vs Sanity 5-row table above.

## Quick Recap
- Smoke = broad, after build. Sanity = narrow, after minor change.
- Sanity is a subset of Regression. Both ≠ each other.

---

# SLIDE 13 — System Testing

## 1. Plain English Explanation
Test the **whole system end-to-end** against the original objectives. Not individual pieces — the integrated product.

## 2. Theory (Exactly as in slides)
- System testing **compares the entire system or program to its original objectives**.
- **Attempting to demonstrate how the entire system fails** to meet its objectives.
- **Requires a set of measurable objectives** for the product.

## 3. PRO TIPS
- **Key word:** "**entire** system." (Not modules — the whole thing.)
- "Attempting to demonstrate how the system **fails**" — testers actively try to break it.
- **A4 Sheet:** *System Testing = entire system vs original objectives → tries to expose failures.*

## Quick Recap
- Full integrated product, full spec.
- Goal: expose failure to meet objectives.

---

# SLIDE 14 — User Acceptance Testing (UAT)

## 1. Plain English Explanation
Final stage — the **actual customer/end user** tests the system to confirm it does what they need.

## 2. Theory (Exactly as in slides)
- Process of comparing the program to its **initial requirements and the current needs of the end users**.
- Usually performed by the **customer or end user**.
- Developer will conduct user tests **during the development cycle** prior to delivering the finished product.

## 3. PRO TIPS
- **Key distinguishing feature:** UAT is done by the **customer**, not the dev team.
- **A4 Sheet:** *UAT → done by customer → against initial reqs + current end-user needs.*

## Quick Recap
- Done by **customer / end user**.
- Final validation before sign-off.
- Relates to "Validation" concept from Lecture 1.

---

# SLIDES 15 to 24 — The Star Truck Café Scenario (Worked Example)

The slides walk through a **complete project** to demonstrate where each functional test type fits.

## Story Summary
- **Steve** owns Star Truck Café.
- **John** works at **TechSolutions**.
- Steve hires John to build a **Salary Management System**.

## Specification (Slides 17–18)
The system has **4 sub-systems**:
1. **Attendance Management** (fingerprint in/out times, monthly hours report) → **Oliver**
2. **Overtime Calculation** (work after 6pm → overtime pay) → **Andrew**
3. **Salary Calculation** (monthly salary using attendance + overtime) → **Lilia**
4. **User Management** (owner sees all; workers see own data) → **Jessica**

## Where Each Test Fits

| Test Type | Applied to | In the Story |
|-----------|-----------|---------------|
| **Unit Testing** | Each sub-system individually | Slides 21–24 |
| **Smoke Testing** | Core: user management + monthly salary generation | Slide 25 |
| **System Testing** | Entire integrated Salary Management System vs spec | Slide 26 |

## 3. PRO TIPS
- This **scenario is exam gold** — be ready to identify which test fits which situation.
- **A4 Sheet:** Map the 4 sub-systems → 4 unit tests; then smoke; then system; then UAT.

---

# SLIDES 27 & 28 — Change Request + Regression Testing

## Scenario
**Change request:** *"If employee works after 9pm, double the overtime rate for hours after 9pm."*

This is a **major change** → triggers full **regression testing** across all 4 sub-systems:
- Attendance management
- Overtime calculation
- User management
- Salary calculation

## PRO TIPS
- After a **significant change** → do **Regression Testing** (full re-run).
- This pairs with Slide 11 (select regression tests by frequency/change/criticality).

---

# SLIDES 29 & 30 — Minor Change Request + Sanity Testing

## Scenario
**Minor change:** *"Change overtime trigger from 9pm to 10pm."*

This is a **minor tweak** → triggers **Sanity Testing** only on:
- The overtime calculation with double rate when the overtime is **after 10pm**.

## PRO TIPS — Regression vs Sanity Trigger Rule
- **Major change** → Regression (full re-run).
- **Minor change** → Sanity (focused check).

---

# SLIDE 31 — User Acceptance Testing (Final Step)

## Scenario
Steve (the customer) and his team verify the final Salary Management System.

This concludes the Functional Testing flow in the story:
**Unit → Smoke → System → (change) → Regression → (minor change) → Sanity → UAT.**

## PRO TIPS
- **Memory trick — the order in the story:** "**U-Sm-Sy-R-Sa-U**" → Unit → Smoke → System → Regression → Sanity → UAT.

---

# 🎯 EXTRA FUNCTIONAL TESTING EXAMPLES (Beyond Slides)

### Example A — Simple
**Spec:** A team builds a calculator app.
- **Unit Testing:** Test `add()`, `subtract()`, `multiply()`, `divide()` individually.
- **Smoke Testing:** Open the app, can the user tap a number and see it appear?
- **System Testing:** Full integrated calculator vs the spec.
- **UAT:** Customer (the school) tests the calculator with real students.

### Example B — Complex
**Spec:** A team builds an e-banking app with login, transfer, statement, and notifications.
- **Unit Testing:** Login module, Transfer module, Statement module, Notifications module — each tested in isolation.
- **Smoke Testing:** Can the app open? Can a user log in?
- **Regression Testing:** After adding QR-code payments → re-run all old tests (login, transfer, statement, notifications) to ensure no breakage.
- **Sanity Testing:** After renaming the "Send" button to "Transfer" → quick check that the button still triggers a transfer.
- **System Testing:** Full e-banking flow tested end-to-end.
- **UAT:** Real bank customers test on production-like environment.

---

# 📊 MASTER COMPARISON — FUNCTIONAL TESTING TYPES

| Type | When | Scope | Who | Scripted? | Key Phrase |
|------|------|-------|-----|-----------|-------------|
| Unit | During coding | Single method/class | Dev | Yes | "Eases debugging" |
| Smoke | After new build | Core features | QA | Usually yes | "Subset of all test cases" |
| Regression | After any change | Re-run old tests | QA | Usually automated | "Change has not caused errors" |
| Sanity | After minor change | Specific area | QA | **Non-scripted** | "Subset of regression" |
| System | Before release | Entire system | QA | Yes | "Compared to original objectives" |
| UAT | Pre sign-off | End-user perspective | Customer | Sometimes | "Initial reqs + current end-user needs" |

---

# SLIDE 32 — Non-Functional Testing (Definition)

## 1. Plain English Explanation
Non-Functional Testing checks **the qualities** of the system — not what it does, but **how well it does it** (performance, usability, security, etc.).

## 2. Theory (Exactly as in slides)
- A type of testing to check **non-functional aspects** of a software application.
- Examples of non-functional aspects:
  - Performance
  - Usability
  - Reliability
- **Explicitly designed to test the readiness of a system as per non-functional parameters which are never addressed by functional testing.**

## 3. PRO TIPS
- **Common exam keyword:** "Quality attributes" / "non-functional parameters."
- Reliability, Performance, Usability = the "ities" of software.
- **A4 Sheet:** *Non-Functional = quality attributes → never addressed by functional testing.*

## Quick Recap
- Non-Functional = qualities (Performance, Usability, Reliability, Security, etc.).
- Complementary to (not replacing) Functional Testing.

---

# SLIDE 33 — Performance Testing (Definition)

## 1. Plain English Explanation
Test whether the system runs **fast enough and well enough** under the loads it will face in real life.

## 2. Theory (Exactly as in slides)
- Designed to test whether the program **satisfies its performance objectives**.
- Measure the performance of each component to identify which components cause the system to perform poorly.
- Performance testing involves **quantitative tests done in a laboratory environment**.
- Can **compare the performance of two systems**.

## 3. PRO TIPS
- Key word: "**quantitative**" → numbers/metrics, not opinions.
- **A4 Sheet:** *Performance Testing → measures speed/quality vs objectives → quantitative → lab environment.*

---

# SLIDE 34 — Types of Performance Testing

## 1. Plain English Explanation
**6 sub-types of Performance Testing** to memorize. They appear as MCQ targets very often.

## 2. Theory (Exactly as in slides)
```
                  [Performance Testing]
                          │
   ┌──────┬──────┬──────┬──────┬──────┬──────┐
  Load   Stress  Spike  Scal-  Volume Endurance
                        ability
```

## 3. Comparison Table — 6 Performance Sub-Types

| # | Type | What it does | Example |
|---|------|---------------|---------|
| 1 | **Load Testing** | Constantly increasing load until threshold | 100 → 200 → 500 users gradually |
| 2 | **Stress Testing** | Beyond normal/peak load — system breaks | Push to 10,000 users when designed for 5,000 |
| 3 | **Spike Testing** | Sudden huge user surge | 100 → 100,000 users in seconds (Black Friday) |
| 4 | **Scalability Testing** | Capability to scale up | Can the system handle 2× growth next year? |
| 5 | **Volume Testing** | Large amount of **data** | Database with 10 million records |
| 6 | **Endurance Testing** | Expected load over **long time** | Run system at normal load for 72 hours |

## 4. PRO TIPS
- **Memory trick — "L-S-S-S-V-E"** → **L**oad, **S**tress, **S**pike, **S**calability, **V**olume, **E**ndurance.
- **Highest MCQ overlap:** Load vs Stress vs Spike — all three look similar but are different.
- **A4 Sheet:** This 6-row table verbatim.

## Quick Recap
- 6 Performance sub-types.
- Load = gradual increase. Stress = beyond peak. Spike = sudden burst.
- Volume = data. Scalability = future growth. Endurance = long duration.

---

# SLIDES 35 & 36 — Load Testing

## 1. Plain English Explanation
Gradually increase the load on the system until it hits a "breaking point" — measure how it behaves at each level.

## 2. Theory (Exactly as in slides)
- Test a system with **constantly increasing load** until "the time to load" reaches its threshold value.
- Use to **distinguish performance between two different systems**.
- Monitor the **response time and staying power** of an application under heavy load.

**Examples of Load Testing:**
- Testing a printer by sending a large job.
- Editing a very large document in a word processor.
- Continuously reading and writing data into hard disk.
- Running multiple applications simultaneously on the server.
- Testing a mail server by accessing thousands of mailboxes.

## 3. PRO TIPS
- **A4 Sheet:** *Load Testing → constant increase up to threshold → monitor response time + staying power.*

---

# SLIDE 37 — Stress Testing

## 1. Plain English Explanation
**Push the system beyond its limits** to see how it fails and how it recovers.

## 2. Theory (Exactly as in slides)
- Validate an application's behavior when it is **pushed beyond normal or peak load** conditions.
- Checks the stability of software when the **hardware resources are insufficient**.
- Determine failures of a system and identify how the system recovers from failures. This quality is known as **recoverability**.

## 3. PRO TIPS
- Stress = "beyond normal/peak" — keyword that distinguishes from Load.
- **Recoverability** = MCQ target term.
- **A4 Sheet:** *Stress Testing → beyond peak → check stability + recoverability.*

---

# SLIDE 38 — Spike Testing

## 1. Plain English Explanation
**Sudden, sharp spike** in users — like Black Friday traffic. Test if the system survives the shock.

## 2. Theory (Exactly as in slides)
- Performed by **suddenly increasing the number of users by a very large amount**.
- The main aim is to determine whether the system will be able to **sustain the sudden heavy workload**.

## 3. Comparison Table — Load vs Stress vs Spike (Big MCQ Trio)

| Feature | Load | Stress | Spike |
|---------|------|--------|-------|
| Load pattern | **Gradual** increase | Pushed **beyond peak** | **Sudden burst** |
| Goal | Find threshold | Find failure point + recovery | Survive sudden surge |
| Real example | Daily peak hours | Black-out simulation | Concert ticket release |

## 4. PRO TIPS
- **Memory trick:**
  - **Load** = like adding boxes one at a time.
  - **Stress** = like piling boxes until shelf breaks.
  - **Spike** = like dropping all boxes at once.

---

# SLIDE 39 — Endurance Testing

## 1. Plain English Explanation
Run the system at a **normal expected load for a long time**. Watch for slowdowns, memory leaks, random crashes.

## 2. Theory (Exactly as in slides)
- Testing a system with an **expected amount of load over a long period of time**.
- Test cases executed to check the behavior of a system.
- Consider factors such as **memory leaks**, **system fails**, or **random behavior**.

## 3. PRO TIPS
- **Keywords:** "long period," "memory leaks," "expected load."
- **A4 Sheet:** *Endurance = normal load × long duration → catches memory leaks + random fails.*

---

# SLIDE 40 — Scalability Testing

## 1. Plain English Explanation
Can the system **grow** to handle more users/data/transactions in the future without breaking?

## 2. Theory (Exactly as in slides)
- Testing to determine the **capability of scaling up** in terms of any non-functional requirement.
- Determines the **peak** of a system when it has reached a level which **prevents from more scaling**.

## 3. PRO TIPS
- **A4 Sheet:** *Scalability = ability to scale up → find max scaling peak.*

---

# SLIDE 41 — Volume Testing

## 1. Plain English Explanation
Test the system with **huge amounts of data** in its database — not many users, but lots of stored data.

## 2. Theory (Exactly as in slides)
- Testing a software application with a **large amount of data**.
- Monitor the performance of the application under varying **database volumes**.

## 3. PRO TIPS
- **Volume = DATA volume**, NOT user volume. (Common confusion vs Load.)
- **A4 Sheet:** *Volume Testing = huge DATA in DB → not users.*

---

# SLIDE 42 — Uses of Performance Testing

## 2. Theory (Exactly as in slides)
- Improve user experience.
- Gather metrics useful for tuning the system.
- Identify bottlenecks (e.g., database configuration).
- Determine if a new release is ready for production.
- Provide reporting to business stakeholders regarding performance against expectations.

## PRO TIPS
- **5 uses** — memorize for an easy 5-mark essay question.
- **A4 Sheet:** *Performance Testing Uses: UX↑, metrics, bottlenecks, release readiness, stakeholder reports.*

---

# SLIDE 43 — Top Performance Testing Tools

## 2. Theory (Exactly as in slides)
- LoadRunner
- Apache JMeter
- NeoLoad
- Rational Performance Tester
- Loadster
- QEngine (ManageEngine)
- Testing Anywhere
- Loadstorm

## PRO TIPS
- **Memorize at least 3:** **LoadRunner, Apache JMeter, NeoLoad** are the most famous.
- Easy MCQ filler: "Which of the following is a performance testing tool?" → JMeter.

---

# SLIDE 44 — Compatibility Testing (Definition)

## 1. Plain English Explanation
Check whether the software works correctly across **different operating systems, devices, browsers, and platforms**.

## 2. Theory (Exactly as in slides)
- Test an application to ensure that it is **compatible across operating systems, hardware platforms, web browsers, etc.**
- Validation for compatibility requirements set at the **planning stage**.
- Validates that the application **runs properly in versions**.

## 3. PRO TIPS
- **A4 Sheet:** *Compatibility = works on different OS / HW / browsers / versions.*

---

# SLIDE 45 — Types of Compatibility Testing

## 1. Plain English Explanation
**2 sub-types** depending on whether you're testing against **older** or **newer** versions.

## 2. Theory (Exactly as in slides)
- **Backward compatibility Testing** — Verify behavior with **older** versions.
- **Forward compatibility Testing** — Verify behavior with **newer (upcoming)** versions.

## 3. Comparison Table

| Type | Tests with | Example |
|------|-------------|---------|
| **Backward Compatibility** | Older versions | New Word app must still open .doc files from Word 97 |
| **Forward Compatibility** | Newer versions | Today's app must run smoothly on iOS 26 (future) |

## 4. PRO TIPS
- **Memory trick:** "**Back** = old. **Forward** = new."
- **A4 Sheet:** *Compatibility = Backward (old) + Forward (new).*

---

# SLIDE 46 — Security Testing

## 1. Plain English Explanation
Check whether the system is **secure** against known attacks and meets security requirements.

## 2. Theory (Exactly as in slides)
- Security testing is the process of testing an application to check whether it is **according to the specific security objectives**.
- Test cases can be derived by **studying known security problems in similar systems**.
- **Web-based applications often need a higher level of security testing** than most applications.

## 3. PRO TIPS
- **A4 Sheet:** *Security Testing → vs security objectives → web apps need more.*

---

# SLIDE 47 — Usability Testing

## 1. Plain English Explanation
Test whether real users find the system **easy to use** — interface, flow, controls.

## 2. Theory (Exactly as in slides)
- Test the **user-friendliness** of an application and identify usability defects.
- Testing is performed by using a **small set of target end-users**.
- Mainly focuses on:
  - **User's ease to use** the application,
  - **Flexibility in handling controls**,
  - **Ability of the system to meet its objectives**.

## 3. PRO TIPS
- Usability ≠ UAT. **Usability** checks user-friendliness; **UAT** checks if it meets the customer's full requirements.
- **A4 Sheet:** *Usability = ease of use + control flexibility + meets objectives → small target user set.*

---

# SLIDE 48 — Localization Testing

## 1. Plain English Explanation
Test whether the software adapts to **different countries/cultures/languages** (translations, currencies, date formats, religious considerations).

## 2. Theory (Exactly as in slides)
- Test whether the software behaves according to the **local culture or settings**.
- Test whether the application has appropriate **linguistic and cultural aspects for a particular locality**.
- Localization testing of a **globalized application** is the process of identifying whether all components are **designed according to the local culture of target countries and regions**.

## 3. PRO TIPS
- **Common example:** Currency $ vs £ vs ₹; Date 12/05/2026 (US) vs 05/12/2026 (UK).
- **A4 Sheet:** *Localization = adapt to local culture/language/region.*

---

# SLIDE 49 — Non-Functional Testing Summary Diagram

## Summary of 5 main Non-Functional types:

```
                 [Non-Functional Testing]
        ┌──────┬──────┬──────┬──────┬──────┐
      Performance Compatibility Security Usability Localization
```

## PRO TIPS
- **Memory trick — "P-C-S-U-L"** → **P**erformance, **C**ompatibility, **S**ecurity, **U**sability, **L**ocalization.

---

# SLIDE 50 — Activity (Mind Map)
*Activity slide for students to create their own mind map. No theory content.*

---

# 📊 MASTER COMPARISON — NON-FUNCTIONAL TESTING TYPES

| Type | What it tests | Sub-types | Key Tool/Example |
|------|---------------|-----------|-------------------|
| **Performance** | Speed, response, scaling under load | Load, Stress, Spike, Scalability, Volume, Endurance | JMeter, LoadRunner |
| **Compatibility** | Works across OS, browser, version | Backward, Forward | Manual OS/browser checks |
| **Security** | Resists attacks, meets security objectives | (No sub-types listed in slides) | Vulnerability scans |
| **Usability** | User-friendliness | (No sub-types listed in slides) | Small target user group |
| **Localization** | Local culture/language compliance | (No sub-types listed in slides) | Multi-region UX testing |

---

# 📝 MCQ PRACTICE — LECTURE 3

---

### Q1. Unit testing is typically performed by:
A) Customer
B) **Developer** ✅
C) End user
D) Stakeholder

**Answer: B (Slide 6 — eases debugging, done by developer)**

---

### Q2. Which testing is a SUBSET of regression testing?
A) Unit Testing
B) System Testing
C) **Sanity Testing** ✅
D) Smoke Testing

**Answer: C (Slide 12 — "Sanity testing is a subset of regression testing")**

---

### Q3. Spike Testing is performed by:
A) Gradually increasing the load
B) **Suddenly increasing the number of users by a very large amount** ✅
C) Running the system for a long time at expected load
D) Testing with a huge database

**Answer: B (Slide 38)**

---

### Q4. The key difference between Smoke and Sanity testing is:
A) They are the same
B) **Smoke = after new build (broad); Sanity = after minor change (focused)** ✅
C) Smoke is automated; Sanity is manual only
D) Smoke is non-functional; Sanity is functional

**Answer: B (Slides 8, 12)**

---

### Q5. Which is NOT a type of Performance Testing?
A) Load
B) Stress
C) **Localization** ✅
D) Endurance

**Answer: C — Localization is a separate Non-Functional category (Slide 34)**

---

### Q6. Verifying that a new app version still works correctly with files from an older version is called:
A) Forward Compatibility Testing
B) **Backward Compatibility Testing** ✅
C) Regression Testing
D) Smoke Testing

**Answer: B (Slide 45)**

---

### Q7. Volume Testing focuses on:
A) Sudden user spikes
B) **Large amounts of data in the database** ✅
C) Long-duration testing
D) Compatibility across browsers

**Answer: B (Slide 41)**

---

### Q8. "Recoverability" is most associated with which testing type?
A) Load Testing
B) Spike Testing
C) **Stress Testing** ✅
D) Endurance Testing

**Answer: C (Slide 37 — "this quality is known as recoverability")**

---

### Q9. Which of the following is performed by the customer or end user?
A) Unit Testing
B) Smoke Testing
C) System Testing
D) **User Acceptance Testing** ✅

**Answer: D (Slide 14)**

---

### Q10. Apache JMeter is a tool primarily used for:
A) Usability Testing
B) **Performance Testing** ✅
C) Localization Testing
D) Unit Testing

**Answer: B (Slide 43)**

---

# 📌 LECTURE 3 — A4 REFERENCE SHEET MINI-SECTION

```
FUNCTIONAL TESTING (WHAT the system does)
  Definition: verifies each function vs requirement spec
              (compare actual vs expected output)

  6 SUB-TYPES (U-S-R-S-S-U):
    1. Unit         → smallest unit (method/class), dev, eases debugging
    2. Smoke        → core features after new build, subset of all tests
    3. Regression   → re-run old tests after change, usually automated
    4. Sanity       → focused check after MINOR change, non-scripted, subset of regression
    5. System       → entire integrated system vs original objectives
    6. UAT          → done by customer/end user vs initial reqs

  Trigger Rule:
    Major change → Regression (full)
    Minor change → Sanity (focused)

NON-FUNCTIONAL TESTING (HOW WELL the system does)
  Definition: quality attributes never addressed by functional testing

  5 MAIN TYPES (P-C-S-U-L):
    1. Performance Testing
    2. Compatibility Testing
    3. Security Testing
    4. Usability Testing
    5. Localization Testing

  PERFORMANCE SUB-TYPES (L-S-S-S-V-E):
    Load        → gradual increase to threshold
    Stress      → beyond peak load (recoverability)
    Spike       → sudden user surge
    Scalability → capability to scale up
    Volume      → large database / data
    Endurance   → expected load × long time (memory leaks)

  COMPATIBILITY SUB-TYPES:
    Backward    → with older versions
    Forward     → with newer versions

  PERFORMANCE TOOLS (memorize 3):
    LoadRunner, Apache JMeter, NeoLoad

  STAR TRUCK CAFÉ SCENARIO:
    4 sub-systems → Unit Testing each
    Then → Smoke → System → UAT
    Major change (9pm overtime) → Regression
    Minor change (9pm → 10pm)  → Sanity
```

---

# ✅ LECTURE 3 — DONE

This is a **volume lecture** — many definitions to memorize. The exam will likely test you on:
1. Differences between Smoke and Sanity (very common).
2. Differences between Load, Stress, and Spike (very common).
3. Which testing types apply at which point in a real project (use the Star Truck Café story).
4. Compatibility: Backward vs Forward.

Reply **"done"** to continue to **Lecture 4 — Code Coverage Analysis** (then Cyclomatic Complexity).
