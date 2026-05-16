# Lecture 03 — Architectural Structures and Views

**Module:** SE3030 — Software Architecture · 3rd Year, Semester 1 · SLIIT  
**Lecturer:** Chathura R De Silva

> Hi again! This lecture is short but **very important** for the exam. It teaches us that a software system is not a single picture — it's like the human body, which has a **skeletal system**, a **nervous system**, a **blood circulatory system**, etc. Each is a different *view* of the **same body**. Software is the same. Let's dig in. ☕

---

## What you should walk away knowing

1. The **difference between a Structure and a View** (one is reality, the other is the drawing).
2. The **3 categories of structures**: Module, Component-and-Connector (C&C), and Allocation — and what's inside each.
3. The **4+1 View Model** (Logical, Development, Process, Physical + Scenarios).
4. Which **stakeholders care about which views**.
5. A taste of the **Zachman Framework** (enterprise architecture).

> **Pro Tip — exam favourite.** *"List and explain the three main types of architectural structures, with at least one sub-structure for each."* This is almost guaranteed somewhere on the paper. Memorise the **Module / C&C / Allocation** split.

---

## 1. View vs Structure — the most important definitions ⭐

These two words sound the same. They are **not**. Mix them up in the exam and you lose marks.

### Definitions (memorise verbatim)

> **Structure** = the **set of elements itself**, as they exist in the software or hardware.  
> **View** = a **representation** of a coherent set of architectural elements, **written and read by stakeholders**. A view shows a set of elements + the relations among them.

### Plain English version
- **Structure = the real thing.** (The actual modules in your codebase, the actual servers running in production.)
- **View = the picture / document of that real thing.** (The UML diagram you drew, the deployment diagram on Confluence.)

> **Memory Hook — "Structure is the body. View is the X-ray."**  
> The body exists whether or not you take an X-ray. The X-ray is just one way to *see* the body. You can take 10 different X-rays of the same body — each shows different stuff.

### Module example from the slide

| | Definition |
|---|---|
| **Module structure** | The actual set of the system's modules and their organization. |
| **Module view** | The *representation* (diagram, document) of that structure, used by stakeholders. |

> **Note from slide 3:** these terms are *often used interchangeably in industry*, but in this module we'll stick to the precise definitions. **Use them precisely in the exam.**

> **Pro Tip:** If the question says *"draw a deployment view"*, it means draw the diagram. If it asks *"what is the deployment structure of the system"*, it's asking about the actual deployment of software onto hardware.

---

## 2. The body analogy (the "elsewhere" example on slide 4)

This is the lecturer's killer analogy. The slide shows three pictures of a human:
- **Skeletal system** (bones)
- **Nervous system** (nerves)
- **Circulatory system** (blood vessels)

**Same body. Three completely different structures, each highlighting a different aspect.**

A software system is identical: one system, many structures.

> **Memory Hook:** Whenever the exam asks "why do we need multiple views/structures?" → use the body analogy. Markers love it because it's intuitive.

---

## 3. The 3 Architectural Considerations → the 3 Structure Categories ⭐

The lecture frames it as **3 questions the architect must answer**:

| Question | Answered by | Structure category |
|---|---|---|
| 1. How is the system structured as a set of **code units**? | Modules | **Module Structures** |
| 2. How is the system structured as a set of elements with **runtime behavior and interactions**? | Components & Connectors | **Component-and-Connector (C&C) Structures** |
| 3. How does the system **relate to non-software** stuff in its environment? (CPU, files, network, dev team) | Allocation | **Allocation Structures** |

So we have **3 categories of structures**:

```
                       ┌─────────────────────────────┐
                       │      Software Structures    │
                       └─────────────────────────────┘
                                     │
            ┌────────────────────────┼─────────────────────────┐
            ▼                        ▼                         ▼
       Module                  Component-and-                Allocation
       Structures               Connector (C&C)              Structures
                                  Structures
            │                        │                         │
   ┌────────┼────────┐     ┌─────────┼────────┐       ┌────────┼──────────┐
   ▼        ▼        ▼     ▼         ▼        ▼       ▼        ▼          ▼
 Decomp.  Uses    Class  Process  Concurrency Shared  Deploy.  Implement.  Work
 (+Layers)         (Gen)            (etc.)   Data            ation       Assign.
                                            Client-
                                            Server
```

> **Memory Hook — "MCA"** → **M**odule, **C**omponent-and-Connector, **A**llocation. Like the airport code for Macau. ✈️
>
> Or remember the three questions:
> - **Code-time** → Module (how is the code organised?)
> - **Run-time** → C&C (what's happening when the system is running?)
> - **Map-to-real-world-time** → Allocation (where does it live? who builds it?)

---

## 4. Module Structures (code-time view) — 4 types

**Element = a module = a "unit of implementation"** (think: a Java package, a Python module, a folder in your codebase).

The architect uses module structures to answer:
- What is the **primary functional responsibility** of each module?
- What other modules is this module **allowed to use**?
- What does it **actually use**?

### The 4 module structures (memorise these)

| # | Structure | What it shows |
|---|---|---|
| 1 | **Decomposition** | How **larger modules break down into smaller** ones, recursively. (E.g., "Payment module" contains "Payment Gateway" and "Refund Processor".) |
| 2 | **Uses** | Which module **uses** which. ("Module A *requires the correct presence of* Module B.") |
| 3 | **Layers** | Modules grouped into **layers**, where each layer uses only the layer(s) below it. (You saw this in Lec 1 — Presentation / Business / Data.) |
| 4 | **Class (Generalization)** | The **inherits-from** / **is-an-instance-of** relations. (Pure OOP — class diagrams.) |

> **Memory Hook — "DULC"** (rhymes with "Hulk") → **D**ecomposition, **U**ses, **L**ayered, **C**lass.

> **Pro Tip:** When asked to draw a module decomposition, draw a **tree** (parent module → child modules). When asked to draw "Uses", draw an arrow from the using module to the used module.

---

## 5. Component-and-Connector (C&C) Structures (run-time view) — 4 types

**Elements = runtime components and connectors.**  
- **Component** = something that is *running* (a process, a service, a database server).  
- **Connector** = how those components talk (a protocol, a message queue, a socket).  
- **Relation** = "attachment" — how a component is attached to a connector.

The architect uses C&C structures to answer the **runtime questions**:
- What are the major **executing components**? How do they **interact**?
- Where are the major **shared data stores**?
- What is **replicated**?
- How does data **flow** through the system?
- What can **run in parallel**?
- Can the structure **change at runtime**?

### The 4 C&C structures

| # | Structure | Plain English |
|---|---|---|
| 1 | **Process** (or communicating processes) | Units = processes/threads connected by **communication, synchronisation, or exclusion** operations. |
| 2 | **Concurrency** | Units = components; connectors = **logical threads**. A logical thread = a sequence of computation that can be put on its own physical thread. |
| 3 | **Shared Data** (or **Repository**) | Components and connectors that **create, store, and access persistent data**. |
| 4 | **Client-Server** | Components = clients and servers; connectors = **protocols and messages** between them. |

> **Memory Hook — "PCSC"** → **P**rocess, **C**oncurrency, **S**hared data, **C**lient-server. Or remember: *"Processes Concur over Shared Client-Server data."*

> **Pro Tip — exam phrase:** A C&C structure answers *"what does the system look like while it's running?"* — a Module structure answers *"what does the codebase look like sitting on disk?"*. Use this contrast in any compare-question.

---

## 6. Allocation Structures (real-world mapping view) — 3 types

**Maps software elements to non-software environments** — CPUs, files, teams.

Architect asks:
- What **processor** does each element run on?
- In what **files** is each element stored during dev/test/build?
- Which **development team** owns which element?

### The 3 allocation structures

| # | Structure | What it maps |
|---|---|---|
| 1 | **Deployment** | Software → **hardware processing & communication elements**. Relations: *allocated-to* and *migrates-to* (if dynamic). |
| 2 | **Implementation** | Software (usually modules) → **file structure** (folders, repos, build artifacts). |
| 3 | **Work Assignment** | Software modules → **development teams** responsible for building them. |

> **Memory Hook — "DIW"** → **D**eployment, **I**mplementation, **W**ork assignment. Or: "**D**oes **I**t **W**ork in production / source / team?"

> **Pro Tip:** A **deployment diagram** (UML) is the most common type you'll be asked to draw. Show boxes for servers/containers, label them, show which components run on which.

---

## 7. The Master Summary Table (slide 10) ⭐

This is **gold** for the exam — memorise the "Useful for" column.

| Structure | Relations | Useful for |
|---|---|---|
| **Decomposition** | *is-a-submodule-of*; *shares-secret-with* | Resource allocation, project structuring, **information hiding**, **encapsulation**, config control |
| **Uses** | *requires the correct presence of* | Engineering **subsets** & **extensions** |
| **Layered** | *uses the services of*; *provides abstraction to* | Incremental development, **portability** (virtual machines) |
| **Class** | *is-an-instance-of*; *shares access methods of* | OOP — rapid implementation from a **common template** |
| **Client-Server** | *communicates with*; *depends on* | Distributed operation, separation of concerns, **performance analysis**, **load balancing** |
| **Process** | *runs concurrently with*, *excludes*, *precedes* | **Scheduling analysis**, **performance analysis** |
| **Concurrency** | *runs on the same logical thread* | Identifying **resource contention**; where threads fork/join/are created/killed |
| **Shared Data** | *produces data*; *consumes data* | **Performance**, **data integrity**, **modifiability** |
| **Deployment** | *allocated-to*; *migrates-to* | **Performance**, **availability**, **security** analysis |
| **Implementation** | *stored in* | Config control, **integration**, test activities |
| **Work Assignment** | *assigned-to* | **Project management**, expertise allocation, managing commonality |

> **Pro Tip — exam goldmine.** If a question gives a scenario like *"we need to analyse system performance"* → pick **Deployment** or **Process** structure. If *"manage who builds what"* → **Work Assignment**. If *"ensure portability"* → **Layered**. Match the need to the right structure. Easy marks.

---

## 8. Relating Structures to Each Other (slide 11)

Three big ideas:

1. Different structures give **different perspectives** on the same system.
2. Structures are **NOT independent** — an element in one structure often **maps to** an element in another. (e.g., a module from the Decomposition structure becomes a runtime component in the C&C structure.)
3. Structures are the **primary engineering leverage points** — i.e., *changing the architecture means changing one or more of these structures*.

> **Memory Hook:** **"Different views, same system. They overlap."**

---

## 9. Which Structures Should You Document?

Slide 12 — a freeing message:

> **You don't need to document all of them.**

Each structure has the **power to manipulate certain quality attributes**. The architect picks the structures that matter for the *dominant qualities* of the system.

- Need **portability**? Document **Layered**.
- Need **scalability** under load? Document **Deployment** + **Process**.
- Need to coordinate **multiple teams**? Document **Work Assignment**.

There's usually a **dominant structure** for a given system — the one most aligned with the key qualities.

> **Pro Tip — exam scenario:** If asked "which structures should the architect document for system X?", **don't list all 11**. Pick the 2–4 most relevant ones based on the system's stated quality attributes and *explicitly justify your choice*.

---

## 10. Views — Different Stakeholders, Different Views ⭐

> **A view captures a structure.** Different stakeholders need different views.

The slide gives quick examples:

**For the Architect:**
- **Deployment view** → reason about **performance** and **reliability**.
- **Layered view** → reason about **portability**.

**For the Developer:**
- **Class view** (class diagram) → reason about **inheritance** and similar behaviour.

The **stakeholder ↔ view** table on slide 14 is detailed but the **key takeaway** is:

> Different roles need different levels of detail (D = Detailed, S = Some, O = Overview, X = Any) of different views.

A quick summary of who cares most about what:

| Role | What they care most about |
|---|---|
| **Project Manager** | Decomposition + Deployment (planning & people) |
| **Developer** | Almost everything in **Detail** — Decomposition, Uses, Class, Layer, C&C |
| **Tester** | Uses + Class + C&C (to know what interacts with what) |
| **Maintainer** | Everything in detail (they have to fix it!) |
| **Customer** | C&C (Some) + Deployment (Overview) |
| **End User** | C&C + Deployment (just enough to understand) |
| **Architect** | **Everything in detail** — they own the whole picture |

> **Memory Hook:** **"The closer you are to the code, the more module views you need. The closer you are to the business, the less detail you need."**

---

## 11. The 4+1 View Model ⭐⭐ (very examable!)

A famous model by **Philippe Kruchten** for describing architecture from the viewpoints of different stakeholders. Uses **4 views + 1** (scenarios / use cases that tie them together).

```
        ┌─────────────┐         ┌──────────────┐
        │   Logical   │ ───►    │ Development  │
        │    View     │         │     View     │
        └─────────────┘         └──────────────┘
                ▲   ┌──────────────────┐   ▲
                │   │   Scenarios      │   │
                │   │   (Use Cases)    │   │
                ▼   └──────────────────┘   ▼
        ┌─────────────┐         ┌──────────────┐
        │   Process   │ ───►    │   Physical   │
        │    View     │         │     View     │
        └─────────────┘         └──────────────┘
```

| View | What it describes | Audience |
|---|---|---|
| **Logical View** | The **functionality** the system provides to end users (objects, classes, services). | End users / functional analysts |
| **Development View** (a.k.a. Implementation view) | The **modules / packages** in the codebase. | Developers |
| **Process View** | The **runtime processes**, threads, concurrency, and how they communicate. | System integrators / performance engineers |
| **Physical View** (a.k.a. Deployment view) | How software is **mapped to hardware** (servers, networks). | Sysadmins / DevOps |
| **+1: Scenarios** | A handful of **use cases** that exercise the architecture, tying the 4 views together — proves they work as a whole. | Everyone |

> **Memory Hook — "LDPP + S"**: **L**ogical, **D**evelopment, **P**rocess, **P**hysical, plus **S**cenarios.  
> Or: "**Logical for users, Development for devs, Process for runtime, Physical for hardware, Scenarios glue them.**"

### How 4+1 maps to the 3 structure categories from earlier

| 4+1 View | Maps to which structure category? |
|---|---|
| Logical View | Module (often Class structure) |
| Development View | Module (Decomposition, Implementation) |
| Process View | Component-and-Connector (Process) |
| Physical View | Allocation (Deployment) |
| Scenarios | Cross-cutting — exercises all of the above |

> **Pro Tip — likely exam question:** *"Describe the 4+1 View Model and explain what each view captures."* → Draw the diagram + a 1-line description per view. Very predictable question.

---

## 12. Enterprise Architectural Viewpoints — The Zachman Framework (briefly)

Slide 16 introduces the **Zachman Framework** — a **formal, structured way of viewing an entire enterprise** (not just one software system).

It's a **6 × 6 matrix**:
- **Rows** (perspectives): Scope (Contextual) → Enterprise Model → System Model → Technology Model → As Built → Functioning Enterprise.
- **Columns** (questions): **What** · **How** · **Where** · **Who** · **When** · **Why**.

You answer each of the 6 questions at each of the 6 perspective levels — that gives you 36 cells, each holding a different artifact/model.

> **Memory Hook — "6W × 6P"** → 6 questions (W's) × 6 perspectives.

> **Don't over-stress this slide.** The exam is unlikely to ask deep Zachman questions. You should be able to say *"Zachman Framework is an enterprise architecture ontology that uses a 6×6 matrix of rows (Scope → Functioning Enterprise) and columns (What, How, Where, Who, When, Why)"* and move on.

---

## 13. Quick Comparison — All Structures in One Place

```
MODULE STRUCTURES (code-time)
  ├── Decomposition  → tree of modules
  ├── Uses           → who depends on whom
  ├── Layered        → strict use-only-below
  └── Class          → inheritance / generalisation

COMPONENT-AND-CONNECTOR STRUCTURES (run-time)
  ├── Process        → processes & threads communicating
  ├── Concurrency    → logical threads, contention
  ├── Shared Data    → repositories producing/consuming
  └── Client-Server  → client ↔ server protocols

ALLOCATION STRUCTURES (mapping to environment)
  ├── Deployment     → software on hardware
  ├── Implementation → modules in file system
  └── Work Assignment→ modules to teams
```

That's **11 structures** across **3 categories**. Memorise this diagram.

---

## 14. One-Shot Summary (the morning of the exam)

> A **structure** is the actual set of architectural elements as they exist; a **view** is the documented representation of a structure. Software systems have **many structures** at once — like the skeletal, nervous, and circulatory systems of a human body. We group them into **3 categories**: **Module structures** (code-time: Decomposition, Uses, Layered, Class), **Component-and-Connector structures** (run-time: Process, Concurrency, Shared Data, Client-Server), and **Allocation structures** (real-world mapping: Deployment, Implementation, Work Assignment). Each structure manipulates particular **quality attributes**, so the architect should document only the **few that matter** — including any **dominant structure** for the system. Different **stakeholders need different views** at different levels of detail. A famous documentation model is the **4+1 View Model** (Logical, Development, Process, Physical + Scenarios as use cases). At the enterprise level, the **Zachman Framework** offers a 6×6 ontology (rows = perspectives, columns = What/How/Where/Who/When/Why).

---

## 15. Likely Exam Questions (and how to answer)

**Q1. Differentiate between a Structure and a View.**  
→ Structure = the real thing (elements as they exist). View = a documented representation. Use the X-ray analogy.

**Q2. List and explain the three categories of architectural structures, with examples.**  
→ **Module** (Decomposition, Uses, Layered, Class), **C&C** (Process, Concurrency, Shared Data, Client-Server), **Allocation** (Deployment, Implementation, Work Assignment). Give one example each.

**Q3. Describe the 4+1 View Model.**  
→ Diagram + 1-line description per view (Logical, Development, Process, Physical, Scenarios). Mention which stakeholder cares about each.

**Q4. Which structures should an architect document and why?**  
→ Not all — only the ones tied to **dominant quality attributes** of the system. Justify with examples ("if scalability matters, document deployment + process").

**Q5. Map stakeholders to the views they need.**  
→ Use the stakeholder table from section 10. Highlight architect (everything), developer (mostly module views), customer/user (mostly C&C + deployment overview).

**Q6. Explain the relationship between structures.**  
→ Different perspectives on the same system, NOT independent (elements in one structure relate to elements in another), and they are the **primary engineering leverage points** of an architecture.

---

## 16. Vocabulary You Should Use Confidently

- **Structure** — the actual architectural elements.
- **View** — a documented representation of a structure.
- **Module** — a unit of implementation (code).
- **Component** — a runtime unit.
- **Connector** — a runtime communication mechanism.
- **Attachment** — the relation between a component and a connector.
- **Decomposition / Uses / Layered / Class** — module structures.
- **Process / Concurrency / Shared Data / Client-Server** — C&C structures.
- **Deployment / Implementation / Work Assignment** — allocation structures.
- **4+1 View Model** — Kruchten's stakeholder-oriented view model.
- **Logical / Development / Process / Physical / Scenarios** — the 4+1 views.
- **Zachman Framework** — enterprise architecture ontology (6×6 matrix).
- **Dominant Structure** — the structure most aligned with a system's key quality attributes.

---

## 17. References

- Bass, Clements & Kazman — *Software Architecture in Practice*, Chapters 2 & 9.
- http://www.ece.ubc.ca/~matei/EECE417/BASS/ch02lev1sec5.html
- http://www.ece.ubc.ca/~matei/EECE417/BASS/ch09lev1sec3.html
- Philippe Kruchten's 4+1 View paper: https://www.cs.ubc.ca/~gregor/teaching/papers/4+1view-architecture.pdf
- https://www.zachman.com/

---

**Pro Tip — connecting Lectures 1, 2, and 3:**
- **Lec 1** told us *what* architecture is (SQDP / Squid P).
- **Lec 2** told us *how* it's produced (4 influences → 7 activities).
- **Lec 3** tells us *how to look at and document it* (3 structure categories, multiple views, 4+1 model).

Send Lecture 4 when you're ready. 🚀
