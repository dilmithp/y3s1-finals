# Lecture 12 — Software Architecture Frameworks

**Module:** SE3030 — Software Architecture · 3rd Year, Semester 1 · SLIIT  
**Lecturer:** Chathura R De Silva

> 🎓 **The final lecture!** This one zooms out from "designing one system" to "managing architecture across an entire enterprise". The two big frameworks are **Zachman** and **TOGAF** — both touched on briefly in Lec 3, but here we go deep. The 2025 paper didn't directly test these, but they could appear (they did in earlier years), so it's worth understanding the headlines. ☕

---

## What you should walk away knowing

1. What **Enterprise Architecture (EA)** is and why it matters.
2. The **4 key Architecture Principles** every architect should follow.
3. The **2 major Enterprise Architecture frameworks**: **Zachman** and **TOGAF**.
4. **TOGAF's ADM** (Architecture Development Method) — its **9 phases**.
5. **Zachman's 6×6 ontology** (Why · How · What · Who · Where · When × 6 perspectives).
6. When to use each framework.

> **Pro Tip:** If asked about EA frameworks, the safest answer pairs **Zachman (the *what* — a classification ontology)** with **TOGAF (the *how* — a step-by-step process)**. They complement, not compete.

---

## 1. Why Software Architecture? (Quick recap from Lec 1)

The lecture opens with a refresher:
- Provides a **standard governing structure**.
- Provides **solutions to known problems**.
- Helps make projects **successful**.
- Addresses risks: failing to consider key scenarios, design for common problems, or appreciate long-term consequences.
- Makes products **easy to maintain**.

> **Memory Hook:** *"Architecture = governance + reuse + risk management + maintainability."*

---

## 2. When Do We Need to "Architect"?

3 triggers from the lecture:

| Trigger | Why it matters |
|---|---|
| **The solution gets bigger** | Modern software is far more complex than yesterday's |
| **You have to think about the future** | Software lasts longer — data especially is no longer "throw-away" |
| **Increased usage and usage types** | Earlier only direct users interacted with software; now systems interact with each other |

> **Pro Tip — exam phrase:** *"Software architecture becomes essential as systems grow in complexity, longevity, and interconnectedness."*

---

## 3. Enterprise Architecture (EA) ⭐

> **Definition:** *"A well-defined practice for conducting **enterprise analysis, design, planning, and implementation**, using a **holistic approach** at all times, for the successful development and execution of strategy."*

In simpler words: **EA = applying architectural thinking to the WHOLE organisation**, not just one piece of software.

It guides organisations through **business, information, process, and technology changes** needed to execute their strategies.

> **Memory Hook:** *"Software architecture designs an app. Enterprise architecture designs the company's IT brain."*

### Benefits of EA

**Business Benefits:**
- Helps achieve business strategy
- **Faster time to market** for new innovations
- More **consistent business processes** across business units
- More **reliability + security**, less **risk**

**IT Benefits:**
- Better **traceability of IT costs**
- **Lower IT costs** (design, buy, operate, support, change)
- **Faster design and development**
- Less **complexity**
- Less **IT risk**

> **Memory Hook:** *"Business wins faster + cheaper + safer. IT wins cleaner + cheaper + less stressful."*

---

## 4. The 4 Key Architecture Principles ⭐

Every architect — software or enterprise — should internalise these 4:

| # | Principle | What it means |
|---|---|---|
| 1 | **Build to change instead of building to last** | Anticipate change. Build flexibility for future requirements. |
| 2 | **Model to analyse and reduce risk** | Use design tools (UML) to visualise. Capture decisions, analyse impact. **Don't over-formalise** — keep adaptability. |
| 3 | **Communication and Collaboration** | Use **visualisations** to communicate the architecture and design changes to all stakeholders. |
| 4 | **Identify key engineering decisions** | Know **where mistakes are most often made**. Get those right the **first time** — late changes are always costly. |

> **Memory Hook — "BMC-I"** → **B**uild to change · **M**odel to analyse · **C**ommunicate · **I**dentify key decisions.

> **Pro Tip — exam phrase:** *"Modern architecture principles emphasise **building for change** rather than longevity, **modelling to manage risk**, **communicating with stakeholders visually**, and **focusing effort on the few decisions** that are most expensive to get wrong."*

---

## 5. Enterprise Architecture Frameworks — A Short History

### Zachman Framework (1987)
- John Zachman, working at **IBM**, published *"A Framework for Information Systems Architecture"* in 1987.
- Provided a **classification scheme** for artifacts describing the **What, How, Where, Who, When, and Why** of information systems.
- Often considered the **first** EA framework in the public domain (1982 first mention).

### TOGAF (1994 → today)
- In 1994, **The Open Group** selected **TAFIM** (from the US Department of Defense) as a basis for **TOGAF (The Open Group Architecture Framework)**.
- "Architecture" in TOGAF means **IT architecture**.
- Most widely used EA framework today.

> **Memory Hook:** *"Zachman = classification ontology (the WHAT). TOGAF = step-by-step process (the HOW)."*

---

## 6. TOGAF — The Open Group Architecture Framework ⭐⭐

### Definition
> *"TOGAF is a framework for **enterprise architecture** that provides an approach for **designing, planning, implementing, and governing** an enterprise IT architecture."*

### TOGAF's 4 Levels

TOGAF models architecture at **4 levels**:

| Level | What it covers |
|---|---|
| **Business** | Business processes, workflows |
| **Application** | Applications + their interactions |
| **Data** | Data models + data flows |
| **Technology** | Hardware, networks, platform services |

> **Memory Hook — "BADT"** → **B**usiness · **A**pplication · **D**ata · **T**echnology.

### TOGAF Components (3 main pieces)
1. **Architecture Development Method (ADM)** ← the heart of TOGAF — a step-by-step process
2. **Enterprise Continuum** — a virtual repository of architecture assets
3. **Resource Base** — guidelines, templates, examples

### Key TOGAF Principle
> *"TOGAF relies heavily on **modularization**, **standardization**, and **already existing proven technologies and products**."*

---

## 7. TOGAF ADM — Architecture Development Method ⭐⭐⭐

The **ADM** is a **step-by-step iterative cycle** for developing or changing an architecture. It has **9 phases** (Preliminary + A through H) plus a continuous **Requirements Management** activity in the centre.

```
                    ┌─────────────┐
                    │ Preliminary │  ← Frameworks & Principles
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  A: Vision  │  ← Architecture Vision
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ B: Business │
                    │   Architect │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐    ┌──────────────────┐
                    │ C: InfoSys  │    │   Requirements   │
                    │  Architect  │◄──►│   Management     │
                    └──────┬──────┘    │   (centre/loop)  │
                           │           └──────────────────┘
                    ┌──────▼──────┐
                    │ D: Tech     │
                    │  Architect  │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ E: Opports  │  ← How to deliver
                    │ & Solutions │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ F: Migrate  │  ← Implementation plan
                    │     Plan    │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ G: Implem.  │  ← Architectural oversight
                    │  Governance │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ H: Change   │  ← Change management
                    │  Management │
                    └──────┬──────┘
                           │
                          (loop back to A or beyond)
```

### The 9 Phases Explained ⭐

| Phase | Name | What it does | Output |
|---|---|---|---|
| **Preliminary** | Setup | Define framework + principles. Tailor TOGAF. | **Request for Architecture Work** |
| **A** | **Architecture Vision** | Sell the benefits to stakeholders + decision-makers. Outline vision + business goals + drivers + constraints. | **Statement of Architecture Work** |
| **B** | **Business Architecture** | Identify Target Business Architecture. Show ROI. | Business models · Activity/Process models · Use Cases |
| **C** | **Information Systems Architecture** | Two sub-architectures: **Data Architecture** (Class diagrams, ER diagrams) + **Applications Architecture** (Component diagrams) | **Architecture Definition Document** |
| **D** | **Technology Architecture** | Structure + interaction of platform services. Logical + physical tech components. | Baseline Tech Architecture · Network/Computing/Hardware view · Communications view · Processing view · **Technology Architecture Report** |
| **E** | **Opportunities and Solutions** | How to **deliver** the target architecture. Incremental conversion if change is large. **First complete Architecture Roadmap.** | High-level Implementation Plan · High-level Migration Plan · Impact Analysis |
| **F** | **Migration Plan** | Detailed Implementation + Migration Plan. Coordinated with change management, business planning, portfolio management, ops management. | Detailed Migration Plan |
| **G** | **Implementation Governance** | Architectural **oversight to implementation**. Ensure project conforms to target architecture. Compliance reviews. | **Architecture Contract Document** |
| **H** | **Architecture Change Management** | Continuous monitoring. Manage change requests (governance, new tech, business changes). Decide whether change = simple update OR full re-architecture. | Architecture updates · Changes to framework/principles · New Request for Architecture Work |
| **(centre)** | **Requirements Management** | Continuous, ongoing. Sits in the **centre** of ADM. Requirements produced/analysed/reviewed in **every** phase. | Changed requirements · Requirements Impact Statement |

> **Memory Hook — "Pre-A B C D E F G H + RM"** → 9 phases + Requirements Management always at the centre.
>
> **Story version:** *"Setup (Pre) → Vision (A) → Business (B) → InfoSys (C) → Technology (D) → How to deliver (E) → Plan migration (F) → Implement with governance (G) → Manage changes (H) — and Requirements Management oversees them all."*

> **Pro Tip — likely exam question:** *"Explain TOGAF ADM and its phases."* → Use the diagram + the 9-row table. Mention Requirements Management is **continuous, central**, and **not** a one-off phase.

---

## 8. Zachman Framework ⭐⭐

### Definition
> *"Zachman Framework is an **enterprise ontology** and a fundamental structure for **Enterprise Architecture** which provides a **formal and structured way of viewing and defining an enterprise**."*

It's a **2-dimensional classification schema**:

```
                        ZACHMAN FRAMEWORK = 6 × 6 MATRIX
                        
                    Why    How    What    Who    When    Where
                    ────  ────  ────  ────  ────  ────
   Row 1: Scope (Planner's View)
   Row 2: Enterprise Model (Owner's View)
   Row 3: System Model (Designer's View)
   Row 4: Technology Model (Builder's View)
   Row 5: As Built (Integrator's View / Sub-Contractor)
   Row 6: Functioning Enterprise (User's View)
```

### The 2 Dimensions

**Dimension 1 — Columns (the 6 Interrogatives — what to model):**
| Column | Question | Models |
|---|---|---|
| **Why** | Motivation | Goals, motivations, business rules |
| **How** | Function | Processes, functions |
| **What** | Data | Data, things, entities |
| **Who** | People | Roles, organisation, stakeholders |
| **When** | Time | Cycles, events, schedules |
| **Where** | Network | Locations, geography |

> **Memory Hook for columns — "5W + 1H"** → the journalist's questions.

**Dimension 2 — Rows (the 6 Perspectives — who's looking):**
| Row | Perspective | Whose view |
|---|---|---|
| **Row 1: Scope** | **Contextual** | Planner |
| **Row 2: Enterprise Model** | **Conceptual** | Owner / Business mgmt |
| **Row 3: System Model** | **Logical** | Designer / Architect |
| **Row 4: Technology Model** | **Physical** | Builder / Engineer |
| **Row 5: As Built** | **As-Built / Detailed Representations** | Integrator / Sub-contractor |
| **Row 6: Functioning Enterprise** | **Functioning Instances** | User |

> **Memory Hook for rows:** Top row = "Why are we doing this?" (Scope) → bottom row = "How does it actually run?" (Functioning).

### What each cell contains
Each of the **36 cells** holds an **artifact** describing one column for one perspective. Examples:

- **Row 1, "What"** = High-level data classes related to each function.
- **Row 3, "How"** = Logical representation of information systems and their relationships.
- **Row 4, "Where"** = Network devices and their relationships.
- **Row 6, "When"** = Timing definitions operating to sequence activities.

### Row-by-row summary

| Row | Why | How | What | Who | When | Where |
|---|---|---|---|---|---|---|
| **1. Scope** (Planner) | Business goals & objectives | High-level functions | High-level data classes | Stakeholders | Cycles & events | Locations |
| **2. Enterprise** (Owner) | Policies & standards per process | Business processes | Business data | Roles per process | Events per process | Locations per process |
| **3. System** (Designer) | Business rule policies | Logical info systems | Logical data models | Logical access privileges | Logical events & responses | Logical distributed arch |
| **4. Technology** (Builder) | Rules constrained by IT standards | App specs on platforms | DBMS, logical data models | Access privileges to tech | Trigger specs | Network devices |
| **5. As Built** (Integrator) | Rules constrained by tech standards | Programs coded for platforms | Physical data definitions | Access controls | Coded timing | Configured devices |
| **6. Functioning** (User) | Operating characteristics | Functioning code | Actual DB values | Personnel | Sending/receiving messages | Operational timing |

> **Pro Tip — exam phrase:** *"Zachman is a **classification ontology** — it tells you **WHAT artifacts you need** at each perspective level. It's not a process; for the process, you use TOGAF ADM."*

---

## 9. Zachman vs TOGAF — How They Complement ⭐

| | **Zachman** | **TOGAF** |
|---|---|---|
| Type | **Ontology / Classification** | **Process / Method** |
| Tells you | **WHAT** to document | **HOW** to develop the architecture |
| Structure | 6 × 6 matrix of artifacts | 9-phase ADM cycle |
| Year | 1987 | 1994 |
| Best for | Cataloguing artifacts | Step-by-step development |
| Use together? | **YES** — Zachman tells you what cells to fill, TOGAF tells you the process | |

> **Memory Hook:** *"Zachman is the cabinet (with labelled drawers). TOGAF is the manual (telling you how to fill them)."*

---

## 10. The 2 Worked Exercises (slide 16, 18)

### Exercise 1 — Vehicle Ownership

**Brief:** Many vehicle types (cars, vans, bikes…). A person may own a vehicle for a given time, registered at the Department of Motor Vehicles.

**Approach to building Data Architecture:**
1. **Requirement clarification meetings** + **Use Case diagrams**.
2. **Gap Analysis** on requirements vs business entities.
3. Identify **Business + Logical Data Models**. Create **ER diagrams** + **Class diagrams**.

**Sample assumptions to state:**
- A vehicle cannot be both Car and Van at once → **Total Participation**.
- A vehicle is owned by 1 person at a time → **1:M relationship**.
- Ownership can be transferred → **Association** (not Composition).
- Attributes: text, number, date.

**Diagrams produced:** ER Diagram · Class Diagram · Table Structures.

### Exercise 2 — CCTV Camera System

**Brief:** CCTV cameras send videos to a central server for storage + later retrieval.

**Q1. Data Architecture** → diagrams (ER, Class).  
**Q2. Application Architecture** → Application Communication diagram, Component diagram.

> **Pro Tip:** These exercises exemplify **Phase C (Information Systems Architecture)** of TOGAF ADM. If a case study asks you to "design the data architecture", do exactly this: clarify requirements → assumptions → diagrams.

---

## 11. One-Shot Summary (the morning of the exam)

> **Software architecture** becomes essential as systems grow in **complexity, longevity, and interconnection**. **Enterprise Architecture (EA)** applies architectural thinking to the whole organisation — its business, information, processes, and technology — for the successful development and execution of strategy. EA delivers **business benefits** (faster time-to-market, consistent processes, less risk) and **IT benefits** (lower cost, faster development, less complexity). The **4 key architecture principles** are: **Build to change**, **Model to analyse and reduce risk**, **Communicate visually with stakeholders**, and **Identify key engineering decisions**. The **2 major EA frameworks** are: **Zachman Framework** (1987 — an **enterprise ontology / classification schema** with a **6 × 6 matrix** of **What, How, Where, Who, When, Why** × six perspectives **Scope → Enterprise Model → System Model → Technology Model → As Built → Functioning Enterprise**) and **TOGAF** (1994 — **The Open Group Architecture Framework**, modelled at 4 levels: **Business, Application, Data, Technology**, with components: **ADM, Enterprise Continuum, Resource Base**). **TOGAF's heart is the ADM (Architecture Development Method)** — a 9-phase iterative cycle: **Preliminary → A: Vision → B: Business Arch → C: Information Systems → D: Technology → E: Opportunities & Solutions → F: Migration Plan → G: Implementation Governance → H: Architecture Change Management** — with **Requirements Management** continuously at the centre. **Zachman tells you WHAT to document; TOGAF tells you HOW to develop it.** Used together, they cover both the artifact catalogue and the development process.

---

## 12. Likely Exam Questions (and how to answer)

**Q1. What is Enterprise Architecture? List its benefits.**  
→ Definition (holistic enterprise analysis/design/planning/implementation). Business benefits (strategy, time-to-market, consistency, risk, security) + IT benefits (cost traceability, lower cost, faster dev, less complexity, less risk).

**Q2. List and explain the 4 key architecture principles.**  
→ BMC-I: Build to change · Model to analyse · Communicate · Identify key decisions. One-line each.

**Q3. Explain TOGAF and describe the phases of the ADM.** ⭐  
→ Definition (EA framework with ADM, Enterprise Continuum, Resource Base). 4 levels (BADT). 9 ADM phases (Preliminary, A–H) + Requirements Management at the centre. Use the diagram + table.

**Q4. Explain the Zachman Framework.** ⭐  
→ Definition (enterprise ontology). 2D classification: **6 columns** (5W + 1H) × **6 rows** (Scope → Functioning Enterprise). Each cell holds an artifact for one (column, perspective) pair.

**Q5. Differentiate between Zachman and TOGAF.**  
→ Zachman = **classification ontology** (WHAT artifacts). TOGAF = **process method** (HOW to develop). They complement each other.

**Q6. What is the role of Requirements Management in TOGAF ADM?**  
→ Sits in the **centre** of ADM. **Continuous, ongoing**. Requirements produced/analysed/reviewed in every phase. Ensures changes are well governed across all phases.

---

## 13. Vocabulary You Should Use Confidently

- **Enterprise Architecture (EA)** — architectural practice for the whole organisation.
- **Zachman Framework** — 6×6 enterprise ontology (1987, John Zachman).
- **TOGAF** — The Open Group Architecture Framework (1994).
- **ADM** — Architecture Development Method, the heart of TOGAF (9 phases + Requirements Management).
- **Enterprise Continuum** — virtual repository of TOGAF architecture assets.
- **Resource Base** — TOGAF's guidelines, templates, examples.
- **TAFIM** — US DoD framework that TOGAF was derived from.
- **5W + 1H** — Why, How, What, Who, When, Where (Zachman columns).
- **Architecture Vision** — TOGAF Phase A.
- **Business / Information Systems / Technology Architecture** — TOGAF Phases B, C, D.
- **Architecture Roadmap** — output of TOGAF Phase E.
- **Architecture Contract Document** — output of TOGAF Phase G.
- **Build to change, not to last** — modern architecture principle.

---

## 14. References

- TOGAF documentation — http://pubs.opengroup.org/architecture/togaf8-doc/arch/toc.html
- TOGAF ADM overview — https://www.orbussoftware.com/enterprise-architecture/togaf/what-is-the-adm/
- Zachman Framework — https://www.zachman.com/

---

## 🎓 Course Wrap-Up — The Full SE3030 Story

Congratulations — you've reached the end of the lecture series. Here's the whole story tied together:

| Lecture | Big Idea | Key memory hook |
|---|---|---|
| **Lec 1** | What software architecture *is* | **SQDP / Squid P** (Style + Quality attributes + Decisions + Principles) |
| **Lec 2** | How architecture is *produced* | ABC + 7 Activities (B-U-C-D-A-I-C) + 5 Strategies |
| **Lec 3** | How to *view & document* it | 3 structures (MCA) + 4+1 View Model |
| **Lec 4** | Monolithic vs Distributed decision | 3 C's (Cohesion, Coupling, Connascence) + Architecture Quantum |
| **Lec 5** | Real-world examples | PTS (Priorities → Trade-offs → Structure) — Stack Overflow vs Uber |
| **Lec 6** | Quality attributes (vocabulary) | AIMPRRSSTU + 4 requirement types + ISO 25010 |
| **Lec 7** | How to *specify* QAs formally | SSAERR (6-part QAS template) |
| **Lec 8** | How to *achieve* QAs | Tactic frameworks (DRP for Availability, DMA for Performance, RDR for Security…) |
| **Lec 9** | The catalogue of architectural patterns | 19 styles + IaaS/PaaS/SaaS + N-Tier vs Layered |
| **Lec 10** | How to *evaluate* architecture | ARID + SAAM (SDECE) + risks/non-risks |
| **Lec 11** | How to find *trade-offs* | ATAM + Sensitivity / Trade-off / Risk / Non-risk + Utility Tree |
| **Lec 12** | Enterprise-scale frameworks | TOGAF ADM (9 phases) + Zachman (6×6 ontology) |

---

## 🎯 Final A4 Reference Sheet — What to put on it

You're allowed **one A4 reference sheet** in the exam. Based on the 2025 paper, prioritise:

**Side 1 (Core Concepts):**
1. The **SQDP / "Squid P"** definition of architecture (Lec 1)
2. The **7 Architectural Activities** (B-U-C-D-A-I-C) (Lec 2)
3. The **4 ABC Influences** (Lec 2)
4. The **3 architectural structures** (MCA) (Lec 3)
5. The **4+1 View Model** diagram (Lec 3)
6. The **Architecture Quantum** 4 properties (Lec 4)
7. The **Monolithic vs Distributed** comparison table (Lec 4)
8. The **10 Quality Attributes** (AIMPRRSSTU) with one-line each (Lec 6)

**Side 2 (Practical Tools):**
9. The **6-part QAS template** (SSAERR) (Lec 7)
10. **Tactics framework** for Availability (DRP), Performance (DMA), Security (RDR) (Lec 8)
11. **Architectural styles** quick comparison (Monolith / Modular Monolith / Layered / N-Tier / Microservices / Microkernel / Event-Driven) (Lec 4 + 9)
12. **N-Tier vs Layered** distinction (Lec 9)
13. **IaaS / PaaS / SaaS** one-line each (Lec 9)
14. **SAAM 5 steps** (SDECE) (Lec 10)
15. **ATAM 4 key concepts** (Sensitivity / Trade-off / Risk / Non-risk) (Lec 11)
16. The **3 trade-off pairs** (Performance↔Modifiability, Availability↔Consistency, Security↔Usability) (Lec 4)

---

## 💪 Final Pep Talk

You've now got **a complete student-friendly note for every lecture** + **a past paper analysis** + **memory hooks for every key concept**.

The SE3030 exam is **mostly case-study based** — they want to see you **think like an architect**. So the formula for any case-study question is:

1. **Identify functional + non-functional requirements** (Lec 6).
2. **Pick the dominant quality attributes** + justify (Lec 6).
3. **Match QAs to architectural styles** (Lec 9).
4. **Recommend a style** + **state trade-offs** (Lec 4 + 11).
5. **Draw a labelled block diagram** (label every component + every arrow's protocol).
6. **Mention evolution path** (Stack Overflow → Uber arc, Lec 5).

For the QAS/Tactics question (Q4-style):
- Use the **6-row SSAERR table** for QAS (Lec 7).
- Use the **3-step format** (Name → Describe → Link to QAS) for Tactics (Lec 8).
- Always include a **number** in the response measure.

For the short-answer questions (Q3-style):
- Memorise the textbook definitions (one-liners earn marks fast).
- Use the comparison tables for any "differentiate X vs Y" question.

You've got this. Good luck on exam day. 🍀🎓

---

**The end of the SE3030 lecture series. All 12 lectures are now saved as Markdown files in your outputs folder.** 🚀
