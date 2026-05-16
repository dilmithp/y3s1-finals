# Lecture 08 — Quality Attribute Tactics

**Module:** SE3030 — Software Architecture · 3rd Year, Semester 1 · SLIIT  
**Lecturer:** Chathura R De Silva

> ⚠️ **CRITICAL EXAM LECTURE** — The 2025 paper (Q4.a.ii and Q4.a.iv) asked you to *"Propose a tactic and describe how you can improve [Availability/Performance]"*. So this lecture pairs directly with QAS — first you **specify** the quality requirement (Lec 7), then you **achieve** it with tactics (this lecture). Memorise the menu of tactics for at least Availability and Performance. ☕

---

## What you should walk away knowing

1. What an **architectural tactic** is and how it differs from a pattern.
2. The **6 tactic categories** organised by quality attribute:
   - **Availability** (Fault Detection / Recovery / Prevention)
   - **Modifiability** (Localize / Prevent Ripple / Defer Binding)
   - **Performance** (Resource Demand / Management / Arbitration)
   - **Security** (Resisting / Detecting / Recovery from Attacks)
   - **Testability** (Input-Output / Internal Monitoring)
   - **Usability** (Runtime / Design Time)
3. **Concrete tactic names** you can confidently quote in the exam (Heartbeat, Voting, Active Redundancy, Caching, Authentication, etc.).
4. How to **propose a tactic** for a given quality attribute requirement.

---

## 1. What is a Tactic? ⭐

> **Definition:** *"An **architectural tactic** is a means of satisfying a **quality attribute response measure** by manipulating some aspect of a **quality attribute model** through architectural decisions."*

In plain English:
- Quality requirement = "I want the system to be available."
- **Tactic** = "I'll add **redundant servers + heartbeats**."

A **tactic is a planned, named way to achieve a quality goal**. Each tactic is a **design option** for the architect.

> **Memory Hook — "Goal vs How"**  
> **QAS** (Lec 7) = **Goal** ("system must be 99.99% available")  
> **Tactic** (this lec) = **How** ("use heartbeat detection + active redundancy")

### Tactic vs Pattern (key distinction!)

| | Tactic | Pattern |
|---|---|---|
| Granularity | **Single design decision** for one quality goal | **Larger structure** that bundles many tactics |
| Example | "Use Heartbeat for fault detection" | "Use the Microservices pattern" (which itself uses many tactics) |
| Reusability | Reusable across many architectures | Reusable but heavier-weight |

> **Key takeaway:** *"Patterns package tactics."* A single pattern (e.g., Layered Architecture, Microkernel) typically implements **multiple tactics** at once. This makes architectural analysis tricky — but useful, because choosing one good pattern gets you many tactics for free.

> **Pro Tip — exam phrase:** *"A collection of tactics forms an architectural strategy."*

---

## 2. The Tactics Framework — A Mental Model ⭐

For each quality attribute, tactics are organised as a **hierarchy** (a "framework"). All frameworks follow the same shape:

```
                        ┌────────────────┐
                        │  QUALITY GOAL  │
                        └────────────────┘
                                │
                ┌───────────────┼───────────────┐
                ▼               ▼               ▼
            Category 1      Category 2      Category 3
           (sub-goal)      (sub-goal)      (sub-goal)
                │
        ┌───────┼───────┐
        ▼       ▼       ▼
     Tactic  Tactic  Tactic     (specific named techniques)
```

So when answering an exam question, you can:
1. **Name the category** (e.g., "Fault Detection")
2. **Name the specific tactic** (e.g., "Heartbeat")
3. **Describe how it satisfies the QAS response measure**

That's a perfect tactic answer — and it earns full marks.

---

## 3. Availability Tactics ⭐⭐ (the most exam-tested!)

### The big idea
> A **fault** (or combination of faults) has the potential to cause a **failure**, which would affect availability.  
> Availability tactics **keep faults from becoming failures**, or at least **bound the effects** of the fault and **make repair possible**.

### The 3 categories of Availability tactics

```
                        ┌─────────────────┐
                        │   AVAILABILITY  │
                        └─────────────────┘
                                │
                ┌───────────────┼─────────────────┐
                ▼               ▼                 ▼
        Fault Detection   Fault Recovery     Fault Prevention
                                │
                    ┌───────────┴───────────┐
                    ▼                       ▼
               Preparation &              Reintroduction
                  Repair
```

> **Memory Hook — "Detect, Recover, Prevent"** → **DRP**.

### 3.1 Fault Detection tactics

| Tactic | What it does |
|---|---|
| **Ping/Echo** | Send a ping to the component; wait for an echo. If no echo → notify fault correction system. *("**Are you alive?**")* |
| **Heartbeat** | Component **emits a heartbeat periodically**; another component listens. If silence → notify fault correction. *("**I am alive…**")* |
| **Exceptions** | Trigger an **exception handler** when a fault occurs (best within the same process/component). *("**I'm dead**")* |

> **Memory Hook:** *"Ping = caller asks; Heartbeat = callee says; Exceptions = code throws."*

### 3.2 Fault Recovery — Preparation & Repair

| Tactic | What it does | Downtime |
|---|---|---|
| **Voting** | Run **redundant processors**; processes **vote on the answer**. If one disagrees → fail it. | **None** |
| **Active Redundancy** | **All redundant components respond to all events**; output taken from the **first to respond**. | **None to seconds** |
| **Passive Redundancy** | Only the **master** responds; the **backup's state is updated** so it can take over when needed. | **Seconds** |
| **Spare** | Keep a **standby spare** component to replace various failed components. | **Minutes** |

> **Memory Hook — Recovery time spectrum:**  
> Voting & Active = "**No wait**" (most expensive)  
> Passive = "Quick switch" (medium)  
> Spare = "Cold start" (cheapest, slowest)

> **Pro Tip — exam phrase:** *"For mission-critical systems requiring zero downtime, use **Active Redundancy** or **Voting**. For cost-sensitive systems where seconds-to-minutes downtime is acceptable, use **Passive Redundancy** or **Spare**."*

### 3.3 Fault Recovery — Reintroduction

These tactics handle bringing a previously failed component **back into service**:

| Tactic | What it does |
|---|---|
| **Shadow Operation** | Failed component **mimics the backup** for a while to verify correct operation before going live. |
| **State Resynchronization** | When a failed component returns to service, **its state is resynchronised** with the backup. |
| **Checkpoint / Rollback** | Record **consistent states** periodically; on fault, **restore to the checkpoint**. |

### 3.4 Fault Prevention

| Tactic | What it does |
|---|---|
| **Removal from Service** | Take a component down **periodically** to prevent anticipated failures (e.g., **scheduled reboots** to prevent memory leaks). |
| **Transactions** | **Bundle sequential steps** into atomic chunks that can be undone in case of a fault on an intermediate step. |
| **Process Monitor** | **Monitor for faulting processes**; **kill and restart** when a fault is detected. |

### Master Availability Tactics Cheat Sheet ⭐

```
                        AVAILABILITY
                              │
         ┌────────────────────┼────────────────────┐
         ▼                    ▼                    ▼
    DETECTION             RECOVERY              PREVENTION
    ──────────         ───────────────         ──────────────
    · Ping/Echo        Prep & Repair:          · Removal from
    · Heartbeat        · Voting                  Service
    · Exceptions       · Active Redundancy     · Transactions
                       · Passive Redundancy    · Process Monitor
                       · Spare
                       
                       Reintroduction:
                       · Shadow Operation
                       · State Resync
                       · Checkpoint/Rollback
```

> **Pro Tip — exam-ready Availability tactic answer:** *"To improve availability, I propose using **Active Redundancy** (a Fault Recovery tactic). Multiple redundant servers respond to all events, and the output is taken from the first to respond. This gives near-zero downtime even when one server fails — meeting the response measure of 99.99% uptime."*

---

## 4. Modifiability Tactics ⭐

### The big idea
> Goal = **control the time and cost** to **implement, test, and deploy changes**.

### The 3 categories of Modifiability tactics

```
                       MODIFIABILITY
                             │
         ┌───────────────────┼─────────────────────┐
         ▼                   ▼                     ▼
   Localize           Prevent Ripple          Defer Binding
   Modifications      Effect                  Time
   (reduce # of      (limit impact of         (control deployment
    affected          dependent module          time and cost)
    modules)          changes)
```

> **Memory Hook — "LPD"** → **L**ocalize · **P**revent ripple · **D**efer binding.

### 4.1 Localize Modifications (reduce # of modules affected)

| Tactic | What it does |
|---|---|
| **Maintain Semantic Coherence** | Keep things **related to each other** **together** in the same module. (High cohesion!) |
| **Anticipate Expected Changes** | Keep things **likely to change** in **one place**. |
| **Generalize the Module** | Make a module **more general** → it computes a broader range of functions based on input. |
| **Limit Possible Options** | **Don't allow much change** to begin with — fewer options = simpler. |

### 4.2 Prevent Ripple Effect (limit module dependencies)

| Tactic | What it does |
|---|---|
| **Hide Information** | Less visible info = fewer things others depend on. (Encapsulation!) |
| **Maintain Existing Interfaces** | **Don't change interfaces**; use the **Adapter pattern** if needed. |
| **Restrict Communication Paths** | Don't let data flow through **too many modules**. |
| **Use an Intermediary** | **Break the dependency chain** with patterns like **Façade, Mediator, Delegate, Proxy**. |

### 4.3 Defer Binding Time (control deployment time)

| Tactic | What it does |
|---|---|
| **Runtime Registration** | Components **identify themselves** after the system starts (plug & play). |
| **Configuration Files** | Settings loaded at **initiation time** — change config, not code. |
| **Polymorphism** | Method names **interpreted at runtime**. |
| **Component Replacement** | Runtime elements can be **changed at load time**. |
| **Adherence to Defined Protocols** | Runtime binding of **independent processes**. |

> **Memory Hook for Modifiability:**  
> *"Localize = pack tight. Prevent ripple = build walls. Defer binding = decide later."*

---

## 5. Performance Tactics ⭐⭐ (the other most exam-tested!)

### The big idea
> Goal = **generate a response to an event** within some **time constraint**.
>
> **Two main contributing factors:**
> - **Resource Consumption** — CPU, Disk I/O, Memory, Network
> - **Blocked Time** — waiting for resources, dependencies, multi-process priorities

### The 3 categories of Performance tactics

```
                        PERFORMANCE
                              │
         ┌────────────────────┼────────────────────┐
         ▼                    ▼                    ▼
    Resource             Resource              Resource
    Demand               Management            Arbitration
    (reduce work)        (use resources       (decide who
                          smarter)             gets what)
```

> **Memory Hook — "DMA"** → **D**emand · **M**anagement · **A**rbitration.

### 5.1 Resource Demand tactics (reduce the work needed)

| Tactic | What it does | Real example |
|---|---|---|
| **Increase Computational Efficiency** | Use **better algorithms**. | Bubble sort → Quick sort |
| **Reduce Computational Overhead** | Don't compute the same value multiple times. | `final static double pi = 22/7` (compute once, refer many times) |
| **Control Frequency of Sampling** | **Reduce sampling frequencies** of listeners/watchers. | Poll every 5 sec instead of every 0.1 sec |

### 5.2 Resource Management tactics (use what you have smarter)

| Tactic | What it does | Real example |
|---|---|---|
| **Introduce Concurrency** | If requests can be processed **in parallel**, blocked time is reduced. | Multi-threading; async processing |
| **Maintain Multiple Copies** (of data or computation) | **Caching!** Cache must stay consistent and synchronized. | Redis cache for hot data; CDN for static assets |
| **Increase Available Resources** | Add **faster or more processors / memory / network**. | Vertical scaling — more RAM, faster CPU |

> **Pro Tip:** **Caching** is the single most powerful performance tactic in real systems. Almost every high-performance architecture uses it. (Recall Stack Overflow from Lec 5: 1.5 TB of RAM holding 30% of DB data + Redis cache.)

### 5.3 Resource Arbitration tactics (when there's contention)

When multiple requests fight for the same resource (disk, network), **scheduling policies** decide who wins:

| Goal of scheduling | What it ensures |
|---|---|
| **Optimal Resource Usage** | Don't leave resources idle |
| **Maximize Throughput** | Process the most events per unit time |
| **Ensure Fairness** | All users get reasonable service |
| **Prevent Starvation** | No request waits forever |

**Common scheduling policies:** FIFO (First-In-First-Out), Fixed Priority, Round Robin.

### Master Performance Tactics Cheat Sheet ⭐

```
                        PERFORMANCE
                              │
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
   RESOURCE              RESOURCE              RESOURCE
   DEMAND                MANAGEMENT            ARBITRATION
   ──────────            ──────────────        ──────────────
   · Increase            · Introduce           Scheduling Policies:
     computational         Concurrency         · FIFO
     efficiency          · Multiple Copies     · Fixed
   · Reduce               (Caching!)           · Round Robin
     computational       · Increase
     overhead              Available
   · Control               Resources
     Sampling Freq
```

> **Pro Tip — exam-ready Performance tactic answer:** *"To improve performance, I propose **Maintain Multiple Copies** (a Resource Management tactic) by introducing a **Redis cache for thumbnails**. Since thumbnails are requested 10,000× more often than large photos, caching them in memory drops latency from disk-IO speed (~50ms) to RAM speed (~1ms), meeting the response measure of <200ms latency."* 🎯 (This directly answers the 2025 Q4.a.iv!)

---

## 6. Security Tactics ⭐

### The big idea
> Goal = ensure **Non-repudiation, Confidentiality, Integrity, and Assurance** (recall NCIA from Lec 7).
>
> **3 main concerns:**
> - **Resisting Attacks** (prevent)
> - **Detecting Attacks** (notice)
> - **Recovery from Attacks** (recover)

> **Memory Hook — "RDR"** → **R**esist · **D**etect · **R**ecover.

### 6.1 Resisting Attacks

| Tactic | What it does |
|---|---|
| **Authenticate Users** | Ensure user is **who they claim to be**. |
| **Authorize Users** | Ensure an authenticated user has the **right to access**. |
| **Maintain Data Confidentiality** | **Encrypt** data and communication links (VPN, SSL/TLS). |
| **Limit Exposure** | Avoid single point of failure; **limited services per host**. |
| **Limit Access** | **Firewall, DMZ** (demilitarized zone). |

### 6.2 Detecting Attacks

| Tactic | What it does |
|---|---|
| **Intrusion Detection** | Compare **historical statistics with current activity** for: server traffic, resource usage, network monitoring. |

### 6.3 Recovery from Attacks

| Tactic | What it does |
|---|---|
| **Restoration** | Use **availability tactics** (with extra care) — redundant copies of system & data. |
| **Identification** | Maintain an **audit trail** to trace attacker actions. (Note: the audit trail itself becomes a target; must live in a **trusted environment**.) |

> **Pro Tip:** Notice how **Security** and **Availability** tactics overlap — recovery from a successful attack uses redundancy and backup. This is one example of QAs interacting (recall the DoS overlap from Lec 6).

---

## 7. Testability Tactics

### The big idea
> Goal = **allow easier testing** when an increment of software development is completed. Main focus = **runtime testing**, which requires:
> - **Inputs** to be **provided** to the software.
> - **Outputs** to be **captured**.

### The 2 categories of Testability tactics

```
                        TESTABILITY
                              │
                ┌─────────────┴─────────────┐
                ▼                           ▼
         Input / Output              Internal Monitoring
```

### 7.1 Input/Output tactics

| Tactic | What it does |
|---|---|
| **Record / Playback** | **Capture data crossing an interface** during real use; replay it as input to the test harness. |
| **Separate Interface from Implementation** | Allows **stubbing** (mocking) — the rest of the system can be tested without the real component. |
| **Specialize Access Routes / Interfaces** | Hierarchy of test interfaces. ⚠️ Be cautious about exposing unwanted interfaces. |

### 7.2 Internal Monitoring tactics

| Tactic | What it does |
|---|---|
| **Built-in Monitors** | Permanent or temporary interfaces that **report internal state**. Useful for testing other QAs at runtime (Performance, Availability, Security). |

> **Memory Hook:** *"Testability = Mock + Monitor."*

---

## 8. Usability Tactics ⭐

### The big idea
> Goal = **provide an easy way for the user to accomplish a task**, plus **the kind of support the system gives the user**.
>
> **Two main categories:**

```
                        USABILITY
                              │
                ┌─────────────┴─────────────┐
                ▼                           ▼
         Runtime Tactics              Design Time Tactics
         (during use)                 (during construction)
```

### 8.1 Runtime tactics

| Tactic | What it does | Example |
|---|---|---|
| **User Initiatives** | Operations to help the user. | **Pause**, **Cancel**, **Undo**, **Redo** |
| **System Initiatives** | The system actively helps. | **Feedback**, **suggestions**, **notifications**, **confirmations** |
| **Mixed Initiatives** | User starts; system helps. | "Upload" → progress bar |

### 8.2 Design Time tactics

| Tactic | What it does |
|---|---|
| **Separate UI from the rest of the application** | E.g., **MVC pattern** (Model-View-Controller) — UI changes don't affect business logic. |
| **Separate UI Components** | Use modular UI components. |
| **Maintain Semantic Coherence** | Localize expected changes (same as Modifiability). |

> **Memory Hook:** *"Usability = Help the user (runtime) + Build it cleanly (design time)."*

---

## 9. Mega Summary — All Tactics in One Table ⭐⭐⭐

This is your **ultimate revision sheet**. Photocopy this onto your A4 reference sheet.

| QA | Categories | Named Tactics |
|---|---|---|
| **Availability** | Fault Detection · Fault Recovery (Prep+Repair, Reintroduction) · Fault Prevention | Ping/Echo · Heartbeat · Exceptions · Voting · Active Redundancy · Passive Redundancy · Spare · Shadow Operation · State Resync · Checkpoint/Rollback · Removal from Service · Transactions · Process Monitor |
| **Modifiability** | Localize Mods · Prevent Ripple · Defer Binding | Semantic Coherence · Anticipate Changes · Generalize · Limit Options · Hide Information · Maintain Interfaces · Restrict Comm Paths · Intermediary · Runtime Registration · Config Files · Polymorphism · Component Replacement · Defined Protocols |
| **Performance** | Resource Demand · Resource Management · Resource Arbitration | Computational Efficiency · Reduce Overhead · Control Sampling · Concurrency · Multiple Copies (Cache!) · More Resources · Scheduling (FIFO, Fixed, Round Robin) |
| **Security** | Resisting · Detecting · Recovery | Authenticate · Authorize · Encrypt · Limit Exposure · Limit Access (Firewall/DMZ) · Intrusion Detection · Restoration · Audit Trail |
| **Testability** | Input/Output · Internal Monitoring | Record/Playback · Separate Interface from Implementation (Mocking) · Specialised Access Routes · Built-in Monitors |
| **Usability** | Runtime · Design Time | User Initiatives (Cancel/Undo) · System Initiatives (Feedback/Notify) · Mixed Initiatives · Separate UI (MVC) · Separate UI Components · Semantic Coherence |

---

## 10. How to Propose a Tactic in the Exam (Step-by-Step) ⭐⭐

When the exam says *"Propose a tactic and describe how you can improve [QA] for above"*, follow this **3-step format**:

### Step 1 — Name the tactic precisely
*"I propose using **Active Redundancy** (an Availability tactic in the Fault Recovery — Preparation & Repair category)."*

### Step 2 — Describe what it does
*"Multiple redundant servers run in parallel and respond to every incoming request. The output is taken from the first server to respond."*

### Step 3 — Explain how it satisfies the response measure
*"This ensures near-zero downtime even when one server crashes — directly satisfying the QAS response measure of 99.9% availability for accessing large photos."*

> **Pro Tip — exam shortcut:** Use the magic phrase *"This satisfies the QAS response measure of [number] by [mechanism]"*. Markers love seeing the link to the QAS.

### 🎯 Worked Example — Q4.a.ii from 2025 paper

**Question:** *"Propose a tactic and describe how you can improve **Availability** for [the photo-sharing site]."*

**Answer:**
> *"I propose using **Passive Redundancy** (an Availability — Fault Recovery — Preparation & Repair tactic). The system would run a **master server** serving photo requests, with one or more **backup servers** whose state is continuously updated from the master. If the master fails, a backup takes over within **seconds**. This ensures the public consumer interface remains available with at most a few seconds of disruption — meeting the high availability requirement for accessing large photos. (For zero downtime, **Active Redundancy** could be chosen instead, at higher infrastructure cost.)"*

That's a full **2-mark answer in 60 seconds**. ✅

### 🎯 Worked Example — Q4.a.iv from 2025 paper

**Question:** *"Propose a tactic and describe how you can improve **Performance** for [the photo-sharing site]."*

**Answer:**
> *"I propose using **Maintain Multiple Copies** (a Performance — Resource Management tactic), specifically **caching thumbnails on a CDN (Content Delivery Network)**. Since thumbnails are accessed 10,000× more frequently than large photos, caching them in **edge servers near the user** drops latency from server-side processing time (~200ms) to CDN response time (~20ms), and dramatically reduces load on the origin server. Combined with **Increase Available Resources** (provisioning more web servers), this satisfies the performance response measure of sub-200ms thumbnail latency at peak load."*

That's a **2-mark answer in 60 seconds**. ✅

---

## 11. One-Shot Summary (the morning of the exam)

> An **architectural tactic** is a **planned, named way to satisfy a quality attribute response measure** through architectural decisions. Tactics are smaller than patterns — *"patterns package tactics"* — and a collection of tactics forms an **architectural strategy**. Tactics are organised into **frameworks (hierarchies)** per quality attribute. **Availability** tactics fall into **Detection** (Ping/Echo, Heartbeat, Exceptions), **Recovery** — Preparation & Repair (Voting, Active/Passive Redundancy, Spare) and Reintroduction (Shadow, State Resync, Checkpoint/Rollback), and **Prevention** (Removal from Service, Transactions, Process Monitor). **Modifiability** tactics fall into **Localize Modifications** (Semantic Coherence, Anticipate Changes, Generalise, Limit Options), **Prevent Ripple Effect** (Hide Info, Maintain Interfaces, Restrict Comm, Intermediary), and **Defer Binding** (Runtime Registration, Config Files, Polymorphism, Component Replacement, Defined Protocols). **Performance** tactics fall into **Resource Demand** (Computational Efficiency, Reduce Overhead, Control Sampling), **Resource Management** (Concurrency, Multiple Copies/Caching, More Resources), and **Resource Arbitration** (Scheduling Policies — FIFO, Fixed, Round Robin). **Security** tactics fall into **Resisting** (Authenticate, Authorize, Encrypt, Limit Exposure/Access), **Detecting** (Intrusion Detection), and **Recovery** (Restoration, Identification). **Testability** uses **Input/Output** (Record-Playback, Separate Interface from Implementation, Specialised Access Routes) and **Internal Monitoring** (Built-in Monitors). **Usability** uses **Runtime** tactics (User/System/Mixed Initiatives) and **Design Time** tactics (Separate UI, MVC, Semantic Coherence). To **propose a tactic** in the exam: **name it precisely**, **describe what it does**, and **link it to the QAS response measure**.

---

## 12. Likely Exam Questions (and how to answer)

**Q1. Define an architectural tactic. How does it differ from a pattern?**  
→ Definition (planned design decision satisfying a QA response measure). Difference: tactic is finer-grained; pattern bundles multiple tactics.

**Q2. List 3 fault detection tactics for Availability.**  
→ Ping/Echo · Heartbeat · Exceptions. Brief description each.

**Q3. Differentiate between Active Redundancy, Passive Redundancy, and Spare.**  
→ Active = all respond, first wins (no downtime). Passive = master responds, backup ready (seconds). Spare = standby for many failures (minutes).

**Q4. Propose a tactic to improve [QA] for [system].** ⭐ (almost certain!)  
→ Use the **3-step format**: (1) Name + category, (2) Describe, (3) Link to QAS response measure.

**Q5. List Performance tactics organised by category.**  
→ Resource Demand (Computational Efficiency, Reduce Overhead, Control Sampling) · Resource Management (Concurrency, Multiple Copies, More Resources) · Resource Arbitration (Scheduling).

**Q6. Why is "Maintain Multiple Copies" a particularly powerful Performance tactic?**  
→ Caching dramatically reduces latency by serving from RAM/CDN instead of origin/disk. Real-world example: Stack Overflow's 1.5 TB RAM cache + Redis.

**Q7. Explain Security tactics for Resisting Attacks.**  
→ Authenticate · Authorize · Maintain Confidentiality (encryption) · Limit Exposure · Limit Access (Firewall/DMZ).

---

## 13. Vocabulary You Should Use Confidently

- **Architectural tactic** — design decision satisfying a QA response measure.
- **Architectural strategy** — collection of tactics.
- **Pattern packages tactics** — patterns implement multiple tactics.
- **Fault Detection / Recovery / Prevention** — Availability tactic categories.
- **Ping/Echo, Heartbeat, Active/Passive Redundancy, Voting, Spare, Checkpoint/Rollback** — named Availability tactics.
- **Localize / Prevent Ripple / Defer Binding** — Modifiability tactic categories.
- **Resource Demand / Management / Arbitration** — Performance tactic categories.
- **Caching / Concurrency / Scheduling** — common Performance tactics.
- **Resisting / Detecting / Recovery from Attacks** — Security tactic categories.
- **Authentication / Authorization / Encryption / Firewall / DMZ / Audit Trail** — named Security tactics.
- **Record/Playback / Mocking / Built-in Monitors** — Testability tactics.
- **User / System / Mixed Initiatives / MVC** — Usability tactics.

---

## 14. References

- Bass, Clements & Kazman — *Software Architecture in Practice* (Chapter 5 — Achieving Qualities).
- http://www.ece.ubc.ca/~matei/EECE417/BASS/ch05.html

---

**Pro Tip — connection to past paper (2025) and QAS lecture (Lec 7):**

The exam pattern is consistent:
- **Q4.a.i** → Concrete QAS for **Availability** (use Lec 7 SSAERR template)
- **Q4.a.ii** → **Tactic** for **Availability** (use this lecture: pick from the Availability framework)
- **Q4.a.iii** → Concrete QAS for **Performance** (use Lec 7 SSAERR template)
- **Q4.a.iv** → **Tactic** for **Performance** (use this lecture: pick from the Performance framework)

So the **flow is**:
1. **Lec 6** — define quality attributes (vocabulary).
2. **Lec 7** — express them formally (QAS / SSAERR template).
3. **Lec 8 (this lecture)** — achieve them (Tactics).

Practice writing **3 QAS + 3 Tactics for each of Availability and Performance** before the exam. You'll be ready for any case study they throw at you. 💪

Send Lecture 9 (Architectural Patterns & Styles) when you're ready. 🚀
