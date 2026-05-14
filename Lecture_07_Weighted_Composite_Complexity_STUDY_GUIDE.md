# LECTURE 7 — WEIGHTED COMPOSITE COMPLEXITY (WCC)
## Complete Slide-by-Slide Exam Preparation Guide
### Course: Software Engineering Process and Quality Management (SLIIT)

---

> # 🔥🔥🔥 THE #1 EXAM-CRITICAL LECTURE 🔥🔥🔥
>
> Your exam paper will have **one essay** that is a SOFTWARE METRIC question (CC / CFS / **WCC**). Of these three, **WCC is the most likely** because:
> - It's the most recent and most complex metric
> - It integrates CC + CFS concepts (control structures + size)
> - It requires the **most steps** (best for an essay-worth question)
> - All four of your peers' reference sheets dedicate prime space to WCC
>
> **What you MUST be able to do:**
> 1. Count **tokens per line** using 17 official rules
> 2. Apply **3 weight tables** (Wc, Wn, Wi)
> 3. Calculate **Wt = Wc + Wn + Wi**, then **WC = S × Wt**, then **WCC = Σ WC**
> 4. Show a complete **9-column table** as the answer
> 5. Show every step of working

---

# SLIDE 1 — Title Slide
"Lecture 7 — Software Metrics (Weighted Composite Complexity Metric)." Skip.

---

# SLIDE 2 — WCC Overview

## 1. Plain English Explanation
**WCC** measures how complex a program is by considering **4 factors** simultaneously: how big each line is, what kind of control structure it's part of, how deeply nested it is, and how deep in the inheritance hierarchy it sits.

## 2. Theory (Exactly as in slides)
- **Measure the complexity of the program.**
- **Object Oriented Metric**
- **Based on 4 key factors:**
  - **Size (S)**
  - **Type of control structures (Wc)**
  - **Nesting level of control structures (Wn)**
  - **Inheritance level of statements (Wi)**

## 3. PRO TIPS
- **Memory trick: "S-C-N-I"** → Size, Control, Nesting, Inheritance.
- WCC is an **OO metric** — that's why Inheritance matters (CFS doesn't include this).
- **A4 Sheet:** *WCC = OO metric with 4 factors: S, Wc, Wn, Wi.*

---

# SLIDE 3 — Computing the WCC Value (MASTER FORMULAS)

## 1. Plain English Explanation
WCC is computed line-by-line, then summed across the whole program.

## 2. LaTeX Formulas (THE BIG THREE)

### Formula 1 — Total Weight per Statement
$$\boxed{W_t = W_c + W_n + W_i}$$

### Formula 2 — Weighted Complexity per Single Statement
$$\boxed{WC = S \times W_t}$$

### Formula 3 — Total WCC of the Program
$$\boxed{WCC = \sum_{j=1}^{n} S_j \times (W_t)_j}$$

**Where:**
| Symbol | Meaning |
|--------|---------|
| $S_j$ | Size of jᵗʰ executable statement (token count) |
| $n$ | Total number of executable statements |
| $(W_t)_j$ | Total weight of jᵗʰ executable statement |
| $W_c$ | Weight due to type of control structure |
| $W_n$ | Weight due to nesting level |
| $W_i$ | Weight due to inheritance level |

## 3. PRO TIPS
- **Memory order: "Wt → WC → WCC"** — three letters at three scales (statement weight → statement complexity → program complexity).
- **A4 Sheet:** Write all 3 formulas verbatim.

---

# SLIDE 4 — Identify the Size (S) of a Statement

## 1. Plain English Explanation
The **Size (S)** of a statement = the **total number of tokens** in it. A "token" is a fundamental program element (operator, keyword, identifier, etc.) — but **not everything in the code is a token**.

## 2. Theory (Exactly as in slides)
- The **Size (S)** of a statement is the **total number of tokens** it contains.
- In WCC, a **token** is a fundamental program element used to measure the size of a statement.
- **Not everything in the code is a token.**
- Refer to the guidelines document to identify tokens.

---

# 🎯 THE 17 OFFICIAL TOKEN COUNTING RULES (FROM COURSEWEB GUIDELINES)

> *These are the rules referenced in the slide. Memorize these — they ARE the exam grading criteria.*

| # | Rule | Examples |
|---|------|----------|
| **1** | Token identification **begins after the class declaration** | `public class Result {` → no tokens here |
| **2** | In general: **operators, keywords (except access flags), strings, identifiers, numerical values (including zero)** are separate tokens | `marks`, `>`, `-1`, `&&`, `void` |
| **3** | All characters inside `' '` or `" "` = **a SINGLE token** | `"Hello World"` → 1 token |
| **4** | **Array name + `[]`** = ONE token | `args[]` → 1 token, not 2 |
| **5** | Each **comma** that separates components = a separate token | `a, b, c` → comma counted twice |
| **6** | **Brackets `()` `{}` `[]` are NOT separate tokens** (unless part of array/method/control) | standalone `{` `}` skipped |
| **7** | In **variable DECLARATION** → variable name is **NOT** a token. In **variable DEFINITION** (with init) → variable name **IS** a token | `int x;` → x not counted. `int x = 5;` → x counted |
| **8** | **Method name + `()`** = ONE token. For **user-defined methods**, the components **inside `()` are NOT tokens** | `outresult()` → 1 token. `outresult(50)` → still 1 token (50 ignored). Same for user-defined constructors |
| **9** | In a decisional statement, the **keyword + round brackets = ONE token**: `if()`, `if-else()`, `else-if()`, `for()`, `while()`, `do-while()`, `switch()`. But a statement with **only `else` or `do`** is NOT counted | `if(...)` → 1 token. `else` alone → 0 |
| **10** | `case :` and `default :` in a switch = **separate tokens** | each case is its own token |
| **11** | `catch()` + round brackets = ONE token. **`try` alone is NOT counted** | similar to else/do |
| **12** | The **`.` operator** that connects classes/fields/methods = separate token. The names connected by `.` are also separate tokens | `System.out.println("x")` → System, ., out, ., println(), "x" = **6 tokens** |
| **13** | The statement **terminator `;` is NOT a token** | every `;` is free |
| **14** | Manipulators like **`endl`, `"\n"`** = tokens | `cout << endl;` → endl counted |
| **15** | The **`*` in pointer declaration** is NOT a token (just notation) | `int* ptr;` → * skipped |
| **16** | The **`return` keyword is NOT a token** | `return x;` → only x counted |
| **17** | For a program which does **NOT** have a **built-in root class**, the weight allocation of Wi begins at **1** (NOT 0). | All statements in standalone Java class → Wi starts at 1 |

## ✅ QUICK COUNT / DON'T COUNT TABLE (Combined with your original brief)

| ✅ COUNTED | ❌ NOT COUNTED |
|-----------|----------------|
| Variable names (in expressions or definitions) | Blank lines |
| Operators (`+`, `-`, `=`, `>`, `<`, `&&`, `||`, `.`, etc.) | Import statements |
| Method calls with `()` (e.g., `println()`) | Class declarations (rule 1) |
| String literals in `" "` or `' '` (whole thing = 1 token) | Standalone closing braces `}` |
| Keywords: `if-else()`, `for()`, `while()`, `switch()`, `case:`, `default:`, `catch()`, `break`, `new` | `else` and `do` keywords alone (rules 9, 11) |
| `void` as return type | Data type keywords as declarations: `int`, `String`, `double`, `boolean` (but their VARIABLE NAME counts if there's `=`) |
| Increment/decrement: `i++`, `i--` | Access modifiers: `public`, `private`, `static`, `final` (rule 2) |
| Numeric literals (including zero) | Parameters inside user-defined method calls: `outresult(50)` → `50` is skipped (rule 8) |
| Dot `.` operator | `return` keyword (rule 16) |
| Array name + `[]` (one token together) | Statement terminator `;` (rule 13) |
| Each comma `,` (rule 5) | Pointer `*` notation (rule 15) |
| `endl`, `"\n"` (rule 14) | Brackets `(){}[]` alone (rule 6) |

---

# SLIDES 5-6 — Token Identification Example (Result Class)

## Source Code
```java
public class Result {                              // Line 1
    public void outresult(int marks) {             // Line 2
        if (marks > -1 && marks < 50)              // Line 3
            System.out.println("Fail");            // Line 4
        else                                        // Line 5
            System.out.println("Pass");            // Line 6
    }
    public static void main(String args[]) {       // Line 7
        Result r = new Result();                   // Line 8
        r.outresult(50);                           // Line 9
    }
}
```

## Token Count Table (Steps 1–3)

| Line | Program Statement | Tokens | S |
|------|-------------------|---------|---|
| 1 | `public class Result {` | (skipped — class declaration, rule 1) | — |
| 2 | `public void outresult(int marks) {` | `void`, `outresult()` | **2** |
| 3 | `if (marks > -1 && marks < 50)` | `if-else()`, `marks`, `>`, `-1`, `&&`, `marks`, `<`, `50` | **8** |
| 4 | `System.out.println("Fail");` | `System`, `.`, `out`, `.`, `println()`, `"Fail"` | **6** |
| 5 | `else` | (rule 9 — else alone is NOT counted) | — |
| 6 | `System.out.println("Pass");` | `System`, `.`, `out`, `.`, `println()`, `"Pass"` | **6** |
| 7 | `public static void main(String args[]) {` | `void`, `main()` | **2** |
| 8 | `Result r = new Result();` | `Result`, `r`, `=`, `new`, `Result()` | **5** |
| 9 | `r.outresult(50);` | `r`, `.`, `outresult()` | **3** |

## Why Each Line's Count is What It Is

### Line 2: `public void outresult(int marks) {` → S = 2
- ❌ `public` → access flag (rule 2)
- ✅ `void` → keyword/return type
- ✅ `outresult()` → method name + brackets = 1 token (rule 8)
- ❌ `int` → data type in declaration
- ❌ `marks` → parameter inside user-defined method (rule 8)
- ❌ `{` → bracket (rule 6)

### Line 3: `if (marks > -1 && marks < 50)` → S = 8
- ✅ `if-else()` → decisional keyword + brackets = 1 token (rule 9)
- ✅ `marks` (first appearance) → identifier
- ✅ `>` → operator
- ✅ `-1` → numeric literal
- ✅ `&&` → operator
- ✅ `marks` (second appearance) → identifier
- ✅ `<` → operator
- ✅ `50` → numeric literal

### Line 4 & 6: `System.out.println("XXX");` → S = 6
- ✅ `System` → identifier
- ✅ `.` → connecting operator (rule 12)
- ✅ `out` → field name
- ✅ `.` → connecting operator
- ✅ `println()` → method call (rule 8 — note: `println` is library, not user-defined, so the string `"Fail"`/`"Pass"` IS counted separately)
- ✅ `"Fail"` / `"Pass"` → string in quotes (rule 3 → single token)

### Line 8: `Result r = new Result();` → S = 5
- ✅ `Result` → class identifier
- ✅ `r` → variable name in **DEFINITION** with `=` (rule 7)
- ✅ `=` → operator
- ✅ `new` → keyword
- ✅ `Result()` → constructor call (rule 8)

### Line 9: `r.outresult(50);` → S = 3
- ✅ `r` → identifier
- ✅ `.` → connecting operator
- ✅ `outresult()` → method call (rule 8 — `50` is NOT counted because `outresult` is user-defined)

---

# SLIDE 7 — Weight Due to Type of Control Structure (Wc) — TABLE 1

## 1. Theory (Exactly as in slides)

| Type of Control Structure | Weight (Wc) |
|----------------------------|-------------|
| **Sequential** | **0** |
| **Branch** | **1** |
| **Iterative** | **2** |
| **Switch statement with n cases** | **n** |

## 2. PRO TIPS
- **Memory trick: "0-1-2-n"** → Sequential, Branch, Iterative, Switch.
- **A statement only has a Wc value if the line ITSELF is a control statement.** Otherwise Wc = 0.
  - The `if` line gets Wc = 1.
  - The `println` line INSIDE the if gets Wc = 0 (it's a sequential statement, even though it's inside a branch).
- **Switch trap:** A switch with 4 cases → Wc = 4 (for the switch line itself).
- **A4 Sheet:** This 4-row table verbatim.

---

# SLIDE 8 — Wc Applied to the Example

Adding the **Wc column** to the table:

| Line | Statement | Tokens | S | **Wc** |
|------|-----------|---------|---|-------|
| 1 | `public class Result {` | — | — | — |
| 2 | `public void outresult(int marks) {` | void, outresult() | 2 | **0** (sequential) |
| 3 | `if (marks > -1 && marks < 50)` | if-else(), marks, >, -1, &&, marks, <, 50 | 8 | **1** (branch) |
| 4 | `System.out.println("Fail");` | System, ., out, ., println(), "Fail" | 6 | **0** (sequential — line itself isn't a control structure) |
| 6 | `System.out.println("Pass");` | System, ., out, ., println(), "Pass" | 6 | **0** |
| 7 | `public static void main(String args[]) {` | void, main() | 2 | **0** |
| 8 | `Result r = new Result();` | Result, r, =, new, Result() | 5 | **0** |
| 9 | `r.outresult(50);` | r, ., outresult() | 3 | **0** |

---

# SLIDE 9 — Weight Due to Nesting Level (Wn) — TABLE 2

## 1. Theory (Exactly as in slides)

| Nesting Level of Statements | Weight (Wn) |
|------------------------------|-------------|
| Sequential statements (no nesting) | **0** |
| Statements inside the **outermost / 1st level** control structures | **1** |
| Statements inside the **2nd level** control structures | **2** |
| Statements inside the **3rd level** control structures | **3** |
| Statements inside the **nth level** control structures | **n** |

## 2. PRO TIPS
- **The control structure line ITSELF is at the level where it sits.** Example:
  - A top-level `if` → that `if` line has Wn = 1.
  - A `for` inside that `if` → that `for` line has Wn = 2.
  - A statement inside the `for` → Wn = 3.
- **Memory cue:** "How deep am I inside braces?"
- **Visual technique (RECOMMENDED for exam):** Before assigning Wn, draw a small **nesting diagram** of nested control structures.
- **A4 Sheet:** This 5-row table verbatim.

---

# SLIDE 10 — Wn Applied to the Example

Nesting visualization:
```
class Result {
  outresult() {
    if (...)              ← Wn = 1 (1st level control)
      System.out...        ← Wn = 1 (inside 1st level)
    else
      System.out...        ← Wn = 1 (inside 1st level)
  }
  main() {
    Result r = new Result();  ← Wn = 0 (no nesting)
    r.outresult(50);          ← Wn = 0 (no nesting)
  }
}
```

| Line | Statement | S | Wc | **Wn** |
|------|-----------|---|----|-------|
| 2 | `public void outresult(int marks) {` | 2 | 0 | **0** (method declaration is sequential) |
| 3 | `if (marks > -1 && marks < 50)` | 8 | 1 | **1** (the if line is at 1st level) |
| 4 | `System.out.println("Fail");` | 6 | 0 | **1** (inside the if at 1st level) |
| 6 | `System.out.println("Pass");` | 6 | 0 | **1** (inside the else at 1st level) |
| 7 | `main(...){` | 2 | 0 | **0** (sequential) |
| 8 | `Result r = new Result();` | 5 | 0 | **0** (sequential) |
| 9 | `r.outresult(50);` | 3 | 0 | **0** (sequential) |

---

# SLIDE 11 — Weight Due to Inheritance Level (Wi) — TABLE 3

## 1. Theory (Exactly as in slides)

| Inheritance Level of Statements | Weight (Wi) |
|----------------------------------|-------------|
| Statements inside the **base class / root class** | **0** |
| Statements inside the **1st derived class** | **1** |
| Statements inside the **2nd derived class** | **2** |
| Statements inside the **nth derived class** | **n** |

## 2. CRITICAL RULE (FROM RULE 17 IN COURSEWEB GUIDELINES)
> *"For a program which does NOT have a built-in root class, the weight allocation of the Wi attribute begins at 1."*

**Why this matters for Java:** Every Java class implicitly extends `Object`. But in WCC, the **Result** class in our example is treated as the **1st derived class** (Wi = 1) because there is no user-defined root class above it.

## 3. PRO TIPS
- **All Java classes that don't extend another user-class → Wi = 1 for their statements.**
- If a class **extends** another class → its statements are Wi = 2.
- If that subclass is extended again → Wi = 3, etc.
- **A4 Sheet:** This 4-row table + Rule 17 caveat.

---

# SLIDE 12 — Wi Applied to the Example

Since `Result` is a standalone class with no user-defined parent → all statements inside Result get **Wi = 1** (rule 17).

| Line | Statement | S | Wc | Wn | **Wi** |
|------|-----------|---|----|----|-------|
| 2 | method declaration | 2 | 0 | 0 | **1** |
| 3 | if-statement | 8 | 1 | 1 | **1** |
| 4 | print "Fail" | 6 | 0 | 1 | **1** |
| 6 | print "Pass" | 6 | 0 | 1 | **1** |
| 7 | main method declaration | 2 | 0 | 0 | **1** |
| 8 | Result r = new Result() | 5 | 0 | 0 | **1** |
| 9 | r.outresult(50) | 3 | 0 | 0 | **1** |

---

# SLIDE 13 — Total Weight per Statement (Wt)

## Formula
$$\boxed{W_t = W_c + W_n + W_i}$$

This combines the **3 dimensions of complexity** (control type + nesting + inheritance) into one number per statement.

---

# SLIDE 14 — Wt Applied to the Example

| Line | Statement | S | Wc | Wn | Wi | **Wt** |
|------|-----------|---|----|----|----|-------|
| 2 | method decl | 2 | 0 | 0 | 1 | **0+0+1 = 1** |
| 3 | if statement | 8 | 1 | 1 | 1 | **1+1+1 = 3** |
| 4 | print "Fail" | 6 | 0 | 1 | 1 | **0+1+1 = 2** |
| 6 | print "Pass" | 6 | 0 | 1 | 1 | **0+1+1 = 2** |
| 7 | main decl | 2 | 0 | 0 | 1 | **0+0+1 = 1** |
| 8 | new Result() | 5 | 0 | 0 | 1 | **0+0+1 = 1** |
| 9 | r.outresult(50) | 3 | 0 | 0 | 1 | **0+0+1 = 1** |

---

# SLIDE 15 — Weighted Complexity per Single Statement (WC)

## Formula
$$\boxed{WC = S \times W_t}$$

It tells us how complex **one line** is by factoring in:
- How many **tokens** it contains (Size S)
- How **"heavy" or complex its context** is (Total Weight Wt)

---

# SLIDE 16 — WC Applied to Each Line of the Example

| Line | Statement | S | Wc | Wn | Wi | Wt | **WC = S × Wt** |
|------|-----------|---|----|----|----|----|---|
| 2 | method decl | 2 | 0 | 0 | 1 | 1 | **2 × 1 = 2** |
| 3 | if statement | 8 | 1 | 1 | 1 | 3 | **8 × 3 = 24** |
| 4 | print "Fail" | 6 | 0 | 1 | 1 | 2 | **6 × 2 = 12** |
| 6 | print "Pass" | 6 | 0 | 1 | 1 | 2 | **6 × 2 = 12** |
| 7 | main decl | 2 | 0 | 0 | 1 | 1 | **2 × 1 = 2** |
| 8 | new Result() | 5 | 0 | 0 | 1 | 1 | **5 × 1 = 5** |
| 9 | r.outresult(50) | 3 | 0 | 0 | 1 | 1 | **3 × 1 = 3** |

---

# SLIDE 17 — WCC for the Whole Program

## Formula
$$WCC = \sum_{j=1}^{n} WC_j$$

**Just sum all WC values across every executable line.**

---

# SLIDE 18 — FINAL CALCULATION (WCC = 60)

## Complete Table

| Line | Statement | Tokens | S | Wc | Wn | Wi | Wt | WC |
|------|-----------|--------|---|----|----|----|----|-----|
| 1 | `public class Result {` | — | — | — | — | — | — | — |
| 2 | `public void outresult(int marks) {` | void, outresult() | 2 | 0 | 0 | 1 | 1 | **2** |
| 3 | `if (marks > -1 && marks < 50)` | if-else(), marks, >, -1, &&, marks, <, 50 | 8 | 1 | 1 | 1 | 3 | **24** |
| 4 | `System.out.println("Fail");` | System, ., out, ., println(), "Fail" | 6 | 0 | 1 | 1 | 2 | **12** |
| 5 | `else` | — | — | — | — | — | — | — |
| 6 | `System.out.println("Pass");` | System, ., out, ., println(), "Pass" | 6 | 0 | 1 | 1 | 2 | **12** |
| 7 | `public static void main(String args[]) {` | void, main() | 2 | 0 | 0 | 1 | 1 | **2** |
| 8 | `Result r = new Result();` | Result, r, =, new, Result() | 5 | 0 | 0 | 1 | 1 | **5** |
| 9 | `r.outresult(50);` | r, ., outresult() | 3 | 0 | 0 | 1 | 1 | **3** |
| | **WCC Value** | | | | | | | **60** |

## Running Sum
$$WCC = 2 + 24 + 12 + 12 + 2 + 5 + 3 = \mathbf{60}$$

---

# 📋 THE 9-STEP EXAM ANSWER FORMAT (Per Your Original Brief)

> **Always present your WCC essay answer in this exact format.**

### STEP 1 — Identify all executable statements
Skip:
- ❌ Class declaration (line `public class Result {`)
- ❌ Blank lines
- ❌ Standalone braces `{` `}`
- ❌ Standalone `else`, `do`, `try`

### STEP 2 — Count tokens per line (build a table)
Use the 17 rules. Show: `Tokens listed | Why each is counted`

### STEP 3 — Determine S (size) = total token count per line

### STEP 4 — Determine Wc (use Table 1)
- Sequential = 0
- Branch = 1
- Iterative = 2
- Switch with N cases = N

### STEP 5 — Determine Wn (draw nesting diagram first)
- Top level (no nesting) = 0
- Inside 1st-level control = 1
- Inside 2nd-level control = 2
- Inside nth-level = n

### STEP 6 — Determine Wi (identify base/derived class hierarchy)
- Base class = 0
- 1st derived class = 1
- 2nd derived = 2 …
- **If no user-defined root class → start at 1** (Rule 17)

### STEP 7 — Calculate Wt = Wc + Wn + Wi for each line

### STEP 8 — Calculate WC = S × Wt for each line

### STEP 9 — Sum all WC → **Final WCC Value**

---

# 🎯 EXTRA WORKED EXAMPLE #1 — Simple (with one loop)

## Source Code
```java
public class Counter {
    public static void main(String args[]) {
        int sum = 0;
        for (int i = 1; i <= 5; i++)
            sum = sum + i;
        System.out.println(sum);
    }
}
```

## Step-by-Step

### Steps 1–3 — Tokens and Size

| Line | Statement | Tokens | S |
|------|-----------|--------|---|
| 1 | `public class Counter {` | (skip — class decl) | — |
| 2 | `public static void main(String args[]) {` | void, main() | 2 |
| 3 | `int sum = 0;` | sum, =, 0 | 3 |
| 4 | `for (int i = 1; i <= 5; i++)` | for(), i, =, 1, i, <=, 5, i++ | 8 |
| 5 | `sum = sum + i;` | sum, =, sum, +, i | 5 |
| 6 | `System.out.println(sum);` | System, ., out, ., println(), sum | 6 |

> ⚠️ **Note on line 4:** The `for()` is one token (rule 9). Inside the for header: `i`, `=`, `1` (definition with init, rule 7 → name counts), then `i`, `<=`, `5`, then `i++` (`++` is operator). Total = 1 + 3 + 3 + 1 = 8.

> Note on line 6: `sum` IS counted here because it's used in an expression, and `println()` is a library method so its argument `sum` IS counted (rule 8 only excludes args of user-defined methods).

### Step 4 — Wc (Type of Control)
- Line 2 (method decl): 0
- Line 3 (sequential assignment): 0
- Line 4 (**iterative** for loop): **2**
- Line 5 (inside loop, sequential statement): 0
- Line 6 (sequential): 0

### Step 5 — Wn (Nesting)
- Line 2: 0 (no nesting)
- Line 3: 0 (top-level inside method)
- Line 4: **1** (the for is at 1st level)
- Line 5: **2** (inside the for, which IS the 1st level)
- Line 6: 0 (back outside the for)

Wait — actually let me reconsider. The for statement *itself* is at level 1 (Wn = 1). Statements *inside* the for body are at level 2 (Wn = 2 per the table).

But looking again at the canonical example: Line 3 (`if`) had Wn = 1, and line 4 (`println` INSIDE the if) ALSO had Wn = 1. So the slide's convention is: **the control structure line and the statements directly inside it share the same nesting level** (both = 1 at 1st level).

So actually:
- Line 4 (for): **Wn = 1**
- Line 5 (inside for): **Wn = 1**

This matches the slide's pattern.

### Step 6 — Wi (Inheritance)
Counter has no parent → Wi = **1** for all statements (Rule 17).

### Steps 7–9 — Final Table

| Line | Tokens | S | Wc | Wn | Wi | Wt | WC |
|------|--------|---|----|----|----|----|-----|
| 2 | void, main() | 2 | 0 | 0 | 1 | 1 | **2** |
| 3 | sum, =, 0 | 3 | 0 | 0 | 1 | 1 | **3** |
| 4 | for(), i, =, 1, i, <=, 5, i++ | 8 | 2 | 1 | 1 | 4 | **32** |
| 5 | sum, =, sum, +, i | 5 | 0 | 1 | 1 | 2 | **10** |
| 6 | System, ., out, ., println(), sum | 6 | 0 | 0 | 1 | 1 | **6** |

$$WCC = 2 + 3 + 32 + 10 + 6 = \mathbf{53}$$

---

# 🎯 EXTRA WORKED EXAMPLE #2 — Complex (with switch + nesting)

## Source Code
```java
public class Grader {
    public void grade(int marks) {
        switch (marks) {
            case 90: System.out.println("A"); break;
            case 80: System.out.println("B"); break;
            case 70: System.out.println("C"); break;
            default: System.out.println("F"); break;
        }
    }
}
```

### Tokens and S

| Line | Statement | Tokens | S |
|------|-----------|--------|---|
| 1 | `public class Grader {` | (skip) | — |
| 2 | `public void grade(int marks) {` | void, grade() | 2 |
| 3 | `switch (marks) {` | switch(), marks | 2 |
| 4 | `case 90: System.out.println("A"); break;` | case:, 90, System, ., out, ., println(), "A", break | 9 |
| 5 | `case 80: System.out.println("B"); break;` | case:, 80, System, ., out, ., println(), "B", break | 9 |
| 6 | `case 70: System.out.println("C"); break;` | case:, 70, System, ., out, ., println(), "C", break | 9 |
| 7 | `default: System.out.println("F"); break;` | default:, System, ., out, ., println(), "F", break | 8 |

> Note: `case 90:` → `case:` is one token (rule 10) + `90` is a separate numeric token = 2 tokens just for the case label, then the println chain (6 tokens) + `break` (keyword, counted) = 9 total. Same for default but no number = 8.

### Weights

- **Wc:**
  - Line 2: 0 (method decl)
  - Line 3 (`switch` with **3 cases + default** → n = 3): **Wc = 3**
  - Lines 4–7: 0 (these are sequential statements inside the switch)

> ⚠️ Important: Wc for switch = **number of cases** (excluding default). 3 cases → Wc = 3.

- **Wn:**
  - Line 2: 0
  - Line 3: **1** (switch is at 1st level)
  - Lines 4–7: **1** (statements inside the switch at 1st level)

- **Wi:** All = 1 (Grader is 1st derived class, rule 17)

### Final Table

| Line | Tokens | S | Wc | Wn | Wi | Wt | WC |
|------|--------|---|----|----|----|----|-----|
| 2 | void, grade() | 2 | 0 | 0 | 1 | 1 | **2** |
| 3 | switch(), marks | 2 | 3 | 1 | 1 | 5 | **10** |
| 4 | case:, 90, System,.,out,.,println(),"A",break | 9 | 0 | 1 | 1 | 2 | **18** |
| 5 | case:, 80, System,.,out,.,println(),"B",break | 9 | 0 | 1 | 1 | 2 | **18** |
| 6 | case:, 70, System,.,out,.,println(),"C",break | 9 | 0 | 1 | 1 | 2 | **18** |
| 7 | default:, System,.,out,.,println(),"F",break | 8 | 0 | 1 | 1 | 2 | **16** |

$$WCC = 2 + 10 + 18 + 18 + 18 + 16 = \mathbf{82}$$

---

# 📊 MASTER REFERENCE — ALL 3 WCC WEIGHT TABLES

## Table 1: Wc (Control Structure Type)

| Type | Weight |
|------|--------|
| Sequential | **0** |
| Branch (if-else) | **1** |
| Iterative (for / while / do-while) | **2** |
| Switch with n cases | **n** |

## Table 2: Wn (Nesting Level)

| Level | Weight |
|-------|--------|
| Sequential (no nesting) | **0** |
| 1st-level control structure | **1** |
| 2nd-level (nested once) | **2** |
| 3rd-level (nested twice) | **3** |
| nth-level | **n** |

## Table 3: Wi (Inheritance Level)

| Level | Weight |
|-------|--------|
| Base / Root class | **0** |
| 1st derived class | **1** |
| 2nd derived class | **2** |
| nth derived class | **n** |
| ⚠️ **Standalone class (no built-in root)** | **starts at 1** (Rule 17) |

---

# 📝 MCQ PRACTICE — LECTURE 7 (WCC)

---

### Q1. The formula for the total weight of a statement is:
A) Wt = Wc × Wn × Wi
B) **Wt = Wc + Wn + Wi** ✅
C) Wt = S × (Wc + Wn + Wi)
D) Wt = S + Wc + Wn + Wi

**Answer: B (Slide 13)**

---

### Q2. The Weighted Complexity for a single statement is:
A) WC = S + Wt
B) **WC = S × Wt** ✅
C) WC = Wt / S
D) WC = S × Wc × Wn × Wi

**Answer: B (Slide 15)**

---

### Q3. The cognitive weight Wc for an iterative structure is:
A) 0
B) 1
C) **2** ✅
D) n

**Answer: C (Slide 7)**

---

### Q4. The cognitive weight Wc for a switch statement with 5 cases is:
A) 1
B) 2
C) **5** ✅
D) 6

**Answer: C — Switch with n cases gives Wc = n (Slide 7)**

---

### Q5. A statement inside the 3rd-level control structure has Wn equal to:
A) 1
B) 2
C) **3** ✅
D) n

**Answer: C (Slide 9)**

---

### Q6. In WCC, the statement `r.outresult(50);` has S = 3 because:
A) There are 3 characters
B) **The `50` is NOT counted (argument of user-defined method) — only `r`, `.`, `outresult()` count** ✅
C) Only operators count
D) Method names don't count

**Answer: B (Rule 8)**

---

### Q7. The token count for `if-else()`, `switch()`, and `for()` is:
A) 0 each
B) **1 each (keyword + brackets = one token)** ✅
C) 2 each
D) n each

**Answer: B (Rule 9)**

---

### Q8. For a Java class with no user-defined parent class, the Wi value of statements inside it is:
A) 0
B) **1 (Rule 17 — Wi starts at 1 if no built-in root class)** ✅
C) 2
D) n

**Answer: B (Slide 11 + Rule 17)**

---

### Q9. The statement `System.out.println("Hello");` has size S equal to:
A) 4
B) 5
C) **6** ✅
D) 7

**Answer: C — Tokens: System, ., out, ., println(), "Hello" = 6**

---

### Q10. The final WCC of a program is calculated by:
A) Multiplying all WC values
B) Taking the maximum WC
C) **Summing all WC values across executable lines** ✅
D) Taking the average

**Answer: C (Slide 17)**

---

### Q11. Which of the following is NOT counted as a token in WCC?
A) `void`
B) Variable names in definitions (with `=`)
C) **Access flags like `public` and `static`** ✅
D) Numeric literals

**Answer: C (Rule 2)**

---

### Q12. In the worked example, why does line 3 (`if (marks > -1 && marks < 50)`) get Wt = 3?
A) Because it has 3 operators
B) **Because Wc=1 (branch) + Wn=1 (1st level) + Wi=1 (1st derived class) = 3** ✅
C) Because it has 3 tokens
D) Because WC = 3

**Answer: B (Slide 14)**

---

# 📌 LECTURE 7 — A4 REFERENCE SHEET MINI-SECTION

```
WEIGHTED COMPOSITE COMPLEXITY (WCC)
  OO metric, 4 key factors:
    S  = Size (token count)
    Wc = Weight due to type of control structure
    Wn = Weight due to nesting level
    Wi = Weight due to inheritance level

FORMULAS (3):
  Wt  = Wc + Wn + Wi              (Total weight per statement)
  WC  = S × Wt                    (Complexity per statement)
  WCC = Σ WC across all lines     (Total program complexity)

WEIGHT TABLES:
  Wc (Control Type):
    Sequential = 0, Branch = 1, Iterative = 2, Switch(n) = n
  Wn (Nesting):
    Top-level = 0, 1st = 1, 2nd = 2, 3rd = 3, nth = n
  Wi (Inheritance):
    Base = 0, 1st derived = 1, 2nd derived = 2, nth = n
    ⚠ NO built-in root class → starts at 1 (Rule 17)

TOKEN COUNTING — KEY RULES (17 official):
  ✅ COUNTED:
    operators (+, -, =, >, <, &&, ||, ., etc.)
    keywords (except access flags)
    identifiers (variable names if in DEFINITION or expression)
    strings in " " (one token, no matter how long)
    numeric literals (including 0)
    if-else(), for(), while(), do-while(), switch(), catch() = 1 each
    case:, default: (separate tokens)
    method_name() + () = 1 token
    void as return type, new, break, endl, "\n"
    each comma ,
    array[] (one token together with array name)
    i++, i--
  ❌ NOT COUNTED:
    access flags: public, private, static, final
    data type keywords in declarations: int, String, double
    variable name in DECLARATION (no =)
    parameters inside user-defined method/constructor ()
    parameters inside user-defined method invocations
    else, do, try (when standalone)
    return keyword
    statement terminator ;
    standalone braces ( ) { } [ ]
    pointer * notation
    everything before class declaration starts

9-STEP EXAM ANSWER FORMAT:
  1. Identify executable statements (skip class decl, braces, else, blank lines)
  2. Count tokens per line
  3. Determine S (per line)
  4. Determine Wc (control structure type)
  5. Determine Wn (draw nesting diagram first)
  6. Determine Wi (identify inheritance hierarchy)
  7. Calculate Wt = Wc + Wn + Wi
  8. Calculate WC = S × Wt
  9. Sum all WC → WCC value

CANONICAL EXAMPLE (memorize):
  Result class with if-else and main → WCC = 60

LINE-BY-LINE PATTERNS:
  method_decl (void method()):     S=2, Wc=0, Wn=0, Wi=1 → WC=2
  println("X"):                     S=6, often inside if so Wn=1 → WC=12
  if (compound condition):          S=8, Wc=1, Wn=1, Wi=1 → WC=24
  obj = new Class():                S=5, Wc=0 → WC=5
  obj.method(arg):                  S=3 (arg ignored if user-defined) → WC=3
```

---

# ✅ LECTURE 7 — DONE — 🎉 ALL METRIC LECTURES COMPLETE

You now have **EVERY metric** ready for the exam:
- ✅ **Lecture 4A** — Code Coverage (3 formulas)
- ✅ **Lecture 4B** — Cyclomatic Complexity (V(G) = e−n+2 = d+1)
- ✅ **Lecture 5** — Cognitive Functional Size (BCS weights, Sf = (Ni+No)×Wc)
- ✅ **Lecture 7** — Weighted Composite Complexity (3 weight tables, 17 token rules, WCC = ΣWC)

---

## 🔑 Top exam strategy for the metric essay question:

1. **First, recognize which metric is asked** (look for keywords):
   - "Token count" / "Wc, Wn, Wi" / "WCC" → **Weighted Composite Complexity (Lecture 7)**
   - "Cognitive weight" / "BCS" / "Sf" → **Cognitive Functional Size (Lecture 5)**
   - "Independent paths" / "V(G)" / "Cyclomatic" → **Cyclomatic Complexity (Lecture 4B)**

2. **Always show the formula FIRST**, then substitute.

3. **Build a table** (the marker will check your working column by column).

4. **State the final answer clearly in BOLD** (e.g., "**WCC = 60**").

5. **Don't skip the trivial lines** — even a method declaration with just `void, methodName()` contributes 2 × 1 = 2 to WCC.

---

# 🎯 FULL COURSE STATUS

You now have **comprehensive study guides for all 11 lectures**:
- ✅ Lecture 1 — Introduction to Software Testing
- ✅ Lecture 2 — Specification Based Test Case Design Techniques
- ✅ Lecture 3 — Functional and Non-Functional Testing
- ✅ Lecture 4A — Code Coverage Analysis
- ✅ Lecture 4B — Cyclomatic Complexity Measure
- ✅ Lecture 5 — Cognitive Functional Size (CFS)
- ⚠️ Lecture 6 — *Not uploaded (missing from your files)*
- ✅ Lecture 7 — Weighted Composite Complexity (WCC) **← you are here**
- ✅ Lecture 8 — Software Testing Lifecycle (STLC)
- ✅ Lecture 9 — Test Automation
- ✅ Lecture 10 — Test-Driven Development (TDD)
- ✅ Lecture 11 — Trends in Software Testing

**Want me to compile a single A4 Reference Sheet (both sides, exam-allowed) combining everything?** Just say "make A4 sheet" — I'll fit it all on one printable double-sided page.
