# 🛠️ System Design (SDE-1, 1–2 YOE)

A complete beginner-friendly guide to system design for interviews and real-world development.

---

## 1. Monolith vs Microservices

**Interview one-liner:**
Monolith is one big system, Microservices break it into small independent services.

<details>
<summary>Detailed Explanation</summary>

* **Monolith**: Single codebase, everything packaged together (UI, business logic, database).

  * Easy to start, harder to scale.
  * Example: Early-stage startups (like early Flipkart).

* **Microservices**: Break application into small, independent services that communicate via APIs.

  * Independent scaling & deployment.
  * Example: Netflix, Amazon.

**Trade-offs:**

* Monolith → Simpler, but tight coupling.
* Microservices → Flexible, but adds complexity (network calls, service discovery).

</details>

---

## 2. Horizontal vs Vertical Scaling

**Interview one-liner:**
Vertical scaling = bigger machine, Horizontal scaling = more machines.

<details>
<summary>Detailed Explanation</summary>

* **Vertical Scaling**: Increase CPU, RAM on a single server.

  * Example: Upgrading AWS EC2 from t2.small → m5.large.
* **Horizontal Scaling**: Add more servers and distribute load.

  * Example: Adding 10 web servers behind a load balancer.

**Trade-offs:**

* Vertical → Simple but limited.
* Horizontal → Infinite scaling but needs load balancers, distributed systems.

</details>

---

## 3. Stateful vs Stateless Systems

**Interview one-liner:**
Stateful remembers client data, Stateless treats every request independently.

<details>
<summary>Detailed Explanation</summary>

* **Stateful**: Server stores user session (like login info).

  * Example: Traditional banking apps.
* **Stateless**: Each request is independent; client provides all info.

  * Example: REST APIs, JWT-based authentication.

**Trade-offs:**

* Stateful → Easier for sessions but harder to scale.
* Stateless → Easier to scale, harder to manage session persistence.

</details>

---

## 4. Caching

**Interview one-liner:**
Caching stores frequently used data closer to users to reduce latency.

<details>
<summary>Detailed Explanation</summary>

* **Client-side cache**: Browser cache.
* **CDN cache**: Cloudflare/Akamai store content globally.
* **Server-side cache**: Redis/Memcached.

**Trade-offs:**

* Faster response, but needs invalidation strategy.

</details>

---

## 5. Cache Eviction Policies (LRU, LFU)

**Interview one-liner:**
LRU removes least recently used items, LFU removes least frequently used items.

<details>
<summary>Detailed Explanation</summary>

* **LRU (Least Recently Used)**: Remove the item not used recently.
* **LFU (Least Frequently Used)**: Remove the item used least number of times.

**Example:**
Netflix video thumbnails → LRU.
E-commerce popular items → LFU.

</details>

---

## 6. Databases: SQL vs NoSQL

**Interview one-liner:**
SQL = structured & relational, NoSQL = flexible & scalable.

<details>
<summary>Detailed Explanation</summary>

* **SQL**: Tables, rows, fixed schema.

  * Example: MySQL, PostgreSQL.
* **NoSQL**: Key-Value, Document, Column, Graph.

  * Example: MongoDB, DynamoDB, Cassandra.

**Trade-offs:**

* SQL → Consistency, complex queries.
* NoSQL → Flexibility, scalability.

</details>

---

## 7. Indexing (Primary, Secondary)

**Interview one-liner:**
Indexes make data retrieval faster.

<details>
<summary>Detailed Explanation</summary>

* **Primary Index**: Based on primary key.
* **Secondary Index**: Extra lookup.

**Example:**

* Primary: `user_id`
* Secondary: `email`

</details>

---

## 8. Sharding, Replication, Partitioning

**Interview one-liner:**
Sharding = split data, Replication = duplicate data, Partitioning = logical data separation.

<details>
<summary>Detailed Explanation</summary>

* **Sharding**: Splitting across multiple databases.
* **Replication**: Copying data to multiple nodes.
* **Partitioning**: Dividing within same DB.

**Example:**

* Instagram users split by country = sharding.
* 3 DB copies for backup = replication.

</details>

---

## 9. Load Balancers

**Interview one-liner:**
Distributes traffic across servers.

<details>
<summary>Detailed Explanation</summary>

* **Round Robin**: Sequential distribution.
* **Least Connections**: Server with least load.
* **IP Hash**: Same IP goes to same server.

**L4 vs L7**:

* L4: TCP/UDP traffic.
* L7: Application layer (HTTP headers, cookies).

</details>

---

## 10. Message Queues & Event-Driven Systems

**Interview one-liner:**
Message queues decouple producers & consumers.

<details>
<summary>Detailed Explanation</summary>

* **Producer → Queue → Consumer**
* Tools: Kafka, RabbitMQ, AWS SQS.

**Example:**

* Flipkart order service sends event → Inventory service consumes.

</details>

---

## 11. CDN (Content Delivery Network)

**Interview one-liner:**
CDNs bring content closer to users.

<details>
<summary>Detailed Explanation</summary>

* Cloudflare, Akamai store static content globally.
* Reduce latency, improve performance.

**Example:**

* Netflix streaming, YouTube videos.

</details>

---

## 12. Storage Systems (Extra for 2 YOE)

**Interview one-liner:**
Block = raw storage, File = files/folders, Object = blobs.

<details>
<summary>Detailed Explanation</summary>

* **Block Storage**: Like hard disk (AWS EBS).
* **File Storage**: Hierarchical files (AWS EFS).
* **Object Storage**: Unstructured (AWS S3).

**Example:**

* S3 for images, EBS for databases, EFS for shared file system.

</details>

---

# ✅ Interview Safe Phrases

* "It depends on use case."
* "Trade-off between consistency, availability, and performance."
* "For scaling, I’d prefer stateless + horizontal scaling."

---

# 📌 Pro Tips

* Always explain *why* you choose an approach.
* Use real-world apps as examples.
* Keep answers short but expandable if interviewer asks.

---
