# 📘 System Design Essentials for SDE‑1 (1–2 YOE)

> **How to use this file:** Each topic has a short **Interview one‑liner** and a collapsible section with **easy explanation, internals, real‑world examples, trade‑offs, and pitfalls**. Open the dropdowns as you revise. Keep answers structured: **Definition → Why → How → Example → Trade‑offs**.

---

## Table of Contents
- [1. Core Foundations](#1-core-foundations)
  - System Design — What & Why
  - HLD vs LLD
  - How the Web Works (DNS → TCP/TLS → HTTP)
  - Networking Basics (TCP vs UDP)
  - REST APIs & HTTP Methods
  - HTTP Status Codes
  - OS Basics (Process vs Thread, Concurrency vs Parallelism, Blocking vs Non‑blocking I/O)
- [2. Core Building Blocks](#2-core-building-blocks)
  - Monolith vs Microservices
  - Horizontal vs Vertical Scaling
  - Stateful vs Stateless Systems
  - Caching (Client, CDN, Server)
  - Cache Eviction (LRU, LFU, TTL)
  - Databases (SQL vs NoSQL)
  - Indexing (Primary, Secondary)
  - Sharding, Replication, Partitioning
  - Load Balancing (Round‑Robin, Least‑Connections, IP‑Hash; L4 vs L7)
  - Message Queues & Event‑Driven (Kafka, RabbitMQ, SQS; Producer/Consumer)
  - CDN (Cloudflare, Akamai)
  - Storage Systems (Block, File, Object)
- [3. Essential System Design Concepts](#3-essential-system-design-concepts)
  - Scalability, Latency, Throughput
  - CAP Theorem
  - Consistency Models (Strong, Eventual, Causal)
  - ACID Transactions
  - Rate Limiting (Token/Leaky Bucket)
  - API Design Principles (REST, versioning, pagination)
  - API Pagination (Offset vs Cursor)
- [4. Scalability & Reliability Patterns](#4-scalability--reliability-patterns)
  - Fault Tolerance
  - Redundancy & Failover (Active‑Passive, Active‑Active)
  - Auto‑Scaling
  - Circuit Breaker, Retry/Backoff
  - Idempotency
  - Distributed Locks
- [5. Security Basics](#5-security-basics)
  - HTTPS/TLS
  - Authentication vs Authorization
  - OAuth2 & JWT
  - CORS
  - API Throttling
- [6. Hands‑On Design Scenarios](#6-hands-on-design-scenarios)
  - URL Shortener
  - Chat App
  - E‑commerce
  - Social Feed
  - Video Streaming
  - Ride Sharing (2 YOE+)
  - Food Delivery (2 YOE+)
  - Standalone Rate Limiter
- [7. LLD & Patterns](#7-lld--patterns)
  - UML basics
  - Practice problems (Parking Lot, BookMyShow, ATM)
  - Design Patterns (Singleton, Factory, Strategy, Observer, Builder, Proxy)
- [8. Observability & DevOps Awareness (minimal)](#8-observability--devops-awareness-minimal)

---

## 1. Core Foundations

### System Design — What & Why
**Interview one‑liner:** Designing the **architecture and components** of a system to meet requirements for **scale, performance, reliability, and cost**.

<details>
<summary>Open for easy explanation, internals, examples, trade‑offs</summary>

**Easy explanation:** It’s the blueprint: break the product into services, data stores, caches, queues, and define how they talk.

**How it works:** Gather requirements → define APIs & data flows → choose storage, caching, consistency, and failure handling → estimate capacity.

**Real‑world:** WhatsApp (mass messaging), Instagram (media feed at scale), Zomato (search + orders + delivery).

**When/Why:** Interviews test your ability to reason about trade‑offs and growth; on job, it avoids costly redesigns.

**Pitfalls:** Jumping to tech names before requirements; ignoring constraints (latency, throughput, SLA, cost).
</details>

### HLD vs LLD
**Interview one‑liner:** **HLD** = big blocks and interactions; **LLD** = internal class/model logic of each block.

<details>
<summary>Details</summary>
**HLD:** services, DB choices, APIs, scaling, failure modes.  
**LLD:** data models, classes, method contracts, DB schema.

**Example:** Chat app HLD (Gateway, Messaging Service, Store). LLD (Message entity, repository, idempotency key).

**Tip:** Start with HLD on whiteboard, then drill one or two blocks to LLD depth if asked.
</details>

### How the Web Works (DNS → TCP/TLS → HTTP)
**Interview one‑liner:** Browser resolves **domain → IP (DNS)**, opens **TCP/TLS**, sends **HTTP** request, gets response.

<details>
<summary>Details</summary>
**Flow:** URL typed → DNS lookup → get server IP → TCP 3‑way handshake → (HTTPS: TLS handshake) → HTTP GET/POST → server builds response → browser renders.

**Why it matters:** Knowing the path helps you place caches, CDNs, and diagnose latency.
</details>

### Networking Basics: TCP vs UDP
**Interview one‑liner:** **TCP** reliable, ordered; **UDP** fast, no guarantees.

<details>
<summary>Details</summary>
**Use TCP:** web, DB, emails. **Use UDP:** streaming, gaming, voice (where delay beats perfect delivery).

**Internals:** TCP handshake, retransmission, flow/ congestion control. UDP = fire‑and‑forget datagrams.
</details>

### REST APIs & HTTP Methods
**Interview one‑liner:** **Noun‑based endpoints**, use HTTP verbs: **GET** read, **POST** create, **PUT/PATCH** update, **DELETE** remove.

<details>
<summary>Details</summary>
**Principles:** stateless, proper status codes, auth, pagination, rate limits, versioning (`/v1`).  
**Example:** `GET /users/42`, `POST /orders`, `PATCH /users/42`.
</details>

### HTTP Status Codes
**Interview one‑liner:** 2xx success, 3xx redirect, 4xx client error, 5xx server error.

<details>
<summary>Details</summary>
**Know these:** 200 OK, 201 Created, 204 No Content, 301/302 Redirect, 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 409 Conflict, 422 Unprocessable, 429 Too Many Requests, 500 Internal Error, 502/503/504 Upstream/Overload/Timeout.
</details>

### OS Basics
**Interview one‑liner:** **Process** = program with its own memory; **Thread** = lightweight execution unit sharing process memory.

<details>
<summary>Details</summary>
**Concurrency vs Parallelism:** Interleaving vs truly simultaneous on multiple cores.  
**Blocking vs Non‑blocking I/O:** Thread waits vs continues and gets callback/poll later.  
**Why it matters:** Determines server model (thread‑per‑request vs async/reactor) and capacity.
</details>

---

## 2. Core Building Blocks

### Monolith vs Microservices
**Interview one‑liner:** Start simple (monolith); split into microservices when **scale, team size, or deployment velocity** demands.

<details>
<summary>Details</summary>
**Monolith pros:** Simple dev/deploy, easy transactions, less ops. **Cons:** Slower deploys at scale, tight coupling.  
**Microservices pros:** Independent scaling/deploys, fault isolation, tech heterogeneity. **Cons:** Network complexity, distributed data, observability needed.  
**Migration tip:** Strangle pattern—extract one bounded context at a time.
</details>

### Horizontal vs Vertical Scaling
**Interview one‑liner:** **Vertical** = bigger box; **Horizontal** = more boxes behind a load balancer.

<details>
<summary>Details</summary>
Vertical quick but capped; horizontal elastic, HA friendly. Use autoscaling + stateless services for horizontal.
</details>

### Stateful vs Stateless Systems
**Interview one‑liner:** Stateless scales easier; stateful needs sticky sessions or shared state.

<details>
<summary>Details</summary>
Keep app stateless; keep state in managed stores (DB, cache). If session needed, use JWT or shared session store (Redis). Avoid node‑local sessions.
</details>

### Caching (Client, CDN, Server)
**Interview one‑liner:** Put hot data closer to users to cut latency and DB load.

<details>
<summary>Details</summary>
**Client:** browser cache headers. **CDN:** static assets, media. **Server:** Redis/Memcached for DB results, computed views.  
**Patterns:** read‑through, write‑through, write‑back, cache‑aside. **Keys:** TTLs, invalidation on writes.
</details>

### Cache Eviction (LRU, LFU, TTL)
**Interview one‑liner:** When full, evict **Least‑Recently‑Used** or **Least‑Frequently‑Used**; always set sane **TTLs**.

<details>
<summary>Details</summary>
**LRU:** great for temporal locality (feeds). **LFU:** stable hotkeys (popular products). Combine with TTL to prevent staleness.
</details>

### Databases: SQL vs NoSQL
**Interview one‑liner:** **SQL** for transactions and relations; **NoSQL** for flexible schema and scale.

<details>
<summary>Details</summary>
**SQL (MySQL/Postgres):** joins, ACID, strong consistency.  
**NoSQL:** key‑value (Redis), document (MongoDB), wide‑column (Cassandra), graph (Neo4j). Choose by access patterns.
</details>

### Indexing (Primary, Secondary)
**Interview one‑liner:** Index = fast lookup structure; speeds reads, slows writes a bit.

<details>
<summary>Details</summary>
**Primary:** unique id lookup. **Secondary:** by email/date/status. Use covering indexes, watch write amplification.
</details>

### Sharding, Replication, Partitioning
**Interview one‑liner:** **Replication** for availability; **Sharding** for scale; **Partitioning** is the general split.

<details>
<summary>Details</summary>
**Replication:** leader/follower, read replicas, failover.  
**Sharding:** range, hash, geo; needs routing (consistent hashing).  
**Partitioning:** by rows (horizontal) or columns (vertical). Keep hot shards small; rebalance proactively.
</details>

### Load Balancing (algorithms & layers)
**Interview one‑liner:** Distribute requests using **Round‑Robin/Least‑Connections/IP‑Hash** at **L4 (fast)** or **L7 (smart)**.

<details>
<summary>Details</summary>
**L4:** routes by IP/port; protocol‑agnostic. **L7:** routes by URL/cookies/headers (A/B, canary). Health checks, timeouts, retries are essential.
</details>

### Message Queues & Event‑Driven
**Interview one‑liner:** Use queues (Kafka/RabbitMQ/SQS) to **decouple**, absorb spikes, and process **async**.

<details>
<summary>Details</summary>
**Patterns:** producer → topic/queue → consumer(s); fan‑out; dead‑letter queues.  
**Kafka:** high throughput, ordered partitions, retention. **RabbitMQ:** routing patterns, ack/nack. **SQS:** managed, simple.
</details>

### CDN (Cloudflare, Akamai)
**Interview one‑liner:** Edge cache for static (and some dynamic) content to cut latency worldwide.

<details>
<summary>Details</summary>
Use signed URLs, cache‑control headers, origin shield. Put images/video on object storage + CDN (e.g., S3 + CloudFront/Cloudflare).
</details>

### Storage Systems (Block, File, Object)
**Interview one‑liner:** **Block** = disks for DB; **File** = shared filesystem; **Object** = blobs at massive scale.

<details>
<summary>Details</summary>
**Block (EBS):** low‑latency, mount to one host. **File (EFS/NFS):** POSIX, multi‑attach. **Object (S3):** eventual consistency, versioning, lifecycle policies.
</details>

---

## 3. Essential System Design Concepts

### Scalability, Latency, Throughput
**Interview one‑liner:** Scale = handle more load; Latency = time per request; Throughput = requests per second.

<details>
<summary>Details</summary>
Optimize latency with caches, CDNs, locality; throughput with horizontal scale, batching, async. Measure P50/P90/P99.
</details>

### CAP Theorem
**Interview one‑liner:** In a partition, you can choose **Consistency or Availability**, not both.

<details>
<summary>Details</summary>
Most real systems are **AP (eventual)** or **CP (consistent)** depending on domain: feeds vs finance.
</details>

### Consistency Models (Strong, Eventual, Causal)
**Interview one‑liner:** Strong = latest always; Eventual = converges; Causal = respects cause‑before‑effect.

<details>
<summary>Details</summary>
Pick based on UX: likes can be eventual; balances should be strong; social graphs often causal.
</details>

### ACID Transactions
**Interview one‑liner:** **Atomic, Consistent, Isolated, Durable**—reliable multi‑step DB changes.

<details>
<summary>Details</summary>
Isolation levels (Read Committed, Repeatable Read, Serializable). Use transactions for payments, inventory.
</details>

### Rate Limiting (Token/Leaky Bucket)
**Interview one‑liner:** Control request rate per user/IP to protect systems.

<details>
<summary>Details</summary>
**Token bucket:** allows bursts; **Leaky bucket:** smooths. Return **429** on exceed; implement at gateway with Redis counters.
</details>

### API Design Principles (REST, versioning, pagination)
**Interview one‑liner:** Clean nouns, proper verbs/codes, **/v1** versioning, **pagination** for lists.

<details>
<summary>Details</summary>
**Pagination:** limit & offset (simple) vs cursor/keyset (stable at scale). Include `next_cursor`.
</details>

### API Pagination (Offset vs Cursor)
**Interview one‑liner:** Offset is easy but slow for deep pages; Cursor is fast and consistent under writes.

<details>
<summary>Details</summary>
Use cursor for feeds/logs; offset for admin tools and small datasets.
</details>

---

## 4. Scalability & Reliability Patterns

### Fault Tolerance
**Interview one‑liner:** Design to **keep working** when parts fail.

<details>
<summary>Details</summary>
Redundancy, health checks, timeouts, retries, graceful degradation (serve cached data if DB down).
</details>

### Redundancy & Failover (Active‑Passive, Active‑Active)
**Interview one‑liner:** Keep **spares**; switch on failure (passive) or share load (active‑active).

<details>
<summary>Details</summary>
Active‑passive simpler (promotion time). Active‑active needs conflict resolution (multi‑primary DBs).
</details>

### Auto‑Scaling
**Interview one‑liner:** Scale instance count automatically by metrics (CPU/RPS/lag).

<details>
<summary>Details</summary>
Warm‑up, min/max bounds, scale‑in protection, predictive vs reactive policies.
</details>

### Circuit Breaker, Retry/Backoff
**Interview one‑liner:** Stop hammering a failing dependency; retry carefully with **exponential backoff + jitter**.

<details>
<summary>Details</summary>
States: closed → open (on error threshold) → half‑open (probe). Combine with timeouts and bulkheads.
</details>

### Idempotency
**Interview one‑liner:** Same request repeated ⇒ same effect. Critical for retries (e.g., payments).

<details>
<summary>Details</summary>
Use idempotency keys for POST; PUT is naturally idempotent; design DB constraints to enforce once‑only actions.
</details>

### Distributed Locks
**Interview one‑liner:** Ensure only one worker performs a critical action at a time.

<details>
<summary>Details</summary>
Use Redis (SET NX PX) or Zookeeper/Consul; add expirations; consider fencing tokens to avoid split‑brain.
</details>

---

## 5. Security Basics

### HTTPS/TLS
**Interview one‑liner:** Encrypt traffic to prevent snooping/tampering.

<details>
<summary>Details</summary>
Certificates, TLS handshake, HSTS, perfect forward secrecy. Always HTTPS for auth and APIs.
</details>

### Authentication vs Authorization
**Interview one‑liner:** **AuthN** = who you are; **AuthZ** = what you can do.

<details>
<summary>Details</summary>
Separate concerns; principle of least privilege; role‑/attribute‑based access control.
</details>

### OAuth2 & JWT
**Interview one‑liner:** OAuth2 issues access tokens; **JWT** is a signed token carrying claims.

<details>
<summary>Details</summary>
Store short‑lived access tokens, refresh tokens; verify signatures; rotate keys; avoid putting secrets in JWT payload.
</details>

### CORS
**Interview one‑liner:** Browser policy that restricts cross‑origin requests unless the server allows them.

<details>
<summary>Details</summary>
Set `Access-Control-Allow-Origin` precisely; preflight (OPTIONS) for non‑simple requests.
</details>

### API Throttling
**Interview one‑liner:** Enforce per‑key/IP limits; return **429**; protect downstreams.

<details>
<summary>Details</summary>
Implement at API gateway or edge; differentiate hard vs soft limits; expose headers for remaining quota.
</details>

---

## 6. Hands‑On Design Scenarios

### URL Shortener
**Interview one‑liner:** Map short IDs → long URLs; super read‑heavy.

<details>
<summary>Details</summary>
**Core:** API, key generator (base62, snowflake), DB (NoSQL), cache hot keys, 301 redirects, rate limits, abuse detection.  
**Scale:** Pre‑generate IDs, sharded storage; analytics as async pipeline.
</details>

### Chat App
**Interview one‑liner:** Real‑time messaging with delivery guarantees and offline support.

<details>
<summary>Details</summary>
WebSockets, message service, store‑and‑forward, read receipts, presence, partitions by user/shard. Use MQ for fan‑out; long‑term storage in wide‑column store.
</details>

### E‑commerce
**Interview one‑liner:** Catalog, cart, checkout, payment, inventory, search.

<details>
<summary>Details</summary>
Microservices per domain; cache product pages; search index; order pipeline via events; Saga/compensation for cross‑service consistency; anti‑fraud; idempotent checkout.
</details>

### Social Feed
**Interview one‑liner:** Generate personalized timelines efficiently.

<details>
<summary>Details</summary>
Push vs pull vs hybrid fan‑out; cache recent feeds; ranker service; write amplification vs read amplification trade‑off.
</details>

### Video Streaming
**Interview one‑liner:** Store/encode/serve video via CDN with adaptive bitrate.

<details>
<summary>Details</summary>
Upload → transcode (queue, workers) → object storage → CDN (HLS/DASH segments). Metadata service; previews/thumbnails cached.
</details>

### Ride Sharing (2 YOE+)
**Interview one‑liner:** Match riders/drivers with geo‑spatial search at low latency.

<details>
<summary>Details</summary>
Geohash indices, proximity queries, real‑time location streams, surge pricing, city sharding, eventual consistency for ETAs.
</details>

### Food Delivery (2 YOE+)
**Interview one‑liner:** Orders across restaurants with courier assignment and live tracking.

<details>
<summary>Details</summary>
Order topic events, restaurant confirmations, courier matching, live GPS via websockets, SLA alerts, delivery slotting.
</details>

### Standalone Rate Limiter
**Interview one‑liner:** Centralized limiter using Redis counters/tokens.

<details>
<summary>Details</summary>
Key = `{api_key}:{window}`; atomic INCR/EXPIRE; return 429 on exceed; shard via consistent hashing; expose retry‑after.
</details>

---

## 7. LLD & Patterns

### UML Basics
**Interview one‑liner:** Use class, sequence, and component diagrams to communicate design.

<details>
<summary>Details</summary>
Class relationships (is‑a/has‑a), lifelines in sequence diagrams, interfaces; keep diagrams minimal and readable.
</details>

### Practice LLD Problems
**Interview one‑liner:** Practice a few classic domains to show modeling skills.

<details>
<summary>Details</summary>
**Parking Lot:** slots, vehicles, pricing, tickets.  
**BookMyShow:** shows, seats, bookings, payments, concurrency on seat selection.  
**ATM:** accounts, transactions, limits, error flows.
</details>

### Design Patterns
**Interview one‑liner:** Reusable solutions to recurring design problems.

<details>
<summary>Details</summary>
**Singleton:** one instance (config/logger).  
**Factory:** create related objects without `new`.  
**Strategy:** swap algorithms at runtime (payment methods).  
**Observer:** event notifications (webhooks).  
**Builder:** assemble complex objects step‑by‑step (HTTP request).  
**Proxy:** stand‑in to control access (caching proxy, remote proxy).
</details>

---

## 8. Observability & DevOps Awareness (minimal)

> Only where relevant to system design; full DevOps guide is separate.

<details>
<summary>What to know</summary>
**Logs/Metrics/Tracing:** Correlate requests across services (trace IDs).  
**Dashboards/Alerts:** SLOs, error rates, latency percentiles.  
**Load Testing:** JMeter/Locust to validate capacity.  
**Containers:** Docker images; basic k8s primitives (Pod, Deployment, Service).  
**CI/CD:** Rollouts, canary/blue‑green; config as code.
</details>

---

## Final Cheat‑Sheet (say it like this)
- **Start with requirements** (users, RPS, latency, data volume, SLAs).  
- **Sketch HLD** (clients, gateways, services, DBs, caches, queues, CDN, LB).  
- **Call out trade‑offs** (SQL vs NoSQL, consistency vs availability, cost vs latency).  
- **Plan for failures** (timeouts, retries, circuit breakers, fallbacks).  
- **Plan scale** (stateless services + horizontal scale + autoscaling).  
- **Security first** (HTTPS, auth, authZ, rate limits).  
- **Measure** (logs/metrics/traces; P99 latency).  
- **Close with evolution** (MVP today, how to scale next: shard, cache, async).
