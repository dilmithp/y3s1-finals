# LECTURE 2 — SPECIFICATION BASED TEST CASE DESIGN TECHNIQUES
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **⚠️ IMPORTANT NOTE FOR THIS LECTURE**
> Lecture 2 is mostly **conceptual + practical** with ONE formula (Test Coverage %). The big metric formulas (CC, CFS, WCC) appear later in Lectures 4, 5, and 7.
>
> Focus for this lecture:
> - 3 techniques: **Equivalence Partitioning, Boundary Value Analysis, Decision Table**
> - Each one can appear as an essay question with a small calculation/worked example.
> - Heavy MCQ targets: definitions, "what is Black Box?", "how many rules?", "what is mutually exclusive action?".

---

# SLIDE 1 — Title Slide
"Lecture 2 – Specification Based Test Case Design Techniques." Skip.

---

# SLIDE 2 — Introduction to Specification Based Testing

## 1. Plain English Explanation
Specification Based Testing means we test the software based on **what it should do** (according to the spec), **not** how it does it internally. We don't look at the code — we just check the inputs and outputs.

## 2. Theory (Exactly as in slides)
**Key Characteristics:**
- Focuses on **what** the system should do (not how)
- Independent of internal structure (**Black Box Testing / Behaviour Based Testing**)
- Uses **functional requirements** as a reference

## 3. Comparison Table — Specification Based vs Code Based

| Feature | Specification Based (Black Box) | Code Based (White Box) |
|---------|----------------------------------|-------------------------|
| Focus | What the system should do | How the system does it |
| Sees internal code? | ❌ No | ✅ Yes |
| Based on | Functional requirements | Source code structure |
| Other names | Black Box Testing, Behaviour Based Testing | White Box Testing, Structural Testing |
| Tester needs coding skills? | No | Yes |

## 4. Real-World Application
When you hand a banking app to a non-developer tester, they only know "I should be able to log in with my username/password" — they don't read the Java source. That's Black Box / Specification Based Testing.

## 5. PRO TIPS
- **Three synonyms to memorize:** Specification Based = Black Box = Behaviour Based.
- **Common MCQ trap:** Don't confuse Black Box (Spec) with Static testing. They're different concepts.
- **A4 Sheet:** *Spec Based = Black Box = Behaviour Based → based on WHAT (not HOW) → uses functional requirements.*

## Quick Recap
- Tests **what**, not **how**.
- Three names for it: Spec Based / Black Box / Behaviour Based.
- Based on functional requirements.

---

# SLIDE 3 — Why Use Specification-Based Testing?

## 1. Plain English Explanation
Four reasons this approach is valuable.

## 2. Theory (Exactly as in slides)
- Ensures correctness
- Covers diverse inputs and outputs
- Helps catch missing or unclear requirements early
- Doesn't require coding knowledge

## 3. Comparison Table — Four Benefits

| # | Benefit | Why it matters |
|---|---------|----------------|
| 1 | Ensures correctness | Confirms the system behaves as specified |
| 2 | Covers diverse inputs/outputs | Finds bugs across many input scenarios |
| 3 | Catches missing/unclear requirements early | Spec gaps surface during test design |
| 4 | No coding knowledge required | Business analysts, QA teams, end users can write tests |

## 4. PRO TIPS
- **Memory trick: "C-D-C-N"** → **C**orrectness, **D**iverse inputs, **C**atches gaps, **N**o coding needed.
- **A4 Sheet:** Four bullets — short list, easy 4 marks.

## Quick Recap
- 4 benefits to memorize.
- The "no coding needed" point is the most-tested distinguishing feature vs White Box.

---

# SLIDE 4 — Types of Specification Based Test Case Design Techniques

## 1. Plain English Explanation
There are **3 main techniques** under this umbrella. You will be tested on each.

## 2. Theory (Exactly as in slides)
1. Equivalence Partitioning
2. Boundary Value Analysis
3. Decision Table

## 3. Comparison Table — The 3 Techniques at a Glance

| # | Technique | Best Used For | Output |
|---|-----------|----------------|---------|
| 1 | **Equivalence Partitioning (EP)** | Grouping inputs that behave the same | One test per partition |
| 2 | **Boundary Value Analysis (BVA)** | Testing values at the edges of partitions | Tests at min, max, ±1 |
| 3 | **Decision Table (DT)** | Complex business rules with multiple inputs | Tests for every combination of conditions |

## 4. PRO TIPS
- **Memory trick: "E-B-D"** → **E**quivalence, **B**oundary, **D**ecision.
- These are also called the "three pillars" of black-box test design.
- **A4 Sheet:** A 3-row table like the one above — instant recall.

## Quick Recap
- 3 techniques: EP, BVA, DT.
- EP groups inputs; BVA tests edges; DT covers combinations of rules.

---

# SLIDES 5 & 6 — Equivalence Partitioning (Definition + Assumptions)

## 1. Plain English Explanation
Instead of testing every single input, **group similar inputs together** and test only **one value from each group** — because the system should treat all values in the same group the same way.

## 2. Theory (Exactly as in slides)
- Divide inputs into **groups that are expected to behave the same way**.
- Reduces the number of test cases while ensuring sufficient coverage.
- Example: An age-based system that allows users aged 18–60:
  - Invalid Partition: Age < 18
  - Valid Partition: Age 18–60
  - Invalid Partition: Age > 60

**Assumptions of EP:**
- The system will handle all the test input variations within a partition in the same way.
- If one input passes, all others in the same partition will also pass.
- If one input fails, all others in the same partition will also fail.

## 3. Comparison Table — Valid vs Invalid Partition

| Partition Type | Definition | Example (age 18–60 rule) |
|----------------|------------|---------------------------|
| **Valid Equivalence Partition (VP)** | Values the system should **accept** | Age 18 to 60 |
| **Invalid Equivalence Partition (IP)** | Values the system should **reject** | Age < 18, OR Age > 60 |

## 4. PRO TIPS
- **Memory trick:** EP = "Equal-treated Partitions."
- **Common exam mistake:** Listing 5 partitions when only 3 exist. Always check: how many distinct *behaviours* does the spec produce?
- **A4 Sheet:** *EP → 1 test per partition → covers Valid + Invalid groups → assumes uniform behaviour inside each group.*

## Quick Recap
- Group inputs that should behave the same.
- Pick **one** test value from each group.
- 2 types of partitions: **Valid** and **Invalid**.

---

# SLIDES 7 & 8 — Gym Example (Why We Need EP)

## 1. Plain English Explanation
Fitness 1st gym allows ages 16 to 60. If you tested every age from 0 to 100, that's 100 combinations. Impossible. So we use EP to reduce that to just 3 tests.

## 2. Theory (From the slides)
- Less than 16 → 16 combinations (0 to 15)
- 16 to 60 → 45 combinations
- Greater than 60 → 40 combinations (assuming up to 100)
- **Total: 100 combinations** — too many to test individually.

## 3. PRO TIPS
- **Exam tip:** This is the classic exam scenario. Memorize the gym example.
- **A4 Sheet:** *Without EP → 100 tests. With EP → 3 tests.*

## Quick Recap
- EP solves the "too many combinations" problem.
- Reduces 100 → 3 tests for the gym scenario.

---

# SLIDES 9 & 10 — How to Do Equivalence Partitioning

## 1. Plain English Explanation
Step-by-step: identify which inputs the system should **accept** (Valid Partition) and which inputs it should **reject** (Invalid Partition). Then pick one test value from each.

## 2. Theory (Exactly as in slides)
- **Valid Equivalence Partition** = values the component or system should accept.
- **Invalid Equivalence Partition** = values that should be rejected.

**Visual from slide 10:**
```
   Invalid Partition (IP)   |   Valid Partition (VP)   |   Invalid Partition (IP)
                          15 | 16 ------------------ 60 | 61
```

## 3. PRO TIPS
- Draw this number line in your exam answer — examiners love visual proof.
- **A4 Sheet:** Always sketch the line: IP | VP | IP with the boundary numbers labelled.

---

# SLIDES 11, 12, 13 — Sub-Partitions Example

## 1. Plain English Explanation
A partition can have **sub-partitions** if extra rules apply inside it. Example: ages 16–20 need age-proof, ages 21–54 don't, ages 55–60 need age-proof again. So the Valid Partition splits into VP1, VP2, VP3.

## 2. Theory (From slides)
With the new requirement (ages 16–20 and 55–60 need proof of age):

```
IP    | VP1   | VP2   | VP3   | IP
   15 | 16-20 | 21-54 | 55-60 | 61+
```

## 3. Comparison Table — Sub-Partitions

| Sub-Partition | Range | Behavior |
|---------------|-------|----------|
| VP1 | 16–20 | Valid, **must attach age proof** |
| VP2 | 21–54 | Valid, no proof needed |
| VP3 | 55–60 | Valid, **must attach age proof** |

## 4. Test Conditions (Slide 13)
| # | Test Input | Partition |
|---|------------|-----------|
| 1 | Enter Age 5 | Invalid (< 16) |
| 2 | Enter Age 18 | VP1 (proof needed) |
| 3 | Enter Age 30 | VP2 (no proof) |
| 4 | Enter Age 58 | VP3 (proof needed) |
| 5 | Enter Age 65 | Invalid (> 60) |

## 5. PRO TIPS
- **Exam trap:** Don't write only 3 partitions when sub-partitions exist. **Count distinct behaviours, not just ranges.**
- **A4 Sheet:** Note: "Each new behaviour rule = a new partition."

## Quick Recap
- Sub-partitions appear when extra rules change behaviour inside a valid range.
- Always test one representative value per sub-partition.

---

# SLIDE 14 — Rules + Coverage Formula

## 1. Plain English Explanation
EP follows two rules:
1. **Unique partitions** (no overlap between partition values).
2. **Complete coverage** (test all partitions).

And there is a simple coverage formula.

## 2. Theory (Exactly as in slides)
- **Unique Partitions** – Each test value belongs to only one partition (no overlap).
- **Complete Coverage** – Test cases should cover all identified partitions.
- **Coverage Measurement** – Calculated as:

## 3. LaTeX Formula

$$\text{Test Coverage} = \frac{\text{Partitions Tested}}{\text{Total Recognized Partitions}} \times 100\%$$

**Variable breakdown:**

| Symbol | Meaning |
|--------|---------|
| Partitions Tested | Number of partitions for which at least one test case exists |
| Total Recognized Partitions | Total number of partitions identified from the spec |
| × 100% | Converts ratio to percentage |

## 4. Worked Example

> If your spec has **5 partitions** (1 invalid below, 3 valid sub-partitions, 1 invalid above) and you test **4 of them**:
> $$\text{Test Coverage} = \frac{4}{5} \times 100\% = 80\%$$

## 5. PRO TIPS
- **A4 Sheet:** Write the formula in LaTeX form exactly: $\text{Test Coverage} = \frac{\text{Partitions Tested}}{\text{Total Recognized Partitions}} \times 100\%$
- **Common error:** Counting test cases instead of partitions in the numerator. **Count partitions, not test cases.**
- For full marks: always show formula → substitution → final answer with `%` sign.

## Quick Recap
- 2 rules: Unique partitions, Complete coverage.
- 1 formula: tested / total × 100%.

---

# SLIDE 15 — Drawbacks of Equivalence Partitioning

## 1. Plain English Explanation
EP isn't perfect. It has 3 main weaknesses.

## 2. Theory (Exactly as in slides)
- Depends on **correct partitioning** (if you partition wrong, your tests are wrong).
- Limited to **stated requirements** (catches only what's in the spec).
- No insight into **code implementation**.

## 3. Comparison Table — EP Drawbacks Explained

| # | Drawback | Why it's a problem |
|---|----------|---------------------|
| 1 | Depends on correct partitioning | If tester misidentifies groups, bugs hide |
| 2 | Limited to stated requirements | Hidden behaviours in undocumented rules go untested |
| 3 | No insight into code implementation | EP can't find code-level bugs (uninitialized variables, dead code, etc.) |

## 4. PRO TIPS
- **A4 Sheet:** *EP drawbacks: wrong partitions, only stated reqs, no code insight.*

## Quick Recap
- 3 drawbacks: bad partitioning, spec-only, no code visibility.

---

# SLIDES 16 & 17 — Equivalence Partitioning Exercise (Order Pizza)

## Problem from slides:
> Order Pizza textbox:
> - Pizza values **1–10** valid → success message
> - Less than 1 → error: "Please enter a valid count"
> - Greater than 10 → error: "Only 10 Pizzas can be ordered at a time"

## Slide Answer:
| Partition | Type | Sample Test Value |
|-----------|------|--------------------|
| Less than 1 | Invalid | **Enter Pizza Value = -1** |
| 1 to 10 | Valid | **Enter Pizza Value = 5** |
| Greater than 10 | Invalid | **Enter Pizza Value = 15** |

**Total: 3 test cases cover all 3 partitions → 100% partition coverage.**

---

# 🎯 EXTRA EQUIVALENCE PARTITIONING EXAMPLES (Beyond Slides)

### Example A — Simple (Beginner)
**Spec:** A movie ticket booking system allows the user to buy **1–8 tickets** per transaction.

**Partitions:**

| Partition | Range | Type | Test Value |
|-----------|-------|------|------------|
| Below valid | < 1 | Invalid | 0 |
| Valid | 1–8 | Valid | 4 |
| Above valid | > 8 | Invalid | 15 |

**Coverage:** 3 tested / 3 total = **100%**.

---

### Example B — Complex (with Sub-Partitions)
**Spec:** A car insurance system:
- Drivers under **18** → rejected
- Drivers **18–24** → "Young driver" surcharge applied
- Drivers **25–65** → Standard premium
- Drivers **66–75** → "Senior" surcharge
- Drivers **above 75** → rejected

**Partitions:**

| # | Partition | Range | Type | Test Value |
|---|-----------|-------|------|------------|
| 1 | Below valid | < 18 | Invalid | 16 |
| 2 | VP1 — young | 18–24 | Valid | 20 |
| 3 | VP2 — standard | 25–65 | Valid | 40 |
| 4 | VP3 — senior | 66–75 | Valid | 70 |
| 5 | Above valid | > 75 | Invalid | 80 |

**Coverage:** 5/5 = **100%**.

**If only 3 tests were run (16, 40, 80): Coverage = 3/5 × 100% = 60%.**

---

## PRO TIPS — EQUIVALENCE PARTITIONING SUMMARY
- **Rule of thumb:** count distinct behaviours in the spec → that's your partition count.
- **Watch for the trap:** "valid" can sometimes contain multiple sub-partitions.
- **Always include the formula** in essay answers, even if not explicitly asked.

---

# SLIDE 18 — Boundary Value Analysis (Definition)

## 1. Plain English Explanation
After EP groups inputs, **BVA tests the edges** of those groups. Why? Because bugs often hide at the boundaries — programmers commonly write `<` when they meant `<=`, etc.

## 2. Theory (Exactly as in slides)
- A software testing technique in which tests are designed to include **representatives of boundary values in a range**.
- An extension of equivalence partitioning.
- Testing the **boundaries of partitions**.
- Usable only when the partition is **ordered, consisting of numeric or sequential data**.
- The **minimum and maximum values** of a partition are its boundary values.

## 3. PRO TIPS
- **Memory trick:** BVA = "Bugs love edges."
- **A4 Sheet:** *BVA = extension of EP → test boundaries (min, max, ±1) → only works for ordered/numeric data.*

## Quick Recap
- BVA tests the edges of partitions.
- Works only on ordered/numeric/sequential data.
- It is an **extension** of EP, not a replacement.

---

# SLIDE 19 — Why BVA?

## 1. Plain English Explanation
EP alone is not enough — bugs near partition boundaries slip through. BVA is specifically designed to catch them.

## 2. Theory (Exactly as in slides)
- High chances of defects **at the boundaries** of a partition.
- Equivalence partitioning alone is **not sufficient** to catch such defects.
- Boundary Value Analysis was designed to **detect anomalies at the boundaries**.

## Quick Recap
- EP misses edge bugs.
- BVA catches them.

---

# SLIDES 20–22 — How to Do BVA (3-Step Approach)

## 1. Plain English Explanation
For each valid partition, take **3 values per boundary**: the boundary itself, one below, one above. So for a range 16–60, you get **6 BVA test values** (15, 16, 17, 59, 60, 61).

## 2. Theory (Exactly as in slides)
**3-step approach to identify boundaries:**
1. Identify the **exact boundary value** of the partition class → **16 and 60**
2. Get the boundary value which is **one less** than the exact boundary → **15 and 59**
3. Get the boundary value which is **one more** than the exact boundary → **17 and 61**

**Visual from slide 22:**
```
            ────────────●────────●────────────●────────●─────────
                       15  16  17           59  60  61
                       │  ↑   │            │   ↑   │
                       │  exact            │  exact │
                       │  boundary         │  boundary│
                       one less / more on each side
```

## 3. Comparison Table — BVA Values for Range 16–60

| Value | Type | Reason |
|-------|------|--------|
| 15 | Invalid Boundary | One less than min |
| **16** | **Valid Boundary** | Exact lower boundary |
| 17 | Valid Boundary | One more than min |
| 59 | Valid Boundary | One less than max |
| **60** | **Valid Boundary** | Exact upper boundary |
| 61 | Invalid Boundary | One more than max |

## 4. PRO TIPS
- **The "3-value per boundary" rule:** boundary, boundary−1, boundary+1.
- **Memory trick:** "Edge ±1 always" → that's 3 values per edge × 2 edges = **6 BVA tests for a single range**.
- **A4 Sheet:** *BVA per boundary = (B−1, B, B+1) → total 6 values for one range.*

## Quick Recap
- 3 values per boundary.
- For a single range, **6 BVA tests** total.

---

# SLIDE 23 — Valid vs Invalid Boundaries

## 2. Theory (Exactly as in slides)
- **Valid Boundary Conditions** → Age 16, 17, 59, 60
- **Invalid Boundary Conditions** → Age 15, 61
- Valid boundary conditions fall under valid partition class.
- Invalid boundary conditions fall under invalid partition class.

## 3. Comparison Table

| Value | Inside Valid Range (16–60)? | Classification |
|-------|------------------------------|----------------|
| 15 | No | **Invalid Boundary** |
| 16 | Yes | Valid Boundary |
| 17 | Yes | Valid Boundary |
| 59 | Yes | Valid Boundary |
| 60 | Yes | Valid Boundary |
| 61 | No | **Invalid Boundary** |

## PRO TIPS
- **Memory trick:** Of 6 boundary tests, **4 are valid, 2 are invalid** (the ±1 outside).

---

# SLIDES 24 & 25 — BVA + EP Combined

## 1. Plain English Explanation
For complete coverage, combine **EP** (one value from each partition's middle) **+ BVA** (six edge values). Together they form a full test set.

## 2. Theory (From slides)
For the gym example (range 16–60):
- **EP test values:** 5, 30, 65 (one per partition)
- **BVA test values:** 15, 16, 17, 59, 60, 61
- **All combined test conditions:** **5, 15, 16, 17, 30, 59, 60, 61, 65** (9 values total)

## 3. Comparison Table — Combined Approach

| Value | Source | Why Included |
|-------|--------|--------------|
| 5 | EP | Mid-point of invalid partition (< 16) |
| 15 | BVA | One below lower valid boundary |
| 16 | BVA | Lower valid boundary |
| 17 | BVA | One above lower valid boundary |
| 30 | EP | Mid-point of valid partition |
| 59 | BVA | One below upper valid boundary |
| 60 | BVA | Upper valid boundary |
| 61 | BVA | One above upper valid boundary |
| 65 | EP | Mid-point of invalid partition (> 60) |

## 4. PRO TIPS
- **Memory trick:** EP + BVA = **3 + 6 = 9 test values** for a single 2-bounded range.
- This is the strongest possible black-box coverage for ranges.
- **A4 Sheet:** *"Best coverage: EP (mid of each partition) + BVA (±1 of each boundary)."*

---

# SLIDE 26 — Drawbacks of BVA

## 2. Theory (Exactly as in slides)
- BVA + EP **assume the app won't allow any other characters/values** — but real apps may not enforce this.
- BVA cannot handle situations where the **decision depends on more than one input value** (e.g., gym form with separate Male/Female age limits).

## 3. PRO TIPS
- **A4 Sheet:** BVA drawbacks → (1) assumes input filter exists, (2) fails with multi-input dependencies (use Decision Table for that).
- **Common essay answer:** "When multiple input fields interact, BVA fails → use Decision Table instead."

## Quick Recap
- 2 drawbacks of BVA.
- For multi-input rules → switch to Decision Table.

---

# SLIDES 27 & 28 — BVA Exercise (Order Pizza)

## Problem from slides:
Same Order Pizza spec (1–10 valid).

## Slide Answer:
| Value | Type |
|-------|------|
| **0** | Invalid (one below min) |
| **1** | Valid (min) |
| **2** | Valid (one above min) |
| **9** | Valid (one below max) |
| **10** | Valid (max) |
| **11** | Invalid (one above max) |

**Total: 6 BVA test values for a single 1–10 range.**

---

# 🎯 EXTRA BOUNDARY VALUE ANALYSIS EXAMPLES (Beyond Slides)

### Example A — Simple
**Spec:** A library system allows borrowing **1 to 5 books** at a time.

| Value | Type |
|-------|------|
| 0 | Invalid (B−1) |
| 1 | Valid (B) |
| 2 | Valid (B+1) |
| 4 | Valid (B−1) |
| 5 | Valid (B) |
| 6 | Invalid (B+1) |

**6 tests → covers both edges + ±1.**

---

### Example B — Complex (with Combined EP + BVA)
**Spec:** A flight booking system allows **passenger age between 2 and 99**.

**Step 1 — EP partitions:**
- Invalid: < 2
- Valid: 2–99
- Invalid: > 99

**Step 2 — EP test values:** 0 (for < 2), 50 (for valid mid), 110 (for > 99) → 3 values.

**Step 3 — BVA test values:** 1, 2, 3, 98, 99, 100 → 6 values.

**Step 4 — Combined (9 values):** 0, 1, 2, 3, 50, 98, 99, 100, 110.

**Step 5 — Coverage:**
$$\text{Coverage} = \frac{3}{3} \times 100\% = 100\%$$

---

## PRO TIPS — BVA SUMMARY
- **Pattern:** "B−1, B, B+1" for each boundary. Two boundaries = 6 values.
- **Combined approach (EP + BVA):** 9 values for a single 2-bounded range.
- **Common trap:** Forgetting the upper boundary's outside value (e.g., 61 in gym example).

---

# SLIDE 29 — Decision Table (Definition)

## 1. Plain English Explanation
When the system's behaviour depends on **combinations of multiple inputs**, EP and BVA aren't enough. **Decision Tables** systematically list every combination of true/false conditions and the action that should happen.

## 2. Theory (Exactly as in slides)
- Software testing technique in which tests are **focused on business logic / business rules**.
- A decision table is a good way to deal with **combinations of inputs**.
- Provides a **systematic way of stating complex business rules** (useful for developers + testers).
- Helps testers explore effects of combinations of different inputs and software states.

## 3. PRO TIPS
- **Memory trick:** DT = "Decisions Tabled."
- Use whenever you see "if X AND Y" or "if X OR Y" in the spec.
- **A4 Sheet:** *DT → for combinations of inputs / business rules → systematic.*

## Quick Recap
- DT is for combinations + business logic.
- EP/BVA handle single inputs; DT handles multi-input rules.

---

# SLIDES 30 to 33 — How to Build a Decision Table (Steps 1–3)

## 1. Plain English Explanation
Building a Decision Table is a **5-step process**: pick the function, list conditions, calculate combinations, fill outcomes, write test cases.

## 2. Theory (Steps 1–3 from slides)

**Step 1.** Identify a suitable function/subsystem that reacts to combinations of inputs. Avoid systems with too many inputs (combinations explode).

**Step 2.** Identify the conditions.
- Example: Gym membership app.
  - Condition 1: Enter total amount
  - Condition 2: Enter number of months

**Step 3.** Identify all combinations of True and False.

## 3. LaTeX Formula for Total Combinations

$$\text{Total Combinations} = 2^{\text{Number of Conditions}}$$

**Variable breakdown:**

| Symbol | Meaning |
|--------|---------|
| 2 | Each condition has 2 states (True or False) |
| Number of Conditions | How many independent conditions are in the spec |
| Total Combinations | The number of columns (rules) your decision table needs |

## 4. Worked Examples for the Formula

| # of Conditions | Total Combinations |
|-----------------|---------------------|
| 1 | 2¹ = 2 |
| 2 | 2² = 4 |
| 3 | 2³ = 8 |
| 4 | 2⁴ = 16 |
| 5 | 2⁵ = 32 |

## 5. PRO TIPS
- **A4 Sheet:** *Total Rules = 2^(# of conditions).*
- **High-frequency MCQ:** "How many rules in a 3-condition decision table?" → 2³ = **8**.

---

# SLIDES 34 to 36 — Decision Table (Steps 4 — Fill the Outcomes)

## 1. Plain English Explanation
For each column (rule), determine which action should happen. Add rows for actions.

## 2. Theory (Slide 34 — Gym example)

| Conditions | Rule 1 | Rule 2 | Rule 3 | Rule 4 |
|------------|--------|--------|--------|--------|
| Enter total amount | T | T | F | F |
| Enter number of months | T | F | T | F |
| **Actions / Outcomes** | | | | |
| Calculate how many months for membership | Y | Y | | |
| Total cost of membership | Y | | Y | |

Then (slide 35–36) we **add an error message action** for Rule 4 (where the user enters nothing):

| Conditions | Rule 1 | Rule 2 | Rule 3 | Rule 4 |
|------------|--------|--------|--------|--------|
| Enter total amount | T | T | F | F |
| Enter number of months | T | F | T | F |
| Calculate how many months | Y | Y | | |
| Total cost of membership | Y | | Y | |
| Error message | | | | Y |

## 3. PRO TIPS
- **A4 Sheet:** Don't forget — even combinations **not stated in the spec** must be added (usually as error/edge cases).

---

# SLIDES 37–40 — Mutually Exclusive Actions

## 1. Plain English Explanation
A decision table is "mutually exclusive" if **only one action happens per rule**. The slide modifies the gym example so each rule has exactly **one Yes**, achieving mutual exclusivity.

## 2. Theory (Slides 38, 40)

**Modified table:**

| Conditions | Rule 1 | Rule 2 | Rule 3 | Rule 4 |
|------------|--------|--------|--------|--------|
| Enter total amount | T | T | F | F |
| Enter number of months | T | F | T | F |
| Calculate # of months | | Y | | |
| Total cost of membership | | | Y | |
| Error message | Y | | | Y |

Now: **only one Y per column.** That is *mutually exclusive action*.

## 3. Comparison Table — Mutually Exclusive vs Non-Exclusive

| Property | Non-Mutually Exclusive | Mutually Exclusive |
|----------|-------------------------|--------------------|
| Y per rule | Multiple possible | Exactly 1 |
| Behavior | Multiple actions trigger | One action triggers |
| Use case | When system can do many things at once | When only one outcome is allowed |

## 4. PRO TIPS
- **Definition to memorize:** *"Mutually exclusive action: only one action occurs for each combination of conditions."*
- High MCQ likelihood: "What does mutually exclusive action mean?" → memorize verbatim.

---

# SLIDE 41 — Step 5: Write Test Cases

## 1. Plain English Explanation
Each rule (column) in the decision table becomes one test case.

## 2. PRO TIPS
- **Rule of thumb:** Number of test cases = number of rules.
- For 2 conditions → 4 test cases. For 3 conditions → 8.

---

# SLIDE 42 — Decision Table Exercise (Credit Card Discounts)

## Problem from slide:
- New customers: **15% discount** today
- Existing customer + loyalty card: **10% discount**
- Has coupon: **20% off** (and **coupon priority** — if new customer also has coupon, coupon overrides new-customer discount)

**Identify 3 conditions:**
1. Is the customer New?
2. Holds a loyalty card?
3. Has a coupon?

**Total rules = 2³ = 8.**

## ✅ FULL WORKED SOLUTION (Beyond the slide — slide leaves this open)

| Conditions | R1 | R2 | R3 | R4 | R5 | R6 | R7 | R8 |
|------------|----|----|----|----|----|----|----|----|
| New customer | T | T | T | T | F | F | F | F |
| Loyalty card | T | T | F | F | T | T | F | F |
| Coupon | T | F | T | F | T | F | T | F |
| **Actions** | | | | | | | | |
| 15% (new) discount | | Y | | Y | | | | |
| 10% (loyalty) discount | | | | | | Y | | |
| 20% (coupon) discount | Y | | Y | | Y | | Y | |
| No discount | | | | | | | | Y |

**Reasoning notes:**
- Coupon **always wins** when present (R1, R3, R5, R7).
- New customer **without** coupon gets 15% (R2, R4).
- Existing customer **with loyalty + no coupon** gets 10% (R6).
- Existing customer with no loyalty, no coupon (R8) → no discount.

**Note on R5 (New + Loyalty + Coupon):** The slide didn't say loyalty card is mutually exclusive with "new," so technically this combination exists. Coupon priority applies → 20%.

---

# 🎯 EXTRA DECISION TABLE EXAMPLES (Beyond Slides)

### Example A — Simple (2 conditions)
**Spec — ATM withdrawal:**
- Valid PIN AND sufficient balance → dispense cash
- Otherwise → show error

**Decision Table:**

| Conditions | R1 | R2 | R3 | R4 |
|------------|----|----|----|----|
| Valid PIN | T | T | F | F |
| Sufficient balance | T | F | T | F |
| **Actions** | | | | |
| Dispense cash | Y | | | |
| Show error | | Y | Y | Y |

**4 rules from 2² = 4. Mutually exclusive ✅.**

---

### Example B — Complex (3 conditions)
**Spec — Online order shipping calculator:**
- Premium member → free shipping
- Order > $100 → free shipping
- Otherwise → $5 shipping
- Express add-on selected → +$10 (regardless of free shipping)

**Conditions:**
1. Premium member?
2. Order > $100?
3. Express selected?

**Total = 2³ = 8 rules.**

| Conditions | R1 | R2 | R3 | R4 | R5 | R6 | R7 | R8 |
|------------|----|----|----|----|----|----|----|----|
| Premium | T | T | T | T | F | F | F | F |
| Order > $100 | T | T | F | F | T | T | F | F |
| Express | T | F | T | F | T | F | T | F |
| **Actions** | | | | | | | | |
| Free shipping | Y | Y | Y | Y | Y | Y | | |
| $5 shipping | | | | | | | Y | Y |
| +$10 express | Y | | Y | | Y | | Y | |

**Test cases:** 8 (one per rule).

---

## PRO TIPS — DECISION TABLE SUMMARY
- **Total rules formula:** $2^{\text{conditions}}$ — memorize.
- **Each rule = one test case.**
- **Mutually exclusive action** = one Y per rule.
- **Use DT when:** spec contains "if X AND/OR Y" combinations.
- **A4 Sheet:** Save space for one example 2-condition DT (4 rules).

---

# 📊 MASTER COMPARISON — THE 3 TECHNIQUES

| Feature | Equivalence Partitioning | Boundary Value Analysis | Decision Table |
|---------|---------------------------|-------------------------|-----------------|
| **What it tests** | Groups of similar inputs | Edge values of partitions | Combinations of inputs |
| **Best for** | Single ordered input | Single ordered numeric input | Multi-input business rules |
| **Test value count** | 1 per partition | 6 per range (B±1 × 2 boundaries) | $2^n$ (n = conditions) |
| **Key formula** | Coverage = tested/total ×100% | None (rule: B−1, B, B+1) | Rules = $2^n$ |
| **Limitation** | Can't catch edge bugs | Can't handle multi-input rules | Combinations explode for >5 conditions |
| **Memory trick** | "Equal-treated groups" | "Bugs love edges" | "Truth-table for behavior" |

---

# 📝 MCQ PRACTICE — LECTURE 2

---

### Q1. Specification-based testing is also known as:
A) White Box Testing
B) **Black Box / Behaviour Based Testing** ✅
C) Unit Testing
D) Regression Testing

**Answer: B (Slide 2)**

---

### Q2. The formula for test coverage in Equivalence Partitioning is:
A) (Total Recognized Partitions / Partitions Tested) × 100%
B) **(Partitions Tested / Total Recognized Partitions) × 100%** ✅
C) Partitions Tested × Total Recognized Partitions
D) 2^(Partitions Tested)

**Answer: B (Slide 14)**

---

### Q3. For a single valid range with two boundaries, how many BVA test values are required?
A) 2
B) 3
C) **6** ✅
D) 9

**Answer: C — three values per boundary × 2 boundaries = 6 (Slides 20–22)**

---

### Q4. The total number of rules in a Decision Table with 4 conditions is:
A) 4
B) 8
C) **16** ✅
D) 32

**Answer: C — 2⁴ = 16 (Slide 33)**

---

### Q5. Boundary Value Analysis is:
A) A replacement for Equivalence Partitioning
B) **An extension of Equivalence Partitioning** ✅
C) The same as Decision Table testing
D) White-box testing

**Answer: B (Slide 18)**

---

### Q6. Which technique is best when business decisions depend on multiple inputs?
A) Equivalence Partitioning
B) Boundary Value Analysis
C) **Decision Table** ✅
D) Static Testing

**Answer: C (Slide 29)**

---

### Q7. "Mutually exclusive action" in a Decision Table means:
A) Multiple actions occur per rule
B) **Only one action occurs per combination of conditions** ✅
C) No actions occur per rule
D) Conditions cancel each other out

**Answer: B (Slide 39)**

---

### Q8. For a partition range 20–50, which set is correct BVA test values?
A) 20, 35, 50
B) **19, 20, 21, 49, 50, 51** ✅
C) 0, 20, 50, 100
D) 20, 50

**Answer: B — three per boundary on each side (Slides 20–22)**

---

# 📌 LECTURE 2 — A4 REFERENCE SHEET MINI-SECTION

```
SPECIFICATION-BASED TESTING
  = Black Box = Behaviour Based
  - Tests WHAT (not HOW)
  - Based on functional requirements

3 TECHNIQUES (E-B-D):
  1. Equivalence Partitioning (EP)
  2. Boundary Value Analysis (BVA)
  3. Decision Table (DT)

EQUIVALENCE PARTITIONING:
  - 1 test per partition (Valid + Invalid)
  - Assume: same behaviour within partition
  - Formula:
    Coverage = (Partitions Tested / Total Partitions) × 100%
  - Drawbacks: wrong partitioning, spec-only, no code view

BOUNDARY VALUE ANALYSIS:
  - Extension of EP
  - 3 values per boundary: (B−1, B, B+1)
  - For range with 2 boundaries → 6 BVA values
  - Only numeric/ordered/sequential data
  - Drawbacks: assumes input filter, fails on multi-input

EP + BVA combined for full coverage:
  For range a..b: { mid_below, a−1, a, a+1, mid, b−1, b, b+1, mid_above }
  = 9 test values

DECISION TABLE:
  - For combinations of inputs / business rules
  - Total Rules = 2^(# conditions)
  - 5 Steps: function → conditions → combos → outcomes → test cases
  - Mutually exclusive action: only ONE Y per rule

EXAMPLES TO REMEMBER:
  Gym (16-60):
    EP → 5, 30, 65
    BVA → 15, 16, 17, 59, 60, 61
    Combined → 5, 15, 16, 17, 30, 59, 60, 61, 65

  Order Pizza (1-10):
    EP → -1, 5, 15
    BVA → 0, 1, 2, 9, 10, 11
```

---

# ✅ LECTURE 2 — DONE

Heavy on **practical examples**: gym membership, pizza order, credit card discounts. Expect at least one exam question that asks for an EP/BVA/DT worked solution.

Reply **"done"** to move to **Lecture 3 — Functional and Non-Functional Testing.**
