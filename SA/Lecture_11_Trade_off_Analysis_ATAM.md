# Lecture 11 — Trade-off Analysis (ATAM)

**Module:** SE3030 — Software Architecture · 3rd Year, Semester 1 · SLIIT  
**Lecturer:** Chathura R De Silva

> ⚠️ **EXAM-CRITICAL** — The 2025 paper Q4.b.ii (3 marks) asked: *"Identify a Trade-off in above proposal and discuss mitigation plans"*. This whole lecture is about identifying and analysing trade-offs. The headline tool is **ATAM**. ☕

---

## What you should walk away knowing

1. What a **trade-off** is (and why architecture is mostly about managing them).
2. What **ATAM** is, **why** it exists, and how it **complements SAAM**.
3. The **4 Phases** and **9 Steps** of ATAM.
4. The **4 critical outputs**: **Risks · Non-risks · Sensitivity Points · Trade-off Points**.
5. How to build a **Quality Attribute Utility Tree**.
6. The **3 scenario types**: **Use case · Growth · Exploratory**.
7. How to **identify a trade-off** in a case-study and propose **mitigation**.

> **Pro Tip:** ATAM is heavy on terminology — **Sensitivity Point, Trade-off Point, Risk, Non-risk, Utility Tree**. Master these labels. They're the easiest marks in any ATAM question.

---

## 1. What is a Trade-off? ⭐

> **Definition:** *"A trade-off is a situation that involves **losing one quality** or aspect in return for **gaining another quality** or aspect."*

The architect's daily question:
> *"How much must I give up to get a little more of what I want most?"*

Examples we've seen:
- **Performance ↔ Modifiability** (heavy optimisation makes code rigid)
- **Availability ↔ Consistency** (CAP theorem)
- **Security ↔ Usability** (more checks = more friction)

> **Memory Hook — "Architecture is the art of managing trade-offs."** (Same line from Lec 4 — repeated for emphasis.)

---

## 2. What is ATAM? ⭐⭐⭐

> **ATAM = Architecture Trade-off Analysis Method.**  
> Developed at the **SEI (Software Engineering Institute, Carnegie Mellon)** at the **end of the 1990s**.

### Definition (memorise verbatim)
> *"The objective of ATAM is to provide a **justifiable way to understand a Software Architecture's fitness with respect to multiple competing Quality Attributes**."*

### Why ATAM exists (3 reasons)
1. To **assess the consequences** of architectural design decisions in light of QAs.
2. To help **foresee how a QA can be affected** by an architectural design decision.
3. To **trade off among multiple competing QAs** — *before* the system is built.

### How ATAM differs from SAAM ⭐

| | **SAAM** | **ATAM** |
|---|---|---|
| Focus | **One QA at a time** | **Multiple competing QAs** |
| Output | Quality prediction · candidate comparison | **Trade-off identification** + sensitivity & risk analysis |
| Style | Lighter, simpler | **Heavyweight**, formal |
| Approach | Scenario-based | Scenario-based + utility tree + analysis |
| Best for | Comparing candidate architectures | Understanding **trade-offs** between conflicting QAs |

> **Memory Hook:** *"SAAM = single quality. ATAM = many qualities + trade-offs."*

---

## 3. Stakeholder Expectations & Conflicting Goals

Different stakeholders care about different qualities — and they often **conflict**. The lecture maps it out:

| View | Cares about |
|---|---|
| **End User's view** | Performance · Availability · Usability · Security |
| **Developer's view** | Maintainability · Portability · Reusability · Testability |
| **Business / Community view** | Time to Market · Cost · Projected Lifetime · Targeted Market · Legacy Integration · Rollout Schedule |

> **Pro Tip — exam phrase:** *"Different stakeholders prioritise different quality attributes; ATAM brings these competing concerns into one structured trade-off analysis."*

---

## 4. ATAM Participants (3 groups) ⭐

| Group | Who | Size | Role |
|---|---|---|---|
| **Evaluation Team** | External group — consultants or other org members | **3–5** members | Conduct the evaluation; assigned specific roles |
| **Project Decision Makers** | Empowered to speak for the project; **architect MUST be present** | **2+** members (Project Manager, Customer, etc.) | Authority to mandate changes |
| **Architecture Stakeholders** | People with vested interest in the architecture | **12–15** members | Affected by the architecture (devs, sysadmins, security, etc.) |

> **Memory Hook — "ETP-DMS"** → **E**valuation **T**eam · **P**roject **D**ecision **M**akers · **S**takeholders.

---

## 5. The 4 Phases of ATAM ⭐⭐

```
   PHASE 0          PHASE 1            PHASE 2            PHASE 3
   ─────────        ─────────          ─────────          ──────────
   Partnership &    Evaluation         Evaluation         Follow-up
   Preparation      (Eval Team only)   (+ Stakeholders)
                    Steps 1–6          Steps 7–9
   Assemble team    Present ATAM,      Brainstorm         Address
   Prepare arch     business drivers,  scenarios,         issues
   description      architecture,      analyze            Deliver
                    approaches,        approaches,        final
                    utility tree,      present results    report
                    analyze
```

| Phase | What happens |
|---|---|
| **Phase 0 — Partnership & Preparation** | Assemble Evaluation Team + leadership + key decision makers. Prepare architecture description and initial scenarios. |
| **Phase 1 — Evaluation (Eval Team only)** | The 6 internal steps below. Evaluation team works with the architect to understand and analyse the architecture. |
| **Phase 2 — Evaluation (+ Stakeholders)** | The 3 stakeholder-involving steps. Stakeholders join to brainstorm scenarios and confirm trade-offs. |
| **Phase 3 — Follow-up** | Address raised issues; deliver the **final report**. |

> **Memory Hook:** *"Prep → Architects-only → Stakeholders join → Follow-up."*

---

## 6. The 9 Steps of ATAM ⭐⭐⭐

ATAM has **9 steps** spread across Phase 1 (Steps 1–6) and Phase 2 (Steps 7–9).

### Phase 1 Steps (Eval Team + Architects)

| # | Step | What happens |
|---|---|---|
| 1 | **Present the ATAM** | Evaluation leader explains the process and sets expectations |
| 2 | **Present Business Drivers** | Decision Makers present system overview from a business perspective: most important functions, constraints, business goals, stakeholders, **architectural drivers** (major QA goals) |
| 3 | **Present the Architecture** | Architect(s) present the architecture, technical constraints (OS, hardware, middleware), interactions with other systems |
| 4 | **Identify Architectural Approaches** | Architectural patterns / approaches identified at high level — these become the basis for later analysis |
| 5 | **Generate Quality Attribute Utility Tree** | Present QA goals in detail as **Concrete QAS** + assign **priorities** + **difficulty** |
| 6 | **Analyze Architectural Approaches** | Determine how approaches satisfy refined QA goals → identify **Risks, Sensitivity Points, Trade-off Points** |

### Phase 2 Steps (with Stakeholders)

| # | Step | What happens |
|---|---|---|
| 7 | **Brainstorm and Prioritize Scenarios** | Larger set of scenarios generated with **all stakeholders** + voting to prioritise |
| 8 | **Analyze Architectural Approaches** | Same as Step 6, but on the **high-priority scenarios** from Step 7. Document additional Risks / Sensitivity / Trade-offs |
| 9 | **Present Results** | Findings presented to all stakeholders |

> **Memory Hook — Step 1 to 9 in 3 chunks:**  
> **Steps 1–4:** *"Set the stage."* (Present ATAM, business, arch, approaches)  
> **Steps 5–6:** *"Build the tree, find the issues."* (Utility Tree + first analysis)  
> **Steps 7–9:** *"Bring everyone in, deepen, deliver."* (Stakeholder brainstorm + deeper analysis + present)

---

## 7. The 4 Key ATAM Concepts ⭐⭐⭐ (this is examined a lot!)

These are the **deliverables** ATAM finds. Memorise the definition + a 1-line example for each.

### 7.1 Sensitivity Point
> **Definition:** *"A property of a component that is **critical to the success** of the system."*

In other words: **a single decision that strongly affects ONE quality attribute**.

**Examples:**
- The **number of simultaneous database clients** affects performance → **sensitivity point** for Performance.
- Keeping a **backup database** affects reliability → **sensitivity point** for Reliability.
- The **power of encryption** (number of bits in the key) → **sensitivity point** for Security.

> **Memory Hook:** *"Change this knob → one quality moves a lot."*

### 7.2 Trade-off Point ⭐⭐
> **Definition:** *"A property that **affects more than one attribute** or sensitivity point."*

In other words: **a single decision where improving one QA hurts another**.

**Examples:**
- To get the required **performance**, the team had to use **assembly language** → that **reduced portability**. → A **trade-off point** between Performance and Portability.
- Keeping a **backup database** improves **reliability** but **hurts performance** → trade-off point.

> **Memory Hook:** *"Change this knob → two qualities move in opposite directions."*

### 7.3 Risk
> **Definition:** *"Architecturally significant decisions that have **not been made**, or that **have been made incorrectly**, that may lead to **negative consequences** later."*

In simpler words: **a problematic decision in the current architecture**.

**Examples:**
- The decision to keep a backup database is a **risk** if the performance cost is **excessive**.
- Rules for writing business logic in the second tier of the 3-tier architecture **aren't clearly articulated** → could result in functional duplication, hurting modifiability of the third tier.

### 7.4 Non-Risk
> **Definition:** *"Good decisions that **rely on assumptions** that are frequently **implicit** in the architecture."*

In other words: **a decision that's fine — provided the assumption holds**.

**Examples:**
- The decision to keep a backup database is a **non-risk** if the performance cost is **not excessive**.
- *"Assuming message arrival rates of once per second, processing time <30 ms, and one higher-priority process — a 1-second soft deadline seems reasonable for performance."* → **non-risk**, but only because of the assumed conditions.

> **Memory Hook for the 4 concepts:**  
> **Sensitivity** = **one knob, one quality**.  
> **Trade-off** = **one knob, two qualities** (going opposite ways).  
> **Risk** = **bad / unmade decision**.  
> **Non-risk** = **good decision with assumptions** (which need to be documented and verified).

> **Pro Tip — exam template:** *"In the proposed architecture, [decision X] is a **trade-off point** between [QA1, e.g., performance] and [QA2, e.g., portability], because [reasoning]. To mitigate, we could [mitigation, e.g., introduce caching at layer Y]."* That's the perfect Q4.b.ii answer.

---

## 8. The Quality Attribute Utility Tree ⭐ (examable concept!)

A **utility tree** is a top-down structured way to characterise the *driving* QA requirements of a system.

### Structure (3 levels)

```
                                  Utility
                                     │
              ┌──────────────────────┼──────────────────────┐
              ▼                      ▼                      ▼
        Quality Attribute      Quality Attribute      Quality Attribute
        (e.g., Performance)    (e.g., Security)       (e.g., Modifiability)
              │                      │                      │
        ┌─────┴─────┐                                        │
        ▼           ▼                                        │
   Refinement  Refinement                              Refinement
   (sub-goal)  (sub-goal)                              (sub-goal)
        │           │
        ▼           ▼
   Scenario    Scenario          ← LEAVES (concrete QAS)
   [H, M]      [M, L]              with priority [Importance, Difficulty]
```

| Level | What it holds |
|---|---|
| **Quality Attribute Level** | Top-level QAs (typically Performance, Modifiability, Security, Availability) |
| **Refinement Level** | Decomposes the QA into sub-goals if possible |
| **Scenario Level (leaves)** | **Concrete Quality Attribute Scenarios** with **rankings** |

### How to rank scenarios (the 2 dimensions)

Each leaf-scenario gets a pair of rankings:

| Dimension | Scale |
|---|---|
| **Importance / Priority** | High / Medium / Low (or 1–10) |
| **Difficulty Factor** (how hard for the architecture to achieve) | High / Medium / Low (or 1–10) |

So a scenario might be marked **(H, M)** = High importance, Medium difficulty.

### Why the utility tree matters
- **Top-down vehicle** to figure out which QAs really *drive* the architecture.
- **Forces concrete scenarios** at the leaves (no vague "must be fast").
- **Voting on rankings** prioritises what to focus the analysis on.

> **Pro Tip:** Ranking scenarios as **(H, H)** marks them as **most worth the architect's attention** — high importance AND hard for the architecture to achieve = highest risk.

> **Memory Hook:** *"Utility tree = QAs at the trunk, refinements as branches, concrete scenarios as the leaves — each leaf gets a (Priority, Difficulty) tag."*

---

## 9. The 3 Types of Scenarios in ATAM ⭐

The lecture distinguishes **3 scenario types** (this is examable!):

| Type | What it tests | Example |
|---|---|---|
| **Use Case Scenario** | **Normal expected behaviour** | "Remote user requests a database report via the Web during peak period and receives it within 5 seconds." |
| **Growth Scenario** | **Anticipated changes / scaling** | "Add a new data server to reduce latency in scenario 1 from 5s to 2.5s within 1 person-week." |
| **Exploratory Scenario** | **Extreme conditions / unexpected stresses** | "Half of the servers go down during normal operation without affecting overall system availability." |

> **Memory Hook — "UGE"** → **U**se case · **G**rowth · **E**xploratory.

> **Pro Tip:** *"Scenarios should be as specific as possible."* — direct from the slide. Always include **concrete numbers** (5 seconds, person-weeks, server counts).

---

## 10. The 7 Outputs of ATAM ⭐⭐ (high-value memorisation!)

ATAM produces **7 documented outputs**:

| # | Output | What it is |
|---|---|---|
| 1 | **Concise presentation** of the architecture | Summary of architectural decisions |
| 2 | **Articulation** of the business goals | Why this architecture matters |
| 3 | **Quality requirements as scenarios** | The QAS leaves of the utility tree |
| 4 | **Mapping of architectural decisions to quality requirements** | How each decision supports each scenario |
| 5 | **Sensitivity points + Trade-off points** | Decisions that strongly affect QAs (single or multiple) |
| 6 | **Risks + Non-risks** | Basis for the **risk mitigation plan** |
| 7 | **Risk themes** | Systemic weaknesses that *explain* the risks |

> **Memory Hook — "ABS-MSTRR"** (ugly but works): **A**rch presentation · **B**usiness goals · **S**cenarios · **M**apping · **S**ensitivity/Trade-offs · **T**ricky risks (and Non-risks) · **R**isk themes.

> **Pro Tip:** Compare with SAAM outputs (Lec 10): SAAM gives Prioritised QAs, Mapping, Risks/Non-risks. **ATAM adds Sensitivity Points, Trade-off Points, and Risk Themes** — the trade-off-specific outputs.

---

## 11. Benefits of ATAM ⭐

The lecture lists **5 main benefits**:

1. **Identifies risks early** in the lifecycle (cheap to fix!).
2. **Increased communication** among stakeholders.
3. **Clarified quality attribute requirements**.
4. **Improved architecture documentation**.
5. **Documented basis for architectural decisions** (so future architects understand *why*).

Plus from slide 56:
- *"Technical participants are typically **amazed at how many risks can be found in a short time**."*
- *"Managers appreciate the opportunity to see precisely **how technical issues threaten achievement of their business goals**."*

---

## 12. The Game-Based Architecture Example (Phase 1 walkthrough)

The lecture's worked example: a **"game space"** component that lets one game run on **multiple game engines** without modification. Quality attributes prioritised:

| QA | Goal |
|---|---|
| **Portability** | Run the same game on multiple game engines without modifying the game |
| **Modifiability** | Minimise changes needed across architecture components |
| **Performance** | <1 second response time per stimulus; ≥20 frames/sec |

### Architectural approaches identified
- **MVC pattern** → breaks dependency, separates core from view (good for Portability + Modifiability)
- **Asynchronous messaging** → reduces network overhead impact on display rate
- **Ontologies** → independent game knowledge representation
- **Mid-game scripting** → easy modifiability (but ~10x slower than precompiled code!)
- **API + Object mapping table** → clean integration

### Sensitivity Points found (S1–S4)
- Network latency · Message load · Single unique identifier · Ontology change propagation

### Trade-off Points found (T1–T5) ⭐
- **T1, T2, T3, T4**: Portability (+) and Modifiability (+) **vs Performance (−)** — separating into layers, mid-game scripting, ontologies all hurt performance
- **T5**: Modifiability (−) vs Performance (+)

### Risks (R1–R5)
- Tight coupling between MVC controller and model · Data integrity · Pre-determined messages requiring redeploy · Scripting not exposing all functionality · Manual mapping if no unique IDs

### Non-Risks (N1–N6)
- Removing direct view-controller link · Asynchronous mechanism (avoids frame rate impact) · API stability · Compatibility assumptions

> **Pro Tip:** This worked example shows the standard ATAM output format — **labelled S, T, R, N items**. If asked to do an ATAM analysis in the exam, mimic this format.

---

## 13. Identifying a Trade-off + Mitigation ⭐⭐ (Q4.b.ii of past paper!)

When the exam says *"Identify a trade-off and discuss mitigation plans"*, follow this **3-step format**:

### Step 1 — Name the trade-off precisely
*"In the proposed architecture, [decision X] creates a **trade-off point** between [QA A] and [QA B]."*

### Step 2 — Explain the trade-off mechanism
*"Improving [QA A] via [decision] degrades [QA B] because [mechanism]."*

### Step 3 — Propose mitigation
*"To mitigate this, we can [tactic / pattern], which [how it helps]. The residual cost is [acceptable / negligible / acknowledged]."*

### 🎯 Worked Example for the courthouse digitization case (Q4.b)

**Question recall:** Courthouse digitises millions of documents. AI-assisted character/image recognition planned for smart search.

**Trade-off identified:**
> *"The decision to add **AI-assisted character/image recognition** for smart search creates a **trade-off point** between **Search Quality (Functional Suitability)** and **Performance (latency + cost)**. Running OCR + NLP models on every document at search time would significantly slow down responses and increase compute cost. However, doing it asynchronously (offline indexing) creates a **trade-off** with **Modifiability** — re-indexing all documents whenever the AI model changes is expensive."*

**Mitigation plan:**
> *"Mitigate by **(1) running OCR/AI extraction asynchronously at upload time** (Performance Tactic: 'Maintain Multiple Copies' — pre-computed search index instead of on-demand processing), **(2) caching** the extracted text + embeddings in a search engine like Elasticsearch (Performance Tactic: 'Maintain Multiple Copies'), and **(3) versioning the AI model** so that the legacy index keeps working while the new model gradually re-indexes documents in the background (Modifiability Tactic: 'Defer Binding Time' via configuration files / versioned APIs)."*

That's a **3-mark answer in 4 minutes**, using vocabulary from this lecture + Lec 8 tactics. ✅

---

## 14. The Architect's Role in ATAM (recap from Lec 1, 2)

The lecture restates the architect's responsibilities (slide 10) — useful for "role of architect" questions:

- **Abstracts complexity** into a manageable model
- **Sets quantifiable QA objectives**
- **Maintains control over the architecture lifecycle**
- **Stays on course** with the long-term vision
- **Makes critical decisions** for implementation, operations, maintenance
- **Creates and distributes** tailored views to stakeholders
- **Works closely with executives** to justify architecture investment
- **Acts as an agent of change** in immature processes
- **Inspires and mentors** colleagues

> **Memory Hook:** *"Envision · Realize · Influence."* — the architect's 3 modes (slide 8).

---

## 15. One-Shot Summary (the morning of the exam)

> **ATAM (Architecture Trade-off Analysis Method)** is an SEI evaluation method that provides a justifiable way to understand a software architecture's fitness with respect to **multiple competing quality attributes**. Where SAAM evaluates one QA at a time, ATAM specifically identifies **trade-offs**. ATAM has **4 phases** (Partnership & Preparation → Evaluation by Eval Team → Evaluation with Stakeholders → Follow-up) and **9 steps** (Present ATAM, Present Business Drivers, Present Architecture, Identify Approaches, Generate Utility Tree, Analyze Approaches, Brainstorm Scenarios, Re-analyze, Present Results). ATAM involves **3 participant groups**: Evaluation Team (3–5), Project Decision Makers (2+, including the architect), and Stakeholders (12–15). Its **central tool** is the **Quality Attribute Utility Tree** — QAs at the top, refinements as branches, **concrete scenarios as leaves**, each leaf rated for (Importance, Difficulty). Scenarios come in **3 types**: **Use Case** (normal behaviour), **Growth** (anticipated changes), and **Exploratory** (extreme conditions). ATAM identifies **4 key concept types**: **Sensitivity Points** (one decision strongly affects one QA), **Trade-off Points** (one decision affects multiple QAs in opposing ways), **Risks** (bad/missing decisions), and **Non-risks** (good decisions, but assumption-dependent). Outputs include the architecture presentation, business goals, scenarios, decision-to-QA mapping, sensitivity & trade-off points, risks & non-risks, and **risk themes**. Benefits: early risk identification, stakeholder communication, clarified QAs, improved documentation, justified decisions. To **identify a trade-off + propose mitigation** in the exam: name the trade-off precisely (which two QAs?), explain the mechanism, then propose a tactic from Lec 8 to mitigate it.

---

## 16. Likely Exam Questions (and how to answer)

**Q1. Define ATAM. How does it differ from SAAM?**  
→ ATAM = Architecture Trade-off Analysis Method, focused on multiple competing QAs. SAAM = single-QA evaluation. Use the comparison table in section 2.

**Q2. List the 4 phases and 9 steps of ATAM.**  
→ 4 phases (Partnership & Preparation, Evaluation by Eval Team, Evaluation with Stakeholders, Follow-up). 9 steps grouped 1–6 (Phase 1) and 7–9 (Phase 2). One-line each.

**Q3. Differentiate between Sensitivity Point, Trade-off Point, Risk, and Non-risk.** ⭐ (highly examable!)  
→ Use the 4 definitions from section 7, each with one example. Remember: *Sensitivity = one knob, one QA · Trade-off = one knob, two QAs · Risk = bad decision · Non-risk = good decision with assumptions*.

**Q4. What is a Quality Attribute Utility Tree? Explain its structure.**  
→ Top-down characterisation tool. 3 levels: QA → Refinement → Scenario (leaves). Each leaf has (Importance, Difficulty) ratings.

**Q5. Explain the 3 types of scenarios used in ATAM.**  
→ Use Case (normal), Growth (anticipated changes), Exploratory (extreme/unexpected). Give a 1-line example each.

**Q6. What are the 7 outputs of ATAM?**  
→ List from section 10: Arch presentation, Business goals, Scenarios, Mapping, Sensitivity & Trade-off Points, Risks & Non-risks, Risk Themes.

**Q7. Identify a trade-off in [given case study] and propose mitigation.** ⭐ (2025 Q4.b.ii!)  
→ Use the **3-step format** from section 13. Name the trade-off → explain the mechanism → propose mitigation tactic from Lec 8.

**Q8. List the participants of ATAM and their roles.**  
→ Evaluation Team (3–5, external) · Project Decision Makers (2+, includes architect) · Stakeholders (12–15, vested interest).

---

## 17. Vocabulary You Should Use Confidently

- **Trade-off** — losing one QA to gain another.
- **ATAM** — Architecture Trade-off Analysis Method.
- **SEI** — Software Engineering Institute (Carnegie Mellon).
- **Architectural driver** — major QA goal that shapes the architecture.
- **Quality Attribute Utility Tree** — top-down characterisation of QAs with concrete scenarios at the leaves.
- **Refinement** (in utility tree) — sub-goal decomposition of a QA.
- **Concrete scenario** — specific QAS with a number.
- **Importance / Difficulty** — the 2 ranking dimensions for utility tree leaves.
- **Use Case Scenario / Growth Scenario / Exploratory Scenario** — 3 ATAM scenario types.
- **Sensitivity Point** — one decision, strongly affects one QA.
- **Trade-off Point** — one decision, affects multiple QAs (often in opposing directions).
- **Risk** — problematic / unmade architectural decision.
- **Non-risk** — good decision dependent on assumptions.
- **Risk theme** — systemic weakness explaining multiple risks.
- **Risk mitigation plan** — what you do about identified risks.

---

## 18. References

- SEI ATAM page — https://www.sei.cmu.edu/architecture/tools/evaluate/atam.cfm
- *Software Architecture in Practice* (2nd ed.), Chapter 11 — http://etutorials.org/Programming/Software+architecture+in+practice,+second+edition/Part+Three+Analyzing+Architectures/Chapter+11.+The+ATAM+A+Comprehensive+Method+for+Architecture+Evaluation/
- *Using ATAM to Evaluate a Game-based Architecture* — http://www.cs.rug.nl/~paris/ACE2006/papers/BinSubaih.pdf

---

**Pro Tip — connections to other lectures and past paper:**

- **Lec 4** introduced the *concept* of trade-offs (Performance↔Modifiability, etc.). ATAM gives you the **method** to systematically identify them.
- **Lec 7 (QAS)** — ATAM uses QAS as the leaves of the Utility Tree.
- **Lec 8 (Tactics)** — Mitigation plans for trade-offs draw from the tactics framework (Caching, Redundancy, Defer Binding, etc.).
- **Lec 10 (SAAM)** — ATAM is the *next-generation* method; SAAM evaluates one QA, ATAM evaluates trade-offs across many.
- **2025 Q4.b.ii** asked for trade-off + mitigation → use the **3-step format** from section 13.

Send Lecture 12 (Architecture Frameworks) when you're ready — that completes the lecture series. 🚀
