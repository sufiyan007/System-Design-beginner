# 📘 System Design Notes for SDE-1 (1–2 YOE)

This guide is designed for developers with **1–2 years of experience** preparing for **system design interviews**. It contains **short interview-safe definitions**, **collapsible detailed explanations**, **real-world examples**, and **trade-offs** where relevant.

---

## 1. Core Foundations

### What is System Design?
**Definition:** The process of defining the architecture, components, and interactions of a software system to meet specific requirements.

<details>
<summary>Detailed Explanation</summary>
System design is about breaking down a problem into smaller components (databases, APIs, caching, scaling) and deciding how they work together. It covers both **High-Level Design (HLD)** and **Low-Level Design (LLD)**.
</details>

**Example:** Designing Instagram → User service, Media storage, Feed generation, Notifications.

---

### Monolith vs Microservices
**Definition:** Monolith = one big codebase; Microservices = multiple independent services.

<details>
<summary>Detailed Explanation</summary>
- **Monolith:** Easier to start, everything in one codebase. Harder to scale with growth.
- **Microservices:** Each service handles a specific function. Allows independent scaling, deployments, but adds complexity (network calls, monitoring).
</details>

**Example:** 
- Monolith: Early-stage startups with single deployable app.
- Microservices: Netflix, Amazon.

**Trade-off:** Start simple with monolith → migrate to microservices when scale demands.

---

### Horizontal vs Vertical Scaling
**Definition:** Vertical = add more power to one machine; Horizontal = add more machines.

<details>
<summary>Detailed Explanation</summary>
- **Vertical Scaling:** Increase CPU/RAM. Limited growth, downtime required.
- **Horizontal Scaling:** Add more servers, distribute load. Needs load balancers.
</details>

**Example:** E-commerce website on Black Friday adds more servers → horizontal scaling.

**Trade-off:** Vertical is quick but limited; horizontal is scalable but complex.

---

### Stateful vs Stateless Systems
**Definition:** Stateful = server remembers user session; Stateless = every request is independent.

<details>
<summary>Detailed Explanation</summary>
- **Stateful:** Requires server memory of client state (sessions). Hard to scale.
- **Stateless:** No memory of past requests. Easier scaling, common in REST APIs.
</details>

**Example:**
- Stateful: Online banking session.
- Stateless: Fetching stock prices via API.

---

## 2. Caching

### Caching Basics
**Definition:** Temporary storage to serve repeated requests faster.

<details>
<summary>Detailed Explanation</summary>
Caches reduce database load and improve latency. Can exist at **client-side, CDN, or server-side**.
</details>

**Example:** Browser stores images, Cloudflare caches static assets, Redis caches DB queries.

---

### Cache Eviction Policies
**Definition:** Rules for removing old cache data when storage is full.

<details>
<summary>Detailed Explanation</summary>
- **LRU (Least Recently Used):** Removes least recently accessed.
- **LFU (Least Frequently Used):** Removes least frequently accessed.
- **FIFO:** Removes oldest inserted.
</details>

**Example:** Redis supports LRU eviction.

---

## 3. Databases

### SQL vs NoSQL
**Definition:** SQL = structured relational DB; NoSQL = non-relational, flexible.

<details>
<summary>Detailed Explanation</summary>
- **SQL:** Tables, rows, schema enforced, strong consistency. (MySQL, PostgreSQL)
- **NoSQL:** Key-value, document, column, graph. Flexible, high scalability. (MongoDB, DynamoDB)
</details>

**Example:**
- SQL: Banking transactions.
- NoSQL: Instagram feed.

**Trade-off:** SQL for ACID compliance, NoSQL for scalability.

---

### Indexing
**Definition:** Data structure that improves query speed at cost of extra storage.

<details>
<summary>Detailed Explanation</summary>
- **Primary Index:** Based on primary key.
- **Secondary Index:** Additional searchable fields.
</details>

**Example:** Search by `user_id` → primary index. Search by `email` → secondary index.

---

### Sharding, Replication, Partitioning
**Definition:** Techniques for scaling databases.

<details>
<summary>Detailed Explanation</summary>
- **Replication:** Copy of DB on multiple servers (high availability).
- **Sharding:** Split DB horizontally (user 1–1000 on shard 1, etc.).
- **Partitioning:** Splitting DB logically.
</details>

**Example:** Twitter user data sharded by user ID.

---

## 4. Load Balancers

### Basics
**Definition:** Distribute traffic across servers to prevent overload.

<details>
<summary>Detailed Explanation</summary>
- **Algorithms:** Round Robin, Least Connections, IP Hash.
- **Types:** L4 (transport layer), L7 (application layer).
</details>

**Example:** AWS Elastic Load Balancer.

---

## 5. Message Queues & Event-Driven Systems

### Producer-Consumer Pattern
**Definition:** Producer sends messages → Queue → Consumer processes them.

<details>
<summary>Detailed Explanation</summary>
Helps decouple services, ensures reliability, and handles spikes.
</details>

**Example:** Order service (producer) → Kafka queue → Payment service (consumer).

---

### Kafka, RabbitMQ, AWS SQS
**Definition:** Tools for asynchronous message processing.

<details>
<summary>Detailed Explanation</summary>
- **Kafka:** Distributed streaming platform.
- **RabbitMQ:** Traditional message broker.
- **AWS SQS:** Managed message queue.
</details>

**Example:** Netflix uses Kafka for event streaming.

---

## 6. CDN (Content Delivery Network)

### Basics
**Definition:** Globally distributed servers that cache and deliver content closer to users.

<details>
<summary>Detailed Explanation</summary>
Reduces latency by serving static assets (images, CSS, JS) from nearest edge server.
</details>

**Example:** Cloudflare, Akamai.

---

## 7. Storage Systems (extra for 2 YOE)

### Block, File, Object Storage
**Definition:** Different storage abstractions.

<details>
<summary>Detailed Explanation</summary>
- **Block Storage (EBS):** Raw volumes attached to servers.
- **File Storage (EFS):** File system accessible by multiple servers.
- **Object Storage (S3):** Stores data as objects with metadata.
</details>

**Example:**
- Block: Database disk.
- File: Shared team documents.
- Object: User images on Instagram.

---

# ✅ Interview Tips
- Always **define first in 1 line** → then expand if asked.
- Use **real-world examples** (Instagram, Netflix, Amazon).
- Always mention **trade-offs**.
- Keep answers structured: Definition → Example → Trade-off.
