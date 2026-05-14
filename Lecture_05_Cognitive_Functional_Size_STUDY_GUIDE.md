# LECTURE 5 — COGNITIVE FUNCTIONAL SIZE (CFS)
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> **🔥 EXAM CRITICAL — ONE OF THE THREE METRIC TOPICS**
> The exam will have one essay on **CC / CFS / WCC**. **CFS = Cognitive Functional Size** is this lecture's headline metric.
>
> **Focus:**
> - **BCS Weight Table** (Sequence=1, Branch=2/3, Iteration=3, Recursion=3, Function Call=2)
> - **Wc formula** (with/without nesting)
> - **Sf formula** for basic and complex components
> - The slide example: Bubble Sort → Wc = 37, and the Marks example → Sf = 30 CWU
> - **Step-by-step calculation method** — exam expects you to show all working

---

# SLIDE 1 — Title Slide
"Lecture 5 — Software Metrics (Cognitive Functional Size Metric)." Skip.

---

# SLIDE 2 — Cognitive Functional Size Metric

## 1. Plain English Explanation
**Cognitive Functional Size (CFS)** measures how **mentally hard** a piece of software is to understand. It uses three things:
1. How complex its **control structures** are (loops, ifs, function calls)
2. How many **inputs** it takes
3. How many **outputs** it produces

## 2. Theory (Exactly as in slides)
- **Paradigm Independent metric** (works for procedural, OO, etc.)
- CFS is a function of **three fundamental factors**:
  1. **Cognitive weights of Basic Control Structures (BCSs)**
  2. **Number of inputs (Ni)**
  3. **Number of outputs (No)**
- **Cognitive weight of software** = the **degree of difficulty or effort required to understand** a software component based on its control structures.

## 3. PRO TIPS
- **3 ingredients of CFS — "BCS + Ni + No"** memorize.
- **Key definition:** *"Cognitive weight = difficulty of understanding the component."*
- **A4 Sheet:** *CFS = function of (BCS weights, Ni, No). Paradigm-independent.*

---

# SLIDES 3-5 — The 3 Basic Control Structure Categories

## Category 1 — Sequence Structures
**Definition (slide 3):** *A series of actions completed in a specific order.*
```java
System.out.println("Step 1");
System.out.println("Step 2");
System.out.println("Step 3");
```

## Category 2 — Branch Structures
**Definition (slide 4):** *Executes certain code only when a condition is met.*
```java
if (age >= 18)
    System.out.println("Eligible");
else
    System.out.println("Not eligible");
```

## Category 3 — Iterative Structures
**Definition (slide 5):** *Executes a code block repeatedly until a condition is met.*
```java
for (int i=1; i<=5; i++)
    System.out.println(i);
```

## PRO TIPS
- **3 main categories — "S-B-I"** → Sequence, Branch, Iterative.
- Plus a 4th hidden category: **Embedded Components** (Function Call + Recursion) — see Slide 6.
- **A4 Sheet:** *4 BCS categories: Sequence, Branch, Iteration, Embedded.*

---

# SLIDE 6 — BCS WEIGHT TABLE (THE MOST IMPORTANT TABLE IN THIS LECTURE)

## 1. Plain English Explanation
**Each control structure** has a cognitive weight $W_i$. Memorize all 8 values.

## 2. Theory (Exactly as in slides)

| Category | BCS Type | Symbol | $W_i$ (Weight) |
|----------|----------|--------|-----------------|
| **Sequence** | Sequence (SEQ) | series of statements | **1** |
| **Branch** | If-then-[else] (ITE) | `if/else` | **2** |
| **Branch** | Case (CASE) | `switch/case` | **3** |
| **Iteration** | For-do (Rᵢ) | `for` loop | **3** |
| **Iteration** | Do-while (R₁) | `do-while` | **3** |
| **Iteration** | While-do (R₀) | `while` loop | **3** |
| **Embedded** | Function Call (FC) | method call | **2** |
| **Embedded** | Recursion (REC) | self-calling method | **3** |

## 3. PRO TIPS — Memory Tricks
- **Sequence = 1** (simplest).
- **If-else = 2.**
- **Everything else (case, for, do-while, while, recursion) = 3.**
- **Function Call = 2** (lower than recursion because a normal call is easier to reason about).
- **Memory phrase:** *"Sequence is **1**, if-else is **2**, function-call is **2**, all others are **3**."*
- **A4 Sheet:** This table verbatim — it's the foundation of CFS calculation.

## Quick Recap
- 8 BCS types with weights 1, 2, 3.
- Only Sequence = 1.
- Only If-then-[else] and Function Call = 2.
- All other 5 = 3.

---

# SLIDES 7-8 — Total Cognitive Weight (Wc) Formula

## 1. Plain English Explanation
**Wc** = total cognitive weight of all the BCSs in your code. If BCSs are **nested**, you **multiply** the weights of nested layers. If BCSs are in **sequence** (side by side), you **add** them.

## 2. Theory (Exactly as in slides)

The total cognitive weight of a software component **Wc** is defined as:

$$W_c = \sum_{j=1}^{q} \left[ \prod_{k=1}^{m} \sum_{i=1}^{n} W_c(j, k, i) \right]$$

**Where:**
- $q$ = number of **linear blocks** (sequence-level chunks side-by-side)
- $m$ = number of **layers of nesting** within a block
- $n$ = number of **linear BCSs in each layer**

## 3. Simplified Formula (No Nesting)

If there are NO embedded/nested BCSs (m = 1), the formula collapses to:

$$W_c = \sum_{j=1}^{q} \sum_{i=1}^{n} W_c(j, i)$$

## 4. PRO TIPS — How to Read the Formula
- **Inner Σ** = sum of BCS weights in **one layer of one block**.
- **Π (product)** = multiply layers together (because nested layers compound difficulty).
- **Outer Σ** = sum the q blocks (which are side by side in code).

**Rules of Thumb:**
- **Side-by-side BCSs → ADD their weights**
- **Nested BCSs → MULTIPLY across nesting layers**

- **A4 Sheet:**
  - *Wc (nested): Σⱼ [Πₖ Σᵢ Wc(j,k,i)]*
  - *Wc (no nesting): Σⱼ Σᵢ Wc(j,i)*
  - *Nesting = multiply. Sequence = add.*

## Quick Recap
- Two versions of Wc formula: with nesting (Π) and without (just sums).
- Nested layers MULTIPLY. Sequential blocks ADD.

---

# SLIDE 9 — WORKED EXAMPLE 1: Bubble Sort (Wc = 37)

## 1. Plain English Explanation
Let's compute Wc for a classic bubble sort with **3 nested loops/ifs**.

## 2. Source Code
```java
public void bubbleSort() {
    int out, in;
    for (out = nElems-1; out > 1; out--)        // FOR
        for (in = 0; in < out; in++)             // FOR (nested)
            if (a[in] > a[in+1])                 // IF (nested)
                swap(in, in+1);                  // FUNCTION CALL (nested)
}
```

## 3. Structure of BCSs (from slide)
```
SEQUENCE
  └── FOR (outer)
        └── FOR (inner, nested)
              └── IF (nested inside inner FOR)
                    └── FUNCTION CALL (nested inside IF)
```

## 4. Step-by-Step Calculation

**Identify weights:**
- SEQUENCE (outer wrap) → $W = 1$
- FOR (outer) → $W = 3$
- FOR (inner, nested) → $W = 3$
- IF (nested) → $W = 2$
- Function Call (nested) → $W = 2$

**Apply formula (nested):**
$$W_c = 1 + 3 \times (3 \times (2 \times 2))$$

Wait — using the slide's exact computation:
$$W_c = 1 + 3 \times (3 \times (2 \times (2)))$$

Slide computes it as:
$$W_c = 1 + 3 (3 (2 (2))) = 1 + 36 = \mathbf{37}$$

**Detailed breakdown:**
- Innermost: function call $W = 2$
- Wrap in IF: $2 \times 2 = 4$
- Wrap in inner FOR: $3 \times 4 = 12$
- Wrap in outer FOR: $3 \times 12 = 36$
- Add the outer Sequence: $1 + 36 = \mathbf{37}$

## 5. PRO TIPS
- **CRITICAL EXAM RULE:** Whenever a BCS is **inside another BCS**, multiply.
- The **outermost Sequence (W=1)** is always added at the end.
- **A4 Sheet:** Bubble sort example: $W_c = 1 + 3(3(2(2))) = 37$.

---

# SLIDE 11 — WORKED EXAMPLE 2: Two Side-by-Side For Loops (Wc = 7)

## 1. Source Code
```java
public static void main(String[] args) {
    String[] modules = {"SEPQM", "DS", "ESD", "AF", "SA"};

    for (int i = 0; i < modules.length; i++) {
        System.out.println(modules[i]);
    }

    System.out.println("In reverse order:");

    for (int i = modules.length - 1; i >= 0; i--) {
        System.out.println(modules[i]);
    }
}
```

## 2. Structure of BCSs
```
SEQUENCE → FOR → FOR
(side by side, NOT nested)
```

## 3. Calculation (Slide 11)

Since the two FORs are **side-by-side (NOT nested)**, we ADD them.

$$W_c = 1 + 3 + 3 = \mathbf{7}$$

**Where:**
- 1 = Sequence weight
- 3 = first FOR
- 3 = second FOR

## 4. PRO TIPS
- **Side-by-side loops/ifs = ADD their weights, don't multiply.**
- **A4 Sheet:** *2 side-by-side for-loops: Wc = 1 + 3 + 3 = 7.*

---

# SLIDE 12 — CFS Formula for a Basic Component

## 1. Plain English Explanation
For a single method, the Cognitive Functional Size is calculated by multiplying (Ni + No) by Wc.

## 2. Theory (Exactly as in slides)

The CFS of a basic software component (with one method) Sf is:

$$\boxed{S_f = (N_i + N_o) \times W_c}$$

**Where:**
- $N_i$ = **Number of inputs** to the component
- $N_o$ = **Number of outputs** from the component
- $W_c$ = **Total cognitive weight**

## 3. Counting Rules
- **Ni** = number of formal parameters / inputs read from user
- **No** = number of return values / outputs printed (typically counted as how many distinct outputs visible at a time)

## 4. PRO TIPS
- **Unit of CFS:** **CWU** = Cognitive Weight Units.
- **A4 Sheet:** $S_f = (N_i + N_o) \times W_c$

## Quick Recap
- **CFS of basic component = (Inputs + Outputs) × Total Cognitive Weight.**

---

# SLIDE 13 — CFS Formula for a Complex Component

## Plain English
For a component with multiple methods, sum the CFS of each method.

## Theory (Exactly as in slides)

$$\boxed{S_f(c) = \sum_{c=1}^{n} S_f(c)}$$

Where:
- $n$ = number of methods in the complex component
- $S_f(c)$ = CFS of each individual method

## PRO TIPS
- **Add up CFS from each method.**
- **A4 Sheet:** *Complex component CFS = Σ of each method's Sf.*

---

# SLIDE 14 — CFS Formula for a Software System

## Plain English
For an entire system of multiple components, sum the CFS of each component.

## Theory (Exactly as in slides)

$$\boxed{\hat{S}_f = \sum_{k=1}^{p} S_f(k)}$$

Where:
- $p$ = number of components in the system
- $S_f(k)$ = CFS of each component

## PRO TIPS
- **3 levels: Method (Sf) → Component (Sf(c)) → System (Ŝf).**
- **A4 Sheet:** *System CFS = Σ component CFS = Σ method CFS.*

---

# SLIDES 15-16 — WORKED EXAMPLE: Marks Grading System (Sf = 30 CWU)

## 1. Source Code (Slide 15)
```java
import java.util.Scanner;
public class Results {
    public static void main(String[] args) {
        System.out.print("Enter your marks: ");
        Scanner sc = new Scanner(System.in);
        int marks = sc.nextInt();
        while (marks < 0 || marks > 100) {
            System.out.print("Enter a valid mark: ");
            marks = sc.nextInt();
        }
        if (marks > 75)
            System.out.println("A Pass");
        else if (marks <= 75 && marks > 65)
            System.out.println("B Pass");
        else if (marks <= 65 && marks > 45)
            System.out.println("C Pass");
        else
            System.out.println("Fail");
    }
}
```

## 2. Structure of BCSs (Slide 16)
```
SEQUENCE
  ├── WHILE
  ├── IF
  ├── ELSE IF
  └── ELSE IF
(all side-by-side after sequence; no deep nesting)
```

## 3. Step-by-Step Calculation

### Step 1 — Calculate Wc
Identify each BCS and its weight:
- SEQUENCE → $W = 1$
- WHILE → $W = 3$
- IF → $W = 2$
- ELSE IF (first) → $W = 2$
- ELSE IF (second) → $W = 2$

Since these are **side-by-side** (no nesting between them shown):

$$W_c = 1 + 3 + 2 + 2 + 2 = \mathbf{10}$$

### Step 2 — Count Ni and No
- **Ni = 2** (inputs: `marks` and `marks` again inside the while loop — though it's the same variable, the slide counts 2 distinct read operations)
- **No = 1** ("Only one S.O.P statement is executed at a given time" — per the slide's note)

### Step 3 — Apply CFS Formula

$$S_f = (N_i + N_o) \times W_c = (2 + 1) \times 10 = \mathbf{30 \text{ CWU}}$$

## 4. PRO TIPS
- **Important counting rule from the slide:** *"Only one S.O.P statement is executed at a given time"* — so even with 4 print statements, No = 1.
- **A4 Sheet:** Marks example: Wc = 10, Ni = 2, No = 1, Sf = 30 CWU.

## Quick Recap
- Calculation flow: identify BCSs → weights → Wc → count Ni/No → apply formula → Sf.

---

# 📊 MASTER REFERENCE TABLES

## Table A — BCS Weight Reference (Slide 6, again)

| BCS | $W_i$ |
|-----|-------|
| Sequence (SEQ) | **1** |
| If-then-[else] (ITE) | **2** |
| Case (CASE / switch) | **3** |
| For-do | **3** |
| Do-while | **3** |
| While-do | **3** |
| Function Call (FC) | **2** |
| Recursion (REC) | **3** |

## Table B — The 4 CFS Formulas

| # | Formula | Used For |
|---|---------|----------|
| 1 | $W_c = \sum_j [\prod_k \sum_i W_c(j,k,i)]$ | Wc with nesting |
| 2 | $W_c = \sum_j \sum_i W_c(j,i)$ | Wc without nesting (m=1) |
| 3 | $S_f = (N_i + N_o) \times W_c$ | Basic component (one method) |
| 4 | $S_f(c) = \sum_{c=1}^{n} S_f(c)$ | Complex component (n methods) |
| 5 | $\hat{S}_f = \sum_{k=1}^{p} S_f(k)$ | Whole system (p components) |

---

# 🎯 EXTRA WORKED EXAMPLES (Beyond Slides)

### Example A — Simple Method (No Nesting)

```java
public int sumPositive(int[] arr) {       // Ni = 1 (arr), No = 1 (return)
    int sum = 0;
    for (int i = 0; i < arr.length; i++) {     // FOR (W=3)
        if (arr[i] > 0)                          // IF nested in FOR (W=2)
            sum += arr[i];
    }
    return sum;
}
```

**BCS structure:** SEQUENCE → FOR → IF (nested inside FOR)

**Wc calculation:**
- Innermost: IF = 2
- Wrapped in FOR (nested): $3 \times 2 = 6$
- Add Sequence: $1 + 6 = \mathbf{7}$

**Ni = 1, No = 1**

$$S_f = (1 + 1) \times 7 = \mathbf{14 \text{ CWU}}$$

---

### Example B — Method with 2 Side-by-side Loops

```java
public void process(int[] a, int[] b) {     // Ni = 2, No = 0
    for (int i = 0; i < a.length; i++)        // FOR (W=3)
        System.out.println(a[i]);

    for (int i = 0; i < b.length; i++)        // FOR (W=3)
        System.out.println(b[i]);
}
```

**BCS structure:** SEQUENCE → FOR + FOR (side-by-side)

**Wc = 1 + 3 + 3 = 7**

Counting outputs: again "one S.O.P at a time" — **No = 1**.

$$S_f = (2 + 1) \times 7 = \mathbf{21 \text{ CWU}}$$

---

### Example C — Complex Component (2 Methods)

Suppose a class has 2 methods:
- `method1`: Sf = 14 CWU
- `method2`: Sf = 21 CWU

$$S_f(\text{component}) = 14 + 21 = \mathbf{35 \text{ CWU}}$$

---

# 📝 MCQ PRACTICE — LECTURE 5 (CFS)

---

### Q1. The cognitive weight of a **Sequence** structure is:
A) **1** ✅
B) 2
C) 3
D) 0

**Answer: A (Slide 6)**

---

### Q2. The cognitive weight of an **If-then-else** structure is:
A) 1
B) **2** ✅
C) 3
D) 4

**Answer: B (Slide 6)**

---

### Q3. The cognitive weight of a **For-do** iteration is:
A) 1
B) 2
C) **3** ✅
D) 4

**Answer: C (Slide 6)**

---

### Q4. The cognitive weight of a **Function Call** is:
A) 1
B) **2** ✅
C) 3
D) 4

**Answer: B (Slide 6)**

---

### Q5. The CFS of a basic component is calculated by:
A) Sum of Ni and No only
B) Wc only
C) **(Ni + No) × Wc** ✅
D) (Ni × No) / Wc

**Answer: C (Slide 12)**

---

### Q6. When BCSs are nested, their cognitive weights are:
A) Added
B) **Multiplied across nesting layers** ✅
C) Subtracted
D) Divided

**Answer: B (Slide 7 — the Π in the formula)**

---

### Q7. The unit of Cognitive Functional Size is:
A) Bytes
B) Lines of Code
C) **CWU (Cognitive Weight Units)** ✅
D) Cyclomatic Units

**Answer: C (Slide 16)**

---

### Q8. CFS is a **paradigm independent** metric, meaning:
A) It only works for OO programming
B) It only works for procedural code
C) **It works regardless of programming paradigm** ✅
D) It requires specific language features

**Answer: C (Slide 2)**

---

### Q9. In the Bubble Sort example, the Wc = 37 comes from:
A) 1 + 3 + 3 + 2 + 2
B) **1 + 3(3(2(2))) = 1 + 36 = 37** ✅
C) 3 × 3 × 2 × 2
D) 1 × 3 × 3 × 2 × 2

**Answer: B (Slide 9 — because all loops/if/call are nested)**

---

### Q10. The CFS of a complex component with n methods is:
A) The product of Sf of each method
B) **The sum of Sf of each method** ✅
C) The Sf of the largest method only
D) The average of Sf

**Answer: B (Slide 13)**

---

# 📌 LECTURE 5 — A4 REFERENCE SHEET MINI-SECTION

```
COGNITIVE FUNCTIONAL SIZE (CFS)
  Paradigm-independent metric
  3 factors: BCS weights, Ni, No
  Cognitive weight = effort to understand

BCS WEIGHT TABLE (memorize):
  Sequence (SEQ)         → 1
  If-then-[else] (ITE)   → 2
  Case / Switch (CASE)   → 3
  For-do (Rᵢ)            → 3
  Do-while (R₁)          → 3
  While-do (R₀)          → 3
  Function Call (FC)     → 2
  Recursion (REC)        → 3

MEMORY: Sequence=1, If-else=2, FC=2, EVERY OTHER=3.

WC FORMULAS:
  With nesting:    Wc = Σⱼ [Πₖ Σᵢ Wc(j,k,i)]
  Without nesting: Wc = Σⱼ Σᵢ Wc(j,i)

RULES:
  Side-by-side BCSs → ADD weights
  Nested BCSs       → MULTIPLY across layers

CFS FORMULAS:
  Basic component:   Sf = (Ni + No) × Wc
  Complex component: Sf(c) = Σ Sf(c)
  Whole system:      Ŝf = Σ Sf(k)

UNIT: CWU (Cognitive Weight Units)

KEY EXAMPLES:
  Bubble Sort     → Wc = 1 + 3(3(2(2))) = 37
  Two side-by-side FORs → Wc = 1 + 3 + 3 = 7
  Marks grading   → Wc = 10, Sf = 30 CWU (Ni=2, No=1)

COUNTING RULES:
  Ni = # of inputs / params / reads
  No = # of outputs (typically 1 if only "one S.O.P at a time")
```

---

# ✅ LECTURE 5 — DONE

**Top exam-likely essay questions for this lecture:**
1. **"Calculate the CFS for the given Java code."** (your hottest exam target — see WCC lecture for similar)
2. **"List BCS types and their cognitive weights."**
3. **"Differentiate Wc for nested vs side-by-side structures."**
4. **"Why is CFS called a 'paradigm-independent' metric?"**

---

# 🎉 ALL THREE METRIC LECTURES COMPLETE

You now have detailed study guides for:
- ✅ **Lecture 4A** — Code Coverage Analysis (5 methods, 3 formulas)
- ✅ **Lecture 4B** — Cyclomatic Complexity (V(G) = e-n+2, V(G) = d+1, V_g = n+d)
- ✅ **Lecture 5** — Cognitive Functional Size (BCS weights, Wc, Sf)

**Still pending:**
- **Lecture 7 — Weighted Composite Complexity (WCC)** ← the **most likely exam metric question** because WCC builds on CC + CFS.

Want me to do Lecture 7 next? (highly recommended — it ties everything together)
