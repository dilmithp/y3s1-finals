# Lecture 09 — Architectural Patterns & Styles

**Module:** SE3030 — Software Architecture · 3rd Year, Semester 1 · SLIIT  
**Lecturer:** Chathura R De Silva

> ⚠️ **MASSIVELY EXAM-CRITICAL** — The 2025 paper Q1 (25 marks!) asked you to **compare 5 architectural styles** (Monolithic, Modular Monolithic, Event-Driven, Microkernel, Microservices) and pick one. Q3.4 asked about Cloud + service offerings. Q3.6 asked **N-Tier vs Layered**. This lecture is your toolkit. ☕

---

## What you should walk away knowing

1. What an **architectural style** is (and why it = "architectural pattern" in this course).
2. The full **menu of 19 styles** the lecture lists — and the **deep dive** on the most exam-critical ones.
3. For each style: **definition · key features · advantages · disadvantages · examples · when to use**.
4. The **N-Tier vs Layered** distinction (a guaranteed exam question).
5. **Cloud Architecture** + IaaS/PaaS/SaaS (Q3.4 of the past paper).
6. The big closing idea: **real systems combine multiple styles**.

> **Pro Tip:** The way to score top-band marks here is **comparing styles in tables** with concrete examples. Don't just say "Microservices is good for scaling" — say "**Netflix uses Microservices because…**". Concrete examples = top marks.

---

## 1. What is an Architectural Style? ⭐

> **Definition:** *"An architectural style — sometimes called an architectural pattern — is a set of **principles** that shapes an application, a system, or a system of systems."*

It improves **partitioning** and promotes **design reuse** by providing solutions to **frequently recurring problems**.

It also provides a **common language** to discuss systems — usually **independent of specific technologies/frameworks** (Java, .NET, etc.) — so architects can have higher-level conversations.

> **Memory Hook:** *"A style is a recipe; a system is the dish."* The same recipe (style) can be cooked with different ingredients (technologies).

> **Note:** In this course, *"style"* and *"pattern"* are used **interchangeably** — but in some books a **style** is the higher-level shape (e.g., Microservices) and a **pattern** is the named technique (e.g., Circuit Breaker). Don't lose marks splitting hairs.

---

## 2. The Full Menu of Architectural Styles (slide 3)

The lecture lists **19 styles**. You don't need to memorise *all* of them in detail, but you should **recognise them** and know the **deep-dive ones** cold.

```
   1. Monolithic              11. Microservice
   2. Client-Server           12. Peer-to-Peer
   3. Component-based         13. Rule-based
   4. Layered                 14. Service Oriented (SOA)
   5. N-Tier                  15. Message Bus
   6. Object Oriented         16. Pipe and Filter
   7. Blackboard              17. REST
   8. Event Driven            18. Publish-Subscribe
   9. Domain Driven           19. Cloud
   10. Plugin (Microkernel)
```

The lecture **deep-dives** into the bolded ones below. Memorise these:

```
   ⭐ Client-Server     ⭐ Component-based   ⭐ Layered          ⭐ N-Tier
   ⭐ Object Oriented   ⭐ Pipe and Filter   ⭐ Publish-Subscribe
   ⭐ SOA               ⭐ Message Bus       ⭐ Microservices    ⭐ Cloud
   ⭐ Domain Driven
```

Plus from **Lecture 4**, you already know **Monolithic**, **Modular Monolithic**, **Event-Driven**, **Microkernel** — all of which appeared in 2025 Q1!

---

## 3. The Style-by-Style Guide ⭐⭐

For each style: definition · key features · pros · cons · examples · when to use.

> **Universal exam template per style:**  
> *"[Style] is [definition]. Its key features are [list]. It is well-suited when [when to use]. Examples include [system]. The main pros are [...] and the main cons are [...]."*

---

### 3.1 Client-Server Architecture

**Definition:** A **server** provides functions/data/content to one or more **clients**.

**Key features:**
- **Centralised** — one (or few) servers, many clients.
- The **client knows how to locate the server** (URL, IP).
- Connection over **HTTP, RPC, sockets**, etc.

**Examples:** Outlook → Exchange Server (SMTP/POP) · Gmail → Google's mail servers (HTTP).

**Advantages:**
- **Centralised security** (one place to lock down).
- Easier to back up the central server.

**Disadvantages:**
- **Single point of failure** (the server).
- **Maintenance / downtime** issues.

**When to use:** Centralised data, modest scale, clear client-server separation (e.g., traditional web apps).

---

### 3.2 Component-based Architecture

**Definition:** Build the system from **reusable, self-contained components** with well-defined interfaces.

**Key features:**
- Emphasises **separation of concerns**.
- Components are **highly cohesive + loosely coupled**.
- Components are **substitutable**.

**Examples:** Java `.jar` files · Windows `.dll` files · React UI components.

**Advantages:**
- **Reusability** (lowers dev cost).
- **Extendability** (each component can be tuned independently).

**Disadvantages:**
- Managing a **large component base** can become hard (versioning, integration).

**When to use:** Building product families, UI frameworks, anywhere reuse pays off.

---

### 3.3 Layered Architecture ⭐

**Definition:** Group related functions into **horizontal layers stacked on top of each other**.

**Key features:**
- A layer **only communicates with itself or layers below it**.
- Promotes **separation of concerns**.

**Classic example layers:**
```
   ┌─────────────────────────┐
   │  Presentation Layer     │  ← UI, controllers
   ├─────────────────────────┤
   │  Service Layer          │  ← business workflow orchestration
   ├─────────────────────────┤
   │  Business Logic Layer   │  ← domain rules
   ├─────────────────────────┤
   │  Data Access Layer      │  ← DB queries
   └─────────────────────────┘
```

**Examples:** Classic enterprise web apps · TCP/IP stack.

**Advantages:**
- Many shared with Component-based.
- Can **extend to N-Tier** for distribution.

**Disadvantages:**
- Bottom layers **can't communicate with top** without **cyclic dependencies** (which break the model).
- Architecture **sinkhole** — many requests just pass through layers without doing real work.

**When to use:** Enterprise CRUD applications, structured environments.

---

### 3.4 N-Tier Architecture ⭐ (Q3.6 of past paper!)

**Definition:** **Layered architecture** where **each tier can run on a separate physical location**.

**Key features:**
- Each tier = **a deployable unit on its own machine**.
- "**N**" = the number of tiers (3-Tier is common: presentation, application, data).

**Examples:** Commercial web apps (browser → web server → app server → DB server).

**Advantages:**
- Inherits all advantages of Layered.
- **Can scale up** — multiple nodes per tier.
- Tiers that need more resources can be allocated more nodes independently.

**Disadvantages:**
- **Maintenance of multiple nodes** (more infrastructure to manage).
- **Data communication cost** (network calls between tiers).

**When to use:** Larger web applications needing physical separation for scalability and security.

### ⭐ N-Tier vs Layered — the GUARANTEED exam comparison (Q3.6 in 2025!)

| Aspect | **Layered** | **N-Tier** |
|---|---|---|
| **Separation type** | **Logical** (within same deployment) | **Physical** (across different machines/processes) |
| **Communication** | In-process function calls | Over the network (HTTP, RPC) |
| **Scalability** | Limited (whole app scales together) | Each tier can scale independently |
| **Deployment** | Single deployment unit | Multiple deployment units |
| **Performance** | Faster (no network) | Slower (network latency) |
| **Cost / complexity** | Lower | Higher (more infra) |
| **Security** | Less isolated | Better isolation per tier |
| **Examples** | A monolithic web app with UI/Service/DAL layers | A web app with separate web server + app server + DB server |

**Similarities:**
- Both organise the system into **stacked layers**.
- Both enforce **strict layer-to-layer communication** (only call the layer below).
- Both promote **separation of concerns**.

**Key difference:**
> **Every N-Tier architecture is layered, but not every layered architecture is N-Tier.**  
> Layered = logical structure. N-Tier = layered + physical distribution.

> **Pro Tip — exam phrase:** *"N-Tier extends Layered Architecture by allowing each tier to be deployed on different physical locations, enabling independent scaling at the cost of network communication overhead."*

---

### 3.5 Object Oriented Architecture

**Definition:** View the system as a set of **cooperating objects** that contain data + behaviour and exchange messages (method calls).

**Key features:**
- Components = **objects** (data + behaviour).
- Connectors = **messages** (method invocations via interfaces).
- 4 OOP principles: **Abstraction, Encapsulation, Inheritance, Polymorphism**.

**Examples:** Most modern applications.

**Advantages:**
- **Reusability**, **Extensibility**, **High cohesion**.
- Excellent **tool support** (UML, IDEs).

**Disadvantages:**
- **Speed** (overhead of object dispatch).
- **Effort** — short-term cost is higher than procedural code.

**When to use:** Most general-purpose enterprise software (the default style for the last 30+ years).

---

### 3.6 Pipe and Filter Architecture

**Definition:** Data flows through a sequence of independent **filters** connected by **pipes**.

**Key features:**
- **Filters** = transform input data → output data.
- **Pipes** = pass data between filters.
- Filters are **independent** — no shared state, no knowledge of upstream/downstream.

```
   [Source] → [Filter 1] → [Filter 2] → [Filter 3] → [Sink]
```

**Examples:**
- Unix shell pipelines (`cat file | grep pattern | sort | uniq`).
- **Compilers** (lexical analysis → parsing → semantic analysis → code generation).

**Advantages:**
- Easy to **add/remove filters**.
- **Concurrent execution** (each filter can be its own thread/process).

**Disadvantages:**
- **Performance** — may force a "lowest common denominator" on data transmission.
- **No filter cooperation** (they can't share state).

**When to use:** ETL pipelines, data transformation, compilers, image/audio processing.

---

### 3.7 Publish-Subscribe Architecture

**Definition:** **Subscribers** register/deregister to receive specific messages or content. **Publishers** broadcast messages to subscribers.

**Key features:**
- Can use **proxies / brokers** to manage distribution.
- Can be **topic-based** (subscribe to a topic) or **content-based** (subscribe to messages matching content filters).

**Examples:** Mobile push notifications (Google Cloud Messaging) · News alerts · Kafka topics.

**Advantages:**
- **Avoids polling** — saves bandwidth and power.
- Can use **queues / message buses** to manage delivery.
- **Highly scalable** (publishers and subscribers don't know each other).

**Disadvantages:**
- Mostly **one-way** communication.
- **Decoupling** can make debugging hard (who consumed which message?).

**When to use:** Real-time notifications, event broadcasting, IoT data fan-out.

---

### 3.8 Service Oriented Architecture (SOA)

**Definition:** Application functionality is provided as a set of **remote services** using **standard communication protocols** (often SOAP-based).

**Key features:**
- Services + clients are **independent of vendors, products, technologies**.
- Built on principles like:
  - **Autonomous** (services own their logic)
  - **Standard Service Contract** (well-defined interfaces, e.g., WSDL)
  - **Abstracted & Encapsulated**
  - **Distributable & Discoverable**

**Examples:** Many SOAP-based enterprise web services.

**Advantages:**
- **Interoperability** — integrate products built with different technologies.
- **Reusability** of services.
- **Widely adopted** with well-defined standards & tools.

**Disadvantages:**
- Requires **high availability** of all services.
- Heavyweight protocols (SOAP/XML overhead).

**When to use:** Large enterprise integration of legacy systems with strong central governance.

---

### 3.9 Message Bus Architecture

**Definition:** Systems communicate **asynchronously** by passing messages via a **common intermediary (the bus)**.

**Key features:**
- Widely used for **Enterprise Application Integration (EAI)**.
- Many SOA systems use **message-oriented middleware**.

**Examples:** Enterprise Service Bus implementations — JBoss ESB, Mule ESB, WSO2 ESB.

**Advantages:**
- **Extensibility** — easily add/remove apps from the bus.
- **Integrates different technologies** via standard protocols.
- **Highly scalable**.

**Disadvantages:**
- **Requires middleware** (the ESB itself becomes a complex piece of infrastructure).

**When to use:** Connecting many heterogeneous systems where async messaging suits the workflow.

---

### 3.10 Microservices Architecture ⭐⭐

**Definition:** Structures the system as a **collection of loosely coupled services**, decomposed into **small, cohesive computation units** using **lightweight protocols**.

**Key features:**
- Similar to SOA but **smaller, more focused services**.
- Lightweight communication (REST, gRPC, message brokers).
- Each service can be **independently deployed**.

**Examples:** Netflix, Twitter, Amazon (recall Lec 5!).

**Advantages:**
- **Lightweight protocols** allow thin clients.
- Supports **CI/CD** very well.
- **Easy to deploy & scale services independently**.
- **Fault isolation** — one service down doesn't kill the whole system.

**Disadvantages:**
- Maintenance requires **special DevOps skills**.
- **Increased network communication** within the system.
- **Operational complexity** explodes (recall Uber's tangled microservices in Lec 5!).

**When to use:** Large systems, multiple teams, differing scale/quality needs per feature, mature DevOps.

---

### 3.11 Domain Driven Architecture

**Definition:** Focus mainly on the **business domain** and the logic around it. Technical and domain experts collaborate closely.

**Key features:**
- Centred on the **ubiquitous language** (shared vocabulary).
- **Ontology** = knowledge representation of the domain.

**Examples:** Web Content Management Systems.

**Advantages:**
- **Easy for domain experts** to understand and contribute.

**Disadvantages:**
- For **larger teams**, the system can get **complex and disorganised**.

**When to use:** Complex business domains where deep domain modelling is critical (banking, insurance, healthcare).

---

### 3.12 Cloud Architecture ⭐ (Q3.4 of past paper!)

**Definition:** Enables access to a **shared pool of computing resources** that can be **rapidly provisioned** to a new consumer.

**Key features:**
- Lets the business **focus on its core business** instead of infrastructure.
- Supports **multi-tenancy** (multiple customers share infrastructure safely).
- **3 service models** — IaaS, PaaS, SaaS.

**Examples:** AWS-based systems, Salesforce.

**Advantages:**
- **Elasticity** — scale up and down on demand.
- **Pay as you grow** (operational expense vs capital expense).
- No upfront infrastructure investment.

**Disadvantages:**
- **Security concerns** — your data sits with a third party.
- **Vendor lock-in** can occur.

### ⭐ The 3 Cloud Service Models — IaaS / PaaS / SaaS (memorise!)

| Model | What you get | What you manage | What the cloud provider manages | Example |
|---|---|---|---|---|
| **IaaS** (Infrastructure-as-a-Service) | **Virtual machines, storage, network** | OS, runtime, apps, data | Hardware, virtualisation | **AWS EC2**, Azure VMs, Google Compute Engine |
| **PaaS** (Platform-as-a-Service) | **A managed platform/runtime** to run your code | Your app + data | OS, runtime, middleware, hardware | **Heroku**, AWS Elastic Beanstalk, Google App Engine |
| **SaaS** (Software-as-a-Service) | **A complete application** delivered over the web | Just your data + config | Everything else | **Gmail**, Salesforce, Office 365 |

```
            More control ◄──────────────────────► Less effort
              ┌───────┐    ┌────────┐    ┌────────┐
   On-prem ── │ IaaS  │ ── │ PaaS   │ ── │ SaaS   │
              └───────┘    └────────┘    └────────┘
              VMs only    Platform     Whole App
```

> **Memory Hook — "I rent the bricks, P rent the kitchen, S rent the meal."**  
> **IaaS** = renting the building blocks (VMs).  
> **PaaS** = renting a kitchen + appliances (you bring the recipe = code).  
> **SaaS** = renting a finished meal (you just consume).

**Pros & Cons of each:**

| Model | Pros | Cons |
|---|---|---|
| **IaaS** | Maximum control & flexibility · Familiar OS environment | Most management burden · You patch / secure / scale |
| **PaaS** | Faster development · Auto-scaling · No infra management | Less control · Vendor lock-in to platform APIs |
| **SaaS** | Zero installation · Always up-to-date · Minimum cost to start | Least customisation · Data lives with provider · Internet-dependent |

> **Pro Tip — exam:** *"Cloud Architecture lets organisations consume IT resources as services in 3 models: IaaS provides infrastructure (VMs), PaaS provides a managed runtime/platform, SaaS provides full applications. As you move from IaaS → PaaS → SaaS, you trade control for convenience."*

---

## 4. Combining Different Architectural Styles ⭐

> *"The overall architecture of a system is most often a **combination of multiple architectural styles**."*

Real example: A **Layered architecture combined with Object-Oriented design with Component-based deployment**, hosted on the **Cloud (PaaS)**.

**Factors that influence the combination:**
- **Knowledge / experience / capabilities** of the development team.
- **Organisational constraints** (e.g., data security policies vs cloud/SaaS adoption).

> **Memory Hook — "Real architectures are stews, not single-ingredient dishes."**

> **Pro Tip — exam framing:** When recommending an architecture in a case study, **don't pick one style and stop**. Say something like *"I recommend a Microservices architecture, with each service internally Layered, communicating via a Publish-Subscribe message bus, and deployed on PaaS."* This shows architectural maturity.

---

## 5. Master Comparison Table ⭐⭐⭐

This is your one-page revision sheet. Memorise this.

| Style | Type | Best for | Avoid when |
|---|---|---|---|
| **Client-Server** | Centralised | Traditional web apps; one DB to rule them all | High availability needs (single point of failure) |
| **Component-based** | Modular | Reusable libraries, UI frameworks | Tiny one-off applications |
| **Layered** | Logical layers | Enterprise CRUD apps | Real-time, event-heavy, distributed-deployment needs |
| **N-Tier** | Layered + physical distribution | Large web apps with scaling needs per tier | Latency-critical apps (network overhead) |
| **Object-Oriented** | Code organisation | Most general-purpose apps | Performance-extreme systems |
| **Pipe and Filter** | Data flow | ETL, compilers, processing pipelines | Interactive systems |
| **Publish-Subscribe** | Event-driven async | Notifications, IoT fan-out, event broadcasting | Strict request-response transactions |
| **SOA** | Service-based, heavy | Large enterprise integration | Small teams; agile startups |
| **Message Bus** | Async middleware | EAI; many heterogeneous systems | Simple two-app integrations |
| **Microservices** | Distributed services | Large systems, multiple teams, varied scale needs | Small teams, weak DevOps, unclear domain |
| **Domain-Driven** | Domain-centric | Complex business logic | Simple CRUD apps |
| **Cloud** | Resource model | Need elasticity, pay-as-you-go | Strict on-premises data residency |
| **Monolithic** (Lec 4) | Single deployment | Small teams, simple domain | Independent scaling needed |
| **Modular Monolithic** (Lec 4) | Single deployment + modules | Stepping stone; medium teams | Need fully independent deployment |
| **Event-Driven** (Lec 4) | Async event flow | Real-time reactivity, multiple consumers per event | Need strict ACID consistency |
| **Microkernel** (Lec 4) | Core + plugins | Customer-customisable products | No real plug-in variability |

---

## 6. Quality Attribute Cheat Sheet — Style Selection ⭐

| Quality Attribute Priority | Best Style |
|---|---|
| **Performance** (latency, throughput) | Monolithic / Layered (in-process is fastest) |
| **Scalability** (per service) | Microservices, N-Tier |
| **Availability** (no downtime) | Microservices + Active Redundancy |
| **Modifiability / Extensibility** | Microkernel (plugins), Component-based |
| **Reusability** | Component-based, SOA |
| **Real-time reactivity** | Event-Driven, Publish-Subscribe |
| **Distributed integration** | SOA, Message Bus |
| **Cost optimisation / Elasticity** | Cloud (PaaS, SaaS) |
| **Simplicity** (small team, fast delivery) | Monolithic, Modular Monolithic |
| **Customisation per customer** | Microkernel |
| **Domain modelling** | Domain-Driven |
| **Data transformation pipeline** | Pipe and Filter |

> **Pro Tip — exam case-study trick:** Match the **dominant quality attribute(s)** in the case study to the style in this table. Half the work is done.

---

## 7. One-Shot Summary (the morning of the exam)

> An **architectural style** (= **pattern** in this course) is a set of **principles** that shapes a system, providing solutions to recurring problems and a common vocabulary across teams. The lecture covers **19 styles**, with deep dives on the most common: **Client-Server** (centralised), **Component-based** (reusable substitutable parts), **Layered** (logical stacked layers), **N-Tier** (Layered + physical distribution — *every N-Tier is Layered, not vice versa*), **Object-Oriented** (cooperating objects, 4 OOP principles), **Pipe and Filter** (data flowing through stateless filters), **Publish-Subscribe** (subscribers register, publishers broadcast), **SOA** (services with standard contracts, heavyweight), **Message Bus** (async communication via central intermediary), **Microservices** (small, lightweight, independently deployable services), **Domain-Driven** (domain-centric collaboration), and **Cloud Architecture** (shared resource pool, with **3 service models: IaaS, PaaS, SaaS** — trading control for convenience). From Lecture 4: **Monolithic, Modular Monolithic, Event-Driven, Microkernel**. **Real-world systems combine multiple styles** — e.g., Microservices internally Layered, communicating via Pub-Sub, deployed on PaaS. **Style selection is driven by the dominant quality attributes** of the system. **N-Tier vs Layered**: Layered is *logical*, N-Tier is *physical distribution* of layers across machines.

---

## 8. Likely Exam Questions (and how to answer)

**Q1. Define an architectural style. List 5 common styles.**  
→ Definition (recurring solution + common language). List 5 from the menu, briefly describe each.

**Q2. Compare N-Tier and Layered architecture.** ⭐ (2025 Q3.6!)  
→ Use the comparison table in section 3.4. Highlight: **logical vs physical** as the killer difference.

**Q3. Explain Cloud Architecture. Describe IaaS, PaaS, and SaaS with pros/cons.** ⭐ (2025 Q3.4!)  
→ Definition + diagram of the spectrum + the IaaS/PaaS/SaaS table from section 3.12.

**Q4. Compare Monolithic, Modular Monolithic, Event-Driven, Microkernel, and Microservices for a given case study.** ⭐ (2025 Q1!)  
→ Build a 5×N table (5 styles × N quality attributes). Use the master quality-attribute selection table in section 6.

**Q5. Why are real architectures often combinations of multiple styles?**  
→ Different parts of the system have different quality needs; team experience and organisational constraints push toward hybrids. Give an example.

**Q6. Differentiate between SOA and Microservices.**  
→ SOA = larger services + heavyweight protocols (SOAP) + ESB · Microservices = small, focused, lightweight protocols (REST/gRPC) + decentralised. Recall Lec 5 (Uber's DOMA).

**Q7. Explain Publish-Subscribe with an example.**  
→ Definition + topic-based vs content-based + example (mobile push notifications). Pros/cons.

---

## 9. Vocabulary You Should Use Confidently

- **Architectural style / pattern** — recurring solution to architectural problems.
- **Tier** — physical deployment unit.
- **Layer** — logical grouping of related functions.
- **Client / Server** — requester / provider in client-server.
- **Cohesion / Coupling** — internal unity / external connections (recall Lec 4).
- **Component / Connector** — runtime building blocks (recall Lec 3).
- **Filter / Pipe** — pipe-and-filter elements.
- **Topic / Content-based subscription** — publish-subscribe variants.
- **ESB (Enterprise Service Bus)** — middleware for message-bus architecture.
- **WSDL / SOAP** — SOA service description and protocol.
- **REST / gRPC** — lightweight microservices protocols.
- **Multi-tenancy** — multiple customers sharing infrastructure safely.
- **IaaS / PaaS / SaaS** — cloud service models.
- **Elasticity** — auto-scale up/down on demand.

---

## 10. References

- Mark Richards — *Software Architecture Patterns* (free O'Reilly book).
- Microsoft Application Architecture Guide — https://msdn.microsoft.com/en-us/library/ee658117.aspx
- Taylor & Medvidovic — *Software Architecture: Foundations, Theory, and Practice*.

---

**Pro Tip — connections to previous lectures and past paper:**

- **Lec 1** (SQDP) → **architectural style is the "S" — Structure**.
- **Lec 4** (Monolith vs Distributed) → all styles fit into one of these two camps.
- **Lec 5** (Real World) → Stack Overflow (monolith), Uber (microservices → DOMA) — these are case studies *of these styles*.
- **Lec 6/7/8** (Quality Attributes / QAS / Tactics) → the QAs **drive** which style you pick.
- **2025 Q1** asked you to compare 5 styles — use the master table in section 5.
- **2025 Q3.4** asked about Cloud + service offerings — use section 3.12.
- **2025 Q3.6** asked N-Tier vs Layered — use section 3.4 comparison table.

Send Lecture 10 (Architecture Evaluation — SAAM!) when you're ready. SAAM was a 4-mark direct question in 2025 (Q3.5), so it's the next high-priority lecture. 🚀
