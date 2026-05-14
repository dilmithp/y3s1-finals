# LECTURE 4B — CYCLOMATIC COMPLEXITY MEASURE (CC)
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **🔥 EXAM CRITICAL — ONE OF THE THREE METRIC TOPICS**
> The exam paper says: *"1 of these 2 essays will be a SOFTWARE METRIC question (CC / CFS / WCC)."*
> **CC = Cyclomatic Complexity** is one of those three. Master this guide.
>
> Focus:
> - **Two formulas:** $V(G) = e - n + 2$ and $V(G) = d + 1$
> - **Class-level formula:** $V_g = n + d$
> - How to **draw a Control Flow Graph** from Java code
> - How to **count decision nodes** correctly
> - 6 worked examples from the slides — practice all of them

---

# SLIDE 1 — Title Slide
"Lecture 4 — Software Metrics (Cyclomatic Complexity Measure)." Skip.

---

# SLIDE 2 — How Software Quality Can Be Measured

## 2. Theory (Exactly as in slides)
**Software quality metrics include:**
- Code Quality
- Reliability
- Performance
- Usability
- Correctness
- Maintainability
- Integrity
- Security

## PRO TIPS
- **8 quality dimensions** — easy MCQ filler.
- **A4 Sheet:** *Quality metrics = Code Q, Reliability, Perf, Usability, Correctness, Maintainability, Integrity, Security.*

---

# SLIDE 3 — Why These Metrics Matter

## 2. Theory (Exactly as in slides)
- Help developers **track and improve software quality**
- Ensure **users get a good experience**
- Reduce **risks and costs** related to software failures

---

# SLIDE 4 — Cyclomatic Complexity Measure (MASTER FORMULAS)

## 1. Plain English Explanation
**Cyclomatic Complexity (CC)** measures **how complex** a program is by counting the number of **linearly independent paths** through its code. More decisions = more paths = higher CC.

## 2. Theory (Exactly as in slides)
> *Measures the number of linearly independent paths in a program.*

## 3. LaTeX Formulas

### Formula 1 — Graph-based:
$$V(G) = e - n + 2$$

Where:
- $e$ = number of **edges**
- $n$ = number of **nodes**

### Formula 2 — Decision-based:
$$V(G) = d + 1$$

Where:
- $d$ = number of **decision statements** (if, while, for, case, etc.)

### Formula 3 — Class-level:
$$V_g = n + d_i$$

Where:
- $n$ = number of **methods** in the class
- $d_i$ = total **decisions across all methods**

> *Spelled out (Slide 4):* "V_g = No. of decision statements in each method + No. of methods in a class"

## 4. PRO TIPS
- **3 formulas — memorize all 3.** Different questions use different formulas.
- **Most-used in exam:** $V(G) = d + 1$ (simplest — just count decisions).
- **Exam trap:** A `switch` with `case 1, case 2, case 3, default` counts as **3 decisions** (because there are 3 case branches; default is the fall-through, not a decision).
- **A4 Sheet:** All 3 formulas with definitions.

---

# SLIDES 6-8 — Bytecode CC + Compound Statements

## Plain English
The slides note that **CC of bytecode** (class file) can be **higher** than CC of the source file because compound conditions (like `if (A && B)`) get split into multiple branch instructions in bytecode.

## Theory (Exactly as in slides)
> You can't expect the same cyclomatic complexity from all the approaches. The CC value obtained from the **class file** can be **higher than** CC obtained from the **source file**.

## PRO TIPS
- **Key fact:** Bytecode CC ≥ Source CC.
- **A4 Sheet:** *Source CC may differ from bytecode CC. Compound conditions split in bytecode → higher CC.*

---

# SLIDE 9 — How to Draw the Control Flow Graph

## 2. Theory (Exactly as in slides — same as Slide 26 of Code Coverage lecture)
1. Use **⊙** (circle with dot) for **start/stop** nodes.
2. Use **●** (filled dot) for **intermediary** nodes.
3. **Label** start, stop, decisions, T/F paths.
4. **Edges always indicate direction** (arrows).
5. Start node, procedure nodes, and decisions can be **combined**.
6. A **procedure node** = one or more **non-decisional statements**.

---

# SLIDES 10-13 — CFG Example (if-else with V(G) = 2)

## Source Code (Slide 10)
```java
int p;
if (p < 10)
    System.out.println("Value of p is less than 10");
else
    System.out.println("Value of p is greater than or equal to 10");
```

## CFG Versions

### Version A (Slide 11 — separate decision node)
```
[start ⊙]
   ↓
[p ●] (procedure)
   ↓
[decision (if) ●]
   ├── True ── [• print "less"]
   └── False ── [• print "greater"]
   ↓
[stop ⊙]
```
**V(G) = e − n + 2 = 5 − 5 + 2 = 2**

### Version B (Slide 12 — combined start + decision)
```
[start, decision(if) ⊙]
   ├── True ── [• print "less"]
   └── False ── [• print "greater"]
   ↓
[stop ⊙]
```
**V(G) = e − n + 2 = 4 − 4 + 2 = 2**

## PRO TIPS
- **Important:** Even though the graph looks different, **V(G) stays the same** = 2.
- This is the "minimum CC" of an if-else block.
- **A4 Sheet:** *if-else block alone → V(G) = 2.*

---

# SLIDE 14 — Cyclomatic Complexity of a Class

## 1. Plain English Explanation
For a whole class, total CC = sum of CC of all its methods.

## 2. Theory (Exactly as in slides)

$$\text{Total CC for a class} (V_g) = \sum_{i=1}^{n} V(G_i)$$

$$V_g = \sum_{i=1}^{n} (d_i + 1)$$

$$\boxed{V_g = n + d_i}$$

Where:
- $n$ = number of methods in the class
- $G_i$ = flow graph for method $i$
- $d_i$ = number of decisions in method $i$

## 3. PRO TIPS
- **MOST USEFUL CLASS FORMULA: $V_g = n + d$** (where d = total decisions across all methods).
- **Memory trick:** "n methods + d decisions = class CC."
- **A4 Sheet:** *Class CC = #methods + total decisions.*

---

# SLIDES 16-18 — How V(G) = d+1 is derived from V(G) = e-n+2

## 1. Plain English Explanation
This is a **mini proof** showing why both formulas give the same answer.

## 2. Theory (Exactly as in slides)

**Nodes in a CFG:**
- Decision nodes (d)
- Procedure nodes (p)
- Start node (1)
- Stop node (1)
- **Total: n = d + p + 2**

> ⚠️ *Note: Slide 16 says "n = d + p + 1" — combining start and stop as one extra node. Both conventions yield the same final result, just by adjusting the formulas.*

The slide uses: **n = d + p + 1**

**Edges in a CFG:**
- Each **decision node** has **2 outgoing edges** (T + F) → contributes **2d** edges
- Each **procedure node** has **1 outgoing edge** → contributes **1p** edges
- **Total: e = 2d + p**

**Derivation:**
$$V(G) = e - n + 2 = (2d + p) - (d + p + 1) + 2 = d + 1$$

## 3. PRO TIPS
- This proof rarely appears as a direct exam question, but **understanding it** clarifies why $V(G) = d + 1$ works.
- **A4 Sheet:** *Edges = 2d + p, Nodes = d + p + 1 → simplifies to V(G) = d + 1.*

---

# SLIDES 19-22 — Worked Examples 1 & 2

## Example 1 — Simple `if` (no else)

```java
public static void D0(boolean a, String x) {
    if (a)
        System.out.println("x");
}
```

**CFG (Slide 20):**
```
[start, decision(if) ⊙]
   ├── True ── [• print x]
   └── False ──────→
              ↓
           [stop ⊙]
```

**Calculation:**
- **Decisions (d) = 1** (just `if`)
- **V(G) = d + 1 = 1 + 1 = 2**

Or by graph: e=3, n=3 → V(G) = 3 − 3 + 2 = **2**

---

## Example 2 — `if-else`

```java
public static void D1(boolean a, String x, String y) {
    if (a)
        System.out.println("x");
    else
        System.out.println("y");
}
```

**CFG (Slide 22):**
```
[start, decision(if) ⊙]
   ├── True ── [• print x]
   └── False ── [• print y]
                  ↓
              [stop ⊙]
```

**Calculation:**
- **d = 1** (one `if`)
- **V(G) = d + 1 = 1 + 1 = 2**

Or by graph: e=4, n=4 → V(G) = 4 − 4 + 2 = **2**

## PRO TIPS
- **Lesson:** `if` alone and `if-else` both have **V(G) = 2**. The presence of `else` doesn't add a new decision — it's the same `if`'s False branch.
- **A4 Sheet:** *`if` alone or `if-else` = V(G) = 2.*

---

# SLIDES 23-24 — Worked Example 3 — `for` loop

```java
public static void D3(int m, String x) {
    for (int i=0; i<m; i++)
        System.out.println("x");
}
```

**CFG (Slide 24):**
```
[start, decision(for) ⊙]
   ├── True ── [• print x] ──→ loop back
   └── False ──→ [stop ⊙]
```

**Calculation:**
- **d = 1** (the `for` condition is the decision)
- **V(G) = d + 1 = 2**

Or by graph: e=3, n=3 → V(G) = 3 − 3 + 2 = **2**

## PRO TIPS
- **Rule:** Any loop (for / while / do-while) contributes **1 decision** → adds 1 to V(G).
- **A4 Sheet:** *Loop = 1 decision = +1 to V(G).*

---

# SLIDES 25-26 — Worked Example 4 — `do-while` loop

```java
public static void D3(int a, String x) {
    do {
        System.out.println("x");
        a++;
    } while (a < 10);
}
```

**CFG (Slide 26):**
```
[start ⊙]
   ↓
[• body (print, a++)] ──→
   ↓
[decision (do-while) ●]
   ├── True ──→ loop back to body
   └── False ──→ [stop ⊙]
```

**Calculation:**
- **d = 1**
- **V(G) = d + 1 = 2**

Or by graph: e=3, n=3 → V(G) = 3 − 3 + 2 = **2**

---

# SLIDES 27-28 — Worked Example 5 — Composite Method (Nested if-else)

```java
void composite(boolean a, boolean b, String x, String y, String z) {
    if (a)
        System.out.println(x);
    else {
        if (b)
            System.out.println(y);
        else
            System.out.println(z);
    }
}
```

**CFG (Slide 28):**
```
[start, decision(if a) ⊙]
   ├── True ── [• print x]
   └── False ── [decision(if b) ●]
                  ├── True ── [• print y]
                  └── False ── [• print z]
                              ↓
                          [stop ⊙]
```

**Calculation:**
- **d = 2** (two `if` statements)
- **V(G) = d + 1 = 2 + 1 = 3**

Or by graph: e=7, n=6 → V(G) = 7 − 6 + 2 = **3**

## PRO TIPS
- **Rule:** Each `if` (even nested inside `else`) counts as **1 decision**.
- **Common exam trap:** Don't forget to count BOTH `if` statements.

---

# SLIDES 29-30 — Worked Example 6 — `switch-case`

```java
public static void main(String[] args) {
    int i = 0;
    switch (i) {
        case 1: System.out.println("its 1"); break;
        case 2: System.out.println("its 2"); break;
        case 3: System.out.println("its 3"); break;
        default: System.out.println("its none"); break;
    }
}
```

**CFG (Slide 30):**
```
[start, decision(switch) ⊙]
   ├── 1 ── [• "its 1"]
   ├── 2 ── [• "its 2"]
   ├── 3 ── [• "its 3"]
   └── default ── [• "its none"]
                  ↓
              [stop ⊙]
```

**Calculation by graph:**
- e = 8, n = 6
- **V(G) = e − n + 2 = 8 − 6 + 2 = 4**

**By d+1:** A switch with **3 cases + default** has effectively **3 decisions** (each case acts like an if-else against the value). Plus the default fall-through. d = 3 → V(G) = 3 + 1 = **4**.

## PRO TIPS
- **Switch rule:** A `switch` with **N case branches** (excluding default) gives **V(G) = N + 1**.
  - 3 cases + default → V(G) = 4
  - 4 cases + default → V(G) = 5
- **A4 Sheet:** *Switch with N cases (+default) → V(G) = N+1.*

---

# 📊 CC QUICK-REFERENCE TABLE FOR COMMON STRUCTURES

| Structure | Example | Decisions (d) | V(G) |
|-----------|---------|----------------|------|
| Linear code (no branches) | `print(x);` | 0 | **1** |
| Single `if` | `if(x>0) print(x);` | 1 | **2** |
| `if-else` | `if/else` | 1 | **2** |
| Single `for` / `while` | `for(...)` or `while(...)` | 1 | **2** |
| `do-while` | `do { } while()` | 1 | **2** |
| Nested `if` inside `else` | composite() above | 2 | **3** |
| `switch` with 3 cases + default | Example 6 above | 3 | **4** |
| `if` with `&&` (compound) | `if(A && B)` | 2 (in bytecode) | **3** (varies by tool) |

---

# 🎯 EXTRA WORKED EXAMPLES (Beyond Slides)

### Example A — Simple `while` with internal `if`
```java
void countPositives(int[] arr) {
    int count = 0;
    int i = 0;
    while (i < arr.length) {
        if (arr[i] > 0)
            count++;
        i++;
    }
    print(count);
}
```

**Decisions:**
- 1 × `while`
- 1 × `if`
- **d = 2**

**V(G) = d + 1 = 2 + 1 = 3**

---

### Example B — Class-level CC

```java
class Calculator {
    int add(int a, int b) { return a + b; }                // d = 0
    int divide(int a, int b) {                              // d = 1
        if (b == 0) return 0;
        return a / b;
    }
    int max(int a, int b) {                                 // d = 1
        if (a > b) return a;
        else return b;
    }
}
```

- **n = 3 methods**
- **Total decisions = 0 + 1 + 1 = 2**
- **$V_g = n + d = 3 + 2 = 5$**

---

# 📝 MCQ PRACTICE — LECTURE 4B (Cyclomatic Complexity)

---

### Q1. The formula V(G) = e − n + 2 calculates:
A) Statement Coverage
B) Decision Coverage
C) **Cyclomatic Complexity** ✅
D) Code Coverage percentage

**Answer: C (Slide 4)**

---

### Q2. The shorter formula V(G) = d + 1 uses:
A) Number of edges
B) **Number of decision statements** ✅
C) Number of methods
D) Number of lines of code

**Answer: B (Slide 4)**

---

### Q3. For an `if-else` block (no other code), V(G) is:
A) 1
B) **2** ✅
C) 3
D) 4

**Answer: B (Slide 13)**

---

### Q4. A switch statement with 4 cases and default has:
A) V(G) = 4
B) **V(G) = 5** ✅
C) V(G) = 6
D) V(G) = 8

**Answer: B — V(G) = number of cases + 1 = 4 + 1 = 5**

---

### Q5. The Class-level Cyclomatic Complexity is:
A) Just V(G) of the largest method
B) **Sum of V(G) of all methods = number of methods + total decisions** ✅
C) Average of all methods
D) Product of all V(G)

**Answer: B (Slide 14)**

---

### Q6. CC of bytecode (class file) vs source file:
A) Always equal
B) **Bytecode CC can be higher than source CC** ✅
C) Source CC is always higher
D) They are unrelated

**Answer: B (Slide 8)**

---

### Q7. Edges in a CFG with d decision nodes + p procedure nodes = ?
A) d + p
B) d + p + 2
C) **2d + p** ✅
D) 2d + 2p

**Answer: C (Slide 17)**

---

### Q8. The class has 4 methods. Method 1 has 2 ifs. Method 2 has 1 if. Method 3 has 1 while. Method 4 has 0 decisions. Class CC?
A) 4
B) 7
C) **8** ✅
D) 10

**Answer: C — V_g = n + d = 4 + (2+1+1+0) = 4 + 4 = 8**

---

# 📌 LECTURE 4B — A4 REFERENCE SHEET MINI-SECTION

```
CYCLOMATIC COMPLEXITY (CC)
  Measures: # of linearly independent paths
  Also = max # of test cases needed for path coverage

FORMULAS (3):
  Formula 1: V(G) = e − n + 2
             e = edges, n = nodes
  Formula 2: V(G) = d + 1
             d = number of decision statements
  Formula 3 (Class): V_g = n + d_i
             n = methods, d_i = decisions in method i

  Spelled out: V_g = (No. of decision statements in each method)
                       + (No. of methods in a class)

COMMON V(G) VALUES:
  Linear code        → V(G) = 1
  if (with or without else) → V(G) = 2
  for / while / do-while    → V(G) = 2
  nested if-else (1 nest)   → V(G) = 3
  switch with N cases       → V(G) = N + 1

PROOF (V(G) = d+1):
  Edges e = 2d + p
  Nodes n = d + p + 1
  V(G) = e − n + 2
       = (2d + p) − (d + p + 1) + 2
       = d + 1

CFG SYMBOLS:
  ⊙  = start/stop
  ●  = procedure (intermediary)
  arrows: True/False labels

BYTECODE vs SOURCE:
  Bytecode CC ≥ Source CC (compound conditions split)

INTERPRETATION (Industry guideline, not in slides):
  1–10  → simple, low risk
  11–20 → moderate
  21–50 → complex
  >50   → unstable, high risk
```

---

# ✅ LECTURE 4B — DONE

**Top exam-likely questions for this lecture:**
1. **"Calculate V(G) for the given Java code."** (use d+1 or e−n+2)
2. **"Draw the Control Flow Graph for this code."**
3. **"Compute the total Cyclomatic Complexity of a class."** (use V_g = n + d)
4. **"Derive V(G) = d + 1 from V(G) = e − n + 2."**

**Next: Lecture 5 — Cognitive Functional Size (CFS).**
