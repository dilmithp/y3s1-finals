# SE3040 – Application Frameworks: Complete Study Notes

> Detailed, page-by-page study notes compiled from all uploaded lecture slides. Every page of every PDF is covered without skipping. Each lecture is summarized first, then walked through page-by-page with explanations and context.

## Table of Contents

1. [Lecture 01 – Introduction & Best Practices](#lecture-01--introduction--best-practices) (32 pages)
2. [Lecture 02 – Application Frameworks](#lecture-02--application-frameworks) (35 pages)
3. [Lecture 03 – JavaScript](#lecture-03--javascript) (16 pages)
4. [Lecture 04 – NodeJS](#lecture-04--nodejs) (17 pages)
5. [Lecture 05 – REST and ExpressJS](#lecture-05--rest-and-expressjs) (33 pages)
6. [Lecture 06 – NoSQL and MongoDB](#lecture-06--nosql-and-mongodb) (21 pages)
7. [Lecture 08 Part 01 – ReactJS](#lecture-08-part-01--reactjs) (73 pages)
8. [Lecture 08 Part 02 – ReactJS](#lecture-08-part-02--reactjs) (50 pages)
9. [Lecture 09 – Framework Selection](#lecture-09--framework-selection) (26 pages)

---

## Lecture 01 – Introduction & Best Practices

### Page 1 – Title Slide
The module is **SE3040 – Application Frameworks**, and this is Lecture 01 titled "Introduction." It sets the stage for the course, which is centered on building applications using industry-grade frameworks and engineering practices.

### Page 2 – Agenda
The lecture walks through five things: what this course is, the course's objectives, the topics to be covered, how students will be evaluated, and finally the *principles, guidelines, and practices* that underpin good engineering. The progression goes from administrative information to the conceptual foundation of professional software development.

### Page 3 – Our Team
Introduces the teaching team: Ms. Karthiga Rajendran (Lecturer-in-Charge), Mr. Eishan Weerasinghe (Co-Lecturer), Ms. Madusha Weerasooriya (Assistant Lecturer), Mr. Janidu Illesinghe (Academic Instructor), and Ms. Piumi Navodya (Academic Instructor). All are from the Department of Software Engineering, Faculty of Computing.

### Page 4 – Module Outline
The module name is *Application Frameworks*, code **SE3040**, worth **4 credit points**. Assessment splits into two halves: **Continuous Assessments (60%)** and **Final Examination (40%)**. The heavy CA weight signals that this is a hands-on, project-driven course.

### Page 5 – Evaluation Breakdown
Evaluation focuses on applying concepts in practical settings. The CA breakdown is: **Mid Examination 20%, Assignment Milestone 01 10%, Assignment Milestone 02 25%, Weekly Lab Submission 5%**. The Final Exam contributes 40%. Milestone 02 (25%) is the most heavily weighted single CA component, signalling the final project is the main deliverable.

### Page 6 – What is this Course?
The course centers on application development using industry standards and leading frameworks. It is primarily built around **Java and JavaScript**. It also focuses on industry practices and principles in software engineering, popular JavaScript and Java frameworks, and an introduction to **NoSQL databases**.

### Page 7 – Objectives (Conceptual)
Students will learn industry practices and principles, discover new trends in JavaScript and Java, gain JavaScript full-stack development knowledge, learn NoSQL/MongoDB, learn **REST-style web services**, and study leading frameworks together with architecture and authentication mechanisms used in industry.

### Page 8 – Objectives (Technology Stack)
The concrete technology stack to be learned: **JavaScript, ReactJS, NodeJS, ExpressJS, MongoDB**, popular frameworks for web app development, and **containerization** (e.g., Docker). Together this forms the MERN stack plus DevOps fundamentals.

### Page 9 – Section Divider: Principles, Guidelines & Practices
A divider introducing the second half of the lecture, which covers the conceptual backbone of how good engineers think and work. The course splits these into three layers: principles (rules), guidelines (heuristics for decision-making), and practices (recurring activities).

### Page 10 – PRINCIPLES – S.O.L.I.D.
The **SOLID** principles are five rules for designing object-oriented classes well: **S**ingle Responsibility, **O**pen-Close, **L**iskov Substitution, **I**nterface Segregation, and **D**ependency Inversion. They were popularized by Robert C. Martin and have become the canonical class-design checklist.

### Page 11 – Single Responsibility Principle (SRP)
A class should have **one and only one reason to change**, meaning it should have only one job. This rule applies not only to classes but to any "unit": function, module, API. The classic example: a class that calculates a circle's area and outputs it as HTML violates SRP because two reasons could force a change — math logic and output format. If JSON output is later required, the class must change for a reason unrelated to math.

### Page 12 – Open/Close Principle (OCP)
*"Objects or entities should be open for extension, but closed for modification."* If you have a class that computes the area of a circle and a square, adding a triangle should not force editing the existing class — you should be able to extend it instead. The practical mechanism is **abstraction**: depend on abstract types (interfaces, base classes) rather than concrete implementations whenever change is likely.

### Page 13 – Liskov Substitution Principle (LSP)
*"Every subclass/derived class should be able to substitute its parent/base class."* When you extend a class, the subclass must support all the base class's behavior. Specifically: child classes should not leave methods unimplemented, and they should not give different semantics to inherited methods when overriding. If code that works with the parent breaks when given the child, LSP is violated.

### Page 14 – Interface Segregation Principle (ISP)
*"Clients should not be forced to implement methods they do not use."* Example: a `Shape` interface with both `draw()` and `calculateArea()` forces a client that only wants to draw to implement area calculation too. These are called **fat interfaces**. The remedy is to split into smaller, role-specific interfaces, each serving a particular kind of client.

### Page 15 – Dependency Inversion Principle (DIP)
*"Higher-level modules should not depend on lower-level modules; both should depend on abstractions."* If `OrderProcessor` depends directly on a concrete `OrderDatabase`, the two are tightly coupled. By introducing an `IOrderDatabase` interface and having both `OrderProcessor` depend on it and `OrderDatabase` implement it, you decouple them. The code becomes flexible (swap implementations) and maintainable (test with mocks).

### Page 16 – GUIDELINES — 1. Think Through the Problem
Before any solution work, fully understand the problem. Don't start designing prematurely; clarify any vague piece of the requirement first. There are *no stupid questions* — asking is cheaper than building the wrong thing.

### Page 17 – 2. Approaching the Solution
Software engineering is about finding a **technical solution to a business problem**. To do this well, follow a small set of approaches: **Divide and Conquer, KISS, Learn from mistakes, Remember why the software exists, Remember you are not the user.**

### Page 18 – Divide and Conquer
Break the problem into smaller, manageable pieces. Each piece should be understandable on its own. Find the balance between *priority* (what needs solving first) and *clarity* (keeping each piece simple).

### Page 19 – KISS + Learn from Mistakes
**KISS — Keep It Simple, Stupid**: don't deliberately add complexity, don't overthink, don't over-engineer.
**Learn from mistakes**: embrace change rather than fearing it. Anticipate likely changes, but keep extension paths open rather than building speculative features now.

### Page 20 – Why Software Exists + You're Not the User
**Reason software exists**: keep the bigger purpose in mind; losing sight of *why* often leads down wrong technical paths.
**You won't be using the software**: end-users are usually not as technical as the developer. Don't assume the user will understand. User-friendliness and UX matter more than developer convenience.

### Page 21 – Implementing the Solution
When moving from design to code, follow these guidelines: **YAGNI, DRY, Embrace abstraction, DRITW, Write code that does one thing well, Debugging is harder than writing code, Kaizen.**

### Page 22 – YAGNI and DRY
**YAGNI — You Aren't Gonna Need It**: don't write speculative code "for the future." Requirements change; speculative code is usually wasted effort.
**DRY — Don't Repeat Yourself**: reuse code, keep it generalized and reusable, avoid duplication.

### Page 23 – Embrace Abstraction + DRITW
**Embrace Abstraction**: a system should function without each component knowing the internals of every other. A `User` class should authenticate without knowing where the credentials come from.
**DRITW — Don't Reinvent the Wheel**: if someone has solved the problem (a library, framework, algorithm), use it rather than reimplementing it.

### Page 24 – One Thing Well + Readability
**Write code that does one thing well**: a single piece of code should do one thing, and do it well. Avoid "magic" code that does many things.
**Debugging is harder than writing code**: keep code readable. Readable beats compact every time — clever one-liners that no one can debug later are a liability.

### Page 25 – KAIZEN
*"Leave it better than when you found it."* When you touch code to fix a bug, fix the surrounding code too where needed. A band-aid fix won't help if the underlying issue is a design flaw — improve the design as you go.

### Page 26 – PRACTICES
Practices are recurring norms developers follow during day-to-day work. They were distilled from years of industry experience by experts and are now considered universal best practices: **Unit Testing, Code Quality, Code Review, Version Controlling, Continuous Integration.**

### Page 27 – Unit Testing
A unit test is small code that verifies a unit of your main code (class, function, module, API). It checks that the unit produces the expected output. Unit tests let developers refactor confidently — if all tests still pass, you haven't broken anything. Writing tests also drives **testable**, more **extensible** code. They are a verification mechanism and help catch integration issues early.

### Page 28 – Code Quality
Maintainable code requires quality. Code must be readable, follow engineering best practices, and follow language/domain conventions. Quality should be analyzed frequently using tools (static analysis). Watch for: code complexity, large methods/classes, meaningless identifiers, code duplication, and methods with too many parameters.

### Page 29 – Code Review
The single best way to improve code quality. The objective is to improve the **code**, not to criticize the **developer**. More eyes catch more issues. Rule of thumb: review under **400 LOC** at a time, at a rate of about **500 LOC/hour**, and don't review continuously for more than an hour. Forms: peer review, lead review, pair programming.

### Page 30 – Version Controlling
Code should always be version-controlled. Benefits: developers can change code freely without fear of breakage, multiple developers can collaborate on the same codebase, and you remove the single-point-of-failure of a "one machine" codebase. Use **branches** and **tags** to organize parallel work and releases.

### Page 31 – Continuous Integration (CI)
CI is a development practice: developers **check in code several times a day** to a shared repository, and each check-in is verified by an **automated build** (compilation + tests). This lets the team catch issues early — long-lived branches accumulate hidden conflicts that CI surfaces immediately.

### Page 32 – Thank You
Closing slide.

---

## Lecture 02 – Application Frameworks

(This lecture, despite its filename, is actually about **Version Controlling** — the second lecture in the SE3040 series, delivered by Mr. Aruna Ishara Gamage.)

### Page 1 – Title Slide
**SE3040 Application Frameworks – Lecture 02: Version Controlling**, delivered by Mr. Aruna Ishara Gamage. The lecture covers what version control is, why it matters, terminology, best practices, and the Git/GitHub distinction.

### Page 2 – Version Controlling (Agenda)
The lecture flow: (1) *What and why* — definitions and motivations, (2) *Terminology* — common vocabulary like commit, branch, merge, (3) *Best practices* — how to use VCS well in a team, (4) *GIT vs GITHUB* — distinguishing the tool from the hosting platform.

### Page 3 – WHAT? (Definition of Version Control)
Version control is the practice of **tracking and managing changes to software code**. Changes are identified by a **revision number**, and each revision records a **timestamp** and the **person who made the change**. Revisions can be **restored**, **compared**, and **merged**. In one line: *"management of multiple revisions of the same unit of information."*

### Page 4 – WHY? (Motivation)
Reasons to use version control: a **centralized source code repository** (everyone draws from one source of truth), **easier backups**, **easy collaborative development**, an **overview of changes** done to any file (audit trail), **access control** (who can read/write what), and assistance with **conflict resolution** when multiple people edit the same code.

### Page 5 – Benefits of Version Control
Five concrete benefits: **Security** (protects against accidental loss/corruption), **Clean History** (tracks all changes and authors), **Collaboration** (teams work simultaneously), **Branching & Merging** (feature work without breaking main), **Scalability** (works for tiny and huge projects equally).

### Page 6 – Version Control Terminology
Key vocabulary: **Repository** (central project storage), **Trunk / Master / Main Branch** (most stable version), **Stage** (mark files for tracking), **Commit** (snapshot of changes), **Merge** (combine branches), **Branch** (a parallel copy of code for features or bug fixes), **Merge Conflict** (conflicting changes that need manual resolution).

### Page 7 – Git: The Popular VCS
Git is a **distributed** version control system, meaning every client gets a complete clone with full history — in a disaster, the entire codebase can be restored from any clone. It is **free and open source**, supports **multiple branches/tags** (e.g., feature branches, release branches), is **faster than older systems** (it's a C program designed around Linux kernel development), supports **HTTP and SSH** protocols, and uniquely offers a **staging area**, **local commits** (commit without pushing), and **stashing** (temporarily store changes).

### Page 8 – Git vs GitHub
**Git** is a *version control system* — software that runs locally on your machine to track changes and support collaboration. **GitHub** is a *cloud-based hosting service* for Git repositories, providing a UI plus extras like issue tracking and CI/CD integration. Git is the engine; GitHub is one of many platforms built on top.

### Page 9 – GitHub Alternatives
**Git alternatives** (other VCS tools): **Fossil** (distributed VCS with built-in bug tracking and wiki), **Mercurial** (high-performance distributed VCS), **Subversion (SVN)** (centralized, common in legacy projects).
**GitHub alternatives** (other hosting): **GitLab** (CI/CD and DevOps integration), **Bitbucket** (Git and Mercurial, integrates with Atlassian tools), **AWS CodeCommit** (managed Git on AWS), **Azure Repos** (cloud repos for Azure).

### Page 10 – Git Commands (Overview)
Quick list of the most commonly used Git commands: `git init`, `git clone`, `git add`, `git commit`, `git push`. Reference link: Atlassian Bitbucket's basic-git-commands page.

### Page 11 – Basic Git Commands – Initializing, Cloning, Staging, Committing
**Initialization/Cloning**: `git init` creates a fresh repo; `git clone <url>` copies an existing remote repo.
**Staging/Committing**: `git add <file>` stages a specific file; `git add .` stages everything; `git commit -m "message"` commits with a message.

### Page 12 – Staging in Git (What and Why)
**Staging** is the step between modifying files and committing them — a middle area where you prepare changes. It matters because it lets you review changes before committing, group related changes into one commit, and commit only selected files (not everything that changed). Workflow: modify files → `git add` to stage → `git commit` to save.

### Page 13 – Staging vs. Committing
**Staging** prepares files for commit but doesn't save them permanently. **Committing** saves staged changes into the repository with a message.
Useful staging commands: `git add <file>` stages one file, `git add .` stages everything, `git status` shows what's staged, and `git reset <file>` unstages a file.

### Page 14 – Basic Git Commands – Branching, Merging, Remotes
**Branching & Merging**: `git branch <name>` creates a branch, `git checkout <name>` switches to one, `git merge <name>` merges another branch into the current one, `git branch -d <name>` deletes a branch (after merging).
**Remote work**: `git remote add origin <url>` links to a remote, `git push origin <branch>` pushes, `git pull origin <branch>` pulls, `git fetch` fetches without merging.

### Page 15 – Basic Git Commands – Undoing Changes
**Undoing**: `git reset --soft HEAD~1` undoes the last commit but keeps your changes (so you can recommit). `git reset --hard HEAD~1` undoes the last commit *and* discards the changes — destructive. `git checkout -- <file>` discards local changes in a file (revert to last committed version).

### Page 16 – Git Branching
Branching lets developers work on features separately, keeps the main branch stable, and supports many parallel branches. Standard pattern: never develop directly on main; create a feature branch, build there, then merge back.

### Page 17 – Pull Requests (PR)
A pull request is a request to merge changes from one branch into another. It is the formal mechanism for **code review** — others can see the diff, comment, and approve before merging. PRs are the quality-control gate before code lands in shared branches.

### Page 18 – Merge Conflicts (Definition)
A merge conflict happens when Git **cannot automatically combine** changes because two branches modified the same part of the same file in different ways. If changes don't overlap, Git merges automatically; if they do, Git flags a conflict and requires manual resolution.

### Page 19 – Merge Conflict Example (Scenario)
Alice and Bob both edit `index.html`. In her feature branch Alice writes `<h1>Welcome to Our Website!</h1>`, while Bob's main branch has `<h1>Welcome to My Website!</h1>`. Bob commits first. When Alice runs `git checkout main` and `git merge feature-branch`, Git detects the conflict and stops the merge so a human can decide.

### Page 20 – Merge Conflict Resolution (Identifying)
Use `git status` to find conflicted files. Git inserts conflict markers into the file:
```
<<<<<<< HEAD
<h1>Welcome to My Website!</h1>       # main branch (HEAD)
=======
<h1>Welcome to Our Website!</h1>      # feature branch
>>>>>>> feature-branch
```
`HEAD` is the current branch; below the `=======` is the incoming branch.

### Page 21 – Merge Conflict Resolution (Options)
Three options: **(1) Accept Current (HEAD)** — keep Bob's `My Website`. **(2) Accept Incoming (feature-branch)** — keep Alice's `Our Website`. **(3) Accept Both / Manual Merge** — combine into something like `<h1>Welcome to My Website! (Our Website!)</h1>`. Choosing wisely requires understanding which intent should win.

### Page 22 – Finalizing the Merge Resolution
After editing the file manually to fix the conflict markers: `git add index.html` (stage the fix), `git commit -m "Resolved merge conflict in index.html"`, `git push origin main`. The conflict is resolved and merged.

### Page 23 – Best Practices for Version Control
Use **meaningful commit messages**, never commit **sensitive data** (passwords, tokens), use `.gitignore` to exclude build artefacts and secrets, always work with the latest version of the file, **pull at least once per day** (especially with distributed VCS), **merge with the development branch daily** to avoid integration drift, always make sure code works before pushing (don't break others), and **follow a formal review process** when merging.

### Page 24 – Push to GitHub – Step 1: Create the Repo
Steps to push a local repo to GitHub. Step 1: on GitHub, click *New Repository*, give it a name (e.g., MyProject), choose Public/Private, **do not initialize with README** (it conflicts with an existing local repo), click *Create*. GitHub gives you a URL like `https://github.com/your-username/MyProject.git`.

### Page 25 – Push to GitHub – Steps 2 & 3: Navigate and Init
Step 2: open Git Bash and `cd` to your project folder. Step 3: if not yet a Git repo, run `git init` to initialize.

### Page 26 – Push to GitHub – Steps 4 & 5: Add and Commit
Step 4: check status with `git status`, then `git add .` to stage everything.
Step 5: `git commit -m "Initial commit"` to commit with a meaningful message.

### Page 27 – Push to GitHub – Step 6: Add Remote
Step 6: link your local repo to GitHub:
```
git remote add origin https://github.com/your-username/MyProject.git
```
or with a Personal Access Token embedded for private repos. First-time setup uses `git remote add origin <URL>`; to change later use `git remote set-url origin <URL>`.

### Page 28 – Push to GitHub – Step 7: Push
Step 7: rename the local branch to main and push with upstream tracking:
```
git branch -M main
git push -u origin main
```
`-u` sets the upstream so future `git push`/`git pull` don't need the branch argument.

### Page 29 – Clone a GitHub Repo – Steps 1 & 2
Step 1: find the repo on GitHub, click *Code*, copy the **HTTPS** URL like `https://github.com/your-username/repository-name.git`.
Step 2: open Git Bash on Windows or Terminal on Mac/Linux.

### Page 30 – Clone a GitHub Repo – Steps 3 & 4
Step 3: `cd` into the directory where you want the repo to live.
Step 4: clone. For public repos:
```
git clone https://github.com/your-username/repository-name.git
```

### Page 31 – Clone a GitHub Repo – Private Repo Auth
For private repos, GitHub requires authentication. Use a **Personal Access Token (PAT)** instead of a password:
```
git clone https://your-username:your-pat@github.com/your-username/repository-name.git
```
PATs replaced password-based HTTPS auth on GitHub years ago.

### Page 32 – Clone a GitHub Repo – Steps 5 & 6: Navigate and Verify
Step 5: `cd repository-name` to enter the freshly cloned folder.
Step 6: run `git status` to confirm the clone worked and see what state the working tree is in.

### Page 33 – GitHub Student Developer Pack
A reference to the **GitHub Student Developer Pack** — a free bundle of developer tools (cloud credits, IDE licenses, domains, etc.) for verified students. Students should sign up to access this.

### Page 34 – Git: Interactive Learning
Two recommended interactive tutorials: **[1] try.github.io** for fundamentals, and **[2] pcottle.github.io/learnGitBranching/** for an advanced visual branching demo.

### Page 35 – That's All Folks
Closing slide for Q&A.

---

## Lecture 03 – JavaScript

### Page 1 – Title Slide
**SE3040 – Application Frameworks, Lecture 03: JavaScript.** The lecture introduces the JavaScript language with a focus on the features most relevant to building modern web apps.

### Page 2 – Agenda
The lecture covers: an introduction to JS, classes and objects, how `this` behaves, function closures, callbacks, and promises. The order moves from language basics to the tricky async-handling that JavaScript is famous for.

### Page 3 – JavaScript Overview
JavaScript is an **interpreted** language. It is essentially **single-threaded** — although Web Workers can create new threads, the language model is single-threaded. It is **asynchronous** via the **Non-Blocking I/O (NIO)** model. It is **dynamically typed** (variables have no fixed type). It supports both **OOP and functional programming** (multi-paradigm). And it has an **eventing system** that manages its asynchronous operations — the event loop is at the heart of JS execution.

### Page 4 – Classes and Objects
Classically, a **constructor function** with the `new` keyword creates objects — a regular function called with `new` acts as a class. **ES6 introduced the `class` keyword**, though support varied initially across engines. You can also create objects with **object literals** (`{ key: value }`). JavaScript also supports **static methods and variables** attached to constructors/classes.

### Page 5 – `this` in JavaScript
`this` behaves differently from other languages and is one of JS's notorious gotchas. Inside an object's method, `this` refers to the object itself. In the **global context**, `this` is the **global object** (in browsers, `window`), unless in **strict mode** where it is `undefined`. If a method is passed to another object, `this` refers to *that* object when called, not the original — `this` is determined by **how a function is called**, not where it is defined. This is especially noticeable in callbacks and closures, where `this` can silently change.

### Page 6 – Closure
A **closure** is a function that returns another function — more precisely, an inner function that retains access to its enclosing function's scope even after the outer function returns. Closures **encapsulate variables**, restricting outside access. They are the canonical way to create **private variables** in JS, accessible only through specific methods that close over them.

### Page 7 – Callback
JavaScript uses asynchronous programming despite being single-threaded; **callbacks** and **promises** are the two main ways to handle async execution. A **callback** is a function passed as an argument to another function and executed later, usually when an async operation finishes. Sequentially nesting callbacks for chained async operations leads to **"callback hell"** — deeply indented, hard-to-read code.

### Page 8 – Promises (Introduction)
A **Promise** is an object representing the eventual completion (or failure) of an async operation. Think of a promise as a *placeholder* for a value you don't have yet but will receive in the future. A promise is always in one of three states: **Pending** (initial, operation hasn't finished), **Fulfilled** (operation succeeded, value is available), or **Rejected** (operation failed with an error).

### Page 9 – Promises (Mechanism)
Promises were introduced specifically to solve callback hell. They expose a set of methods — chiefly `.then()`, `.catch()`, `.finally()` — and a **chaining** mechanism so complex async flows can be expressed linearly instead of as nested callbacks.

### Page 10 – Activity (Promise Task)
**Task:** Write a function that returns a Promise which **resolves** if a condition (e.g., a number comparison) is true, and **rejects** if false. This is a basic exercise in creating promises with `new Promise((resolve, reject) => { ... })`.

### Page 11 – Activity (Repeat / Continued)
Same activity prompt repeated — likely a continuation slide showing a sample solution or providing space for student practice during class.

### Page 12 – Async/Await (Introduction)
`async/await` is **syntactic sugar** over Promises, introduced in **ES2017 (ES8)**. It lets you write async code that looks and behaves like synchronous code, dramatically improving readability. Adding `async` before a function declaration automatically makes that function return a Promise — even plain returned values are wrapped in a resolved Promise. Key rules: an async function always returns a Promise, returned values become the resolved value, and a thrown error becomes a rejected Promise.

### Page 13 – Async/Await (Usage)
The **`await`** keyword can only be used inside an `async` function. It **pauses execution** of the async function until the awaited Promise resolves, then returns the resolved value. Crucially, `await` *pauses the function* but **does not block the main thread** — other code keeps running. The value after `await` should usually be a Promise (though `await` works with any value, wrapping non-promises automatically).

### Page 14 – Practical Applications of Async JS
Real-world uses of async JavaScript: **AJAX / Fetch API** for HTTP requests, dynamic content updates without page reload, and working with external APIs. **Timers** like `setTimeout()`, `setInterval()`, and `requestAnimationFrame()` for delayed or repeated execution. **File operations and I/O** in Node.js — reading files, database queries, network requests — all use async patterns.

### Page 15 – Advanced Concepts in Async JS
Going deeper: **Microtasks vs Macrotasks** — promise callbacks (microtasks) have higher priority than `setTimeout` callbacks (macrotasks) in the event loop. **Error handling** — proper patterns to catch errors across callbacks, promises, and async/await (try/catch only works inside async functions). **Concurrent operations** — managing many async ops at once, cancellation patterns, avoiding race conditions. **Async iterators and generators** — `async function*` and `for await...of` enable advanced async control flow.

### Page 16 – Thank You
Closing slide.

---

## Lecture 04 – NodeJS

### Page 1 – Title Slide
**SE3040 – Application Frameworks, Lecture 04: NodeJS.** The lecture introduces Node.js — what it is, how it works, when to use it, its trade-offs, and its module/package ecosystem.

### Page 2 – Agenda
The lecture covers: NodeJS introduction, the event loop, use cases, advantages/disadvantages, package manager (npm), and core modules + file system. The structure moves from what Node is to how to build with it.

### Page 3 – Node.js (Introduction)
**Node.js** is a *runtime environment* that lets JavaScript run on the **server side**. It was created by **Ryan Dahl** to build fast, interactive web apps that need live updates (e.g., chat apps over WebSockets). It is **open-source, cross-platform**, and meant for **server-side and networking applications**. Its **event-driven, non-blocking I/O model** makes it lightweight and efficient, and ideal for **data-intensive, real-time** applications running across distributed devices.

### Page 4 – Event-Driven Model
Execution flow is determined by **events** rather than a fixed sequential order. The system listens for events and, when one occurs, runs a **callback function** (event handler) without blocking — making the system responsive and efficient. The three key components are the **event emitter** (something that fires events), the **event listener** (something that subscribes), and the **callback function** (what runs when the event fires).

### Page 5 – Event Loop
The **event loop** is the core mechanism in Node.js that lets it handle many operations concurrently without blocking. Long-running I/O is offloaded; when results come back, callbacks are queued and run on the main thread. This single-threaded loop is what makes Node fast and efficient for real-time applications even though it does not use OS threads per request.

### Page 6 – Use Cases (Strengths & Limits)
Node is **not ideal for CPU-intensive** heavy computation — long computations block the event loop. It is **excellent for fast, scalable network applications** and can handle a huge number of simultaneous connections with high throughput. Importantly, Node **does not spawn a new thread per connection** (which would exhaust memory); instead it handles them all on a single thread using non-blocking I/O. Node has demonstrated **over 1 million concurrent connections**. One caveat: an uncaught error that bubbles up to the core event loop will **crash the entire process**.

### Page 7 – Use Cases – Activity
**Activity prompt:** discuss and write down a real-world success story of companies or projects that have effectively used Node.js. (Examples one might list: Netflix, LinkedIn, Uber, PayPal, Walmart.)

### Page 8 – Use Cases (Where Node Shines)
Five canonical use cases: **I/O-bound applications**, **data streaming applications**, **data-intensive real-time applications**, **JSON APIs** (REST backends), and **Single Page Applications (SPAs)** where the server provides APIs to a JS front end.

### Page 9 – Advantages
**Single language end-to-end** — JavaScript on client and server, simplifying team skills. **Easy to scale** both horizontally (more nodes) and vertically (more resources). **Improved performance** because the **V8 engine** compiles JS directly to machine code. **Caching** of modules in memory after first use further improves runtime speed. **Easily extensible**, with strong tooling for unit testing. The **npm** package manager and its large module ecosystem are major advantages.

### Page 10 – Disadvantages
Even with many libraries, the number of **truly robust libraries** is comparatively low. **Not suitable for CPU-intensive tasks** (single-threaded blocking). The **asynchronous programming model** is more complex to learn than synchronous code.
*Exercises:* (1) What are robust libraries? (2) Which Node libraries qualify as robust? (3) Why is the count of robust libraries lower than the total module count?

### Page 11 – Node Package Manager (npm)
**npm** provides reusable Node components via an online repository. It has **built-in dependency management**, **versioning**, and a **scripting** mechanism. **Global installations** are system-wide; **local installations** are scoped to the project. By default, dependencies install into the **`node_modules`** directory. The **`package.json`** file in the project root holds project info — name, version, author, repo, required Node version, scripts, dependencies, etc.

### Page 12 – Node Package Manager (cont.)
Notes on **version range syntax** (e.g., `^1.2.3` allows compatible minor updates, `~1.2.3` allows compatible patch updates). There are **two dependency categories**: **dependencies** (needed at runtime, e.g., `express`, `mongoose`) and **devDependencies** (needed only during development, e.g., `jest`, `nodemon`). Production installs can skip devDependencies.

### Page 13 – Core Modules
A **module** is a reusable block of code; in Node, each file is treated as a separate module. **Three types**: **Core/Built-in** modules ship with Node (`fs`, `path`, `http`, `os`), **Local modules** are files you create, **Third-party modules** are installed via npm (e.g., `npm install chalk`). **Why modules?** — *Reusability* (use same code in many places), *Avoid conflicts* (each module has its own scope), *Maintainability* (easier to find and fix bugs).

### Page 14 – Core Modules (Mechanics)
Outlines how modules work — `require()` (CommonJS) or `import` (ES Modules) loads a module, and `module.exports` (or `export`) exposes values. Also covers creating your own local modules: write a file with `module.exports = ...`, then require it from another file with a relative path.

### Page 15 – File System (`fs` Module)
The **`fs` module** is one of the most-used core modules, providing access to the file system: **read files, write files, delete files, create directories**. Use cases: **Data Persistence** — variables only live in RAM, so files persist across runs. **Configuration Management** — settings that change without recompiling. **Logging and Debugging** — track what happens in your application. **File uploads/processing** — handle user-generated content.

### Page 16 – Example
**Example/exercise:** create a sample Node project, inspect the folder structure and `package.json`, and run a Hello World program. Typically `npm init`, then a tiny `index.js` that prints to console, run with `node index.js`.

### Page 17 – Thank You
Closing slide.

---

## Lecture 05 – REST and ExpressJS

### Page 1 – Title Slide
**SE3040 – Application Frameworks, Lecture 05: RESTful Web Services and Express JS.** The lecture wires together four core ideas — 3-tier architecture, MVC, REST, and Express — to show how a modern web app is built.

### Page 2 – Agenda
The lecture covers: Introduction, 3-tier architecture, Application Layer, MVC architecture, REST service, and Express JS. The flow goes from system-level architecture down to the framework that implements it.

### Page 3 – Introduction
As applications grow, responsibilities must be separated to improve **maintenance, testing, and scalability**. Modern apps use architectural patterns to achieve this. Today's lecture connects four ideas: **3-Tier Architecture** (overall system design), **MVC** (internal organization pattern), **REST** (communication style), and **Express.js** (the implementation framework).

### Page 4 – Three Tier Architecture (Section Divider)
Section divider introducing the **3-tier architecture** model — Presentation, Application, and Data layers — and how it organizes large applications into separable layers.

### Page 5 – Why 3-Tier Architecture?
Four reasons: **Independent Infrastructure** — each layer runs on its own infrastructure, improving performance and maintainability. **Parallel Development** — different teams can work on different tiers simultaneously. **Scalability** — each layer can be scaled independently without disturbing others. **Enhanced Security** — isolating data and logic from the frontend reduces attack surface compared with 2-tier designs.

### Page 6 – Presentation Layer
The **Presentation Layer** (client-side / frontend) is what users see and interact with. Its goal is a smooth UX with responsive, accessible interfaces. **Modern frameworks/libraries**: React.js, Angular, Vue.js. **Legacy frontend tech**: jQuery, AJAX (Asynchronous JavaScript and XML).

### Page 7 – Application Layer
The **Application Layer** (server-side / backend) handles business logic, processes requests, and manages data. It is the intermediary between the Presentation Layer and the Database Layer. Implementation technologies include: **Java** (Spring, Spring Boot), **Node.js** (Express.js, Koa), **Python** (Django, Flask), **PHP** (Laravel, Symfony), **.NET** (ASP.NET Core).

### Page 8 – MVC Architecture in 3-Tier (Section Divider)
Section divider — MVC operates *within* the Application Layer of a 3-tier system. The three concepts (3-tier, MVC, REST) work at different levels: 3-tier is system architecture, MVC is the internal organization of the application tier, and REST is the communication style between tiers.

### Page 9 – MVC Architecture (Definition)
**MVC (Model-View-Controller)** is a software design pattern for organizing application code. It separates the app into three interconnected components, each with specific responsibilities: Model (data + business rules), View (presentation/format), and Controller (request handling and coordination).

### Page 10 – MVC Architecture (Responsibilities Table)
**Model**: business logic, data validation, database operations, business rules enforcement. **Controller**: send/receive HTTP requests, validate request data, call Model methods, call View to format the response. **View**: format data for presentation, structure API responses, hide sensitive data, create a consistent response format.

### Page 11 – Presentation ↔ Application Layer (REST API Flow)
A typical REST API communication scenario: **User Action** — user submits a form on the frontend (e.g., signup). **Frontend Request** — frontend sends a POST request with the form data. **Backend Processing** — backend validates data, updates the database, processes business logic. **Backend Response** — backend sends success/failure response. **Frontend Update** — frontend updates the UI dynamically (e.g., "Registration Successful!").

### Page 12 – Application Layer: APIs (Definition)
**API (Application Programming Interface)** is a software interface that lets two or more applications communicate. It is a bridge between software components, enabling seamless integration. APIs **abstract complexity**, letting developers interact with services without knowing internal implementation. An API also defines a **contract of services** — how applications should request and exchange data.

### Page 13 – Application Layer: APIs (Benefits)
**Standardized Communication** — uses standard protocols (HTTP/HTTPS, WebSockets, gRPC), with JSON or XML responses. **Encapsulation & Abstraction** — hides complex implementation; developers don't need to understand the database queries or backend logic. **Reusability & Efficiency** — APIs let apps reuse functionality, reducing duplicated code; e.g., a Stripe payment API can be integrated into many apps without writing payment logic from scratch.

### Page 14 – Application Layer: APIs (Types)
Different API styles: **REST API** — uses HTTP methods (GET/POST/PUT/DELETE), stateless, resource-oriented, JSON/XML responses, common for web/mobile/cloud services. **SOAP API** — older XML-based protocol. **RPC (Remote Procedure Call)** — exposes remote functions. **WebSockets API** — bi-directional persistent connection for real-time. **GraphQL API** — query language with a single endpoint and flexible payloads.

### Page 15 – REST (Definition)
**REST (Representational State Transfer)** is an **architectural style** for building web services. A web service is a way for applications to exchange data — machine-to-machine communication over the web. REST defines a set of **constraints** for how clients and servers should communicate, using **HTTP** as the underlying protocol.

### Page 16 – REST – Resources
In REST, **everything is a resource** (e.g., user, product, order). Each resource has a **unique URI** like `/api/users/123`. Clients use HTTP **methods** to act on resources: **GET** to retrieve, **POST** to create, **PUT** to update, **DELETE** to remove. The combination of URI + method expresses the action.

### Page 17 – REST – HTTP Request and Response (Anatomy)
Diagrams of an HTTP **Request Message** (method, URL, headers, body) and an HTTP **Response Message** (status code, headers, body). Together they make the request/response cycle.

### Page 18 – REST Example – Create Student
Example: Student Management API at `https://api.school.com/students`. **Create student** uses POST with the student data in the request body, returning the created resource. This is a classic REST endpoint pattern.

### Page 19 – REST Example – Get All Students
**Get all students:** `GET https://api.school.com/students` returns an array of student objects:
```json
[
  { "id": 101, "name": "Sanduni", "age": 23 },
  { "id": 123, "name": "Perera", "age": 26 }
]
```

### Page 20 – REST Example – Update (Full)
**Update entire resource:** `PUT https://api.school.com/students/123` with the full updated body `{ "name": "Kasun Perera", "age": 26 }`. The response includes a confirmation message plus the updated record. `PUT` is for **full replacement**.

### Page 21 – REST Example – Partial Update
**Partial update:** `PATCH https://api.school.com/students/123` with only the fields to change, e.g., `{ "age": 27 }`. Server updates only those fields. `PATCH` is for **partial modifications**, unlike PUT.

### Page 22 – REST Example – Delete
**Delete:** `DELETE https://api.school.com/students/123` removes the resource. Response confirms the deletion. (Note the slide reuses "Student age updated successfully" — likely a typo in the slide.)

### Page 23 – REST – HTTP Status Codes (Classes)
HTTP status codes are **3-digit numbers** indicating the status of a client request. The first digit classifies the response: **1xx Informational**, **2xx Success**, **3xx Redirection**, **4xx Client Error**, **5xx Server Error**. The last two digits give specifics.

### Page 24 – REST – Common HTTP Codes
Commonly used codes to memorize: **200 OK** (Success), **201 Created**, **202 Accepted**, **204 No Content**, **301 Moved Permanently**, **400 Bad Request**, **404 Not Found**, **500 Internal Server Error**, **502 Bad Gateway**, **503 Service Unavailable**. Each carries a specific meaning for the client to act on.

### Page 25 – Express JS (Introduction)
**Express.js** is a web application framework for Node.js. It provides tools to build web servers and APIs. It is **minimal and flexible** — it doesn't impose much structure. The lecture frames it as: the **construction kit** to build your app, the **toolbox** with what you need, and the **foundation** on which you implement 3-Tier, MVC, and REST patterns.

### Page 26 – Express JS in 3-Tier and MVC
**Express operates in Tier 2 (Application Tier)** and connects Tier 1 (frontend) with Tier 3 (database). It provides: **HTTP server functionality** (listens for requests), **Middleware** (request processing), **DB connection capability** (connects to Tier 3), and **Response handling**. Mapping to MVC: `express.Router()` → **Controller**, JavaScript Classes (e.g., Mongoose models) → **Model**, `res.json()` → **View**.

### Page 27 – Express JS – Routing
**Routing** determines how the app responds to client requests for specific URLs and HTTP methods. The slide uses a **hotel receptionist analogy**: customer walks in (client request) → receptionist asks where to go (router checks URL) → customer says room 305 (`/room/305`) → receptionist directs them (route handler executes) → customer reaches the room (response is sent back).

### Page 28 – Express JS – Basic Routing Syntax
Basic syntax: `app.METHOD(PATH, HANDLER)`. **app** is the Express instance, **METHOD** is the HTTP method (get/post/put/delete), **PATH** is the URL, **HANDLER** is the function that runs when the route matches. Example:
```javascript
app.get('/about', (req, res) => {
  res.send('This is the about page');
});
```

### Page 29 – Express JS – Middleware
**Middleware** is a function that runs **between** the client request and the server response. It can modify the request, modify the response, or terminate the cycle. There are three categories: **built-in middleware** (handle requests, parse data, serve static files), **third-party middleware** (logging, authentication, caching), and **custom middleware** (write your own to handle specific app needs).

### Page 30 – Express JS – Working with Databases
Express can talk to **SQL** databases (MySQL, PostgreSQL) and **NoSQL** databases (MongoDB). Connect via a **database driver** or an **ORM** (Object-Relational Mapping) library — **Sequelize** for SQL or **Mongoose** for MongoDB. Queries use SQL or a DB-specific query language. ORMs provide a higher-level interface that simplifies CRUD operations.

### Page 31 – Express JS – REST APIs
Express is well-suited for REST APIs because of its routing + middleware. To build a REST API: define routes matching HTTP methods and resources; use middleware for **input validation**, **authentication**, **rate limiting**; follow REST principles — meaningful URIs, correct HTTP status codes, consistent interface.

### Page 32 – Tutorial – Build a Simple Express Backend
Case study: **Student Management System**. Build an API that supports: add a new student, get all students, get a student by ID, update student info, delete a student. This is the canonical CRUD exercise to put together everything in the lecture.

### Page 33 – Thank You
Closing slide.

---

## Lecture 06 – NoSQL and MongoDB

### Page 1 – Title Slide
**SE3040 – Application Frameworks, Lecture 06: NoSQL and MongoDB.** Introduces non-relational databases, the trade-offs involved, the major NoSQL families, and MongoDB as the document-store example for this course.

### Page 2 – Agenda
The lecture covers: fundamentals of NoSQL, the CAP theorem, types of NoSQL databases, an introduction to MongoDB, and how to integrate MongoDB with Express. It proceeds from theory to practical integration.

### Page 3 – Fundamentals of NoSQL
**NoSQL ("Not Only SQL")** is a modern database approach distinct from traditional relational systems. It is designed to store, retrieve, and manage large volumes of **unstructured, semi-structured, or rapidly changing** data efficiently. Unlike relational databases with fixed schemas, NoSQL offers **flexibility, scalability, and high performance** for modern data-intensive applications like social networks, IoT systems, and real-time analytics.

### Page 4 – NoSQL vs Relational DB (Comparison Table)
Side-by-side comparison: **Structure** — relational is structured with table relationships; NoSQL is flexible with dynamic structures. **Query language** — relational uses SQL; NoSQL uses various (JSON/BSON). **Consistency** — relational enforces strict consistency; NoSQL often favors availability + partition tolerance. **Transactions** — relational handles complex transactions well; NoSQL is often faster and more scalable. **Purpose** — relational for structured data + complex queries, NoSQL for unstructured + scale. **Scaling** — relational scales vertically (limited); NoSQL scales horizontally. **Examples** — MySQL, Oracle, MS SQL Server vs. MongoDB, Cassandra, Couchbase. **Cost** — relational is relatively expensive; NoSQL relatively cheap. **Use cases** — relational for financial/transactional/inventory systems; NoSQL for big data, IoT, content management, cloud computing.

### Page 5 – NoSQL vs Relational – Real-World Example
A *Book* record. In a **relational database** it is normalized across multiple tables — `Books` (ISBN, Title, Edition), `Authors` (AuthorID, Author Name), and a join table `Author-ISBN` linking them. Relations are enforced with primary/foreign keys, optimized for storage with referential integrity. In a **NoSQL document database**, the same book is one JSON document with ISBN, Title, Edition, Author Name, and AuthorID embedded as attributes — optimized for intuitive development and horizontal scalability.

### Page 6 – NoSQL Key Characteristics
**Schema-less Structure** — no predefined tables/columns required. **Horizontal Scalability** — expand by adding more servers, not upgrading hardware. **High Performance** — fast reads/writes, low latency. **Flexible Data Models** — supports document, key-value, column, and graph types. **Distributed and Fault-Tolerant** — designed for multi-node operation with automatic replication and recovery.

### Page 7 – Types of NoSQL
Five main NoSQL families: **Document-Based**, **Key-Value Stores**, **Graph Databases**, **Column Family Stores**, and **In-Memory** databases. Each is suited to different data shapes and access patterns.

### Page 8 – Document-Based Databases
Store data in **structured documents** (JSON, BSON, or XML) instead of rows/columns. Each document holds key-value pairs and can have a flexible structure — different documents in one collection can have different fields. **Schema-less** by design. Hierarchical storage supports **nested structures**. **Easy mapping** between application objects and DB records. **Examples**: MongoDB, CouchDB, Firebase Firestore.

### Page 9 – Key-Value Stores
The **simplest** NoSQL type. Data is stored as **key-value pairs**, retrieved by a unique key. Values can be strings, JSON objects, or binary. **Extremely fast** read/write. Ideal for **caching and session management**. **Highly scalable and distributed** by design. Simple data model. **Examples**: Redis, Amazon DynamoDB, Riak. Example data: `"user123"` → `{"name": "Sanduni", "email": "sanduni@gmail.com"}`; `"session456"` → `{"token": "abc123xyz", "expires": "..."}`.

### Page 10 – Column-Family Databases
Also called **wide-column stores**. Organize data into **columns and column families** rather than rows and tables. Each column family has rows identified by a key, but each row can have a different set of columns — efficient for **analytical queries and sparse datasets**. Optimized for high-performance read/write of large datasets. **Examples**: Apache Cassandra, HBase, ScyllaDB.

### Page 11 – Graph Databases
Store data in **nodes (entities)** and **edges (relationships)**, ideal for **highly connected data**. Each node and edge can carry attributes. They use query languages like **Cypher** (Neo4j) or **Gremlin** to traverse relationships efficiently. Designed for relationship-heavy data and intuitive visualization (think social networks, fraud detection, recommendations). **Examples**: Neo4j, Amazon Neptune, ArangoDB.

### Page 12 – Exercise: Column-Family + Graph
**Exercise prompt**: research more about Column-Family databases and Graph databases on your own. The lecture leaves this for self-study.

### Page 13 – Exercise: Advantages and Limitations
**Exercise prompt**: discuss the advantages and limitations of NoSQL databases. (Advantages: scalability, flexibility, speed. Limitations: weaker consistency, less mature transactions, varied query languages.)

### Page 14 – CAP Theorem
Explains the **trade-offs in distributed databases**. A distributed system can guarantee at most **two of three** properties: **Consistency** (every read sees the most recent write — all nodes show the same data), **Availability** (every request gets a response, even if some nodes are down), **Partition Tolerance** (the system continues to function even when communication between nodes fails or is delayed). In practice, partition tolerance is required for distributed systems, so the real trade-off is C vs A.

### Page 15 – MongoDB (Introduction)
**MongoDB** is a popular **NoSQL, document-oriented** database designed to store and manage large data volumes flexibly, scalably, and performantly. It uses **JSON-like documents** stored internally as **BSON (Binary JSON)** for efficiency. Ideal for unstructured or semi-structured data. Developed by **MongoDB Inc.**, first released in **2009**, and now among the most widely used NoSQL databases worldwide.

### Page 16 – MongoDB Key Characteristics
**Document-Oriented Storage** — data is in JSON-like documents containing key-value pairs (instead of rows/columns). **Schema-Less Design** — documents in one collection can have different structures, ideal for evolving apps. **High Scalability** via **sharding** (horizontal distribution across servers). **High Availability** via **replication** (Replica Sets — multiple copies of data for fault tolerance).

### Page 17 – MongoDB Data Structure (Hierarchy)
Four levels: **Database** — top-level container for collections (e.g., `UniversityDB`). **Collection** — a group of related documents, like a table in RDBMS (e.g., `Students`). **Document** — an individual record in JSON/BSON (e.g., `{"name": "Sanduni", "age": 27}`). **Field** — a key-value pair inside a document (e.g., `"name": "Sanduni"`).

### Page 18 – MongoDB Common Operations
Four CRUD operations in MongoDB Query Language: **Insert** — `db.students.insertOne({name: "Sanduni", age: 25})`; **Find** — `db.students.find({city: "Wattala"})`; **Update** — `db.students.updateOne({name: "Sanduni"}, {$set: {age: 26}})`; **Delete** — `db.students.deleteOne({name: "Sanduni"})`. Note operators are prefixed with `$` (e.g., `$set`).

### Page 19 – MongoDB Common Operations – Examples (Exercises)
Three exercises: (1) Find all docs in `customers` where `country: "Sri Lanka"` and `loyaltyPoints > 500`, sorted by `lastPurchaseDate` descending. (2) Update `loyaltyPoints` to `0` in the `funds` collection where `status: "expired"`. (3) Delete all docs from `logs` where `severity: "low"` AND `createdAt` is older than 30 days, assuming `createdAt` is ISODate.

### Page 20 – Tutorial: Connecting MongoDB with Backend Server
Tutorial slide for the live demo — typically uses **Mongoose** (an ODM) in an Express app: install with `npm install mongoose`, `mongoose.connect(URI)`, define a schema, then use the model's methods (`Model.find`, `Model.create`, etc.) inside route handlers.

### Page 21 – Thank You
Closing slide.

---

## Lecture 08 Part 01 – ReactJS

*(Slide title says "Lecture 07" but this file is labeled Lecture 08 in the SE3040 course materials — it is the React introduction lecture.)*

### Page 1 – Title Slide
**SE3040 – Application Frameworks, Lecture 07/08: ReactJS Part 01.** The first of two React lectures covering frontend foundations, the React mental model, components, props, state, lifecycle, hooks, state management basics, and build tools.

### Page 2 – Agenda
The 12-item agenda: (1) Intro to Frontend Development, (2) Web Foundations (HTML/CSS/JS), (3) DOM & Virtual DOM, (4) Introduction to React, (5) React Components & JSX, (6) Props and State, (7) Component Lifecycle, (8) Event Handling, (9) Hooks (useState, useEffect), (10) State Management Basics, (11) Build Tools (Babel, Webpack, Vite), (12) Setting Up a Modern React Project.

### Page 3 – What is Frontend Development?
Frontend development is the process of creating the **visual and interactive layer** of a web application that users directly interact with. It involves designing how the app looks, making it interactive, ensuring it is responsive and accessible, and creating a smooth user experience. Frontend runs **entirely on web browsers** (Chrome, Firefox, Safari, Edge).

### Page 4 – Role of a Frontend Developer
A frontend developer focuses on: building user interfaces, ensuring mobile responsiveness, implementing animations and transitions, integrating with backend APIs, managing browser compatibility, optimizing performance, enhancing accessibility (WCAG standards). Example tasks: navigation menus, forms and input validation, rendering data from the backend, building SPA components with React, Angular, or Vue.

### Page 5 – Why Frontend Development is Important
Frontend is the **first impression** of any application. It determines **usability and user satisfaction**, impacts **user engagement**, influences **conversion rate** in business apps, and affects **brand identity and visual communication**. Technically: efficient UI reduces server load, enhances app responsiveness, and enables dynamic, real-time updates. Apps like Facebook, Gmail, and YouTube depend on powerful frontend engineering.

### Page 6 – Frontend vs Backend
**Frontend (client-side)** runs in the browser; handles UI, animations, events, forms; focuses on layout design, responsiveness, user interaction, accessibility. **Backend (server-side)** runs on servers; handles business logic, data processing, authentication, APIs, and databases. Real-world: on YouTube, **frontend** = videos, buttons, search box; **backend** = storing videos, user accounts, recommendations.

### Page 7 – Frontend Has Two Broad Areas
**UI/UX Design** focuses on visual layout, color theory, typography, user navigation, accessibility (A11Y), and HCI principles; tools include Figma, Adobe XD, and Canva. **Frontend Engineering** focuses on HTML/CSS/JS, frameworks (React/Angular/Vue), optimization, build tools (Vite/Webpack), testing tools (Jest, React Testing Library), and DevOps (CI/CD for frontend).

### Page 8 – The Frontend Technology Stack
Five buckets: **Core Languages** — HTML5, CSS3, JavaScript (ES6+); **Frameworks & Libraries** — React, Angular, Vue; **Styling Tools** — Tailwind CSS, Bootstrap, Material UI, Sass/Less; **Build Tools** — Vite, Webpack, Parcel; **Version Control** — Git, with GitHub/GitLab/Bitbucket as hosts.

### Page 9 – Types of Frontend Applications
Three types: **Static Websites** — pure HTML+CSS, no dynamic content (portfolios, brochure sites). **Dynamic Websites** — JS-based interactivity, forms, dynamic data (news sites, blogs). **Single Page Applications (SPA)** — the whole app loads once and new content renders via JS, giving a fast, app-like experience (Facebook, Gmail, Twitter Web App) using React/Vue/Angular.

### Page 10 – The Need for Frameworks Like React
Traditional frontend development had challenges: hard to manage complex UIs, slow DOM updates, unmaintainable code, no structured component system, limited reusability. **React solves these** with components, the Virtual DOM, state management, hooks, and a declarative programming model.

### Page 11 – Web Foundations Overview
Three core technologies underpin any frontend (including React): **HTML** for structure (layout and elements — headings, paragraphs, forms, images, buttons), **CSS** for styling (colors, fonts, spacing, layout, responsiveness), and **JavaScript** for behavior (events, logic, API calls, dynamic updates).

### Page 12 – HTML (Structure)
HTML provides the **skeleton** of a web page. It uses **tags** to organize content into headings, paragraphs, images, lists. **Semantic HTML** improves SEO and accessibility. Example: `<h1>Welcome</h1> <p>This is my website</p>`. In React, you write HTML-like syntax using JSX.

### Page 13 – CSS (Styling & Layout)
CSS controls how HTML elements look and adapt across screen sizes. CSS handles colors, fonts, spacing; layout via **Flexbox & Grid**; animations and transitions; responsive design for mobile/tablet. Example: `button { background: blue; color: white; }`. React integrates well with CSS frameworks like Tailwind, MUI, and Bootstrap.

### Page 14 – JavaScript (Interactivity & Logic)
JavaScript brings the page to life: click events, form validation, API calls (fetching from backend), modifying the DOM dynamically, running logic in the browser. Example: `document.getElementById("btn").onclick = () => alert("Clicked!");`. React is built on JavaScript and makes UI updates easier via components and the Virtual DOM.

### Page 15 – What is the DOM?
The **DOM (Document Object Model)** is the browser's internal representation of your web page. It represents HTML as a **tree structure**, where each element is a **node**. JS can read, modify, create, or delete elements via the DOM. React ultimately interacts with the DOM through JSX (under the hood).

### Page 16 – Why DOM Exists?
The browser converts HTML into the DOM so it can **render content visually**, **process styling** (CSS), **handle events** (click, scroll, input), and **update content** when JS modifies the page. The DOM is what makes dynamic pages possible.

### Page 17 – DOM Manipulation with JavaScript (Traditional Way)
JS modifies the DOM directly: e.g., `document.getElementById("title").innerText = "Updated Title";`. Problems at scale: repeated DOM access is slow, the browser must recalculate layout, UI gets janky for large apps, code is hard to maintain, and inconsistent UI state becomes a risk.

### Page 18 – What is the Virtual DOM?
The **Virtual DOM (VDOM)** is a lightweight JavaScript representation of the actual DOM. React keeps a copy of the UI in memory; updating the VDOM is faster than updating the real DOM; React uses the VDOM to decide **when and what** to update. Flow: Actual DOM (slow) ↔ Virtual DOM (lightweight copy) ↔ React Components (JSX).

### Page 19 – DOM vs Virtual DOM
**Nature**: real browser structure vs JS object representation. **Update Speed**: slow vs fast. **Re-render**: whole page / large sections vs only changed nodes. **Efficiency**: low for large UIs vs very high. **Used by**: the browser vs React.

### Page 20 – Evolution of Frontend Development
A graphical history slide tracing the journey from static HTML through jQuery/AJAX to modern component frameworks like React. Highlights how each generation solved limitations of the previous one — leading to today's component-based, reactive architectures.

### Page 21 – ReactJS (Section Divider)
Section divider transitioning from frontend fundamentals to React-specific content.

### Page 22 – Introduction to React
**React** is a JavaScript **library** for building modern, interactive user interfaces. Developed and maintained by **Meta (Facebook)**. Used for **Single Page Applications**. Represents the **View** layer in MVC. Ideal for large apps that update without reloading. Supports multiple platforms: **ReactJS** (web), **React Native** (mobile), **React 360 / React VR** (VR/AR). Focuses on speed, simplicity, scalability. Examples: Facebook, Instagram, WhatsApp Web, Netflix UI.

### Page 23 – Why React?
React solves modern UI challenges via: **Fast Rendering (Virtual DOM)** — only changed UI parts update; **Component-Based Architecture** — UI built like LEGO blocks, reusable and maintainable; **Declarative UI** — you describe *what* the UI should look like, React figures out *how*; **One-Way Data Flow** — predictable behavior, easy debugging; **Cross-platform** — React.js for web, React Native for mobile, React VR for VR.

### Page 24 – JSX (React Syntax)
**JSX = JavaScript XML**. Features: write HTML-like syntax inside JavaScript, easy to read/write, supports dynamic JS expressions, **compiled by Babel** into pure JavaScript, **prevents XSS** (auto-escapes), supports expressions inside `{}`, easier maintenance. Example: `const element = <h1>Welcome to React</h1>;`. JSX is the foundation of building React UI.

### Page 25 – JSX Rules + Render Steps
**JSX Rules**: must return **one parent element** (`<div>...</div>`), use `className` instead of `class` (because `class` is a JS reserved word), embed JS expressions in `{}`, must **close all tags** (even self-closing like `<img />`), no `if` directly inside JSX → use a ternary. **How React Renders**: (1) component returns JSX, (2) Babel converts JSX to JS, (3) React creates the Virtual DOM, (4) React compares new VDOM with old, (5) only changed UI updates in the real DOM.

### Page 26 – React File Structure
Typical layout: `/src` holds main development files; `/components` holds reusable UI pieces; `App.jsx` is the main app component; `index.jsx` mounts the app to the DOM. This separation supports modular, maintainable codebases.

### Page 27 – React Components
**Components** are the building blocks of every React UI. They make UI **modular and reusable**, each has its own structure/logic/styling, and they simplify large app development. Two types: **Functional Components** (modern standard) and **Class Components** (older React). Everything you see on a React screen can be broken down into components.

### Page 28 – Types of Components
**Functional Components** (modern, recommended): simple JS functions, use **Hooks** like `useState` and `useEffect`, easy to read and maintain.
**Class Components** (older): use `class` syntax, have lifecycle methods, still important for legacy projects.

### Page 29 – What Are Props?
**Props = "properties"**. Allow data to flow from **parent → child** components. Key traits: **read-only/immutable** (cannot be changed by the child), make components **reusable**, passed similarly to HTML attributes. Use cases: display dynamic content, customize components, pass callback functions.

### Page 30 – Props (Example)
**Parent**: `<App><Welcome name="WMT" /></App>`.
**Child**: `function Welcome(props) { return <h1>Hello, {props.name}</h1>; }`.
**Output**: `Hello, WMT`. Why props matter: they enable configurable components like `<Button text="Save" color="green" />` and `<Button text="Cancel" color="red" />` — same component, different behavior, fully reusable UI.

### Page 31 – What is State?
**State** = data that changes over time inside a component. React **re-renders the UI** whenever state changes. Examples: toggle button, dropdown open/close, logged-in user, counter value, API response data, form inputs. State is what makes React components **interactive**.

### Page 32 – State (Example)
A counter example: `useState(0)` initializes state to 0; `setCount` updates it; the UI **re-renders automatically** when state changes. The destructuring pattern `const [count, setCount] = useState(0)` is the canonical form.

### Page 33 – State (Rules) + Callbacks
**Rules**: (1) Never modify state directly (`count = count + 1` ✗, `setCount(count + 1)` ✓). (2) State updates are **asynchronous**. (3) Every state change triggers a **re-render**. (4) Put **minimal required data** in state — avoid storing values that can be calculated.
**Callback Pattern**: child-to-parent communication is done by passing functions as props from the parent.

### Page 34 – Component Lifecycle (Phases)
React components go through three main phases: **Mounting** (component created and inserted into the DOM), **Updating** (triggered when state or props change), **Unmounting** (component removed from the DOM). React provides **lifecycle methods** (class components) and **hooks** (functional components) to run code at each stage.

### Page 35 – Mounting Phase (Class Components)
Methods that run when a class component first appears: **`constructor(props)`** — initialize state, bind event handlers, runs before render. **`render()`** — returns JSX, must be pure (no side effects). **`componentDidMount()`** — runs after the component is added to the DOM; good for fetching API data, subscribing to events, initializing timers.

### Page 36 – Updating Phase (Class Components)
Triggered when props or state change: **`shouldComponentUpdate(nextProps, nextState)`** — controls re-rendering; returning `false` avoids unnecessary renders (performance). **`render()`** — re-renders UI with updated state/props. **`getSnapshotBeforeUpdate(prevProps, prevState)`** — captures info from the DOM before update (useful for scroll position, animation); its return value is passed to componentDidUpdate. **`componentDidUpdate(prevProps, prevState, snapshot)`** — runs after the update; good for DOM updates, new API calls, acting on the snapshot.

### Page 37 – Unmounting Phase (Class Components)
**`componentWillUnmount()`** — runs right before the component is removed from the DOM. Used for **cleanup**: remove event listeners, stop timers, cancel network requests, clean up subscriptions. Failing to clean up causes memory leaks.

### Page 38 – Functional Components Lifecycle (useEffect)
Functional components replace lifecycle methods with **`useEffect`**:
- **Mount + Update**: `useEffect(() => { ... });` — runs every render
- **Mount only**: `useEffect(() => { ... }, []);` — empty dependency array
- **Unmount (Cleanup)**: `useEffect(() => { return () => { ... }; }, []);` — returned function runs at unmount
- **Update only (specific state)**: `useEffect(() => { ... }, [count]);` — runs when `count` changes

### Page 39 – React Component Lifecycle (Detailed)
Recap of class lifecycle methods: **`componentDidMount()`** for initialization/API calls after mount; **`componentWillUnmount()`** for cleanup before unmount; **`shouldComponentUpdate(nextProps, nextState)`** to control re-render; **`getDerivedStateFromProps(props, state)`** — static, runs before render on mount and updates, returns object to update state based on new props; **`getSnapshotBeforeUpdate(prevProps, prevState)`** — captures DOM info before commit; **`componentDidUpdate(prevProps, prevState, snapshot)`** — post-update logic. All can be represented via `useEffect()` in functional components.

### Page 40 – Mapping Class Methods to useEffect
**`constructor()`** → `useState()`. **`componentDidMount()`** → `useEffect(() => {}, [])`. **`shouldComponentUpdate()`** → `React.memo()`, `useMemo`, `useCallback`. **`render()`** → `return()` in the function component. **`getSnapshotBeforeUpdate()`** → `useLayoutEffect()`. **`componentDidUpdate()`** → `useEffect(() => {}, [dependencies])`. **`componentWillUnmount()`** → cleanup function in `useEffect()`.

### Page 41 – What Are Event Handlers?
**Event handlers** are functions that run when the user interacts with the UI. React responds to events like clicking a button, typing in input, submitting a form, moving the mouse, pressing a key. React uses a **Synthetic Event System** that **normalizes events across browsers** and **improves performance with event delegation** (one root listener instead of many).

### Page 42 – Event Handling Syntax + Writing Handlers
React syntax: **camelCase event names** (e.g., `onClick` not `onclick`), and **JS functions** instead of strings (e.g., `onClick={handleClick}` not `onclick="handleClick()"`). Important: handler can have any name, can be defined inside the component, and React binds events automatically — **no need for `addEventListener`**.

### Page 43 – Passing Arguments to Event Handlers
To pass parameters, use an **arrow function**: `onClick={() => handleDelete(item.id)}`. Useful for updating specific items, passing IDs, and dynamic actions. Without the arrow, `handleDelete(item.id)` would execute immediately during render instead of on click.

### Page 44 – Event Object + Common React Events
React handlers receive a **SyntheticEvent** object: `e.target` (the element), `e.target.value` (typed text in input), `e.clientX/clientY` (mouse position), `e.key` (pressed key). **Common events**: Mouse — `onClick`, `onDoubleClick`, `onMouseEnter`, `onMouseLeave`; Keyboard — `onKeyDown`, `onKeyPress`, `onKeyUp`; Form — `onChange`, `onSubmit`, `onInput`; Clipboard — `onCopy`, `onPaste`.

### Page 45 – Handling Form Submissions + Inline vs Named Handlers
React prevents the default page reload on form submit via **`e.preventDefault()`** — essential in React forms. **Named handlers** (recommended for clarity and performance): `<form onSubmit={handleSubmit}>`. **Inline functions**: `<form onSubmit={(e) => { ... }}>` — works, but is less reusable. Best practice: use named handlers for clarity.

### Page 46 – What Are React Hooks?
**Hooks** are special functions that let **functional components** use React features. *Why hooks?* Functional components couldn't use state or lifecycle before; hooks are easier than class components; they give cleaner, more reusable logic; no `this` keyword; encourage functional programming. *What they replace*: `this.state` → `useState`; lifecycle methods → `useEffect`; Context Consumer → `useContext`; Redux-like reducers → `useReducer`.

### Page 47 – Rules of Hooks + Common Hooks
**Rule 1**: Call hooks at the **top level** of the component — never inside loops, conditions, or nested functions. **Rule 2**: Call hooks only **inside React components or custom hooks**. Reason: React needs to track hook order across renders. Most common hooks: **`useState`**, **`useEffect`**, **`useContext`**, **`useReducer`**.

### Page 48 – useState Hook
`useState` lets components store and update values. Syntax: `const [count, setCount] = useState(initialValue);`. Key points: updating state **re-renders** the component; use **functional updates** when the new value depends on the previous one (`setCount(prev => prev + 1)`) to avoid stale closures.

### Page 49 – useEffect Hook
`useEffect` runs **side effects** — work that happens outside the UI render. Examples: fetching API data, subscribing to events, timers, manipulating the DOM, saving to localStorage. Syntax variants: run every render `useEffect(() => {})`; run only on mount `useEffect(() => {}, [])`; run when dependencies change `useEffect(() => {}, [count])`; cleanup on unmount `useEffect(() => { return () => console.log("cleanup"); }, [])`.

### Page 50 – useContext + useReducer
**`useContext`** avoids "props drilling" — passing data through many components that don't use it. Without context: `App → Dashboard → Sidebar → UserProfile`. With context, pass data directly to any descendant. `const value = useContext(MyContext);`. Used for theme, user session, cart.
**`useReducer`** is used for complex state logic — alternative to multiple useState updates. It is **predictable, scalable, and similar to Redux** in its `(state, action) => newState` pattern.

### Page 51 – What Is State? (Recap)
**State** = a component's current data, which determines how the UI looks. Examples: text in an input, whether a modal is open, selected list item, API data (users, products), logged-in user info. Without state, the UI would be static and never change.

### Page 52 – Managing State – Reacting to Inputs
As your app grows, organize **where state lives** and **how it flows**. Redundant or duplicate state causes bugs and inconsistent UI. React encourages a **declarative mindset**: instead of updating DOM elements manually, describe states the component can be in, and React updates the UI when state changes. **Designer-like thinking**: think about UI as a set of states and transitions based on user input.

### Page 53 – Managing State – State Structure
Five principles: **Group related state** — if you always update two state vars together, merge them. **Avoid contradictions** — don't let state pieces "disagree" with each other. **Avoid redundant state** — if something can be calculated from props or existing state, don't store it. **Avoid duplication** — duplicated data is hard to sync. **Avoid deeply nested state** — flat structures are easier to update.

### Page 54 – Managing State – State Sharing (Lifting State Up)
Sometimes two or more components need the **same state**. Handle this by: (1) moving the shared state to the **closest common parent**, (2) passing the state down via props, (3) passing update functions down via props. This pattern is called **Lifting State Up**. Use when two components must be synchronized, when the parent must coordinate data, or when a change in one component should update another.

### Page 55 – Managing State – Preserving & Resetting State
React decides whether to **preserve or reset** state based on a component's position in the UI tree. **State is preserved when**: the component stays in the same position and its `key` doesn't change. **State is reset when**: the component is conditionally removed from DOM, its `key` changes, or its position in the tree changes. Switching components resets the state of whichever is unmounted — useful to know to avoid unintended data loss and form resets.

### Page 56 – Managing State – Using Reducer
When state updates become complicated (many variables, many handlers, scattered logic), use **`useReducer`**. A reducer **centralizes all state update logic**, makes updates **predictable**, and is similar to Redux. Reducers improve clarity for large or complex components.

### Page 57 – Managing State – With Context
Normally, parent passes info to child via props. **Props drilling** through many components becomes verbose. **Context** lets a parent make information available to any descendant without manually passing props. Great for: authentication (logged-in user), theme, language selection, cart state, global app settings. **Caveat**: overusing context causes unnecessary re-renders — use wisely.

### Page 58 – Build Tools in Modern Web Development
Modern apps rely on: JSX, ES6+ features (let/const, classes, async/await), modules (import/export), TypeScript, CSS preprocessors, images/fonts/assets, large component-based architectures. **Build tools** help by: transpiling code to be browser-compatible, bundling files into fewer HTTP requests, optimizing output for smaller/faster apps, running dev servers with hot reload, improving developer experience. Without them, React/Vue/Svelte apps would not run reliably across all browsers.

### Page 59 – Babel
**Babel** is a JavaScript compiler that lets you write modern JS and transform it into code that runs in older browsers. It transforms features like arrow functions, template literals, destructuring into compatible equivalents. Babel uses **plugins** — choose which features to transform. It can also transform other languages that compile to JS, like **TypeScript** and **JSX**. Open-source, community-maintained, widely supported. Supports advanced features like async/await, class properties, decorators.

### Page 60 – Bundling
**Bundling** combines multiple files and modules into a single optimized file efficient for the browser. Why: modern apps have many JS modules, components, images, styles; browsers handle fewer larger files better than many small ones; bundling reduces HTTP requests, improving performance; ensures dependencies load in the right order. **What bundlers do**: analyze the **dependency graph**, then merge everything into one or few production files (e.g., `bundle.js`).

### Page 61 – Bundling (Optimization Techniques)
Most bundlers also apply: **Minification** — remove spaces, comments, shorten variable names. **Tree Shaking** — remove unused code. **Code Splitting** — load code only when needed. **Caching** — faster reloads on subsequent page visits. Why it matters: improves performance, reduces latency, ensures compatibility, allows modular code structure while shipping optimized output.

### Page 62 – Webpack
**Webpack** is the most widely used module bundler. What it does: bundles JS modules into optimized files; processes assets like CSS, images, fonts, JSON; builds a **dependency graph**; generates a production-ready bundle. How it works: (1) starts from your entry file (e.g., `index.js`), (2) analyzes imports and builds the dependency graph, (3) processes each file using **loaders**, (4) uses **plugins** to optimize, (5) stores final output in `dist/` folder (e.g., `bundle.js`).

### Page 63 – Webpack (Key Features)
**Loaders** convert non-JS files (CSS, images, JSX, TypeScript) into modules. **Plugins** optimize output (minification, compression, env variables). **Code Splitting** loads only what's needed. **Tree Shaking** removes unused code. **Hot Module Replacement (HMR)** updates modules without full refresh. **Dev Server** for live preview and auto reload. Why it's important: works with React/Angular/Vue, highly customizable for enterprise, mature plugin ecosystem, handles complex workflows.

### Page 64 – Parcel
**Parcel** is a **zero-configuration** bundler — extremely fast, simple, developer-friendly. Why popular: **zero config** (no Webpack-style config files), **fast build times** via multi-core processing, **simple setup** ideal for small/medium apps and beginners, **automatic transformations** based on file types.

### Page 65 – Parcel (Features)
Parcel bundles JS, CSS, HTML, images, fonts, JSON, and more. **Auto-transpiles** JS (via Babel) and TypeScript without setup. Built-in support for JSX, React, and modern JS. Built-in **dev server with hot reloading**. **Intelligent caching** for faster rebuilds. Production optimizations: minification, tree shaking, image compression, code splitting.

### Page 66 – Parcel (Advanced + When to Use)
Advanced: supports multiple entry points (multi-page apps), friendly error messages and diagnostic overlays, integrates with React/Vue/Svelte, auto-detects installed dependencies. **Use Parcel when**: you want a fast, simple tool; you don't want to maintain a long Webpack config; you're building a small/medium project; you want bundling + dev server + JSX/TS out of the box.

### Page 67 – Vite
**Vite** is a next-generation build tool and dev server for modern frameworks like React, Vue, and Svelte. **Why it was created**: traditional bundlers (Webpack, Parcel) get slow because they bundle the entire project before serving and rebuilding on file changes is expensive. Vite solves this using **native ES modules** and an ultra-fast dev server.

### Page 68 – Vite (Key Features + How It Works)
**Features**: super-fast startup, **native ES module** support (serves source files directly to the browser, no pre-bundling), **lightning-fast HMR** (only changed modules update), optimized production build using **Rollup**, minimal configuration. **How it works**: *Development* — browser loads modules directly, no bundling, instant startup. *Production* — Vite uses **Rollup** internally to bundle, tree-shake, minify, and code-split for a highly optimized build.

### Page 69 – Vite (Benefits + When to Use)
**Benefits**: 10×–20× faster development experience; built-in support for JSX, TypeScript, CSS/PostCSS, JSON, images, assets; plugin system compatible with Rollup plugins; great choice for modern frameworks. **Use Vite when**: building a modern React or Vue app; you want the fastest dev server; you want minimal hassle and configuration; you care about fast HMR and smooth development flow. **Vite is now the official recommended tool for starting a new React project.**

### Page 70 – Webpack vs Parcel vs Vite (Comparison Table)
Side-by-side: **Developer Experience** — Moderate / Easy / Very Easy. **Configuration** — Highly configurable but complex / Zero or low / Minimal. **Build Time (Dev)** — Slow for large apps / Fast for small-medium / Extremely fast (no bundling in dev). **Build Time (Prod)** — Fast (depends on config) / Fast / Very fast (Rollup). **HMR** — Built-in but slower / Very fast / Super fast. **Tree Shaking** — Yes/Yes/Yes. **Code Splitting** — Highly customizable / Yes / Yes (Rollup-powered). **Plugin Ecosystem** — Largest / Growing / Large via Rollup. **Learning Curve** — Steep / Beginner-friendly / Very beginner-friendly. **Best Use Case** — Large enterprise / Small-medium / Modern React/Vue requiring speed.

### Page 71 – Setting Up React (Official Recommendation)
React's official documentation now **recommends using a framework** instead of manually setting up React with bundlers like Webpack or Create React App. Why? Frameworks automatically solve real-world problems: **routing, data fetching, server-side rendering (SSR), code splitting, SEO, file-based routing, optimized production builds**. Frameworks give you a complete environment from day one.

### Page 72 – Setting Up React (Popular Frameworks)
Four major options: **(1) Next.js** — most popular, officially recommended; full-stack React with file-based routing, SSR, SSG, API routes, great performance and SEO; ideal for production apps. **(2) Remix** — focused on web fundamentals, optimized data loading and routing, great for fast interactive apps. **(3) Gatsby** — static site generator, ideal for blogs/docs/marketing sites, plugin ecosystem, blazing-fast static builds. **(4) Expo** — for React Native mobile apps; single codebase for Android+iOS; built-in camera, notifications, assets.

### Page 73 – Thank You
Closing slide.

---

## Lecture 08 Part 02 – ReactJS

### Page 1 – Title Slide
**SE3040 – Application Frameworks, Lecture 08: ReactJS Part 02.** Part 2 dives into advanced state management (Context API, Redux Toolkit) and modern React 18 features (Concurrent Rendering, Suspense, SSR).

### Page 2 – Why Do We Need Advanced State Management? (The Problem)
As applications grow, state becomes **more complex and harder to manage**. Components start to share state across many levels, pass too many props (**prop-drilling**), and re-render unnecessarily. Local state (`useState`) becomes insufficient when multiple components depend on the same data, when data updates frequently (API calls, auth, themes, cart items), or when global configuration is needed (language, dark mode, user role).

### Page 3 – Key Challenges + What Part 2 Introduces
**Key challenges**: **Prop Drilling** (passing data through many nested components), **Inconsistent State** (hard to synchronize), **Repeated Logic** (duplicate handling code), **Performance Issues** (too many re-renders). **What Part 2 covers**: **Context API** (avoids prop drilling, simple global state), **Redux Toolkit** (scalable, predictable state for large apps), **React 18 features** (concurrent rendering, transitions), **Suspense** (better async UI handling).

### Page 4 – What is the Context API?
The **Context API** is a built-in React solution that lets components **share data without passing props manually** at every level — solving the prop drilling problem in deeply nested trees. **Conceptual workflow**: (1) **Create Context** — like a shared storage bucket. (2) **Provide Context** — a Provider component makes data available to all children. (3) **Consume Context** — components read the shared data via `useContext()` (functional) or `Context.Consumer` (legacy).

### Page 5 – When to Use the Context API
Use Context when the data is **needed by many components** and **not expected to change extremely frequently**. Example scenarios: user authentication data, theme settings (Dark/Light mode), language/localization, app-wide configs. Context is a sweet spot for cross-cutting concerns that don't update on every keystroke.

### Page 6 – Why Context? (The Prop Drilling Problem)
In React, data normally flows top-down via props. When many components need the same data, props must be passed through multiple layers — even through intermediate components that don't use it. This creates **unnecessary re-renders**, **hard-to-maintain component trees**, **complicated refactoring**, and **increased risk of bugs**.

### Page 7 – How Context Solves It
Context provides a **global shared storage** — any component in the tree can access the data directly, without props going through parents. Reduces UI wiring and simplifies complex hierarchies. **Without Context**: `App → Layout → Sidebar → UserMenu → UserAvatar` (every parent must pass `username` even if unused). **With Context**: `<UserContext.Provider>` wraps the whole app, and `UserAvatar` accesses `username` directly via `useContext()`.

### Page 8 – How Context API Works (3 Steps)
**Step 1: Create a Context** — `const MyContext = createContext()` defines the shared "global space" (no data yet, just the structure). **Step 2: Wrap your app with a Provider** — `<MyContext.Provider value={...}>` makes values available to all nested components. The `value` prop holds the shared data. **Step 3: Consume Data Using `useContext()`** — any component reads the data without props. **Key outcome**: Context enables global reading and updating of shared state without prop drilling.

### Page 9 – Creating a Context — Step 1: Create the File
Best practice: keep each context in its own file for clarity and reuse. The file defines the type of context but does not store any data yet — it's just a structural definition that exports the context object.

### Page 10 – Creating a Context — Step 2: Create a Provider Component
Providers wrap your app and supply the global value. A provider component typically uses `useState` to hold the data (e.g., `[theme, setTheme]`) and provides them through `<Context.Provider value={{ theme, setTheme }}>`. This shares state with the entire app, and any descendant can read or update the theme.

### Page 11 – Creating a Context — Step 3: Wrap the Root App
In `index.js` (or `main.jsx` for Vite), wrap `<App />` with the provider component. **Key idea**: you can create multiple providers — `AuthProvider`, `LanguageProvider`, `SettingsProvider` — each handling a separate slice of global state. Nesting them is fine, but stack them in a sensible order.

### Page 12 – Consuming Context with useContext() — Reading
Once the Provider is set, any component can read the shared data using `useContext(MyContext)`. This avoids passing props through every level. Benefits: **no props needed**, cleaner and less repetitive, **component automatically updates when the context value changes**.

### Page 13 – Consuming Context — Updating Values
You can also update context from any consumer. When a button calls a setter exposed via context (e.g., `setTheme('dark')`), the global theme updates and all components using that context **automatically re-render**. No prop drilling required. **Best practice reminder**: only use `useContext()` inside components wrapped by the Provider — outside the Provider, `useContext()` returns `undefined`.

### Page 14 – When Should You Use Context API? (Best Use Cases)
Use Context for: data needed by many components (user profile, authentication status, app settings); UI-related global state (dark/light theme, font size, layout mode like grid/list, sidebar open/closed toggles); rarely-updated global data (app version, language/i18n, currency, role-based UI configuration).

### Page 15 – Ideal Scenarios + When NOT to Use Context
**Ideal**: state is simple, doesn't change frequently, consumed by many sibling components, you want to eliminate prop drilling, you want to avoid external dependencies. **Avoid Context when**: state updates very frequently (e.g., typing text), you need complex state transitions, multiple contexts nest deeply, you need strong debugging tools, or you're working on a large-scale app with many global states. **Guiding rule**: Context API = good for simple global state; Redux Toolkit = good for complex, scalable state.

### Page 16 – Limitations of Context API (1 & 2)
**1. Re-renders Can Become Expensive** — when context value changes, **all consuming components re-render**, even those using only part of the data. Hurts performance in large apps. If `UserContext` updates frequently, the entire UI may re-render.
**2. Not Designed for Highly Dynamic or Complex State** — poor at rapidly changing values (search input, counters, animation), complex business logic, multi-level async workflows, cached API data. Redux Toolkit or Zustand is better.

### Page 17 – Limitations of Context API (3, 4, 5)
**3. No Built-in Debugging or DevTools** — no time-travel debugging, action logging, or state change tracing; Redux DevTools provides these for large apps.
**4. Multiple Contexts → Harder to Manage** — apps grow into `AuthContext`, `ThemeContext`, `LanguageContext`, `CartContext`, `SettingsContext` — leading to **"Provider Hell"** that's hard to read and maintain.
**5. Not Ideal for Sharing Across Many Features** — poor fit for large forms, API caching, pagination, global filters, notifications, real-time updates.

### Page 18 – Introduction to Redux (Problem it Solves)
**Redux** is a predictable global state management library for **large and complex** React applications. When your app grows, many components need the same data, state updates become hard to track, component-to-component communication gets messy, and debugging is hard. **Redux centralizes state into one single store** for the entire app.

### Page 19 – Redux Core Principles + Popularity
**Core principles**: **(1) Single Source of Truth** — one global store holds the entire app state; easy to debug, log, reason about. **(2) State is Read-Only** — components cannot directly modify state; updates happen through **actions** only. **(3) Changes Made With Pure Reducers** — `(state, action) → newState` pure functions, ensuring predictability.
**Why popular**: great for medium-to-large apps, works consistently across the UI, predictable transitions, excellent Redux DevTools, perfect for API calls, complex workflows, real-time updates, multi-feature state.

### Page 20 – When to Use Redux
Use Redux when your app has **lots of shared/global state**, requires **complex state logic**, needs to **scale over time**, needs **strong debugging tools**, or must handle **frequent state updates efficiently**. If none of these apply, Context API or local state is usually enough.

### Page 21 – Why Use React Redux? (Performance + Hooks API)
**React Redux** is the official library that connects Redux with React, the most efficient way for React components to interact with the store.
**1. Automatic Performance Optimization** — components re-render **only when their specific state slice changes**; more efficient than manual subscriptions.
**2. Simple Modern API Using Hooks** — `useSelector()` reads/selects specific state values (auto-subscribes, triggers re-render only when needed); `useDispatch()` lets components dispatch actions. These replace the older `connect()` HOC.

### Page 22 – Why Use React Redux? (DX, Predictability, RTK)
**3. Great Developer Experience** — integrates seamlessly with Redux DevTools, action logging, time-travel debugging, state inspection.
**4. Encourages Predictable UI Behavior** — components behave consistently, bugs are easier to track, UI stays in sync because state comes from a centralized store.
**5. Works Perfectly with Redux Toolkit** — Redux + Redux Toolkit is the officially recommended setup: less boilerplate, cleaner reducer logic, built-in async support, better maintainability.

### Page 23 – Redux Toolkit (Why) — Eliminates Boilerplate + Immutability
**Redux Toolkit (RTK)** is the official recommended approach for writing Redux logic. **Eliminates Boilerplate**: classic Redux required action types, action creators, switch-case reducers, and manual immutability — RTK removes all of that. **Built-In Immutability with Immer**: you can "mutate" state inside reducers (`state.value++`), and Immer converts it into an immutable update — making reducer logic simple and beginner-friendly (previously not allowed in Redux).

### Page 24 – Redux Toolkit (More Features)
**Built-In DevTools & Middleware**: RTK auto-configures Redux DevTools, Thunk middleware (for async calls), better default settings — no extra setup.
**Slices Combine Logic Together**: a "slice" includes initial state, reducers, actions, and case reducers all in one file — cleaner architecture.
**Great for Async (API) Logic**: provides `createAsyncThunk()` for async operations and **RTK Query** for API caching, fetching, invalidation — much easier than classic Redux async patterns.

### Page 25 – Installing Redux Toolkit & React Redux
Two packages needed: **Redux Toolkit** provides `configureStore`, `createSlice`, `createAsyncThunk`, built-in middleware, Immer for immutability, DevTools support. **React Redux** is the official binding between React and Redux, providing `Provider`, `useSelector`, `useDispatch`. Install both with `npm install @reduxjs/toolkit react-redux`.

### Page 26 – Using Redux State — Reading with useSelector
Once store and slices are set up, interact with Redux via React Redux hooks: `useSelector()` to read state, `useDispatch()` to update. **Reading**: `useSelector()` lets a component subscribe to specific parts of Redux state — automatically re-renders when that part changes, efficient (only re-renders when necessary). Example: `const count = useSelector(state => state.counter.value);`.

### Page 27 – Using Redux State — Dispatching with useDispatch
`useDispatch()` returns the **dispatch function**, used to trigger state updates. Updates state predictably and uses slice actions created automatically by Redux Toolkit. Example: `const dispatch = useDispatch(); dispatch(increment());`. Combined with `useSelector`, these hooks fully replace the older `connect()` HOC pattern.

### Page 28 – Using Redux State — Combined Example
A combined example slide showing a complete component using both hooks: reading state with `useSelector`, and dispatching actions with `useDispatch`. This pattern is what most production Redux code looks like today.

### Page 29 – Context API vs Redux Toolkit — When to Use Context
**Best for simple, UI-related global state.** Ideal scenarios: theme switching, user authentication info, language/locale settings, layout preferences (sidebar open, grid/list view), configuration that rarely changes. **Strengths**: simple, built into React, no extra dependencies, great for small-to-medium apps, easy to understand. **Limitations**: re-renders all consumers when value changes, not suitable for complex logic, no debugging tools, hard to scale across many features.

### Page 30 – Context API vs Redux Toolkit — When to Use RTK
**Best for large, multi-feature, complex applications.** Ideal: multiple components depend on shared global data, data updated frequently (API responses, pagination), complex logic (derived state, multiple reducers), real-time updates (chat, dashboards), apps requiring robust debugging, predictable state transitions. **Strengths**: scalable/structured architecture, built-in async logic (`createAsyncThunk`), built-in DevTools (action history, time-travel), performance-optimized subscription model, centralized store improves consistency. **Limitations**: slightly more setup than Context; might be overkill for small apps.

### Page 31 – Advance React (Section Divider)
A divider introducing three modern React features that the second half of the lecture covers: **Concurrent Rendering**, **React Suspense**, **Server-Side Rendering (SSR)**.

### Page 32 – Concurrent Rendering (What)
React 18 introduced **Concurrent Rendering**, a new rendering system that improves performance, responsiveness, and UX — especially in large apps. **What it allows React to do**: **Interrupt rendering work** (pause a long update if something urgent like user typing happens); **Work in the background** (prepare UI updates without blocking the main thread); **Prioritize updates** (urgent updates like typing first, non-urgent ones like filtering big lists as background tasks); **Avoid UI freezing** (heavy renders no longer lock the UI).

### Page 33 – Concurrent Rendering (Why & How)
**Why it was needed**: before React 18, UI could freeze while React processed updates; large state updates caused slow interactions; browsers felt unresponsive in heavy apps. **How to use it**: concurrent features are **opt-in** — you enable them when needed; normal rendering still works the same. Enabled through hooks like `useTransition()`, `useDeferredValue()`, and `Suspense`. React automatically handles scheduling and prioritizing.
**Benefits**: smoother UX, faster perceived performance, great for search bars and long lists, better on low-end devices.

### Page 34 – useTransition (Why & How)
`useTransition` separates **urgent updates from non-urgent updates**, making UI feel smoother. **Why**: heavy operations (filtering long lists, rendering large tables, big-dataset searches) cause UI lag, input delay, frozen screens. `useTransition` fixes this by running heavy updates in the background.
**How it works**: `const [isPending, startTransition] = useTransition();`. `startTransition(callback)` tells React to run the update as **non-urgent**. `isPending` is a boolean indicating if the transition is ongoing — useful for showing loading indicators.

### Page 35 – useTransition (Example)
Example: filtering a large list smoothly. Typing into a search input is urgent (sets the query state immediately). The expensive filter operation is wrapped in `startTransition`, so React schedules it as low-priority. The input stays responsive, heavy filtering runs in the background, the UI doesn't freeze, and users get immediate response for urgent actions. The key idea: urgent UI interactions and non-urgent heavy computations run smoothly without blocking each other.

### Page 36 – useDeferredValue (Why)
`useDeferredValue` allows you to **delay updating a non-urgent value**, improving responsiveness when typing or interacting quickly. Similar to `useTransition` but easier for input-based UI updates. **Why**: in large apps, typing into search boxes, filtering large datasets, or triggering heavy recalculations causes input lag, delayed keystrokes, UI freezing. `useDeferredValue` prevents this by deferring heavy updates.

### Page 37 – useDeferredValue (How It Works)
You give React a value, and React returns a **deferred version**: `const deferredQuery = useDeferredValue(query);`. `query` updates **instantly** (responsive typing), while `deferredQuery` updates **later** (used for heavy calculations like filtering, sorting, rendering big lists). The deferred value lags behind by a render or two, but only when React is overloaded.

### Page 38 – useDeferredValue (Example)
Example: a smooth search box with heavy list rendering. Bind `query` to the input directly (so typing is instant), then pass `deferredQuery` to the expensive `filteredList` calculation. As the user types, the input stays responsive; the heavy filter runs only when React has time.

### Page 39 – useDeferredValue (Achievements & When to Use)
**What this achieves**: immediate response to typing, heavy list filtering happens after the user finishes typing, UI doesn't freeze, great for search bars/dropdown filters/dashboards.
**When to use**: search filters, auto-suggestions, live data display, pagination UI, large tables or lists, any component with heavy updates triggered by typing.

### Page 40 – React Suspense (What It Does)
**Suspense** is a React feature that lets you **pause rendering while waiting for something** (data or code) and show a **fallback UI** in the meantime. Makes loading states **clean, declarative, automatic**. Instead of `if (loading) return <Spinner />;` everywhere, Suspense wraps components and lets React: wait for async resources, show a fallback loader, resume rendering when ready.

### Page 41 – React Suspense (Key Use Cases)
Four use cases: **(1) Lazy Loading Components** — load components only when needed (better performance). **(2) Server Components & Streaming** (React 18 / Next.js 13+) — Suspense works with async server rendering. **(3) Data Fetching** (with frameworks/libraries) — integrates with React Server Components, React Query (experimental), Relay, Next.js App Router. **(4) Graceful Fallback UI** — loading screens, skeletons, spinners, placeholders.

### Page 42 – React Suspense (Lazy Loading Example + Importance)
**Lazy Loading Example**: `const LazyComponent = lazy(() => import('./LazyComponent'));` then wrap with `<Suspense fallback={<Spinner />}><LazyComponent /></Suspense>`. `lazy()` loads the component only when needed; `Suspense` shows fallback UI until it loads.
**Why Suspense is important**: cleaner loading logic, consistent UX across the app, helps split your app into smaller chunks (**code-splitting**), more responsive UI, integrates deeply with SSR. **Summary**: Suspense = declarative loading handling that improves performance and UX.

### Page 43 – Server-Side Rendering (SSR) — How It Works
**SSR** renders React components **on the server instead of the browser** — the server sends fully rendered HTML to the client, improving performance and SEO.
**Step-by-step**: (1) **User requests a page** — browser sends a request. (2) **Server runs React components** — React executes on the server, fetches data, generates HTML. (3) **Server sends pre-rendered HTML** — the browser instantly displays meaningful content (fast first paint). (4) **JavaScript loads and hydrates the page** — attaches event listeners, making the page interactive.

### Page 44 – SSR (Why It's Useful)
**Better SEO** — search engines fully index rendered HTML (ideal for blogs, e-commerce, landing pages). **Faster First Load** — users see UI immediately instead of waiting for JS. **Better Performance on Slow Devices** — heavy computation runs on the server, not the user's device. **Great for Dynamic Content** — data-driven pages load faster when rendered on the server.

### Page 45 – SSR (Where It's Used in React)
SSR is **not done using plain React**. Instead, frameworks like **Next.js** provide SSR out of the box. Next.js SSR features: `getServerSideProps()`, dynamic server-side rendering, streaming SSR, Server Components (React 18). Next.js is the **officially recommended React framework**.

### Page 46 – SSR (When to Use)
Use SSR when your app needs: search engine visibility, dynamic content with fast initial load, public-facing pages, strong performance on low-power devices, improved perceived performance. **Examples**: e-commerce product pages, blogs and news websites, marketing landing pages, portfolio websites. **Summary**: SSR = faster first load + better SEO + server-powered rendering → recommended for content-heavy and public-facing sites.

### Page 47 – Client-Side Rendering (CSR) — How It Works
**CSR** means the browser renders the UI after downloading JavaScript. The most common strategy in apps created with Vite, CRA, or Next.js client components.
**Step-by-step**: (1) Browser loads a **minimal HTML file** (usually `<div id="root"></div>`). (2) **JavaScript bundle downloads** — React code loads into the browser. (3) **React builds the UI on the client** — all components render using browser CPU. (4) **Data is fetched from APIs (client-side)** — the UI appears only after data + JS loading.

### Page 48 – CSR (Advantages & Disadvantages)
**Advantages**: excellent interactivity (dynamic UI, frequent updates, complex workflows); fast navigation between pages (app behaves like a desktop app once loaded); simpler architecture (no server-rendering logic); lower server load (backend serves static files); works offline (with Service Workers — PWAs).
**Disadvantages**: slow first page load (browser downloads + parses + executes JS before UI appears); poor SEO (search engines struggle to index JS-rendered pages); heavy on low-power devices (phones/laptops with weak CPU); not ideal for content-focused sites (blogs, news, landing pages suffer).

### Page 49 – CSR (Where Ideal + Common Tools)
**Where CSR is ideal**: dashboards (analytics, admin panels), social media and messaging apps (Facebook Web, Twitter, Instagram, Slack, Discord), SaaS tools (Notion-like apps, project management tools, code editors), internal/auth-gated applications (SEO irrelevant inside private systems).
**Common tools**: React + Vite (recommended for modern projects), Create React App (deprecated), Next.js Client Components, Parcel/Webpack apps. **Summary**: CSR = interactive, dynamic, fast-after-load, but weak for SEO and slow initial rendering. Best for apps, not content pages.

### Page 50 – Thank You
Closing slide.

---

## Lecture 09 – Framework Selection

### Page 1 – Title Slide
**SE3040 – Application Frameworks, Lecture 09: Framework Selection Strategies.** The final lecture pivots from "how to use frameworks" to "how to choose one" — a decision-making discipline as important as the technical skills themselves.

### Page 2 – Agenda
The lecture covers: Introduction, Key Decision Factors, Framework Categories and Use Cases, the Selection Process (including the **reality** of framework selection), Common Framework Combinations, and Migration Strategies. The flow moves from theory to the messy real-world practice and on to migration when the original choice no longer fits.

### Page 3 – Introduction — The Framework Landscape in 2026
The modern software ecosystem offers an **abundance of frameworks** for both frontend and backend development. This diversity gives flexibility but also creates **decision-making complexity**. Choosing wrong can lead to: increased development time and cost, **technical debt** accumulation, difficulty in hiring and team scaling, performance bottlenecks, and maintenance challenges. Framework choice is one of the highest-impact early decisions on a project.

### Page 4 – Why Framework Selection Matters
A framework decision is often a **long-term commitment** that affects: **development velocity**, **system performance and scalability**, **team productivity and satisfaction**, **maintenance costs over the project lifetime**, and the **ability to adapt to changing requirements**. Reversing a framework choice mid-project is expensive — sometimes catastrophic — so the upfront thinking is worth the time.

### Page 5 – Key Decision Factors (Project + Team)
**1. Project Requirements Analysis** — application type (SPA vs static vs mobile vs API), performance requirements, scalability considerations. **2. Team Considerations** — existing expertise (using what the team already knows is often the right call), team size and structure, hiring and talent pool (is there a local market of people who know the framework?).

### Page 6 – Key Decision Factors (Technical + Business)
**3. Technical Considerations** — ecosystem maturity (how many libraries exist?), community and support, performance characteristics, integration requirements (does it play well with your existing stack?). **4. Business Considerations** — time to market, budget constraints, long-term viability (will the framework still be maintained in 5 years?).

### Page 7 – Framework Categories — Frontend (React)
**React Ecosystem**: best for **large-scale applications**, teams with React experience, rich ecosystems. **Considerations**: requires additional libraries for routing, state management — React itself is just a view library. **When to choose**: need flexibility, large talent pool, extensive third-party support. **Next.js** layered on React provides full-stack functionality with SSR/SSG — excellent for SEO-critical apps.

### Page 8 – Frontend Frameworks — Vue and Angular
**2. Vue.js** — best for progressive enhancement, teams wanting a gentle learning curve. **Considerations**: smaller ecosystem than React but growing. **When to choose**: rapid development, developer experience priority, gradual migration.
**3. Angular** — best for enterprise applications, teams wanting opinionated structure. **Considerations**: steeper learning curve, more verbose. **When to choose**: large enterprise projects, TypeScript-first teams, need a comprehensive batteries-included solution.

### Page 9 – Frontend Frameworks — Svelte and Solid
**4. Svelte/SvelteKit** — best for performance-critical apps, small bundle size priority. **Considerations**: smaller community, newer ecosystem. **When to choose**: performance is paramount, team willing to adopt newer technology.
**5. Solid.js** — best for React-like development with better performance. **Considerations**: young ecosystem, smaller community. **When to choose**: fine-grained reactivity needs, performance-first approach.

### Page 10 – Backend Frameworks — Node.js (Express, Nest)
**1. Node.js Frameworks**
**a. Express.js** — best for APIs, microservices, teams needing flexibility. **Considerations**: minimalist, requires additional libraries for structure. **When to choose**: small to medium projects, need maximum control.
**b. Nest.js** — best for enterprise applications, microservices architecture. **Considerations**: opinionated, Angular-inspired architecture. **When to choose**: large teams, need structure and TypeScript support.

### Page 11 – Backend Frameworks — Fastify + Python (Django)
**c. Fastify** — best for high-performance APIs. **Considerations**: similar to Express but faster. **When to choose**: performance-critical services.
**2. Python Frameworks**
**a. Django** — best for full-stack web apps, rapid development. **Considerations**: batteries-included, opinionated. **When to choose**: need admin interface, ORM, built-in authentication.

### Page 12 – Backend Frameworks — Flask and FastAPI
**b. Flask** — best for microservices, APIs, smaller applications. **Considerations**: minimalist, flexible. **When to choose**: need flexibility, small to medium projects.
**c. FastAPI** — best for modern APIs, microservices, ML model serving. **Considerations**: async support, automatic documentation. **When to choose**: need OpenAPI docs, async operations, type hints.

### Page 13 – Backend Frameworks — JVM (Spring Boot, Micronaut)
**3. Java/JVM Frameworks**
**a. Spring Boot** — best for enterprise apps, microservices. **Considerations**: comprehensive, enterprise-grade. **When to choose**: large organizations, Java expertise, need mature ecosystem.
**b. Micronaut** — best for microservices, cloud-native applications. **Considerations**: low memory footprint, fast startup. **When to choose**: serverless, containerized environments.

### Page 14 – Backend Frameworks — .NET and Rails
**a. ASP.NET Core** — best for enterprise apps, cross-platform development. **Considerations**: Microsoft ecosystem, excellent tooling. **When to choose**: .NET expertise, Azure deployment, enterprise environments.
**b. Ruby on Rails** — best for rapid development, startups, MVPs. **Considerations**: convention over configuration. **When to choose**: speed of development priority, proven patterns needed.

### Page 15 – The Selection Process (Structured Framework)
A **structured decision-making framework** is a systematic process to choose a framework instead of going by gut. Five stages: **(1) Requirement Gathering**, **(2) Initial Screening** (filter out clearly unsuitable options), **(3) Detailed Evaluation** (deep comparison), **(4) Proof of Concept** (build a small slice with the top candidates), **(5) Final Decision**.

### Page 16 – Detailed Evaluation Structure (Example)
A **weighted scoring matrix** example for comparing three frameworks across criteria:
- Performance (20%): A=8, B=7, C=9
- Team Expertise (15%): A=9, B=5, C=6
- Community Support (15%): A=9, B=8, C=6
- Development Speed (15%): A=7, B=9, C=7
- Scalability (15%): A=8, B=8, C=9
- Ecosystem (10%): A=9, B=7, C=6
- Documentation (10%): A=8, B=9, C=7
- **Total**: A=**8.15**, B=7.45, C=7.5
Framework A wins on the weighted score. The exercise forces explicit trade-offs.

### Page 17 – The Reality of Framework Selection
**Honest take**. The textbook version: "Conduct comprehensive requirements analysis, create weighted evaluation matrices, score systematically." **The industry reality** — most decisions actually happen as: **"Let's use what we already know"** (60%), **"We need to ship fast, what's fastest?"** (25%), **"This specific requirement forces our hand"** (10%), **"Let's actually think this through carefully"** (5%). And that's often okay — pragmatism beats process when ship dates loom.

### Page 18 – Red Flags to Watch For (Framework)
**Framework red flags** — signs a framework should be avoided: infrequent updates or abandoned development, major **security vulnerabilities** not being addressed, declining community activity, frequent **breaking changes** without clear migration paths, poor documentation or outdated tutorials, heavy reliance on a **single maintainer** (bus factor of one).

### Page 19 – Red Flags to Watch For (Decision-Making)
**Decision-making red flags**: choosing based **solely on popularity or hype**, ignoring team capabilities and learning curves, overlooking long-term **maintenance implications**, selecting frameworks that don't match project scale (using enterprise frameworks for tiny projects, or vice versa), following trends without evaluation. The wrong reasons are often more dangerous than the wrong framework.

### Page 20 – Common Framework Combinations (Full-Stack)
**Popular full-stack combinations**: **MERN Stack** (MongoDB, Express, React, Node), **MEAN Stack** (MongoDB, Express, Angular, Node), **Next.js + Backend** (Next handles frontend + API routes alongside a separate service), **Django + React/Vue** (Django backend, JS frontend), **Spring Boot + Angular** (enterprise Java + Angular). Each combination has a stable culture and recipes around it.

### Page 21 – Common Framework Combinations (Microservices)
**Microservices Considerations**: with microservices you are **not limited to a single framework**. Different services can use different frameworks based on specific needs. **Frontend can be decoupled** from backend technology choices. **API-first design** enables polyglot architectures. Consider **service boundaries and communication patterns** (REST, gRPC, events) when choosing frameworks for each service.

### Page 22 – Migration Approaches — Strangler Fig Pattern
**Strangler Fig Pattern**: gradually replace the old system with the new — run both systems in parallel, route some traffic to the new, expand its scope over time. Minimizes risk through **incremental migration** and allows **rollback** if issues arise. Named after the strangler fig tree that grows around a host tree and eventually replaces it.

### Page 23 – Migration Approaches — Big Bang Rewrite
**Big Bang Rewrite**: complete rewrite in the new framework, deployed all at once. **Higher risk** but faster completion. Suitable for smaller applications where the surface is small enough to redo. Requires a **feature freeze** during migration (no new features on the old system while rewriting) — politically and operationally difficult on larger projects.

### Page 24 – Migration Approaches — Hybrid Approach
**Hybrid Approach**: use the new framework for **new features**, maintain the old framework for **existing features**. Create an **API layer** between the two systems so they can communicate. Long-term coexistence is possible — this often becomes the de facto state at large organizations whether intended or not.

### Page 25 – Conclusion and Takeaways
Five lessons: **(1) No Perfect Framework** — every framework has trade-offs; choose based on context. **(2) Team Matters** — a framework your team understands well **beats a "better" framework they don't**. **(3) Start Simple** — don't over-engineer; you can always add complexity later. **(4) Document Decisions** — record *why* you chose a framework, for future reference and onboarding. **(5) Plan for Change** — architecture should allow for framework evolution or replacement; lock-in is a real cost.

### Page 26 – Thank You
Closing slide.

---

## Summary

This study guide covers all **303 pages** across the 9 uploaded SE3040 lecture PDFs:

| Lecture | Topic | Pages |
|---|---|---|
| 01 | Introduction & Best Practices (SOLID, guidelines, practices) | 32 |
| 02 | Version Controlling (Git, GitHub, workflows) | 35 |
| 03 | JavaScript (classes, `this`, closures, async patterns) | 16 |
| 04 | NodeJS (event loop, npm, modules, fs) | 17 |
| 05 | REST and ExpressJS (3-tier, MVC, REST, Express) | 33 |
| 06 | NoSQL and MongoDB (CAP, MongoDB, CRUD) | 21 |
| 08 P1 | ReactJS Part 01 (foundations, components, hooks, build tools) | 73 |
| 08 P2 | ReactJS Part 02 (Context, Redux Toolkit, concurrent rendering, SSR/CSR) | 50 |
| 09 | Framework Selection Strategies | 26 |
| **Total** | | **303** |

Every page is represented as a numbered section above, with a detailed explanation of the slide's content, the broader concept it illustrates, and (where useful) examples or context.

