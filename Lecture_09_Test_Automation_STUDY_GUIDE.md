# LECTURE 9 — TEST AUTOMATION
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **⚠️ IMPORTANT NOTE FOR THIS LECTURE**
> Lecture 9 is a **conceptual + tool-heavy** lecture — no math, no calculations. It is the second-biggest topic for L8–L11 essay questions.
>
> Focus for this lecture:
> - When to / NOT to automate (**6 + 6 cases**)
> - Manual vs Automated Testing comparison (multi-row table)
> - Test Automation Lifecycle (**6 stages**)
> - Test Automation Pyramid (**3 levels**)
> - **5 types of Test Automation Frameworks** (Linear, Modular, Data-Driven, Keyword-Driven, Hybrid, BDD)
> - Tools (Selenium, Appium, JMeter, etc.)
> - Flaky tests, CI/CD, Myths
>
> **Top exam-likely essay:** "Compare Manual vs Automated Testing" + "Explain Test Automation Frameworks" + "Test Automation Lifecycle."

---

# SLIDE 1 — Title Slide
"Test Automation" — date and lecturer. Skip.

---

# SLIDE 2 — Test Automation Overview

## 1. Plain English Explanation
This lecture has **7 topics**:
1. Introduction to Test Automation
2. Manual vs Automated Testing
3. Principles of Test Automation
4. Test Automation Lifecycle
5. Test Automation Frameworks
6. Challenges & Myths in Test Automation
7. Assignment 2

## PRO TIPS
- Roadmap of the lecture. Memorize the 7 topics — exam essays often follow this order.

---

# SLIDE 3 — What is Automation?

## 1. Plain English Explanation
General "automation" means making something **operate on its own**, without needing a human.

## 2. Theory (Exactly as in slides)
> Making an apparatus, a process, or a system operate automatically.

## PRO TIPS
- **A4 Sheet:** *Automation = making a system operate automatically.*

---

# SLIDE 4 — What is Test Automation?

## 1. Plain English Explanation
Test automation is using **software tools** to run test cases automatically — without a human clicking through every button.

## 2. Theory (Exactly as in slides)
> Test automation is the use of **software tools** to automatically **run and validate test cases**, enhancing testing efficiency…

## PRO TIPS
- **HIGH-FREQUENCY EXAM DEFINITION** — memorize verbatim.
- **A4 Sheet:** *Test Automation = software tools auto-run & validate test cases → enhances efficiency.*

## Quick Recap
- Test Automation = use software tools to auto-run + validate tests.

---

# SLIDE 5 — What/When to Automate? (6 Cases ✅)

## 1. Plain English Explanation
**6 testing scenarios** that are good candidates for automation. Each has a short reason + example.

## 2. Theory (Exactly as in slides)

| # | Scenario | Reason / Example |
|---|----------|------------------|
| 1 | **Regression Testing** | Run frequently to ensure new code hasn't broken existing functionality (e-com app) |
| 2 | **Smoke Testing / Sanity Checks** | Quick checks to see if basic functionalities work before deeper testing |
| 3 | **High Volume / Repetitive Tests** | Saves time and reduces human error (load testing) |
| 4 | **Data-Driven Testing** | Same test logic with multiple input data sets (500 input combinations) |
| 5 | **Cross-Browser / Cross-Device Testing** | Tools can quickly test on different browsers / devices |
| 6 | **Stable Features** | Automate tests for features that don't change often (Login/Logout) |

## 3. PRO TIPS
- **Memory trick — "R-S-H-D-C-S"** → Regression, Smoke, High-volume, Data-driven, Cross-platform, Stable.
- **HIGH ESSAY PROBABILITY:** "When should you automate testing? Give 6 cases with examples."

## Quick Recap
- 6 scenarios to automate. Memorize all.

---

# SLIDE 6 — What/When NOT to Automate? (6 Cases ❌)

## 1. Plain English Explanation
**6 scenarios** where automation is a bad idea. Each has a reason + example.

## 2. Theory (Exactly as in slides)

| # | Scenario | Reason / Example |
|---|----------|------------------|
| 1 | **Exploratory Testing** | Requires human intuition, creativity, observation (to find visual bugs) |
| 2 | **Short-Lived Features** | Not worth it for features that will be removed soon (a holiday sale) |
| 3 | **Unstable or Frequently Changing UI** | Tests will break often (Promotional page) |
| 4 | **Usability Testing** | Needs human feedback on look, feel, ease of use (New color scheme) |
| 5 | **Tests That Run Only Once** | Effort to automate outweighs the benefit (One-time data migration) |
| 6 | **Complex Logics Involved** | Some things are too delicate to automate (Image comparison, CAPTCHA) |

## 3. PRO TIPS
- **Memory trick — "E-S-U-U-O-C"** → Exploratory, Short-lived, Unstable UI, Usability, Once-only, Complex.
- **Common MCQ:** "Which is NOT a good candidate for automation?" → answer = usually Exploratory or Usability testing.

## Quick Recap
- 6 scenarios NOT to automate. Memorize all.

---

# SLIDE 7 — Benefits of Test Automation

## 1. Plain English Explanation
Two perspectives: **app-wise benefits** (quality) + **cost-wise benefits** (money/time/ROI).

## 2. Theory (Exactly as in slides)

**Application-wise:**
- Improved Quality
- Improved Accuracy
- Enhanced Test Coverage
- Early Bug Detection
- Reusable Test Scripts

**Cost-wise:**
- Save Cost
- Save Time
- Increases ROI

## 3. PRO TIPS
- **5 app benefits + 3 cost benefits = 8 total benefits** to memorize.
- **A4 Sheet:** *Benefits: Quality↑, Accuracy↑, Coverage↑, Early bugs, Reusable scripts | Save cost, Save time, ROI↑*

## Quick Recap
- 8 benefits — app-wise (5) + cost-wise (3).

---

# SLIDES 8-10 — Manual vs Automated Testing (CRITICAL EXAM TABLE)

## 1. Plain English Explanation
Manual testing = human tester clicks through. Automated testing = software framework runs tests automatically. Each has trade-offs.

## 2. Comparison Table — Manual vs Automated (7 dimensions from slides)

| # | Key Difference | Manual Testing | Automated Testing |
|---|----------------|-----------------|---------------------|
| 1 | **Execution Time** | More time, sequential, higher resource usage | Faster execution, less resource consumption |
| 2 | **Initial Setup** | Less effort initially | More effort to create/maintain scripts and tools |
| 3 | **Reliability** | Less reliable (human error possible) | Higher reliability (consistent execution) |
| 4 | **Programming** | Non-programmable, limits complex tests | Allows complex tests to uncover hidden defects |
| 5 | **Reusability** | Often requires new test cases for each function | Test scripts can be reused across cycles |
| 6 | **Reporting** | Reporting varies (manually implemented) | Standardized, consistent reporting |
| 7 | **Flexibility** | More adaptable to changing requirements | Less flexible to unexpected changes (pre-programmed) |

## 3. PRO TIPS
- **VERY HIGH EXAM PROBABILITY:** "Compare Manual vs Automated Testing." → memorize this 7-row table.
- **Key essay phrases:**
  - "Manual is more flexible but slower."
  - "Automated is faster + reliable but requires more initial setup."
- **A4 Sheet:** Full 7-row table.

## Quick Recap
- 7 dimensions to compare Manual vs Automated.
- Manual = flexible, slow, human-prone. Automated = consistent, fast, less flexible.

---

# SLIDE 11 — Principles of Test Automation

## 1. Plain English Explanation
**6 guiding principles** every test automation effort should follow.

## 2. Theory (Exactly as in slides)
1. Tests should **improve quality**.
2. Tests should **reduce the risk of introducing failures**.
3. Testing **helps to understand the code**.
4. Tests must be **easy to write**.
5. A test suite must be **easy to run**.
6. A test suite should need **minimal maintenance**.

## 3. PRO TIPS
- **Memory trick — "Q-R-U-W-R-M"** → Quality, Risk-reduction, Understand code, Write easy, Run easy, Minimal maintenance.
- **A4 Sheet:** 6 principles in one line each.

## Quick Recap
- 6 principles → memorize all in order.

---

# SLIDE 12 — Test Automation Lifecycle (6 Stages)

## 1. Plain English Explanation
A structured 6-stage process for setting up and running test automation.

## 2. Theory (Exactly as in slides)
```
Stage 1                Stage 2               Stage 3
Deciding the          Choosing the          Plan, Design,
scope of Test     →   Right Automation  →   and Strategy
Automation            Tool

Stage 4                Stage 5               Stage 6
Set-Up Test       →   Test Script &     →   Test Analysis
Environment           Execution             and Reporting
```

## 3. Comparison Table — 6 Stages at a Glance

| # | Stage | Purpose |
|---|-------|---------|
| 1 | Deciding the scope | What/why to automate |
| 2 | Choosing the right tool | Pick the best automation tool for stack |
| 3 | Plan, Design, Strategy | High-level approach, objectives, KPIs |
| 4 | Set-Up Test Environment | AUT, tools, data, browsers, CI/CD |
| 5 | Test Script & Execution | Write & run automation scripts |
| 6 | Test Analysis & Reporting | Evaluate results, generate reports, share insights |

## 4. PRO TIPS
- **Memory trick — "S-T-P-E-W-R"** → Scope, Tool, Plan, Environment, Write/Run, Report.
- **HIGH ESSAY PROBABILITY:** "List and explain the 6 stages of the Test Automation Lifecycle."
- **A4 Sheet:** 6-stage flow chart.

## Quick Recap
- 6 ordered stages — Scope → Tool → Plan → Environment → Script/Execution → Analysis/Report.

---

# SLIDE 13 — Stage 1: Scope of Test Automation

## 1. Plain English Explanation
Decide **what** and **why** to automate before doing anything else. Consider complexity, frequency, importance.

## 2. Theory (Exactly as in slides)
- First step: figure out **what to automate**.
- Decide **what and why** to automate.
- Find suitability based on:
  - How **complex** they may be
  - How **often** they get run
  - How **vital** they may be
- Focus on automating tests for **important functions** or matters humans aren't good at.
- Work with designers, developers, QA engineers, and others.

## PRO TIPS
- **3 criteria for picking automation candidates: "C-O-V"** → Complexity, Often-run, Vital.
- **A4 Sheet:** *Scope = What + Why automate → check Complexity, Often, Vital.*

---

# SLIDE 14 — Stage 2: Choosing the Right Automation Tools

## 1. Plain English Explanation
Compare automation tools against your tech stack, team skills, budget before committing.

## 2. Theory (Exactly as in slides)
**Factors to consider:**
- **Technology Support:** Web, Desktop, Mobile
- **Scripting / Programming Requirements:** Code, No-Code, Low-Code
- **Open-source vs. Licensed**
- **Ease of Use**
- **Adoption Time**
- **Customer Support**
- **End-to-End Testing**

## PRO TIPS
- **7 factors** to memorize for tool selection.
- **A4 Sheet:** *Tool factors: Tech support, Scripting type, Open-source/Paid, Ease of use, Adoption, Support, E2E.*

---

# SLIDES 15-18 — Automation Tools (Reference Knowledge)

## 1. Plain English Explanation
A catalog of the major automation tools. **Memorize the top 5–6** — these are MCQ targets.

## 2. Tool Cheat Sheet (Most-tested tools)

| Tool | Type | Scripting Language(s) | Platform | Pricing |
|------|------|-----------------------|----------|---------|
| **Selenium** | Web automation | Java, C#, Python, Ruby, JS, Kotlin | Web (Desktop / Mobile via Appium) | Free (Open Source) |
| **Appium** | Mobile app automation | Java, Python, Ruby, JS, Kotlin | Mobile (iOS, Android), Web (Mobile) | Free (Open Source) |
| **Playwright** | Web testing (dynamic UI) | JS, TypeScript, Python, C#, Java | Web (Desktop, Mobile) | Free (Open Source) |
| **Cypress** | JS-based Web testing | JS, TypeScript | Web (Chrome-based) | Free, Paid for dashboard |
| **Cucumber** | BDD testing | Gherkin + Java/Ruby | Web, API | Free |
| **TestNG** | Java unit/test framework | Java | Unit, Functional, Integration | Free |
| **TestComplete** | Commercial UI testing | JS, Python, VBScript, DelphiScript | Web, Desktop, Mobile | Paid |
| **Postman** | API testing | (GUI / JS scripting) | API | Free / Paid |
| **JMeter** | Performance / Load testing | (GUI / Java) | Web | Free (Open Source) |
| **LoadRunner** | Performance / Load testing | (Various) | Web / Mobile | Paid |

## 3. Tool Category Summary (Slide 18)

| Category | Tools |
|----------|-------|
| **Best for Web Automation** | Playwright, Selenium, Cypress |
| **Best for Mobile Testing** | Appium, Katalon Studio |
| **Beginner Friendly** | Katalon, TestCafe, Cypress |
| **Enterprise-Grade Tools** | TestComplete, UFT One, Ranorex |
| **Open-Source Leaders** | Selenium, Appium, Robot Framework, Playwright |

## 4. Slide 19 — Tools by Category

| Category | Examples |
|----------|----------|
| **Front-end** | TestSigma, Selenium, TestComplete |
| **Performance** | JMeter, LoadRunner, Gatling |
| **Database** | dbForge Studio, SQLTest, Database Benchmark |

## 5. PRO TIPS
- **Top 5 must-memorize tools:**
  - **Selenium** = web automation
  - **Appium** = mobile automation
  - **JMeter** = performance/load (open source)
  - **LoadRunner** = performance/load (commercial)
  - **Cucumber** = BDD (Gherkin)
- **MCQ tip:** Open-source tools → Selenium, Appium, Robot Framework, Playwright, JMeter.

## Quick Recap
- 10+ tools — but only 5–6 are MCQ favorites.

---

# SLIDE 20 — Stage 3: Plan, Design and Strategy

## 1. Plain English Explanation
Build the high-level automation strategy. Set objectives, scope, tools, KPIs, costs.

## 2. Theory (Exactly as in slides)

| Activity | Description | Example |
|----------|-------------|---------|
| **Define Automation Objectives** | Clarify what you want to achieve | Speed up regression testing; improve coverage |
| **Finalize Scope** | Decide what to automate / leave out | Automate login + checkout; skip UI animations |
| **Select Tools & Frameworks** | Choose suitable tools for tech stack | Selenium + TestNG for web; Appium for mobile |
| **Assess Skills & Resources** | Understand team capability / gaps | QA team needs Python training |
| **Develop Automation Strategy** | High-level approach: CI/CD, data, reporting | Run nightly in CI, page object model, Allure reports |
| **Estimate Timeline & Cost** | Time + cost estimates | Initial setup = 2 weeks; monthly maint = 8 hrs |
| **Define KPIs & Metrics** | How to measure success | Execution time, pass rate, coverage |

## PRO TIPS
- **7 activities** — memorize for a 7-mark essay.
- **A4 Sheet:** *Plan = Objectives + Scope + Tools + Skills + Strategy + Timeline + KPIs.*

---

# SLIDE 21 — Stage 4: Setup Test Environment

## 1. Plain English Explanation
Make sure everything needed to run tests is set up: app, tools, data, browsers, CI/CD, monitoring.

## 2. Theory (Exactly as in slides)
- **Application Under Test (AUT)** — Deployed version of the app
- **Test Tools / Frameworks** — Tools for writing/executing tests
- **Test Data** — Structured data for scenarios
- **Browsers / Devices** — Devices, browsers, emulators
- **Environment Configs** — Variables, credentials, API keys, DB info
- **CI/CD Integration** — Connect with CI to run tests automatically
- **Monitoring & Logs** — Logs and dashboards for debugging

## PRO TIPS
- **7 components of a test environment** — memorize.
- **A4 Sheet:** *Env setup: AUT, Tools, Data, Browsers, Configs, CI/CD, Monitoring.*

---

# SLIDES 22-23 — Stage 5: Test Script & Execution

## 1. Plain English Explanation
Write the actual test scripts using your chosen tool, then run them.

## 2. Example (Selenium + Python from Slide 23)
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

def test_login_success():
    driver = webdriver.Chrome()
    driver.get("https://example.com/login")
    
    driver.find_element(By.ID, "username").send_keys("valid_user")
    driver.find_element(By.ID, "password").send_keys("secure_password")
    driver.find_element(By.ID, "loginBtn").click()
    
    # Assertion
    assert "Dashboard" in driver.page_source
    
    driver.quit()
```

## 3. PRO TIPS
- **Don't memorize the code** — but recognize Selenium structure if shown in MCQ.
- Keywords to spot: `webdriver.Chrome()`, `find_element(By.ID, ...)`, `send_keys()`, `assert`.

---

# SLIDES 24-25 — Stage 6: Test Analysis & Reporting

## 1. Plain English Explanation
Final stage. Gather results, analyze failures, generate reports, share insights, improve quality.

## 2. Theory (Exactly as in slides)

**Key Activities:**

| Activity | Description |
|----------|-------------|
| Collect Test Results | Gather execution data: passed, failed, skipped |
| Analyze Failures | Investigate: app bug, flaky test, environment issue |
| Generate Reports | HTML, PDFs, dashboards |
| Visualize Metrics | Execution time, pass rate, coverage |
| Share Insights | QA, Dev, PMs — dashboards, emails, standups |
| Improve Test Quality | Refactor flaky tests; add missing coverage |

**Useful Metrics to Track:**

| Metric | Why It Matters |
|--------|-----------------|
| Pass/Fail Rate | Overall stability |
| Test Flakiness Rate | Flags unstable tests |
| Time to Execute | Suite efficiency |
| Test Coverage | Critical paths tested |
| Defects Detected Early | Automation ROI |

## 3. Example Daily Report (Slide 25)
> **Project:** Online Banking App
> - 98 tests run → 90 passed, 8 failed
> - 5 flaky tests identified
> - Avg execution time: 6.5 mins
> - Coverage: 80% of core flows
> - Shared via Slack + CI dashboard

## 4. PRO TIPS
- **5 metrics to memorize:** Pass/Fail, Flakiness, Time, Coverage, Early Defects.
- **A4 Sheet:** *Reporting = Collect + Analyze + Generate + Visualize + Share + Improve.*

---

# SLIDE 26 — Test Automation Pyramid

## 1. Plain English Explanation
A model showing the **3 layers** of tests in an ideal automation strategy. Most tests should be at the bottom (Unit), fewer at the top (Acceptance).

## 2. Theory (Exactly as in slides)
```
                  ▲
                 / \
                /   \
               /Accept-\        Acceptance Tests
              / ance    \       (entire app + UI, real-world)
             /-----------\
            /             \
           /  Integration  \    Integration Tests
          /     Tests       \   (program units combined as groups)
         /-------------------\
        /                     \
       /        Unit           \  Unit Tests
      /         Tests           \ (isolated small pieces of code)
     /___________________________\
                                  
   ← Number of tests increases →   
   Cost & time-per-test goes DOWN  
   Speed of execution goes UP      
```

## 3. Comparison Table — The Pyramid

| Layer | What It Tests | Number of Tests | Cost | Speed |
|-------|---------------|------------------|------|-------|
| **Acceptance** (top) | Whole app + UI in real-world scenario | Fewest | High | Slow |
| **Integration** (middle) | Program units combined as groups | More | Medium | Medium |
| **Unit** (bottom) | Isolated small code pieces | Most | Low | Fast |

## 4. PRO TIPS
- **Memory trick:** "**Lots of Unit, Some Integration, Few Acceptance**" — pyramid shape.
- **Higher up = slower, more expensive, fewer tests.**
- **A4 Sheet:** Draw the pyramid with 3 layers labeled.

## Quick Recap
- Test pyramid: Unit (most) → Integration (middle) → Acceptance (fewest).

---

# SLIDE 27 — Classification of Test Automation

## 1. Plain English Explanation
Test automation can be classified along **4 dimensions**.

## 2. Theory (Exactly as in slides)

| Dimension | Categories |
|-----------|------------|
| **Type of testing** | Functional, Non-Functional |
| **Type of tests** | Unit, Smoke, API, UI, Regression, Security, Performance, UAT, … |
| **Phase of tests** | Development (Unit), Integration (API), System (UAT/GUI) |
| **Execution platform** | Device (Desktop, tablet, phone, browser), Mobile (Native, mobile web, emulator), Location (On-prem, Cloud, multi-geo) |

## PRO TIPS
- **4 classification dimensions** — memorize.
- **A4 Sheet:** *Classify automation by: Type of testing / Type of tests / Phase / Execution platform.*

---

# SLIDE 28 — Test Automation Frameworks (Overview)

## 1. Plain English Explanation
A **framework** is the foundation that organizes your test scripts, tools, and best practices. Different frameworks suit different projects.

## 2. Theory (Exactly as in slides)
> A test automation framework is a set of **guidelines, tools, and practices** designed to help automate software testing in a structured and efficient way.
>
> It's the **foundation and toolbox** you use to write, organize, and run automated tests consistently across your project.

**5 Types of Frameworks (from slide):**
1. Modular Testing Framework
2. Data Driven Testing Framework
3. Keyword Driven Testing Framework
4. Hybrid Testing Framework
5. Behavior Driven Development (BDD) Framework

> *Note: Slide 30 also introduces a 6th type — **Linear Scripting Framework** — that wasn't shown in the type diagram on slide 28 but is treated as a framework type elsewhere. Total = 6 frameworks (including Linear).*

## PRO TIPS
- **Memory trick — "L-M-D-K-H-B"** → **L**inear, **M**odular, **D**ata-driven, **K**eyword-driven, **H**ybrid, **B**DD.
- **HIGHEST EXAM-LIKELY ESSAY:** "Explain the types of Test Automation Frameworks with advantages/disadvantages."

## Quick Recap
- 6 framework types (5 + Linear). Memorize all + examples.

---

# SLIDE 29 — Key Features of Automation Frameworks

## 2. Theory (Exactly as in slides)
- **Reusability** — Common functions and utilities used across tests
- **Maintainability** — Easier to update tests as the app changes
- **Scalability** — Supports adding more tests without breaking
- **Consistency** — Standardizes test writing, naming, structure
- **Reporting** — Logs, pass/fail summaries, screenshots
- **Integration** — Connects with CI/CD tools, bug trackers

## PRO TIPS
- **6 key features — "R-M-S-C-R-I"** → Reusability, Maintainability, Scalability, Consistency, Reporting, Integration.
- **A4 Sheet:** *Framework features = R-M-S-C-R-I.*

---

# SLIDE 30 — Framework #1: Linear Scripting (Record & Playback)

## 1. Plain English Explanation
Simplest framework: you **record** your manual actions (clicks, typing) and **play them back**. No coding needed. Best for beginners or tiny projects.

## 2. Theory (Exactly as in slides)
- Also known as the **'Record and Playback'** framework
- Simple and best for small projects or beginners
- Each test is written individually without much reuse

**Advantages:**
- Coding knowledge **not required**
- Quick way to generate test scripts

**Disadvantages:**
- Hard to maintain as project grows
- Lack of reusability

**Example:** Selenium IDE — record browser actions and play them back.

## PRO TIPS
- **A4 Sheet:** *Linear = Record/Playback → no coding → no reuse → small projects only.*

---

# SLIDE 31 — Framework #2: Modular Testing Framework

## 1. Plain English Explanation
Break tests into **reusable modules** (like login, logout, search). Each test case calls modules as needed.

## 2. Theory (Exactly as in slides)
- Breaks tests into **independent, reusable modules**
- Each test case calls these modules as needed
- Use **Page Object Model (POM)** for maintainability

**Advantages:**
- Better scalability and easier to maintain
- Can write test scripts independently

**Disadvantages:**
- Requires more initial effort to develop scripts
- Requires coding skills to set up the framework

**Example (from slide):**
```python
# login_module.py
def login(username, password):
    # login steps here

# test_cart.py
from login_module import login
login('user1', 'pass123')
# continue with cart tests
```

## PRO TIPS
- **Key concept:** Page Object Model (POM) — every page = a class.
- **A4 Sheet:** *Modular = reusable modules (POM) → scalable but more upfront work.*

---

# SLIDE 32 — Framework #3: Data-Driven Framework

## 1. Plain English Explanation
Separate **test logic** from **test data**. Same script runs with many different data sets from Excel/CSV/DB.

## 2. Theory (Exactly as in slides)
- Focused on **separating test scripts logic and test data**
- Test data kept in external files: MS Excel, MS Access, SQL DB, XML files

**Advantages:**
- Supports multiple data sets
- Modifying test scripts won't affect test data

**Disadvantages:**
- Requires coding skills
- Setting up framework + data takes more time

**Example:** Use an Excel or CSV file to test a form with 100 inputs.

## PRO TIPS
- **Distinguishing keyword:** "data is **external** (Excel, CSV, SQL, XML)."
- **A4 Sheet:** *Data-driven = test logic + external data files → multiple data sets per script.*

---

# SLIDES 33-34 — Framework #4: Keyword-Driven Framework

## 1. Plain English Explanation
Tests are written as **keywords** like `OpenBrowser`, `EnterText`, `Click`. Non-coders can build tests by chaining keywords.

## 2. Theory (Exactly as in slides)
**How it works:**
```
Keyword Library → Automation Script → Application Under Test
  Test Input Data       Enter Input Data
  Test Output Data      Send Output Data
```

**Advantages:**
- No need to be an expert to write test scripts
- Reusable code — different scripts can point to same keyword

**Disadvantages:**
- Takes more time to design
- Initial cost is high

## 3. Example (from Slide 34 — Login to a website):

| Step | Keyword | Object | Test Data |
|------|---------|--------|-----------|
| 1 | OpenBrowser | chrome | URL |
| 2 | EnterText | username_field | testuser |
| 3 | EnterText | password_field | password123 |
| 4 | Click | login_button | — |
| 5 | VerifyText | welcome_label | Welcome, User! |
| 6 | CloseBrowser | — | — |

## 4. PRO TIPS
- **Distinguishing keyword:** "keywords" (action verbs) drive the framework.
- **Tool:** Robot Framework is the most famous Keyword-Driven tool.
- **A4 Sheet:** *Keyword-driven = action keywords in tables → reusable, non-coder friendly, high setup cost.*

---

# SLIDE 35 — Framework #5: Hybrid Framework

## 1. Plain English Explanation
Combines **2+ framework types** (e.g., Modular + Data-Driven + Keyword-Driven). **Most real-world projects use Hybrid.**

## 2. Theory (Exactly as in slides)
- Combines two or more approaches (like data + keyword driven)
- **Most real-world projects use hybrid frameworks**
- **Example:** Selenium with Python where test logic is modular, data is externalized in Excel, actions are keyword-based.

## PRO TIPS
- **Memory cue:** "Hybrid = best of all worlds."
- **A4 Sheet:** *Hybrid = mix of 2+ framework types → most common in real projects.*

---

# SLIDES 36-37 — Framework #6: Behavior-Driven Development (BDD)

## 1. Plain English Explanation
Tests are written in **natural language** so business stakeholders can read them. Uses **Gherkin syntax** (Given-When-Then).

## 2. Theory (Exactly as in slides)
- BDD is a development approach that **encourages collaboration** between developers, testers, and business stakeholders.
- Focuses on writing tests in **natural language** that non-technical stakeholders can understand.
- Tests written in **Gherkin syntax (Given–When–Then format)** describing expected behavior from a user perspective.

## 3. Example Gherkin Syntax (Slide 37)
```gherkin
Feature: Login functionality

Scenario: Successful login with valid credentials
   Given the user is on the login page
   When the user enters valid username and password
   And clicks the login button
   Then the user should be redirected to the dashboard
```

## 4. PRO TIPS
- **Memory cue:** BDD = **G**iven-**W**hen-**T**hen = **G-W-T**.
- **Tools:** Cucumber (Java), Behave (Python), SpecFlow (.NET).
- **Strong essay phrase:** "BDD bridges devs, testers, and business stakeholders by using natural language Gherkin tests."

---

# SLIDE 38 — Frameworks vs Tools (Summary)

| Framework Type | Tools / Libraries |
|----------------|--------------------|
| **Linear** | Selenium IDE, Katalon Recorder |
| **Modular** | Selenium + Python/Java |
| **Data-Driven** | TestNG + Excel, JUnit + CSV |
| **Keyword-Driven** | Robot Framework, Katalon Studio |
| **Hybrid** | Selenium + TestNG + Apache POI |
| **BDD** | Cucumber (Java), Behave (Python) |

## PRO TIPS
- **MCQ MAGIC ANSWER PAIRS:**
  - BDD → **Cucumber** / **Behave**
  - Keyword-Driven → **Robot Framework**
  - Data-Driven → **TestNG / JUnit + external data**
  - Linear → **Selenium IDE**
- **A4 Sheet:** This 6-row table verbatim.

---

# SLIDE 39 — Integrating Test Automation with CI/CD

## 1. Plain English Explanation
**CI/CD** = pipeline that automatically integrates code + delivers it. Adding automated tests to CI/CD = fast feedback and early bug detection.

## 2. Theory (Exactly as in slides)
- **Continuous Integration (CI):** Automating the integration of code changes into the main codebase.
- **Continuous Delivery (CD):** Automating the deployment process to ensure new changes are automatically released.

**Automation in CI/CD:**
- Integrate automated tests in the CI/CD pipeline to run **on every code commit**.
- **Benefits:** Faster feedback loops, early bug detection, seamless delivery.

## PRO TIPS
- **CI vs CD:**
  - CI = Code integration into main.
  - CD = Code delivery to production.
- **A4 Sheet:** *CI = code integration; CD = code delivery. Automated tests run on every commit.*

---

# SLIDE 40 — Challenges in Test Automation

## 2. Theory (Exactly as in slides)

| # | Challenge | Description |
|---|-----------|-------------|
| 1 | **High Initial Investment** | Significant time and cost to choose tools, build frameworks, train staff |
| 2 | **Test Maintenance Overhead** | UI / app changes require frequent test updates |
| 3 | **Unstable Tests (Flaky Tests)** | Pass sometimes, fail sometimes — reduces trust |
| 4 | **Partial Test Coverage** | Not all test cases can be automated |
| 5 | **Choosing the Right Tool** | Matching tools with tech stack, team skill, project needs is hard |
| 6 | **Lack of Skilled Resources** | Need testing knowledge + programming skills |

## PRO TIPS
- **6 challenges to memorize** for a 6-mark essay.
- **A4 Sheet:** Memory acronym "**H-T-U-P-C-L**" → High cost, Test maintenance, Unstable tests, Partial coverage, Choosing tool, Lack of skills.

---

# SLIDE 41 — Flaky Tests

## 1. Plain English Explanation
A **flaky test** is one that **passes sometimes and fails sometimes** — for no reason connected to the code. Big problem for trust in automation.

## 2. Theory (Exactly as in slides)
> A flaky test is a test that **sometimes passes and sometimes fails without any change to the code**.
>
> The test result is not reliable even though the code and environment haven't changed.

**Common Causes of Flaky Tests:**

| Cause | Example |
|-------|---------|
| **Timing issues / async waits** | Test clicks a button before it's actually clickable |
| **Element not yet loaded** | Trying to read a field before it appears |
| **Network / API delays** | Test fails if an API call is slow but eventually works |
| **Dependency on external systems** | Test hits a 3rd-party API that is temporarily down |

## PRO TIPS
- **4 causes of flaky tests** — memorize.
- **A4 Sheet:** *Flaky test = unreliable test → causes: Timing, Loading, Network, External systems.*

## Quick Recap
- Flaky test = passes sometimes, fails sometimes.
- 4 main causes: timing, loading, network, external deps.

---

# SLIDE 42 — Myths in Test Automation (10 Myths)

## 2. Theory (Exactly as in slides)

| # | Myth |
|---|------|
| 1 | Test automation is expensive and requires a lot of resources. |
| 2 | Test automation totally eliminates the need for manual testing and replaces jobs. |
| 3 | Test automation is only suitable for large projects with ample resources. |
| 4 | It's better to use Selenium or another open-source tool to test. |
| 5 | You need to be a technical expert to utilize automation. |
| 6 | Test automation can be done absolutely by anyone. |
| 7 | Test automation is just a fad. |
| 8 | Test automation is a one-time activity. |
| 9 | Test automation is only for regression testing. |
| 10 | Test automation is inflexible and cannot adapt to changes in software requirements. It is hard to maintain. |

## PRO TIPS
- **10 myths** — memorize at least 5 for partial credit.
- **Most-tested myths:** #2 (replaces manual), #8 (one-time activity), #9 (regression only).
- **A4 Sheet:** Top 5 myths in 1-line each.

---

# SLIDES 43-45
*Assignment 2 details, Quiz instructions, Thank You slide. No teaching content.*

---

# 🎯 EXTRA EXAMPLES (Beyond Slides)

### Example A — Simple Framework Choice Scenario
**Spec:** A small startup needs to automate a login page only. 2 testers, neither knows coding.

**Best framework:** **Linear (Record & Playback)** with **Selenium IDE**.
**Why:** No coding required, fast setup, small scale.

---

### Example B — Complex Framework Choice Scenario
**Spec:** A large bank automates regression tests for 200+ APIs and 50 web screens. Has 4 testers (Python + Java skilled).

**Best framework:** **Hybrid (Modular + Data-Driven + BDD)**.
**Why:**
- **Modular** → reusable login/transaction modules.
- **Data-Driven** → 1,000+ input combinations from Excel.
- **BDD (Cucumber)** → business stakeholders can read test scenarios.
**Tools:** Selenium + TestNG + Apache POI + Cucumber + JMeter (for performance).

---

# 📊 MASTER COMPARISON — 6 FRAMEWORK TYPES

| Framework | Coding Required? | Reusable? | Best For | Tools |
|-----------|------------------|------------|----------|-------|
| **Linear** | ❌ No | ❌ No | Tiny projects, beginners | Selenium IDE |
| **Modular** | ✅ Yes | ✅ Yes | Medium projects with reusable parts | Selenium + Java/Python |
| **Data-Driven** | ✅ Yes | ✅ Yes (data) | Many input combos | TestNG + Excel/CSV |
| **Keyword-Driven** | ⚠️ Some | ✅ Yes (keywords) | Non-coders writing tests | Robot Framework |
| **Hybrid** | ✅ Yes | ✅ Yes | Most real-world projects | Selenium + TestNG + POI |
| **BDD** | ✅ Yes (steps) | ✅ Yes (scenarios) | Cross-team collaboration | Cucumber, Behave |

---

# 📝 MCQ PRACTICE — LECTURE 9

---

### Q1. Which of the following is the BEST candidate for automation?
A) Exploratory Testing
B) Usability Testing
C) **Regression Testing** ✅
D) Short-lived feature

**Answer: C (Slide 5)**

---

### Q2. Which framework is also known as "Record and Playback"?
A) Modular
B) Keyword-Driven
C) Hybrid
D) **Linear Scripting** ✅

**Answer: D (Slide 30)**

---

### Q3. BDD tests are written in:
A) Java syntax
B) Python syntax
C) **Gherkin syntax (Given-When-Then)** ✅
D) JavaScript syntax

**Answer: C (Slide 37)**

---

### Q4. A test that sometimes passes and sometimes fails without any change to the code is called:
A) Unstable test
B) **Flaky test** ✅
C) Manual test
D) Regression test

**Answer: B (Slide 41)**

---

### Q5. Which tool is BEST for mobile app automation?
A) Selenium
B) **Appium** ✅
C) JMeter
D) Cucumber

**Answer: B (Slides 16-18)**

---

### Q6. The Test Automation Pyramid suggests we should have:
A) Most acceptance tests, fewest unit tests
B) Equal number of all three layers
C) **Most unit tests, fewest acceptance tests** ✅
D) Only integration tests

**Answer: C (Slide 26)**

---

### Q7. Which framework separates test scripts from test data using Excel/CSV files?
A) Linear
B) Keyword-Driven
C) BDD
D) **Data-Driven** ✅

**Answer: D (Slide 32)**

---

### Q8. Which is NOT a stage of the Test Automation Lifecycle?
A) Deciding the scope
B) Choosing the right tool
C) **Bug Fixing** ✅
D) Test Analysis and Reporting

**Answer: C — Bug fixing is not part of the test automation lifecycle (Slide 12)**

---

### Q9. Continuous Integration (CI) means:
A) Continuously delivering code to production
B) **Automating integration of code changes into the main codebase** ✅
C) Manually integrating code once a week
D) Eliminating all automated tests

**Answer: B (Slide 39)**

---

### Q10. Which is the MOST commonly used framework in real-world projects?
A) Linear
B) Keyword-Driven only
C) **Hybrid** ✅
D) BDD only

**Answer: C (Slide 35)**

---

# 📌 LECTURE 9 — A4 REFERENCE SHEET MINI-SECTION

```
TEST AUTOMATION
  Definition: Use of software tools to auto-run & validate test cases → enhances efficiency

WHEN TO AUTOMATE (R-S-H-D-C-S):
  Regression, Smoke/Sanity, High-volume, Data-driven,
  Cross-browser/device, Stable features

WHEN NOT TO AUTOMATE (E-S-U-U-O-C):
  Exploratory, Short-lived, Unstable UI, Usability,
  Once-only, Complex logic (CAPTCHA, image)

BENEFITS:
  App-wise (5): Quality↑, Accuracy↑, Coverage↑, Early bugs, Reusable scripts
  Cost-wise (3): Save Cost, Save Time, ROI↑

MANUAL vs AUTOMATED (7 dimensions):
  Execution time, Initial setup, Reliability, Programming,
  Reusability, Reporting, Flexibility

6 PRINCIPLES OF TEST AUTOMATION (Q-R-U-W-R-M):
  Quality, Risk reduction, Understand code,
  Write easy, Run easy, Minimal maintenance

TEST AUTOMATION LIFECYCLE (6 stages, S-T-P-E-W-R):
  1. Scope
  2. Tool selection
  3. Plan/Design/Strategy
  4. Environment setup
  5. Script & Execution
  6. Analysis & Reporting

TEST AUTOMATION PYRAMID:
  Acceptance tests (top, few)
  Integration tests (middle)
  Unit tests (bottom, many) → fast, cheap

CLASSIFICATION (4 dimensions):
  Type of testing / Type of tests / Phase / Execution platform

6 FRAMEWORK TYPES (L-M-D-K-H-B):
  Linear      → Record/Playback (Selenium IDE)
  Modular     → POM, reusable modules
  Data-Driven → external test data (Excel/CSV)
  Keyword-Driven → action keywords (Robot Framework)
  Hybrid      → mix of all (most real projects)
  BDD         → Gherkin syntax G-W-T (Cucumber/Behave)

FRAMEWORK KEY FEATURES (R-M-S-C-R-I):
  Reusability, Maintainability, Scalability,
  Consistency, Reporting, Integration

KEY TOOLS:
  Web: Selenium, Playwright, Cypress
  Mobile: Appium, Katalon
  Performance: JMeter, LoadRunner
  API: Postman
  BDD: Cucumber, Behave
  Performance (DB): dbForge, SQLTest

CI/CD:
  CI = Continuous Integration (code → main)
  CD = Continuous Delivery (code → production)
  Auto-tests run on every code commit

6 CHALLENGES:
  High investment, Maintenance, Flaky tests,
  Partial coverage, Tool choice, Lack of skills

FLAKY TEST CAUSES (4):
  Timing/async, Element not loaded,
  Network/API delays, External dependencies

10 MYTHS (top 3):
  #2 — Replaces manual testing entirely
  #8 — One-time activity
  #9 — Only for regression
```

---

# ✅ LECTURE 9 — DONE

This lecture is **memorization-heavy** — frameworks, tools, lifecycle stages, principles. The exam will almost certainly ask:
1. **"Compare Manual vs Automated Testing"** — use the 7-row comparison table.
2. **"Explain the 5 (or 6) types of Test Automation Frameworks with examples."**
3. **"When should you / should you NOT automate?"** — list the 6+6 cases.
4. **"Explain the Test Automation Lifecycle."**
5. **"What is a Flaky Test?"** — 4 causes.

Reply **"done"** to continue to **Lecture 10**.
