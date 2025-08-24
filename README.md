# 🛠️ System Design Notes for SDE‑1 (1–2 YOE)

A clean, beginner‑friendly, and interview‑oriented guide.

---

## 📌 Core Foundations

### What is System Design?

> "System Design is how we plan and organize the components of a software system to handle requirements, scalability, and reliability."

### HLD vs LLD

* **HLD (High Level Design):** Focuses on architecture, components, and data flow.
* **LLD (Low Level Design):** Focuses on class diagrams, database schema, and detailed logic.

### Why Companies Test System Design

> "To check if you can design scalable, reliable, and maintainable systems, not just write code."

### Real‑world Examples

* WhatsApp → chat system
* Instagram → media sharing
* Zomato → food ordering platform

---

## 🌐 How the Web Works

### DNS

> "DNS is like a phonebook that converts website names into IP addresses."

### IP

> "IP is the address of a machine on the internet."

### HTTP/HTTPS

> "HTTP is the protocol for communication between client and server. HTTPS is the secure version using encryption."

### Request/Response Lifecycle

> "Client sends a request, server processes it, and returns a response."

---

## 🔌 Networking Basics

### TCP vs UDP

* **TCP:** Reliable, ordered, slower (used in web, emails).
* **UDP:** Fast, lightweight, no guarantee (used in streaming, gaming).

### REST APIs

> "REST APIs let different systems talk using HTTP methods like GET, POST, PUT, DELETE."

### HTTP Methods

* GET → Read
* POST → Create
* PUT → Update
* DELETE → Remove

### Status Codes

* 200 → Success
* 404 → Not Found
* 500 → Server Error

---

## 💻 OS Basics

### Process vs Thread

* **Process:** Independent execution unit with its own memory.
* **Thread:** Lightweight unit inside a process sharing memory.

### Concurrency vs Parallelism

> "Concurrency is dealing with multiple tasks at once, parallelism is actually running them simultaneously."

---

## 🧩 Monolith vs Microservices

* **Monolith:** One big codebase, simple but hard to scale.
* **Microservices:** Small independent services, scalable but complex.

---

## 📈 Scaling

### Vertical Scaling

> "Adding more power (CPU, RAM) to a single machine."

### Horizontal Scaling

> "Adding more machines to handle load."

---

## 🗂️ Stateful vs Stateless

* **Stateful:** Server remembers client data (e.g., banking session).
* **Stateless:** Each request is independent (e.g., REST APIs).

---

## ⚡ Caching

### What is Caching?

> "Caching is storing frequently accessed data in memory for faster response."

### Types

* Client‑side → Browser cache
* CDN → Edge cache
* Server‑side → Redis, Memcached

### Eviction Policies

* LRU → Least Recently Used
* LFU → Least Frequently Used

---

## 🗄️ Databases

### SQL vs NoSQL

* **SQL:** Structured, relational (MySQL, Postgres).
* **NoSQL:** Flexible, unstructured (MongoDB, DynamoDB).

### Indexing

> "Indexing is like a book index that speeds up lookups in a database."

* Primary Index → Unique identifier
* Secondary Index → Non‑unique fields

### Sharding

> "Splitting a database into smaller chunks across servers."

### Replication

> "Copying data across multiple servers for reliability."

### Partitioning

> "Dividing a database/table for faster queries."

---

## ⚖️ Load Balancers

### What is Load Balancing?

> "Distributing incoming traffic across multiple servers to avoid overload."

### Algorithms

* Round Robin → Rotate requests equally
* Least Connections → Send to least busy server
* IP Hash → Stick user to one server

### L4 vs L7 Load Balancing

* L4 → Based on IP/port
* L7 → Based on application data (URL, headers)

---

## 📬 Messaging Systems

### What are Message Queues?

> "Message Queues decouple producers and consumers, allowing async communication."

### Popular Tools

* Kafka → High throughput streaming
* RabbitMQ → Reliable messaging
* AWS SQS → Cloud queue service

---

## 🛠️ Common Interview Topics

### CDN

> "CDN is a distributed network of servers that cache content closer to users."

### Consistency Models

* Strong → Always up‑to‑date
* Eventual → Updates propagate with delay

### CAP Theorem

> "You can only guarantee 2 out of 3: Consistency, Availability, Partition tolerance."

### Rate Limiting

> "Controlling the number of requests a client can make in a time frame."

### API Gateway

> "Single entry point for all client requests, handles routing, auth, rate limiting."

### Authentication vs Authorization

* Authentication → Who you are
* Authorization → What you can do

---

✅ This file gives you **easy interview one‑liners** for every important topic. When asked, start with the one‑liner, then expand with examples if required.
