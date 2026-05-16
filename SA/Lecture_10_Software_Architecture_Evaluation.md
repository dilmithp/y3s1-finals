# Lecture 10 — Software Architecture Evaluation

**Module:** SE3030 — Software Architecture · 3rd Year, Semester 1 · SLIIT  
**Lecturer:** Chathura R De Silva

> ⚠️ **HIGH-PRIORITY EXAM LECTURE** — The 2025 paper Q3.5 (4 marks) directly asked: *"Explain SAAM (Software Architecture Analysis Method) in brief and outline its main objectives and benefits."* Almost certainly repeats. This lecture is also where the famous **3 SEI methods** live: **ARID, SAAM, ATAM**. Memorise all 3 — but SAAM most of all. ☕

---

## What you should walk away knowing

1. **Why** we evaluate architectures (and how expensive it is to skip).
2. **How** to evaluate (4 method types: scenario-based, mathematical, simulation, experience).
3. **When** to evaluate (Early vs Late).
4. **Challenges**, **stakeholders**, **planning**, and **outputs** of evaluation.
5. The **3 SEI methods**: **ARID, SAAM, ATAM** — purpose, steps, and benefits.
6. **Other evaluation methods** (SALUTA, ALMA, FAAM…) at a recognition level.

> **Pro Tip:** SAAM's **5 steps**, **objectives**, and **benefits** are *the* most likely 4-mark question on this whole lecture. Memorise them like a song.

---

## 1. Why Software Architecture Evaluation? ⭐

The killer questions:
- *"How can you be sure the architecture chosen for your software is the **right one**?"*
- *"How can you be sure it **won't lead to disaster**?"*

> **Architecture evaluation aims to find deficiencies in an architecture as early as possible** — because:
> - **Modifying architecture during the design phase is CHEAP.**
> - **Modifying architecture later is COSTLY** (sometimes catastrophically so — recall Boeing 737 MAX from Lec 5!).

Architecture decides **everything** else: schedules, budgets, performance goals, team structure, documentation, testing, maintenance.

> **Memory Hook:** *"Cheap to fix today, expensive to fix tomorrow."*

---

## 2. How to Evaluate — Method Types ⭐

Evaluation is based on **questioning** or **measuring** techniques. There are two flavours:

| Type | Approach |
|---|---|
| **Qualitative Evaluation** | Subjective reasoning (asking experts, walkthroughs, scenarios) |
| **Quantitative Evaluation** | Numeric measurement (mathematical models, simulations) |

### The 4 Method Types

| # | Type | What it does |
|---|---|---|
| 1 | **Scenario-based** | Use scenarios (use cases, QAS) to walk through the architecture and see how it responds. *(SAAM, ATAM, ARID)* |
| 2 | **Mathematical model-based** | Use formal equations to predict performance, reliability, etc. |
| 3 | **Simulation-based** | Build an executable simulation to observe behaviour under load. |
| 4 | **Experience-based reasoning** | Senior architects use intuition / past projects to evaluate. |

> **Memory Hook — "SMSE"** → **S**cenario · **M**athematical · **S**imulation · **E**xperience.

> **Pro Tip:** The 3 SEI methods (ARID, SAAM, ATAM) are all **scenario-based**.

---

## 3. When to Evaluate — Early vs Late ⭐

Two timing options, both valid:

### Early Evaluation
- **The classic application** — done **after** the architecture is specified but **before** implementation begins.
- Can be done **at any stage** during architecture creation.
- Uses **specification + description** of the architecture, plus **interviews with architects**.
- **Goal:** Examine architectural decisions made so far + choose among options.

### Late Evaluation
- Done **after** implementation is complete.
- Mainly used when architecture is **inherited from a legacy system**.
- Uses **metrics** like **cohesion and coupling** of components.
- **Goal:** Identify the gap between **planned architecture** and **actual architecture** (recall *architecture drift* from Lec 2!).

> **Memory Hook:** *"Early = 'should we?'; Late = 'did we?'"*

| | Early | Late |
|---|---|---|
| When | After spec, before build | After build |
| Based on | Spec + interviews | Metrics + code |
| Goal | Catch issues cheaply | Reverse-engineer + check conformance |
| Example use | New project | Legacy system review |

---

## 4. Challenges of Evaluation

The lecture flags **4 challenges**:

1. **Need an expert evaluation team** to handle unpredictable risks alongside known ones.
2. **Lack of common understanding** of the high-level design among stakeholders.
3. **Different stakeholders have different interests** (often conflicting).
4. **Quality requirements may not be properly written** (or not finished) when the architecture is being designed.

> **Pro Tip:** This connects beautifully to Lec 7 (QAS) — if the team **wrote proper Quality Attribute Scenarios upfront**, challenge #4 disappears.

---

## 5. Who is Involved?

Just **2 groups**:

| Group | Role |
|---|---|
| **Evaluation Team** | The people who **conduct the evaluation** and perform the analysis. Ideally **separate from the architects/developers** (independent perspective). |
| **Stakeholders** | The people with a **vested interest** in the architecture and the system (users, sponsors, ops, security…). |

> **Memory Hook:** *"Reviewers + Owners."*

---

## 6. Planning & Process — What You Need Before Starting

The lecture lists **8 things** you need before starting an evaluation:

1. **Clearly articulated goals and requirements** for the architecture.
2. **Select an evaluation method** (ARID? SAAM? ATAM?).
3. **Controlled scope** — a small number of explicit goals.
4. **Cost-effectiveness** — full reviews aren't needed for small projects.
5. **Ensure key personnel are available** (at least one rep per stakeholder group).
6. **Have a competent evaluation team** — ideally separate from architects/devs.
7. **Managed expectations** — be clear about what the review will and won't deliver.
8. **Circulate results** — afterwards, share a draft with all stakeholders, with a **ranked list of potential issues found**.

---

## 7. What are the Outputs? ⭐

Three concrete outputs:

| Output | What it gives you |
|---|---|
| **Prioritised Statement of Quality Attribute Requirements** | A clear, ordered list of QAs the architecture must satisfy — **excellent documentation** that guides architectural evolution. |
| **Mapping of Approaches to Quality Attributes** | A mapping showing **how each architectural approach achieves (or fails to achieve)** the desired QAs. |
| **Risks and Non-risks** | **Risks** = potentially problematic architectural decisions. **Non-risks** = good decisions that rely on assumptions (often *implicit* in the architecture). |

> **Memory Hook:** *"Priorities, Mappings, and Risks."*

> **Pro Tip — exam phrase:** *"Architecture evaluation produces a prioritised QA statement, a mapping from approaches to qualities, and an explicit list of risks and non-risks."* Memorise verbatim.

---

## 8. Advantages of Evaluation

The lecture lists **6 main advantages** + **1 cautionary stat**:

1. **Forces articulation** of specific quality goals.
2. **Prioritises conflicting goals.**
3. **Puts stakeholders in the same room** (rare and valuable!).
4. **Improves the quality of architectural documentation.**
5. **Uncovers cross-project reuse opportunities.**
6. The average evaluation adds **only a few days** to the project schedule (small % of total).

> **Cautionary closing:** *"Architecture created in haste will precipitate disaster: performance goals not met, security goals failing, customer dissatisfaction, system too hard to change, schedules and budgets through the roof."* — directly from the slide.

---

## 9. The 3 SEI Methods ⭐⭐⭐

> Most common evaluation methods evaluate **only 1 quality attribute** at a time. These **3 advanced methods** (developed at **SEI = Software Engineering Institute, Carnegie Mellon**) handle **multiple QAs** and **identify trade-offs**.

| Method | Full Name | When to use |
|---|---|---|
| **ARID** | **A**ctive **R**eviews for **I**ntermediate **D**esigns | Reviewing a **preliminary** design (component or subsystem) for its **intended usage context** |
| **SAAM** | **S**oftware **A**rchitecture **A**nalysis **M**ethod | Predicting **quality before development** — comparing candidate architectures via **scenarios** |
| **ATAM** | **A**rchitecture **T**radeoff **A**nalysis **M**ethod | Understanding **trade-offs** across multiple **competing** quality attributes (covered in Lec 11!) |

> **Memory Hook — "ASA"** (the 3 SEI methods, alphabetically): **A**RID · **S**AAM · **A**TAM.

> **Memory Hook — Purpose order:** *"ARID for early designs, SAAM to predict quality, ATAM for trade-offs."*

---

## 10. ARID — Active Reviews for Intermediate Designs

### What it is
Method for reviewing **preliminary software designs** (such as for a **component** or **subsystem**) for **suitability in its intended usage context**.

**Key features:**
- **Stakeholder-centric** — requires active stakeholder participation.
- **Easy and lightweight**.
- **Does NOT require complete documentation** (good for early stages).
- Result: **high-fidelity design review + high-quality familiarisation** with the design.

### ARID — The 4 Steps ⭐

| # | Step | What happens |
|---|---|---|
| 1 | **Identify Reviewers** | Designer + ARID facilitator pick the best reviewers — usually engineers who'll **use the design**. |
| 2 | **Overview & Presentation** | Designer prepares + presents an overview, walking through examples. A scribe captures Q&A. |
| 3 | **Brainstorming** | Reviewers brainstorm **scenarios** the design will face. Prioritise. → If it works under those scenarios, it passes. |
| 4 | **Artifacts** | Reviewers jointly write **code or pseudo-code** that uses the design's services to solve each high-priority scenario. The scribe records issues. |

> **Memory Hook — "I-O-B-A"** → **I**dentify · **O**verview · **B**rainstorm · **A**rtifacts. Or *"IOBA"* like a tree species 🌳.

### ARID — Benefits
- **Engages stakeholders early** — get their buy-in.
- **Informs designers** about whether the design is suitable for the overall system.
- **Early insight into viability** — catch errors, inconsistencies, inadequacies early.

> **Pro Tip:** ARID is for **preliminary designs of components/subsystems** — not the whole architecture. It's a **lightweight, early** review.

---

## 11. SAAM — Software Architecture Analysis Method ⭐⭐⭐ (the 2025 Q3.5 question!)

### Definition (memorise verbatim)
> *"SAAM aims to **predict the quality of a system before it has been developed**. The quality of the architecture is **validated by analysing the impact of predefined scenarios on architectural components**. It addresses concerns at the architecture design level which **inherently crosscut multiple architectural components**. SAAM is a **scenario-based evaluation** method."*

### Main objectives ⭐
1. **Predict** the quality of a system **before development**.
2. **Validate the architecture** by analysing the impact of scenarios on architectural components.
3. **Cross-cutting evaluation** of concerns that span multiple components.
4. **Compare candidate architectures**.
5. **Expose risks and trouble spots** early.

### SAAM — The 5 Steps ⭐⭐⭐

| # | Step | What happens |
|---|---|---|
| 1 | **Specify** | **Collect requirements & constraints**. Develop the initial **scenarios**. |
| 2 | **Describe Architectures** | Present the **candidate architecture(s)**, with both **static and dynamic representations** of the system. |
| 3 | **Elicit Scenarios** | **Simulate scenarios** with **relevant stakeholders present** — facilitated brainstorming. |
| 4 | **Classify and Prioritise Scenarios** | Categorise as **Direct** (architecture supports it directly) vs **Indirect** (architecture must be modified). Use **voting** to prioritise. |
| 5 | **Evaluate** | Evaluate the architecture **with respect to the prioritised scenarios** — expose impact / problems. |
|   | **Results** | Document findings. |

> **Memory Hook — "SDECE"** → **S**pecify · **D**escribe · **E**licit · **C**lassify · **E**valuate. Or remember the 5-step flow visually:
>
> ```
>   SPECIFY → DESCRIBE → ELICIT → CLASSIFY → EVALUATE → RESULTS
>   (reqs &   (candidate (brainstorm  (direct vs   (architecture
>    scenarios) arch.)    scenarios)   indirect,    impact
>                                       prioritise)  exposed)
> ```

### Direct vs Indirect Scenarios (key SAAM concept!)

| | Direct Scenario | Indirect Scenario |
|---|---|---|
| What | Architecture **supports the scenario directly** without modification | Architecture **needs to be modified** to support the scenario |
| Implication | The architecture is **fit** for that requirement | A change is needed → identify the **cost** of that change |
| Example | "User views their account balance" → already supported | "Add multi-currency support" → needs significant modification |

### SAAM — Benefits ⭐
1. **Helps assess risks** inherent in an architecture.
2. **Compares candidate software architectures** systematically.
3. **Guides inspection** of the architecture, focusing on potential **trouble spots** — like requirement conflicts or incomplete design specs from a particular stakeholder's perspective.

### 🎯 Worked exam answer template — *"Explain SAAM in brief and outline its main objectives and benefits"* (4 marks, 2025 Q3.5)

> *"**SAAM (Software Architecture Analysis Method)** is a **scenario-based** software architecture evaluation method developed at the SEI. It aims to **predict the quality of a system before it has been developed** by analysing the impact of predefined scenarios on architectural components, addressing concerns that cross-cut multiple components.*  
>
> *Its **5 steps** are: (1) **Specify** — collect requirements and develop scenarios; (2) **Describe Architectures** — present candidate architectures statically and dynamically; (3) **Elicit Scenarios** — brainstorm with stakeholders; (4) **Classify and Prioritise** — distinguish direct from indirect scenarios and vote; (5) **Evaluate** — assess the architecture against the prioritised scenarios.*  
>
> *Its **main objectives** are to predict architectural quality early, compare candidate architectures, and expose risks. Its **benefits** include: (1) helping assess risks in the architecture, (2) enabling systematic comparison of candidate architectures, and (3) guiding inspection toward trouble spots like requirement conflicts and incomplete specifications."*

That's a **full 4-mark answer in ~5 minutes**. ✅

---

## 12. ATAM — Architecture Tradeoff Analysis Method (preview — covered in Lec 11)

### What it is (just so you recognise it)
> *"A structured technique for understanding the **trade-offs inherent in the architectures of software-intensive systems**. Provides a principled way to evaluate a software architecture's fitness with respect to **multiple competing quality attributes**. Is a **spiral model** of design: postulate candidate architectures → analyse → mitigate risks → refined architectures."*

The full ATAM treatment (steps, sensitivity points, trade-off points, risks/non-risks) is in **Lecture 11 (Trade-off Analysis)** — we'll go deep there.

### Quick comparison: ARID vs SAAM vs ATAM ⭐

| | **ARID** | **SAAM** | **ATAM** |
|---|---|---|---|
| Stage | Early (preliminary designs) | Architecture design (before build) | Architecture design (multiple QA evaluation) |
| Scope | Component/subsystem | Whole architecture | Whole architecture + trade-offs |
| Output | Design suitability | Architecture quality prediction; candidate comparison | Trade-off identification; sensitivity & risk analysis |
| Approach | Active stakeholder review | Scenario-based | Scenario-based, **multi-QA** |
| Weight | **Lightweight** | Medium | **Heavy**, formal |
| Documentation needed | Minimal | Moderate | Full |
| Best for | Component design feedback | Comparing candidate architectures | Understanding QA trade-offs |

> **Memory Hook:** *"ARID is the sketch review. SAAM is the prediction. ATAM is the surgery."*

---

## 13. Other Architecture Evaluation Methods (slide 19 — recognition level)

The lecture mentions a handful of **specialised** methods (each focused on one or two quality attributes):

| Method | Focus |
|---|---|
| **SALUTA** | **U**sability (Scenario-based Architecture Level Usability Analysis) |
| **ALMA** | **M**odifiability (Architecture Level Modifiability Analysis) |
| **Software Architecture-based Reliability Analysis** | Reliability |
| **Software Architecture-based Performance Analysis** | Performance — quantitative estimation |
| **FAAM** | Two related qualities (e.g., **Interoperability + Extensibility**) — *Family-Architecture Assessment Method* |

> **Pro Tip:** You don't need to memorise these in detail. Just recognise the names if asked: *"name 3 evaluation methods other than SAAM/ATAM/ARID"* → SALUTA, ALMA, FAAM.

---

## 14. Mathematical Model-based Evaluation (briefly)

Some evaluations use **well-known mathematical equations** to **quantitatively assess operational QAs**:

- Model architecture using equations.
- Use models to obtain **architectural statistics** (e.g., mean execution time of a component).
- Use those statistics to **estimate operational QAs** like **reliability** and **performance**.

> **Memory Hook:** *"Math doesn't lie — but garbage in, garbage out."*

---

## 15. Late Evaluation Methods (briefly)

Used when the system is already built:

- Identify **the difference between actual and planned architecture** (= architecture drift).
- Provide guidelines to **reconstruct the actual architecture** so it conforms to the planned one.
- During **testing phase**, also used to **check source code compliance** with the planned design.

> **Pro Tip:** This connects directly to Lec 2's *"Ensuring implementation conforms to the architecture"* activity — and to Q2.4 of the 2025 paper!

---

## 16. One-Shot Summary (the morning of the exam)

> **Software Architecture Evaluation** finds deficiencies in an architecture **as early as possible**, because *modifying architecture in design is cheap, modifying after build is costly*. Evaluation is **qualitative or quantitative** and uses **4 method types**: **scenario-based, mathematical model-based, simulation-based, experience-based**. It can happen **early** (before implementation, based on spec) or **late** (after implementation, based on metrics — used for legacy systems). Outputs: **(1) prioritised QA requirements, (2) mapping of approaches to QAs, (3) risks and non-risks**. The **3 SEI evaluation methods** are: **ARID** (Active Reviews for Intermediate Designs — lightweight review of preliminary component designs), **SAAM** (Software Architecture Analysis Method — scenario-based, predicts quality before build, compares candidate architectures), and **ATAM** (Architecture Tradeoff Analysis Method — handles multiple competing QAs and identifies trade-offs; covered in Lec 11). **SAAM's 5 steps**: **Specify** → **Describe Architectures** → **Elicit Scenarios** → **Classify & Prioritise** (Direct vs Indirect scenarios; voting) → **Evaluate**. SAAM's benefits: assess risks, compare candidates, guide inspection. ARID's 4 steps: **Identify Reviewers → Overview → Brainstorm → Artifacts**. Other specialised methods include SALUTA (usability), ALMA (modifiability), FAAM (interoperability + extensibility).

---

## 17. Likely Exam Questions (and how to answer)

**Q1. Why is software architecture evaluation important?** ⭐  
→ Modifying architecture in design = cheap, modifying after build = catastrophically expensive. Architecture decides budgets, schedules, performance, team, testing, maintenance.

**Q2. Differentiate between Early and Late architecture evaluation.**  
→ Use the 2-row table from section 3. Highlight: Early = pre-implementation, based on spec; Late = post-implementation, based on metrics, used for legacy systems.

**Q3. What are the outputs of an architecture evaluation?**  
→ Prioritised QA requirements · Mapping of approaches to QAs · Risks and Non-risks. Define each.

**Q4. Explain SAAM in brief and outline its main objectives and benefits.** ⭐⭐ (2025 Q3.5 — guaranteed!)  
→ Use the **worked answer template** from section 11.

**Q5. Differentiate between ARID, SAAM, and ATAM.**  
→ Use the 3-method comparison table in section 12.

**Q6. What are Direct and Indirect Scenarios in SAAM?**  
→ Direct = supported without modification. Indirect = needs architecture modification → cost of change becomes the focus.

**Q7. What is ARID? Explain its steps.**  
→ Definition (lightweight review of preliminary designs) + 4 steps (Identify Reviewers, Overview, Brainstorm, Artifacts).

**Q8. List 3 specialised evaluation methods focused on a single QA.**  
→ SALUTA (usability), ALMA (modifiability), FAAM (interoperability + extensibility).

---

## 18. Vocabulary You Should Use Confidently

- **Architecture evaluation** — assessment to find deficiencies early.
- **Qualitative / Quantitative evaluation** — subjective vs numeric.
- **Scenario-based / Mathematical / Simulation / Experience-based** — 4 method types.
- **Early evaluation / Late evaluation** — pre- vs post-implementation.
- **Risks / Non-risks** — problematic vs good (but assumption-dependent) decisions.
- **SEI** — Software Engineering Institute (Carnegie Mellon).
- **ARID** — Active Reviews for Intermediate Designs.
- **SAAM** — Software Architecture Analysis Method (5 steps: SDECE).
- **ATAM** — Architecture Tradeoff Analysis Method (Lec 11).
- **Direct Scenario / Indirect Scenario** — supported vs needs-modification.
- **Architecture drift** — gap between planned and actual architecture.
- **SALUTA / ALMA / FAAM** — single/dual QA evaluation methods.

---

## 19. References

- SEI Software Architecture page — https://www.sei.cmu.edu/architecture/tools/evaluate/
- *Scenario-Based Software Architecture Evaluation Methods* (paper) — http://www.win.tue.nl/oas/architecting/aimes/papers/Scenario-Based%20SWA%20Evaluation%20Methods.pdf

---

**Pro Tip — connections to other lectures and past paper:**
- **Lec 2** (Activities) → Activity 5 = "Analyzing or Evaluating the Architecture" — that's *exactly* what this lecture deep-dives.
- **Lec 7** (QAS) → SAAM uses scenarios — they should be **QAS** for maximum precision.
- **Lec 11** (next!) → ATAM in detail.
- **2025 Q3.5** asked for SAAM in 4 marks — your worked template (section 11) is your direct answer.
- **2025 Q2.4** asked about *"implementation conforms to architecture in maintenance phase"* — that's **late evaluation** (section 15).

Send Lecture 11 (Trade-off Analysis / ATAM) when you're ready. The ATAM detail will complete your evaluation toolkit. 🚀
