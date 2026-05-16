# Lecture 07 — Quality Attribute Scenarios (QAS)

**Module:** SE3030 — Software Architecture · 3rd Year, Semester 1 · SLIIT  
**Lecturer:** Chathura R De Silva

> ⚠️ **CRITICAL EXAM LECTURE** — The 2025 paper had **2 sub-questions (Q4.a.i and Q4.a.iii)** that directly asked you to **write concrete QAS for Availability and Performance**. This will almost certainly happen again. The **6-part template** in this lecture is **mandatory memorisation**. ☕

---

## What you should walk away knowing

1. What a **Quality Attribute Scenario (QAS)** is and why we use them.
2. The difference between a **General** and **Concrete** scenario.
3. The **6-part QAS template** (cold, by heart!).
4. How to write a **concrete QAS for each** of the 6 main quality attributes:
   - Availability · Modifiability · Performance · Security · Testability · Usability
5. The **possible values** each part of the template can take for each attribute.

> **Pro Tip:** This is one lecture where you absolutely **cannot wing it** in the exam. Memorise the template structure (SSAERR) and *practice writing scenarios* until it's second nature.

---

## 1. What is a Quality Attribute Scenario? ⭐

> **Definition:** A **Quality Attribute Scenario (QAS)** is a **universal, formal way to express quality attributes**. Its goal is to capture **unambiguous and testable** quality requirements — the same way **use case scenarios** capture functional requirements.

In plain English:
- Functional requirement → "User can withdraw money" (one feature)
- Use case → "User selects amount → enters PIN → cash dispensed" (formal sequence)
- Quality attribute → "System must be fast" (vague!)
- **Quality Attribute Scenario** → "**Under normal load, when a user clicks Withdraw, the system completes the cash dispensing within 3 seconds**" (formal, testable!)

> **Memory Hook:** *"QAS is to quality attributes what Use Cases are to functions."* They both make vague wishes into **testable, unambiguous specifications**.

---

## 2. General vs Concrete Scenarios ⭐

| | General Scenario | Concrete Scenario |
|---|---|---|
| **Scope** | **System-independent** — could apply to any system | **Specific** to one particular system |
| **Use** | Template / framework for thinking | Actual quality requirement for *your* system |
| **What it gives you** | A **menu** of possible values (Source, Stimulus, etc.) | One **chosen path** through that menu, with **specific values** |

> **Memory Hook:**  
> **General** = recipe ("for fried rice, you need a starch + protein + vegetables").  
> **Concrete** = your dinner ("100g cooked rice + 1 chicken breast + 50g carrots").

> **Key takeaway from the slide:** *"Concrete scenarios are needed to make the quality requirements operational. A collection of concrete scenarios can be used as the quality attribute requirements for a system."*

---

## 3. The 6-Part QAS Template ⭐⭐⭐ (memorise!)

Every QAS — general or concrete — has the **same 6 parts**. The exam will ask you to identify them or write a scenario containing them.

```
                      ┌────────────────────────────────────────┐
                      │   Quality Attribute Scenario (QAS)     │
                      └────────────────────────────────────────┘
                                       │
       ┌──────┬───────────┬────────────┼────────────┬──────────┬───────────────┐
       ▼      ▼           ▼            ▼            ▼          ▼               ▼
   Source  Stimulus  Artifact   Environment    Response   Response Measure
   (who)   (action)   (what)       (when)       (result)    (measurement)
```

### The 6 parts in detail

| # | Part | Question it answers | Plain English |
|---|---|---|---|
| 1 | **Source** | **Who?** | The **originator** of the event/action — could be a user, an admin, an external system, an internal component, or a hostile attacker. |
| 2 | **Stimulus** | **What action?** | The **action or external event** that arrives at the system. ("User clicks button", "fault occurs", "message arrives".) |
| 3 | **Artifact** | **What part of the system?** | The **part of the system** to which the quality requirement applies. ("The login module", "the database", "the entire system".) |
| 4 | **Environment** | **When / under what conditions?** | The **external circumstances** when the requirement must be met. ("During normal operation", "under overload", "at runtime".) |
| 5 | **Response** | **What does the system do?** | How the system **reacts** to the stimulus. |
| 6 | **Response Measure** | **How well? (in numbers)** | The **metric** that quantifies the quality attribute — *this is where numbers go*. |

> **Memory Hook — "SSAERR"** (pronounced "SAY-err") → **S**ource, **S**timulus, **A**rtifact, **E**nvironment, **R**esponse, **R**esponse Measure.
>
> Or remember as **"Who, What, Which, When, Result, Number"** — and that's your scenario.

> **Pro Tip — exam template:** When asked to write a concrete QAS, structure your answer as a **6-row table** or as a **single sentence that names all 6 parts explicitly**:
>
> *"[SOURCE] (e.g., An authenticated user) [STIMULUS] (clicks Submit) on [ARTIFACT] (the checkout page) during [ENVIRONMENT] (normal operation), and [RESPONSE] (the system processes the order and shows confirmation) within [RESPONSE MEASURE] (2 seconds)."*
>
> Markers love when you label each part. Don't make them guess!

---

## 4. The 6 Quality Attributes Covered ⭐

The lecture walks through QAS for these 6 attributes (memorise this list!):

```
┌──────────────────────────────────────────────────┐
│        The 6 QAs covered with QAS templates:     │
│                                                  │
│   1. Availability                                │
│   2. Modifiability                               │
│   3. Performance                                 │
│   4. Security                                    │
│   5. Testability                                 │
│   6. Usability                                   │
└──────────────────────────────────────────────────┘
```

> **Memory Hook — "AMPSTU"** → **A**vailability · **M**odifiability · **P**erformance · **S**ecurity · **T**estability · **U**sability.
> (Almost like "amp shoe"… 🔌👟 ugly = memorable)

---

## 5. Availability QAS ⭐ (highly examable!)

### What Availability is concerned with
- **System failure and its consequences.**
- **Faults vs Failures** (a fault might lead to a failure).
- **Non-operative time** — when the system isn't working.
- **Frequency, results, prevention, notifications.**

> Definition: *"The availability of a system is the probability that it will be operational when it is needed."*

### General Scenario — Availability

| Part | Possible Values |
|---|---|
| **Source** | Internal to the system; external to the system |
| **Stimulus** | **Fault**: omission, crash, timing, response (incorrect) |
| **Artifact** | System's **processors, communication channels, persistent storage, processes** |
| **Environment** | Normal operation; **degraded mode** (fewer features / fallback) |
| **Response** | System should **detect** the event and do one or more of:<br>· **Record** it<br>· **Notify** appropriate parties (user, other systems)<br>· **Disable** sources of events causing the fault<br>· Be **unavailable** for a prespecified interval (depending on criticality)<br>· **Continue** to operate in normal or degraded mode |
| **Response Measure** | Time interval when the system **must be available**; **availability time**; time interval in which system can be in **degraded mode**; **repair time** |

### Concrete Scenario — Availability (textbook example)

> *"An **unanticipated external message** is received by a **process** during **normal operation**. The process **informs the operator** of the receipt of the message and **continues to operate with no downtime**."*

Let's break it down:

| Part | Value |
|---|---|
| **Source** | External system (the unanticipated message originator) |
| **Stimulus** | Unanticipated external message arrives |
| **Artifact** | A process inside the system |
| **Environment** | Normal operation |
| **Response** | Informs the operator; continues to operate |
| **Response Measure** | **No downtime** (zero seconds of unavailability) |

### Worked Exercise — MS Word Availability QAS (slide 9)

> *"A **Kill Signal** is received from the **Windows OS** to the **Ms. Word Application** during **process Not Responding state** and the application **saves unsaved work in a temp file** and **process terminates without any data loss**."*

| Part | Value |
|---|---|
| **Source** | Windows OS |
| **Stimulus** | Kill Signal sent to Word |
| **Artifact** | MS Word Application |
| **Environment** | Process is in "Not Responding" state |
| **Response** | Saves unsaved work in a temp file; process terminates |
| **Response Measure** | **Zero data loss** |

> **Pro Tip — exam template for Availability QAS:**  
> *"[Internal/external source] sends [fault stimulus] to [system component] during [normal/degraded mode], and the system [detects/notifies/recovers] within [time interval / data loss spec]."*

---

## 6. Modifiability QAS ⭐

### What Modifiability is concerned with
- **The cost of change.** Modifiability raises 2 concerns:
  - **What** can change? → Functions, Platform, Environment, Protocol, Qualities, Capacity
  - **When** is the change made and **who** makes it? → A developer, end user, or sysadmin; at implementation, compilation, build, configuration, or execution time

### General Scenario — Modifiability

| Part | Possible Values |
|---|---|
| **Source** | End user, developer, system administrator |
| **Stimulus** | Wishes to **add / delete / modify / vary** functionality, quality attribute, capacity |
| **Artifact** | System UI, platform, environment; system that interoperates with target system |
| **Environment** | At **runtime, compile time, build time, design time** |
| **Response** | **Locates** places in architecture to be modified; **makes modification** without affecting other functionality; **tests** modification; **deploys** modification |
| **Response Measure** | **Cost** in number of elements affected, effort, money; **extent** to which it affects other functions/qualities |

### Concrete Scenario — Modifiability (textbook example)

> *"A **developer** wishes to **change the user interface to make a screen's background color blue**. This change will be made to the **code at design time**. It will take **less than three hours to make and test the change** and **no side effect changes will occur** in the behavior."*

| Part | Value |
|---|---|
| **Source** | Developer |
| **Stimulus** | Wishes to change the UI background colour to blue |
| **Artifact** | The code (UI module) |
| **Environment** | At design time |
| **Response** | Locates and makes the change; tests it |
| **Response Measure** | **Less than 3 hours**; **zero side effects** |

### Worked Exercise — DB Password Update QAS (slide 14)

> *"**System Administrator** wishes to **change the password of the database configuration file** on the **Data Tier** at the **System Maintenance Time**; the activity takes **2 minutes** and the application is able to **connect to the Database without any issues**."*

| Part | Value |
|---|---|
| **Source** | System Administrator |
| **Stimulus** | Wishes to change DB password in the config file |
| **Artifact** | Data Tier (database configuration file) |
| **Environment** | System Maintenance Time |
| **Response** | Password updated; application reconnects |
| **Response Measure** | **2 minutes** to complete; zero connection issues |

---

## 7. Performance QAS ⭐⭐ (very examable!)

### What Performance is concerned with
- **Timing.** Events arrive (interrupts, messages, requests, time passing) and the system must **respond**.
- Basically: **how long does it take the system to respond when an event occurs?**

### General Scenario — Performance

| Part | Possible Values |
|---|---|
| **Source** | One of a number of **independent sources**, possibly from within the system |
| **Stimulus** | **Periodic** events arrive; **sporadic** events arrive; **stochastic** (random) events arrive |
| **Artifact** | The system |
| **Environment** | Normal mode; **overload** mode |
| **Response** | Processes stimuli; changes level of service |
| **Response Measure** | **Latency, deadline, throughput, jitter, miss rate, data loss** |

> **Memory Hook for Response Measures:** "**LDTJMD**" — Latency, Deadline, Throughput, Jitter, Miss-rate, Data-loss. Or just "**Latency + Throughput + the rest**".

### Concrete Scenario — Performance (textbook example)

> *"**Users** initiate **1,000 transactions per minute randomly** under **normal operations**, and these transactions are **processed with an average latency of two seconds**."*

| Part | Value |
|---|---|
| **Source** | Users |
| **Stimulus** | 1,000 transactions per minute (stochastic / random) |
| **Artifact** | The system |
| **Environment** | Normal operations |
| **Response** | Processes transactions |
| **Response Measure** | **Average latency = 2 seconds** |

### Worked Exercise — Banking Weekly Report QAS (slide 19)

> *"The **Finance Analyst** schedules a **weekly report** of the Banking Application during **Normal Operational Time (8am-5pm)**, the process starts to execute at the **Off-Peak Time (10pm-2am)** and the **Report Excel File generates successfully within 30 minutes**."*

| Part | Value |
|---|---|
| **Source** | Finance Analyst |
| **Stimulus** | Schedules weekly report |
| **Artifact** | Banking Application (report generator) |
| **Environment** | Schedule during 8am-5pm; execution during 10pm-2am off-peak |
| **Response** | Excel report file generated successfully |
| **Response Measure** | **Max latency 18 hours** (8am → 2am); **Max deadline = latency + 30 minutes** |

> **Pro Tip — exam template for Performance QAS:**  
> *"[Source] generates [periodic/sporadic/stochastic] events on [artifact] during [normal/overload mode], and the system processes them with [latency/throughput/...] of [number]."*

---

## 8. Security QAS

### What Security is concerned with
> *"Security is a measure of the system's ability to **resist unauthorized usage** while still **providing services to legitimate users**."*

**An attempt to breach security is called an attack.** Forms include:
- Unauthorized attempt to **access** data
- **Modify** data
- **Deny services** (DoS) to legitimate users

### The 6 Security characterizations (memorise!) ⭐

| # | Characterization | Plain English |
|---|---|---|
| 1 | **Non-repudiation** | A transaction **cannot be denied** by any party (you can prove who did it) |
| 2 | **Confidentiality** | Data/services are **protected from unauthorized access** |
| 3 | **Integrity** | Data/services are **delivered as intended** (not tampered with) |
| 4 | **Assurance / Authenticity** | The parties to a transaction **are who they claim to be** |
| 5 | **Availability** (no DoS) | The system is **available for legitimate use** |
| 6 | **Auditing** | The system **tracks activities** |

> **Memory Hook — "NCIA AA"** → **N**on-repudiation, **C**onfidentiality, **I**ntegrity, **A**ssurance/authenticity, **A**vailability (no DoS), **A**uditing.

### General Scenario — Security

| Part | Possible Values |
|---|---|
| **Source** | Individual or system, **correctly identified / wrongly identified / unknown**, internal/external, authorized/not authorized, with access to limited or vast resources |
| **Stimulus** | Tries to **display, change/delete, access** data/services; **reduce availability** |
| **Artifact** | System services; data within system |
| **Environment** | Online/offline; connected/disconnected; firewalled/open |
| **Response** | **Authenticates** user; **hides identity**; **blocks** access; **allows** access; **grants/withdraws** permission; **records** access; stores data in **unreadable format**; recognizes unusual demand for services and **informs/restricts** |
| **Response Measure** | **Time/effort/resources** required to **circumvent** security; **probability of success / detection / identification**; **percentage of services available under DoS**; **restore** time; **extent of damage** |

### Concrete Scenario — Security (textbook example)

> *"A **correctly identified individual** tries to **modify system data** from an **external site**; the system **maintains an audit trail** and the **correct data is restored within one day**."*

| Part | Value |
|---|---|
| **Source** | A correctly identified individual |
| **Stimulus** | Tries to modify system data |
| **Artifact** | System data |
| **Environment** | External site |
| **Response** | Maintains an audit trail |
| **Response Measure** | **Correct data restored within 1 day** |

---

## 9. Testability QAS

### What Testability is concerned with
> *"Software testability refers to the ease with which software can be made to demonstrate its faults through (typically execution-based) testing."*

**Eye-opening fact from the slide:** *"At least **40% of the cost** of developing well-engineered systems is taken up by testing."*

For a system to be properly testable, it must be possible to:
- **Control** each component's internal state and inputs.
- **Observe** its outputs.

> **Memory Hook:** *"Testability = Control + Observe."*

### General Scenario — Testability

| Part | Possible Values |
|---|---|
| **Source** | Unit developer; Increment integrator; System verifier; Client acceptance tester; System user |
| **Stimulus** | Analysis / architecture / design / class / subsystem integration completed; system delivered |
| **Artifact** | Piece of design; piece of code; complete application |
| **Environment** | At design / development / compile / deployment time |
| **Response** | Provides access to **state values**; provides **computed values**; prepares **test environment** |
| **Response Measure** | **% of statements executed** (coverage); **probability of failure if fault exists**; **time to perform tests**; **length of longest dependency chain**; **time to prepare test environment** |

### Concrete Scenario — Testability (textbook example)

> *"A **unit tester** performs a **unit test** on a **completed system component** that provides an **interface for controlling its behavior and observing its output**; **85% path coverage is achieved within three hours**."*

| Part | Value |
|---|---|
| **Source** | Unit tester |
| **Stimulus** | Performs a unit test |
| **Artifact** | Completed system component |
| **Environment** | Component provides interface for control and observation |
| **Response** | Achieves test coverage |
| **Response Measure** | **85% path coverage within 3 hours** |

---

## 10. Usability QAS

### What Usability is concerned with (recall from Lec 6 — LEEAC)
1. **Learn** features
2. **Efficient** use
3. **Errors** handled well
4. **Adapt** to user needs
5. **Confidence** in actions

### General Scenario — Usability

| Part | Possible Values |
|---|---|
| **Source** | **End user is always the source** (can be broken into roles/actors) |
| **Stimulus** | Wants to **learn** features; **use efficiently**; **minimize errors**; **adapt** system; **feel comfortable** |
| **Artifact** | The system (or part of the system the user is interacting with) |
| **Environment** | At **runtime** or **configure time** |
| **Response** | System provides one or more of:<br>· To support learning system features<br>· To support efficient use<br>· To minimize impact of errors<br>· To adapt: customizability, internationalization<br>· To feel comfortable: display state, work at user's pace |
| **Response Measure** | **Task time, number of errors, problems solved, user satisfaction, knowledge gained, success ratio, time/data lost** |

### Concrete Scenario — Usability (textbook example)

> *"A **user**, wanting to **minimize the impact of an error**, wishes to **cancel a system operation at runtime**; **cancellation takes place in less than one second**."*

| Part | Value |
|---|---|
| **Source** | User |
| **Stimulus** | Wishes to cancel a system operation (to minimize error impact) |
| **Artifact** | The system |
| **Environment** | At runtime |
| **Response** | Cancels operation |
| **Response Measure** | **Cancellation in <1 second** |

---

## 11. Master Summary Table — All 6 QAs at a glance ⭐

| QA | Concerned with | Typical Source | Typical Stimulus | Typical Response Measure |
|---|---|---|---|---|
| **Availability** | System failure & consequences | Internal/external | Fault (omission, crash, timing, incorrect) | Uptime %, downtime interval, repair time |
| **Modifiability** | Cost of change | Developer / sysadmin / user | Wishes to add/delete/modify | Effort (hours, money, # elements affected) |
| **Performance** | Timing | Independent sources | Periodic / sporadic / stochastic events | Latency, throughput, jitter, miss rate |
| **Security** | Resisting attacks | Identified/unidentified user/system | Try to access / modify / DoS | Time to circumvent, % services up under DoS, restore time |
| **Testability** | Ease of demonstrating faults | Tester / integrator / dev | Phase completed / system delivered | % coverage, time to test, time to set up env |
| **Usability** | User effectiveness | **End user** (always!) | Wants to learn / be efficient / minimize errors | Task time, errors, satisfaction |

> **Pro Tip — exam revision:** Photocopy this table onto your A4 reference sheet. It saves you **hours** of memorisation in the exam.

---

## 12. Step-by-Step: How to Write a Concrete QAS in the Exam ⭐⭐

This is the **template** you need when the exam says *"Write a concrete QAS for [Quality Attribute] of [some system]"*.

### Step 1 — Identify the quality attribute
The exam tells you which one. (e.g., "Performance for the photo-sharing site")

### Step 2 — Recall the General Scenario possibilities
Use the master table above as a reminder.

### Step 3 — Pick a specific value for each of the 6 parts
Make sure each value is **specific to the system in the question**, not generic.

### Step 4 — Write it as a single sentence (or table)
**Best format for the exam:** A 6-row table with each part labelled. This makes marking trivial — full marks every time.

### 🎯 Worked example — Q4.a.i from 2025 paper

**Question:** *"Write concrete Quality Attribute Scenarios for **Availability** for the public photo sharing website."*

**Recall from the question:** "Expect high availability on accessing large photos."

**Concrete QAS:**

| Part | Value |
|---|---|
| **Source** | An external user on the internet |
| **Stimulus** | Sends an HTTP GET request for a large photo |
| **Artifact** | The Public Consumer Module's large-photo serving subsystem |
| **Environment** | During normal operation (peak traffic, weekday business hours) |
| **Response** | The system serves the requested large photo, or — if the primary server fails — automatically fails over to a standby and serves the photo |
| **Response Measure** | **99.9% availability per month** (≤43 minutes downtime); **zero failed downloads** during failover |

That's a **3-mark answer in 90 seconds**. ✅

### 🎯 Worked example — Q4.a.iii from 2025 paper

**Question:** *"Write concrete Quality Attribute Scenarios for **Performance** for the public photo sharing website."*

**Recall:** "Anticipated thumbnail view frequency is 10,000 times more than large photo view frequency."

**Concrete QAS:**

| Part | Value |
|---|---|
| **Source** | Public consumers (thousands of independent users) |
| **Stimulus** | Stochastic HTTP requests for thumbnails (~10,000× the volume of large-photo requests) |
| **Artifact** | The thumbnail-serving subsystem of the Public Consumer Module |
| **Environment** | Normal operation, peak browsing time |
| **Response** | The system serves the requested thumbnails |
| **Response Measure** | **Average latency ≤ 200 ms** per thumbnail; **throughput ≥ 1,000 requests per second** |

That's a **3-mark answer in 90 seconds**. ✅

> **Pro Tip — common student mistake:** Students forget to give a **specific number** for the response measure. Without numbers, it's not a concrete scenario — you'll lose marks.

---

## 13. One-Shot Summary (the morning of the exam)

> A **Quality Attribute Scenario (QAS)** is the formal, testable way to express a quality attribute — analogous to use case scenarios for functional requirements. **General scenarios** are system-independent templates listing the *possibilities* for each part; **Concrete scenarios** apply specific values for a particular system. Every QAS has **6 parts** — **SSAERR**: **Source** (who), **Stimulus** (what action), **Artifact** (which part of the system), **Environment** (when / under what conditions), **Response** (what the system does), **Response Measure** (the number that quantifies it). The lecture covers QAS templates for the **6 main quality attributes** — **AMPSTU**: **Availability**, **Modifiability**, **Performance**, **Security**, **Testability**, **Usability** — each with characteristic Sources, Stimuli, Artifacts, Environments, Responses, and Response Measures. Security is further characterized by **6 security concerns**: **Non-repudiation, Confidentiality, Integrity, Assurance/authenticity, Availability (no DoS), Auditing**. To **write a concrete QAS** in the exam: pick specific values for each of the 6 parts, present it as a **6-row labelled table**, and **always include a number** in the response measure (latency in ms, uptime %, hours of effort, etc.). The next lecture introduces **Tactics** — *how* you actually achieve a quality attribute response measure.

---

## 14. Likely Exam Questions (and how to answer)

**Q1. What is a Quality Attribute Scenario? Why is it useful?**  
→ Definition (universal, formal way to express QAs; testable & unambiguous). It's useful because it converts vague NFRs ("must be fast") into testable specifications ("response time <2 sec under 1,000 TPS").

**Q2. List and explain the 6 parts of a QAS.**  
→ The SSAERR table: Source, Stimulus, Artifact, Environment, Response, Response Measure. One-line explanation each.

**Q3. Differentiate between General and Concrete scenarios.**  
→ General = system-independent template (lists possibilities). Concrete = system-specific instance (chosen specific values, especially numeric response measure).

**Q4. Write a concrete QAS for [Availability / Performance / Security / etc.] for [some system].** ⭐ (almost certain!)  
→ Use the **6-row labelled table** template. Pick specific values. Include numbers in the response measure.

**Q5. List the 6 security characterizations.**  
→ NCIAAA: Non-repudiation, Confidentiality, Integrity, Assurance/Authenticity, Availability (no DoS), Auditing.

**Q6. Identify Source, Stimulus, etc. from a given scenario.**  
→ Highlight each labelled part in the given paragraph.

---

## 15. Vocabulary You Should Use Confidently

- **Quality Attribute Scenario (QAS)** — formal way to express a QA.
- **General scenario** — system-independent template.
- **Concrete scenario** — specific to a particular system, with specific values.
- **Source** — who/what initiates the stimulus.
- **Stimulus** — the action/event that arrives.
- **Artifact** — the system part that the QA applies to.
- **Environment** — circumstances when the QA must be met.
- **Response** — how the system reacts.
- **Response Measure** — the metric that quantifies it.
- **Fault vs Failure** — a fault may lead to a failure.
- **Latency / Throughput / Jitter / Miss-rate** — performance response measures.
- **Non-repudiation, Confidentiality, Integrity, Assurance, Availability (no DoS), Auditing** — security characterizations.
- **Path coverage** — a testability metric.

---

## 16. References

- Bass, Clements & Kazman — *Software Architecture in Practice* (Chapter 4 — Understanding Quality Attributes).
- http://www.ece.ubc.ca/~matei/EECE417/BASS/ch04lev1sec4.html
- http://etutorials.org/Programming/Software+architecture+in+practice,+second+edition/Part+Two+Creating+an+Architecture/Chapter+4.+Understanding+Quality+Attributes/4.4+Quality+Attribute+Scenarios+in+Practice/

---

**Pro Tip — connection to past paper (2025):**
- **Q4.a.i** asked for a concrete QAS for **Availability** — use the format from section 12.
- **Q4.a.iii** asked for a concrete QAS for **Performance** — same format.
- **Q4.a.ii** and **Q4.a.iv** asked for a **Tactic** — that's the **next lecture (Lec 8)**.

This is the most **mechanically-tested** lecture in the course. **Practice writing 5–10 concrete scenarios before the exam** for different systems (banking app, photo site, e-commerce, healthcare). Once you can do it in <2 minutes, you're golden.

Send Lecture 8 (Tactics) when you're ready. 🚀
