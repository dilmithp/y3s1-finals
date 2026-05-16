# SE3030 — 11 MUST-MASTER Topics for the Exam

> **Reading guide:** This is a deep-dive masterclass on the 11 topics most likely to appear in your 2026 exam, based on the 2025 paper. Each topic includes all theory points, real-world examples, and practical scenarios. Study these and you can answer ~95% of any case-study question. ☕

---

## Table of Contents

1. [Architectural Styles (the Big 5)](#1)
2. [Quality Attributes](#2)
3. [Architecture Business Cycle (ABC)](#3)
4. [The 7 Architectural Activities](#4)
5. [Quality Attribute Scenarios (QAS)](#5)
6. [Tactics](#6)
7. [4+1 View Model](#7)
8. [SAAM — Software Architecture Analysis Method](#8)
9. [N-Tier vs Layered](#9)
10. [Cloud Architecture (IaaS / PaaS / SaaS)](#10)
11. [Drawing & Critiquing Block Diagrams](#11)

---

<a name="1"></a>
# 1. Architectural Styles — The Big 5 (Q1 directly tests these!)

## What is an Architectural Style?

> An **architectural style** is a set of principles that shapes a system, providing solutions to recurring problems and a common vocabulary for stakeholders. *Same recipe, different ingredients.*

The 2025 Q1 specifically listed **5 styles** you must master:

| # | Style | Type |
|---|---|---|
| 1 | **Monolithic** | Single deployment unit |
| 2 | **Modular Monolithic** | Single deployment, internally modular |
| 3 | **Event-Driven** | Distributed, async via events |
| 4 | **Microkernel** | Core + plugins |
| 5 | **Microservices** | Distributed, many independently deployable services |

Let's go deep into each.

---

## 1.1 Monolithic Architecture

### Theory
> A **monolithic** application is built and deployed as a **single executable / package**. One codebase, one database typically, one deployment unit. All components run in the same process and communicate via in-process function calls.

### Key Structural Features
- **Single deployment unit** — one process running everything (UI, business logic, persistence).
- **Single database** — usually one shared DB serving the whole app.
- **In-process communication** — no network calls between modules (fast!).
- **Single technology stack** — usually one programming language and framework.

### Advantages (the case FOR monolith)
1. **Simple to develop, test, debug, deploy** initially — only one process to worry about.
2. **Low operational overhead** — one app to monitor, one log file, one set of metrics.
3. **No network latency** between internal components — function calls are nanoseconds.
4. **Easy transactions** — single DB means ACID is trivial.
5. **Faster initial development** — less boilerplate, no service discovery, no contracts.

### Disadvantages (the case AGAINST monolith)
1. **Tight coupling** — change in one part forces a full rebuild + redeploy of the entire app.
2. **Scaling means scaling the entire app** — even if only the checkout module is hot, you must scale everything.
3. **Codebase grows large and unwieldy** — "Big Ball of Mud" risk.
4. **Single tech stack** — you can't use Python ML libs for one feature while writing the rest in Java.
5. **A bug in any module can crash the whole process** — no fault isolation.
6. **Long build/deploy cycles** as the project grows (minutes → hours).

### When to Choose Monolithic
- Small team (≤10 engineers).
- MVP / startup with uncertain requirements.
- Limited DevOps maturity (no containers, no orchestration).
- Predictable, modest load.
- Tight ACID transaction requirements across the domain.

### When to Avoid
- Multiple teams need to deploy independently.
- Different features need very different scaling profiles.
- Need polyglot tech stacks (Python ML + Java services + Go networking).

### Real-World Examples ⭐
- **Stack Overflow** (the famous monolith!) — runs ~200 sites on 11 IIS servers with **50 engineers**, deploying to production in 4 minutes, several times daily. (Lecture 5 case study.)
- **Basecamp** (37signals) — proudly stays monolithic; their CEO David Heinemeier Hansson is a vocal "majestic monolith" advocate.
- **GitHub** until recently — was a single Rails monolith for over a decade.
- **Early-stage Shopify** — monolithic Rails app until 2020+.

### Real-World Scenario
> *A 3-person startup wants to build an online tutoring platform. They have 6 months and $50k. Quality attributes: time-to-market, low cost. Microservices would consume their entire runway on DevOps overhead alone. **The right answer is a Monolith.** They can split it later when team grows past 10 people.*

---

## 1.2 Modular Monolithic Architecture

### Theory
> A **modular monolith** is a single deployable unit (like a classic monolith) **but** with the codebase split into **well-bounded modules** that communicate through explicit interfaces, not by reaching into each other's internals. Often a **stepping stone** toward microservices.

### Key Structural Features
- **Still one deployment** — single binary/package, one process.
- **Internal modules** with clear boundaries (e.g., `auth`, `billing`, `core`, `notifications`).
- **Modules communicate via internal APIs** — not direct database access into each other's tables.
- **Each module typically owns its data** (separate schemas in the same DB, sometimes).
- **Discipline-enforced** — there's no compiler stopping you from breaking module boundaries; you need a culture/team that enforces it.

### Advantages
1. **Operational simplicity of a monolith** — one deploy, one DB to monitor.
2. **Better maintainability** — modules have clear boundaries → lower coupling than a classic monolith.
3. **Easy to extract modules into microservices later** — boundaries are already clean.
4. **In-process calls remain cheap and consistent** — no network overhead.
5. **Easier debugging** — a single process to attach a debugger to.

### Disadvantages
1. **Discipline required** — without enforcement, boundaries decay; modules start reaching into each other's data.
2. **Still one deployment unit** — can't scale modules independently.
3. **Usually single tech stack**.
4. **Single point of failure** — one OOM crash takes down the entire app.

### When to Choose Modular Monolith
- You want monolith simplicity **but** anticipate growth.
- Want to defer microservices complexity.
- Team is still small (5–20) but expected to grow significantly.
- You want a clean migration path to microservices if needed.

### Real-World Examples ⭐
- **Shopify's "majestic monolith"** — Shopify openly published their architecture in 2020. They embraced modular monolith with strict boundaries (using Ruby's namespaces + their internal "Components" pattern). They host 1M+ merchants on it.
- **Many fintech / SaaS backends** that explicitly avoided microservices — e.g., Stripe (early), Plaid (early).
- **The Django/Rails culture** — encourages modular design within a single app.

### Real-World Scenario
> *A growing SaaS company has 25 engineers, deployed weekly, on a Rails monolith. They notice teams stepping on each other's toes when changing the codebase. They're not big enough for microservices (operational complexity), but they need cleaner boundaries. **Solution: refactor into a Modular Monolith** with 5 bounded contexts (auth, billing, core product, notifications, admin). When they reach 50+ engineers or need independent scaling, they can extract one module at a time into a service.*

> **Pro Tip — Q1 2025 evolution path:** When the question asks about long-term evolution, the **gold answer** is: *"Start with a Modular Monolith for fast initial delivery (within 1 year). Evolve to Microservices as the team scales beyond ~30 engineers and as different parts develop different quality attribute needs."* This is the **Stack Overflow → Uber arc** in miniature.

---

## 1.3 Event-Driven Architecture (EDA)

### Theory
> In **Event-Driven Architecture**, components communicate by **producing and consuming events** through a broker (event bus, message queue) — rather than calling each other directly. Producers don't know who consumes; consumers don't know who produced. **Loose coupling at runtime.**

### Two Common Topologies

| Topology | Description | When to use |
|---|---|---|
| **Broker (Publish/Subscribe)** | Events flow through a broker like Kafka, RabbitMQ, AWS SNS/SQS. Best for high-throughput async reactions. | Most common — order processing, IoT, log aggregation. |
| **Mediator** | A central orchestrator coordinates multi-step workflows (think workflow engines like AWS Step Functions, Camunda). | Complex business workflows requiring sequencing/compensation. |

### Key Components
- **Producers (Publishers)** — components that emit events ("OrderPlaced", "PaymentReceived").
- **Event Broker** — middleware that routes events (Kafka, RabbitMQ, etc.).
- **Consumers (Subscribers)** — components that react to events.
- **Events** — immutable records of something that happened in the past.
- **Topics / Channels** — categorisation of events (e.g., "orders" topic).

### Advantages
1. **Highly decoupled** — add consumers without changing producers.
2. **Scalable + responsive** — async processing absorbs traffic bursts.
3. **Real-time reactivity** — natural fit for streaming, monitoring, IoT.
4. **Resilience** — broker buffers when consumers are down (consumers catch up later).
5. **Extensibility** — new behaviours by subscribing to existing events without touching producers.

### Disadvantages
1. **Eventual consistency** — no single transaction across producers/consumers.
2. **Hard to trace end-to-end flows** — needs correlation IDs + distributed tracing.
3. **Event schema evolution is tricky** — version your events!
4. **Debugging asynchronous, out-of-order behaviour is hard**.
5. **Duplicate / out-of-order events** require idempotent consumers.

### When to Choose Event-Driven
- Real-time systems (live dashboards, fraud detection).
- Streaming data (IoT telemetry, log analytics).
- Financial transactions where many downstream systems must react.
- E-commerce: "OrderPlaced" → inventory, payment, fulfilment, recommendations, notifications all react.
- Workflows with many independent reactions.

### When to Avoid
- Strict ACID consistency required across the whole domain.
- Simple request-response interactions (use REST instead).
- Small system without multiple subscribers per event.

### Real-World Examples ⭐
- **Uber's pricing and dispatch system** — uses Kafka for real-time event streaming.
- **LinkedIn** — built Kafka originally to handle their event stream (now an industry standard).
- **Netflix** — uses event-driven architectures for personalization and metrics pipelines.
- **Banking transaction processing** — each transaction triggers fraud check, ledger update, notification, audit log.
- **IoT telemetry pipelines** — sensors emit events to Kafka; multiple consumers process for monitoring, ML, storage.

### Real-World Scenario
> *An e-commerce site previously had a monolith where placing an order took 5 seconds (synchronous: reserve inventory → charge card → send email → update analytics → recommend products). They switched to EDA: the API just publishes an "OrderPlaced" event in 50ms. Six independent consumers subscribe — payment service, inventory service, notifications, analytics, recommendations, fraud detection — and they each react asynchronously. Order acknowledgment time dropped from 5s to 100ms. The user gets fast feedback; the back-office work happens behind the scenes. **Trade-off: eventual consistency — the user might briefly see "order processing" before "confirmed", but the system became 10× more responsive and resilient.***

---

## 1.4 Microkernel Architecture (Plugin Architecture)

### Theory
> A **microkernel architecture** has a minimal **core system** ("microkernel") that provides only the essential generic behaviour. All variable / customer-specific / feature-specific functionality lives in **plug-in modules** that register against well-defined extension points.

### Key Structural Features
- **Core Kernel** — small, stable, generic. Provides extension points, plugin registry, dispatch.
- **Plug-ins** — independent modules implementing specific functionality. Loaded at startup or dynamically at runtime.
- **Extension Points** — defined interfaces the core exposes for plug-ins to hook into.
- **Plugin Registry** — runtime catalog of installed plug-ins.

### Diagram
```
              Plugin A ──┐
                         │
              Plugin B ──┼──► Core (Microkernel)  ◄── Plugin D
                         │      • Plugin registry
              Plugin C ──┘      • Dispatch logic    ◄── Plugin E
                                • Shared services
```

### Advantages
1. **Excellent extensibility** — add features without modifying the core.
2. **Strong isolation** — a bad plugin can be disabled without affecting others.
3. **Per-customer customisation** — different customers get different plugin sets (very common in product platforms).
4. **Plugins can be developed and deployed independently of the core**.
5. **Stability** — the core stays small and predictable.

### Disadvantages
1. **Core API design is hard** — getting extension points wrong cascades into massive rework.
2. **Versioning of plugin contracts is painful** — backward compatibility matters forever.
3. **Discoverability suffers** — behaviour is spread across many plugins; understanding what the system does requires examining all of them.
4. **Not a great fit when there's nothing genuinely variable** — overkill for systems without customer-specific needs.
5. **Performance overhead** of indirect calls through extension points.

### When to Choose Microkernel
- Product needs **per-customer customisation** or **per-industry variants**.
- Rules engines (insurance, tax, compliance).
- IDEs, editors, browsers.
- Systems with optional features (e.g., insurance claim systems with country-specific regulations).
- ERP / claims-processing platforms where each client has different workflows.

### Real-World Examples ⭐
- **Eclipse IDE** — the canonical example. Eclipse's core is tiny; everything (Java support, Git integration, debugger, even the UI) is a plugin.
- **VS Code** — same model. The base editor is small; extensions provide language support, theming, debugging, etc.
- **Jenkins (CI/CD)** — core Jenkins + thousands of plugins for build steps, integrations, deployment targets.
- **Web browsers (Chrome, Firefox)** — extensions/add-ons follow the microkernel pattern.
- **MS Office add-ins, Photoshop plugins, WordPress plugins**.
- **ERP systems (SAP, Salesforce platform)** — core + customer customisation modules.
- **Insurance claim systems** — core claim lifecycle + per-insurer rule plugins.

### Real-World Scenario
> *An insurance company sells claim-processing software to 50 different insurers worldwide. Each insurer has unique rules (currency, regulations, claim types, fraud detection logic). A monolith would be a nightmare — every insurer change requires touching the same codebase. A microservices architecture is overkill given modest load. **Microkernel is perfect:** the core handles the generic claim lifecycle (intake → assess → decide → pay → close), and each insurer has their own plugin with their specific rules, forms, regulations, and third-party integrations. Adding a new insurer = writing a new plugin, no core changes.*

---

## 1.5 Microservices Architecture

### Theory
> **Microservices** decompose the system into a set of **small, independently deployable services**, each owning a **bounded context** and its **own data store**. Services communicate over the network — synchronously (HTTP/REST, gRPC) or asynchronously (messaging).

### Key Structural Features
- **Small focused services** — each does one thing well.
- **Independently deployable** — deploy one service without coordinating with others.
- **Decentralised data management** — each service owns its data (no shared database!).
- **Lightweight communication** — REST/gRPC for sync, message brokers for async.
- **Smart endpoints, dumb pipes** — services contain business logic, not the message bus.
- **API gateway** — single entry point that routes to services + handles auth/throttling.
- **Service discovery** — services find each other dynamically (Consul, Eureka, Kubernetes DNS).

### Diagram
```
   Client → [API Gateway] → Auth + Routing
                  │
       ┌──────────┼──────────┬─────────┐
       ▼          ▼          ▼         ▼
   [Catalog]  [Cart]     [Payment]  [Notification]
       │         │          │            │
       DB        DB         DB           DB
       └──────── Event Bus (Kafka) ──────┘
                  ▼               ▼
             [Analytics]   [Recommendations]
```

### Advantages
1. **Independent deployability** — small teams ship without coordinating.
2. **Independent scalability** — scale only hot services (e.g., 10× catalog servers during flash sales, leave payment as-is).
3. **Technology heterogeneity** — pick the right tool per service (Python for ML, Go for high-perf networking, Java for transaction-heavy).
4. **Fault isolation** — failure in one service need not bring down the whole system.
5. **Aligns with organisational structure** (Conway's Law) — team per service.
6. **Supports continuous delivery at scale** — deploy hundreds of times per day.

### Disadvantages
1. **Operational complexity** — many moving parts. Requires mature DevOps (CI/CD, container orchestration, observability, distributed tracing).
2. **Distributed-system pitfalls** — network latency, partial failure, eventual consistency.
3. **Data consistency is hard** — no global ACID; need sagas, outbox patterns, idempotency.
4. **Testing is harder** — contract tests, integration tests, full-environment tests.
5. **Initial cost is high** — not suited to early-stage products.
6. **Versioning of APIs and shared events** is non-trivial.
7. **Debugging across services** requires distributed tracing tools (Jaeger, Zipkin).

### When to Choose Microservices
- Large system with multiple teams (10+).
- Differing scaling needs across features (catalog read-heavy, payments write-heavy).
- Need rapid, independent deployments.
- Cloud-native environment with strong DevOps capability.
- Bounded contexts are clear (you understand your domain well).

### When to Avoid
- Small team — operational complexity will crush you.
- Unclear domain boundaries — you'll repeatedly redraw service lines (expensive!).
- Weak DevOps capability — no Kubernetes, no observability, no CI/CD.
- Tight ACID consistency required across the whole domain.

### Real-World Examples ⭐
- **Netflix** — the poster child. ~700 microservices serving 200M+ subscribers.
- **Amazon (retail)** — pioneered microservices in the early 2000s. Famous "two-pizza team" rule (a team is small enough to be fed by two pizzas).
- **Uber** — has ~2,000+ microservices; led to the famous tangle problem (Lec 5).
- **Spotify** — squads/tribes own services.
- **Twitter, LinkedIn, Airbnb** — all microservices at scale.

### Real-World Scenario
> *Netflix processes 1 billion+ hours of video streaming per week. Their catalog service needs to handle 10M+ reads/sec but rarely changes. Their recommendations service needs heavy ML compute, runs hourly. Their video encoding service needs GPUs and runs in batch. Their billing service needs ACID transactions. **No single architecture serves all these needs.** Microservices let each service have its own quality attribute profile, scaling strategy, tech stack, and team. The cost: ~1000 engineers managing the infrastructure complexity.*

> **Pro Tip — Q1 2025 caveat:** *Don't recommend Microservices for every case study.* Markers know "just use microservices" is the lazy answer. Use it only when the case explicitly has multiple teams + differing scaling needs + mature DevOps + many bounded contexts.

---

## 1.6 The Big-5 Comparison (memorise this table for Q1!) ⭐

| Aspect | Monolithic | Modular Monolith | Event-Driven | Microkernel | Microservices |
|---|---|---|---|---|---|
| **Deployment** | Single | Single | Multiple | Core + plugins | Multiple |
| **Coupling** | Tight | Medium | Loose (async) | Loose | Loose |
| **Scalability** | Whole app | Whole app | Per service | Per plugin (limited) | Per service ✅ |
| **Complexity** | LOW ✅ | Low-Medium | High | Medium | HIGH ❌ |
| **Best for** | Small team, MVP | Growing team | Real-time, async workflows | Customer customisation | Large team, varied scale |
| **Data** | Single DB | Single DB w/ schemas | Distributed via events | Plugin-specific | Per-service DB |
| **Real example** | Stack Overflow | Shopify | LinkedIn Kafka | Eclipse, VS Code | Netflix, Uber |

---

<a name="2"></a>
# 2. Quality Attributes — Definitions, Trade-offs, Prioritisation

## What are Quality Attributes?

> **Quality Attributes (QAs)** — also called **"-ilities"** or **architecture characteristics** — are **measurable, testable** properties of a system that indicate **how well** it satisfies stakeholders' needs. They are **orthogonal to functionality** (you can talk about QAs without knowing what the system actually does).

## 2.1 The 4 Requirement Types (foundation)

Architecture is driven by quality attributes, not features. But quality attributes are just one of 4 requirement types:

| Type | Definition | Example | Architect's Role |
|---|---|---|---|
| **Functional** | What the system DOES | "User can withdraw money from ATM" | Less important — features can be added later |
| **Non-Functional (QAs)** | HOW WELL it does it ("-ilities") | "Withdrawal completes in <2 sec" | **PRIMARY CONCERN** |
| **Business Requirements** | Strategic — negotiable | "Launch within 6 months for $200k" | Balance with technical needs |
| **Constraints** | Pre-decided — **NON-negotiable** | "Must use open-source software only" | **Strict adherence** |

⚠️ **Critical exam trap:** Business Requirement (negotiable) ≠ Constraint (locked in).

## 2.2 The 10 Core Quality Attributes (memorise!) ⭐

Mnemonic: **AIMPRRSSTU**

### A — Availability
> The probability that the system is operational when needed. Measured as % uptime (e.g., 99.99% = ~52 min downtime/year).

**Affected by:** System errors, maintenance, infrastructure failures, malicious attacks, system load, dependent services.

**Real example:** AWS S3 has 99.999999999% durability (11 nines) and 99.99% availability. Banking ATMs aim for 99.95%+. Twitter's "Fail Whale" days were availability failures.

### I — Interoperability
> Ability to exchange information successfully by communicating with other systems.

**Two levels:**
- **Syntactic** — same data format/protocol (both use JSON over HTTPS).
- **Semantic** — same meaning (both agree `currency="USD"` means US Dollars, not Australian).

**Real example:** Payment systems must interop with banks (SWIFT, ACH). Healthcare uses HL7/FHIR for inter-hospital data exchange. Open Banking APIs (PSD2 in EU) enforce interoperability between banks and fintech.

### M — Modifiability
> The cost to make a change. Lower cost = higher modifiability.

**4 types of change:**
- **Functional change** (add dark mode)
- **Environment change** (Windows → Linux)
- **Protocol change** (REST → gRPC)
- **Dependency change** (MySQL → MongoDB)

**Real example:** Google Chrome's modifiability is high — they can add features and ship updates every 4 weeks. A 30-year-old COBOL banking system has low modifiability — every change is a months-long project.

### P — Performance
> The responsiveness of a system to execute actions within a given time interval.

**Two metrics:**
- **Latency** — time for ONE event (e.g., page load in 200ms).
- **Throughput** — events per time (e.g., 10,000 transactions per second).

**Real example:** Google Search returns results in <200ms globally. High-frequency trading systems target sub-millisecond latency. WhatsApp handles 100B+ messages/day (throughput).

### R — Reliability
> Probability the system will not fail to perform its intended functions over a specified time. Measured as MTBF (Mean Time Between Failures).

**Affected by:** Availability + Accuracy + Predictability.

**Real example:** NASA's Space Shuttle software had a defect rate of 0.1 errors per 1000 lines (vs industry average 1–25 per 1000) — extreme reliability requirement.

### R — Reusability
> Capability of components to be used in other applications.

**Example:** Software libraries (npm packages, JAR files), shared microservices.

**⚠ Cautionary tale — Therac 25 (radiation therapy machine, 1985–87):** Engineers reused software from the older Therac-20, which had **hardware safety interlocks** masking subtle software bugs. Therac 25 removed the hardware interlocks (to save cost) but kept the buggy software. Result: 3+ patients killed by radiation overdoses. **Reusability without context awareness can be deadly.**

### S — Scalability
> Ability to handle increased load without performance degradation.

**4 dimensions of load:**
- Load (request volume)
- Functions (number of features)
- Geographic (one country → globally)
- Methods (number of APIs)

**2 methods to scale:**
- **Horizontal** — add more servers (cashier analogy: hire more cashiers)
- **Vertical** — upgrade hardware (give one cashier caffeine)

**Real example:** Black Friday 2023: Amazon scaled horizontally by spinning up tens of thousands of extra EC2 instances. Twitter survived the Royal Wedding spike in 2018 by adding more compute. WhatsApp scales vertically + horizontally — uses Erlang VM (vertical) + many nodes (horizontal).

### S — Security
> Capability to prevent malicious attacks and unauthorized usage while serving legitimate users.

**6 concerns (NCIAAA):**
- **N**on-repudiation — can't deny a transaction
- **C**onfidentiality — protected from unauthorised access
- **I**ntegrity — data delivered as intended (not tampered with)
- **A**ssurance / authenticity — parties are who they claim to be
- **A**vailability (no DoS)
- **A**uditing — system tracks activities

**DoS attacks** are interesting — they're **both** security AND availability issues. Use this as a "QA overlap" example in the exam.

**Real example:** GDPR forces EU companies to implement confidentiality. PCI-DSS requires payment systems to encrypt card numbers. Banks log every transaction (auditing). 2-factor auth is authenticity.

### T — Testability
> Ease of demonstrating faults through testing. ~40% of dev cost is testing.

**Requires:** Ability to **control** internal state + inputs, and **observe** outputs.

**Real example:** Spotify uses contract testing (Pact) for their microservices. Google's "Hermetic Servers" approach ensures every test runs in an isolated environment for reproducibility.

### U — Usability
> How well users can accomplish their tasks.

**5 facets (LEEAC):**
- **L**earnability
- **E**fficiency
- **E**rror handling
- **A**daptability
- **C**onfidence in correctness

**Real example:** Apple's Human Interface Guidelines drive iOS usability. Slack's onboarding is praised for high learnability. Microsoft Office's ribbon was a major usability redesign in 2007.

## 2.3 ISO 25010 Classification (formal grouping)

Quality attributes are formally grouped by ISO 25010 into 8 categories:

| Category | Sub-attributes |
|---|---|
| **Functional Suitability** | Completeness, correctness, appropriateness |
| **Performance Efficiency** | Time behaviour, resource utilisation, capacity |
| **Compatibility** | Co-existence, interoperability |
| **Usability** | Learnability, operability, accessibility |
| **Reliability** | Maturity, availability, fault tolerance, recoverability |
| **Security** | Confidentiality, integrity, non-repudiation, accountability, authenticity |
| **Maintainability** | Modularity, reusability, modifiability, testability |
| **Portability** | Adaptability, installability, replaceability |

## 2.4 Trade-offs — The Architect's Daily Reality ⭐

> **"Architecture is the art of managing trade-offs."** — Use this phrase in any open-ended QA question.

### The 3 Classic Trade-off Pairs

| Boost… | Often Degrades… | Why |
|---|---|---|
| **Performance** | **Modifiability** | Heavy optimisation/caching makes code rigid (hardcoded paths, denormalised data) |
| **Availability** | **Consistency** (CAP theorem) | Replicating data for availability → some replicas will lag → eventual consistency |
| **Security** | **Usability** | More auth checks, MFA, captchas, password complexity = more user friction |

### Additional Real Trade-offs

| Boost… | Often Degrades… | Example |
|---|---|---|
| **Reusability** | **Performance** | Generic library can't optimise for one use case |
| **Reusability** | **Safety** | Therac 25 — reused software without re-validating context |
| **Testability** | **Performance** | Mock interfaces add overhead |
| **Backwards Compatibility** | **Safety** | Boeing 737 MAX — kept old aircraft type rating to avoid pilot retraining |
| **Modifiability** | **Security** | More flexibility means more attack surface |

### Real-World Trade-off Story
> *Twitter's 2008 architecture used Rails monolith + MySQL. Their priority was **time-to-market** (Performance and Scalability were lower priorities). When they hit massive scale, they re-architected to use Scala microservices + Kafka. The trade-off: they sacrificed development velocity (which is high on Rails) for runtime scalability and performance.*

## 2.5 Prioritising Quality Attributes

In any case study, you must:

1. **Read the brief carefully** — quality attributes are buried in phrases:
   - "millions of users" → **Scalability**
   - "24/7 access" → **Availability**
   - "medical records" → **Security** + **Reliability**
   - "future AI features" → **Modifiability** + **Extensibility**
   - "phased delivery" → **Deployability**
   - "third-party integration" → **Interoperability**
   - "small team / tight budget" → **Simplicity** (operational complexity)
   - "global users" → **Performance** + **Scalability**

2. **Pick 2–3 dominant ones** — don't try to satisfy all 10 (it's impossible).

3. **Explicitly state the trade-offs** you accept.

### Exam-Style Example

**Brief excerpt (MediConnect-like):** *"National health platform managing patient records, integrating with hospital legacy systems, serving millions of users including patients, healthcare professionals, and government administrators. Must accommodate future AI diagnosis features."*

**Dominant QAs:**
- **Security** (medical records, sensitive PII)
- **Scalability** (millions of users)
- **Interoperability** (legacy hospital systems — semantic AND syntactic)
- **Modifiability/Extensibility** (future AI features)
- **Availability** (national infrastructure)

**Trade-offs accepted:**
- Security vs Usability — extra auth checks (justified for medical data)
- Modifiability vs Performance — microservices network overhead (justified for team autonomy)

---

<a name="3"></a>
# 3. Architecture Business Cycle (ABC)

## What is the ABC?

> **Software architecture is a result of technical, business, and social influences. Its existence in turn affects those same environments, which then influence future architectures.** This **feedback loop** is the **Architecture Business Cycle (ABC)**.

The ABC is NOT a one-way arrow. It's a **circle** — architecture both **shapes** and **is shaped by** its environment.

## 3.1 The Architect's Influences (the "input" arrow)

The architect synthesises **4 influences** into a single architecture:

### Influence 1 — Stakeholders
Different stakeholders want different things:

| Stakeholder | Primary Concern |
|---|---|
| **Management** | Low cost, predictable schedule |
| **Marketing** | Fast time-to-market, competitive features |
| **End User** | Good UX, fast response, easy to use |
| **System Administrators** | Easy to operate, observable, secure |
| **Security Officers** | Compliance, no breaches |
| **Regulators** | Compliance with standards (GDPR, HIPAA, PCI-DSS) |

**Real scenario:** When building a banking app, the CISO demands TLS 1.3 + MFA + transaction signing (security). Product management demands biometric login (usability). The architect must balance: implement MFA but use device biometrics to make MFA fast.

### Influence 2 — Developing Organization
The company building the system shapes the architecture:

- **Past investments** — "We've already paid for Oracle DB licences, so we use Oracle."
- **Future investments** — "We're moving to AWS over the next 2 years; build cloud-native."
- **Organisational structure** — Conway's Law: *"Any organisation that designs a system will produce a design whose structure is a copy of the organisation's communication structure."*

**Real scenario:** Amazon's microservices reflect their two-pizza team structure. Conversely, a small startup with 4 engineers shouldn't build microservices — they'd be reinventing communication channels.

### Influence 3 — Architect's Experience
The architect's own background biases their design:

- **Technical skills** — knows AWS but not Azure → recommends AWS.
- **Domain knowledge** — has worked in banking → designs differently than someone from gaming.
- **Past project lessons** — burned by microservices once? Will recommend modular monolith.

**Real scenario:** Two architects designing the same e-commerce platform — one from Java enterprise background (likely recommends Spring microservices with Kafka), another from Rails startup background (likely recommends modular monolith first).

### Influence 4 — Technical Environment
The current state of software engineering:

- **Available SE techniques** (DevOps maturity, container orchestration, observability tools)
- **Industry trends** (microservices in 2018, serverless in 2022, AI-augmented dev in 2025)
- **Available technologies** (Kubernetes, Kafka, gRPC didn't exist 15 years ago)

**Real scenario:** A 2010 architect couldn't have recommended Kubernetes (didn't exist until 2014). A 2025 architect can leverage Kubernetes, service meshes (Istio), and OpenTelemetry — none of which existed when many legacy systems were built.

## 3.2 The Architect's Influences Diagram

```
   Stakeholders ───┐
                   ├──→ Requirements (Qualities) ──┐
   Developing Org ─┘                               │
                                                   ▼
   Technical Environment ────────────────→ ARCHITECT(s) ──→ Architecture ──→ System
                                                   ▲
   Architect's Experience ───────────────────────┘
```

The architect is a **funnel**: many influences pour in, a single architecture comes out.

## 3.3 The Back-Arrow — What Architecture Affects (Ramifications)

The "cycle" part of ABC: architecture **changes** its own influences. **5 ramifications**:

### Ramification 1 — Structure of the Developing Organization
Architecture decides team structure.
- Microservices → squads / cross-functional teams.
- Monolith → functional teams (frontend, backend, DB).
- "Inverse Conway Maneuver" — design the architecture you want, then restructure teams to match.

### Ramification 2 — Goals of the Developing Organization
- A successful product opens new markets the company didn't plan for.
- A failed architecture (Boeing 737 MAX) can cripple the company's strategic plans.

### Ramification 3 — Future Customer Requirements
- Uber's tracking feature created an expectation; now every food delivery app must have live tracking.
- Netflix's recommendation engine raised user expectations across the entire entertainment industry.

### Ramification 4 — The Architect
- Architects gain experience from each project.
- Brings lessons learned into the next architecture.

### Ramification 5 — Development Process & Culture
- Microservices forced DevOps culture into many companies.
- Adoption of CI/CD, monitoring tools, blameless post-mortems — all driven by distributed architectures.

## 3.4 Putting it Together — The Cycle

```
   Influences ────→ Architect ────→ Architecture ────→ System
        ▲                                                  │
        │                                                  │
        └──────────── (feedback) ──────────────────────────┘
```

## 3.5 Real-World ABC Example — Netflix

> Netflix's journey shows the ABC in action:
>
> 1. **Initial influences (2000s):** They were a DVD-by-mail company. Stakeholders wanted online streaming. Tech environment: AWS just emerged. Architect's background: traditional Java enterprise.
> 2. **Initial architecture:** Monolith on a traditional DB.
> 3. **System ramifications:** Massive scaling needs as streaming took off. Database corruption incident in 2008 caused a 3-day outage.
> 4. **Feedback loop:** The outage changed the developing organisation — they decided "we can't run our own infrastructure". This new requirement (use cloud) re-influenced future architecture.
> 5. **New architecture:** Microservices on AWS. This required new processes (CI/CD, chaos engineering — "Chaos Monkey").
> 6. **Industry ramifications:** Netflix's success popularised microservices industry-wide. Now most companies "do microservices" because Netflix did.

## 3.6 Exam-Style Answer Template for ABC Questions

**Q3.1 2025 asked: "Explain the Architecture Business Cycle." (4 marks)**

> *The Architecture Business Cycle (ABC) describes how software architecture is the result of **technical, business, and social influences** (stakeholders, developing organisation, architect's experience, technical environment), and how the resulting architecture in turn **affects** those same environments — changing the organisation's structure, goals, future customer expectations, the architect's experience, and the development process — which then influences future architectures. This **feedback loop** between architecture and its environment is what makes architecture a strategic, evolving practice rather than a one-time design activity.*

That's a **full-marks 4-mark answer**.

---

<a name="4"></a>
# 4. The 7 Architectural Activities

The 2025 paper Q2 asked about this **3 times** in different sub-questions (10 + 6 + 6 marks). Memorise this list.

> Mnemonic: **B-U-C-D-A-I-C**

## The 7 Activities

| # | Activity | What it is | Why it matters |
|---|---|---|---|
| 1 | **Business Case** | Justifying why we build this system | Without it, the project never gets funded |
| 2 | **Understanding Requirements** | FRs + NFRs (especially Architecturally Significant Requirements - ASRs) | Wrong requirements = wrong architecture |
| 3 | **Creating/Selecting Architecture** | The actual design work | The core architect activity |
| 4 | **Documenting & Communicating** | Writing it down for stakeholders | Without comms, the architecture is useless |
| 5 | **Analyzing/Evaluating** | Reviewing for risks and trade-offs | Catch problems early when fix is cheap |
| 6 | **Implementing** | Making it real | Architecture without implementation is fiction |
| 7 | **Conformance** | Ensuring code matches architecture | Prevents architecture drift |

## 4.1 Activity 1 — Creating the Business Case

The architect helps answer questions like:
- **Market need** — is there demand?
- **Cost** — how much will it cost to build + operate?
- **Target market** — who will use it?
- **Time-to-market** — when must it ship?
- **Integration** — does it interface with existing systems?
- **Limitations / constraints** — regulatory, technical, budgetary?

**Why the architect MUST be consulted:**
> *If the architect is not consulted, business goals may become technically infeasible. A salesperson might promise "we'll deliver in 3 months for $10k" — but only an architect can spot that the features promised actually require 9 months and $80k.*

**Real-world scenario:** A startup founder once told their architect "we'll launch in 4 months with all these features". The architect did rough sizing: 18 months realistic. The founder went to investors with the 4-month promise anyway. Result: investors lost faith when the deadline slipped repeatedly, and the company died.

## 4.2 Activity 2 — Understanding the Requirements

Split into:

### Functional Requirements
- **OOAD** uses **Use Cases / Scenarios**.
- **Safety-critical systems** use **Formal Specification Languages** (Z, B, TLA+) or **Finite-State Machine models**.

### Non-Functional Requirements (the architect's main concern)
- **Quality Attribute Scenarios (QAS)** — formal, testable
- **Prototyping** — build a small thing to validate feasibility
- **Domain Modelling** — model the business to surface hidden requirements

> **Architecturally Significant Requirements (ASRs)** — the architect doesn't worry about *every* requirement. They focus on the ASRs — the ones that shape the architecture.

**Real example:** Twitter's ASR in 2010 was "handle 1 billion+ tweets/day" — this drove their move from Rails monolith to Scala. A non-ASR might be "tweets should support emoji" — that's a feature, not architecture.

## 4.3 Activity 3 — Creating or Selecting the Architecture

This is **iterative**:

```
   System Requirements & Project Context
                 │
                 ▼
          Requirements Analysis ◄──── NO (loop back)
                 │
                 ▼
       Architecturally significant aspects
                 │
                 ▼
           Decision-Making
                 │
                 ▼
      Candidate components + relations
                 │
                 ▼
        Architectural Evaluation
                 │
                 ▼
        ┌──────────────────┐
        │ Architecture     │── YES ──→ DONE
        │ acceptable?      │── NO  ──→ back to Requirements Analysis
        └──────────────────┘
```

**Key insight:** First-attempt architectures are rarely right. Iterate.

## 4.4 Activity 4 — Documenting & Communicating

Different audiences need different things:

| Audience | What they need |
|---|---|
| **Developers** | Work assignments — what to build |
| **Testers** | Task structure — what to test |
| **Management** | Scheduling implications — who blocks whom |
| **Customer** | High-level architecture (no code) |
| **Operations** | Deployment, monitoring requirements |

**Real-world scenario:** A bank built a great architecture but documentation was sparse. When the lead architect left, the team struggled for months figuring out the system. Documentation isn't optional — it's **business continuity**.

## 4.5 Activity 5 — Analyzing/Evaluating

Multiple candidate designs always exist. Choose rationally using formal methods:

| Method | Focus |
|---|---|
| **ATAM** (Architecture Tradeoff Analysis Method) | **Multiple competing QAs + trade-offs** |
| **CBAM** (Cost-Benefit Analysis Method) | **Economic implications** |
| **SAAM** (Software Architecture Analysis Method) | **One QA at a time, candidate comparison** |
| **ARID** (Active Reviews for Intermediate Designs) | **Preliminary component designs** |

(More on SAAM in Section 8.)

## 4.6 Activity 6 — Implementing

The architect's role during implementation:

- **Technology selection** — which DB, which message broker, which cloud
- **Process setup** — code review process, branching strategy, CI/CD pipelines
- **Team building** — identify technical specialists
- **Skill gap mitigation** — training, hiring, consulting
- **Constant guidance** — answer "is this within the architecture?" questions

**Real-world scenario:** During implementation, developers often face decisions not covered by architecture decisions (e.g., "should this query use a JOIN or a separate call?"). The architect's job is to be available to answer these without becoming a bottleneck.

## 4.7 Activity 7 — Ensuring Implementation Conforms to Architecture

> *"Constant vigilance is required to ensure that the actual architecture and its representation remain faithful to each other in the maintenance phase."*

This is **THE EXAM-CRITICAL ACTIVITY** for Q2.4 2025 (which asked exactly this!).

### Architecture Drift / Erosion
Over time, the **actual** system slowly diverges from the **documented** architecture:
- Developers take shortcuts under deadline pressure.
- Bug fixes patch the wrong place.
- New features ignore module boundaries.
- Refactoring is deferred indefinitely.
- Documentation goes stale.

### How to prevent drift in maintenance:

1. **Code reviews** — every PR checked against architecture rules.
2. **Architecture Review Board (ARB)** — periodic deep reviews of changes.
3. **Static analysis tools** — automated checks (e.g., ArchUnit for Java enforces layer rules).
4. **Late evaluation** — measure cohesion + coupling metrics on the actual code.
5. **Ongoing documentation** — keep diagrams in sync with code (architecture-as-code).
6. **Variances** — formal exceptions to architecture rules when needed (with reason).
7. **Refactoring debt tracking** — log every shortcut taken; pay it down later.

### Real-World Example — Architecture Erosion
> *A large UK bank had a beautiful 3-tier architecture in 2005. By 2020, after countless quick fixes, the system had ~20% direct presentation-to-database calls (bypassing the business layer). When they tried to modernise (move data layer to a new DB), they couldn't — the dependencies were everywhere. The fix cost £150 million and 4 years.* **Architecture drift compounds.**

## 4.8 Exam Answer Template for Q2.4 (6 marks!)

**Q2.4 2025: "Ensuring that the implementation conforms to the architecture is an important step in the Architectural Activities. With appropriate reasons, discuss the importance of this step in the maintenance phase of the software."**

> *In the maintenance phase, architectural drift is the architect's biggest enemy. As bugs are fixed, features added, and shortcuts taken under deadline pressure, the actual system slowly diverges from the documented architecture — a phenomenon known as **architecture drift** or **architecture erosion**. The importance of this step in maintenance:*
>
> *1. **Prevents technical debt accumulation** — small unchecked shortcuts compound into massive refactoring costs.*
>
> *2. **Maintains intended quality attributes** — for instance, if a layered architecture's rule "only the business layer accesses the database" is violated, security and modifiability are silently degraded.*
>
> *3. **Protects future modifiability** — when boundaries blur, future changes ripple unpredictably across the system.*
>
> *4. **Maintains documentation accuracy** — without conformance checks, diagrams become fiction, and new team members are misled.*
>
> *5. **Enables architectural evolution** — you can only evolve an architecture you can trust. Drifted systems are nearly impossible to refactor (e.g., a UK bank case where £150M was needed to undo 15 years of drift).*
>
> *6. **The cost curve** — fixing architecture violations early is cheap; doing it after years of accumulation is exponentially expensive.*
>
> *Enforcement mechanisms include: code reviews, Architecture Review Boards (ARBs), static analysis tools (e.g., ArchUnit), late evaluation via cohesion/coupling metrics, and formal variances for legitimate exceptions.*

That's a **full 6-mark answer**.

---

<a name="5"></a>
# 5. Quality Attribute Scenarios (QAS)

The 2025 Q4 asked you to write **concrete QAS for Availability AND Performance** (3 marks each).

## What is a QAS?

> A **Quality Attribute Scenario (QAS)** is a **universal, formal way to express quality attributes** — analogous to use cases for functional requirements. It captures **unambiguous, testable** quality requirements.

## 5.1 General vs Concrete

| | General Scenario | Concrete Scenario |
|---|---|---|
| **Scope** | System-independent template | System-specific instance |
| **Purpose** | Framework / menu of possibilities | The actual requirement for YOUR system |
| **Use in exam** | Background knowledge | What you MUST WRITE |

## 5.2 The 6-Part Template — "SSAERR" ⭐⭐⭐

Every QAS has **6 parts**:

| # | Part | Question | Plain English |
|---|---|---|---|
| 1 | **Source** | WHO? | The originator (user, system, attacker) |
| 2 | **Stimulus** | WHAT ACTION? | The event/action that arrives |
| 3 | **Artifact** | WHICH PART? | The part of the system affected |
| 4 | **Environment** | WHEN/CONDITIONS? | Normal? Overload? Degraded? |
| 5 | **Response** | WHAT DOES SYSTEM DO? | The reaction |
| 6 | **Response Measure** | HOW WELL? (NUMBER!) | The metric — **MUST include a number** |

⚠️ **The #1 student mistake:** Forgetting a NUMBER in the response measure. *"Must be fast"* = 0 marks. *"<200ms p95 latency under 1000 RPS"* = full marks.

## 5.3 Availability QAS — Worked Example

### Real Scenario
> *An online banking app must remain available even when one server fails.*

### Concrete QAS
| Part | Value |
|---|---|
| **Source** | External attacker (or internal hardware failure) |
| **Stimulus** | Primary application server crashes (omission fault) |
| **Artifact** | The transaction processing subsystem |
| **Environment** | Peak weekday operating hours (10 AM–4 PM) |
| **Response** | System detects the crash via heartbeat, fails over to standby server, logs the event |
| **Response Measure** | **Failover completes within 5 seconds; zero transactions lost; 99.95% monthly uptime maintained** |

### How to Write It as a Single Sentence
*"An external attacker (or internal hardware failure) causes the primary application server to crash during peak weekday operating hours. The system detects the crash via heartbeat, fails over to the standby server in under 5 seconds with zero transaction loss, while maintaining 99.95% monthly uptime."*

## 5.4 Performance QAS — Worked Example

### Real Scenario
> *A photo-sharing site serves thumbnails 10,000× more often than full-size images.*

### Concrete QAS
| Part | Value |
|---|---|
| **Source** | Thousands of concurrent public users |
| **Stimulus** | Stochastic HTTP requests for thumbnails (peak: 10,000 RPS) |
| **Artifact** | The thumbnail-serving subsystem |
| **Environment** | Normal operation, peak browsing time (8–10 PM) |
| **Response** | System serves the requested thumbnails from cache or origin |
| **Response Measure** | **Average latency ≤ 200ms; p99 latency ≤ 500ms; throughput ≥ 10,000 req/sec** |

## 5.5 Modifiability QAS — Worked Example

### Real Scenario
> *Developers regularly need to add new payment providers (Stripe, PayPal, regional banks).*

### Concrete QAS
| Part | Value |
|---|---|
| **Source** | Backend developer |
| **Stimulus** | Wants to add a new payment provider integration |
| **Artifact** | The payment service codebase |
| **Environment** | At design time + deploy time |
| **Response** | Developer adds new provider as a plugin without modifying core payment logic; tests pass; deploys via standard pipeline |
| **Response Measure** | **<2 person-days of effort; zero changes to core PaymentProcessor class; <1 hour deploy time; no impact on other payment providers** |

## 5.6 Security QAS — Worked Example

### Real Scenario
> *A health platform must detect and respond to unauthorized data access attempts.*

### Concrete QAS
| Part | Value |
|---|---|
| **Source** | Correctly identified individual (insider threat) or unauthenticated external attacker |
| **Stimulus** | Attempts to access patient records they're not authorized for |
| **Artifact** | The patient records subsystem |
| **Environment** | Online, normal operation |
| **Response** | System blocks access, logs the attempt with full context (who, when, what), alerts the security team |
| **Response Measure** | **0% false negatives on blocking; alert sent within 60 seconds; full audit trail with user ID, timestamp, IP, requested record; 100% legitimate access traffic unaffected** |

## 5.7 Testability QAS — Worked Example

### Real Scenario
> *A unit tester needs to validate a completed payment processing component.*

### Concrete QAS
| Part | Value |
|---|---|
| **Source** | Unit tester |
| **Stimulus** | Performs unit tests on the completed payment processor |
| **Artifact** | The payment processor component |
| **Environment** | CI/CD pipeline, automated test environment |
| **Response** | Component provides mockable interfaces, dependency injection, and built-in monitors for state observation |
| **Response Measure** | **≥85% statement coverage achieved in <30 seconds; full test suite completes in <5 minutes; new test setup time <10 minutes** |

## 5.8 Usability QAS — Worked Example

### Real Scenario
> *A user wants to cancel a long-running file upload.*

### Concrete QAS
| Part | Value |
|---|---|
| **Source** | End user |
| **Stimulus** | Clicks "Cancel" during a file upload |
| **Artifact** | The upload module |
| **Environment** | At runtime, during normal operation |
| **Response** | System aborts the upload, frees server resources, displays "Upload cancelled" confirmation |
| **Response Measure** | **Cancellation completes in <1 second; no data corruption; clear UI feedback within 200ms** |

## 5.9 The Exam Answer Template

> Whenever you see *"Write a concrete QAS for [QA] for [system]"*, use the **6-row labelled table** + always include numbers.

---

<a name="6"></a>
# 6. Tactics — How to Actually Achieve Quality Attributes

The 2025 Q4 asked you to **propose tactics** for Availability AND Performance (2 marks each).

## What is a Tactic?

> An **architectural tactic** is a **named, planned way** to satisfy a quality attribute response measure through architectural decisions. Tactics are **smaller than patterns** — *"patterns package tactics"*.

## 6.1 The 3-Step Format for Proposing a Tactic ⭐

When the exam asks "propose a tactic":

> **Step 1.** Name the tactic + its category.
> **Step 2.** Describe what it does (the mechanism).
> **Step 3.** Link it to the QAS response measure: *"This satisfies the QAS response measure of [X] by [mechanism]."*

## 6.2 Availability Tactics — "DRP" (Detection · Recovery · Prevention)

### Detection — "Are you alive?"
| Tactic | What it does | Real example |
|---|---|---|
| **Ping/Echo** | Send a ping, wait for echo. No echo = fault. | Kubernetes liveness probe — pings every 10s. |
| **Heartbeat** | Component periodically emits "I am alive". | Cassandra nodes heartbeat in a cluster. |
| **Exceptions** | Trigger exception handler when fault occurs in-process. | Java try-catch, Python except. |

### Recovery — Preparation + Repair
| Tactic | Downtime | Real example |
|---|---|---|
| **Voting** | 0 | Aerospace systems — 3 redundant computers vote on flight commands. |
| **Active Redundancy** | 0 to seconds | DynamoDB's multi-master replication. |
| **Passive Redundancy** | Seconds | PostgreSQL streaming replication with hot standby. |
| **Spare** | Minutes | AWS Auto Scaling Group with standby instances. |

### Recovery — Reintroduction
| Tactic | What it does | Real example |
|---|---|---|
| **Shadow Operation** | Recovered component mimics backup before going live. | Netflix's "Sticky Canaries" — new code runs in shadow mode first. |
| **State Resynchronization** | Sync state after recovery. | Cassandra's anti-entropy repair. |
| **Checkpoint/Rollback** | Save state periodically; restore on fault. | Database transactions with savepoints. |

### Prevention
| Tactic | What it does | Real example |
|---|---|---|
| **Removal from Service** | Take component down periodically. | Restarting Java apps to prevent memory leaks (some banks do this nightly). |
| **Transactions** | Atomic units of work. | ACID transactions in any RDBMS. |
| **Process Monitor** | Watch for faulting processes, restart. | systemd, Kubernetes pod restart policy, PM2 for Node.js. |

### Worked Tactic Answer — Q4.a.ii 2025

> *"I propose using **Passive Redundancy** (an Availability tactic in the Fault Recovery — Preparation & Repair category). The system runs a **master server** serving photo requests, with one or more **backup servers** whose state is continuously updated from the master. If the master fails, a heartbeat-driven failover promotes a backup within **seconds**. This satisfies the QAS response measure of high availability with at most a few seconds of disruption — meeting the requirement for accessing large photos. For absolute zero downtime, **Active Redundancy** could be chosen at higher infrastructure cost."*

## 6.3 Performance Tactics — "DMA" (Demand · Management · Arbitration)

### Resource Demand — Reduce the Work
| Tactic | What it does | Real example |
|---|---|---|
| **Increase Computational Efficiency** | Better algorithms. | Quicksort instead of bubble sort. Use B-trees not linear scans. |
| **Reduce Computational Overhead** | Compute once, refer many times. | Memoization. Pre-computed config (Java `final static`). |
| **Control Sampling Frequency** | Lower poll rates. | Reduce heartbeat from 1s to 5s if 5s is sufficient. |

### Resource Management — Use Smarter ⭐
| Tactic | What it does | Real example |
|---|---|---|
| **Introduce Concurrency** | Parallel processing. | Multi-threading. Goroutines. async/await. Worker pools. |
| **Maintain Multiple Copies (Caching!)** | Cache data near consumers. | **Redis, Memcached, CDN (Cloudflare/Akamai)**. Stack Overflow's 1.5 TB RAM cache. |
| **Increase Available Resources** | More/faster hardware. | Vertical: bigger EC2 instance. Horizontal: more instances. |

### Resource Arbitration — Decide Who Wins
When multiple requests compete for the same resource:
| Policy | What it does | Example |
|---|---|---|
| **FIFO** | First-in-first-out queue | Email inbox, ticket queues |
| **Fixed Priority** | Higher priority always wins | OS process priorities |
| **Round Robin** | Equal time slices to each | Multi-tenant DB query schedulers |

### Worked Tactic Answer — Q4.a.iv 2025 ⭐

> *"I propose using **Maintain Multiple Copies** (a Performance tactic in the Resource Management category), specifically **caching thumbnails on a CDN (Content Delivery Network)**. Since thumbnails are accessed **10,000× more frequently** than large photos, caching them in edge servers (Cloudflare, AWS CloudFront) drops latency from server-side processing time (~200ms) to CDN response time (~20ms), and dramatically reduces load on the origin server. Combined with **Increase Available Resources** (provisioning more web servers behind a load balancer), this satisfies the performance response measure of sub-200ms thumbnail latency at peak load (10,000 RPS)."*

## 6.4 Modifiability Tactics — "LPD"

### Localize Modifications
- **Maintain Semantic Coherence** — keep related things together (high cohesion!)
- **Anticipate Expected Changes** — keep volatile parts in one place
- **Generalize the Module** — make it broader-purpose
- **Limit Possible Options** — fewer dials = simpler

### Prevent Ripple Effect
- **Hide Information** — encapsulation
- **Maintain Existing Interfaces** — use Adapter pattern
- **Restrict Communication Paths** — don't let data flow through too many modules
- **Use an Intermediary** — Façade, Mediator, Delegate, Proxy patterns

### Defer Binding Time
- **Runtime Registration** — plug & play
- **Configuration Files** — change config, not code (e.g., `.env`, `application.yml`)
- **Polymorphism** — method names resolved at runtime
- **Component Replacement** — load components at runtime
- **Adherence to Defined Protocols** — independent processes bind at runtime

**Real example:** Java's interface-based polymorphism + Spring's dependency injection allow swapping implementations without code changes.

## 6.5 Security Tactics — "RDR" (Resist · Detect · Recover)

### Resist Attacks
- **Authenticate Users** — verify identity (passwords, MFA, biometrics)
- **Authorize Users** — verify permissions (RBAC, ABAC)
- **Maintain Data Confidentiality** — encrypt (TLS, AES, RSA)
- **Limit Exposure** — minimise attack surface (no unused services)
- **Limit Access** — firewalls, DMZ, VPN

### Detect Attacks
- **Intrusion Detection (IDS)** — compare historical vs current behaviour
  - Snort, Suricata, AWS GuardDuty

### Recover from Attacks
- **Restoration** — use availability tactics (backups, redundancy)
- **Identification** — audit trail (must live in trusted environment!)

**Real example:** A bank uses TLS (confidentiality), MFA (authentication), RBAC (authorization), AWS GuardDuty (IDS), encrypted backups in offsite location (restoration), and immutable audit logs in WORM storage (identification).

## 6.6 Testability Tactics

### Input / Output
- **Record / Playback** — capture real traffic for tests
- **Separate Interface from Implementation** — enables mocking
- **Specialize Access Routes** — test-only interfaces (use cautiously)

### Internal Monitoring
- **Built-in Monitors** — components expose state observation interfaces

**Real example:** Spotify's Pact framework for contract testing. Twitter's open-source Diffy for shadow testing. OpenTelemetry for built-in monitoring.

## 6.7 Usability Tactics

### Runtime
- **User Initiatives** — Cancel, Undo, Redo, Pause
- **System Initiatives** — feedback, suggestions, notifications, confirmations
- **Mixed** — progress bars

### Design Time
- **Separate UI from rest** — MVC, MVVM patterns
- **Separate UI Components** — modular UI
- **Maintain Semantic Coherence** — localise expected changes

**Real example:** All modern apps use Cancel/Undo (Ctrl+Z is everywhere). Gmail's "Undo Send" gives 30 seconds to retract. React's component model is a usability tactic at design time.

---

<a name="7"></a>
# 7. The 4+1 View Model (Q3.3 — 5 marks!)

## What is the 4+1 View Model?

> Philippe Kruchten's **4+1 View Model** describes software architecture from **5 perspectives**, each tailored to a different stakeholder group. Used because **one diagram cannot show everything**.

## 7.1 The 5 Views

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

### Logical View — "What does it do?"
- **Captures:** Functionality. Objects, classes, services.
- **Diagrams:** UML class diagrams, ER diagrams, domain models.
- **Audience:** End users, functional analysts.
- **Real example:** Netflix's logical view shows "User", "Profile", "Title", "Recommendation" as logical entities.

### Development View — "How is the code organised?"
- **Captures:** Modules, packages, libraries, build artifacts.
- **Diagrams:** UML package diagrams, dependency graphs.
- **Audience:** Developers.
- **Real example:** Netflix's development view shows microservice repositories grouped by team ownership.

### Process View — "What's running at runtime?"
- **Captures:** Processes, threads, concurrency, communication.
- **Diagrams:** UML activity diagrams, sequence diagrams.
- **Audience:** System integrators, performance engineers.
- **Real example:** Netflix's process view shows how a video play request flows through 50+ services in real-time.

### Physical View (Deployment View) — "Where does it run?"
- **Captures:** Software mapped to hardware. Servers, networks, datacentres.
- **Diagrams:** UML deployment diagrams, network topology.
- **Audience:** SysAdmins, DevOps.
- **Real example:** Netflix's physical view shows AWS regions, availability zones, ELBs, EC2 instances, CloudFront edges.

### +1 — Scenarios (Use Cases)
- **Captures:** Important use cases that exercise all 4 views.
- **Diagrams:** Use case diagrams, scenario walkthroughs.
- **Audience:** Everyone — proves the architecture works as a whole.
- **Real example:** Netflix's "User watches Stranger Things on a smart TV in Brazil" scenario walks through all 4 views simultaneously.

## 7.2 Why "4+1" and not just "5"?

The **Scenarios** are NOT a separate view of static structure — they're **dynamic validation** that ties the other 4 views together. If a scenario can be successfully traced through all 4 views, the architecture is consistent.

## 7.3 Mapping 4+1 to Our 3 Structures (from Lec 3)

| 4+1 View | Maps to which structure category? |
|---|---|
| Logical | Module (Class structure) |
| Development | Module (Decomposition, Implementation) |
| Process | Component-and-Connector (Process structure) |
| Physical | Allocation (Deployment) |
| Scenarios | Cross-cutting |

## 7.4 Real-World Application — Spotify

> *Spotify uses 4+1 to communicate with diverse stakeholders.*
>
> - **Logical view** (for product managers): "User", "Playlist", "Track", "Artist" with their relationships.
> - **Development view** (for engineers): Squads own specific microservices; each squad's repos = their part of the development view.
> - **Process view** (for performance team): How a "play" request flows: client → API gateway → playlist service → recommendation service → encoding service → CDN.
> - **Physical view** (for SREs): Spotify runs on Google Cloud Platform across multiple regions; CDN delivers audio from edge.
> - **Scenarios**: "User searches for a song" walks through all 4 views to validate end-to-end.

## 7.5 Exam Answer Template — Q3.3 (5 marks)

> *The **4+1 View Model**, developed by Philippe Kruchten, describes software architecture from 5 stakeholder-oriented perspectives:*
>
> *1. **Logical View** — captures the functionality the system provides as objects, classes, and services. Audience: end users and functional analysts.*
>
> *2. **Development View** (Implementation View) — captures the modules and packages in the codebase. Audience: developers.*
>
> *3. **Process View** — captures runtime processes, threads, concurrency, and how they communicate. Audience: system integrators and performance engineers.*
>
> *4. **Physical View** (Deployment View) — captures how software is mapped to hardware (servers, networks). Audience: SysAdmins and DevOps.*
>
> *5. **+1: Scenarios** — a set of important use cases that exercise the architecture by tying the 4 views together. Used to validate that the architecture is consistent across views.*
>
> *This model is widely used because no single view can communicate everything about an architecture — each stakeholder needs the appropriate level of detail for their concerns.*

That's a **full 5-mark answer**.

---

<a name="8"></a>
# 8. SAAM — Software Architecture Analysis Method (Q3.5 — 4 marks!)

## What is SAAM?

> **SAAM** (Software Architecture Analysis Method) is a **scenario-based** software architecture evaluation method developed at the **SEI (Software Engineering Institute, Carnegie Mellon)**. It aims to **predict the quality of a system before it has been developed** by analysing the impact of predefined scenarios on architectural components.

## 8.1 Why Use SAAM?

- Predicts architectural quality **before development** (cheap to fix problems!)
- **Compares candidate architectures** systematically
- Exposes **risks** and **trouble spots**

## 8.2 The 5 SAAM Steps — "SDECE" ⭐⭐⭐

### Step 1 — Specify
- Collect **requirements and constraints**.
- Develop **initial scenarios** (representing stakeholders' interests).

### Step 2 — Describe Architectures
- Present **candidate architecture(s)**.
- Provide both **static** (structure) and **dynamic** (behavioural) representations.

### Step 3 — Elicit Scenarios
- Simulate scenarios with **relevant stakeholders present**.
- **Facilitated brainstorming** to generate scenario set.

### Step 4 — Classify and Prioritise Scenarios
Two categories:
- **Direct Scenarios** — architecture **supports them directly** without modification.
- **Indirect Scenarios** — architecture **requires modification** to support them.

**Voting** is used to prioritise.

### Step 5 — Evaluate
- Evaluate architecture against the **prioritised scenarios**.
- Identify **impact** (which components affected, what changes needed).
- Document **results**.

## 8.3 Direct vs Indirect Scenarios — The Key SAAM Concept

| | Direct Scenario | Indirect Scenario |
|---|---|---|
| **What** | Architecture handles it as-is | Architecture must be modified |
| **Implication** | Architecture is **fit** for that requirement | A change is **needed** → cost analysis |
| **Action** | Validates the architecture | Drives improvements / re-design |
| **Example** | "User views their account balance" → existing API supports it | "Add multi-currency support" → significant modification needed |

## 8.4 SAAM Benefits

1. **Helps assess risks** inherent in an architecture
2. **Compares candidate architectures** systematically
3. **Guides inspection** of the architecture, focusing on **trouble spots** — like requirement conflicts or incomplete design specs from particular stakeholders' perspectives

## 8.5 SAAM vs ATAM vs ARID

| | ARID | SAAM | ATAM |
|---|---|---|---|
| **Stage** | Preliminary (component-level) | Architecture design | Architecture design + multi-QA |
| **Focus** | Design suitability | Quality prediction; candidate comparison | Trade-offs + Sensitivity + Risk analysis |
| **QAs handled** | Few | **One at a time** | **MULTIPLE competing QAs** |
| **Weight** | Lightweight | Medium | Heavy / Formal |

## 8.6 Real-World SAAM Application

> *A government agency is choosing between two candidate architectures for a new tax filing system:*
> - **Architecture A:** A modular monolith with PostgreSQL backend.
> - **Architecture B:** Microservices with separate databases per service.
>
> *They run a SAAM workshop:*
> - **Step 1 (Specify):** Collect requirements — 10M citizens, peak load on April 15, 7-year data retention.
> - **Step 2 (Describe):** Both architectures presented as block diagrams + sequence diagrams.
> - **Step 3 (Elicit):** Stakeholders brainstorm 30 scenarios: filing returns, amending returns, audit access, ML fraud detection, data exports.
> - **Step 4 (Classify):** Architecture A handles 20 scenarios directly, requires modification for 10 (mostly fraud detection ML). Architecture B handles 25 directly, requires modification for 5.
> - **Step 5 (Evaluate):** Architecture B wins on modifiability for future ML features, but Architecture A wins on operational simplicity and cost.
>
> *Decision: Architecture A (modular monolith) for v1, with explicit plan to extract fraud detection as a microservice later. SAAM provides the rationale for this decision.*

## 8.7 Exam Answer Template — Q3.5 (4 marks)

**Q3.5 2025: "Explain SAAM (Software Architecture Analysis Method) in brief and outline its main objectives and benefits."**

> ***SAAM (Software Architecture Analysis Method)** is a **scenario-based** software architecture evaluation method developed at the Software Engineering Institute (SEI). It aims to **predict the quality of a system before it has been developed** by analysing the impact of predefined scenarios on architectural components. It addresses concerns at the architecture design level that cross-cut multiple architectural components.*
>
> ***The 5 SAAM steps are:** (1) **Specify** — collect requirements and develop initial scenarios; (2) **Describe Architectures** — present candidate architectures with static and dynamic representations; (3) **Elicit Scenarios** — facilitated brainstorming with stakeholders; (4) **Classify and Prioritise** — distinguish **Direct** scenarios (architecture supports as-is) from **Indirect** scenarios (architecture needs modification), then vote to prioritise; (5) **Evaluate** — assess the architecture against the prioritised scenarios.*
>
> ***Main objectives:** predict quality early, compare candidate architectures systematically, and expose risks.*
>
> ***Benefits:** (1) helps assess risks inherent in an architecture; (2) enables systematic comparison of candidate architectures; (3) guides inspection toward trouble spots like requirement conflicts and incomplete specifications.*

**Full 4-mark answer.** ✅

---

<a name="9"></a>
# 9. N-Tier vs Layered Architecture (Q3.6 — 4 marks!)

This was a direct distinction question in 2025. Will likely repeat.

## What Are They?

### Layered Architecture
> Groups related functions into **horizontal layers** stacked on top of each other. Each layer can only communicate with itself or layers **below** it.

### N-Tier Architecture
> An **extension of Layered architecture** where **each layer can execute on a different physical location** (machine, network).

## 9.1 The Killer Distinction ⭐

> **Layered = LOGICAL separation. N-Tier = PHYSICAL separation.**
>
> **Every N-Tier architecture is Layered, but not every Layered architecture is N-Tier.**

## 9.2 Visual Comparison

### Layered (single machine, logical layers):
```
   ┌──────────────────────────────────┐
   │ Machine 1 (one process)          │
   │  ┌────────────────────────────┐  │
   │  │  Presentation Layer        │  │
   │  ├────────────────────────────┤  │
   │  │  Business Logic Layer      │  │
   │  ├────────────────────────────┤  │
   │  │  Data Access Layer         │  │
   │  └────────────────────────────┘  │
   │       │  in-process call         │
   │       ▼                          │
   │  Database (same machine)         │
   └──────────────────────────────────┘
```

### N-Tier (multiple machines, physical tiers):
```
   ┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
   │ Browser  │────▶│ Web Tier │────▶│ App Tier │────▶│ DB Tier  │
   │ (Tier 1) │     │ (Tier 2) │     │ (Tier 3) │     │ (Tier 4) │
   └──────────┘     └──────────┘     └──────────┘     └──────────┘
                       HTTP              gRPC             SQL
                    (network)          (network)        (network)
```

## 9.3 Detailed Comparison Table

| Aspect | Layered | N-Tier |
|---|---|---|
| **Separation type** | **Logical** (in same deployment) | **Physical** (across machines) |
| **Communication** | In-process function calls | Network calls (HTTP, RPC, gRPC) |
| **Latency** | Microseconds | Milliseconds |
| **Scalability** | Whole app scales together | Each tier scales independently |
| **Performance** | Faster (no network) | Slower (network latency) |
| **Cost / Infrastructure** | Lower | Higher (more servers, network) |
| **Complexity** | Lower | Higher |
| **Security isolation** | Less | Better (per-tier firewalls) |
| **Fault isolation** | Less | Better (tier failures isolated) |
| **Deployment** | Single unit | Multiple units, possibly different schedules |
| **Examples** | Desktop apps, classic web apps | Modern web apps, enterprise systems |

## 9.4 Similarities

- Both organise the system into **stacked layers**.
- Both enforce **strict layer-to-layer communication** (only call layer below, no skipping).
- Both promote **separation of concerns**.
- Both face the **"architecture sinkhole" anti-pattern** (requests passing through layers without doing real work).

## 9.5 Real-World Examples

### Pure Layered (logical):
- **Classic desktop apps** — Microsoft Excel (UI / Logic / Data layers in one process).
- **Mobile apps** — iOS/Android apps with clear UI / ViewModel / Repository layers.
- **A small Spring Boot application** running on one server with HSQLDB in-memory.

### N-Tier (physical):
- **Classic 3-tier web apps** — Apache (web tier) + Tomcat (app tier) + MySQL (data tier), often on separate servers.
- **Enterprise applications** — Browser → CDN → Load Balancer → Web Servers → App Servers → Cache (Redis) → DB.
- **AWS reference architectures** — Route 53 → CloudFront → ALB → EC2 (web) → EC2 (app) → RDS.

## 9.6 Real-World Scenario

> *Netflix's video streaming used to be a monolith with logical layers (Layered architecture). When they migrated to AWS in 2008, they kept the layered structure but spread it across multiple tiers: client → ELB → API gateway → microservices → caches → databases — all on different EC2 instances across availability zones. This is N-Tier architecture in the cloud era.*

> *Conversely, a simple Spring Boot CRUD app you build in your final year project — with Controllers, Services, and Repositories all in one JAR running on Tomcat — is a Layered architecture, not N-Tier, even though it has all three layers.*

## 9.7 Exam Answer Template — Q3.6 (4 marks)

> ***Layered Architecture** organises related functions into horizontal layers stacked on top of each other, where each layer can only communicate with itself or layers below it. It enforces **logical separation** within a single deployment unit, and components communicate via in-process function calls.*
>
> ***N-Tier Architecture** is an **extension of Layered architecture** where each layer is deployed on a **different physical location** (separate machines or processes). Components communicate via network protocols (HTTP, RPC, gRPC).*
>
> ***Similarities:** both stack functions into layers, both enforce strict layer-to-layer communication (call only the layer below), and both promote separation of concerns. Every N-Tier architecture is therefore Layered at heart.*
>
> ***Differences:** Layered is **logical** separation (one deployment), N-Tier is **physical** distribution (multiple deployments). Layered offers faster communication (in-process), simpler deployment, and lower cost — but cannot scale layers independently. N-Tier allows independent scaling per tier, better security/fault isolation, and supports distributed teams — but incurs network latency, higher infrastructure cost, and operational complexity.*
>
> ***Example:** A Spring Boot app with Controllers/Services/Repositories in one JAR is Layered. Browser → Load Balancer → Web Servers → App Servers → Database on separate EC2 instances is N-Tier.*

**Full 4-mark answer.** ✅

---

<a name="10"></a>
# 10. Cloud Architecture + IaaS/PaaS/SaaS (Q3.4 — 4 marks!)

## What is Cloud Architecture?

> **Cloud Architecture** is an architectural style that enables access to a **shared pool of computing resources** that can be **rapidly provisioned** to new consumers, allowing the business to focus on its core business instead of infrastructure.

## 10.1 Key Characteristics of Cloud

1. **On-demand self-service** — provision resources without human intervention.
2. **Broad network access** — accessible from anywhere over the network.
3. **Resource pooling** — multi-tenancy; shared infrastructure.
4. **Rapid elasticity** — scale up or down quickly.
5. **Measured service** — pay only for what you use.

## 10.2 The 3 Cloud Service Models ⭐⭐⭐

```
            More control ◄──────────────────────────► Less effort
              ┌───────┐    ┌────────┐    ┌────────┐
   On-prem ── │ IaaS  │ ── │ PaaS   │ ── │ SaaS   │
              └───────┘    └────────┘    └────────┘
              VMs only    Platform     Whole App
              You manage:    │            │
              everything     │            │
                          You manage:     │
                          App + data      │
                                      You manage:
                                      Just data + config
```

### IaaS (Infrastructure-as-a-Service)
> Provides virtual machines, storage, and network. You manage OS, runtime, applications, and data.

- **You get:** VMs, virtual networks, block storage, object storage, load balancers.
- **You manage:** Operating system, runtime, middleware, apps, data.
- **Cloud provider manages:** Hardware, virtualisation, datacentre, networking.

#### Pros
- Maximum **control and flexibility**.
- Familiar OS environment.
- Can run any application — even legacy ones.
- **Lift-and-shift** migration is easiest.

#### Cons
- **Most management burden** — you patch, secure, scale.
- Requires sysadmin expertise.
- Manual scaling unless you build automation.

#### Real Examples
- **AWS EC2** (Elastic Compute Cloud)
- **Microsoft Azure Virtual Machines**
- **Google Compute Engine**
- **DigitalOcean Droplets**

#### Real-World Scenario
> *A traditional Java application running on Tomcat + Oracle DB on bare metal. To move to the cloud cheaply, the team uses IaaS: spin up EC2 instances, install Tomcat, restore Oracle from backups. Same architecture, just on rented hardware. No app changes needed. Total cloud migration time: 2 weeks.*

### PaaS (Platform-as-a-Service)
> Provides a **managed platform/runtime** to run your code. You bring the code; the platform handles everything else.

- **You get:** Managed runtime (e.g., Node.js, Python, Java), managed databases, managed message queues.
- **You manage:** Your application code and your data.
- **Cloud provider manages:** OS, runtime, middleware, hardware, scaling.

#### Pros
- **Faster development** — no infrastructure setup.
- **Auto-scaling** built in.
- No OS patching, no infra management.
- Focus on business logic.

#### Cons
- **Less control** over the environment.
- **Vendor lock-in** to platform APIs.
- Limited to supported runtimes and languages.
- Can be expensive at scale.

#### Real Examples
- **Heroku** — push code, it runs.
- **AWS Elastic Beanstalk**
- **Google App Engine**
- **Azure App Service**
- **AWS Lambda** (FaaS — a subset of PaaS).

#### Real-World Scenario
> *A startup builds a Node.js app and deploys to Heroku. They focus 100% on features. Heroku handles OS, runtime, scaling, logging, monitoring. Total infrastructure setup time: 30 minutes. Trade-off: when they hit 100k users, their Heroku bill is much higher than equivalent IaaS — at which point they may consider migration.*

### SaaS (Software-as-a-Service)
> Provides a **complete application** delivered over the web. You just use it.

- **You get:** A working application.
- **You manage:** Just your data and configuration within the app.
- **Cloud provider manages:** Everything — infrastructure, application code, updates.

#### Pros
- **Zero installation**.
- **Always up-to-date** — provider pushes updates.
- **Minimum cost to start** — often free tier.
- **Predictable subscription pricing**.

#### Cons
- **Least customisation** — you live within the app's features.
- **Data lives with the provider** (security/privacy concerns).
- **Internet-dependent**.
- Can't access raw data easily.

#### Real Examples
- **Gmail / Google Workspace**
- **Microsoft Office 365**
- **Salesforce CRM**
- **Slack, Zoom, Dropbox**
- **Notion, GitHub, Atlassian Jira**

#### Real-World Scenario
> *A small accounting firm doesn't want to maintain email servers. They subscribe to Office 365 (SaaS). For $10/user/month, they get Outlook, Word, Excel, Teams, OneDrive — all maintained by Microsoft. They never patch a server, never worry about backups. They lose the ability to host emails on-premise — that's the trade-off.*

## 10.3 The Spectrum

```
   Bare Metal      IaaS         PaaS         SaaS
   ────────       ────         ────         ────
   You do         You skip      You only     You only
   EVERYTHING    hardware      do code +    USE
                 only          data         the app
```

## 10.4 Cloud Architecture Pros & Cons (Q3.4 also asks)

### Advantages of Cloud Architecture
1. **Elasticity** — scale up and down on demand
2. **Pay-as-you-grow** — no upfront capital expense
3. **Global reach** — deploy worldwide in minutes
4. **Reduced complexity** — managed services for DBs, queues, ML
5. **Faster time-to-market** — no procurement delays
6. **Resilience** — multi-region, multi-AZ deployments

### Disadvantages of Cloud Architecture
1. **Security concerns** — your data lives with a third party
2. **Vendor lock-in** — proprietary APIs (Lambda, Cosmos DB, etc.)
3. **Compliance challenges** — data residency, GDPR, HIPAA
4. **Cost surprises** — can balloon without governance
5. **Internet dependency** — outages affect everyone
6. **Less control** over underlying infrastructure

## 10.5 Real-World Cloud Examples

### Big Companies on Cloud
- **Netflix** — entirely on AWS (used to run their own datacentres).
- **Spotify** — Google Cloud Platform.
- **Dropbox** — was on AWS, then built their own datacentres ("Magic Pocket" — reverse cloud migration at scale).
- **Airbnb** — AWS-heavy.

### Multi-Cloud Strategies
- **Apple** — uses AWS, Google Cloud, and Microsoft Azure to avoid lock-in.
- **NASA** — multiple cloud providers for different workloads.

## 10.6 Exam Answer Template — Q3.4 (4 marks)

**Q3.4 2025: "Explain Cloud Architecture style and describe the advantages and disadvantages of its different service offerings."**

> ***Cloud Architecture** is an architectural style that enables access to a **shared pool of computing resources** that can be rapidly provisioned on demand, allowing organisations to focus on their core business instead of infrastructure. It supports **multi-tenancy**, **elastic scaling**, and **pay-as-you-grow** pricing.*
>
> ***The 3 service offerings are:***
>
> ***IaaS (Infrastructure-as-a-Service)** — provides virtual machines, storage, and networking. Examples: AWS EC2, Azure VMs. **Advantages:** maximum control + flexibility; familiar OS environment; supports any application including legacy. **Disadvantages:** most management burden (patching, scaling, securing); requires sysadmin expertise.*
>
> ***PaaS (Platform-as-a-Service)** — provides a managed runtime/platform; you bring just the code. Examples: Heroku, AWS Elastic Beanstalk, Google App Engine. **Advantages:** faster development; built-in auto-scaling; no infrastructure management. **Disadvantages:** less control; vendor lock-in to platform APIs; limited to supported runtimes.*
>
> ***SaaS (Software-as-a-Service)** — provides a complete application; you just use it. Examples: Gmail, Salesforce, Office 365. **Advantages:** zero installation; always up-to-date; minimum cost to start; predictable subscription pricing. **Disadvantages:** least customisation; data lives with provider (security/compliance risk); internet-dependent.*
>
> *As you move from IaaS → PaaS → SaaS, you trade **control** for **convenience**.*

**Full 4-mark answer.** ✅

---

<a name="11"></a>
# 11. Drawing & Critiquing Block Diagrams (Q1.6 & Q4.a.v!)

Architecture exams almost always include a diagram question. The 2025 Q1.6 asked for a **6-mark block diagram** of an architecture. Q4.a.v asked you to **critique a given diagram** for 6 marks.

## 11.1 What is a Block Diagram?

> A **block diagram** shows the **high-level components** of a system and how they **communicate**. Boxes represent components/services/databases; arrows represent communication.

## 11.2 The 7 Rules of Drawing Great Block Diagrams ⭐

### Rule 1 — Label EVERY box
Don't draw "Server 1". Draw "Authentication Service" or "Product Catalog API".

### Rule 2 — Label EVERY arrow with the protocol
This is the biggest mark-earner. Examples:
- `REST/JSON over HTTPS`
- `gRPC`
- `Kafka events`
- `SQL`
- `WebSocket`
- `AMQP`

### Rule 3 — Show direction of communication
Arrows should be **directional** (→) showing who initiates calls.

### Rule 4 — Group logically related components
Use boxes/containers to group services by domain or tier.

### Rule 5 — Show data stores explicitly
Use cylinder shapes for databases, with labels like "PostgreSQL (Users)", "Redis (Cache)".

### Rule 6 — Include the client(s)
Most architectures serve users — show the browser/mobile app/IoT device on the left.

### Rule 7 — Show external systems
If you integrate with third-party APIs (Stripe, Twilio), draw them as external boxes.

## 11.3 A Worked Example — E-Commerce Microservices

```
   ┌──────────┐     ┌──────────┐     ┌─────────────────┐
   │  Browser │────▶│ CDN      │────▶│  API Gateway    │
   │ (mobile/ │HTTPS│(Cloudflare)│ HTTPS│  (auth/rate    │
   │  web)    │     │          │     │   limit/route)  │
   └──────────┘     └──────────┘     └────────┬────────┘
                                              │ REST/JSON
                            ┌─────────────────┼─────────────┬─────────────┐
                            ▼                 ▼             ▼             ▼
                    ┌──────────────┐  ┌─────────────┐ ┌──────────┐ ┌────────────┐
                    │   Catalog    │  │    Cart     │ │ Payment  │ │  Notifi-   │
                    │   Service    │  │   Service   │ │ Service  │ │  cations   │
                    └──────┬───────┘  └─────┬───────┘ └────┬─────┘ └─────┬──────┘
                           │ SQL            │ SQL          │ gRPC        │ SMTP/Push
                           ▼                ▼              ▼             ▼
                    ┌────────────┐  ┌──────────────┐ ┌──────────┐  External: Stripe
                    │ PostgreSQL │  │  PostgreSQL  │ │  Stripe  │  (Payments) + FCM
                    │ (Catalog)  │  │   (Carts)    │ │   API    │  (Push)
                    └────────────┘  └──────────────┘ └──────────┘
                           ▲                ▲              │
                           │                │              │
                           └────────────────┴──────────────┘
                                            │ Kafka events
                                            ▼
                                    ┌────────────────┐
                                    │  Event Bus     │
                                    │   (Kafka)      │
                                    └────────┬───────┘
                                             │
                                  ┌──────────┴──────────┐
                                  ▼                     ▼
                          ┌──────────────┐      ┌──────────────┐
                          │  Analytics   │      │ Recommen-    │
                          │    Service   │      │ dations Svc  │
                          └──────────────┘      └──────────────┘
```

### Description for the diagram (always include 2–4 lines!):
> *The architecture follows a microservices style behind an API Gateway. The Gateway centralises authentication, rate limiting, and request routing. Each business domain (Catalog, Cart, Payment, Notifications) has its own service with its own data store, communicating with the Gateway via REST/JSON over HTTPS. Asynchronous events flow through Kafka, allowing decoupled services like Analytics and Recommendations to react without coupling to the main request path. External integrations (Stripe for payments, FCM for push notifications) are isolated to specific services.*

## 11.4 How to Critique a Given Architecture (Q4.a.v Style)

When the exam shows you a diagram and asks you to critique it, look for these **8 anti-patterns**:

### Anti-Pattern 1 — Single Point of Failure
**Symptom:** Only one instance of a critical component.
**Suggest:** Add redundancy / load balancer / active or passive failover (Availability tactics).

### Anti-Pattern 2 — No Caching
**Symptom:** All read requests hit the database.
**Suggest:** Add Redis/CDN for hot data (Performance tactic: Maintain Multiple Copies).

### Anti-Pattern 3 — Public Access to Critical Features
**Symptom:** No authentication module between client and sensitive services.
**Suggest:** Add API Gateway with auth, or separate authenticated module (Security tactic: Authenticate Users).

### Anti-Pattern 4 — Missing CDN for Read-Heavy Content
**Symptom:** All static content (images, thumbnails) served by origin.
**Suggest:** CDN at the edge (especially when read frequency >> write frequency).

### Anti-Pattern 5 — No Fault Detection
**Symptom:** No heartbeat / health checks between components.
**Suggest:** Heartbeat or Ping-Echo (Availability tactic).

### Anti-Pattern 6 — Synchronous Heavy Operations
**Symptom:** User waits for analytics, notifications, recommendations in their main request.
**Suggest:** Message bus / Pub-Sub for async processing.

### Anti-Pattern 7 — Single Database for All Services
**Symptom:** All services share one DB.
**Suggest:** Split DB by domain / quantum (each service owns its data).

### Anti-Pattern 8 — Coupling Through Direct Service-to-Service Calls
**Symptom:** Service A calls Service B which calls Service C which calls Service A (cyclic dependency).
**Suggest:** Decouple via events; introduce a gateway / mediator.

## 11.5 Real Q4.a.v 2025 Example — Photo Site Critique

The given diagram showed a **single server** with both the Uploader (authenticated) and the Public Consumer modules sharing the same large photo storage, with no caching, no CDN, no separation.

### Critique:

> *The given architecture has several significant weaknesses:*
>
> *1. **Single point of failure** — only one server hosts both the Uploader and Consumer modules. Any failure brings down both functions. **Suggestion:** Deploy on multiple servers behind a load balancer with active or passive redundancy.*
>
> *2. **No caching for thumbnails** — given that thumbnail views are 10,000× more frequent than large photo views, serving them from origin every time wastes server resources and increases latency. **Suggestion:** Add a CDN (e.g., CloudFront, Cloudflare) at the edge for thumbnails, with origin as fallback. This applies the Performance tactic 'Maintain Multiple Copies'.*
>
> *3. **No separation between Uploader and Consumer modules** — they share the same server, meaning a spike in public traffic could degrade upload performance for authenticated users, and vice versa. **Suggestion:** Deploy them on separate scaling groups (separate quanta), since their quality attributes differ (Uploader needs security + transactional integrity; Consumer needs high availability + read performance).*
>
> *4. **No fault detection / failover mechanism** — if the server crashes, users see a complete outage. **Suggestion:** Add health checks (Ping/Echo) + automatic failover to a standby (Passive Redundancy).*
>
> *5. **No protection against DDoS or abuse on the public Consumer endpoint** — the read-only HTTP endpoint is exposed to the internet directly. **Suggestion:** Add rate limiting at an API Gateway, or use a CDN that includes DDoS protection (Cloudflare, AWS Shield).*
>
> *6. **No clear handling of large photo storage** — large photos hit the same disk as everything else. **Suggestion:** Use object storage (S3) for large photos, with the CDN pulling from S3.*

That's a **6-mark answer** that names specific anti-patterns and provides concrete suggestions tied to architectural tactics.

## 11.6 Universal Diagram Template You Can Adapt

For ANY case study, your block diagram should at minimum include:

1. **Client(s)** on the left (browser, mobile, IoT, third-party)
2. **Edge layer** — CDN or API Gateway
3. **Application services** — your business logic
4. **Data stores** — databases, caches
5. **Message bus** if async needed
6. **External integrations** — third-party APIs
7. **Cross-cutting concerns** — logging/monitoring service (optional but impressive)

## 11.7 Block Diagram Drawing Checklist (use in exam!)

- [ ] Every box has a clear name
- [ ] Every arrow has a labelled protocol
- [ ] Direction of every arrow is shown
- [ ] Data stores are visible (cylinder shapes)
- [ ] Client(s) are shown on the left
- [ ] External systems are clearly outside the main system
- [ ] Logical grouping of related services
- [ ] A 2-4 line description below the diagram
- [ ] (Bonus) Show fault tolerance — load balancers, redundant instances
- [ ] (Bonus) Show edge layer (CDN, API Gateway)

---

# Final Reminders & Master Cheat Sheet

## The 11 Topics Recap

1. ✅ **Architectural Styles** — Mono / Mod-Mono / Event-Driven / Microkernel / Microservices
2. ✅ **Quality Attributes** — AIMPRRSSTU + 3 trade-off pairs + ISO 25010
3. ✅ **ABC** — 4 influences, 5 ramifications, feedback loop
4. ✅ **7 Activities** — B-U-C-D-A-I-C
5. ✅ **QAS** — SSAERR 6-part template, ALWAYS include a NUMBER
6. ✅ **Tactics** — DRP (Availability), DMA (Performance), LPD (Modifiability), RDR (Security)
7. ✅ **4+1 View Model** — LDPP + Scenarios
8. ✅ **SAAM** — SDECE 5-step + Direct vs Indirect scenarios
9. ✅ **N-Tier vs Layered** — Physical vs Logical
10. ✅ **Cloud + IaaS/PaaS/SaaS** — Control vs Convenience spectrum
11. ✅ **Block Diagrams** — Label everything, 7 rules, 8 critique anti-patterns

## The Universal Exam Formula

For ANY case-study question:

1. **Identify FRs and NFRs** from the brief.
2. **Pick 2-3 dominant QAs** with explicit justification.
3. **Match QAs to architectural styles** (use the Big-5 comparison).
4. **Recommend ONE style** + name 2-3 explicit trade-offs you accept.
5. **Draw a labelled block diagram** (every arrow's protocol named!).
6. **Mention evolution path** if relevant (Stack Overflow → Uber → DOMA arc).
7. **Quote a real-world example** (Netflix, Uber, Stack Overflow, Spotify) for credibility.

## Final Exam-Day Tips

- ⏰ **10-min reading time** — plan Q1 (the biggest case study)
- 📝 **30 min per question** with 5-10 min buffer
- 🔢 **Always include numbers** in Response Measures
- 🏷️ **Label every arrow's protocol** in diagrams
- 💬 **Use precise vocabulary** — "architecture quantum", "eventual consistency", "Conway's Law", "synchronous connascence"
- 🧠 **Quote real-world examples** — Netflix, Uber, Stack Overflow, Spotify, Boeing 737 MAX, Therac 25
- ⚖️ **Always state trade-offs** explicitly when recommending a style
- 🎯 **Tactics format:** Name + Mechanism + "This satisfies the QAS response measure of [X] by [mechanism]"

You've now mastered the 11 topics that will earn you ~95% of the marks. Good luck. 🍀🎓
