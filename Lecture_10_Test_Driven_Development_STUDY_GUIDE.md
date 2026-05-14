# LECTURE 10 — TEST DRIVEN DEVELOPMENT (TDD)
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **⚠️ IMPORTANT NOTE FOR THIS LECTURE**
> Lecture 10 is **pure conceptual + code-example heavy** — no math, no calculations.
>
> This lecture covers the **highest essay-likely topics** in L8–L11:
> - **Red-Green-Refactor cycle** (most famous TDD concept)
> - **3 Rules of TDD**
> - **TDD vs Traditional Testing** (comparison table)
> - **SOLID Principles** (S-O-L-I-D, 5 OOP principles)
> - **Benefits + Challenges** (6 + 6)
> - **Using Mocks in TDD**
>
> **Top exam-likely essay questions:**
> 1. "Explain TDD lifecycle (Red-Green-Refactor)."
> 2. "Compare TDD vs Traditional Testing."
> 3. "Explain the SOLID Principles with examples."

---

# SLIDE 1 — Title Slide
"Test Driven Development." Skip.

---

# SLIDE 2 — TDD Overview

## 1. Plain English Explanation
This lecture covers **8 topics**:
1. Introduction to Test Driven Development
2. TDD vs Traditional Testing
3. Three Rules in TDD
4. TDD Lifecycle
5. SOLID Principles for TDD
6. TDD Impact on Developers
7. Benefits and Challenges
8. TDD Myths

## PRO TIPS
- Memorize the 8 topics — exam structure follows them.

---

# SLIDE 3 — What is Test-Driven Development?

## 1. Plain English Explanation
TDD = **write the test FIRST**, then write **just enough code** to pass it. The opposite of traditional "code first, test later."

## 2. Theory (Exactly as in slides)
- A software development technique which **reiterates the importance of testing**
- Promotes **writing software requirements as tests** as the initial step in developing a code
- **Initially writes tests** and then moves forward with the **least amount of code needed** to get through the tests

## 3. PRO TIPS
- **HIGH-FREQUENCY EXAM DEFINITION** — memorize verbatim.
- **Key phrase:** "Tests first, then the **least amount of code** to make them pass."
- **A4 Sheet:** *TDD = write test FIRST → write minimal code to pass → refactor.*

## Quick Recap
- TDD reverses the normal order: test → code (not code → test).

---

# SLIDE 4 — Brief History of TDD

## 1. Plain English Explanation
TDD was popularized by **Kent Beck** in the late 1990s. He wrote the foundational book in 2002. Closely linked to the Agile movement.

## 2. Theory (Exactly as in slides)
- **Late 1990s:** TDD as a formalized practice was popularized by **Kent Beck** during the development of **Extreme Programming (XP)**.
- Kent Beck later published the book **"Test-Driven Development: By Example" (2002)** — a foundational text.
- Origins tied to the **Agile Movement** — iterative, feedback-driven development.

## 3. PRO TIPS
- **3 KEY FACTS to memorize:**
  - **Kent Beck** = author/popularizer
  - **Extreme Programming (XP)** = where it came from
  - **2002** = book "Test-Driven Development: By Example"
- High-frequency MCQ.

---

# SLIDE 5 — TDD in Agile Context

## 1. Plain English Explanation
TDD fits perfectly inside Agile because both emphasize **fast feedback, continuous integration, and customer collaboration**.

## 2. Theory (Exactly as in slides)
**TDD fits Agile because it supports:**
- **Short feedback loops** (you know if your code works instantly)
- **Continuous integration** (tests support rapid changes)
- **Customer collaboration** (cleaner, testable code is easier to evolve)

Agile methodologies like **Scrum** and **Extreme Programming (XP)** use TDD as a key technical practice.

## 3. PRO TIPS
- **3 reasons TDD fits Agile:** feedback / CI / customer collaboration.
- **Frameworks where TDD fits:** Scrum, XP.
- **A4 Sheet:** *TDD + Agile → short feedback + CI + customer collab. Used in Scrum & XP.*

---

# SLIDE 6 — Test-Driven vs Traditional Testing (CRITICAL EXAM TABLE)

## 1. Plain English Explanation
6 dimensions where TDD and Traditional Testing differ — exam loves this comparison.

## 2. Comparison Table (Exactly as in slides)

| # | Aspect | **TDD** | **Traditional Testing** |
|---|--------|---------|--------------------------|
| 1 | **Approach** | Tests are written **before** code | Testing performed **after** code |
| 2 | **Test Focus** | Small, incremental tests for specific features | Comprehensive testing of the entire application |
| 3 | **Test Creation** | Tests written by **developers** based on requirements | Tests created by **dedicated QA testers** |
| 4 | **Code Coverage** | High coverage, focus on critical paths | Varies by test cases |
| 5 | **Feedback Loop** | **Immediate** feedback on code changes | Feedback **delayed** until testing phase |
| 6 | **Bug Detection** | Bugs identified **early** in development | Bugs may be detected **later** in cycle |

## 3. PRO TIPS
- **VERY HIGH ESSAY PROBABILITY:** "Compare TDD vs Traditional Testing." → memorize this 6-row table.
- **A4 Sheet:** Full 6-row comparison.

## Quick Recap
- TDD = test-first, dev-written, small + early.
- Traditional = test-after, QA-written, comprehensive + late.

---

# SLIDES 7-8 — Steps in TDD (5-Step Process)

## 1. Plain English Explanation
The 5-step TDD workflow — read requirement → write failing test → write code to pass → refactor → repeat.

## 2. Theory (Exactly as in slides)
1. **Read and understand** the feature request from clients.
2. **Translate them by creating a test.** This test will fail when you run it (no code yet).
3. Now, **write and implement the code to pass the test.** Run the test → it should pass. If not, repeat.
4. Once it passes, **clean your code up** by refactoring.
5. **Repeat** above steps for another requirement.

## 3. Flowchart (from Slide 8)
```
[Start] → [Write test case] → [Run all tests]
              ↓
   ┌─ [test fails] → [Write some code] → (loop back to "Run all tests")
   └─ [test passes] → [refactor needed?]
                            ↓
                ┌─ Yes → [Refactor] → (loop back to "Run all tests")
                └─ No → [End]
```

## 4. PRO TIPS
- **5-step process:** Understand → Write test (fail) → Write code (pass) → Refactor → Repeat.
- **A4 Sheet:** *TDD steps: 1) Read req 2) Write failing test 3) Make it pass 4) Refactor 5) Repeat.*

---

# SLIDE 9 — TDD Cycle (Red-Green-Refactor) — MASTER CONCEPT

## 1. Plain English Explanation
The **most famous TDD diagram**. 3 colored phases:
- 🔴 **Red** = test fails (code doesn't exist yet)
- 🟢 **Green** = test passes (code works, but not optimal)
- 🔵 **Blue (Refactor)** = clean up the code

## 2. Theory (Exactly as in slides)

```
        🔴 Write a failing test
              ↓
        🟢 Make the test pass
              ↓
        🔵 Refactor
              ↓
       (loop back to 🔴)
```

| Phase | What it means |
|-------|----------------|
| **🔴 Red** | Code is **not working** (test fails because feature doesn't exist) |
| **🟢 Green** | Everything is **working**, but not optimal yet |
| **🔵 Refactor** | Code is being **cleaned up** (without changing behavior) |

## 3. PRO TIPS
- **HIGHEST EXAM PROBABILITY:** "Explain the Red-Green-Refactor cycle."
- **Memory trick:** "**R-G-R**" → **R**ed (fail), **G**reen (pass), **R**efactor (clean).
- **A4 Sheet:** Draw the 3-phase circle.

## Quick Recap
- 3 phases: Red → Green → Refactor → loop.

---

# SLIDE 10 — TDD Cycle: 🔴 Red Phase

## 1. Plain English Explanation
**Goal:** Write a test that fails — because the feature doesn't exist yet.

## 2. Theory (Exactly as in slides)
**Goal:** Write a test that fails because the functionality you want doesn't exist yet.

**Why?**
- Forces you to **think about the problem** and define **expected behavior before implementation**.
- Ensures your test is **valid** — if it doesn't fail when the feature is missing, something's wrong with the test.
- **Prevents writing unnecessary code** — you only write code to make the test pass.

## 3. PRO TIPS
- **A4 Sheet:** *Red = write a failing test → forces thinking + prevents unnecessary code.*

## Quick Recap
- Red = test FAILS first. That's the goal. It proves the test is valid.

---

# SLIDE 11 — TDD Cycle: 🟢 Green Phase

## 1. Plain English Explanation
**Goal:** Write the **smallest amount of code** to make the failing test pass. No more.

## 2. Theory (Exactly as in slides)
**Goal:** Write **just enough code** to make the failing test from the Red Phase pass — nothing more.

> **"Get it working first. Make it beautiful later."**

**Why?**
- Ensures your test was valid.
- Gives you **confidence** that the system behaves as expected.
- Helps you build functionality **incrementally**.
- Keeps you focused — no extra code means less chance of bugs.

## 3. PRO TIPS
- **Key quote to memorize:** *"Get it working first. Make it beautiful later."*
- **A4 Sheet:** *Green = minimum code to pass test → no extra logic.*

## Quick Recap
- Green = write **minimum** code → make test pass.

---

# SLIDE 12 — TDD Cycle: 🔵 Refactor Phase

## 1. Plain English Explanation
**Goal:** Make the code **clean** — better structure, readability, maintainability — but don't change behavior.

## 2. Theory (Exactly as in slides)
**Goal:** Improve the code's **structure, readability, and maintainability** — without changing its behavior.

> **"Now that it works, let's make it nice."**

**Why?**
- Keeps code **clean and maintainable**.
- Prevents **technical debt** from accumulating.

**What to do?**
- Remove duplication.
- Rename variables/methods for clarity.
- Simplify logic or extract methods.

## 3. PRO TIPS
- **Key quote:** *"Now that it works, let's make it nice."*
- **Key term:** "**Technical debt**" — accumulating bad code over time.
- **A4 Sheet:** *Refactor = clean code → remove duplication, rename, simplify, prevent tech debt.*

## Quick Recap
- Refactor = clean code without changing behavior.
- Prevents technical debt.

---

# SLIDE 13 — Activity (Discuss in Pairs)
*Group activity. No teaching content. Skip.*

---

# SLIDE 14 — Three Rules of TDD (Robert C. Martin's Rules)

## 1. Plain English Explanation
3 strict rules every TDD practitioner follows. **Frequent exam target.**

## 2. Theory (Exactly as in slides)

| # | Rule | Meaning |
|---|------|---------|
| **#1** | **No code without a test** | No new features or logic unless there's already a test **failing** because that logic is missing |
| **#2** | **No more test than needed** | Don't write multiple/long tests upfront. Write just **enough to see the test fail** |
| **#3** | **No more code than needed** | Only write code that's needed to make the current test pass. No extra logic, no predictions of future features |

## 3. PRO TIPS
- **HIGH EXAM PROBABILITY:** "List the 3 rules of TDD."
- **Memory trick:** "**No code without test, No more test, No more code**" → minimalism rule.
- **A4 Sheet:** Three rules in one line each.

## Quick Recap
- 3 strict rules: no code-without-test, minimum tests, minimum code.

---

# SLIDE 15 — Rule #1 Example: No code without a test

## Code Examples (from slide)

**Example A: Addition function**
```python
# You can't write this 'add' function until you've written a test like below
def add(a, b):
    return a + b
```

```python
# First, write this failing test
def test_addition():
    assert add(2, 3) == 5   # ❌ This test will fail initially
```
*Once the test fails, you write the minimal code to make it pass.*

**Example B: Password validator**
```python
# Test (write first)
def test_password_too_short():
    validator = PasswordValidator()
    assert not validator.is_valid("abc")  # Password must be at least 6 characters
```
```python
# Code (write only after test fails)
class PasswordValidator:
    def is_valid(self, password):
        return len(password) >= 6
```

## PRO TIPS
- **Lesson:** Always write the test first. The test must fail before you write any code.

---

# SLIDE 16 — Rule #2 Example: No more test than needed

## Code Example (from slide)
**Scenario:** Build a function that sums numbers from a comma-separated string input.

**First Test:** Check if an empty string returns zero.
```python
def test_add_empty_string_returns_zero():
    assert add("") == 0   # ❌ Fails because 'add' isn't implemented yet
```

**Minimal Code:** Just enough to pass this single test.
```python
def add(numbers):
    return 0   # ✅ Now the test passes
```

> *Here we are NOT jumping ahead and writing tests for comma-separated numbers yet — just focused on the first test.*

## PRO TIPS
- **Lesson:** Add tests **one at a time** — don't write 5 tests at once.

---

# SLIDE 17 — Rule #3 Example: No more code than needed

## Code Example (from slide)
**Next Test:** A string with a single number should return that number.
```python
def test_add_single_number():
    assert add("5") == 5
```

**Code:** Update **just enough** to pass.
```python
def add(numbers):
    if numbers == "":
        return 0
    return int(numbers)
```

> *Here we DON'T yet add code to support two numbers or handle delimiters. That comes with future tests.*

## PRO TIPS
- **Lesson:** Don't predict future features. Code only what the **current test** requires.

---

# SLIDE 18 — Benefits of TDD (6 Benefits)

## 2. Theory (Exactly as in slides)

| # | Benefit | Description |
|---|---------|-------------|
| 1 | **Improve code quality** | Code is written to pass specific tests |
| 2 | **Immediate Feedback** | Finds out immediately if something is broken |
| 3 | **Better Design & Maintainability** | Encourages loosely coupled, highly cohesive code |
| 4 | **Documentation Through Tests** | Tests act as **live documentation** of how the system should behave |
| 5 | **Confidence to Refactor** | You can change code structure without fear — tests will catch regressions |
| 6 | **Facilitates Debugging** | When something breaks, you already have unit tests that isolate logic |

## PRO TIPS
- **Memory trick — "Q-I-D-D-C-D"** → Quality, Immediate, Design, Documentation, Confidence, Debug.
- **A4 Sheet:** 6 benefits in 1-line each.

---

# SLIDE 19 — Challenges of TDD (6 Challenges)

## 2. Theory (Exactly as in slides)

| # | Challenge | Description |
|---|-----------|-------------|
| 1 | **Initial Learning Curve** | Beginners struggle with writing tests first or designing testable code |
| 2 | **Slowdown Development at First** | Writing tests before code consumes time initially |
| 3 | **Maintenance Overhead** | Large suite of outdated/redundant tests becomes a burden |
| 4 | **UI, Legacy, or Non-Deterministic Code** | TDD works best with **deterministic, modular code** |
| 5 | **Over-Testing / Rigid Code** | Writing too many detailed tests makes refactoring painful |
| 6 | **Mindset Change** | Requires a **fundamental shift** in how developers think |

## PRO TIPS
- **Memory trick — "L-S-M-U-O-M"** → Learning curve, Slow start, Maintenance, UI/legacy, Over-testing, Mindset.
- **A4 Sheet:** 6 challenges in 1-line each.

## Quick Recap
- 6 benefits + 6 challenges = standard essay structure.

---

# SLIDE 20 — SOLID Principles for TDD (CRITICAL CONCEPT)

## 1. Plain English Explanation
**SOLID** = 5 OOP design principles. TDD naturally encourages following them.

## 2. Theory (Exactly as in slides)

| Letter | Principle | Purpose |
|--------|-----------|---------|
| **S** | **Single Responsibility Principle (SRP)** | One reason to change |
| **O** | **Open/Closed Principle (OCP)** | Open to extend, closed to modify |
| **L** | **Liskov Substitution Principle (LSP)** | Subclasses must be replaceable |
| **I** | **Interface Segregation Principle (ISP)** | Prefer many small interfaces |
| **D** | **Dependency Inversion Principle (DIP)** | Depend on abstractions, not concrete classes |

## 3. PRO TIPS
- **VERY HIGH EXAM PROBABILITY:** "Explain the SOLID principles."
- **Memorize the 5 letters + 5 names.**
- **A4 Sheet:** SOLID table verbatim.

---

# SLIDE 21-22 — S: Single Responsibility Principle (SRP)

## 2. Theory (Exactly as in slides)

**Principle:** A class should have **one and only one reason to change**.
**TDD Implication:** Writing unit tests first tends to **split responsibilities** to make code more testable.

**Key points:**
- Each module/class/function should **do one thing and do it well**.
- If a class is responsible for more than one thing, those responsibilities become **coupled**.
- A change to one responsibility may impact the others.

## 3. Example (from Slide 22)
**Before (Violates SRP):**
```python
class ReportService:
    def generate_report(self):
        # gathers data, formats it, sends email  ← too many roles
```

**After (TDD forces separation):**
```python
class DataFetcher:
    def get_data(self): pass

class ReportFormatter:
    def format(self, data): pass

class EmailSender:
    def send(self, report): pass
```

## PRO TIPS
- **S = "One Class = One Responsibility"**
- **A4 Sheet:** *SRP → one class, one reason to change.*

---

# SLIDE 23-24 — O: Open/Closed Principle (OCP)

## 2. Theory (Exactly as in slides)

**Principle:** Software entities should be **open for extension but closed for modification**.
**TDD Implication:** TDD encourages code that evolves via **extension** — changing tested code is risky.

**Key points:**
- Add new functionality **without changing existing code**.
- Protects existing behavior from bugs and makes the system easier to maintain.

## 3. Example (from Slide 24)
**Tax calculator extended via new class (not modification):**
```python
class TaxStrategy:
    def calculate(self, amount): pass

class FixedTax(TaxStrategy):
    def calculate(self, amount):
        return amount * 0.1

class ProgressiveTax(TaxStrategy):
    def calculate(self, amount):
        if amount > 1000:
            return amount * 0.2
        else:
            return amount * 0.1
```

> *You don't modify existing logic — you EXTEND with a new class.*

## PRO TIPS
- **O = "Add new classes, don't change old ones."**
- **A4 Sheet:** *OCP → open to extension, closed to modification.*

---

# SLIDE 25-27 — L: Liskov Substitution Principle (LSP)

## 2. Theory (Exactly as in slides)

**Principle:** Subclasses should be **substitutable** for their base classes without altering behavior.
**TDD Implication:** TDD helps spot LSP violations early — when a test for a base class fails with a subclass.

## 3. Example (from Slide 27 — Bird hierarchy)

**Violates LSP:**
```python
class Bird:
    def fly(self):
        print("Flying")

class Ostrich(Bird):
    def fly(self):
        raise NotImplementedError("Ostriches can't fly")  # ❌ breaks substitutability
```

**Fixed (proper hierarchy):**
```python
class Bird:
    def make_sound(self):
        print("Chirp")

class FlyingBird(Bird):
    def fly(self):
        print("Flying")

class Sparrow(FlyingBird):
    pass

class Ostrich(Bird):     # ✅ Ostrich is a Bird but NOT a FlyingBird
    pass
```

## PRO TIPS
- **L = "Subclass must work wherever parent works."**
- **A4 Sheet:** *LSP → subclasses must be replaceable for parents.*

---

# SLIDE 28-29 — I: Interface Segregation Principle (ISP)

## 2. Theory (Exactly as in slides)

**Principle:** Clients shouldn't be forced to depend on **interfaces they don't use**.
**TDD Implication:** TDD naturally leads to **smaller, focused interfaces** because large ones are hard to test.

## 3. Example (from Slide 29 — Printer)

**Before ISP (one big interface):**
```python
class Printer:
    def print_document(self): pass
    def scan_document(self): pass    # SimplePrinter forced to implement this
```

**Better design with ISP (split interfaces):**
```python
class Printable:
    def print_document(self): pass

class Scannable:
    def scan_document(self): pass

class SimplePrinter(Printable): pass
class MultiFunctionPrinter(Printable, Scannable): pass
```

## PRO TIPS
- **I = "Many small interfaces > one fat interface."**
- **A4 Sheet:** *ISP → small, focused interfaces.*

---

# SLIDE 30-31 — D: Dependency Inversion Principle (DIP)

## 2. Theory (Exactly as in slides)

**Principle:** Depend on **abstractions**, not on concrete implementations.
**TDD Implication:** You often start by **mocking dependencies**, which encourages depending on interfaces, not classes.

## 3. Example (from Slide 31 — UserSignupService)

**Tightly coupled (no DIP):**
- UserSignupService directly uses concrete EmailService.
- Tests would send real emails (bad), rely on infrastructure (fragile), hard to mock.

**Better design with DIP:**
- UserSignupService depends on a **MessageSender interface**.
- Tests are isolated, fast, reliable.
- Can verify "a welcome message was sent" without sending real emails.
- Tests stay green even if you switch to SMS or in-app notifications.

## PRO TIPS
- **D = "Depend on interfaces, not concrete classes."**
- **A4 Sheet:** *DIP → high-level modules depend on abstractions, not implementations.*

---

# SLIDE 32-33 — Using Mockups in TDD

## 1. Plain English Explanation
**Mocks** = fake versions of dependencies that pretend to behave like real ones. Used in TDD to isolate the unit under test.

## 2. Theory (Exactly as in slides)

**Goal:** Focus your test on only the **behavior of the System Under Test (SUT)**, without involving real implementations of its dependencies.

**Why Use Mocks in TDD?**
- To test only **one unit at a time**.
- To avoid **slow or unreliable dependencies** (e.g., network, databases).
- To simulate specific behaviors like **errors, timeouts, or success cases**.
- To verify **interaction** between the SUT and its dependencies.

## 3. Example (from Slide 33)
**System Under Test (SUT):** `OrderService` — places an order.
**Dependencies:** `PaymentGateway` and `EmailNotifier`

**Without Mocks:**
- Test would charge a real credit card and send real emails.
- Needs real accounts.
- Tests are slow + can fail due to network/email issues.

**With Mocks:**
- Create mock `PaymentGateway` + mock `EmailNotifier`.
- Inject mocks into `OrderService`.
- Simulate a successful payment.
- Verify the email notifier was called correctly.
- Now you're truly testing just the **behavior** of OrderService.

## PRO TIPS
- **Key term: "SUT" (System Under Test)**.
- **4 reasons to use mocks:** isolate unit, avoid slow deps, simulate specific cases, verify interactions.
- **A4 Sheet:** *Mocks = fake dependencies → test ONE unit at a time → simulate errors/success.*

---

# SLIDES 34-36 — TDD Impact on Developer's Life

## 2. Theory (Exactly as in slides — 5 impacts)

| # | Impact | Description |
|---|--------|-------------|
| 1 | **Reversing the Usual Workflow** | Traditional: code → test. TDD: test → fail → code → pass → refactor. Feels backward at first |
| 2 | **Thinking in Small, Testable Units** | TDD forces breaking problems into small steps, focusing on testability |
| 3 | **Letting Tests Drive Design** | Tests guide your architecture (not the other way around) |
| 4 | **Immediate vs. Long-Term Payoff** | TDD feels slower short-term but creates fewer bugs, cleaner code, faster refactoring long-term |
| 5 | **Team and Organizational Culture** | If only one developer adopts TDD, may not mesh with team. Pressure to "deliver fast" discourages tests-first |

## PRO TIPS
- **5 impacts** — memorize for an essay question.
- **A4 Sheet:** *TDD impacts → reverse workflow, small units, test-driven design, long-term ROI, culture challenge.*

---

# SLIDE 37 — TDD Myths and Reality (3 Myths)

## 2. Theory (Exactly as in slides)

| Myth | Reality |
|------|---------|
| **#1: TDD slows down development** | Initially seems slower, but **speeds up development in the long run** |
| **#2: TDD is just about writing tests** | TDD is more than testing — it's a **design methodology** that drives development |
| **#3: TDD is only for certain projects / languages** | TDD can be applied to **almost any project** — any size, complexity, or technology |

## PRO TIPS
- **3 myths** — small but high-frequency MCQ topic.
- **A4 Sheet:** 3 myths + realities.

---

# SLIDES 38-39
*Quiz + Thank You slides. No content.*

---

# 🎯 EXTRA EXAMPLES (Beyond Slides)

### Example A — Simple (Calculator)
**Step 1 — RED:** Write a test that fails.
```python
def test_multiply():
    assert multiply(2, 3) == 6  # ❌ multiply() doesn't exist yet
```
**Step 2 — GREEN:** Write minimum code.
```python
def multiply(a, b):
    return a * b   # ✅ test passes
```
**Step 3 — REFACTOR:** Code is already clean. No changes needed.

---

### Example B — Complex (Banking with mocks)
**Goal:** Test `TransferService.transfer(from_acc, to_acc, amount)`.
**Dependencies:** `AccountRepo` (DB), `TransactionLogger`.

**Without Mocks:** Test would hit real DB → slow, fragile, needs DB setup.
**With Mocks:**
- Create mock `AccountRepo` (returns fake account balance = $1000).
- Create mock `TransactionLogger`.
- Inject into `TransferService`.
- Call `transfer("A", "B", 500)`.
- Assert: mock balance updated, mock logger was called once with correct args.
**Outcome:** Test runs in milliseconds, no DB needed.

**Applies SOLID:**
- **S (SRP):** TransferService only transfers (doesn't log directly).
- **D (DIP):** Depends on `AccountRepo` interface, not concrete DB.

---

# 📊 MASTER COMPARISON — TDD vs Traditional Testing (Full Table)

| Dimension | TDD | Traditional |
|-----------|------|--------------|
| Order | Test first → then code | Code first → then test |
| Who writes tests | Developer | QA Tester |
| Test size | Small, incremental | Comprehensive, large |
| Feedback | Immediate | Delayed |
| Bug detection | Early | Late |
| Cycle | Red-Green-Refactor | Code → Test phase |

---

# 📝 MCQ PRACTICE — LECTURE 10

---

### Q1. Who popularized TDD in the late 1990s?
A) Joseph Juran
B) **Kent Beck** ✅
C) Philip Crosby
D) Robert C. Martin

**Answer: B (Slide 4)**

---

### Q2. The 3 phases of TDD cycle are:
A) Plan, Execute, Review
B) **Red, Green, Refactor** ✅
C) Test, Build, Deploy
D) Write, Test, Document

**Answer: B (Slide 9)**

---

### Q3. In the Red phase of TDD, the goal is to:
A) Make the test pass
B) **Write a test that fails** ✅
C) Refactor code
D) Write production code

**Answer: B (Slide 10)**

---

### Q4. The 'S' in SOLID stands for:
A) Sequence Pattern
B) Subclass Substitution
C) **Single Responsibility Principle** ✅
D) Static Method Principle

**Answer: C (Slide 20)**

---

### Q5. Which SOLID principle states "subclasses should be substitutable for their base classes"?
A) Single Responsibility
B) Open/Closed
C) **Liskov Substitution** ✅
D) Dependency Inversion

**Answer: C (Slide 25)**

---

### Q6. The book "Test-Driven Development: By Example" was published in:
A) 1995
B) 2000
C) **2002** ✅
D) 2005

**Answer: C (Slide 4)**

---

### Q7. In TDD, when should you write production code?
A) Before any tests
B) **Only when there's a failing test** ✅
C) After all features are designed
D) Only at the end of the sprint

**Answer: B (Slide 14, Rule #1)**

---

### Q8. Mocks in TDD are used primarily to:
A) Replace the entire system
B) **Isolate the System Under Test from its dependencies** ✅
C) Speed up production code
D) Replace the database permanently

**Answer: B (Slide 32)**

---

### Q9. The Open/Closed Principle states that software entities should be:
A) Always open and editable
B) Always closed and unchangeable
C) **Open for extension, closed for modification** ✅
D) Open for testing, closed for refactoring

**Answer: C (Slide 23)**

---

### Q10. Which statement about TDD myths is TRUE?
A) TDD slows down development long-term
B) TDD only works for specific languages
C) TDD is just about writing tests
D) **TDD is a design methodology, not just testing** ✅

**Answer: D (Slide 37)**

---

# 📌 LECTURE 10 — A4 REFERENCE SHEET MINI-SECTION

```
TEST-DRIVEN DEVELOPMENT (TDD)
  Definition: Write test FIRST → write minimal code to pass → refactor
  Origin: Kent Beck, late 1990s, Extreme Programming (XP)
  Book: "Test-Driven Development: By Example" (2002)

TDD in AGILE:
  Short feedback loops, Continuous Integration, Customer collaboration
  Used in Scrum & XP

TDD vs TRADITIONAL (6 dimensions):
  Approach: Tests BEFORE code  vs  Tests AFTER code
  Focus: Small incremental    vs  Comprehensive
  Creator: Developer          vs  QA Tester
  Coverage: High + critical   vs  Varies
  Feedback: Immediate         vs  Delayed
  Bug Detection: Early        vs  Late

5-STEP TDD PROCESS:
  1. Read & understand requirements
  2. Write a failing test
  3. Write minimum code to pass
  4. Refactor (clean up)
  5. Repeat

RED-GREEN-REFACTOR CYCLE:
  RED      = Write a failing test (code doesn't exist yet)
  GREEN    = Write minimum code to pass ("Get it working first")
  REFACTOR = Clean up code without changing behavior ("Make it nice")

3 RULES OF TDD:
  #1 No code without a test
  #2 No more test than needed (write just enough to fail)
  #3 No more code than needed (write just enough to pass)

SOLID PRINCIPLES (S-O-L-I-D):
  S = Single Responsibility    → One reason to change
  O = Open/Closed              → Open to extend, closed to modify
  L = Liskov Substitution      → Subclasses must be replaceable
  I = Interface Segregation    → Many small interfaces > one fat one
  D = Dependency Inversion     → Depend on abstractions, not concrete

MOCKS IN TDD:
  Purpose: Isolate System Under Test (SUT) from real dependencies
  4 reasons: Test one unit, Avoid slow deps, Simulate cases, Verify interactions

6 BENEFITS (Q-I-D-D-C-D):
  Quality↑, Immediate feedback, Better Design,
  Documentation, Confidence to refactor, Debugging

6 CHALLENGES (L-S-M-U-O-M):
  Learning curve, Slowdown initially, Maintenance,
  UI/legacy hard, Over-testing, Mindset change

TDD IMPACT ON DEVELOPERS:
  1. Reverses workflow (test → code)
  2. Forces small testable units
  3. Tests drive design
  4. Short-term slow, long-term fast
  5. Cultural challenge (team adoption)

3 MYTHS:
  #1: Slows development → Reality: Faster long-term
  #2: Just testing → Reality: Design methodology
  #3: Only for some projects → Reality: Any project/language
```

---

# ✅ LECTURE 10 — DONE

**Top 4 exam-likely essay questions for this lecture:**
1. **"Explain the Red-Green-Refactor cycle of TDD."**
2. **"Compare TDD vs Traditional Testing."**
3. **"Explain the SOLID Principles and how TDD relates to them."**
4. **"Why use mocks in TDD?"**

Reply **"done"** to continue to **Lecture 11** (the final one).
