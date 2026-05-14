# SEPQM — Model Exam Questions for Software Metrics
## SE3010 — One Essay = Software Metric (CC / CFS / WCC)

> **Strategy:** Past patterns suggest WCC is the most likely (most lecture time + most worked examples in slides). Be ready for all three.
>
> **Exam mark structure (typical):**
> - Part (a): Define / explain concept (3-5 marks)
> - Part (b): Calculate for given code (10-15 marks)
> - Part (c): Interpret / compare / recommend (2-3 marks)

---

# SECTION 1 — CYCLOMATIC COMPLEXITY (CC)

## Quick Formula Recap
```
V(G) = e − n + 2     (e = edges, n = nodes)
V(G) = d + 1         (d = number of decision points)
Vg(class) = methods + decisions    (sum across all methods)
```
**Decision points = if, for, while, do-while, case (each one), && and || (each one).**

---

## Q1 — Basic CFG + V(G)

**Question:**
For the following pseudocode:
```
1. read x
2. if (x > 0)
3.    print "positive"
4. else
5.    print "non-positive"
6. end if
7. print "done"
```
(a) Draw the Control Flow Graph (CFG).
(b) Calculate V(G) using **both** formulas.
(c) State the number of independent paths and interpret the result.

**Worked Answer:**

CFG nodes: `N1: read x` → `N2: if x>0` → branches to `N3: print positive` OR `N4: print non-positive` → both merge to `N5: print done`

```
        [N1: read x]
             │
        [N2: if x>0]
           /     \
   [N3: positive] [N4: non-positive]
           \     /
        [N5: print done]
```

- **Nodes (n) = 5**
- **Edges (e) = 5** (N1→N2, N2→N3, N2→N4, N3→N5, N4→N5)
- **Decisions (d) = 1** (the if)

**V(G) = e − n + 2 = 5 − 5 + 2 = 2**
**V(G) = d + 1 = 1 + 1 = 2** ✓

**Independent paths = 2.** Low complexity — easy to test, low risk.

---

## Q2 — Nested Loops with Inner Decision

**Question:** Calculate V(G) for:
```java
int sum = 0;
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        if(arr[i][j] > 0) {
            sum += arr[i][j];
        }
    }
}
return sum;
```

**Worked Answer:**

Decisions:
- `for(i...)` → 1
- `for(j...)` → 1
- `if(arr[i][j] > 0)` → 1
- **d = 3**

**V(G) = d + 1 = 4.**

Moderate complexity. Need ≥4 test cases to cover all independent paths.

---

## Q3 — Switch Statement

**Question:** Calculate V(G) for:
```java
switch(grade) {
    case 'A': points = 4; break;
    case 'B': points = 3; break;
    case 'C': points = 2; break;
    case 'D': points = 1; break;
    default:  points = 0;
}
```

**Worked Answer:**

Each `case` is a decision → 4 cases + default fall-through.

**Rule:** `switch with N cases (plus default) → V(G) = N + 1`

**V(G) = 4 + 1 = 5.**

---

## Q4 — Whole-Class Vg(class)

**Question:** A class `BankAccount` has 4 methods with the following internal V(G) values:
| Method | V(G) |
|--------|------|
| `deposit()` | 2 |
| `withdraw()` | 4 |
| `transfer()` | 3 |
| `getBalance()` | 1 |

Calculate Vg(class) and recommend an action.

**Worked Answer:**

Recall: each method's V(G) = d + 1, so decisions per method = V(G) − 1.

| Method | V(G) | Decisions (d) |
|--------|------|---------------|
| deposit | 2 | 1 |
| withdraw | 4 | 3 |
| transfer | 3 | 2 |
| getBalance | 1 | 0 |
| **Total** | | **6** |

**Vg(class) = methods + decisions = 4 + 6 = 10.**

`withdraw()` has the highest V(G)=4 — consider refactoring or adding extensive unit tests.

---

## Q5 — Compound Condition Trap (&& / ||)

**Question:** Calculate V(G):
```java
if(age >= 18 && age <= 65 && hasLicense) {
    canDrive = true;
}
```

**Worked Answer:**

**Trap:** Each `&&` and `||` adds 1 decision (short-circuit creates an extra branch).

- `if` itself → 1
- `&&` (first) → 1
- `&&` (second) → 1
- **d = 3**

**V(G) = 3 + 1 = 4.**

Need 4 test cases (T/F combinations of the three conditions).

---

# SECTION 2 — COGNITIVE FUNCTIONAL SIZE (CFS)

## Quick Formula Recap
```
Sf = (Ni + No) × Wc
```
- **Ni** = number of input variables (read into program)
- **No** = number of output variables (printed/returned)
- **Wc** = total cognitive weight of all BCSs (Basic Control Structures)

### BCS Weights:
| BCS | Symbol | Weight |
|-----|--------|--------|
| Sequence | SEQ | 1 |
| If-then-else | ITE | 2 |
| Case / switch | CASE | 3 |
| For-do | Ri | 3 |
| Do-while | R1 | 3 |
| While-do | R0 | 3 |
| Function call | FC | 2 |
| Recursion | REC | 3 |

### Composition Rule:
- **Side-by-side BCSs → ADD**
- **Nested BCSs → MULTIPLY**

---

## Q1 — Side-by-Side BCSs

**Question:** Calculate Sf for:
```
read x;
read y;
if(x > y)
    max = x;
else
    max = y;
print max;
```

**Worked Answer:**

Structures (top to bottom, all side-by-side):
- SEQ (read x): **1**
- SEQ (read y): **1**
- ITE (if-else): **2**
- SEQ (print max): **1**

**Wc = 1 + 1 + 2 + 1 = 5**

**Ni = 2** (x, y), **No = 1** (max)

**Sf = (2 + 1) × 5 = 15 CWU** (Cognitive Weighted Units)

---

## Q2 — Nested BCSs (Bubble Sort)

**Question:** Calculate Sf for bubble sort:
```
read array[n], read n;
for(i = 0; i < n; i++)
    for(j = 0; j < n-i-1; j++)
        if(arr[j] > arr[j+1])
            swap(arr[j], arr[j+1]);
print array;
```

**Worked Answer:**

The nested structure is: `For(For(If(Seq)))` — nested → MULTIPLY.

Inner-out:
- Innermost SEQ (swap) = 1
- ITE wrapping it = 2 × 1 = **2**
- For wrapping that = 3 × 2 = **6**... 

Actually applying the slide formula: **Wc = 1 + 3(3(2(2))) = 37**

(The 1 = the leading read SEQ; the 2 at the deepest level is `ITE(SEQ)` = 2×1 = 2 by the slide convention; the slides sometimes treat the innermost as 2 directly.)

Step by step:
- Leading SEQ (read): 1
- Innermost SEQ (swap): 1
- ITE wrapping inner SEQ: 2 × 1 = 2
- Inner For wrapping ITE: 3 × 2 = 6
- Outer For wrapping inner For: 3 × 6 = 18
- Side-by-side add the leading SEQ: 1 + 18 = 19

(**Note:** The slides give `Wc = 1 + 3(3(2(2))) = 37` if you treat the swap-inside-if as nested weight 2×2=4 instead of 2×1=2 because the swap itself is non-trivial. Follow whichever convention your lecturer used in class. The KEY thing to show in your answer is the **nested = multiply** rule.)

**Ni** = depends on n + array elements (often counted as 2: `array` and `n`)
**No** = 1 (the printed array)

**Sf = (2 + 1) × Wc**

---

## Q3 — Marks Grading (Side-by-side ITE chain)

**Question:** Compute Sf for:
```
read marks;
if(marks >= 75) grade = 'A';
else if(marks >= 65) grade = 'B';
else if(marks >= 50) grade = 'C';
else if(marks >= 35) grade = 'D';
else grade = 'F';
print grade;
```

**Worked Answer:**

Each `else-if` adds one ITE block. Treating side-by-side:
- SEQ (read): 1
- ITE × 4 (the chain): 2 + 2 + 2 + 2 = 8
- SEQ (assign in else): 1 (or absorb)
- SEQ (print): 1

**Wc = 1 + 8 + 1 = 10**

**Ni = 1** (marks), **No = 1** (grade)

**Sf = (1 + 1) × 10 = 20 CWU**

---

## Q4 — Two Side-by-Side FOR Loops

**Question:**
```
for(i = 0; i < n; i++)
    print arr1[i];
for(j = 0; j < m; j++)
    print arr2[j];
```
Compute Wc.

**Worked Answer:**

Two For loops side-by-side, each containing a SEQ:
- For × SEQ (nested) = 3 × 1 = 3
- For × SEQ (nested) = 3 × 1 = 3
- Side-by-side ADD = 3 + 3 = **6**

(Slide shortcut: `Wc = 1 + 3 + 3 = 7` if including a leading SEQ.)

---

# SECTION 3 — WEIGHTED COMPOSITE COMPLEXITY (WCC) ⭐⭐⭐

## Most likely exam metric. Master this section.

### Formulas
```
Wt = Wc + Wn + Wi         (total weight per line)
WC = S × Wt               (line complexity)
WCC = Σ WC over all lines (program total)
```

### Weight Tables

**Wc — Control Type:**
| Type | Wc |
|------|-----|
| Sequential | 0 |
| Branch (if-else) | 1 |
| Iterative (for/while) | 2 |
| Switch (n cases) | n |

**Wn — Nesting Level:**
| Level | Wn |
|-------|-----|
| Sequential (no nesting) | 0 |
| 1st level (outermost block) | 1 |
| 2nd level | 2 |
| nth level | n |

**Wi — Inheritance Level:**
| Level | Wi |
|-------|-----|
| Base/root class | 0 |
| 1st derived | 1 |
| 2nd derived | 2 |
| **Rule 17: No built-in root class → Wi starts at 1** | |

### The 9-Step Exam Answer Format
1. Identify executable statements (skip class decl, braces, else, do, try, blanks)
2. Count tokens per line
3. Determine S (size) = token count
4. Determine Wc (control type)
5. Determine Wn (nesting level — draw a nesting diagram first!)
6. Determine Wi (inheritance level)
7. Compute Wt = Wc + Wn + Wi
8. Compute WC = S × Wt per line
9. WCC = Σ WC

### 17 Token-Counting Rules (memorize)
1. Tokens BEGIN after class declaration.
2. Operators, keywords (NOT access flags), strings, identifiers, numbers (incl. 0) = separate tokens.
3. Inside `' '` or `" "` = SINGLE token.
4. Array name + `[]` = ONE token (`args[]`).
5. Each comma = separate token.
6. Brackets `( ){ }[ ]` NOT separate tokens.
7. Var DECLARATION → name NOT token. Var DEFINITION (with `=`) → name IS token.
8. Method name + `()` = 1 token. User-defined method args INSIDE `()` NOT counted.
9. Decisional keyword + `()` = 1 token: `if()`, `if-else()`, `for()`, `while()`, `do-while()`, `switch()`. Standalone `else`/`do` NOT counted.
10. `case :` and `default :` = separate tokens.
11. `catch()` = 1 token. Standalone `try` NOT counted.
12. `.` operator + connected names = separate tokens. `System.out` → 3 tokens.
13. Statement terminator `;` NOT a token.
14. Manipulators `endl`, `"\n"` ARE tokens.
15. `*` in pointer declaration NOT a token.
16. `return` keyword NOT counted.
17. No built-in root class → Wi starts at 1.

---

## Q1 — CANONICAL Result Class (the 60 example)

**Question:** Calculate the WCC for the following Java program. Show the complete token count, identify all weights, and present your work in a table.

```java
public class Result {
    void outresult(int m) {
        if(m > -1 && m < 50)
            System.out.println("Fail");
        else
            System.out.println("Pass");
    }

    void main(String args[]) {
        Result r = new Result();
        r.outresult(50);
    }
}
```

**Worked Answer:**

Nesting diagram:
- Class `Result` (Wi base, but Rule 17 → Wi starts at 1)
  - Method `outresult` (1st level inside class → Wn=1 for method header)
    - if-else (1st level inside method → Wn=1)
      - println "Fail" (2nd level → Wn=2)... 

Actually — refer to slide convention: **method header = Wn=0**, body of method = Wn=1, body of if inside method = Wn=2. Different slides count slightly differently. The canonical answer uses Wn pattern below.

| Ln | Statement | Tokens | S | Wc | Wn | Wi | Wt | WC |
|----|-----------|--------|---|----|----|----|----|----|
| 1 | `public class Result {` | (skip — class decl) | — | — | — | — | — | — |
| 2 | `void outresult(int m){` | void, outresult() | 2 | 0 | 0 | 1 | 1 | 2 |
| 3 | `if(m > -1 && m < 50)` | if-else(), m, >, -1, &&, m, <, 50 | 8 | 1 | 1 | 1 | 3 | 24 |
| 4 | `System.out.println("Fail")` | Sys, ., out, ., println(), "Fail" | 6 | 0 | 1 | 1 | 2 | 12 |
| 5 | `else` | (skip) | — | — | — | — | — | — |
| 6 | `System.out.println("Pass")` | Sys, ., out, ., println(), "Pass" | 6 | 0 | 1 | 1 | 2 | 12 |
| 7 | `void main(String args[]){` | void, main() | 2 | 0 | 0 | 1 | 1 | 2 |
| 8 | `Result r = new Result();` | Result, r, =, new, Result() | 5 | 0 | 0 | 1 | 1 | 5 |
| 9 | `r.outresult(50);` | r, ., outresult() | 3 | 0 | 0 | 1 | 1 | 3 |

**WCC = 2 + 24 + 12 + 12 + 2 + 5 + 3 = 60** ⭐

---

## Q2 — Inheritance (Demonstrate Wi)

**Question:** Calculate the WCC for the `Puppy` class. Note the inheritance hierarchy.

```java
class Animal {
    void breathe() {
        System.out.println("breathing");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("woof");
    }
}

class Puppy extends Dog {
    void play(int energy) {
        if(energy > 0)
            System.out.println("running");
    }
}
```

**Hint:** Only compute for class `Puppy`. Wi is determined by depth from root (or starting at 1 by Rule 17 if no built-in root).

**Worked Answer:**

Inheritance level of `Puppy`:
- Animal = base (Rule 17 → Wi=1)
- Dog extends Animal → Wi=2
- Puppy extends Dog → **Wi=3**

| Ln | Statement | Tokens | S | Wc | Wn | Wi | Wt | WC |
|----|-----------|--------|---|----|----|----|----|----|
| 1 | `void play(int energy){` | void, play() | 2 | 0 | 0 | 3 | 3 | 6 |
| 2 | `if(energy > 0)` | if-else(), energy, >, 0 | 4 | 1 | 1 | 3 | 5 | 20 |
| 3 | `System.out.println("running")` | Sys, ., out, ., println(), "running" | 6 | 0 | 2 | 3 | 5 | 30 |

**WCC = 6 + 20 + 30 = 56**

**Interpretation:** Inheritance depth dramatically inflates WCC. A deep class hierarchy carries hidden complexity even when the code looks simple.

---

## Q3 — Nested Loops (Demonstrate Wn growth)

**Question:** Calculate WCC for:
```java
public class Matrix {
    void traverse(int n) {
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(i == j)
                    System.out.println(i);
            }
        }
    }
}
```

**Worked Answer:**

Nesting diagram:
```
Class Matrix (Wi=1, Rule 17)
└─ Method traverse() ........ Wn=0 (header)
   └─ for(i) ................ Wn=1
      └─ for(j) ............. Wn=2
         └─ if(i==j) ........ Wn=3
            └─ println ...... Wn=4
```

| Ln | Statement | Tokens | S | Wc | Wn | Wi | Wt | WC |
|----|-----------|--------|---|----|----|----|----|----|
| 1 | `void traverse(int n){` | void, traverse() | 2 | 0 | 0 | 1 | 1 | 2 |
| 2 | `for(int i=0; i<n; i++){` | for(), i, =, 0, i, <, n, i, ++ | 9 | 2 | 1 | 1 | 4 | 36 |
| 3 | `for(int j=0; j<n; j++){` | for(), j, =, 0, j, <, n, j, ++ | 9 | 2 | 2 | 1 | 5 | 45 |
| 4 | `if(i == j)` | if-else(), i, ==, j | 4 | 1 | 3 | 1 | 5 | 20 |
| 5 | `System.out.println(i)` | Sys, ., out, ., println(), i | 6 | 0 | 4 | 1 | 5 | 30 |

**WCC = 2 + 36 + 45 + 20 + 30 = 133**

**Insight:** Each nesting level multiplies the per-line WC. Deep nesting is the #1 WCC inflator. Refactor toward early-returns or extracted helper methods.

---

## Q4 — Switch (Demonstrate Wc = n)

**Question:** Calculate WCC for:
```java
public class Calculator {
    int compute(int op, int a, int b) {
        switch(op) {
            case 1: return a + b;
            case 2: return a - b;
            case 3: return a * b;
            default: return 0;
        }
    }
}
```

**Hint:** For `switch`, Wc = number of cases (n). Each `case :` counts as 2 tokens (Rule 10).

**Worked Answer:**

| Ln | Statement | Tokens | S | Wc | Wn | Wi | Wt | WC |
|----|-----------|--------|---|----|----|----|----|----|
| 1 | `int compute(int op, int a, int b){` | int, compute(), op, ',', a, ',', b | 7 | 0 | 0 | 1 | 1 | 7 |
| 2 | `switch(op){` | switch(), op | 2 | 3 | 1 | 1 | 5 | 10 |
| 3 | `case 1:` | case, ':', 1 | 3 | 0 | 2 | 1 | 3 | 9 |
| 4 | `return a + b;` | a, +, b (return NOT counted) | 3 | 0 | 2 | 1 | 3 | 9 |
| 5 | `case 2:` | case, ':', 2 | 3 | 0 | 2 | 1 | 3 | 9 |
| 6 | `return a - b;` | a, −, b | 3 | 0 | 2 | 1 | 3 | 9 |
| 7 | `case 3:` | case, ':', 3 | 3 | 0 | 2 | 1 | 3 | 9 |
| 8 | `return a * b;` | a, ×, b | 3 | 0 | 2 | 1 | 3 | 9 |
| 9 | `default :` | default, ':' | 2 | 0 | 2 | 1 | 3 | 6 |
| 10 | `return 0;` | 0 | 1 | 0 | 2 | 1 | 3 | 3 |

**WCC = 7 + 10 + 9 + 9 + 9 + 9 + 9 + 9 + 6 + 3 = 80**

Note: switch's Wc = n (here n=3 cases, not counting default). The case lines themselves have Wc=0 because they're not separate control structures — they're labels inside the switch.

---

## Q5 — Sub-Question Style (Definition + Calculation + Interpret)

**Question (typical 20-mark essay):**

**(a)** Define Weighted Composite Complexity (WCC). State its three weight components and the composite formula. **[5 marks]**

**(b)** Calculate the WCC for the following code, presenting your answer as a table showing S, Wc, Wn, Wi, Wt, and WC for each line. **[12 marks]**
```java
public class Account {
    void process(double bal) {
        if(bal > 1000)
            System.out.println("High");
        else if(bal > 0)
            System.out.println("Normal");
        else
            System.out.println("Overdrawn");
    }
}
```

**(c)** What does a higher WCC value indicate, and how can you reduce it? **[3 marks]**

**Worked Answer:**

**(a)** WCC measures program complexity by combining three weight components per executable line:
- **Wc (Control type weight):** 0 for sequential, 1 for branch (if-else), 2 for iterative, n for switch.
- **Wn (Nesting level weight):** depth of nesting, 0 (no nesting) up to n.
- **Wi (Inheritance level weight):** depth in class hierarchy, 0 for root or 1 if no built-in root class.

The per-line total weight is **Wt = Wc + Wn + Wi**, weighted by line size **WC = S × Wt** where S = token count. The program's WCC = **Σ WC** across all executable lines.

**(b)** Wi = 1 (Rule 17, no built-in root class).

| Ln | Statement | Tokens | S | Wc | Wn | Wi | Wt | WC |
|----|-----------|--------|---|----|----|----|----|----|
| 1 | `void process(double bal){` | void, process() | 2 | 0 | 0 | 1 | 1 | 2 |
| 2 | `if(bal > 1000)` | if-else(), bal, >, 1000 | 4 | 1 | 1 | 1 | 3 | 12 |
| 3 | `System.out.println("High")` | Sys, ., out, ., println(), "High" | 6 | 0 | 2 | 1 | 3 | 18 |
| 4 | `else if(bal > 0)` | if-else(), bal, >, 0 | 4 | 1 | 1 | 1 | 3 | 12 |
| 5 | `System.out.println("Normal")` | Sys, ., out, ., println(), "Normal" | 6 | 0 | 2 | 1 | 3 | 18 |
| 6 | `System.out.println("Overdrawn")` | Sys, ., out, ., println(), "Overdrawn" | 6 | 0 | 2 | 1 | 3 | 18 |

**WCC = 2 + 12 + 18 + 12 + 18 + 18 = 80**

**(c)** A higher WCC indicates that the code is harder to understand, test, and maintain. Drivers of high WCC are deep nesting, many control structures, large lines (high S), and deep inheritance. To reduce WCC:
- **Flatten nesting** by using early returns and guard clauses.
- **Extract helper methods** to reduce per-line size.
- **Avoid deep inheritance** chains — prefer composition over inheritance.
- **Replace nested if-else chains** with polymorphism or lookup tables.

---

# PATTERN SHORTCUTS (memorize for speed)

| Pattern | Tokens | Wc | Common WC at Wi=1 |
|---------|--------|-----|------|
| `void method() { ` (method header, Wn=0) | 2 | 0 | **WC = 2** (Wt = 0+0+1 = 1) |
| `System.out.println("X")` inside if (Wn=2) | 6 | 0 | **WC = 18** (Wt = 0+2+1 = 3) |
| `System.out.println("X")` inside method body (Wn=1) | 6 | 0 | **WC = 12** (Wt = 0+1+1 = 2) |
| `if(A && B)` (Wn=1) | 8 | 1 | **WC = 24** (Wt = 1+1+1 = 3) |
| `if(A)` (Wn=1) | 4 | 1 | **WC = 12** |
| `obj.method(N)` (Wn=1) | 3 | 0 | **WC = 6** |
| `Type x = new Type()` (Wn=1) | 5 | 0 | **WC = 10** |
| `for(int i=0; i<n; i++)` (Wn=1) | 9 | 2 | **WC = 36** (Wt = 2+1+1 = 4) |

---

# EXAM-DAY TIPS

1. **Always draw the nesting diagram FIRST** — it makes Wn assignment automatic and prevents off-by-one mistakes.
2. **Skip non-executables explicitly** in your answer ("Lines 1, 5, 7 are skipped because they are class declaration / else / closing braces"). Examiners give marks for this clarity.
3. **Show your token count for every line** — even a wrong final answer with clear tokens gets partial marks.
4. **State Rule 17 explicitly** when the class has no built-in root (no `extends`) — "Since `X` has no built-in root class, Wi = 1 (Rule 17)."
5. **For switch:** `Wc = n` where n = number of `case` labels (not counting default).
6. **For `&&` and `||`:** each counts as 1 separate token. (And in CC, each adds 1 decision.)
7. **`System.out.println("X")` = 6 tokens.** Always. Memorize this.
8. **`return` is NEVER a token.** Just count what comes after `return`.
9. **Cross-check** with CC or CFS if you finish early — if numbers feel wrong, recount tokens on the highest-WC line.
10. **Time budget:** 25 minutes for the metric essay if it's worth 20 marks.

---

# FINAL CHECKLIST BEFORE WRITING

- [ ] Identified all executable lines
- [ ] Drew nesting diagram
- [ ] Stated Wi value with reason (Rule 17 if no inheritance)
- [ ] Showed token count for every line
- [ ] Used the 9-step structure
- [ ] Showed WC formula `S × Wt` for at least one line
- [ ] Final WCC summed and boxed/bolded
- [ ] Interpreted the result (if asked)

**Good luck, Dilmith! 🎯**
