# Lecture 06 — Software Quality Attributes

**Module:** SE3030 — Software Architecture · 3rd Year, Semester 1 · SLIIT  
**Lecturer:** Chathura R De Silva

> Welcome back! This lecture is the **deep dive** into the *"-ilities"* — the famous **quality attributes**. You've been hearing about them since Lecture 1 (*"orthogonal to functionality"*, *"the success criteria of a system"*). Now we're going to **define each one precisely** so you can use them in any case-study answer with confidence. ☕

---

## What you should walk away knowing

1. The **types of requirements** (Functional / Non-Functional / Business / Constraints) and which ones the architect cares about most.
2. The difference between **Quality** and **Functionality** (and why they're **orthogonal**).
3. The difference between **Business Requirements** and **Constraints** (HUGE exam trap!).
4. **Definitions** for the 10 core quality attributes — by name, in the architect's vocabulary.
5. The **ISO 25010** classification (just the existence + categories).
6. **Architectural attributes** vs system quality attributes.

> **Pro Tip — exam favourite:** "Define [quality attribute X] and explain its importance in software architecture." This kind of question appears almost every year. Memorise the **one-line definition** for each of the 10 attributes in this lecture.

---

## 1. Software Requirements — the foundation

A **requirement** is *what stakeholders expect* from the software. Different stakeholders want different things, sometimes conflicting:

| Stakeholder | Typical wish |
|---|---|
| **End User** | The functionality must work without issues + it should be **easy to use**. |
| **Project Manager** | **Low cost**. |
| **Admin / Security / Maintenance** | Their own specialised wishes (control, observability, patching). |

> **Memory Hook — "Needs vs Wants"**  
> A **need** = the system genuinely cannot work without it.  
> A **want** = it would be nice to have.  
> Architects must distinguish between these — and **find a balance**.

### Three quick Q&A from the slide

| Q | A |
|---|---|
| **When** to identify requirements? | At the **start** of the project. |
| **Who** is responsible? | **Business Analyst + Architect** (jointly). The architect must identify the **Architecturally Significant Requirements (ASRs)**. |
| **Why** must they be clear? | Because **changes are costly** — especially in later stages. The later you find out, the more expensive the fix. |

> **Pro Tip — exam buzzword:** Use the term **"Architecturally Significant Requirements (ASRs)"** in any "role of the architect" answer. It signals that you understand architects don't worry about *every* requirement — just the ones that shape the architecture.

---

## 2. Types of Requirements ⭐ (memorise this 4-way split)

```
                        ┌──────────────────────┐
                        │   REQUIREMENTS       │
                        └──────────────────────┘
                                  │
            ┌─────────────────────┼─────────────────────────┐
            ▼                     ▼                         ▼
       Functional          Non-Functional             Business         + Constraints
  (what the system        (Quality Attributes —      (cost, time-to-     (must-do; no
   must do, behave,        the "-ilities")            market, lifetime)   freedom to change)
   react)
```

| Type | Plain English | Example |
|---|---|---|
| **Functional** | What the system **does** | "User can withdraw money from ATM" |
| **Non-Functional / Quality Attributes** | The "-ilities" — **how well** it does it | "Withdrawal must complete in <2 seconds" |
| **Business Requirements** | **Strategic** business decisions; trade-offs allowed | "Must launch within 6 months for $200k" |
| **Constraints** | **Rules** decided beforehand; **NO** trade-off allowed | "Must use open-source software only" |

### ⚠️ Critical exam trap — Business Requirement vs Constraint

| | Business Requirement | Constraint |
|---|---|---|
| Trade-offs | **YES** — can be negotiated | **NO** — locked in, must comply |
| Example | "Time to market = 6 months" (could be pushed to 7 if needed) | "Must use Java 17" (no debate) |
| Architect's role | Manage trade-offs strategically | **Adhere strictly** to it |

> **Memory Hook:**  
> **Business Requirement** = *negotiable*.  
> **Constraint** = *non-negotiable*.

> **Pro Tip:** If a case-study mentions *"the company has already paid for an Oracle license, so the system must use Oracle"* → that's a **constraint**, not a business requirement. Distinguishing these earns you marks.

---

## 3. Quick Exercise — Calculator app (slide 5)

The lecturer's example helps you spot Functional vs Non-Functional in practice:

| Functional Requirements | Non-Functional Requirements (Quality Attributes) |
|---|---|
| Basic +, −, ×, ÷ operations | Should work on Android, iOS, later Windows (**Portability**) |
| Square root, brackets, etc. | Buttons in numpad order (**Usability**) |
| | Support adding new operations later (**Modifiability / Extensibility**) |
| | Landscape UI? (**Usability**) |
| | How many digits to display? (**Usability + Precision**) |

> **Pro Tip — exam scenario:** When a case study lists features, **separate them** into Functional vs Non-Functional explicitly. It shows the marker you're thinking like an architect, not a developer.

---

## 4. Quality vs Functionality — the precise definitions

These are **textbook definitions** from the slides — useful to quote verbatim in the exam.

> **Functionality:** *"The capability of the software product to provide functions which meets stated and implied needs when software is used under specified conditions."*

> **Quality:** *"The extent to which a product satisfies stated and implied needs when used under specified conditions."*

In plain English:
- **Functionality** = the *features* the software provides.
- **Quality** = *how well* the software provides them.

### Why they're "orthogonal" (key concept!)

> **Functionality does NOT determine the architecture.**  
> For a given set of functional requirements, you can create an **endless number** of architectures to satisfy them.  
> Functionality and Quality Attributes are **orthogonal** (different dimensions).

Visually:

```
            Quality Attribute Axis (the "-ilities")
                   ▲
                   │   ★ Architecture A — same features, different qualities
                   │
                   │   ★ Architecture B — same features, different qualities
                   │
                   │   ★ Architecture C — same features, different qualities
                   │
                   └────────────────────────────────► Functionality Axis
                                  (same features for all)
```

> **Memory Hook:** *"Same features, infinite architectures."* The **architecture is shaped by the QUALITY axis, not the functionality axis.**

---

## 5. Non-Functional Requirements — the architect's main concern

Quoting the slide:

> Non-Functional requirements **are not directly linked to any specific function**. They are qualifications that typically cover **business and system quality requirements** and have a **big influence on the architecture**.

> **When they are forgotten at the beginning of a project, it often results in major problems in later stages.**

This sentence should be tattooed on every architect. Forgetting an NFR like *"the system must be 99.99% available"* until you're building production hardware → game over.

> **Pro Tip — exam phrase:** *"Non-functional requirements are the architect's primary concern because they shape the architecture and are very expensive to retrofit if discovered late."*

---

## 6. Quality Attributes Overview

Definition for the exam:

> **Quality Attributes** are **measurable** and **testable** properties of the system that indicate **how well the system satisfies the needs of stakeholders**.

Two informal categories:
- **Runtime Qualities** — e.g., **Performance**, **Availability** (visible while the system is running).
- **User Qualities** — e.g., **User-friendliness / UX** (visible to users).

> 🗒️ *"There are many Quality Attributes and the list keeps growing…"* — every year, new attributes appear (e.g., **Sustainability**, **Observability**, **Privacy**).

---

## 7. ISO 25010 — the formal classification (just know it exists!)

The lecture references **ISO 25010** as a formal way to classify quality attributes. The standard groups them into **8 categories**:

| ISO 25010 Category | Sample sub-attributes |
|---|---|
| **Functional Suitability** | Completeness, correctness, appropriateness |
| **Performance Efficiency** | Time behaviour, resource utilisation, capacity |
| **Compatibility** | Co-existence, interoperability |
| **Usability** | Learnability, operability, accessibility |
| **Reliability** | Maturity, availability, fault tolerance, recoverability |
| **Security** | Confidentiality, integrity, non-repudiation, accountability, authenticity |
| **Maintainability** | Modularity, reusability, modifiability, testability |
| **Portability** | Adaptability, installability, replaceability |

> **Memory Hook — "FPCURMSP"** = **F**unctional Suitability, **P**erformance, **C**ompatibility, **U**sability, **R**eliability, **S**ecurity, **M**aintainability, **P**ortability.  
> Or just remember: **"Function · Perf · Compat · Use · Rely · Secure · Maintain · Port"**.

> **Pro Tip:** Mention ISO 25010 in any "list quality attributes" question. It signals professional vocabulary. *"As per the ISO 25010 standard, quality attributes can be grouped into 8 main categories…"*

---

## 8. Nature of Quality Attributes (3 things to remember)

| # | Insight | What it means |
|---|---|---|
| 1 | QAs may apply to a **single use case**, a **module**, or the **whole system**. | "The login screen must respond in <500 ms" (use-case-level) vs "The system must be 99.9% available" (system-level). |
| 2 | QAs relate to **different lifecycle phases** | **Design-time** qualities (Modifiability, Testability) vs **Runtime** qualities (Performance, Availability). |
| 3 | QAs **impact each other** | **Performance is affected by almost ALL other QAs.** (Heavy security checks slow it down. Heavy testability hooks slow it down. Etc.) |

> **Memory Hook:** *"Performance is the noisy neighbour — it gets affected by almost everyone else."*

---

## 9. The Architect's Role (only 2 things on this slide!)

According to the slide, the architect's responsibility w.r.t. quality attributes boils down to **two things**:

1. **Understand the importance and priority** of the quality requirements.
2. **Evaluate and make trade-offs** to meet quality levels that satisfy stakeholders.

> Notice the word **trade-offs** again — this is the architect's *core skill*. (Recall Lec 4: "*Architecture is the art of managing trade-offs*.")

---

## 10. ⚠️ Issues with Quality Attribute Definitions

The lecture explicitly warns: **don't be confused by inconsistent terminology**. Three problems:

1. **Grouped differently by different authors.** (Bass/Clements use one taxonomy, ISO uses another.)
2. **Overlapping (or similar) attributes.** Example: **Integrity & Security** — they overlap heavily.
3. **Confusion with definition / meaning.** Example: **Performance** = responsiveness? OR efficiency (CPU % usage)? Both are correct in different contexts.

> **Pro Tip:** When defining a quality attribute in the exam, **clarify which sense you're using**. *"Performance, in the sense of responsiveness (latency)…"*

---

## 11. The 10 Quality Attributes — Definitions ⭐⭐⭐

This is the **examable core** of the lecture. Memorise the one-line definition for each. The lecture covers **10 attributes** in detail.

> **Memory Hook for the 10:** **"A I M P R R S S T U"** →  
> **A**vailability · **I**nteroperability · **M**odifiability · **P**erformance · **R**eliability · **R**eusability · **S**calability · **S**ecurity · **T**estability · **U**sability.

Alphabetical & easy. Now each one in detail.

---

### 11.1 Availability

> **Definition:** System services are available **when and where** users need them. The **proportion of time** the system is functional and working.

**Affected by:**
- System errors, maintenance tasks, infrastructure failures, malicious attacks, system load, dependent services.

**How to measure:**  
**Percentage of total system uptime** over a predefined period (e.g., "99.99% uptime per year" — that's about 52 minutes of downtime per year).

> **Memory Hook:** *"Availability = Is it up right now?"*

---

### 11.2 Interoperability

> **Definition:** Ability of a system to **exchange information successfully by communicating with other systems**.

**Two levels of interoperability:**

| Level | What it means | Example |
|---|---|---|
| **Syntactic** | Ability to communicate using **agreed data formats and protocols** | Both systems use JSON over HTTPS — they can *transport* data |
| **Semantic** | Ability to **interpret the exchanged data meaningfully and accurately** | Both systems agree that `currency = "USD"` means United States Dollars (not Australian Dollars!) |

> **Memory Hook:** *"Syntactic = same envelope. Semantic = same meaning."* You can have one without the other (and that causes bugs).

---

### 11.3 Modifiability

> **Definition:** **Cost to make a change**. The **lower the cost** to change → the **higher the modifiability**.

**Types of changes the architect must anticipate:**

| Type | Example |
|---|---|
| **Functional change** | Add a "dark mode" feature |
| **Environment change** | Switch host OS / platform from Windows to Linux |
| **Protocol change** | Switch from REST to gRPC |
| **Dependency change** | Switch DB from MySQL to Oracle (small change), or MySQL → MongoDB (massive change) |

> **Memory Hook:** *"Modifiability = how cheaply can I change this?"*

> **Pro Tip:** Modifiability is closely tied to **Coupling** (Lec 4). Lower coupling → higher modifiability.

---

### 11.4 Performance

> **Definition:** Indication of the **responsiveness of a system to execute any action within a given time interval**.

**Two key metrics:**

| Metric | Definition | Example |
|---|---|---|
| **Latency** | Time taken to **respond to one event** | "Page loads in 200 ms" |
| **Throughput** | Number of events that take place **within a given time** | "10,000 transactions per second" |

> **Memory Hook:**  
> **Latency** = "How fast for **one** request?"  
> **Throughput** = "How many requests **per second**?"

> **Pro Tip — exam favourite:** A common question is *"distinguish between latency and throughput"*. Use the table above + concrete examples. Easy 5 marks.

---

### 11.5 Reliability

> **Definition:** Ability of a system to **remain operational over time** — the **probability** that a system will not fail to perform its intended functions over a specified time interval.

**Affected by:**
- **Availability** (if it's down, it's not reliable)
- **Accuracy** (if it gives wrong answers, it's not reliable)
- **Predictability** (if behaviour is erratic, it's not reliable)

> **Memory Hook:** *"Reliability = Can I trust it not to break?"* Measured as MTBF (Mean Time Between Failures) in formal contexts.

> **Watch out:** **Availability** is a *snapshot* ("up right now?"). **Reliability** is *over time* ("does it stay up reliably?").

---

### 11.6 Reusability

> **Definition:** Capability for **components and subsystems** to be **suitable for use in other applications** and in other scenarios. Minimises duplication of components and implementation time.

**Examples:** Software libraries, npm packages, JAR files, microservices that other services can call.

> **Memory Hook:** *"Reusability = Build once, use many."*

> **⚠️ Cautionary tale:** Recall **Therac 25** from Lecture 5 — *reusability without context awareness can be deadly*. Reusing software from one machine to another, without re-validating safety assumptions, killed people.

---

### 11.7 Scalability ⭐

> **Definition:** Ability of a system to **handle increases in load without performance degradation**, or the **ability to be readily enlarged**.

**4 dimensions of "load" to scale against:**

| Dimension | Example |
|---|---|
| **Load** (request volume) | 100 → 1 million users |
| **Functions** (number of features) | Adding new features doesn't slow it down |
| **Geographic** | Serving Sri Lanka → serving Asia → serving the world |
| **Methods** | Adding new APIs without bottleneck |

**2 methods to achieve scalability:** ⭐ (very examable!)

| Method | What it means | Analogy |
|---|---|---|
| **Horizontal scaling** | **Add more servers** (more machines doing the same work in parallel) | Hire more cashiers at the supermarket |
| **Vertical scaling** | **Upgrade hardware** of the same server (more CPU, RAM) | Make your one cashier work faster (give them caffeine!) |

> **Memory Hook — "H = Many. V = Mighty."**  
> Horizontal = many smaller machines.  
> Vertical = one mightier machine.

> **Pro Tip:** Distributed architectures (microservices, cloud-native) typically rely on **horizontal scaling**; classic monoliths often **scale vertically** until they hit a hardware ceiling.

---

### 11.8 Security

> **Definition:** Capability of **preventing malicious attacks** and **unauthorised usage**, and **protecting system assets** (data, hardware).

**Examples of threats:** Viruses, malicious users, data theft, hardware tampering.

**The slide's tricky question (slide 24):**

> *"Denial of Service (DoS): Is this a Security issue? Is this **only** a Security issue?"*

**Answer:** DoS attacks **are** a security issue (malicious actor preventing legitimate access), but they are **also** an **availability** issue (the system becomes unavailable). They sit at the intersection of security and availability — a beautiful example of how quality attributes **overlap**.

> **Memory Hook:** *"Security = Keep bad guys out, keep good stuff in."*

> **Pro Tip:** Use the DoS example in any question about **overlapping quality attributes** or **the relationship between security and availability**.

---

### 11.9 Testability

> **Definition:** Ability to **create test criteria** for the system and its components and to **execute these tests** to determine if the criteria are met.

**Key questions testability answers:**
- How **much** can be tested?
- How **much time** does it take to test?

**Why it matters:** Testability makes it more likely that **faults can be isolated** in a **timely and effective** manner.

> **Memory Hook:** *"Testability = Can I prove it's correct cheaply?"*

> **Pro Tip:** Testability is closely linked to **Modularity** and **Low Coupling** (Lec 4). The more decoupled your modules, the more testable they are in isolation.

---

### 11.10 Usability

> **Definition:** How well the application meets the requirements of the user — by being **intuitive**, easy to **localise/globalise**, providing **good access for disabled users**, and resulting in a **good overall user experience**.

**5 considerations of usability** (slide 26):

1. **Learnability** — how easy is it to learn the features?
2. **Efficiency** — how efficiently can the user use the system?
3. **Error handling** — how well does the system handle user errors?
4. **Adaptability** — how well does it adapt to user needs?
5. **Confidence** — to what degree does the system give the user confidence in the correctness of its actions?

> **Memory Hook — "LEEAC"** → **L**earn, **E**fficient, **E**rror handling, **A**dapt, **C**onfidence.

> **Pro Tip:** Usability is often confused with UI design. **They're not the same.** UI is *visuals*. Usability is whether users can *successfully accomplish their goals*. Make this distinction in the exam.

---

## 12. Summary Table — All 10 Quality Attributes ⭐ (revision sheet)

| # | Attribute | One-line definition | Key sub-concepts |
|---|---|---|---|
| 1 | **Availability** | Up when users need it | % uptime |
| 2 | **Interoperability** | Talks to other systems | Syntactic + Semantic |
| 3 | **Modifiability** | Cheap to change | Functional / Environment / Protocol / Dependency change |
| 4 | **Performance** | Fast response | **Latency + Throughput** |
| 5 | **Reliability** | Doesn't break over time | MTBF |
| 6 | **Reusability** | Components used elsewhere | Libraries |
| 7 | **Scalability** | Handles more load | **Horizontal + Vertical** |
| 8 | **Security** | Blocks malicious use | DoS overlaps with availability |
| 9 | **Testability** | Easy to verify correctness | Linked to modularity |
| 10 | **Usability** | Users can succeed | LEEAC: Learn, Efficient, Errors, Adapt, Confidence |

> **Pro Tip — exam revision:** Photocopy this table. Use it as your A4 reference sheet template.

---

## 13. Architectural Attributes (slide 27) — different from system QAs

These are **qualities of the architecture itself**, not of the running system. **3 of them**:

| # | Architectural Attribute | What it means |
|---|---|---|
| 1 | **Conceptual Integrity** | The architecture should **do similar things in similar ways**. Consistency across modules. |
| 2 | **Correctness and Completeness** | Check the architecture for **errors and omissions**. Did we miss anything? |
| 3 | **Buildability** | Can the **available team finish it in a reasonable time**, while staying open to changes during development? |

> **Memory Hook — "CCB"** → **C**onceptual integrity · **C**orrectness/completeness · **B**uildability.

> **Pro Tip:** *"Conceptual integrity"* is a famous term coined by Fred Brooks (*The Mythical Man-Month*). Mentioning him is fine for bonus credibility.

---

## 14. Coming Up Next 👀

Two preview slides at the end:

- **Lecture 7: Quality Attribute Scenarios (QAS)** — a *formal, universal way* to express quality attributes (like a use case for QAs). Captures and documents **unambiguous, testable** requirements.

- **Lecture 8: Tactics** — *means of satisfying* a quality attribute response measure by manipulating an aspect of the QA model through architectural decisions. The "**how**" to actually achieve a quality attribute.

So the story arc is:
- **Lec 6 (this lecture)** = *what* the quality attributes are.
- **Lec 7** = *how to formally describe* them (QAS).
- **Lec 8** = *how to actually achieve* them (Tactics).

---

## 15. One-Shot Summary (the morning of the exam)

> Software requirements split into **four types**: **Functional** (what it does), **Non-Functional / Quality Attributes** (how well — the "-ilities"), **Business Requirements** (strategic, *negotiable*), and **Constraints** (rules with **no trade-offs allowed**). The architect identifies the **Architecturally Significant Requirements (ASRs)** at the start of the project. Functionality and quality are **orthogonal** — for the same features you can build endless architectures of differing quality. Quality Attributes are **measurable, testable** properties; the **ISO 25010** standard groups them into 8 categories. Quality attributes apply at use-case, module, or system level; they cover both design-time (modifiability, testability) and runtime (performance, availability) phases; and they **impact each other** — performance is affected by almost everything. The architect's job is to (1) understand QA priorities and (2) make trade-offs among them. The 10 core attributes covered are **Availability** (% uptime), **Interoperability** (syntactic + semantic), **Modifiability** (cost to change), **Performance** (latency + throughput), **Reliability** (no failures over time), **Reusability** (build once, use many), **Scalability** (horizontal + vertical), **Security** (DoS overlaps with availability), **Testability** (verify cheaply), and **Usability** (LEEAC). Three **architectural attributes** describe the architecture itself: **Conceptual Integrity**, **Correctness/Completeness**, and **Buildability**. Next we'll learn how to formally document QAs as **Quality Attribute Scenarios (QAS)** and how to satisfy them using **Tactics**.

---

## 16. Likely Exam Questions (and how to answer)

**Q1. Distinguish between Functional and Non-Functional requirements with examples.**  
→ Functional = what it does. NFR = how well. Use the calculator example from section 3.

**Q2. Distinguish between Business Requirements and Constraints.**  
→ Business = negotiable, trade-offs allowed. Constraints = locked in, no trade-offs. Examples each.

**Q3. Define quality attributes and explain why they are orthogonal to functionality.**  
→ Definition: measurable, testable properties indicating how well stakeholder needs are met. Orthogonal = same features can be implemented in many architectures, the difference being which qualities they prioritise.

**Q4. Define and explain any 5 quality attributes.**  
→ Pick 5 from the 10. Always include the **definition + sub-concepts + how to measure** for each.

**Q5. Distinguish between Latency and Throughput.**  
→ Latency = time per single event. Throughput = events per time. Use concrete numbers.

**Q6. Distinguish between Horizontal and Vertical scaling.**  
→ Horizontal = add servers. Vertical = upgrade hardware. Use the cashier analogy.

**Q7. Distinguish between Syntactic and Semantic interoperability.**  
→ Syntactic = same data format/protocol. Semantic = same meaning. Use the USD currency example.

**Q8. Why are Quality Attribute definitions sometimes confusing?**  
→ Three reasons: grouped differently by authors, overlapping attributes (security & integrity), and confusion with meaning (performance = responsiveness OR efficiency).

**Q9. Explain the role of an architect with respect to quality attributes.**  
→ (1) Understand importance & priority of QAs. (2) Evaluate and make trade-offs to meet quality levels that satisfy stakeholders.

**Q10. What are architectural attributes? List and explain.**  
→ Conceptual Integrity, Correctness & Completeness, Buildability. They describe the architecture itself.

---

## 17. Vocabulary You Should Use Confidently

- **Architecturally Significant Requirements (ASRs)** — the requirements that shape the architecture.
- **Functional / Non-Functional Requirements** — what / how well.
- **Business Requirement vs Constraint** — negotiable vs locked.
- **Orthogonal** — independent dimensions (functionality and quality).
- **ISO 25010** — international standard for software quality.
- **Latency / Throughput** — performance metrics.
- **Horizontal / Vertical scaling** — scalability methods.
- **Syntactic / Semantic interoperability** — same envelope vs same meaning.
- **MTBF** (Mean Time Between Failures) — reliability metric.
- **Conceptual Integrity** — Fred Brooks's idea: do similar things in similar ways.
- **Quality Attribute Scenario (QAS)** — formal, testable QA requirement (next lecture).
- **Tactic** — architectural means to satisfy a QA (next lecture).

---

## 18. References

- Bass, Clements & Kazman — *Software Architecture in Practice* (multiple editions cover quality attributes in depth).
- **ISO 25010:2011** — Systems and software Quality Requirements and Evaluation (SQuaRE).
- Fred Brooks — *The Mythical Man-Month* (origin of "Conceptual Integrity").

---

**Pro Tip — connection to previous lectures:**
- **Lec 1** introduced the **SQDP** definition; QAs are the **Q**.
- **Lec 4** showed quality attributes drive the **architecture quantum** decision (monolith vs distributed).
- **Lec 5** showed how Stack Overflow prioritised **Performance** and Uber prioritised **Maintainability/Scalability** — leading to very different architectures.
- **This lecture** gives you the **vocabulary and definitions** to discuss any quality attribute precisely.
- **Lec 7 & 8** will show you *how to write QAs formally* and *how to actually achieve them*.

Send Lecture 7 when you're ready. 🚀
