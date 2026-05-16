# Lecture 01 — Software Architecture: An Overview

**Module:** SE3030 — Software Architecture  
**Semester 1, 2026 · SLIIT**

> Hello! Think of this note as me sitting next to you with a cup of tea, explaining the lecture slowly. We will go slide-by-slide, use simple words, and I will sprinkle in **Pro Tips** and **Memory Hooks** along the way so things actually stick for the exam. You do not need any prior knowledge — we build from zero.

---

## What you should be able to do after this lecture

By the end of this note you should be able to:

1. **Define** what software architecture actually is (not the vague "blueprint" answer).
2. Explain that software architecture is **dynamic** — it changes over time.
3. Describe what a software architect is **expected** to do.
4. Tell the story of **how architectural styles evolved** over the years.

> **Pro Tip — exam framing.** Whenever the exam asks "what is software architecture?", do **not** write "a blueprint of the system". That is the *weak* answer your friends will write. Write the **Richards & Ford definition** (4 parts — coming below). Markers love it.

---

## 1. What is Software Architecture?

### The funny quote first
> *"Architecture is about the important stuff… whatever that is."* — **Ralph Johnson**

This sounds like a joke, but it's actually the most honest definition. **Architecture = the important stuff**. The things that are **hard to change later**. Buttons on a screen? Easy to change. Whether your app is one big box or 20 small services? Painful to change. **That second one is architecture.**

### Weak definitions you must avoid

People often say software architecture is:
- "A **plan** or **blueprint** of a software system."
- "A **roadmap** for developing a software system."

These are not *wrong* — they're just **ambiguous**. They don't tell you *what* should be inside the plan. So we need a sharper definition.

### ⭐ The clear definition (memorise this for the exam)

**Mark Richards & Neal Ford**, in their book *Fundamentals of Software Architecture: An Engineering Approach*, say software architecture is a combination of **four things**:

1. **Architectural Style** — the **structure** of the system (e.g., layered, microservices, microkernel).
2. **Quality Attributes** (Architecture characteristics) — the "-ilities" the system must support (scalability, availability, security…).
3. **Architecture Decisions** — the **rules** for building the system.
4. **Design Principles** — the **guidelines** for building the system.

> **Memory Hook — "S Q D P"** → **S**tyle, **Q**uality attributes, **D**ecisions, **P**rinciples.  
> Pronounce it like "**Squid P**". A squid has many arms; architecture has many parts. 🦑

Visual mental picture from the slides (Figure 1-2 in the book):

```
              ── Architecture characteristics (Quality Attributes) ──
             ╔══════════════════════════════════════════════════════╗
             ║                                                      ║
   Decisions ║                The System (slides on a rack)         ║ Design
     ↕       ║                                                      ║ principles
             ╚══════════════════════════════════════════════════════╝
                              ── Structure (Style) ──
```

Think of architecture as a **shelf**: the **shelf itself = Structure**, what sits *on top* and *underneath* = Quality attributes, and the **two side supports = Decisions** (left) and **Design Principles** (right). All four hold the architecture up. Remove one and it collapses.

---

## 2. Architectural Style (the Structure)

The **architectural style** is *how the system is organised*. Some common styles you'll learn later in the module:

- **Layered** (Presentation → Business → Persistence → Database)
- **Microservices** (many small independent services)
- **Microkernel** (a small core + plugins)
- **Event-driven**, **Pipe-and-filter**, **Space-based**, etc.

But here is the important bit the lecture stresses:

> Saying *"it's a microservices architecture"* tells you the **shape**, not the **architecture**.

It's like telling someone your house is *"two-storey"* — okay, but is it safe? Comfortable? Easy to maintain? Did you use concrete or sticks? You haven't told me anything important yet.

### 🏠 The dream house analogy (slide 9 & 12)

The lecturer's example is gold — keep this in your head for the whole module:

| House | Structure | But… |
|---|---|---|
| **Shabby wooden two-storey** | ✅ It is two-storey | ❌ Not safe, not comfortable |
| **Solid concrete two-storey** | ✅ Same structure | ✅ Safe, comfortable, beautiful |

**Same structure, completely different architecture.** Why? Because the *quality attributes* are different. That brings us to the next piece…

> **Pro Tip — exam answer pattern.** If a question asks "is X a complete description of an architecture?" and X is just a style name, the answer is **NO**, because architecture also needs quality attributes + decisions + principles. Always justify with the SQDP framework.

---

## 3. Quality Attributes (Architecture Characteristics)

Also known as the **"-ilities"**. Quality attributes answer the question:

> *"Beyond just working, is this a good system?"*

Examples from the slide (Figure 1-4):

| Group | Examples |
|---|---|
| **Operational** | Availability, Reliability, Performance, Scalability, Elasticity, Fault tolerance, Recoverability |
| **Structural** | Deployability, Testability, Agility, Learnability |
| **Cross-cutting** | Security |

### Key idea — **Orthogonal to functionality**

The word **"orthogonal"** scared me too the first time. It just means **independent / at a right angle / unrelated**.

What it means in plain English:
> You can talk about quality attributes **without even knowing what the app does**.

Example: "The system must be available 99.99% of the time." → I haven't told you if it's a banking app, a game, or a recipe app. Doesn't matter. The quality attribute stands on its own.

> **Memory Hook — "Beyond Does-It-Work"**  
> Functional requirements = *Does it work?*  
> Quality attributes = *Is it any good?*  
> Both matter. Architecture is mostly driven by the **second one**.

> **Pro Tip — spotting them in exam case studies.** Whenever the case study uses words like:
> - "must handle Black Friday traffic spikes" → **Scalability + Elasticity**
> - "must be online 24/7 even if a server dies" → **Availability + Fault tolerance**
> - "must process payments in under 200 ms" → **Performance**
> - "small dev team needs to ship features fast" → **Agility + Deployability**
> - "new junior devs join often" → **Learnability + Testability**
>
> Write the precise -ility name, then justify your architecture using it. This is how you collect easy marks.

---

## 4. Architecture Decisions

These are **rules** that the architect lays down for how the system must be built. They are **strict**. They tell developers *what they can do and what they cannot*.

### The textbook example
> "In a layered architecture, **only** the business / service layer is allowed to access the database. The presentation layer is **not allowed** to call the database directly."

This is a rule. If a developer breaks it, the architecture is broken.

### What if a rule cannot be followed?

In real life, sometimes you simply *cannot* follow a rule (e.g., performance is awful, or a legacy system forces you to). Then you raise a formal **variance** (an exception) which is approved by the **Chief Architect** or the **Architecture Review Board (ARB)**.

> **Memory Hook — "Variance = Permission slip from the principal."**  
> You wanted to break a rule? Fine, but get it signed.

### 🏠 House analogy (slide 15)
> "All **load-bearing** structures must be **reinforced concrete**. Non-load-bearing walls **may** be brick to save cost."

That is an **architecture decision**. It is non-negotiable for load-bearing walls. The decision *constrains* the builder.

---

## 5. Design Principles

If decisions are **rules**, design principles are **guidelines / strong suggestions**. They allow **flexibility**.

The textbook example:
> "**Prefer** asynchronous messaging between microservices to improve performance."

Notice the word *"prefer"*. The architect is saying: *"In most cases, do this — but if there's a good reason to do something else in a specific case, you may."*

### Decisions vs Principles — the table you should remember

| | Architecture Decision | Design Principle |
|---|---|---|
| Nature | **Rule** (must follow) | **Guideline** (should prefer) |
| Flexibility | None — needs a variance | Yes — devs can deviate when justified |
| Word to look for | *must*, *only*, *shall* | *prefer*, *should*, *aim to* |
| Example | "Only business layer accesses DB" | "Prefer async messaging" |

### 🏠 House analogy (slide 19)
> "**Prefer** smooth flooring for comfort, **but** choose flooring based on usage (safety in bathroom, aesthetics in living room, durability in verandah)."

That's a principle — it gives the builder a guideline but allows judgement.

> **Pro Tip — exam trick question.** If you're asked "is X a decision or a principle?", look at the **strength of the language**.  
> "Must / only / never / always" = **Decision**.  
> "Prefer / should / where possible / aim to" = **Principle**.

---

## 6. Putting it all together (the big idea)

The whole point of slides 4–19 is one big takeaway:

> **Software Architecture = Style + Quality Attributes + Decisions + Principles.**

Anyone who answers the exam with just *one* of those is giving an incomplete answer. Write all four. Every single time. ✍️

---

## 7. What is a Software Architect?

The lecture's point is: **the role keeps growing**.

### Then (a decade ago)
Architects mostly worried about **technical things**:
- Modularity
- Components
- Design patterns

That's it. Mostly a "super-senior developer".

### Now (today)
With cloud, microservices, distributed systems, DevOps, security threats, business agility… architects must handle:
- Technical concerns ✅ (still)
- **Strategic technical direction** of the company
- Business goals
- Cross-team coordination
- People & politics (yes, really)
- Compliance, security, cost

> **Memory Hook — "From super-coder to super-coordinator."**

The lecture honestly admits: *"It's not practical to exactly define the bounds of the role."* So instead, we focus on **expectations**.

---

## 8. Expectations of an Architect (likely exam question!) ⭐

The lecture lists **8 expectations**. The exam loves this list. Memorise it.

| # | Expectation | What it really means (plain English) |
|---|---|---|
| 1 | **Make architecture decisions** | Lay down the rules (which style, which DB, which protocol, etc.) |
| 2 | **Continually analyze the architecture** | Architecture is not "draw once and forget". Keep checking if it still fits as the system grows. |
| 3 | **Keep current with latest trends** | Read, learn, attend conferences. Tech moves fast. |
| 4 | **Ensure compliance with decisions** | Make sure developers actually follow the rules you set. |
| 5 | **Diverse exposure and experience** | Worked on many kinds of systems — that breadth helps pick the right style. |
| 6 | **Have business domain knowledge** | Understand the business (banking? retail? healthcare?). You can't design well for a domain you don't understand. |
| 7 | **Possess interpersonal skills** | Talk to devs, managers, clients. Soft skills matter. |
| 8 | **Understand and navigate politics** | Convince stakeholders, handle disagreements, get buy-in. Architecture lives or dies on people. |

> **Memory Hook — "MAKE-CKED-BIPP"**: **M**ake decisions, **A**nalyze, **K**eep current, **E**nsure compliance, **D**iverse exposure, **B**usiness knowledge, **I**nterpersonal, **P**olitics.  
> (Not a real word — just an ugly mnemonic. Ugly = memorable!)
>
> Or simpler: **3 Tech + 3 People + 2 Knowledge**
> - **3 Tech**: Make decisions / Analyze / Ensure compliance
> - **3 People**: Interpersonal / Politics / Keep current
> - **2 Knowledge**: Diverse exposure / Business domain

> **Pro Tip — likely 5-mark question.** "List and briefly explain 5 expectations of a software architect." → Pick any 5 from above, explain each in 1–2 lines. Easy marks.

---

## 9. Evolution of Architectural Styles (the story)

Slide 23 shows the timeline. Memorise this order — it tells a **story**:

```
Big Ball of Mud  →  Monolithic  →  2-Tier  →  3-Tier  →  SOA  →  Microservices
   (chaos)         (one block)    (UI+DB)   (UI+Logic+DB)  (ESB)   (many small)
```

A super-quick tour:

1. **Big Ball of Mud** — no architecture at all. Spaghetti code, legacy, bugs everywhere. The "before architecture was a thing".
2. **Monolithic** — one giant app, one deployable. Simple to build, hard to scale.
3. **2-Tier (Client-Server)** — UI on one machine, database on another. The 1990s look.
4. **3-Tier** — Presentation + Business Logic + Data. Classic enterprise web apps of the 2000s.
5. **SOA (Service-Oriented Architecture)** — bigger systems split into services connected by an **ESB (Enterprise Service Bus)**. Heavyweight, lots of governance.
6. **Microservices** — small, independently deployable services. The modern cloud-native style.

### Why this evolution happened
Each new style was a **response to the problems of the previous one**.
- Monolith → "Too big and tightly coupled" → split into tiers.
- 3-Tier → "Hard to integrate across the enterprise" → SOA.
- SOA → "ESB became a bottleneck, too heavy" → Microservices.
- Microservices → (the next thing is coming, probably serverless / event-driven).

> **Pro Tip — exam diagram.** If you're asked to "show the evolution of architectural styles", draw the **arrow chain** above. Label each box with 1-line description. Easy 5–10 marks.

> **Big Idea — context matters.** Each style was *correct for its time*. Microservices in 1995 would have been crazy (no cloud, no Docker). Monoliths in 2026 are sometimes still the right call for a small startup. **Architecture is contextual.**

---

## 10. Summary (one-shot review)

Read this last paragraph the morning of the exam:

> **Software architecture** is **not** a vague blueprint — it is the combination of **architectural style, quality attributes, architecture decisions, and design principles** (**SQDP / Squid P**). The **style** describes the **structure**, the **quality attributes** describe the *"-ilities"* the system must support (orthogonal to functionality), **decisions** are strict **rules**, and **design principles** are flexible **guidelines**. Architecture is driven by **quality attributes and constraints, not features**. A **software architect** does much more than code today: they make decisions, analyse the architecture, ensure compliance, stay current, and bring business + people skills. Architectural styles have **evolved** from chaotic "big ball of mud", through monolithic, 2-tier, 3-tier, SOA, all the way to microservices — each style solving the previous one's problems. **Architecture is contextual — what's right depends on the situation.**

---

## 11. Likely Exam Questions (and how to answer)

Based on the slides, expect things like:

**Q1. Define software architecture.**  
→ Don't say "blueprint". Say *"Software architecture is the combination of the system's architectural style (structure), quality attributes it must support, architecture decisions (rules), and design principles (guidelines) — as defined by Richards & Ford."* Then briefly explain each of the 4. 🪙

**Q2. Differentiate between architecture decisions and design principles.**  
→ Use the table in section 5. Give an example for each.

**Q3. Why is saying "it is a microservices architecture" not a complete description?**  
→ Because that only describes the **structure (style)**. Architecture also needs quality attributes, decisions, principles. Use the dream-house analogy. 🏠

**Q4. List and explain 5 expectations of a software architect.**  
→ Pick from section 8. 1–2 lines each.

**Q5. Explain the evolution of architectural styles.**  
→ Draw the chain (Big Ball of Mud → Monolithic → 2-Tier → 3-Tier → SOA → Microservices). For each, give 1-line description + the problem it tried to solve.

**Q6. What are quality attributes? Why are they called orthogonal to functionality?**  
→ Quality attributes are the "-ilities" the system must exhibit (availability, scalability…). They are *orthogonal* (independent) from functionality because you can discuss them without knowing what the system actually does.

---

## 12. Words you should be able to use confidently

These are vocabulary that earn marks when used precisely:

- **Architectural style** — the structural shape (layered, microservices…).
- **Quality attribute / Architecture characteristic / "-ility"** — non-functional requirement.
- **Architecture decision** — a *rule* enforced on the system.
- **Variance** — a formally approved exception to an architecture decision.
- **Design principle** — a *guideline* (flexible).
- **Orthogonal to functionality** — independent of what the system does.
- **Architecture Review Board (ARB)** — body that approves variances.
- **Functional requirements** vs **Non-functional requirements (NFRs)**.

---

## 13. References

- Richards, M., & Ford, N., *Fundamentals of Software Architecture: An Engineering Approach* — **Chapter 1**.
- Slide article: *Evolution of Software Architecture: From Mainframes and Monoliths to Distributed Computing*.

---

**Pro Tip — study workflow for this module 🎯**

When the next lecture comes, do this:
1. Read the slides once (fast — no notes).
2. Open the lecture note I'm preparing for you (like this one).
3. Re-read the slides — now you'll understand 90% of it instantly.
4. The night before the exam, **only** read the **Summary** section + the **table of decisions vs principles** + the **expectations list** + the **evolution chain**.

You've got this. Send Lecture 2 whenever you're ready. 💪
