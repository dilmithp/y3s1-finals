# LECTURE 4A — CODE COVERAGE ANALYSIS
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **⚠️ MEGA-IMPORTANT LECTURE — METRIC CALCULATION**
> Lecture 4 has **TWO parts**: this one (Code Coverage Analysis) and **Cyclomatic Complexity** (separate guide).
>
> **Why this is critical:**
> - Contains **3 formulas** that may appear in exam: Statement Coverage, Decision Coverage, Path Coverage.
> - Path Coverage links to **Cyclomatic Complexity** (Lecture 4B).
> - High-frequency MCQ + essay topics.

---

# SLIDE 1 — Title Slide
"Lecture 4 — Code Coverage Analysis." Skip.

---

# SLIDE 2 — Code Coverage Methods (Overview)

## 1. Plain English Explanation
There are **5 main code coverage methods**. The exam usually tests Statement, Decision, and Path Coverage.

## 2. Theory (Exactly as in slides)
1. **Statement Coverage**
2. **Decision Coverage**
3. **Path Coverage**
4. **Condition Coverage**
5. **Multiple Condition Coverage**

## PRO TIPS
- **Memory trick — "S-D-P-C-M"** → Statement, Decision, Path, Condition, Multiple-Condition.
- The 3 most-tested ones: **Statement, Decision, Path**.

---

# SLIDES 3-7 — What is Code Coverage / Why It Matters

## 1. Plain English Explanation
Code coverage tells you **how much of your source code is actually being tested** by your tests. A high % means more code paths are exercised.

## 2. Theory (Exactly as in slides)
- Code coverage describes **how much program source code is covered by a testing plan**.
- Developers look at the number of **subroutines and lines of code** covered.
- Also known as **test coverage**.

**Code Coverage Analysis:**
- Provides reassurance that programs are **broadly tested** and relatively error-free.
- Mostly done to find the **precise areas NOT covered** by testing strategies.
- Tools: Microsoft Visual Studio, **JaCoCo, NUnit, Cobertura, CodeCover, pitest.org**.

**Uses of Code Coverage Analysis:**
- Helps measure **efficiency of test implementation**
- Offers a **quantitative measurement**
- Defines the **degree** to which source code has been tested

## 3. PRO TIPS
- **Memorize tools:** JaCoCo (Java), NUnit (.NET), Cobertura.
- **A4 Sheet:** *Code coverage = % of source code exercised by tests → quantitative.*

---

# SLIDES 8-13 — Method #1: Statement Coverage

## 1. Plain English Explanation
**Statement Coverage** = how many lines of code your tests actually executed (out of the total). Simplest coverage metric.

## 2. Theory (Exactly as in slides)
- Ensures **each statement of the code is executed at least once**.
- Measures **the number of lines executed**.
- Verifies what the written code is expected to do and not to do.
- **White-box testing** — evaluates internal code structure.
- Best performed by a **programmer**.

## 3. LaTeX Formula

$$\text{Statement Coverage} = \frac{\text{Number of executed statements}}{\text{Total number of statements}} \times 100\%$$

**Important counting rule (from Slide 10):**
> *All statements including the statement with a function name and statements with only braces ("{" "}") are counted in statement coverage.*

## 4. Worked Example (Slides 11–13)

**Code:**
```
read a;
read b;
if (a>b)
    print "A is greater than B";
else
    print "B is greater than A";
```

**Total statements = 6**

| Condition | Inputs | Statements executed | Count |
|-----------|--------|----------------------|-------|
| 1 | a=5, b=1 | read a, read b, if(a>b), print "A>B" | 4 |
| 2 | a=1, b=5 | else branch, print "B>A" | 2 |

**Calculation:**
$$\text{Statement Coverage} = \frac{4+2}{6} \times 100\% = \frac{6}{6} \times 100\% = \mathbf{100\%}$$

## 5. PRO TIPS
- **A4 Sheet:** *Statement Coverage = (executed stmts / total stmts) × 100%. Count braces and function names.*
- **Exam trap:** Don't forget to count the **function declaration line** and **standalone braces** as statements.

---

# SLIDES 15-20 — Method #2: Decision Coverage

## 1. Plain English Explanation
**Decision Coverage** = how many **True / False outcomes** of decision (if/while/case) statements your tests covered.

## 2. Theory (Exactly as in slides)
- Reports the **true or false outcomes** of each Boolean expression.
- Focuses on covering the most important combinations.

## 3. LaTeX Formula

$$\text{Decision Coverage} = \frac{\text{Number of decision outcomes exercised}}{\text{Total number of decision outcomes}} \times 100\%$$

> **Key rule:** Each `if`, `while`, `case` etc. has **2 outcomes** (True + False). So 1 decision = 2 possible outcomes.

## 4. Worked Example (Slides 17–19)

**Code:**
```
Read a;
If (a > 5)
    a = a * 3
print (a)
```

**1 decision** (`if (a>5)`) → **2 outcomes** (True + False) → **Total outcomes = 2**.

| Condition | Inputs | Outcome covered |
|-----------|--------|------------------|
| 1 | a=2 | FALSE outcome of `if(a>5)` |
| 2 | a=7 | TRUE outcome of `if(a>5)` |

**Calculation:**
$$\text{Decision Coverage} = \frac{1+1}{2} \times 100\% = \frac{2}{2} \times 100\% = \mathbf{100\%}$$

## 5. PRO TIPS
- **Rule:** Each decision contributes **2 outcomes** to the denominator (True + False).
- **A4 Sheet:** *Decision Coverage = (outcomes exercised / total outcomes) × 100%. Each `if` = 2 outcomes.*

---

# SLIDES 21-32 — Method #3: Path Coverage (The Big One)

## 1. Plain English Explanation
**Path Coverage** = how many **complete linearly independent paths** through the code your tests covered. Uses the **Control Flow Graph (CFG)** + **Cyclomatic Complexity**.

## 2. Theory (Exactly as in slides)
- A **path** = unique sequence of branches from function entry to exit.
- **Path coverage** = designing tests so all **linearly independent paths** are executed at least once.
- A **control flow graph** describes how control flows through the application.
- A **linearly independent path** = a path with **at least one new edge** in the CFG.
- **Cyclomatic Complexity** identifies the number of independent paths.

## 3. LaTeX Formulas

**Number of independent paths:**
$$V(G) = e - n + 2$$

Where:
- $e$ = number of edges
- $n$ = number of nodes

**Path Coverage:**
$$\text{Path Coverage} = \frac{\text{Number of linearly independent paths executed}}{\text{Total number of linearly independent paths}} \times 100\%$$

## 4. Path Coverage 5-Step Process (Slide 25)
1. **Draw the Control Flow Graph**
2. Identify the **total number of linearly independent paths** in the program
3. Identify linearly **independent paths executed by each test condition**
4. Identify the **number of paths covered by all test conditions**
5. **Calculate path coverage**

## 5. Control Flow Graph Rules (Slide 26)

| # | Rule |
|---|------|
| 1 | Use ⊙ (circle with dot) for **start/stop** nodes |
| 2 | Use ● (filled dot) for **intermediary** nodes |
| 3 | Label **start, stop, decisions, true/false** paths |
| 4 | **Edges always indicate directions** (arrows) |
| 5 | Procedure nodes + decisions can be combined with start node |
| 6 | A **procedure node** represents one or more **non-decisional statements** |

## 6. Worked Example (Slides 27–31)

**Code:**
```
Demo(int a)
If (a > 5)
    a = a * 3
if (b > 8)
    b = b - 5
```

**CFG (from Slide 28):**
```
[1] Start, decision(if a>5)
      ├── True ──→ [2] Decision(if b>8)
      │              ├── True ──→ [3] a=a*3 (procedure)
      │              └── False ──→ [4] Stop
      └── False ──→ [4] Stop (b=b-5 not relevant, simplified)
```

**Test Paths (Slide 29):**
| Test | Inputs | Path executed |
|------|--------|---------------|
| 1 | a=4, b=6 | Path 1: 1 → 4 |
| 2 | a=6, b=6 | Path 2: 1 → 2 → 4 |

**Step 4 — paths covered by all tests = 2**
**Step 5 — Total linearly independent paths = 3** (from V(G))

**Calculation:**
$$\text{Path Coverage} = \frac{2}{3} \times 100\% = \mathbf{67\%}$$

## 7. PRO TIPS
- **Memory cue:** Statement = lines. Decision = T/F outcomes. Path = full routes from start to stop.
- **A4 Sheet:**
  - *V(G) = e − n + 2*
  - *Path Coverage = (paths executed / total paths) × 100%*
  - *5-step process: CFG → total paths → executed paths → coverage*

---

# SLIDE 33 — Method #4: Condition Coverage

## 1. Plain English Explanation
**Condition Coverage** = check if **each Boolean sub-expression** in a compound condition is tested for both True and False.

## 2. Theory (Exactly as in slides)
- Measures whether **each Boolean sub-expression** in a condition has been tested for **both True and False outcomes**.
- Ensures every individual condition inside a decision is exercised T and F at least once.

## 3. Example (from slide)
```python
if (A || B):
    print("Condition met")
```

**Condition coverage test cases:**

| Case | A | B | What's tested |
|------|---|---|----------------|
| 1 | True | False | Covers **A=True** |
| 2 | False | True | Covers **B=True** |

> But this does **NOT** check all combinations (i.e., it doesn't satisfy Multiple Condition Coverage).

## PRO TIPS
- **Distinguishing keyword:** Condition Coverage tests **each sub-expression individually** for T/F.
- **A4 Sheet:** *Condition Coverage = each sub-expression tested T+F. NOT all combinations.*

---

# SLIDES 34-35 — Method #5: Multiple Condition Coverage

## 1. Plain English Explanation
**Multiple Condition Coverage** = check **every possible combination** of True/False values of all sub-expressions. Strongest condition-based coverage.

## 2. Theory (Exactly as in slides)
- Checks the **coverage of ALL combinations** of conditions.
- **Total test cases = 2ⁿ** (where n = number of conditions).
- For 2 conditions → 2² = **4 test cases**.

## 3. LaTeX Formula

$$\text{Total Test Cases for MCC} = 2^n$$

Where $n$ = number of conditions.

## 4. Example (Slide 35)
```python
if (A || B):
    print("Condition met")
```

**Multiple Condition Coverage requires 2² = 4 test cases:**

| Case | A | B |
|------|---|---|
| 1 | False | False |
| 2 | False | True |
| 3 | True | False |
| 4 | True | True |

## 5. PRO TIPS
- **Difference vs Condition Coverage:** MCC tests **all combinations** (4 cases for 2 conditions), Condition Coverage only tests each sub-expression's T/F.
- **A4 Sheet:** *MCC = 2ⁿ test cases for n conditions. Tests every combination.*

## Quick Recap
- **Condition Coverage:** Each sub-expression T+F → can be 2 cases for `A || B`.
- **Multiple Condition Coverage:** All combinations → 4 cases for `A || B`.

---

# 📊 MASTER COMPARISON — 5 COVERAGE METHODS

| # | Method | What it Measures | Formula | Strength |
|---|--------|-------------------|---------|----------|
| 1 | **Statement** | Lines executed | (executed / total) × 100% | Weakest |
| 2 | **Decision** | T/F outcomes of decisions | (outcomes exercised / total) × 100% | Stronger |
| 3 | **Path** | Linearly independent paths | (paths exec / total paths) × 100% | Strong |
| 4 | **Condition** | Each sub-expression T+F | (sub-expr tested / total) × 100% | Stronger than Decision |
| 5 | **Multiple Condition** | All combinations of sub-expressions | 2ⁿ test cases needed | Strongest |

**Ordering of strength (weakest → strongest):**
**Statement < Decision < Condition < Multiple Condition**
*Path Coverage is strong but independent of the above.*

---

# 🎯 EXTRA WORKED EXAMPLE — All 3 Major Coverage Types

**Code:**
```java
1: read x;
2: read y;
3: if (x > 0)
4:     z = x + y;
5: else
6:     z = x - y;
7: print z;
```

**Test 1:** x=5, y=3 → executes lines {1, 2, 3, 4, 7} → 5 statements
**Test 2:** x=-1, y=3 → executes lines {1, 2, 3, 6, 7} → 5 statements

### Statement Coverage
- Total statements = 7
- Statements executed across both tests = {1,2,3,4,6,7} = 6 statements
- Coverage = 6/7 × 100% = **85.7%**

*Wait — line 5 (`else`) wasn't executed in either test count above. But the standalone `else` keyword IS counted. Re-count statements executed: T1 covers {1,2,3,4,7}=5, T2 covers {1,2,3,5,6,7}=6 → union = {1,2,3,4,5,6,7} = 7. So coverage = 7/7 = **100%**.*

### Decision Coverage
- 1 decision (`if x>0`) → 2 outcomes (T, F)
- T1 covers T-outcome, T2 covers F-outcome → both exercised
- Coverage = 2/2 × 100% = **100%**

### Path Coverage
- CFG has 2 paths: (start → if → true branch → end) and (start → if → false branch → end)
- Both paths executed → 2/2 = **100%**

---

# 📝 MCQ PRACTICE — LECTURE 4A (Code Coverage)

---

### Q1. Which formula is correct for Statement Coverage?
A) (Total Statements / Executed Statements) × 100%
B) **(Executed Statements / Total Statements) × 100%** ✅
C) Executed Statements + Total Statements
D) 2^(Total Statements)

**Answer: B (Slide 10)**

---

### Q2. Decision Coverage measures:
A) Number of lines of code executed
B) **True/False outcomes of Boolean expressions exercised** ✅
C) All linearly independent paths
D) All combinations of conditions

**Answer: B (Slide 15)**

---

### Q3. For 3 conditions in a compound expression, Multiple Condition Coverage requires:
A) 3 test cases
B) 6 test cases
C) **8 test cases (2³)** ✅
D) 9 test cases

**Answer: C (Slide 34, formula 2ⁿ)**

---

### Q4. Which coverage uses the formula V(G) = e − n + 2?
A) Statement Coverage
B) Decision Coverage
C) Condition Coverage
D) **Path Coverage** ✅

**Answer: D (Slide 23)**

---

### Q5. In a Control Flow Graph, the symbol ⊙ (circle with dot) represents:
A) An intermediary node
B) **Start or Stop node** ✅
C) A decision
D) A loop

**Answer: B (Slide 26)**

---

### Q6. The strongest of these coverage methods is:
A) Statement Coverage
B) Decision Coverage
C) Condition Coverage
D) **Multiple Condition Coverage** ✅

**Answer: D (covers all combinations of sub-expressions)**

---

### Q7. A linearly independent path is:
A) A path that visits every node twice
B) **A path with at least one new edge in the CFG** ✅
C) Only the path from start to end
D) The shortest path

**Answer: B (Slide 22)**

---

# 📌 LECTURE 4A — A4 REFERENCE SHEET MINI-SECTION

```
CODE COVERAGE — 5 METHODS (S-D-P-C-M):
  1. Statement Coverage      → lines executed
  2. Decision Coverage       → T/F of decisions
  3. Path Coverage           → independent paths
  4. Condition Coverage      → each sub-expression T+F
  5. Multiple Condition Cov  → all combinations (2^n)

FORMULAS:

  Statement Coverage = (Executed Stmts / Total Stmts) × 100%
    *Count braces + function declaration lines

  Decision Coverage = (Outcomes Exercised / Total Outcomes) × 100%
    *Each decision = 2 outcomes (T + F)

  Path Coverage = (Paths Executed / Total Paths) × 100%
    *Total paths from V(G) = e − n + 2
    *Or V(G) = d + 1 (decisions + 1)

  MCC Test Cases = 2^n (n = number of conditions)

PATH COVERAGE — 5 STEPS:
  1. Draw CFG
  2. Total independent paths
  3. Paths per test
  4. Total covered paths
  5. Apply formula

CFG SYMBOLS:
  ⊙  = start/stop
  ●  = intermediary (procedure) node
  arrows = directed edges (true/false labels)

STRENGTH ORDER:
  Statement < Decision < Condition < Multiple Condition

KEY TOOLS:
  JaCoCo (Java), NUnit (.NET), Cobertura, CodeCover, pitest.org
```

---

# ✅ LECTURE 4A — DONE

**Top exam-likely questions for this lecture:**
1. Calculate Statement / Decision / Path coverage for a given Java snippet.
2. Draw the Control Flow Graph + compute V(G).
3. Differentiate Condition vs Multiple Condition Coverage.

**Next: Lecture 4B — Cyclomatic Complexity Measure (continues from V(G) formula).**
