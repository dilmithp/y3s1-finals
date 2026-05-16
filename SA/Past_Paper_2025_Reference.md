# SE3030 — Past Paper Reference (June 2025)

**Course:** Software Architecture · 3rd Year, Semester I · SLIIT  
**Duration:** 2 Hours · 4 Questions · 100 Marks · 10-min reading time

> This is your **most valuable revision asset**. The 2026 paper structure will be similar (4 × 25-mark questions, mostly case-study based). Study this paper deeply — patterns repeat.

---

## Quick Pattern Analysis 🎯

| Question | Marks | Type | Topics |
|---|---|---|---|
| **Q1** | 25 | **Big case study** + diagram | Quality attributes · Architectural styles selection · Long-term evolution · Block diagram |
| **Q2** | 25 | **Mid case study** | ABC · Architectural Activities · Implementation conformance |
| **Q3** | 25 | **Short answers** (6 parts) | ABC · NFRs · 4+1 View · Cloud · SAAM · N-Tier vs Layered |
| **Q4** | 25 | **Mixed** (QAS + Tactics + Design) | QAS · Tactics · Architecture critique · Trade-off analysis |

### Big takeaways for revision priority

**MUST master:**
1. **Architectural styles** — Monolithic, Modular Monolithic, Event-Driven, Microkernel, Microservices (Q1 directly tests these 5!)
2. **Quality attributes** — definitions, trade-offs, prioritisation
3. **Architecture Business Cycle (ABC)** — appeared in Q2 AND Q3
4. **Architectural Activities (7)** — Q2 had 3 sub-parts on this, Q3 had one
5. **Quality Attribute Scenarios (QAS)** — Q4 wants you to **write concrete ones**
6. **Tactics** — Q4 wants you to **propose tactics** and explain how they improve quality
7. **4+1 View Model** — Q3 (5 marks)
8. **SAAM** — Q3 (4 marks) — Architecture Evaluation
9. **N-Tier vs Layered** — Q3 (4 marks) — distinction question
10. **Cloud Architecture style** + service offerings (IaaS, PaaS, SaaS) — Q3 (4 marks)
11. **Drawing & critiquing block diagrams** — Q1, Q4

---

## Question 1 — Case Study: MediConnect (25 marks)

**Scenario:** National digital public health initiative for the Health Department.
- Manages medical records, prescriptions, appointments, epidemic outbreaks
- Must integrate with legacy hospital systems
- Web + mobile interfaces
- Scale: millions of users (patients, healthcare professionals, government admins)
- Future features: AI-based diagnosis, data analytics
- Phased delivery — first phase within 1 year
- **Architectural patterns to consider:** Monolithic, Modular Monolithic, Event-Driven, Microkernel, Microservices

| Sub-Q | Marks | Task |
|---|---|---|
| 1 | 2 | Identify functional and non-functional requirements |
| 2 | 4 | Select 2 most critical quality attributes + justify |
| 3 | 4 | Analyse how each architectural style aligns/conflicts with the 2 QAs (table) |
| 4 | 4 | Recommend ONE pattern for the initial release + justify (requirements + trade-offs) |
| 5 | 5 | Long-term evolution: same style or transition? Justify |
| 6 | 6 | High-level architectural diagram (block diagram) + description (label responsibilities, interactions, communication mechanisms) |

### 🎯 Exam strategy for Q1-style questions

1. **List FRs and NFRs separately** in a clear table.
2. Pick 2 QAs that are **most stressed in the brief** (e.g., MediConnect → **Scalability** + **Modifiability/Evolvability** because of millions of users + future features).
3. Build a **5-row × 2-column table** (5 architectural styles × 2 QAs) with ✓/✗/△ entries.
4. Recommend pattern + name **at least 2 specific trade-offs** you accept.
5. For evolution: *"start with X (Modular Monolith), evolve to Y (Microservices) when Z conditions met"* — this is the **Stack Overflow → Uber pattern** from Lec 5!
6. **Diagram:** Use boxes for components, arrows for communication, label EVERY arrow with the protocol (REST/gRPC/message queue/event bus).

---

## Question 2 — Case Study: Sales System Modernization (25 marks)

**Scenario:** Modernise a desktop-based sales system into a cloud-based one.
- Current system has performance + integration issues
- Sales staff frustrated
- Management agreed on the condition that the project is **well-justified** with **strict deadlines + budget constraints**
- Must support third-party POS integration
- Wants incremental evolution based on user feedback

| Sub-Q | Marks | Task |
|---|---|---|
| 1 | 3 | 3 key influences shaping architectural decisions (hint: **ABC**) |
| 2 | 10 | Justify the business case using **Architectural Activities** — at least 5 points |
| 3 | 6 | Next 3 architectural activities after business case approval — describe each contribution |
| 4 | 6 | Importance of **"Ensuring implementation conforms to architecture"** in the **maintenance phase** |

### 🎯 Exam strategy for Q2-style questions

- **Sub-Q 1:** Use the **4 ABC influences** — Stakeholders, Developing Org, Architect's Experience, Technical Environment. Pick 3 most relevant.
- **Sub-Q 2:** Use **Activity 1 (Creating the Business Case)** content from Lec 2. The 5 points should map to the business case sub-questions: market need, cost, target market, time-to-market, integration, limitations.
- **Sub-Q 3:** After Activity 1 (Business Case), the next 3 are: **Understanding Requirements (2)**, **Creating/Selecting Architecture (3)**, **Documenting & Communicating (4)**. Describe what each contributes.
- **Sub-Q 4:** Talk about **architecture drift / erosion**, **maintainability over time**, **constant vigilance**, role of code reviews and architecture review boards, technical debt.

---

## Question 3 — Short Answers (25 marks)

| Sub-Q | Marks | Topic |
|---|---|---|
| 1 | 4 | Explain the **Architecture Business Cycle** |
| 2 | 4 | Define **Non-Functional Requirements** + outline the **3 main categories** |
| 3 | 5 | **4+1 View Model** + focus areas of each view |
| 4 | 4 | **Cloud Architecture style** + advantages/disadvantages of its different service offerings |
| 5 | 4 | **SAAM (Software Architecture Analysis Method)** in brief + main objectives + benefits |
| 6 | 4 | Similarities and differences of **N-Tier vs Layered** architecture |

### 🎯 Exam strategy for Q3-style questions

- These are **definition + structure** questions. Each ~4 marks expects: **definition + 2-3 key points + brief example**.
- For **NFR's 3 categories**: Quality Attributes, Business Requirements, Constraints (from Lec 6).
- For **4+1 View Model**: draw the diagram + 1-line per view (Logical, Development, Process, Physical, Scenarios).
- **Cloud service offerings**: IaaS / PaaS / SaaS — pros and cons of each.
- **SAAM** is from Lec 10 (Architecture Evaluation) — learn it precisely.
- **N-Tier vs Layered**: similar (both layered approaches), but N-Tier is **physical separation** (different machines/processes) while Layered is **logical separation** (within the same deployment).

---

## Question 4 — Mixed: QAS, Tactics, Design (25 marks)

### Part (a) — Public photo sharing website (14 marks)

**Scenario:**
- Single-server design
- Uploader interface (only authorised users) + Public consumer interface
- Thumbnail viewing + large-photo viewing
- High availability needed for large photos
- Thumbnail view frequency = **10,000×** large photo view

| Sub-Q | Marks | Task |
|---|---|---|
| i | 3 | Concrete **Quality Attribute Scenario** for **Availability** |
| ii | 2 | Propose a **Tactic** to improve Availability |
| iii | 3 | Concrete **QAS** for **Performance** |
| iv | 2 | Propose a **Tactic** to improve Performance |
| v | 6 | Critique the given sample architecture + suggest improvements |

### Part (b) — Courthouse digitization (9 marks)

**Scenario:**
- Digitise millions of court documents
- Integration with various government agencies
- Future AI-assisted character/image recognition for smart search
- New records uploaded as digital; existing records scanned slowly over time

| Sub-Q | Marks | Task |
|---|---|---|
| i | 6 | Draw and explain how to architect the solution |
| ii | 3 | Identify a Trade-off + discuss mitigation plans |

### 🎯 Exam strategy for Q4-style questions

- **Master the 6-part QAS template** (Source, Stimulus, Artifact, Environment, Response, Response Measure) — appears in Lec 7.
- Tactics use the language from Lec 8 (e.g., for Availability: ping/echo, heartbeat, redundancy, failover, voting; for Performance: caching, increase resources, concurrency, etc.).
- For **architecture critique (v)**: identify single points of failure, lack of caching, lack of separation, lack of CDN for thumbnails. Suggest improvements (separate uploader/consumer, add CDN for thumbnails since they're 10,000× more frequent).
- For **diagram-based answers**: always **label every arrow with the protocol** and **briefly justify** each component.
- **Trade-off identification**: pick something concrete (e.g., "AI smart search adds latency vs the speed of basic keyword search"). Mitigation: hybrid approach, async indexing.

---

## 🔑 Topics Most Likely to Appear in Your 2026 Exam

Based on this 2025 paper, expect heavy focus on:

| Topic | Why | Lecture |
|---|---|---|
| **Identifying FR vs NFR from a brief** | Q1.1 | Lec 6 |
| **Selecting + justifying critical quality attributes** | Q1.2 | Lec 6 |
| **Comparing architectural styles against QAs (table)** | Q1.3 | Lec 9 |
| **Recommending an architectural pattern with trade-off justification** | Q1.4 | Lec 4, 9 |
| **Long-term architectural evolution** | Q1.5 | Lec 5 (Uber!) |
| **Drawing block diagrams** | Q1.6, Q4.b.i | All |
| **Architecture Business Cycle** | Q2.1, Q3.1 | Lec 2 |
| **Architectural Activities (7)** | Q2.2, Q2.3 | Lec 2 |
| **Implementation conforms to architecture (maintenance)** | Q2.4 | Lec 2 |
| **NFRs and their 3 categories** | Q3.2 | Lec 6 |
| **4+1 View Model** | Q3.3 | Lec 3 |
| **Cloud architecture (IaaS / PaaS / SaaS)** | Q3.4 | (need to study!) |
| **SAAM** | Q3.5 | Lec 10 |
| **N-Tier vs Layered** | Q3.6 | Lec 9 |
| **Writing concrete QAS** | Q4.a.i, iii | Lec 7 |
| **Proposing Tactics** | Q4.a.ii, iv | Lec 8 |
| **Critiquing existing architecture diagrams** | Q4.a.v | Lec 5, 9, 10 |
| **Identifying trade-offs + mitigation** | Q4.b.ii | Lec 4, 5, 11 |

---

## ⏱️ Timing Strategy (2 hours = 120 minutes)

- Reading time: **10 minutes** (use it to plan Q1 — the biggest case study)
- Per question: **120 / 4 = 30 minutes** (allowing 5–10 min buffer)
- For 25-mark case study questions: **don't write more than 1.5 pages per sub-question** unless the marks justify it
- **Diagrams: budget 5–10 min** but they earn high marks per minute spent

---

## ✍️ Universal Answer Templates

### Template 1: Case Study Answer
1. **Restate the problem in 1 line** (shows comprehension)
2. **List dominant quality attributes** (2-3 max)
3. **Shortlist candidate architectures** (2-3 styles)
4. **Recommend one** + state trade-offs
5. **Diagram with labelled arrows**
6. **Mention evolution path** (if relevant)

### Template 2: "Compare X and Y"
1. Quick definitions of both
2. Similarities (table or bullets)
3. Differences (table or bullets)
4. When to use each
5. Concrete example each

### Template 3: "Define X" / "Explain X"
1. Precise definition (memorised)
2. Why it matters
3. Example
4. (If relevant) Sub-categories or steps

### Template 4: "Critique this architecture"
1. List what's good
2. List what's missing/problematic (single points of failure, missing caching, no separation of concerns, etc.)
3. Suggest **specific** improvements + justify

---

## 📋 The 2026 A4 Reference Sheet — What to put on it

You're allowed **one A4 reference sheet** in the exam. Based on this past paper, prioritise:

**Side 1:**
- 7 Architectural Activities (B-U-C-D-A-I-C)
- 4 ABC Influences (S-DOE-T)
- 5 Architectural Styles + 1-line each (Monolithic, Modular Monolith, Event-Driven, Microkernel, Microservices)
- Quality vs Quantity comparison table (Monolithic vs Distributed)
- The 10 quality attributes (A-I-M-P-R-R-S-S-T-U) with one-line each
- 4+1 View Model diagram

**Side 2:**
- QAS 6-part template (Source · Stimulus · Artifact · Environment · Response · Response Measure)
- Common Tactics list (per quality attribute)
- SAAM steps (5 steps if memorised)
- ATAM steps (briefly, in case)
- N-Tier vs Layered comparison
- Cloud service models (IaaS / PaaS / SaaS) one-line each
- Trade-off pairs (Performance↔Modifiability, Availability↔Consistency, Security↔Usability)

---

**Pro Tip — connecting this to your lecture notes:**

| When studying Lecture | Cross-reference these past-paper questions |
|---|---|
| Lec 1 (Overview) | Q1 (architecture styles) |
| Lec 2 (ABC, Activities) | Q2 (whole question), Q3.1 |
| Lec 3 (Structures, Views) | Q3.3 (4+1) |
| Lec 4 (Monolith vs Distributed) | Q1.3, Q1.4 |
| Lec 5 (Real World) | Q1.5 (long-term evolution) |
| Lec 6 (Quality Attributes) | Q1.2, Q3.2 |
| Lec 7 (QAS) | Q4.a.i, Q4.a.iii |
| Lec 8 (Tactics) | Q4.a.ii, Q4.a.iv |
| Lec 9 (Architectural Patterns) | Q1.3, Q3.6 (N-Tier vs Layered) |
| Lec 10 (Architecture Evaluation) | Q3.5 (SAAM) |
| Lec 11 (Trade-off Analysis) | Q4.b.ii |
| Lec 12 (Architecture Frameworks) | (Less directly tested in 2025) |

---

**Final word:** This 2025 paper is your **best predictor** of the 2026 paper. The structure (1 big case study + 1 mid case study + 1 short answer + 1 mixed QAS/Tactics/Design) is highly likely to repeat. Drill these topics first.

Good luck. 💪
