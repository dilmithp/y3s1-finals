# 🥔 Distributed Systems: Async Communication — Explained to a Confused Potato!

---

## 🎬 THE STORY BEGINS...

Imagine you're at a **pizza restaurant**. You walk up to the counter, order a pizza, and then just... **stand there**. Staring. Not moving. Not breathing. Just waiting. The cashier is frozen too, staring back at you. Nobody else can order. The whole restaurant is paralyzed until your pizza is done.

That's **synchronous (blocking) communication**. And it's kind of ridiculous, right?

Now imagine instead: you order your pizza, get a **buzzer**, go sit down, chat with friends, scroll your phone, live your life — and when the pizza's ready, the buzzer goes off and you go pick it up.

That's **asynchronous communication**. And that's what this entire lecture is about. 🍕

---

## 📺 SLIDE 1 & 2 — What Are We Even Talking About?

This lecture covers **three big problems and solutions**:

1. What happens when your app calls a **slow remote method** and just freezes waiting?
2. How do we fix it with **asynchronous calls**?
3. Two main ways to do it:
   - **Remote Callback Functions** (like leaving your number for someone to call back)
   - **Asynchronous Messaging** (like a postal system for software)

**Memory trick:** Think **"Don't Wait, Callback or Message!"**

---

## 📺 SLIDE 3 — The Picture That Says It All

This slide shows two diagrams side by side:

### 🔴 Synchronous (Left Side):
```
Process A sends → Process B
Process A just WAITS... and waits... and waits...
Process B finishes → sends back
Process A finally wakes up
```
Process A is basically **comatose** while B does its work.

### 🟢 Asynchronous (Right Side):
```
Process A sends → Process B
Process A CONTINUES WORKING (living its best life)
Process B finishes → sends back
Process A gets the response whenever it arrives
```

**Key visual to remember:** In async, Process A's timeline keeps going DOWN (it keeps working) while B is doing its thing. In sync, Process A's timeline is **flat/frozen** while waiting.

---

## 📺 SLIDE 4 — Blocking Calls and Distributed Computing

Okay potato, here's why this matters in **distributed systems** specifically.

In a normal local program, if you call a function and it takes 2 milliseconds, no big deal. But in a **distributed system**, you're calling something across a **network** — on another computer, maybe in another country!

### The Problem:
- When you make a **remote function call (RPC)**, the caller **blocks** (freezes) until the remote function finishes and returns
- But what if the remote server is doing something **heavy** — like processing a huge file, running a complex calculation, or just being slow?
- The caller just sits there, **wasting resources**, doing absolutely nothing

**Real-world analogy:** Imagine calling your friend to ask them to look something up. Instead of putting them on hold and doing other things, you just **stand completely still** with the phone to your ear for 10 minutes. That's blocking. Ridiculous!

### Three key points to remember:
1. **Blocking = waiting = wasted resources**
2. Especially bad when the call takes a long time
3. Client waits while server does a long job = **inefficient**

---

## 📺 SLIDE 5 — Synchronous vs. Asynchronous (The Official Definitions)

Now let's get the **proper definitions** locked in, because these WILL appear in MCQs.

### 🔴 Synchronous Invocation = Blocking Call
- **Serial processing** (one thing at a time)
- Control is **passed to** the called function
- Caller **cannot continue** until the called function returns
- Think: **"I'll wait right here until you're done"**

### 🟢 Asynchronous Invocation = Non-Blocking Call
- **Parallel processing** (things happen simultaneously)
- Control is **returned immediately** to the caller
- Called function **carries on in the background**
- At some later time, caller **retrieves the return value**
- Think: **"Call me when you're done, I've got stuff to do"**

**Memory trick:** 
- **Syn**chronous = **Syn**chronized = everyone moves together = BLOCKING
- **A**synchronous = **A**part = they move independently = NON-BLOCKING

---

## 📺 SLIDE 6 — Local Asynchronous Calls

Before we go distributed, even **local** (same computer) programs use async calls. Why?

### Reasons to use async locally:
1. **Maintain GUI responsiveness** — Ever seen a program "freeze" with a spinning wheel? That's because someone made a blocking call on the main UI thread. Async prevents this!
2. **Utilise resources more efficiently** — Keep doing other work during a long-running call
3. **Java Swing event dispatching** — Java's GUI framework uses this pattern

**Real-world example:** When you click "Upload" on a website and the page doesn't freeze — that's async at work. You can still scroll, click other things, etc.

---

## 📺 SLIDE 7 — Distributed Asynchronous Calls

Now here's something interesting. In the **classic client-server model**:
- The **server is passive** — it just sits there waiting
- The **client initiates** all communication (IPC = Inter-Process Communication)

But some applications need the **server to initiate communication** when something happens! Examples:

| Application | Why server needs to initiate |
|-------------|------------------------------|
| **Monitoring** | Alert when temperature spikes |
| **Games** | Tell all players when someone moves |
| **Auctioning** | Notify all bidders of new bid |
| **Voting/Polling** | Update results in real-time |
| **Chat-room** | Deliver messages to all participants |
| **Message/Bulletin board** | Push new posts to subscribers |
| **Groupware** | Sync changes across all users |

**The problem:** If the server is passive, how does it tell clients about events? The client would have to keep asking "anything new? anything new? anything new?" — which is called **polling** and it's terrible. We'll see the better solution next!

---

## 📺 SLIDE 8 — When to Use Asynchronous Calls?

This is important for your exam — knowing **when** to use async, not just what it is.

### Key insight: Every RPC call is POTENTIALLY long-running
- Network failures are only detected **after timeouts expire** (which can take a while!)
- So technically, you could make EVERY call async

### But wait — should you?
**No!** Making every RPC call async **increases code complexity**. You're adding extra code just on the *chance* a network failure occurs.

### The smart rule:
> **Use async calls only on functions that are EXPECTED to take a long time**

Examples of when to use async:
- **Heavy processing tasks** (video encoding, data analysis)
- **Intensive disk I/O tasks** (reading/writing large files)
- **GUI clients** — responsiveness is always a key issue here

**Memory trick:** Don't over-engineer. Async when it's **expected to be slow**, sync when it's **expected to be fast**.

---

## 📺 SLIDE 9 — Remote Asynchronous Communication Methods

There are **two main approaches** for remote async communication:

1. **Remote Callback Functions** — The client registers itself, server calls back
2. **Messaging** (e.g., **JMS** — Java Message Service, **Microsoft Message Queuing**)

And importantly: **Both Java and .NET support callback functions**

Think of these as two different postal systems:
- **Callbacks** = You give someone your phone number and they call you back directly
- **Messaging** = You put a letter in a mailbox, and the postal service delivers it whenever

---

## 📺 SLIDES 10 & 11 — Polling vs. Callback (SUPER IMPORTANT!)

This is a classic exam topic. Let's nail it with a story.

### 🔴 Polling — The Annoying Way

Imagine you ordered a package online. You have no tracking. So you call the delivery company every 5 minutes:
- "Is it here yet?" — "No"
- "Is it here yet?" — "No"  
- "Is it here yet?" — "No"
- "Is it here yet?" — "YES!"

That's **polling**. The client **repeatedly asks** the server until it gets the answer it wants.

**Problems with polling:**
- Wastes network resources (all those unnecessary calls)
- Wastes server resources (answering pointless questions)
- Delay between when event happens and when client finds out

### 🟢 Callback — The Smart Way

Now imagine: you call the delivery company ONCE, leave your phone number, and say "call me when it arrives." Then you go live your life. When the package arrives, THEY call YOU.

That's **callback**. The client **registers itself** with the server, and the server **calls back** when the event occurs.

### The Three Analogies from the Slide (MEMORIZE THESE!):

| Type | Analogy |
|------|---------|
| **Blocking** | Making a call and waiting on hold while the other party is busy with another call |
| **Polling** | Repeatedly calling to check if the other party is available |
| **Callback** | Leaving a message for the other party to call back with certain information |

---

## 📺 SLIDES 12 — Two-Way Communications

Sometimes **both sides** need to be able to initiate communication. This is called **duplex communication**.

### How to achieve it with sockets:
- Use **two sockets** on either side
- With **connection-oriented sockets**, each side acts as **both a client AND a server**

The diagram shows:
```
Process 1 → request → Process 2
Process 1 ← response ← Process 2
(then later...)
Process 1 ← request ← Process 2
Process 1 → response → Process 2
```

Both sides can initiate! Think of it like a **walkie-talkie** where either person can talk first.

---

## 📺 SLIDE 13 — RMI Callbacks (Section Header)

Now we dive into the **technical implementation** of callbacks using **Java RMI** (Remote Method Invocation). 

RMI is Java's way of calling methods on objects that live on **different computers** as if they were local. We covered this in previous lectures. Now we're adding **callbacks** to it.

---

## 📺 SLIDE 14 — RMI Callbacks Explained

### How RMI Callbacks Work:

1. A **callback client registers itself** with an RMI server
2. The server **stores a reference** to the client
3. When a certain **event occurs**, the server **calls back** each registered client

The diagram shows:
```
Server has a "callback list": [C1, C2, C3, C4, C5]
When event happens → server calls back ALL registered clients
```

**Think of it like a newsletter subscription:**
- You subscribe (register) with a news website
- When news breaks, they email (callback) ALL subscribers
- You didn't have to keep checking the website!

---

## 📺 SLIDES 15 & 16 — Multiple Listeners

This is the **Observer Pattern** in distributed systems!

### Multiple Listeners:
- Multiple **listener objects** can register with a single **event source**
- When the event occurs, the event source **notifies ALL registered listeners**

The diagram shows:
```
Listener 1 ──┐
Listener 2 ──┼──→ Event Source
Listener 3 ──┘
```

When event fires:
```
Event Source → send notification → Listener 1
Event Source → send notification → Listener 2  
Event Source → send notification → Listener 3
```

The server has a **"read list"** (callback list) with Listener 1, Listener 2, ... Listener N, and sends notifications to all of them.

**Real-world analogy:** A fire alarm. One alarm (event source), many people (listeners) all get notified simultaneously.

---

## 📺 SLIDE 18 — Callback Implemented by Invoking a Method

This slide shows the **technical mechanism** of how callbacks work:

1. **Listener object** registers with the **Event Source** (calls `register listener`)
2. Event Source stores a reference to the listener
3. When event occurs, Event Source calls `eventOccurred(..)` on the listener object

**Key insight:** The callback is literally just **calling a method on the listener object**. The magic is that this listener object lives on the CLIENT, but the SERVER is calling its method remotely!

This is why RMI is needed — it allows the server to call methods on client-side objects across the network.

---

## 📺 SLIDE 19 — Client Callback (What the Client Must Do)

For a client to receive callbacks, it must do THREE things:

### Step 1: Supply a Remote Interface
Define an interface that the server can call back on. This interface must extend `java.rmi.Remote`.

### Step 2: Instantiate an Object
Create an actual object that **implements** that interface. This object will receive the callbacks.

### Step 3: Pass a Reference to the Server
Call a remote method on the server, **passing a reference to itself**. The server saves this reference in its callback list.

**Analogy:** 
1. You create a "callback card" (interface) with your phone number format
2. You fill in your actual number (implement the interface)
3. You hand the card to the restaurant (pass reference to server)
4. Restaurant calls you when your table is ready (server calls back)

---

## 📺 SLIDE 20 — Client Callback (What the Server Must Do)

The server has two responsibilities:

### Responsibility 1: Collect Client References
Store all the client references in a **data structure** (like a list or vector). This is the "callback list."

### Responsibility 2: Invoke Callback When Event Occurs
When the awaited event happens, the server **iterates through the list** and calls the **callback method** (defined in the client's remote interface) on each registered client.

### Important Technical Note:
> **Two sets of stub-skeletons are needed:**
> - One for the **server remote interface** (normal RMI stuff)
> - One for the **client remote interface** (so server can call back to client)

**This is the key difference from normal RMI** — in normal RMI, only the server has a remote interface. In callback RMI, **both sides have remote interfaces**!

---

## 📺 SLIDE 21 — Callback Client-Server Interactions (The Full Picture)

This is the most detailed technical slide. Let's walk through it step by step:

```
Client Host                          Server Host
─────────────────────────────────────────────────
Client.class                         RMI Registry
SomeInterface_stub.class             SomeInterface_skel.class
CallbackInterface_skel.class         SomeServer.class
                                     CallbackInterface_stub.class
```

### The 5 Steps:

**Step 1:** Client **looks up** the interface object in the RMI Registry on the server host
*(Like looking up a restaurant's phone number in a directory)*

**Step 2:** RMI Registry **returns a remote reference** to the interface object
*(Directory gives you the phone number)*

**Step 3:** Via the server stub, client invokes a remote method to **register itself for callback**, passing a remote reference to itself. Server saves this in its callback list.
*(You call the restaurant and give them YOUR number)*

**Step 4:** Via the server stub, client **interacts with the server** normally (calls remote methods)
*(You order food, ask questions, etc.)*

**Step 5:** When the anticipated event occurs, server **makes a callback** to each registered client via the CallbackInterface stub (server side) and CallbackInterface skeleton (client side)
*(Restaurant calls you back when your table/order is ready)*

**Memory trick for the stubs/skeletons:**
- **Stub** = the fake local object that represents the remote object (on the CALLER's side)
- **Skeleton** = the receiver on the remote side that unpacks the call
- In callbacks: server has a stub for the client's callback interface, client has a skeleton for its own callback interface

---

## 📺 SLIDES 22-27 — RMI Callback Example (Continued)

### The Server Interface (`TemperatureSensor`):

```java
interface TemperatureSensor extends java.rmi.Remote {
    public double getTemperature() throws java.rmi.RemoteException;
    
    public void addTemperatureListener(TemperatureListener listener)
        throws java.rmi.RemoteException;
    
    public void removeTemperatureListener(TemperatureListener listener)
        throws java.rmi.RemoteException;
}
```

**What this means in plain English:**
- `getTemperature()` — just ask "what's the temp right now?" (normal RMI call)
- `addTemperatureListener()` — **"Hey server, add me to your callback list!"** This is the registration method. Notice it takes a `TemperatureListener` as a parameter — that's the client passing a reference to ITSELF!
- `removeTemperatureListener()` — **"Hey server, remove me from your callback list"** — unsubscribe

**Key observation:** The server interface accepts a `TemperatureListener` object as a parameter. This is how the client passes its reference to the server. The server will later use this reference to call back!

---

### The Client Interface (`TemperatureListener`):

```java
interface TemperatureListener extends java.rmi.Remote {
    public void temperatureChanged(double temperature)
        throws java.rmi.RemoteException;
}
```

**What this means in plain English:**
This is the **callback interface** — the interface that the SERVER will call on the CLIENT.

- It extends `java.rmi.Remote` — because the server needs to call this method REMOTELY (across the network, on the client's machine!)
- `temperatureChanged(double temperature)` — this is the **callback method**. When the server detects a temperature change, it calls THIS method on every registered client, passing the new temperature value.

**This is the magic!** The server calls a method on the client. The client defines what happens when that method is called (print it, display it, trigger an alarm, etc.)

**Memory trick:** 
- Server interface = what the CLIENT calls on the SERVER
- Listener/Callback interface = what the SERVER calls on the CLIENT
- They're mirror images of each other!

---

### The Server Implementation:

```java
public class TemperatureSensorServer extends UnicastRemoteObject 
    implements TemperatureSensor, Runnable {
    
    public void addTemperatureListener(TemperatureListener listener)
        throws java.rmi.RemoteException {
        list.add(listener);  // Add client to callback list
    }
    
    public void run() {
        for (;;) {  // Infinite loop - keep monitoring
            if (checkTempChanged()) {
                // Notify registered listeners
                notifyListeners();
            }
        }
    }
```

**Breaking this down:**

1. **`extends UnicastRemoteObject`** — makes this a proper RMI server object
2. **`implements TemperatureSensor`** — implements the server interface
3. **`implements Runnable`** — means it can run in a thread (for continuous monitoring)
4. **`addTemperatureListener()`** — simply adds the client reference to a list called `list`
5. **`run()`** — runs in an infinite loop, constantly checking if temperature changed, and if so, calls `notifyListeners()`

---

### The `notifyListeners()` Method:

```java
private void notifyListeners() {
    for (Enumeration e = list.elements(); e.hasMoreElements(); ) {
        TemperatureListener listener = 
            (TemperatureListener) e.nextElement();
        listener.temperatureChanged(temp);  // THE CALLBACK!
        list.remove(listener);
    }
}
```

**This is where the magic happens!**

- Loop through every registered listener in the list
- Call `temperatureChanged(temp)` on each one
- **`listener.temperatureChanged(temp)`** — this looks like a local method call, but it's actually a **REMOTE METHOD CALL** across the network to the client's machine!
- After notifying, remove the listener from the list

**Think of it like:** The restaurant going through their waiting list, calling each person's number one by one to say "your table is ready!"

---

### The `main()` Method of the Server:

```java
public static void main(String args[]) {
    TemperatureSensorServer sensor = new TemperatureSensorServer();
    String registration = "rmi://" + registry + "/TemperatureSensor";
    Naming.rebind(registration, sensor);  // Register with RMI registry
    Thread thread = new Thread(sensor);
    thread.start();  // Start monitoring in background thread
}
```

**Steps:**
1. Create the server object
2. Register it with the RMI registry (so clients can find it)
3. Start it running in a background thread (so it keeps monitoring continuously)

---

### The Client Implementation:

```java
public class TemperatureMonitor extends UnicastRemoteObject 
    implements TemperatureListener {
    
    public static void main(String args[]) {
        Remote remoteService = Naming.lookup(registration);
        TemperatureSensor sensor = (TemperatureSensor) remoteService;
        
        double reading = sensor.getTemperature();
        System.out.println("Original temp: " + reading);
        
        TemperatureMonitor monitor = new TemperatureMonitor();
        sensor.addTemperatureListener(monitor);  // REGISTER FOR CALLBACK!
    }
    
    public void temperatureChanged(double temperature)
        throws java.rmi.RemoteException {
        System.out.println("Temperature change event: " + temperature);
    }
}
```

**Breaking this down:**

1. **`extends UnicastRemoteObject`** — the CLIENT is also an RMI object! Because the server needs to call methods on it remotely. This is the key difference from normal RMI!
2. **`implements TemperatureListener`** — implements the callback interface
3. **`Naming.lookup()`** — find the server in the RMI registry
4. **`sensor.getTemperature()`** — get current temperature (normal RMI call)
5. **`sensor.addTemperatureListener(monitor)`** — **REGISTER ITSELF** for callbacks, passing `monitor` (which is itself!) to the server
6. **`temperatureChanged()`** — this is the callback method. When the server calls this, the client just prints the new temperature

**The beautiful flow:**
```
Client registers → Server stores reference
Temperature changes → Server calls temperatureChanged() on client
Client receives the call → Prints new temperature
```

---

## 📺 SLIDE 28 — Running the Example

The steps to run this RMI callback application:

1. **Compile** the applications and generate stub/skeleton files for **BOTH** `TemperatureSensorServer` AND `TemperatureSensorMonitor` (remember — both need stubs/skeletons because both have remote interfaces!)
2. Run the **rmiregistry** application (the naming service)
3. Run the **TemperatureSensorServer**
4. Run the **TemperatureSensorMonitor** (client)

**Why generate stubs for both?** Because in callback RMI, the server needs a stub for the client's callback interface, and the client needs a skeleton for its own callback interface. Both sides are "servers" in a sense!

---

## 📺 SLIDE 29 — Asynchronous Callback Functions and Thread Safety

This is a **critical concept** that often appears in exam questions!

### The Problem:
Callback functions use **threads in the background**. Here's what happens:

```
Main Thread: makes remote call → continues doing other work
Worker Thread: waits for response → calls callback function when done
```

Both threads are running **simultaneously**. This creates **thread safety issues**!

### What are thread safety issues?
Imagine two threads both trying to update the same variable at the same time:
- Thread 1 reads value: 5
- Thread 2 reads value: 5
- Thread 1 adds 1, writes: 6
- Thread 2 adds 1, writes: 6
- **Expected result: 7, Actual result: 6** — BUG!

### The Key Points:
- **Main thread** does the remote call and then continues working
- A **worker thread** calls the callback function when response arrives
- Main thread is running **at the same time** as the callback
- You have to **handle thread safety issues manually** (using synchronization, locks, etc.)

**Memory trick:** Callbacks = threads = danger of race conditions = need synchronization!

---

## 📺 SLIDE 30 — Asynchronous Messaging Services (Section Header)

Now we move to the **second major approach** to async communication — **Messaging Services**!

If callbacks are like giving someone your phone number to call back, messaging services are like a **sophisticated postal system** with sorting offices, guaranteed delivery, and multiple recipients.

---

## 📺 SLIDE 31 — Event Based Architectures

This slide introduces the **event bus** concept:

```
Component ←──────────────── Component
     ↑          Event Bus        ↓
     └──────────────────────────┘
                    ↑
                Component (publishes)
```

### How it works:
- **Components** can publish events TO the event bus
- **Components** can receive events FROM the event bus
- The event bus acts as a **middleman/broker**
- Components don't talk to each other directly — they talk through the bus!

**Real-world analogy:** Think of a **radio station**:
- Radio station = event bus
- DJ = publisher (sends out music/events)
- Listeners = subscribers (receive the music/events)
- The DJ doesn't call each listener individually — they just broadcast!

**Benefits of event-based architecture:**
- **Loose coupling** — components don't need to know about each other
- **Scalability** — easy to add more publishers or subscribers
- **Flexibility** — components can be added/removed without breaking others

---

## 📺 SLIDE 32 — Java Message Service (JMS)

Now we get to the **star of the show** — JMS!

### What is JMS?
JMS is a **specification** (not an implementation — important distinction!) that describes a common way for Java programs to:
- **Create** messages
- **Send** messages
- **Receive** messages
- **Read** messages

...in a distributed enterprise environment.

### The Three Key Properties of JMS:

#### 1. 🔗 Loosely Coupled Communication
Sender and receiver don't need to know about each other. They just talk through the messaging system. The sender doesn't care who receives the message, and the receiver doesn't care who sent it.

#### 2. ⚡ Asynchronous Messaging
The sender sends a message and **immediately continues** doing other work. It doesn't wait for the receiver to process the message. The receiver processes it whenever it's ready.

#### 3. ✅ Reliable Delivery
**A message is guaranteed to be delivered once and only once.** This is HUGE. No lost messages, no duplicate messages. The messaging system takes responsibility for delivery.

**Memory trick for the 3 properties:** **LAR** — **L**oosely coupled, **A**synchronous, **R**eliable

### What's OUTSIDE the JMS specification:
- **Security services** — JMS doesn't define how to secure messages
- **Management services** — JMS doesn't define how to manage the messaging system

These are left to individual vendors to implement.

---

## 📺 SLIDE 33 — A JMS Application

A JMS application has **four main components**:

### 1. 📱 JMS Clients
Java programs that **send and/or receive** messages. Your application code. Could be a producer (sender), consumer (receiver), or both.

### 2. 📨 Messages
The actual data being sent. Has a specific structure (we'll see this later — header, properties, body).

### 3. ⚙️ Administered Objects
These are **pre-configured JMS objects** created by an administrator for clients to use. Two types:
- **ConnectionFactory** — used to create connections to the messaging system
- **Destination** — where messages go (either a **Queue** for point-to-point, or a **Topic** for publish-subscribe)

Clients look these up using **JNDI** (Java Naming and Directory Interface) — basically a directory service.

### 4. 🏭 JMS Provider
The actual **messaging system** that implements the JMS specification. Examples: Apache ActiveMQ, IBM MQ, etc. It handles all the actual message routing, storage, and delivery.

**Analogy for the whole system:**
- **JMS Provider** = the postal service (infrastructure)
- **ConnectionFactory** = the post office (where you go to send/receive)
- **Destination** = the mailbox address
- **Messages** = the letters
- **JMS Clients** = you and the person you're writing to

---

## 📺 SLIDE 34 — JMS Messaging Domains

JMS supports **two completely different messaging models**. This is a VERY important distinction for your exam!

### 🔵 Model 1: Point-to-Point (PTP)

**Built around the concept of message QUEUES**

Key characteristics:
- Each message has **only ONE consumer**
- Message goes into a queue, ONE receiver picks it up
- Like sending a **letter** — only one person opens it
- The receiver **acknowledges** receipt

**Use case:** Order processing — one order should be processed by exactly one worker, not multiple!

### 🟡 Model 2: Publish-Subscribe (Pub-Sub)

**Built around the concept of TOPICS**

Key characteristics:
- Each message has **MULTIPLE consumers**
- Publisher sends to a topic, ALL subscribers receive it
- Like a **newspaper** — many people read the same edition
- Subscribers must be active (or use durable subscription) to receive messages

**Use case:** Stock price updates — one price update should go to ALL interested clients!

### Quick Comparison Table:

| Feature | Point-to-Point | Publish-Subscribe |
|---------|---------------|-------------------|
| Destination type | **Queue** | **Topic** |
| Number of consumers | **One** | **Many** |
| Analogy | Letter/Email | Newspaper/Broadcast |
| Use case | Task processing | Event notification |

**Memory trick:** 
- **P**oint-to-**P**oint = **P**rivate (one person)
- **Pub**lish-**Sub**scribe = **P**ublic (everyone)

---

## 📺 SLIDE 35 — Point-to-Point Messaging (Diagram)

The diagram shows:

```
Client1 ──sends──→ [Queue] ──consumes──→ Client2
                      ←──acknowledges──
```

**The flow:**
1. Client1 **sends** a message to the Queue
2. Message sits in the Queue waiting
3. Client2 **consumes** (reads and removes) the message from the Queue
4. Client2 **acknowledges** receipt back to the Queue
5. Queue removes the message (it's been delivered!)

**Key point:** The message is **removed from the queue** once consumed. If Client3 comes along later, the message is GONE. Only one consumer gets it.

**Real-world analogy:** A **task queue** in a call center. A customer's call goes into a queue. ONE agent picks it up. Once that agent takes the call, it's removed from the queue. No other agent handles the same call.

---

## 📺 SLIDE 36 — Publish/Subscribe Messaging (Diagram)

The diagram shows:

```
Client1 ──publishes──→ [Topic] ──delivers──→ Client2
                                └──delivers──→ Client3
```

**The flow:**
1. Client1 **publishes** a message to the Topic
2. Topic **delivers** the message to ALL subscribers
3. Both Client2 AND Client3 receive the SAME message
4. No acknowledgment needed (fire and forget)

**Key point:** The message is **delivered to everyone** who subscribed. Multiple consumers get the same message.

**Real-world analogy:** A **WhatsApp group**. You send one message, everyone in the group receives it. You don't send individual copies to each person.

---

## 📺 SLIDE 37 — Message Consumptions (Continued)

```java
// Synchronous consumption example
connection.start();
Message m = consumer.receive();        // BLOCKS until message arrives
// OR
Message m = consumer.receive(1000);    // Times out after 1000ms
```

**Think of it like:** Standing at your mailbox waiting for the postman. You just stand there until mail arrives. Blocking!

### 🟢 Asynchronous Consumption
- Client registers a **message listener** with the consumer
- Whenever a message arrives, JMS provider **automatically calls** `onMessage()` on the listener
- Client doesn't have to wait or check — it just gets notified!

```java
// Asynchronous consumption example
MessageListener listener = new myListener();
consumer.setMessageListener(listener);
// Now go do other things... onMessage() will be called automatically!
```

**Think of it like:** Setting up a **doorbell**. You don't stand at the door waiting. You go about your day, and when mail arrives, the doorbell rings and you go answer it.

### Key Comparison:

| | Synchronous | Asynchronous |
|--|-------------|--------------|
| How | Call `receive()` | Register `MessageListener` |
| Blocks? | **YES** | **NO** |
| Callback method | None | **`onMessage()`** |
| Analogy | Waiting at mailbox | Doorbell notification |

**Memory trick:** Async consumption = **"Don't call us, we'll call you"** (via `onMessage()`)

---

## 📺 SLIDE 38 — JMS API Programming Model

This is the **most important structural slide** for JMS. It shows how all the pieces connect together. Let's walk through it carefully because this WILL appear in your exam!

### The Hierarchy (Top to Bottom):

```
ConnectionFactory
      ↓ creates
  Connection
      ↓ creates
   Session
   ↙        ↘
creates    creates
  ↓              ↓
Message      Message
Producer     Consumer
  ↓              ↓
sends to    receives from
  ↓              ↓
Destination  Destination
```

And Session also creates → **Messages**

### Let's explain each piece:

#### 🏭 ConnectionFactory
- The **starting point** of everything
- Looked up via JNDI (the naming service)
- Used to **create Connections**
- Think of it as the **post office building** — you go there to start the process

#### 🔌 Connection
- Represents an **active connection** to the JMS provider
- Created by the ConnectionFactory
- Used to **create Sessions**
- Think of it as **walking into the post office** and getting a service number

#### 📋 Session
- A **single-threaded context** for producing and consuming messages
- Created by the Connection
- Used to create:
  - **Message Producers** (senders)
  - **Message Consumers** (receivers)
  - **Messages** themselves
- Think of it as the **service window** at the post office

#### 📤 Message Producer
- Created by the Session
- **Sends messages** to a Destination
- Think of it as the **person handing over a letter** to be sent

#### 📥 Message Consumer
- Created by the Session
- **Receives messages** from a Destination
- Think of it as the **person collecting their mail**

#### 📦 Message
- The actual **data being sent**
- Created by the Session
- Think of it as the **letter or package**

#### 📮 Destination
- Where messages are **sent to** or **received from**
- Either a **Queue** (point-to-point) or **Topic** (pub-sub)
- Think of it as the **mailbox address**

### The Complete Flow in One Sentence:
> Use a **ConnectionFactory** to create a **Connection**, use the Connection to create a **Session**, use the Session to create a **Producer** and/or **Consumer** and **Messages**, then send Messages to or receive Messages from a **Destination**.

**Memory trick for the order:** **"Factory → Connection → Session → Producer/Consumer → Destination"**
Or remember: **"FC-SP-CD"** — **F**actory **C**reates, **S**ession **P**roduces, **C**onsumer **D**elivers

---

## 📺 SLIDE 39 — JMS Client Example (Setting Up)

Now let's see the actual code for setting up a JMS connection:

```java
// Step 1: Get JNDI context (the naming service)
InitialContext jndiContext = new InitialContext();

// Step 2: Look up the ConnectionFactory
ConnectionFactory cf = jndiContext.lookup(connectionfactoryname);

// Step 3: Create a Connection
Connection connection = cf.createConnection();

// Step 4: Create a Session
Session session = connection.createSession(
    false,                    // not transacted
    Session.AUTO_ACKNOWLEDGE  // auto-acknowledge messages
);

// Step 5: Look up Destinations
Destination dest1 = (Queue) jndiContext.lookup("/jms/myQueue");  
// For Point-to-Point

Destination dest2 = (Topic) jndiContext.lookup("/jms/myTopic"); 
// For Publish-Subscribe
```

### Breaking Down `createSession(false, Session.AUTO_ACKNOWLEDGE)`:

**First parameter (transacted):**
- `false` = not a transacted session (normal mode)
- `true` = transacted session (we'll see this later)

**Second parameter (acknowledge mode):**
- `Session.AUTO_ACKNOWLEDGE` = JMS automatically acknowledges messages
- Other options exist but AUTO_ACKNOWLEDGE is the most common

### The Two Destination Types:
- **Queue** → for Point-to-Point messaging
- **Topic** → for Publish-Subscribe messaging

Both are looked up from JNDI — they're **administered objects** pre-configured by an admin.

---

## 📺 SLIDE 40 — Producer Sample

Here's how to **send messages** as a producer:

```java
// Step 1: Setup connection and create session (as shown before)

// Step 2: Create a MessageProducer
MessageProducer producer = session.createProducer(dest1);

// Step 3: Create and send a message
Message m = session.createTextMessage();
m.setText("just another message");
producer.send(m);

// Step 4: Close the connection when done
connection.close();
```

### Breaking it down:

**`session.createProducer(dest1)`**
- Creates a producer that will send to `dest1` (the queue or topic)
- The destination is specified at producer creation time

**`session.createTextMessage()`**
- Creates a new empty TextMessage object
- Session creates the message (not the producer!)

**`m.setText("just another message")`**
- Sets the content of the message

**`producer.send(m)`**
- Actually sends the message to the destination
- This is **non-blocking** — returns immediately after handing message to JMS provider
- The JMS provider takes responsibility for delivery

**`connection.close()`**
- Always close your connection when done!
- Releases resources

**Real-world analogy:**
```
Create producer = Go to post office counter
createTextMessage = Get a blank envelope
setText = Write your letter and put it in envelope
producer.send = Hand it to the postal worker
connection.close = Leave the post office
```

---

## 📺 SLIDE 41 — Consumer Sample (Synchronous)

Here's how to **receive messages synchronously** (blocking):

```java
// Step 1: Setup connection and create session

// Step 2: Create a MessageConsumer
MessageConsumer consumer = session.createConsumer(dest1);

// Step 3: Start the connection (IMPORTANT!)
connection.start();

// Step 4: Receive a message (BLOCKS until message arrives)
Message m = consumer.receive();
```

### Key Points:

**`session.createConsumer(dest1)`**
- Creates a consumer that listens to `dest1`
- Specifies which destination to receive from

**`connection.start()`**
- **VERY IMPORTANT** — you must call this before receiving!
- Activates the connection to begin delivering messages
- Without this, no messages will be delivered

**`consumer.receive()`**
- **BLOCKS** the current thread until a message arrives
- Returns the message when one arrives
- Can also use `consumer.receive(1000)` to timeout after 1000 milliseconds

**Variants of receive():**

| Method | Behavior |
|--------|----------|
| `receive()` | Blocks indefinitely until message arrives |
| `receive(timeout)` | Blocks until message arrives OR timeout expires |
| `receiveNoWait()` | Returns immediately, null if no message |

---

## 📺 SLIDE 42 — Consumer Sample (Asynchronous)

Here's the **better way** — asynchronous consumption:

```java
// Step 1: Setup connection and create session

// Step 2: Create consumer
MessageConsumer consumer = session.createConsumer(dest1);

// Step 3: Create and register a MessageListener
MessageListener listener = new myListener();
consumer.setMessageListener(listener);

// Step 4: Start the connection
connection.start();

// Now the program can do other things!
// onMessage() will be called automatically when messages arrive
```

### The Listener Class:
```java
class myListener implements MessageListener {
    public void onMessage(Message msg) {
        // This is called automatically when a message arrives!
        // Read the message and do computation
    }
}
```

### Key Points:

**`consumer.setMessageListener(listener)`**
- Registers the listener with the consumer
- From this point on, JMS will automatically call `onMessage()` when messages arrive
- **Non-blocking** — your main thread is free to do other work

**`onMessage(Message msg)`**
- The **callback method** that JMS calls when a message arrives
- Runs in a **separate thread** managed by JMS
- You implement this method with your message processing logic

**The beautiful thing:** After setting the listener, your main thread is completely free. JMS handles all the waiting and thread management for you!

---

## 📺 SLIDE 43 — Listener Example (Full Code)

Here's a complete, realistic `onMessage()` implementation:

```java
public void onMessage(Message message) {
    TextMessage msg = null;
    
    try {
        if (message instanceof TextMessage) {
            // Cast to TextMessage to access text content
            msg = (TextMessage) message;
            System.out.println("Reading message: " + msg.getText());
        } else {
            // Handle unexpected message type
            System.out.println("Message of wrong type: " + 
                message.getClass().getName());
        }
    } catch (JMSException e) {
        System.out.println("JMSException in onMessage(): " + e.toString());
    } catch (Throwable t) {
        System.out.println("Exception in onMessage(): " + t.getMessage());
    }
}
```

### Breaking it down:

**`message instanceof TextMessage`**
- Check what TYPE of message arrived before processing
- Good practice — always check the type first!

**`msg.getText()`**
- Extract the text content from the TextMessage

**Why two catch blocks?**
- `JMSException` — for JMS-specific errors
- `Throwable` — catches ANY other error that might occur during processing
- Important: **never let exceptions escape from `onMessage()`** — it can cause problems with the JMS provider

**Real-world analogy:** 
```
onMessage() = Your doorbell rings
instanceof check = Look through peephole to see what kind of delivery it is
msg.getText() = Open the package and read the contents
catch blocks = What to do if something goes wrong
```

---

## 📺 SLIDE 44 — JMS Messages (Structure)

Every JMS message has **three parts**. Think of it like a letter:

### Part 1: 📋 Message Header
- Used for **identifying and routing** messages
- Contains **vendor-specified values** but can also have application-specific data
- Typically **name/value pairs**
- Examples of header fields:
  - `JMSMessageID` — unique ID for the message
  - `JMSDestination` — where the message is going
  - `JMSTimestamp` — when it was sent
  - `JMSExpiration` — when it expires
  - `JMSPriority` — priority level (0-9)
  - `JMSReplyTo` — where to send replies

**Analogy:** The **envelope** of a letter — has the address, return address, stamp, postmark

### Part 2: 🏷️ Message Properties (Optional)
- Additional **application-specific** name/value pairs
- Used for **message filtering** (selectors — we'll see this later)
- You can add custom properties like `priority`, `type`, `region`, etc.

**Analogy:** **Sticky notes** on the outside of the envelope with extra info

### Part 3: 📄 Message Body (Optional)
- Contains the **actual data**
- Five different message body types in JMS specification (next slide!)

**Analogy:** The **letter inside** the envelope — the actual content

---

## 📺 SLIDE 45 — JMS Message Types

There are **five message types** in JMS. This is a common MCQ topic!

| Message Type | Contains | Key Methods |
|-------------|----------|-------------|
| **TextMessage** | A String | `getText()`, `setText()` |
| **MapMessage** | Set of name/value pairs | `setString()`, `setDouble()`, `setLong()`, `getDouble()`, `getString()` |
| **BytesMessage** | Stream of uninterpreted bytes | `writeBytes()`, `readBytes()` |
| **StreamMessage** | Stream of primitive values | `writeString()`, `writeDouble()`, `writeLong()`, `readString()` |
| **ObjectMessage** | Serialized Java object | `setObject()`, `getObject()` |

### When to use each:

**TextMessage** 
- Simple text, XML, JSON
- Most commonly used
- Example: `"Hello World"` or `"<order><id>123</id></order>"`

**MapMessage**
- Structured data with named fields
- Example: `{"name": "John", "age": 25, "salary": 50000.0}`

**BytesMessage**
- Raw binary data
- Example: Image files, encrypted data, custom binary formats

**StreamMessage**
- Sequential stream of primitive values
- Example: A series of numbers or strings in order

**ObjectMessage**
- Any serializable Java object
- Example: Sending a `Customer` object directly
- **Warning:** Both sender and receiver need the same class definition!

**Memory trick:** **"T-M-B-S-O"** — **T**ext, **M**ap, **B**ytes, **S**tream, **O**bject
Or: **"The Mighty Blue Striped Octopus"** 🐙

---

## 📺 SLIDE 46 — More JMS Features (Part 1 Continued)

### Feature 2: 🔄 Request/Reply Pattern (Continued)

**How it works step by step:**

1. Requester creates a **temporary queue** for replies
2. Requester sends a message with `JMSReplyTo` set to the temporary queue
3. Responder receives the message, sees the `JMSReplyTo` address
4. Responder sends reply TO that temporary queue
5. Responder sets `JMSCorrelationID` to match the original `JMSMessageID` (so requester knows which reply belongs to which request)
6. Requester receives the reply from its temporary queue

```
Requester                    Responder
    |                            |
    |--[request + replyTo]------>|
    |                            |
    |<--[reply + correlationID]--|
    |                            |
```

**Real-world analogy:** 
- You send a letter with your **return address** on it
- The recipient writes back TO your return address
- You match the reply to your original letter by a **reference number**

**`JMSCorrelationID`** is the key — it links the reply back to the original request. Without it, if you send multiple requests, you wouldn't know which reply belongs to which request!

**Use case:** When you need a response to your message but still want the benefits of async messaging (loose coupling, reliability).

---

## 📺 SLIDE 47 — More JMS Features (Part 2)

### Feature 3: 💾 Transacted Sessions

Remember database transactions? JMS has them too!

```java
// Create a TRANSACTED session
session = connection.createSession(true, 0);
// Note: first parameter is TRUE for transacted
```

**What transacted sessions allow:**
- Group multiple message operations into a **single atomic unit**
- Either ALL operations succeed (commit) or ALL fail (rollback)
- You can combine **queue AND topic operations** in one transaction

**Example from the slide:**
```java
void onMessage(Message m) {
    try {
        Message m2 = processOrder(m);    // Process the order
        publisher.publish(m2);            // Publish result
        session.commit();                 // ALL OR NOTHING - commit!
    } catch(Exception e) {
        session.rollback();               // Something went wrong - undo everything!
    }
}
```

**Breaking this down:**
- Receive a message (order request)
- Process it and create a result message
- Publish the result
- If everything worked → `commit()` (make it permanent)
- If anything failed → `rollback()` (undo everything, message goes back to queue)

**Real-world analogy:** 
Think of it like a **bank transfer**:
- Debit account A AND credit account B must BOTH happen
- If either fails, NEITHER should happen
- `commit()` = both succeed, transfer complete
- `rollback()` = something failed, put the money back

**Why is this important?**
Without transactions, if your system crashes after publishing the result but before acknowledging the original message, you could end up with:
- The original message processed twice (duplicate processing)
- Or the result published but original not acknowledged

Transactions prevent these **data consistency problems**!

---

## 📺 SLIDE 48 — More JMS Features (Part 3)

### Feature 4: 📬 Persistent/Non-Persistent Delivery

JMS gives you control over how reliably messages are delivered:

#### Persistent Delivery (Default)
- Messages are **stored to disk** by the JMS provider
- If the JMS provider crashes and restarts, messages are **not lost**
- **Slower** (disk I/O involved)
- Use when message loss is **unacceptable**

#### Non-Persistent Delivery
- Messages are kept **only in memory**
- If JMS provider crashes, messages are **lost**
- **Faster** (no disk I/O)
- Use when speed matters more than reliability

```java
// Set delivery mode on the producer
producer.setDeliveryMethod(DeliveryMode.NON_PERSISTENT);

// Or set it per message when sending
producer.send(mesg, DeliveryMode.NON_PERSISTENT, 3, 1000);
//                                                ↑  ↑
//                                          priority  expiry(ms)
```

**The `send()` parameters explained:**
- `mesg` — the message to send
- `DeliveryMode.NON_PERSISTENT` — delivery mode
- `3` — priority (0-9, higher = more important)
- `1000` — expiry time in milliseconds (message expires after 1 second)

**Real-world analogy:**
- **Persistent** = Registered mail with tracking — guaranteed delivery, slower, costs more
- **Non-persistent** = Regular mail — faster, cheaper, but might get lost

---

### Feature 5: 🔍 Message Selectors

This is a **powerful filtering feature** — consumers can choose which messages they want to receive!

```java
// Only receive messages where priority > 6 AND type = 'alert'
subscriber = session.createSubscriber(
    topic, 
    "priority > 6 AND type = 'alert'"
);
```

**The selector syntax is SQL-like** — uses conditions based on message **header** and **property** values.

**How it works:**
- The selector is evaluated by the JMS provider
- Only messages that **match the selector** are delivered to that consumer
- Non-matching messages are simply not delivered (they may go to other consumers)

**In Point-to-Point:**
- Selector determines which **single recipient** gets the message
- Like routing rules in email

**In Publish-Subscribe:**
- Selector acts as a **filter**
- Subscriber only gets messages matching their filter
- Like subscribing to a newspaper but only reading the sports section

**Real-world examples:**

```sql
-- Only high priority alerts
"priority > 6 AND type = 'alert'"

-- Only messages for a specific region
"region = 'ASIA' OR region = 'EUROPE'"

-- Only messages above a certain value
"orderValue > 1000"

-- Only messages of a specific type
"messageType = 'ORDER' AND status = 'PENDING'"
```

**Memory trick:** Message selectors = **SQL WHERE clause for messages**

---

## 📺 SLIDE 49 — JMS Providers

JMS is just a **specification** — you need an actual **implementation** (provider) to use it. Here are the main ones:

| Provider | Vendor |
|----------|--------|
| **SunONE Message Queue** | Sun Microsystems |
| **MQ JMS** | IBM |
| **WebLogic JMS** | BEA (now Oracle) |
| **JMSCourier** | Codemesh |
| **Apache ActiveMQ** | Apache (Open Source) |

### Key Point for Your Exam:
**Apache ActiveMQ** is the most popular **open-source** JMS provider. It's free and widely used in practice.

**Why does this matter?**
Because JMS is a specification, you can **switch providers** without changing your application code! This is the beauty of programming to an interface/specification rather than a specific implementation.

**Analogy:** JMS is like the **USB standard**. Your USB device works with any computer that supports USB, regardless of manufacturer. Similarly, your JMS code works with any JMS provider.

---

## 📺 SLIDE 50 — JMS API in a JEE Application

JMS doesn't exist in isolation — it's part of the **Java Enterprise Edition (JEE)** ecosystem!

### Key Facts:
- Since **J2EE 1.3**, JMS API has been an **integral part** of the platform
- JEE components can use JMS API to **send messages**
- These messages can be consumed **asynchronously** by a specialized Enterprise Java Bean

### The Special Bean: Message-Driven Bean (MDB)
- A type of **Enterprise Java Bean (EJB)**
- Specifically designed to **consume JMS messages asynchronously**
- Acts like a **message listener** but with all the enterprise features of EJB
  - Transaction management
  - Security
  - Resource pooling
  - etc.

**How it fits together:**
```
JEE Component          JMS Queue/Topic        Message-Driven Bean
(Servlet, EJB, etc.)                          (MDB)
      |                      |                      |
      |---sends message------>|                      |
      |                      |---delivers message--->|
      |                      |                      |
      |                      |              onMessage() called
      |                      |              processes message
```

**Real-world analogy:**
- JEE Component = Customer placing an order on a website
- JMS Queue = Order queue in a warehouse
- Message-Driven Bean = Warehouse worker who processes orders

The customer doesn't wait for the order to be processed — they just place it and move on. The warehouse worker processes it asynchronously!

---

## 📺 SLIDE 51 — Microsoft Messaging Queue

For the **.NET world**, Microsoft has their own equivalent:

**Microsoft Message Queuing (MSMQ)**
- The **.NET equivalent of JMS**
- Same concepts, different implementation
- Reference: https://msdn.microsoft.com/en-us/library/ms731089.aspx

### Key Point for Your Exam:
The **concepts are the same** — queues, topics, producers, consumers, async delivery — but the **API and implementation** are different (C# instead of Java, MSMQ instead of JMS providers).

**This shows that async messaging is a universal concept**, not just a Java thing. Every major platform has its own implementation:
- Java → **JMS**
- .NET → **MSMQ**
- Cloud → **AWS SQS**, **Azure Service Bus**, **Google Pub/Sub**

---

## 📺 SLIDE 52 — Summary

The lecture wraps up with these key takeaways:

### 1. Asynchronous Communication = Non-Blocking Calls
Helps distributed components communicate **without waiting** for each other. Maximizes **performance** and **response time**.

### 2. Two Main Approaches:
- **Callback Functions** — direct server-to-client method calls
- **Messaging Services** — indirect communication through a message broker

### 3. When to Stay Synchronous:
Some calls **must** be synchronous if further processing **cannot continue** without the server's response. Don't make everything async just because you can!

---

# 🎯 THE BIG PICTURE — Putting It All Together

Let's connect everything with one final story:

Imagine you're building a **stock trading platform**:

**Problem:** Stock prices change constantly. 10,000 clients need to know about price changes instantly. You can't have each client polling the server every second — that's 10,000 requests per second just for polling!

**Solution 1 — RMI Callbacks:**
- Each client registers with the server as a `PriceListener`
- Server maintains a callback list of all registered clients
- When price changes, server calls `priceChanged()` on each client
- Works great but server must manage thousands of connections directly

**Solution 2 — JMS Pub/Sub:**
- Server publishes price changes to a JMS Topic
- Each client subscribes to the topic
- JMS provider handles delivery to all subscribers
- Much more scalable — server just publishes once, JMS does the rest
- Clients can use message selectors to only receive prices for stocks they care about
- Durable subscriptions ensure clients don't miss updates when briefly offline

**Which is better?** For this use case, JMS Pub/Sub wins because:
- More scalable (JMS handles the fan-out)
- More reliable (persistent delivery)
- Looser coupling (server doesn't know about individual clients)
- Better filtering (message selectors)

---

# 📝 CHEAT SHEET — One A4 Page Summary

Here's everything worth writing on your referral sheet, organized by importance:

---

## 🔑 CORE CONCEPTS

**Synchronous = Blocking = Serial**
- Caller waits until called function returns
- Control passed to called function

**Asynchronous = Non-Blocking = Parallel**
- Control returned immediately to caller
- Called function runs in background
- Caller retrieves result later

**When to use async:** Only on functions **expected** to take long time (heavy processing, disk I/O, GUI responsiveness)

---

## 🔑 POLLING vs CALLBACK vs BLOCKING

| Type | Analogy |
|------|---------|
| Blocking | Call and wait on hold |
| Polling | Repeatedly calling to check |
| Callback | Leave message, they call back |

---

## 🔑 RMI CALLBACKS — KEY FACTS

- Client **registers** itself with server (passes remote reference)
- Server stores references in **callback list**
- Server calls **callback method** on each client when event occurs
- **TWO sets** of stub-skeletons needed (server interface + client callback interface)
- Client must **extend UnicastRemoteObject** (client is also an RMI object!)
- Client must **implement** the callback interface

**Steps:**
1. Client looks up server in RMI Registry
2. Registry returns remote reference
3. Client registers itself for callback
4. Client interacts with server normally
5. Server calls back when event occurs

**Thread Safety:** Callbacks use background threads → must handle thread safety manually!

---

## 🔑 JMS — KEY FACTS

**Three properties:** Loosely coupled, Asynchronous, Reliable (once and only once delivery)

**Outside JMS spec:** Security services, Management services

**Four components:**
- JMS Clients (send/receive)
- Messages
- Administered Objects (ConnectionFactory, Destination)
- JMS Provider (implements JMS)

---

## 🔑 JMS MESSAGING DOMAINS

| | Point-to-Point | Publish-Subscribe |
|--|----------------|-------------------|
| Destination | **Queue** | **Topic** |
| Consumers | **ONE** | **MANY** |
| Analogy | Letter | Newspaper |

---

## 🔑 JMS API HIERARCHY

```
ConnectionFactory → Connection → Session
Session → MessageProducer → sends to Destination
Session → MessageConsumer → receives from Destination
Session → creates Messages
```

---

## 🔑 MESSAGE CONSUMPTION

**Synchronous:** Call `receive()` — BLOCKS until message arrives

**Asynchronous:** Register `MessageListener` → `onMessage()` called automatically

---

## 🔑 FIVE MESSAGE TYPES (T-M-B-S-O)

| Type | Contains |
|------|----------|
| **T**extMessage | String |
| **M**apMessage | Name/value pairs |
| **B**ytesMessage | Raw bytes |
| **S**treamMessage | Primitive values stream |
| **O**bjectMessage | Serialized object |

---

## 🔑 ADVANCED JMS FEATURES

**Durable Subscription:**
- Default: only get messages while connected
- Durable: messages retained until received or expired

**Request/Reply:**
- Use temporary queues
- `JMSReplyTo` = where to send reply
- `JMSCorrelationID` = links reply to original request

**Transacted Sessions:**
- `createSession(true, 0)`
- `commit()` = make permanent
- `rollback()` = undo everything
- Combines queue + topic operations atomically

**Persistent vs Non-Persistent:**
- Persistent = stored to disk, slower, survives crashes
- Non-persistent = memory only, faster, lost on crash

**Message Selectors:**
- SQL-like syntax: `"priority > 6 AND type = 'alert'"`
- PTP = determines single recipient
- Pub-Sub = acts as filter

---

## 🔑 JMS PROVIDERS

Open source: **Apache ActiveMQ**
Others: SunONE MQ, IBM MQ JMS, WebLogic JMS, JMSCourier

**.NET equivalent:** Microsoft Message Queuing (MSMQ)

---

## 🔑 JMS IN JEE

- Part of JEE since **J2EE 1.3**
- **Message-Driven Bean (MDB)** = specialized EJB for async JMS consumption
- MDB implements `onMessage()` with enterprise features (transactions, security, pooling)

---

## 🔑 CALLBACK vs MESSAGING COMPARISON

| | RMI Callbacks | JMS Messaging |
|--|---------------|---------------|
| Coupling | Tighter (server knows clients) | Looser (via broker) |
| Scalability | Limited | High |
| Reliability | Basic | Guaranteed delivery |
| Filtering | Manual | Message selectors |
| Persistence | No | Yes