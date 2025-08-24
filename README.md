# 🛠️ System Design Interview Prep (SDE-1 / 2 YOE)

A collection of core **system design topics** explained in a structured way:  
✅ Quick **Interview one-liner** to answer confidently  
✅ Expandable `<details>` for deeper knowledge  
✅ Real-world examples & trade-offs  

---

## 🧱 Monolith vs Microservices

**Interview one-liner:**  
"Monolith = single deployable unit; Microservices = multiple small services communicating over APIs, enabling scalability and independent deployments."

<details>
<summary>📖 Detailed Explanation</summary>

- **Monolith:** All code + logic in a single deployable artifact (e.g., WAR/JAR in Java).  
- **Microservices:** Each service handles one responsibility (Auth, Payments, Orders). They communicate via REST/gRPC/message queues.  

</details>

<details>
<summary>🌍 Real-world Examples</summary>

- Monolith → Early LinkedIn, Twitter.  
- Microservices → Netflix, Uber, Amazon.  

</details>

<details>
<summary>⚖️ Trade-offs</summary>

- ✅ Microservices: Independent scaling, faster deployments, fault isolation.  
- ❌ Microservices: Complex infra, debugging harder.  
- ✅ Monolith: Simple to build/deploy/test.  
- ❌ Monolith: Difficult to scale, team bottlenecks.  

</details>

---

## 📈 Horizontal vs Vertical Scaling

**Interview one-liner:**  
"Vertical = add more power to one machine; Horizontal = add more machines to share the load."

<details>
<summary>📖 Detailed Explanation</summary>

- **Vertical scaling (scale up):** Increase CPU, RAM, disk of a single server.  
- **Horizontal scaling (scale out):** Add multiple servers behind a load balancer.  

</details>

<details>
<summary>🌍 Real-world Examples</summary>

- Vertical → Buying a bigger AWS EC2 instance.  
- Horizontal → Adding multiple EC2 instances behind an AWS ELB.  

</details>

<details>
<summary>⚖️ Trade-offs</summary>

- ✅ Vertical: Simple, no code changes.  
- ❌ Vertical: Hardware limits, single point of failure.  
- ✅ Horizontal: Fault tolerance, theoretically infinite scale.  
- ❌ Horizontal: Requires distributed systems, data partitioning.  

</details>

---

## 🗄️ Caching

**Interview one-liner:**  
"Cache = temporary fast storage to reduce latency and avoid hitting DB repeatedly."

<details>
<summary>📖 Detailed Explanation</summary>

- **Client-side cache:** Browser storing static assets (CSS, JS, images).  
- **Server-side cache:** Reverse proxies (NGINX, Varnish).  
- **Distributed cache:** Redis, Memcached for storing computed data.  

</details>

<details>
<summary>🌍 Real-world Examples</summary>

- Netflix stores recommendation results in Redis.  
- Amazon caches product details to reduce DB load.  

</details>

<details>
<summary>⚖️ Trade-offs</summary>

- ✅ Faster response times, reduces DB load.  
- ❌ Stale data, cache invalidation is hard.  

</details>

---

## 🧩 CAP Theorem

**Interview one-liner:**  
"In a distributed system, you can only guarantee 2 of Consistency, Availability, Partition tolerance — never all 3."

<details>
<summary>📖 Detailed Explanation</summary>

- **Consistency (C):** Every read gets the latest write.  
- **Availability (A):** Every request gets a response, even if stale.  
- **Partition tolerance (P):** System keeps working despite network issues.  

</details>

<details>
<summary>🌍 Real-world Examples</summary>

- CP → Traditional SQL DBs (Consistency + Partition Tolerance).  
- AP → DynamoDB, Cassandra (Availability + Partition Tolerance).  
- CA → Only possible if no network partitions (rare in practice).  

</details>
