# 🧭 System Design Essentials for SDE-1 (1–2 YOE)

A **beginner-friendly, interview-ready** handbook. Each topic starts with a crisp **Interview One-liner**, followed by a collapsible section with explanations, real-world examples, and trade-offs.

> 🎯 **Tip for interviews**: Start with the **one-liner**, then expand **only if interviewer asks**. Shows clarity + depth.

---

## 📚 Table of Contents

- [Core Foundations](#-core-foundations)
- [Core Building Blocks](#-core-building-blocks)
- [Essential Concepts](#-essential-concepts)
- [Scalability & Reliability Patterns](#-scalability--reliability-patterns)
- [Security Basics](#-security-basics)
- [Hands-on System Designs](#-hands-on-system-designs)
- [LLD & Patterns](#-lld--patterns)
- [Interview Gold](#-interview-gold)

---

## 🔰 Core Foundations

### 🧩 What is System Design
**Interview one-liner:**  
“System design is planning the architecture (components + data + interactions) so the product meets **scale, performance, reliability, and cost** goals.”

<details><summary>📖 Expand</summary>
You turn requirements → **architecture blocks**: API gateway, services, DBs, cache, queues, CDN.  
You consider **latency, throughput, consistency, fault tolerance, cost**.

**Example:** Designing a chat app → WebSockets, Kafka for delivery, Cassandra for storage, Redis for online status.
</details>

---

### 🧭 HLD vs LLD
**Interview one-liner:**  
“HLD = big picture architecture; LLD = detailed classes, DB schema, algorithms.”

<details><summary>📖 Expand</summary>
* **HLD:** components, APIs, scaling, DB entity model.  
* **LLD:** classes, methods, schema, error handling.  

**Example (E-commerce):**  
HLD → Orders, Payments, Inventory services.  
LLD → Order class, SQL schema with indexes.
</details>

---

### 🎯 Why companies test System Design
**Interview one-liner:**  
“To test if you can design **scalable, reliable, cost-efficient systems** under constraints.”

<details><summary>📖 Expand</summary>
* Coding = can you implement.  
* Design = can you **scale, recover from failures, and optimize trade-offs**.  
* They check: clarity, structure, trade-offs, real-world awareness.
</details>

---

### 🌍 Real-world examples
**Interview one-liner:**  
“WhatsApp = real-time; Instagram = feed fan-out; Zomato = geo + orders.”

<details><summary>📖 Expand</summary>
- WhatsApp → WebSockets, store-and-forward, encryption.  
- Instagram → Feed caching, fan-out to many users.  
- Zomato → Menu search, order → payment → delivery pipeline.
</details>

---

### 🌐 How the Web Works (DNS, IP, HTTP/HTTPS)
**Interview one-liner:**  
“DNS resolves → IP; client opens TCP/TLS; sends HTTP request; server responds.”

<details><summary>📖 Expand</summary>
Steps:  
1. Browser resolves DNS → IP.  
2. TCP 3-way handshake (TLS if HTTPS).  
3. HTTP request → response.  
4. Browser renders HTML/JS/CSS, fetches assets (often via CDN).
</details>

---

### 🔁 Request/Response Lifecycle
**Interview one-liner:**  
“Browser → DNS → LB → App → DB/Cache → Response → Render.”

<details><summary>📖 Expand</summary>
Each hop adds latency. Use **CDNs, caches, load balancers** to reduce bottlenecks.  
Tracing/metrics → observability.
</details>

---

### 🌉 Networking Basics (TCP vs UDP)
**Interview one-liner:**  
“TCP = reliable & ordered; UDP = fast but no guarantees.”

<details><summary>📖 Expand</summary>
* TCP → APIs, DBs, web traffic.  
* UDP → gaming, video, VoIP.  
* Trade-off: reliability vs latency.
</details>

---

### 🔌 REST APIs & HTTP Methods
**Interview one-liner:**  
“Use nouns for resources + HTTP verbs (GET, POST, PUT/PATCH, DELETE).”

<details><summary>📖 Expand</summary>
* Stateless, versioned (`/v1`), documented (Swagger).  
* Support pagination, filtering, authentication.  
* Always return correct status codes.
</details>

---

### 🧾 HTTP Status Codes
**Interview one-liner:**  
“2xx = success, 3xx = redirect, 4xx = client error, 5xx = server error.”

<details><summary>📖 Expand</summary>
- **200** OK, **201** Created, **204** No Content  
- **301/302** Redirect  
- **400** Bad Request, **401** Unauthorized, **403** Forbidden, **404** Not Found  
- **429** Too Many Requests  
- **500/502/503** Server errors
</details>

---

### 🖥️ OS Basics
**Interview one-liner:**  
“Process = program instance; Thread = lightweight unit; Concurrency ≠ Parallelism.”

<details><summary>📖 Expand</summary>
* **Process vs Thread:** isolation vs shared memory.  
* **Concurrency:** interleaving tasks. **Parallelism:** simultaneous on multi-core.  
* **Blocking I/O:** thread waits. **Non-blocking:** async (Node.js, NIO).
</details>

---

## 🧱 Core Building Blocks

### 🧱 Monolith vs Microservices
**Interview one-liner:**  
“Monolith = single deploy; Microservices = independent small services.”

<details><summary>📖 Expand</summary>
* Monolith → easier start, harder scale.  
* Microservices → independent deploy, but adds API calls, tracing, contracts.  
* Instagram started monolithic → migrated.
</details>

---

### 📈 Horizontal vs Vertical Scaling
**Interview one-liner:**  
“Vertical = bigger box; Horizontal = more boxes behind LB.”

<details><summary>📖 Expand</summary>
* Vertical has limits & single failure point.  
* Horizontal needs **statelessness** + data partitioning, but enables elasticity.
</details>

---

### 🧠 Stateful vs Stateless
**Interview one-liner:**  
“Stateless scales easily; Stateful needs stickiness or shared store.”

<details><summary>📖 Expand</summary>
* Stateless APIs = token-based auth → any node can serve.  
* Stateful = chat sessions, WebSockets → use Redis/DB to share.
</details>

---

### ⚡ Caching (Client, CDN, Server)
**Interview one-liner:**  
“Cache hot data near users to cut latency & DB load.”

<details><summary>📖 Expand</summary>
- **Client:** browser cache, service worker.  
- **CDN:** edge servers for static/video.  
- **Server:** Redis, Memcached.  

Invalidation = hardest problem → TTL, write-through, cache-aside.
</details>

---

### 🧮 Cache Eviction
**Interview one-liner:**  
“LRU = evict least recently used; LFU = least frequently used.”

<details><summary>📖 Expand</summary>
LRU suits feeds; LFU suits hot items (top sellers).
</details>

---

### 🗃️ Databases
**Interview one-liner:**  
“SQL = structured + ACID; NoSQL = flexible + scale.”

<details><summary>📖 Expand</summary>
- SQL: Postgres/MySQL → joins, strict schema.  
- NoSQL: Mongo (document), Cassandra (column), Redis (KV).  
Pick based on **access patterns** & scale.
</details>

---

### 🔎 Indexing
**Interview one-liner:**  
“Indexes speed up reads but slow down writes.”

<details><summary>📖 Expand</summary>
* **Primary** = PK index.  
* **Secondary** = filters (email, date).  
Trade-off: faster reads, more space + write cost.
</details>

---

### 🧩 Sharding, Replication, Partitioning
**Interview one-liner:**  
“Shard = split data; Replication = copies; Partition = logical split.”

<details><summary>📖 Expand</summary>
* Sharding = user-id ranges/hashes.  
* Replication = HA + read scaling.  
* Partitioning = vertical/horizontal separation.
</details>

---

### ⚖️ Load Balancers
**Interview one-liner:**  
“LB distributes traffic (Round Robin, Least Conn); L4 = transport, L7 = app-aware.”

<details><summary>📖 Expand</summary>
- L4 = TCP, fast.  
- L7 = can route by URL, cookies, headers.  
- Algorithms: Round Robin, Weighted, IP Hash.
</details>

---

### 📨 Message Queues
**Interview one-liner:**  
“Queues decouple producers/consumers; enable async & spike smoothing.”

<details><summary>📖 Expand</summary>
- Kafka = partitioned log.  
- RabbitMQ = routing.  
- SQS = managed.  
Patterns: producer → queue → consumers; DLQ for failures.
</details>

---

### 🌎 CDN
**Interview one-liner:**  
“CDNs cache static assets at edge for speed + less origin load.”

<details><summary>📖 Expand</summary>
- Cloudflare, Akamai.  
- Helps with DDoS, TLS termination.
</details>

---

### 💾 Storage
**Interview one-liner:**  
“Block = disk (EBS), File = shared FS (EFS), Object = blobs (S3).”

<details><summary>📖 Expand</summary>
- Block → DB volumes.  
- File → POSIX sharing.  
- Object → scale + lifecycle (backups, media).
</details>

---

## 🧠 Essential Concepts

### 🚀 Scalability, Latency, Throughput
**Interview one-liner:**  
“Scalability = ability to handle growth; Latency = delay; Throughput = ops/sec.”

---

### 🔺 CAP Theorem
**Interview one-liner:**  
“During network partitions → must trade consistency vs availability.”

---

### 🔗 Consistency Models
**Interview one-liner:**  
“Strong = always fresh; Eventual = may lag; Causal = preserves order.”

---

### 🧾 Transactions & ACID
**Interview one-liner:**  
“ACID = Atomic, Consistent, Isolated, Durable.”

---

### 🚦 Rate Limiting
**Interview one-liner:**  
“Token bucket allows bursts; Leaky bucket smooths; return 429.”

---

### 🧩 API Design
**Interview one-liner:**  
“REST = nouns + verbs, versioning, pagination, auth.”

---

### 📜 Pagination
**Interview one-liner:**  
“Offset is simple but slow; Cursor is fast for large data.”

---

## 🛡️ Scalability & Reliability Patterns

### 🧯 Fault Tolerance
**Interview one-liner:**  
“Assume failures → add retries, redundancy, graceful degrade.”

---

### 🔁 Redundancy & Failover
**Interview one-liner:**  
“Active-Passive = standby; Active-Active = all live.”

---

### 📈 Auto-scaling
**Interview one-liner:**  
“Scale up/down automatically based on load.”

---

### 🧰 Circuit Breaker & Retry/Backoff
**Interview one-liner:**  
“Fail fast if dependency is unhealthy; retry with exponential backoff + jitter.”

---

### 🔄 Idempotency
**Interview one-liner:**  
“Operation gives same result if repeated (e.g., payments).”

---

### 🔒 Distributed Locks
**Interview one-liner:**  
“Locks across nodes (e.g., Redis RedLock) avoid double processing.”

---

### ⚡ (Extra) Sagas, CQRS
**Interview one-liner:**  
“Sagas = distributed transactions via compensating steps; CQRS = separate reads/writes.”

---

## 🔒 Security Basics

### 🔑 HTTPS/TLS
**Interview one-liner:**  
“Encrypt traffic with TLS to prevent snooping & tampering.”

---

### 👥 AuthN vs AuthZ
**Interview one-liner:**  
“AuthN = who you are; AuthZ = what you can do.”

---

### 🔐 OAuth2, JWT
**Interview one-liner:**  
“OAuth2 = delegate access; JWT = stateless signed tokens.”

---

### 🌐 CORS
**Interview one-liner:**  
“CORS controls cross-origin resource sharing in browsers.”

---

### 🚦 API Throttling
**Interview one-liner:**  
“Protect services by capping API calls/user.”

---

## 🛠️ Hands-on Designs

### 🔗 URL Shortener
**Teaches:** hashing, DB choice, caching.

---

### 💬 Chat App
**Teaches:** WebSockets, queues, delivery guarantees.

---

### 🛒 E-commerce
**Teaches:** search, payments, order pipeline.

---

### 📱 Social Feed
**Teaches:** fan-out, ranking, caching.

---

### 🎥 Video Streaming
**Teaches:** CDN, storage, chunking.

---

### 🚗 Ride Sharing (extra)
**Teaches:** geo indexing, dispatch, surge pricing.

---

## 🧩 LLD & Patterns

### 🗺️ UML & LLD Drills
Parking Lot, BookMyShow, ATM.

---

### 🏗️ Patterns
Singleton, Factory, Strategy, Observer, Builder, Proxy.

---

## 🎤 Interview Gold

- ✅ Always start with **clarifying requirements**.  
- ✅ Draw **high-level diagram** (clients, LB, APIs, DB, cache, queue).  
- ✅ State trade-offs: “This improves X but costs Y.”  
- ✅ Handle **failures** explicitly.  
- ✅ Use safe phrases:  
  - “We can scale horizontally if traffic grows.”  
  - “We need to trade consistency for availability.”  
  - “A cache helps reduce latency but adds invalidation complexity.”  

---
