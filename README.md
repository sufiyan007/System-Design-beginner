# 🛠️ System Design Essentials (SDE‑1, 1–2 YOE)

A clean, beginner‑friendly, and interview‑oriented guide in one place.

---

## 📌 Core Foundations

### What is System Design?

> "System Design is how we plan and organize the components of a software system so that it is scalable, reliable, and maintainable."

* Think of it like **blueprinting a building before construction**.
* Used in **interviews** to test real-world problem solving.

**Interview one-liner:** System design is the art of breaking down a big system into smaller, efficient, and reliable components.

<details>
<summary>Real-world examples</summary>

* **WhatsApp** → Messaging system, delivery guarantees, scaling to millions.
* **Instagram** → Feed generation, caching, media storage (CDN).
* **Zomato/Swiggy** → Search, recommendations, real-time tracking.

</details>

---

## 🌍 How the Web Works

* **DNS** → Converts domain name → IP.
* **IP Address** → Identifier of machine.
* **HTTP/HTTPS** → Protocol to transfer data.
* **Request/Response lifecycle** → Browser → DNS → Server → Response → Render.

**Interview one-liner:** DNS is the internet’s phonebook mapping names to IP addresses.

---

## 🔌 Networking Basics

* **TCP** → Reliable, ordered, connection-based.
* **UDP** → Faster, but no guarantee (used in gaming/streaming).

**Interview one-liner:** TCP = reliability, UDP = speed.

---

## 🌐 REST APIs

* **HTTP methods:** GET, POST, PUT, DELETE.
* **Status codes:** 200 OK, 404 Not Found, 500 Internal Error.
* **Stateless communication** → Server does not store client session.

**Real-world example:**

* Zomato: `GET /restaurants?location=blr`
* Instagram: `POST /upload` for images.

---

## ⚙️ OS Basics

* **Process vs Thread**

  * Process = independent execution unit.
  * Thread = lightweight execution inside process.

* **Concurrency vs Parallelism**

  * Concurrency = handling multiple tasks (context switching).
  * Parallelism = executing simultaneously on multiple cores.

**Interview one-liner:** Threads share memory, processes don’t.

---

## 🏗️ Architecture Patterns

### Monolith vs Microservices

* **Monolith** = All code in one place (simple, but hard to scale).
* **Microservices** = Independent services (scalable, but complex).

**Trade-off:** Monolith for startups, Microservices for scale.

### Horizontal vs Vertical Scaling

* **Vertical scaling** = bigger machine (limited).
* **Horizontal scaling** = more machines (preferred for distributed systems).

### Stateful vs Stateless Systems

* **Stateful** = Server remembers client session.
* **Stateless** = Every request independent.

**Interview one-liner:** Stateless scales better.

---

## ⚡ Caching

* **Client-side cache** → Browser stores data.
* **CDN** → Edge servers store static content.
* **Server-side cache** → Redis, Memcached.

### Cache Eviction Policies

* LRU (Least Recently Used)
* LFU (Least Frequently Used)

**Interview one-liner:** Caching = trade storage for speed.

---

## 🗄️ Databases

### SQL vs NoSQL

* **SQL** = Structured, relational, strong consistency.
* **NoSQL** = Flexible schema, high scalability.

### Indexing

* **Primary index** = unique identifier.
* **Secondary index** = extra lookups.

### Scaling DBs

* **Sharding** = Splitting data horizontally.
* **Replication** = Multiple copies for availability.
* **Partitioning** = Logical division of data.

**Interview one-liner:** SQL for transactions, NoSQL for scale.

---

## ⚖️ Load Balancers

* **Distributes traffic** across servers.

### Algorithms

* Round Robin
* Least Connections
* IP Hash

### Types

* **L4 (Transport layer)**
* **L7 (Application layer)**

**Interview one-liner:** Load balancer = traffic cop of distributed systems.

---

## 📩 Message Queues & Event-driven Systems

* **Kafka, RabbitMQ, AWS SQS**.
* Decouples producer and consumer.
* Helps with async tasks and spikes.

**Real-world example:** Order placed → Queue → Inventory service processes.

**Interview one-liner:** Queues smoothen traffic spikes and decouple services.

---

## 🛡️ Reliability & Scalability Patterns

* **CAP Theorem:** Consistency, Availability, Partition Tolerance → can pick only 2.
* **Replication** → improves availability.
* **Failover** → backup system takes over.
* **Auto-scaling** → AWS/GCP adds servers based on demand.

**Interview one-liner:** In distributed systems, you can’t have perfect consistency + availability.

---

## 🏛️ Common Components

* **CDN** → Faster static content delivery.
* **API Gateway** → Entry point for microservices.
* **Reverse Proxy** → Security + load balancing.
* **Authentication & Authorization** → OAuth, JWT.

---

## 📚 Example High-level Designs

### Design Instagram Feed

* Client requests feed.
* API Gateway routes request.
* Feed Service queries DB + cache.
* Media stored in S3 + served via CDN.

### Design URL Shortener

* Hash function for mapping.
* Store in DB with expiry.
* Cache frequently accessed links.

### Design Food Delivery (Zomato/Swiggy)

* Search Service (Elasticsearch).
* Order Service + Queue.
* Tracking via WebSockets.

---

## 🎯 Final Interview Tips

* Always **clarify requirements**.
* Define **scale (users, QPS, storage)**.
* Draw **HLD (components, flows)**.
* Discuss **trade-offs** (SQL vs NoSQL, cache vs DB).
* Think about **failures & scaling**.

**Golden line:** System design is not about the best design, but the most reasonable trade-offs for the given requirements.

---
