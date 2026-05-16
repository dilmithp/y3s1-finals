# Lecture 02 — Architectural Activities & Design Process

**Module:** SE3030 — Software Architecture · 3rd Year, Semester 1 · SLIIT  
**Lecturer:** Chathura R De Silva

> Welcome back! Lecture 1 was about *"what is software architecture?"*. This lecture is about *"how do we actually create one, and what does the process look like?"* Same friendly style — slow English, memory hooks, pro tips. Let's go. ☕

---

## What you should walk away knowing

By the end of this note you should be able to:

1. Explain **where architectures come from** (the 4 influences).
2. Draw and explain the **Architecture Business Cycle (ABC)**.
3. List the **7 architectural activities** an architect performs.
4. Describe the **standard engineering design process** and its **5 alternative strategies**.
5. Explain what makes a "good" architecture (hint: there is no universal "good").

> **Pro Tip — this lecture is process-heavy.** The exam loves to ask "list and explain the activities of an architect" or "list and explain the design strategies". Memorise the **lists** in this lecture cold — they're easy marks.

---

## 1. Where do Architectures come from?

An architecture is not created in a vacuum. The lecture says it is the result of a **set of business and technical decisions**, shaped by **four big influences**:

| # | Influence | Plain English explanation | Example |
|---|---|---|---|
| 1 | **Stakeholders** | The people who care about the system have different wants | **Management** wants low cost · **Marketing** wants fast time-to-market · **End users** want good UX & security |
| 2 | **Developing Organization** | The company building the system has its own situation | Past investments (you already paid for Oracle DB, so you keep using it) · Future investments planned · How teams are structured |
| 3 | **Experience & Background of the Architect(s)** | The architect's own skills and knowledge bias the design | Technical skills (knows AWS, doesn't know Azure) · Domain knowledge (banking? healthcare?) |
| 4 | **Technical Environment** | The current tech world around the project | Available software engineering techniques, practices, and processes |

> **Memory Hook — "S-DOE-T"** → **S**takeholders, **D**eveloping **O**rganization, **E**xperience, **T**echnical environment.  
> Or even simpler: think **"PEOPLE → ORG → ARCHITECT → TECH"** (zooming from outside in to the architect).

### The classic diagram (slide 4 — "Architect's Influences")

```
       Stakeholders ─┐
                     ├──→ Requirements (Qualities) ──┐
   Developing Org ──┘                                │
                                                     ▼
   Technical Environment ─────────────────→  ARCHITECT(s)  ──→ Architecture ──→ System
                                                     ▲
   Architect's Experience ──────────────────────────┘
```

The takeaway: the architect is a **funnel**. Many influences pour in, and a single architecture comes out the other side.

> **Pro Tip — exam diagram.** If asked to "draw the architect's influences", reproduce this diagram. The 4 boxes on the left, arrow into Architect, arrow out to Architecture → System. Easy 5 marks.

---

## 2. The Architecture Business Cycle (ABC) ⭐

This is the **headline concept** of the lecture. Memorise it.

### The big idea (slide 5)

> Software architecture is **a result of** technical, business, and social influences.  
> Its existence in turn **affects** the technical, business, and social environments **that subsequently influence future architectures**.  
> We call this cycle the **Architecture Business Cycle (ABC)**.

In plain English: architecture is a **feedback loop**. The world shapes the architecture → the architecture shapes the world → the new world shapes the next architecture.

### The diagram (slide 6)

It's the **same** architect's-influence diagram from before, but now with **arrows going back from System → Influences**. That's literally the difference.

```
   Influences ────→ Architect ────→ Architecture ────→ System
        ▲                                                  │
        │                                                  │
        └──────────── (feedback) ──────────────────────────┘
```

> **Memory Hook — "Cycle, not arrow."** Architecture is not a one-way arrow from requirements to system — it is a **circle**. Successful systems change companies, change customers, change the architect — and those changes feed the next system.

### Real-world example to make it click
Netflix built a microservices architecture (influenced by their need to scale streaming). That architecture's *success* then influenced:
- The whole industry's belief in microservices (technical environment changed).
- Netflix's hiring (org structure changed — they now hire for distributed systems).
- Customer expectations (users now expect 99.99% uptime everywhere).
- The next generation of Netflix systems (they evolved to even more decoupled designs).

That whole loop is the ABC in action.

---

## 3. Ramifications of Architecture (the "back arrow")

Slide 7 explains the *"what does the architecture affect?"* side of the cycle. **5 things:**

| # | Affected thing | What changes |
|---|---|---|
| 1 | **Structure of the developing organization** | Team layout, the specialised skills needed in each team |
| 2 | **Goals of the development organization** | If the system succeeds/fails, the company may pivot, enter new markets, drop products |
| 3 | **Future customer requirements** | Users start expecting features they didn't know they wanted (e.g., Uber's tracking made customers expect real-time tracking everywhere) |
| 4 | **The Architect** | The architect gains more experience — which they bring to the next system |
| 5 | **Development Process & Culture** | The org adopts new processes (e.g., adopting DevOps because you moved to microservices) |

> **Memory Hook — "OGRA-PC"** → **O**rg structure, **G**oals, **R**equirements (future), **A**rchitect, **P**rocess **C**ulture. Ugly word = memorable!

> **Pro Tip — likely exam question:** "Explain the Architecture Business Cycle with examples." → Talk about the **two-way arrows** (influences → architecture, architecture → influences) and use the 5 ramifications as your examples.

---

## 4. Architectural Activities (the 7-step list) ⭐⭐⭐

This is the **most exam-critical list** in the lecture. **Memorise the 7 activities in order.**

```
1. Creating the Business Case for the System
2. Understanding the Requirements
3. Creating or Selecting the Architecture
4. Documenting and Communicating the Architecture
5. Analyzing or Evaluating the Architecture
6. Implementing the system based on the Architecture
7. Ensuring that the implementation Conforms to the Architecture
```

> **Memory Hook — "Big Umbrella Covers Daring Architects, Including Critics"**  
> **B**usiness case · **U**nderstanding requirements · **C**reating architecture · **D**ocumenting · **A**nalyzing · **I**mplementing · **C**onforming  
> = **B U C D A I C** → silly but it sticks.
>
> Or, more naturally, group them:
> - **Before** building: 1 (Business Case) + 2 (Requirements)
> - **Designing**: 3 (Create) + 4 (Document) + 5 (Evaluate)
> - **After** designing: 6 (Implement) + 7 (Conform)

Now let's walk through each one slowly.

---

### Activity 1 — Creating the Business Case for the System

The "why are we even building this?" step.

The architect (or someone) must answer:
- What's the market need?
- How much should the product cost?
- Who is the target market?
- What is the time-to-market deadline?
- Does it need to interface with other systems?
- Are there limitations (regulation, hardware, legacy)?

**Important note from the slide:** The architect **does not decide** these alone — but if the architect **is not consulted**, the business goals may become **impossible to achieve**.

> **Why?** Because a salesperson might promise "we'll deliver in 3 months for $10k" — and only an architect can spot that the architecture needed for the promised features would take 9 months and cost $80k.

> **Pro Tip — easy 2 marks:** State this idea in any "role of architect" question: *"The architect must be consulted early in business case creation, otherwise business goals may be infeasible."*

---

### Activity 2 — Understanding the Requirements

You can't design a system without understanding what it must do. The lecture splits this into two:

**Functional requirements** (what the system does):
- **OOAD (Object-Oriented Analysis & Design)** uses **Scenarios / Use Cases**.
- **Safety-critical systems** (medical, aviation) use **Finite-State Machine models** or **Formal Specification Languages** — because lives are on the line, you need mathematical proof.

**Non-functional requirements** (the "-ilities" — the qualities):
- **Quality Attribute Scenarios** (we'll learn this in detail in a later lecture)
- **Prototyping** — build a small thing first to see if it can be made fast/secure/scalable enough.
- **Domain Modeling** — model the business domain to surface hidden quality needs.

> **Memory Hook:**  
> Normal app → **Use Cases**.  
> Plane / pacemaker → **Formal methods** (no room for "oops").  
> Qualities → **Scenarios + Prototypes + Domain modeling**.

---

### Activity 3 — Creating or Selecting the Architecture

The actual "design the thing" step. The slide shows a flowchart — let me walk you through it:

```
   System Requirements & Project Context
                 │
                 ▼
          Requirements Analysis ◄──── NO (loop back)
                 │
                 ▼
       Architectural significant aspects
                 │
                 ▼
           Decision-Making
                 │
                 ▼
      Candidate SW components & inter-relations
                 │
                 ▼
        Architectural Evaluation
                 │
                 ▼
          Evaluation description
                 │
                 ▼
        ┌──────────────────┐
        │ Architecture     │── YES ──→ DONE
        │ acceptable?      │── NO  ──→ back to Requirements Analysis
        └──────────────────┘
```

The big idea: it is an **iterative loop**. You design, you evaluate, you redesign. You don't get it right the first time. ✋ This is normal.

> **Pro Tip — exam diagram.** If asked "describe the process of creating an architecture", redraw this simple loop and label each box. The arrows + the *YES/NO* branch are the marks-earners.

---

### Activity 4 — Documenting and Communicating the Architecture

If only the architect understands the architecture, the architecture is **useless**. It must be **communicated clearly and unambiguously** to all stakeholders.

Different stakeholders need different things from the documentation:

| Stakeholder | What they need to understand |
|---|---|
| **Developers** | The work assignments — *what they have to build* |
| **Testers** | The task structure — *what they have to test and how things are broken into testable units* |
| **Management** | The scheduling implications — *how long will each piece take? Who blocks whom?* |

**Golden rule:** *Architectural documentation should be informative, unambiguous, and readable by many people with varied backgrounds.*

> **Memory Hook — "DTM"** → **D**evelopers, **T**esters, **M**anagement. Three audiences, one document set.

> **Pro Tip:** If a case study mentions confused developers or missed deadlines, "poor architecture documentation" is a strong candidate for the root cause.

---

### Activity 5 — Analyzing or Evaluating the Architecture

You will always have **multiple candidate designs**. Some are obviously bad and dropped fast; the rest *"contend for primacy"* (compete to win).

> Choosing among them rationally is *"one of the architect's greatest challenges."* — direct quote from the slide. Underline it.

The lecture mentions **two formal methods** (you'll meet ATAM again in detail later):

| Method | Focus |
|---|---|
| **ATAM** — Architecture Tradeoff Analysis Method | The **most mature** methodology. Helps balance quality-attribute tradeoffs. |
| **CBAM** — Cost Benefit Analysis Method | Focuses on the **economic implications** of architectural decisions. |

> **Memory Hook — "A for Architecture, C for Cost"** → ATAM = quality tradeoffs, CBAM = cost. Easy.

> **Pro Tip — exam ready phrase:** *"ATAM is the most mature methodology for evaluating architectural tradeoffs, while CBAM is used when economic implications are dominant."* Memorise verbatim.

---

### Activity 6 — Implementing the System Based on the Architecture

The architecture is no good if developers ignore it. The architect must ensure devs stay **faithful to the structures and interaction protocols** the architecture defines.

The **environment** (tools, processes, training) should help devs *follow* the architecture rather than fight it.

**Architect's involvement at this stage:**

- **Technology & technical infrastructure** — choose & set up (DBs, message brokers, CI/CD).
- **Software engineering processes** — set up code review rules, branching strategy, etc.
- **Creating the team** — identify technical specialists; spot **skill gaps** and address them via **training**.

> **Pro Tip:** If a case study says *"developers keep doing X instead of Y as the architect intended"*, the issues are usually: (a) bad documentation, (b) wrong tools, or (c) lack of training. Use this.

---

### Activity 7 — Ensuring the Implementation Conforms to the Architecture

Slide is short but the point is sharp:

> **Constant vigilance** is required to keep the *actual* architecture and the *documented* architecture in sync — **especially in the maintenance phase**.

Real systems decay over time. Developers take shortcuts. Bugs are patched in the wrong place. Slowly the *real* system drifts away from the *intended* architecture — this is called **architecture drift / architectural erosion**.

> **Memory Hook — "What's drawn ≠ what's built (eventually)."** The architect's job is to keep these two in sync.

---

## 5. What makes a Good Architecture?

A liberating idea from slide 16:

> **There is no such thing as an inherently good or bad architecture.**

Architectures are *more or less fit* for a **stated purpose**. A microservices architecture is "great" for Netflix and "terrible" for a 4-person startup. Same architecture, different verdict — because the **goals** are different.

So how do we evaluate them?

### Rule-of-thumb recommendations

**Process recommendations** (how you go about designing):
- Identify both **functional requirements** AND the **high-priority quality attributes**.
- **Analyse and formally evaluate** *before* it's too late to change. (Once code is written and deployed, changing architecture is expensive!)

**Product recommendations** (properties of the design itself):
- Use software principles like **Information Hiding** (don't expose what doesn't need to be exposed) and **Separation of Concerns** (each module does one thing).
- Write tasks/processes to allow **easy reallocation** — possibly at **runtime** (e.g., move a process to a different machine without rewriting).

> **Memory Hook:**  
> "Good" = **fit for purpose**.  
> Process side → **identify qualities + evaluate early**.  
> Product side → **hide info, separate concerns, stay flexible**.

> **Pro Tip — exam trap:** Never write "the best architecture is microservices" or "the best architecture is layered". *There is no universally best architecture*. Always answer in terms of the **stated goals / quality attributes**.

---

## 6. Architectural Design Process — Objectives

Slide 17 introduces three objectives of the design process:

1. **Creativity** — enhance your skillset, give you new tools to design with.
2. **Method** — focus on **highly effective techniques** (don't reinvent the wheel).
3. **Judgment** — know **when to invent a novel solution** vs. **when to follow a proven method**.

> **Memory Hook — "Creative, Methodical, Judgemental"** → balance of art + science + wisdom.

The deepest skill of an architect is **judgement** — knowing when to be creative and when to be boring. Boring is often correct.

---

## 7. The Standard Engineering Design Process (4 stages)

Slide 18. This is the **classic textbook linear process** for engineering design — applies beyond just software.

| Stage | What happens |
|---|---|
| **1. Feasibility** | Identify a set of **feasible concepts** for the design as a whole. ("What designs are even possible?") |
| **2. Preliminary design** | Select and develop the **best concept** from those. |
| **3. Detailed design** | Develop full **engineering descriptions** of the chosen concept. |
| **4. Planning** | Evaluate and **alter** the concept to fit **production, distribution, consumption, and retirement** needs. |

> **Memory Hook — "F P D P"** → Feasibility, Preliminary, Detailed, Planning. Or just remember: **brainstorm → pick → detail → plan**.

---

## 8. Potential Problems with the Standard Process

Slide 19 — the standard linear process **breaks down** when:

1. The designer **cannot produce any feasible concepts** → progress just stops.
2. The problem is **too big and complex** → one person can't do steps 1–2 well anymore.
3. The standard approach doesn't handle **system design** (where the *relationship between multiple products* matters, not just one product).
4. As **complexity** grows or **experience** is limited → must adopt **alternative approaches**.

> **Pro Tip — exam framing:** When asked "why isn't the standard linear design process always enough?", give these 4 points.

---

## 9. Alternative Design Strategies ⭐ (5 strategies)

Slide 20. The lecture lists **5 strategies** — memorise them and their one-line definitions.

| Strategy | Behaviour | When to use |
|---|---|---|
| **1. Standard** | **Linear** model — feasibility → preliminary → detailed → planning. No going back. | Simple, well-understood problems. |
| **2. Cyclic** | Process can **revert** to an earlier stage if needed. | When you discover problems mid-design and need to redo earlier steps. |
| **3. Parallel** | **Independent alternatives** are explored **in parallel** at the same time. | When you have time and resources and you want to compare options seriously. |
| **4. Adaptive** | "Lay tracks as you go" — the **next strategy** is decided **at the end of the current stage**. | When you don't know upfront what approach will work. |
| **5. Incremental** | Each stage = **incrementally improving** the existing design. | When you're evolving a legacy/existing system step by step. |

> **Memory Hook — "Steam Cars Park After Idling"**  
> **S**tandard · **C**yclic · **P**arallel · **A**daptive · **I**ncremental.

### A picture in your head for each:

```
Standard    : A → B → C → D                    (straight line)
Cyclic      : A → B → C → ↩ → B → C → D       (loops back)
Parallel    : A → [B1 | B2 | B3] → pick → C    (3 paths at once)
Adaptive    : A → ? → (decide next) → ?        (decide as you go)
Incremental : A → A' → A'' → A'''              (small improvements)
```

> **Pro Tip — easy 10 marks:** "List and explain 5 design strategies with examples." This is a textbook list question. Just give the table above and add one example each.

---

## 10. Identifying a Viable Strategy

Slide 21. How do you *pick* one? Three guides:

1. **Use fundamental design tools** — **abstraction** and **modularity**.
2. **Inspiration** where needed, **predictable techniques** elsewhere. (Translation: be creative in the *new* / *unknown* parts, but use *boring proven methods* in the *known* parts.)
3. **Apply your own experience** — or **borrow others' experience** (e.g., from patterns, books, ex-colleagues).

> **Memory Hook — "Abstract → Inspire → Imitate"**  
> Abstraction & modularity first → creativity where required → reuse experience where possible.

---

## 11. Tools & Patterns of Software Engineering (slide 22)

Three big tools the lecturer highlights:

### Tool 1 — Abstraction (two directions)
- **Abstraction (1)** — look at *details* and abstract **UP** to concepts. ("Bottom-up": see lots of similar code → extract a common interface.)
- **Abstraction (2)** — choose *concepts* first, then add detailed substructure **DOWN**. ("Top-down": decide you need a "Payment Service", then design its internals.)

> **Memory Hook:** **Abstraction = either climbing the ladder (UP) or descending it (DOWN).**

### Tool 2 — Separation of Concerns
Each module/component should focus on **one concern** (one responsibility). Don't mix UI logic with database logic with business rules. Classic example: don't put SQL queries inside your HTML.

### Tool 3 — Architectural Patterns & Styles (we'll learn these in detail later)
- **Layered** — Presentation → Business → Persistence (you saw this in Lec 1).
- **Model-View-Controller (MVC)** — separates data (Model) from display (View) from input handling (Controller). Very common in web frameworks.
- **Client-Server** — clear split between requester and provider.

> **Pro Tip:** Whenever a question asks "what tools / principles guide architectural design?" → answer with **Abstraction**, **Separation of Concerns**, and **proven Patterns/Styles**.

---

## 12. Controlling the Design Strategy (slide 23) — 5 controls

When you're exploring many designs, things get chaotic. The lecturer gives **5 controls** to keep the design activity healthy:

| Control | What it means |
|---|---|
| **Manage the Activity** | Don't let exploration spiral — actively manage it. |
| **Review** | Identify and **review the critical decisions**. Don't slip them through quietly. |
| **Cost** | Weigh the **cost of research/design** against the **penalty of being wrong**. Spend more time when the cost of error is high. |
| **Enforce** | **Insulate uncertain decisions** — wrap them so they can be changed later without affecting everything else. |
| **Cross-check with Requirements** | Continually re-check the requirements as the design exploration reveals new info. |

> **Memory Hook — "MR. CEC"** → **M**anage, **R**eview, **C**ost, **E**nforce, **C**ross-check.

> **Pro Tip:** "Insulate uncertain decisions" is a beautiful idea — it's the same principle behind interfaces, dependency injection, and microservices boundaries. If you don't know if you'll keep using MySQL forever, put a clean interface in front of it so you can swap it later.

---

## 13. Insights from Requirements (slide 24)

Three observations:

1. New architectures are often built **based on experience** with previous ones (and improving them).
2. Requirements can use a **vocabulary of known architectural choices** — e.g., a requirement might literally say *"the system shall use REST APIs"*, which is already an architectural choice.
3. So past designs **directly influence** new design — many critical decisions are **identified or made as requirements** before the architect even starts designing.

In short: **you rarely design from scratch.** Most architectures are evolutions of previous ones.

---

## 14. Insights from Implementation (slide 25)

The "reality check" stage — what implementation tells the designer:

- **Implementation constraints shape the design.** Even *external* constraints can force decisions:
  - Use of a particular **middleware**
  - Use of a particular **programming language**
  - **Software reuse** mandates (e.g., "must reuse the existing auth library")
- **Design and implementation can proceed cooperatively** — don't strictly do design *then* code.
- **Initial partial implementation** can give **critical performance / feasibility information** before you finalise the design. (This is essentially the argument for **prototyping**.)

> **Memory Hook — "Code teaches design."** You learn things by writing some code that you'd never learn from staring at diagrams.

---

## 15. Quick Comparison Summary

A handy table for revision — the **three big lists** from this lecture, side by side:

| Influences (4) | Activities (7) | Design Strategies (5) |
|---|---|---|
| Stakeholders | Business Case | Standard (linear) |
| Developing Org | Requirements | Cyclic |
| Architect's Experience | Create/Select Architecture | Parallel |
| Technical Environment | Document & Communicate | Adaptive |
| | Analyze/Evaluate | Incremental |
| | Implement | |
| | Conformance | |

> **Pro Tip — exam night.** If you only have 10 minutes left to revise this lecture, memorise these **three columns**. They produce ~80% of the exam marks from this lecture.

---

## 16. One-Shot Summary (the morning of the exam)

> Architectures are **shaped by 4 influences** — stakeholders, developing organization, architect's experience, and technical environment. These influences flow through the architect and produce the architecture, which in turn flows *back* and reshapes those same influences — that closed loop is the **Architecture Business Cycle (ABC)**. The architect performs **7 activities**: creating the **business case**, understanding **requirements**, **creating/selecting** the architecture, **documenting & communicating** it, **analyzing & evaluating** (using methods like **ATAM** for quality tradeoffs and **CBAM** for economics), **implementing** it (selecting tech, setting up processes, building the team), and **ensuring conformance** during maintenance. There is **no inherently good or bad architecture** — only "fit for stated purpose". The **standard linear engineering design process** (feasibility → preliminary → detailed → planning) breaks under complexity, so we have **5 alternative strategies**: standard, cyclic, parallel, adaptive, and incremental. Designers use **abstraction**, **separation of concerns**, and known **patterns/styles** as core tools, manage exploration with **MR. CEC** controls (Manage, Review, Cost, Enforce, Cross-check), and learn from both **requirements** (past architectures inform new ones) and **implementation** (code teaches design).

---

## 17. Likely Exam Questions (and how to answer)

**Q1. Explain the Architecture Business Cycle (ABC).**  
→ Define it (two-way feedback loop), draw the diagram (influences → architect → architecture → system → back to influences), and use the **5 ramifications** as examples of the back-arrow.

**Q2. List and describe the 7 architectural activities.**  
→ Bullet list with 1–2 sentences each. Use the **B-U-C-D-A-I-C** order.

**Q3. What are the influences on a software architect?**  
→ The **4 influences** (Stakeholders, Developing Org, Experience, Technical Environment). Give one example for each.

**Q4. List and explain 5 alternative design strategies.**  
→ Standard, Cyclic, Parallel, Adaptive, Incremental — with one-line definitions and when to use.

**Q5. Compare ATAM and CBAM.**  
→ ATAM = mature method for quality-attribute tradeoffs. CBAM = focused on economic/cost implications. ATAM answers "is this good?", CBAM answers "is this worth it?".

**Q6. "There is no good or bad architecture." Discuss.**  
→ Agree, then explain: architectures are *fit for stated purpose*. Same architecture can be excellent for one project and terrible for another (e.g., microservices for Netflix vs for a 4-person startup). Always evaluate **in context**.

**Q7. What are the controls used when managing the design strategy?**  
→ **MR. CEC** — Manage, Review, Cost, Enforce, Cross-check.

---

## 18. Vocabulary You Should Use Confidently

- **Architecture Business Cycle (ABC)** — feedback loop between architecture and its environment.
- **Stakeholder** — anyone who has an interest in the system (mgmt, marketing, users, ops, regulators).
- **Quality Attribute Scenario** — a structured way to specify a non-functional requirement.
- **Use Case / Scenario** — way to capture functional requirements (OOAD).
- **Formal Specification Language** — mathematical specification (used in safety-critical systems).
- **ATAM** — Architecture Tradeoff Analysis Method.
- **CBAM** — Cost Benefit Analysis Method.
- **Architecture Drift / Erosion** — when the implemented system slowly diverges from the documented architecture.
- **Information Hiding** — don't expose what doesn't need to be public.
- **Separation of Concerns** — one module = one responsibility.
- **Abstraction** — reasoning at a higher level by hiding details (or zooming in by adding them).
- **Middleware** — software between OS and apps (e.g., message brokers, ORMs).

---

## 19. References

- Bass, Clements, & Kazman — *Software Architecture in Practice* (2nd ed.).
- http://www.ece.ubc.ca/~matei/EECE417/BASS/ch01.html
- http://www.ics.uci.edu/~taylor/classes/211/DesignAndArchitecture.pdf

---

**Pro Tip — connection back to Lecture 1.** Lecture 1 said architecture = Style + Quality Attributes + Decisions + Principles (**SQDP / Squid P**). Lecture 2 zooms out and asks *how* you produce that SQDP — through **4 influences → 7 activities → various design strategies**. The two lectures lock together perfectly.

Send Lecture 3 whenever you're ready. 🚀
