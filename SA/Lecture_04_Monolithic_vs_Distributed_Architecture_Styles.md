# Lecture 04 — Choosing Between Monolithic and Distributed Architecture Styles

**Module:** SE3030 — Software Architecture · Semester 1, 2026 · SLIIT

> Welcome to one of the **most exam-critical lectures** in the module. This is the one where you learn how to actually answer the big question every architect faces: *"Should I build this as a monolith or as a distributed system?"* The answer hinges on a brilliant little concept called the **Architecture Quantum**. We'll build up to it step by step. ☕

---

## What you should walk away knowing

1. **Quality attributes drive architecture** — and they often **trade off** against each other.
2. The **3 modularity metrics**: Cohesion, Coupling, Connascence.
3. The difference between a **module** (logical) and a **component** (physical).
4. The two ways to **partition** an architecture: **Technical** vs **Domain**.
5. What an **Architecture Quantum** is (and its 4 properties).
6. How to use the quantum concept to decide between **Monolithic** and **Distributed** architecture styles.
7. The **complexity cost** of going distributed.

> **Pro Tip — exam favourite:** *"Define an Architecture Quantum and explain how it helps in choosing between monolithic and distributed architecture styles."* This is the headline question for this lecture. Memorise the 4 quantum properties cold.

---

## 1. Quality Attributes Drive Architecture (Quick Recap)

You've seen this in Lec 1. Quick refresh:

> **Functional requirements** = what the system *does*.  
> **Quality attributes** = the **success criteria** beyond *"does it work"*. The *"-ilities"*.

Quality attributes are **orthogonal to functionality** — you can talk about them without knowing what the system does ("it must be 99.99% available"; that statement applies whether it's a banking app or a game).

The **9 most-mentioned quality attributes** in the slide (Figure 1-4):

| Operational | Cross-cutting | Structural |
|---|---|---|
| Availability | Security | Testability |
| Reliability | | Agility |
| Scalability | | Recoverability |
| Fault Tolerance | | Learnability |
| Elasticity | | Deployability |
| Performance | | |

### 🪙 The Killer Idea — Trade-off Thinking

> **Improving one quality attribute often degrades another.** Architecture is the art of **managing trade-offs**.

Classic trade-offs from the slide:

| If you boost… | …you often hurt |
|---|---|
| **Performance** (caches everywhere, custom code) | **Modifiability** (rigid, hard to change) |
| **Availability** (replicate data widely, accept stale reads) | **Consistency** (data may be temporarily out of sync — CAP theorem) |
| **Security** (multiple auth checks, encryption, MFA) | **Usability** (users hate friction) |

> **Memory Hook — "PMACSU"**: **P**erformance vs **M**odifiability · **A**vailability vs **C**onsistency · **S**ecurity vs **U**sability.

> **Pro Tip — exam phrase to memorise:** *"Architecture is the art of managing trade-offs between competing quality attributes."* Drop this in any open-ended architecture question. Markers love it.

---

## 2. Modularity — The Organizing Principle

> A **module** is a logical grouping of related code (e.g., a group of classes in OOP, or related functions in functional code). Think: a folder, a Python module, a Java package.

The dictionary version: *"each of a set of standardized parts or independent units that can be used to construct a more complex structure."* (Like LEGO bricks 🧱 — the slide even shows this.)

### Why bother with modularity?
- A system designed without paying attention to how pieces wire together → **chaos / "Big Ball of Mud"**.
- Architects must **constantly invest energy** in keeping the structure clean — it does NOT happen by accident.
- **Sustainable code bases require order and consistency.**

### Modules are assessed under **3 metrics** ⭐ (memorise!)

```
            ┌─────────────────────┐
            │     MODULARITY      │
            │  measured by 3 things │
            └─────────────────────┘
                      │
       ┌──────────────┼──────────────┐
       ▼              ▼              ▼
   Cohesion      Coupling      Connascence
  (inside)       (outside)    (change-link)
```

> **Memory Hook — "3 C's: Cohesion, Coupling, Connascence."**

Now let's unpack each.

---

### 2a. Cohesion — *"How together is the code inside one module?"*

> Cohesion = how well the code **within a module** is **unified in purpose**.

**Higher cohesion = better.** A highly cohesive module does **one thing well**.

**Bad (low cohesion):** A `Utils` module containing logging, date formatting, sending emails, and parsing JSON. ❌  
**Good (high cohesion):** A `PaymentProcessor` module that *only* handles payment processing. ✅

> **Memory Hook:** *"Cohesion = inside a module. We want it HIGH (everyone is on the same team)."*

---

### 2b. Coupling — *"How tied is one module to other modules?"*

> Coupling = how strongly **one module is connected to other modules**.

**Lower coupling = better.** High coupling means a change in module A forces changes in B, C, D, E…

**Bad (high coupling):** Module A calls 15 internals of Module B; if B changes a method name, A breaks. ❌  
**Good (low coupling):** Module A only calls Module B's clean public interface. B's internals can change freely. ✅

> **Memory Hook:** *"Coupling = between modules. We want it LOW (modules should be polite acquaintances, not soulmates)."*

> **Pro Tip — golden rule:** *"High Cohesion, Low Coupling"* is a **mantra**. Repeat it like a meditation. It will earn you marks in many questions.

---

### 2c. Connascence — *"If A changes, does B have to change too to keep the system correct?"*

> Two modules are **connascent** if a change in one **requires the other to be modified** to maintain **overall system correctness**.

Connascence is a **deeper, more nuanced** way of measuring **the degree of coupling** between two modules. It highlights **change-based dependency**.

**Example:** Module A serializes a `User` object as JSON `{name, email}`. Module B parses that JSON and reads `name` and `email`. If A renames `email` → `emailAddress`, B will break.  
→ A and B are **connascent on the field name `email`**.

> **Memory Hook:** *"Connascence = 'they were born together' (Latin: con + nascere). Change one, you must change the other."*

> **Pro Tip — relating the 3 C's:**
> - **Cohesion** describes **inside** a module.
> - **Coupling** describes **between** modules in general.
> - **Connascence** describes the **specific change-based dependency** between modules — a finer measure of coupling.

---

## 3. Modules vs Components — Logical vs Physical

This distinction is **subtle but examable**.

| | Module | Component |
|---|---|---|
| What | A **logical grouping** of related code. | The **physical manifestation / packaging** of modules. |
| Form | A folder, a package, a namespace. | A JAR (Java), a DLL (Windows), a `.so` library, a deployable bundle. |
| Who reasons about it | Developers, code organisers. | **Architects** — they primarily reason at this level. |

> **Key sentence to memorise:** *"Components are the physical manifestation (or **realisation**) of modules. Architects primarily reason at the **component level** — the high-level system structure."*

So the architect's chain of thinking:

```
   Code  →  Module (logical group)  →  Component (physical package)  →  Architecture
```

---

## 4. Architecture Partitioning — Two Ways to Slice the Pie ⭐

A **key architectural decision** is how the **top-level components** are organised. This is called **Architecture Partitioning**, and there are **two main ways**:

| | Technical Partitioning | Domain Partitioning |
|---|---|---|
| Components organised by | **Technical capability** (presentation, business logic, persistence) | **Business domain** (CatalogCheckout, ShipToCustomer, Reporting…) |
| Looks like | **Layered architecture** (MVC, classic 3-tier) | **Bounded contexts** (DDD style) — modular monolith, microservices |
| Top-level boxes | Presentation / Business Rules / Service / Persistence | CatalogCheckout / UpdateInventory / ShipToCustomer / Analytics |

### Visual contrast (the famous slide diagram)

```
   TECHNICAL PARTITIONING              DOMAIN PARTITIONING
   ┌───────────────────┐                ┌────────────────────────────┐
   │  Presentation     │                │ CatalogCheckout │ Inventory │
   ├───────────────────┤                ├─────────────────┼───────────┤
   │  Business rules   │                │ ShipToCustomer  │ Reporting │
   ├───────────────────┤                ├─────────────────┼───────────┤
   │  Service          │                │ Analytics       │ Accounts  │
   ├───────────────────┤                └────────────────────────────┘
   │  Persistence      │                            │
   └───────────────────┘                            ▼
              │                                 Database
              ▼
          Database
```

### Technical Partitioning — Pros & Cons

| Pros | Cons |
|---|---|
| Clear separation of code into layers | **Higher global coupling** — a small business workflow change touches *every layer* |
| Naturally aligns with the **Layered architecture pattern** | **Duplication** of domain concepts across layers |
| Easy to find "the data layer" or "the UI layer" | Higher data-level coupling (single shared DB) |
| | **Hard to migrate to distributed** later — too tightly intertwined |

### Domain Partitioning — Pros & Cons

| Pros | Cons |
|---|---|
| **Models the business** closely (not technical implementation) | Related code appears in **multiple places** (e.g., Customer logic in both ShipToCustomer & UpdateAccounts) |
| Easier to apply **Inverse Conway Maneuver** (build cross-functional teams around domains) | Shared technical concerns (logging, security, transactions) need extra coordination — **cross-cutting concerns** |
| **Message flow** matches the problem domain | |
| **Easier migration to distributed architecture** later | |

> **Memory Hook:**  
> **Technical = stack of layers (cake slices horizontally).** 🎂  
> **Domain = grid of business pieces (cake cut into squares).** 🟦🟦🟦
>
> If the question is "I want layers" → **Technical**.  
> If the question mentions "bounded context", "business domain", or "microservices later" → **Domain**.

> **Industry Trend (slide 24):** Domain partitioning is **clearly winning** in the industry. Both **modular monoliths** and **microservices** use it. *Neither is inherently more correct*, but write down "industry trend favours domain partitioning" if asked.

---

## 5. Architecture Quantum ⭐⭐⭐ (the headline concept!)

> An **Architecture Quantum** is:
> 1. An **independently deployable artifact**
> 2. With **high functional cohesion**
> 3. With **synchronous connascence**
> 4. **Sharing a uniform set of quality attributes**

(Singular: **quantum**. Plural: **quanta**. From Latin.)

That definition is the **gold-standard exam answer** — memorise it word-for-word.

### Why does it matter?

> The **architecture quantum** is the **unit at which quality attributes are applied**. Whether you build a monolith or a distributed system **depends entirely on how many quanta your design has**.

So the workflow is:

```
   Components → Group by partitioning strategy → Identify Architecture Quanta
                                                              │
                                                              ▼
                                                   How many quanta do you have?
                                                   ┌─────────┴─────────┐
                                                   ▼                   ▼
                                                One quantum      Multiple quanta
                                                   ▼                   ▼
                                              MONOLITHIC          DISTRIBUTED
```

### Unpacking the 4 properties (memorise these one-liners)

| # | Property | What it means |
|---|---|---|
| 1 | **Independently Deployable** | The quantum contains *everything* it needs to run. You can build, deploy, and operate it **without** deploying other parts of the system simultaneously. |
| 2 | **High Functional Cohesion** | All components inside the quantum are **related** to each other and **collectively serve one clear functional objective**. The quantum has nothing extra and nothing missing. |
| 3 | **Synchronous Connascence** | The components inside talk **synchronously** (caller waits for callee). During that call, both must maintain **compatible quality attributes** (latency, availability, scalability). Otherwise → timeouts and reliability failures. |
| 4 | **Uniform Set of Quality Attributes** | Everything in the quantum agrees on the **same** quality requirements. (E.g., "everything in this quantum must be 99.99% available, 200ms latency.") |

> **Memory Hook — "ID-CON-CON-Q"**:  
> **I**ndependently **D**eployable + **CON**hesion (functional, high) + **CON**nascence (synchronous) + **Q**uality attributes (uniform).

### A quick story to make it click

Imagine an e-commerce system. Two parts:

- **Catalog browsing** — needs **high availability** (99.99%), **low latency** (<100ms), **read-heavy**, **stateless**.
- **Year-end financial reporting** — needs **high consistency**, **batch processing**, **low concurrency**, **runs once a day**.

These **cannot** share quality attributes. They are **two different quanta**. → **Distributed architecture** is the natural fit.

But for a small library management system used by 50 students, every part needs the *same* quality (modest performance, modest availability, modest scalability). **One quantum** → **monolith** is fine.

---

## 6. Broad Categories of Architecture Styles

Slide 31 — based on **type of deployment**, all architecture styles fall into **two camps**:

| Category | Definition | Examples |
|---|---|---|
| **Monolithic** | A **single deployment unit** of code | Layered, Pipeline, Microkernel, Modular Monolith |
| **Distributed** | **Multiple deployment units** connected by **remote access protocols** | Microservices, Service-based, Event-driven, Space-based, Service-Oriented (SOA) |

> **Memory Hook:** *"Monolith = one big block. Distributed = many small blocks talking over the network."*

This list is **highly examable**. Memorise at least **2–3 examples per category**.

---

## 7. Choosing Between Monolithic vs Distributed ⭐⭐

This is the **key decision-making framework** of the lecture.

### The decision question

> *"Can the entire system operate under a single set of quality attributes? Or do different parts require different quality attributes?"*

### The decision tree

```
   Does your system have ONE consistent set of quality attributes
   that works for the whole thing?
                  │
        ┌─────────┴─────────┐
        │                   │
       YES                  NO
        │                   │
        ▼                   ▼
   ONE QUANTUM        MULTIPLE QUANTA
        │                   │
        ▼                   ▼
   MONOLITHIC          DISTRIBUTED
   (Layered,           (Microservices,
   Modular monolith)   Event-driven, SOA)
```

### The classic example to use in the exam

> **Security vs Performance.** A **payments** part of the system needs maximum security (slow, multiple checks, audit trails). A **product catalog** part needs maximum performance (fast, cacheable, public). These quality attributes **conflict**. → Two quanta. → Distributed architecture.

### Side-by-side comparison (memorise this table) ⭐

| Aspect | Monolithic | Distributed |
|---|---|---|
| **Quality Attributes** | Uniform (single quantum) | Per quantum |
| **Deployment** | Single unit | Multiple units |
| **Operational Complexity** | **Lower** ✅ | **Higher** ❌ |
| **Scalability** | Whole system scales together | Per quantum (scale only what's hot) |
| **Failure Isolation** | Low (one bug = whole system down) | Higher (failure of one service is contained) |
| **Network Concerns** | None (all in-process) | Yes (latency, partial failure, security) |
| **Database** | Usually a single shared DB | Each service may have its own DB |
| **Release** | Must release all together | Independent release cadences per service |
| **Examples** | Layered, Modular Monolith | Microservices, Space-based, SOA |
| **Use when** | One consistent quality set is enough | Different parts need different qualities |

> **Pro Tip — Don't fall for the hype.** Distributed (especially microservices) is *not* automatically better. They're only correct when you genuinely have **multiple quanta** with **different quality needs**. For a startup, school project, or small internal tool → **monolith wins** every time.

---

## 8. The Complexity Cost of Distribution ⚠️

Distribution **buys you** flexibility, scalability, fault isolation, but at a **real cost**.

### The Fallacies of Distributed Computing
A famous list, first coined by **L. Peter Deutsch and colleagues at Sun Microsystems in 1994**. These are *false assumptions* developers often make about networks.

The 8 fallacies (worth recognising — the slide says **"Read this"**, so it's likely examable):

1. The network is **reliable**. (No — it isn't.)
2. **Latency** is zero. (No — every call has cost.)
3. **Bandwidth** is infinite. (No — it has limits.)
4. The network is **secure**. (No — assume hostile.)
5. **Topology** doesn't change. (No — servers come and go.)
6. There is **one administrator**. (No — many people manage parts.)
7. **Transport cost** is zero. (No — there's CPU, serialisation, hardware.)
8. The network is **homogeneous**. (No — many different stacks involved.)

> **Memory Hook:** *"Networks lie. Plan for it."* When you go distributed, you sign up to fight **all 8** of these.

> **Pro Tip:** If asked about the **costs / risks of distributed architectures**, mention: (1) operational complexity, (2) network failure modes, (3) data consistency challenges (eventual consistency), (4) debugging difficulty (need distributed tracing), (5) the fallacies of distributed computing.

---

## 9. The Complete Mental Workflow (one big picture)

Tying everything together:

```
       Quality Attributes (the drivers)
                  │
                  ▼
            Modularity  ◄─── (measured by Cohesion, Coupling, Connascence)
                  │
                  ▼
         Modules (logical)
                  │
                  ▼
        Components (physical)
                  │
                  ▼
   Architecture Partitioning
   (Technical or Domain)
                  │
                  ▼
   Group into Architecture Quanta
   (4 properties: independently deployable,
    high functional cohesion,
    synchronous connascence,
    uniform quality attributes)
                  │
       ┌──────────┴──────────┐
       ▼                     ▼
   ONE quantum         MULTIPLE quanta
       ▼                     ▼
  MONOLITHIC            DISTRIBUTED
  (layered, modular     (microservices,
   monolith…)            event-driven, SOA…)
```

> **Pro Tip — exam essay structure.** If asked "How do you decide between monolithic and distributed?", **walk through this whole pipeline** — it shows architectural maturity. Quality attributes → modularity → components → partitioning → quanta → decision. Easy first-class answer.

---

## 10. One-Shot Summary (the morning of the exam)

> **Quality attributes** — not functional requirements — drive architectural decisions, and they often **trade off** against each other (Performance vs Modifiability, Availability vs Consistency, Security vs Usability). System code is organised into **modules** measured by 3 metrics: **Cohesion** (high inside, good), **Coupling** (low between, good), and **Connascence** (a finer change-based measure). Modules are physically packaged as **components** (JARs, DLLs), which architects use as their main reasoning unit. Components are organised top-level by **Architecture Partitioning** — either **Technical** (by tech layers — leads to layered architecture) or **Domain** (by business domain — leads to modular monoliths and microservices; **industry trend favours domain**). Components that are highly related and share the same quality attributes form an **Architecture Quantum** — defined by 4 properties: **independently deployable**, **high functional cohesion**, **synchronous connascence**, and **uniform quality attributes**. The fundamental architecture decision is: *can the whole system operate under one quality-attribute set (one quantum → monolithic)*, or does it need *multiple sets (multiple quanta → distributed)*. Distributed gives flexibility and scalability per quantum but adds **operational complexity**, **network concerns**, and the **fallacies of distributed computing** — never go distributed without justification.

---

## 11. Likely Exam Questions (and how to answer)

**Q1. Define cohesion, coupling, and connascence.**  
→ Use the 3 sub-sections in section 2. Always conclude with the mantra: *"High Cohesion, Low Coupling"*.

**Q2. What is the difference between a module and a component?**  
→ Module = logical grouping (folder, package). Component = physical packaging (JAR, DLL). Architects reason at the component level.

**Q3. Compare Technical Partitioning and Domain Partitioning with their pros and cons.**  
→ Use the comparison + the two pros/cons tables. Mention industry trend = domain.

**Q4. Define Architecture Quantum and list its 4 properties.**  
→ The 4 properties verbatim: independently deployable, high functional cohesion, synchronous connascence, uniform set of quality attributes.

**Q5. How does Architecture Quantum help in choosing between Monolithic and Distributed architecture styles?**  
→ Use the decision tree. *One quantum → monolith. Multiple quanta → distributed.* Use the security-vs-performance example.

**Q6. List the advantages and disadvantages of monolithic and distributed architectures.**  
→ Use the side-by-side table in section 7.

**Q7. Why is distributed architecture not always the right choice?**  
→ The Complexity Cost section. Bring up operational complexity, network failure modes, eventual consistency, debugging, and the **8 fallacies of distributed computing**.

**Q8. Explain trade-off thinking in software architecture with examples.**  
→ Quote *"Architecture is the art of managing trade-offs."* Use Performance↔Modifiability, Availability↔Consistency, Security↔Usability.

---

## 12. Vocabulary You Should Use Confidently

- **Quality Attribute** / **Architecture Characteristic** / **"-ility"** — non-functional requirement.
- **Trade-off** — improving one quality often degrades another.
- **Modularity** — the organising principle of code into related units.
- **Cohesion** — internal unity of a module (HIGH = good).
- **Coupling** — connection strength between modules (LOW = good).
- **Connascence** — change-based dependency between modules.
- **Module** — logical grouping of code.
- **Component** — physical manifestation/packaging of modules.
- **Architecture Partitioning** — top-level organisation of components.
- **Technical Partitioning** — by technical layer.
- **Domain Partitioning** — by business domain (Bounded Context).
- **Bounded Context** — a clearly delimited business area (from Domain-Driven Design).
- **Inverse Conway Maneuver** — building cross-functional teams matched to architectural boundaries.
- **Architecture Quantum / Quanta** — the unit at which quality attributes are applied (4 properties!).
- **Monolithic** — single deployment unit.
- **Distributed** — multiple deployment units over a network.
- **Fallacies of Distributed Computing** — the 8 false assumptions about networks.
- **Synchronous connascence** — caller-waits-for-callee dependency.

---

## 13. References & Further Reading

- Richards, Mark, & Ford, Neal — *Fundamentals of Software Architecture: An Engineering Approach* — read **chapters 03, 04, 07, 08 & 09**.
- The **Fallacies of Distributed Computing** (Deutsch et al., 1994) — Google it. Short, eye-opening read.

---

**Pro Tip — connection to Lectures 1, 2, 3:**
- **Lec 1** = What is architecture? (SQDP / Squid P)
- **Lec 2** = How is it produced? (Influences → Activities → Strategies)
- **Lec 3** = How do we view/document it? (Structures, Views, 4+1 Model)
- **Lec 4** = How do we choose between **monolith** and **distributed**? (Quality attributes → Modularity → Components → Partitioning → **Architecture Quantum** → decision)

Notice how every lecture builds on the last. The **Architecture Quantum** is *the* concept that ties this lecture into a single decision-making tool. Memorise its 4 properties — they will save you in the exam.

Send Lecture 5 when you're ready. 🚀
