# Lecture 05 — Architecture in the Real World: Some Examples

**Module:** SE3030 — Software Architecture · Semester 1, 2026 · SLIIT

> Heads up — **this is a case-study lecture**, and your exam is **mostly case-study based**. So this one is *gold dust*. We're taking everything you've learned (quality attributes, trade-offs, monolith vs distributed, architecture quantum) and applying it to **real, named companies**. Memorise these stories — you can use them as "real-world examples" in almost any case-study answer to score easy bonus marks. ☕

---

## What you should walk away knowing

1. A **3-question framework** for analysing any real-world system.
2. The **Stack Overflow** story — *why a giant monolith was the right answer* for them.
3. The **Uber** story — *monolith → microservices → DOMA* (Domain-Oriented Microservice Architecture), and why each shift happened.
4. Two famous **architecture failures** — Boeing 737 Max and Therac 25 — and the architectural lesson behind each.
5. The big takeaway: **Architecture = Prioritised Quality Attributes → Trade-offs → Structure.**

> **Pro Tip — exam money:** Whenever a case-study question feels open-ended, drop in a real-world parallel. *"This scenario resembles Stack Overflow's situation, where performance dominated and a monolith was correct."* Markers love this.

---

## 1. Why this lecture exists

So far you've learned the **theory**:
- **Lec 1** — what architecture is (SQDP).
- **Lec 2** — how it's produced (4 influences, 7 activities).
- **Lec 3** — how to view/document it (structures, views, 4+1).
- **Lec 4** — quality attributes, trade-offs, monolith vs distributed, architecture quantum.

Now we **apply it to real companies** and see *how their architectural reasoning actually played out* — and what consequences (good and bad) followed.

---

## 2. The Architectural Reasoning Framework ⭐

> *"Architecture is shaped by quality attribute priorities."*  
> Different priorities → Different trade-offs → Different architectures.

For **any real-world system**, ask **3 questions**:

1. **What quality attributes are prioritised?**
2. **What trade-offs are visible?** (i.e., what was sacrificed?)
3. **What architectural structure reflects this?**

> **Memory Hook — "PTS"** → **P**riorities → **T**rade-offs → **S**tructure.

This 3-question recipe is your **secret weapon** for any case-study question. Use it as the spine of your answer every single time.

---

## 3. Case Study #1 — Stack Overflow 🟠 (the "happy monolith")

### The setup
**Stack Overflow** is the giant Q&A platform for developers. The lecture's stats from Feb 9, 2016 give you a sense of scale:

| Metric | Number |
|---|---|
| HTTP requests / day | **209 million** |
| HTTP traffic / day | **1.24 TB** |
| SQL queries / day | **504 million** |
| Avg page render time (question pages) | **22.71 ms** |
| Avg page render time (home page) | **11.80 ms** |

That is **enormous traffic** with **eye-wateringly low latency**. Now let's reason architecturally.

### Step 1 — What quality attributes are prioritised?

| Attribute | Why it matters here |
|---|---|
| **Performance Efficiency** ⭐ (the dominant driver) | Low latency, fast response — UX depends on it. |
| **Availability** | The site must always be up — global audience. |
| **Scalability** | Handle massive traffic. |
| **Reliability** | Data consistency between answers, votes, edits. |
| **Maintainability** | Operational complexity must stay low — only **50 engineers**. |

> 🪙 **The dominant driver is PERFORMANCE.** Everything else gets balanced *around* performance.

### Step 2 — What trade-offs are visible?

| Trade-off | The deal Stack Overflow made |
|---|---|
| **Performance Efficiency vs Reliability (consistency)** | Heavy **caching** reduces latency and DB load — but cache invalidation must be done carefully to keep data consistent. |
| **Performance Efficiency vs Maintainability** | **WebSockets** improve real-time responsiveness — but increase operational complexity. |
| **Performance & Scalability vs Maintainability** | **Elasticsearch** powers fast search at scale — but adds upgrade and re-index complexity. |

### Step 3 — What architectural structure reflects this?

> A **decades-old giant monolithic application**, on-premise, on IIS, running **200 sites**.

The hardware footprint (2016):

| Component | Count |
|---|---|
| Microsoft SQL Servers | 4 |
| IIS Web Servers | 11 |
| Redis Servers (cache) | 2 |
| Tag Engine Servers | 3 |
| Elasticsearch Servers | 3 |
| HAProxy Load Balancers | 4 (CloudFlare-supported) |
| Networks / Firewalls / Cisco Routers | 2 / 2 / 4 |

All this serviced by **only 50 engineers**, deploying to production **in 4 minutes, multiple times a day**. 🤯

### Why a monolith works here ⭐

Even in 2016 (microservices hype era), Stack Overflow stayed monolithic. Why?

1. **Strong centralised data model** — questions, answers, users, votes all relate tightly. One DB schema works fine.
2. **Performance prioritised** — every part of the stack is heavily optimised. In-process function calls beat network calls every time.
3. **Heavy caching reduces DB pressure** — 30% of DB access lives in 1.5 TB of RAM, plus Redis on top.
4. **Simplicity over service fragmentation** — efficient, simple to manage, cost-effective for *their specific use case*.
5. **Often, simplicity beats complexity** — monoliths are simpler to develop, test, and deploy.

> **Memory Hook — "SO = Simplicity Optimised."** Stack Overflow proves the monolith is alive and well when **performance is king** and **data is centralised**.

> **Pro Tip — exam quote:** *"Stack Overflow's architecture demonstrates that a monolith remains a perfectly valid choice when one consistent set of quality attributes — dominated by performance — applies across the system. Operating ~200 sites on 11 web servers with 50 engineers shows that architectural simplicity can scale enormously."*

### Linking back to Lecture 4
Stack Overflow has **one architecture quantum** — the entire system shares the same quality attributes (performance, availability, scalability uniformly). Therefore → **monolith** is correct. ✅

---

## 4. Case Study #2 — Uber 🚗 (the "monolith outgrown")

This is the **classic story** of how architecture must **evolve** as a company grows.

### The journey in 3 phases

```
   Pre-2014               ~2014–2018              ~2018+
   ┌──────────┐          ┌───────────────┐       ┌────────────────┐
   │ MONOLITH │ ───►     │ MICROSERVICES │ ───►  │  DOMA          │
   │ (small   │          │ (huge tangle) │       │  (Domain-      │
   │  team)   │          │               │       │   Oriented MS) │
   └──────────┘          └───────────────┘       └────────────────┘
       ▲                       ▲                         ▲
   Rapid iteration         Independent            Reduce coupling,
   for small team          deployment per         organise services
                           team, scale per        into domains with
                           service                gateways
```

### Phase 1 — Monolith (pre-2014)
Quality attributes prioritised: **rapid iteration**, **fast feature development for a small team**.

Result: a single monolithic codebase, one deployable. Worked fine — for a small team.

### Phase 2 — The pain begins (Uber explodes globally)

As Uber expanded globally, the monolith began to crack:

| Problem | What it looked like |
|---|---|
| **Deployment Bottlenecks** | Deploying *one* feature risked breaking *unrelated* parts of the app. |
| **Team Conflicts** | Multiple teams on the same codebase → endless merge conflicts. |
| **Scalability Limits** | Whole system had to scale together, even if only one component needed more capacity. |
| **Maintenance Overhead** | A single bug or outage could take the **entire platform** down. |

→ A **paradigm shift** was needed.

### Phase 3 — Microservices (the new quality attribute priorities)

A **new prioritisation** of quality attributes:

- **Maintainability**
- **Deployability**
- **Scalability**
- **Performance Efficiency**
- **Reliability**
- **Operational Efficiency**

### The trade-offs Uber accepted

| Trade-off | The deal |
|---|---|
| **Maintainability & Deployability vs Performance Efficiency** | Independent services improve maintainability and deployment autonomy — but introduce **network latency** and overhead. |
| **Scalability & Organisational Modularity vs System Complexity** | Service decomposition lets you scale horizontally — but **operational complexity explodes**. |
| **Flexibility vs Long-term Maintainability** | Custom infrastructure gives more control — but burdens future maintenance. |

> **Key takeaway from the slide:** *"Microservices were adopted primarily to improve maintainability, scalability, and organisational autonomy — accepting performance and complexity costs."*

### The hidden monster (slide 23) 🕸️

By **mid-2018**, Uber's microservice architecture (visualised in the famous Jaeger diagram) was a **giant tangled web** — hundreds of services with thousands of interconnections.

**Symptoms of microservice overload at Uber:**
- Engineers had to wade through **~50 services across 12 different teams** to debug one root cause. 🤯
- Service dependencies went **many layers deep** — hard to reason about.
- Even a **simple feature** required collaboration across multiple teams.
- Slower developer experience, instability for service owners, painful migrations.

> *"Can't live with them, can't live without them."* — direct quote from the slide.

This is the **classic microservices trap**: solve one problem (deployability + scalability), create another (system complexity + ownership confusion).

### Phase 4 — DOMA (Domain-Oriented Microservice Architecture) ⭐

Uber's solution: **DOMA**. Instead of dropping microservices, *organise them better*.

**Core principles of DOMA:**

| Principle | What it means |
|---|---|
| **Domains, not individual services** | Architecture organised around **domains** = collections of related microservices (not one service at a time). |
| **Layers** | Multiple domains grouped into **layers**. The layer design defines which dependencies are allowed. |
| **Gateway per domain** | Each domain exposes a **single clean entry point** — a **gateway**. Internal services hidden behind it. |
| **Domain-agnostic** | Domains shouldn't have hard-coded knowledge of other domains. Cross-domain customisation goes through a defined **extension architecture**. |

> **Does this sound familiar?** ← The slide asks this. The answer: **YES** — DOMA brings back many lessons from **Layered architecture**, **Domain partitioning** (Lec 4), **Bounded Contexts** (DDD), and the **Microkernel** idea (gateways + extension points). It's microservices done with the discipline of older patterns.

### Architecturally, what is the gateway doing?
The DOMA **gateway** abstracts away the internal details of a domain (its multiple services, DB tables, ETL pipelines) and only exposes:
- **RPC APIs** (for synchronous calls)
- **Messaging events** (for async communication)
- **Queries** (for data access)

Other domains can only interact with these public interfaces — not with internal services. **High cohesion within domain. Low coupling across domains.** Sound familiar from Lecture 4? ✅

### The Uber lesson in one line

> *"The architecture must evolve as the company evolves — and even microservices need their own internal organisation (domains + gateways) once they reach scale."*

> **Pro Tip — Uber is your go-to example** for any exam question about **architectural evolution**, **scaling problems with microservices**, or **DOMA / Domain-Driven Design**.

---

## 5. Stack Overflow vs Uber — A Side-by-Side ⭐

Memorise this comparison. It's the kind of thing that earns you a top-band answer.

| Aspect | **Stack Overflow** | **Uber** |
|---|---|---|
| **Dominant quality attribute** | Performance | Maintainability + Deployability + Scalability |
| **Architecture style** | Monolithic (single deployment) | Microservices → DOMA |
| **Number of architecture quanta** | Effectively **one** | **Many** |
| **Team size** | ~50 engineers | Thousands of engineers |
| **Scale of evolution** | Stayed monolithic | Monolith → Microservices → DOMA |
| **Trade-off accepted** | Operational complexity in caching/search/Elasticsearch | Network latency, system complexity, debugging overhead |
| **Big lesson** | Simplicity wins when one quality dominates | Architecture must **evolve**; even microservices need structure |

> **Memory Hook — "SO is one. Uber is many."**  
> Stack Overflow → one quantum → monolith.  
> Uber → many quanta → distributed (microservices, then DOMA).

---

## 6. Notable Failures — When Architecture Goes Wrong 💥

Two cautionary tales the lecture wants you to know.

### 6a. Boeing 737 MAX — *Backwards Compatibility Over Everything Else*

**What happened:** Two crashes (Lion Air Flight 610 in 2018, Ethiopian Airlines ET302 in 2019) killed **346 people total**.

**Architectural reason (in plain English):**
- Boeing wanted the new **737 MAX** to be **certified as the same aircraft type** as previous 737s — pilots could fly it without expensive new training. This was a **commercial / business goal** (faster sales).
- But the MAX had **bigger engines** mounted further forward, which changed flight characteristics — especially nose-up tendency at low speed.
- To compensate, Boeing added **MCAS** (Manoeuvring Characteristics Augmentation System) — software that automatically pushes the nose down if a single sensor reads too high an angle of attack.
- They downplayed MCAS in pilot documentation (to preserve the "same aircraft" story), and the system relied on a **single sensor** with no redundancy.
- When that sensor failed, MCAS pushed the nose down repeatedly. Pilots, untrained on MCAS, couldn't recover.

**Architectural lesson — quality attributes prioritised wrongly:**

| Prioritised | Sacrificed |
|---|---|
| **Backwards compatibility** (commercial) | **Safety** (operational) |
| **Time-to-market** | **Reliability** (single sensor, no redundancy) |
| **Cost reduction** (no extra pilot training) | **Transparency** to operators |

> **The headline lesson:** When the **business goal becomes the dominant architectural driver and overrides safety**, people die. Architecture is *never* purely technical — it has consequences in the real world.

### 6b. Therac 25 — *Reusability at the Cost of Safety*

**What happened:** A computerised radiation therapy machine in the 1980s. Software bugs caused several patients to receive **massive radiation overdoses** (up to 100x the intended amount). At least **3 patients died**, several were severely injured.

**Architectural reason (in plain English):**
- Therac 25 was a successor to Therac-20. Engineers **reused software modules** from the older machine.
- The older Therac-20 had **hardware safety interlocks** that masked subtle race conditions in the software.
- Therac 25 **removed the hardware interlocks** to reduce cost — but **kept the buggy software**, trusting it to handle safety.
- Race conditions in the software caused the high-energy electron beam to fire without the proper protective tungsten target.

**Architectural lesson — quality attributes prioritised wrongly:**

| Prioritised | Sacrificed |
|---|---|
| **Reusability** (reuse old code to save cost/time) | **Safety** + **Reliability** |
| **Cost reduction** (remove hardware interlocks) | **Defence in depth** (multiple safety layers) |

> **The headline lesson:** **Reusing software does not magically inherit safety from the original context.** Removing layers of protection (hardware interlocks) in favour of "trusted" software is dangerous. Architecture must consider the **full operating environment**, not just the code.

> **Pro Tip — exam treasure:** If a case-study question hints at **safety-critical systems** or **medical / aviation / nuclear** software, mention **Therac 25** or **737 MAX** as examples of *what happens when business goals override safety as the dominant quality attribute*. Instant credibility.

---

## 7. The Big Takeaway — Three Sentences

> 1. **Architecture is shaped by prioritised quality attributes.**  
> 2. **Different priorities → different trade-offs → different architectures.**  
> 3. **Poor prioritisation can cost lives — or, less dramatically, kill products.**

---

## 8. One-Shot Summary (the morning of the exam)

> Architecture is not chosen in a vacuum — it reflects the **prioritised quality attributes** of the system. The **3-question framework** to analyse any real system: *What's prioritised? What's traded off? What structure results?* **Stack Overflow** prioritised **performance** above all else; with one consistent set of quality attributes (one architecture quantum), it remained a **giant monolith** — efficient, simple, supporting ~200 sites with only 50 engineers. **Uber** started monolithic for **rapid iteration**, but as the company grew it shifted to **microservices** to gain **maintainability, deployability, and scalability** at the cost of network overhead and complexity. When microservices became too tangled (50+ services across 12 teams to debug one issue), Uber introduced **DOMA (Domain-Oriented Microservice Architecture)** — grouping services into **domains** organised in **layers** and exposing **gateways**, restoring high cohesion within domains and low coupling across them. **Notable failures** show what happens when the wrong qualities dominate: the **Boeing 737 MAX** prioritised backwards compatibility and time-to-market over safety; **Therac 25** prioritised software reuse and cost reduction over reliability and defence-in-depth — both led to deaths. The big lesson: **Architecture is the visible consequence of which quality attributes you chose to win and which you chose to sacrifice.**

---

## 9. Likely Exam Questions (and how to answer)

**Q1. Using a real-world example, explain how prioritised quality attributes shape architectural decisions.**  
→ Pick **Stack Overflow** (performance → monolith) or **Uber** (maintainability/scalability → microservices → DOMA). Use the **PTS** framework: Priorities → Trade-offs → Structure.

**Q2. Why did Stack Overflow keep a monolithic architecture despite its scale?**  
→ Performance was dominant; one consistent set of quality attributes (one quantum); centralised data model; heavy caching solved DB pressure; smaller team meant operational simplicity won. Use the stats (200 sites, 50 engineers).

**Q3. Describe how Uber's architecture evolved and explain the reasons for each shift.**  
→ Phases: Monolith (small team → rapid iteration) → Microservices (deployment bottlenecks, team conflicts, scalability limits) → DOMA (microservices became too tangled — 50 services / 12 teams to debug). Explain DOMA's 4 principles (domains / layers / gateways / domain-agnostic).

**Q4. What is DOMA? Why did Uber adopt it?**  
→ Domain-Oriented Microservice Architecture. Adopted to manage the complexity of pure microservices. Core principles: organise around **domains** (not single services), group into **layers**, expose **gateways** as single entry points, keep domains **agnostic** to each other.

**Q5. With reference to the Boeing 737 MAX or Therac 25 incident, explain how poor architectural prioritisation can lead to system failures.**  
→ Use the "Prioritised vs Sacrificed" tables. Drive home that architecture is *never* purely technical — wrong priorities = real-world harm.

**Q6. Compare Stack Overflow's and Uber's architectural reasoning.**  
→ Use the side-by-side table in section 5.

---

## 10. Vocabulary You Should Use Confidently

- **Architectural reasoning** — the structured analysis: priorities → trade-offs → structure.
- **Dominant driver** — the single quality attribute most shaping the architecture.
- **Centralised data model** — one shared data schema across the system.
- **Caching** — storing frequently accessed data in faster storage to reduce latency.
- **Cache invalidation** — keeping cached data fresh; famously *"one of the two hard problems in CS"*.
- **Domain** (Uber sense) — a collection of related microservices serving one business area.
- **Gateway** — single entry point exposing a domain's interface to other domains.
- **DOMA** — Domain-Oriented Microservice Architecture.
- **MCAS** — Manoeuvring Characteristics Augmentation System (Boeing 737 MAX).
- **Defence in depth** — multiple independent safety/security layers.
- **Backwards compatibility** — keeping new versions usable like older ones (a quality attribute, not always good!).
- **Reusability** — using existing components in a new system (a quality attribute, dangerous if context differs).

---

## 11. References & Further Reading

- *Stack Overflow: The Architecture* — 2016 Edition (Nick Craver's blog)
- *Introducing Domain-Oriented Microservice Architecture* — Uber Engineering Blog
- *Uber and Microservices Architecture: Lessons in Scalability*
- *How the Boeing 737 MAX Disaster Looks to a Software Developer* (Gregory Travis, IEEE)
- The Therac 25 case study (Nancy Leveson's classic paper)

---

**Pro Tip — connection back to Lecture 4.**
- Stack Overflow = **one quantum** → monolith.
- Uber pre-2014 = one quantum → monolith.
- Uber post-2014 = **many quanta** (each service has its own quality needs) → microservices.
- Uber DOMA = many quanta, **organised by domain** (recall *domain partitioning* from Lec 4) with gateways enforcing low coupling.

This lecture is the **practical application** of every theoretical concept from Lec 4. If you can quote Stack Overflow or Uber in your case-study answer, you've shown the marker that you can connect theory to practice — instant top-band material.

Send Lecture 6 when you're ready. 🚀
