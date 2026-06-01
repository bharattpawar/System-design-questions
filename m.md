 # Design a URL Shortener (e.g., TinyURL / Bitly)

---

# Problem Description

Design a distributed URL shortening service similar to TinyURL or Bitly.

The system should accept a long URL and generate a short, unique alias that can be shared easily. When a user visits the shortened URL, the service should quickly redirect them to the original long URL.

The platform should support:

* Custom aliases
* Configurable expiration times
* Analytics tracking
* High scalability for billions of redirections

The design should focus on:

* Scalability
* Reliability
* Low latency
* Database design
* API design
* Distributed system trade-offs
* Caching strategies

---

# Topic Tags

* System Design
* Distributed Systems
* API Design
* Database Design
* Caching
* Scalability
* Hashing & Encoding
* Load Balancing

---

# Expected Architecture Structure

```text
Client
   ↓
CDN
   ↓
Load Balancer
   ↓
API Servers
   ↓
Cache Layer (Redis)
   ↓
Database Cluster
```

Additional optional components:

* Rate Limiter
* Analytics Service
* Message Queue
* Monitoring & Logging
* Distributed ID Generator
* URL Encoding Service

---

# Difficulty Level Notes

## Beginner — Context Diagram

Focus Areas:

* Users interacting with the system
* System boundary
* URL creation flow
* URL redirection flow

Expected Components:

* User / Browser
* URL Shortener Service
* Database

---

## Intermediate — Container Diagram

Focus Areas:

* Internal services
* Load balancing
* Cache layer
* Database interactions
* Read-heavy optimizations

Expected Components:

* Load Balancer
* API Servers
* Cache (Redis)
* Primary Database
* Read Replicas
* Analytics Service

---

## Advanced — Component Diagram

Focus Areas:

* Distributed ID generation
* Base62 encoding
* Database sharding
* Replication & failover
* Cache invalidation
* Hot key handling
* Multi-region deployment
* Security & abuse prevention

Expected Concepts:

* Consistent Hashing
* Bloom Filters
* Async Analytics Processing
* Disaster Recovery
* Monitoring & Observability

---

# Functional Requirements

1. Given a long URL, the system should generate a short and unique alias.
2. Users should be redirected to the original URL when accessing the short link.
3. Users should optionally be able to create custom aliases.
4. Users should be able to specify expiration times for links.
5. The system should prevent duplicate aliases.
6. The service should support analytics such as click counts.
7. The system should validate URLs before shortening them.
8. The service should support API-based access for external applications.

---

# Non-Functional Requirements

1. High Availability — URL redirection should continue even during failures.
2. Low Latency — Redirection should happen within milliseconds.
3. Scalability — The system should support billions of redirects.
4. Durability — URL mappings should not be lost.
5. Fault Tolerance — System should recover from failures.
6. Security — Short URLs should not be easily guessable.
7. Reliability — System should maintain high uptime.
8. Observability — Monitoring and logging should be available.

---

# Constraints

1. Traffic: Assume 100 million new URLs generated per month.
2. Read/Write Ratio: Assume a 100:1 read-to-write ratio.
3. Redirections: Approximately 10 billion redirects per month.
4. Storage Duration: URLs are stored for 5 years.
5. Total Records: Approximately 6 billion URL mappings.
6. Data Size: Each record is approximately 500 bytes.
7. Estimated Storage: Around 3 TB total storage required.
8. Write Throughput: Approximately 40 writes/second.
9. Read Throughput: Approximately 4,000 reads/second.
10. System should support horizontal scaling.

---

# Hints & Guidance

1. Consider using Base62 encoding for generating short URLs.
2. Think about collision handling strategies.
3. Consider Redis caching for popular URLs.
4. Think about scaling a read-heavy workload.
5. Consider database sharding strategies.
6. Think about cache invalidation mechanisms.
7. Consider asynchronous analytics processing.
8. Think about abuse prevention and rate limiting.
9. Consider failover strategies for high availability.
10. Think about using CDN for low latency redirects.

---

# Evaluation Spec (Stage B)

---

# Beginner Level — Context Diagram

## Functional Requirements

1. Show URL creation flow.
2. Show URL redirection flow.
3. Include external users/clients.
4. Include persistent storage.
5. Include URL shortening service.

## Non-Functional Requirements

1. Basic scalability understanding.
2. Basic reliability awareness.
3. Clear system boundary representation.

## Anti-Patterns

1. Missing database component.
2. No redirect flow shown.
3. Ambiguous system boundaries.
4. Mixing implementation details in context diagram.

---

# Intermediate Level — Container Diagram

## Functional Requirements

1. Include Load Balancer.
2. Include Stateless API Servers.
3. Include Cache layer (Redis/Memcached).
4. Include Database layer.
5. Show URL generation mechanism.
6. Include analytics processing flow.
7. Show read/write data flow.

## Non-Functional Requirements

1. Read-heavy optimization.
2. Horizontal scalability.
3. Low latency design.
4. High availability consideration.
5. Cache usage explanation.

## Anti-Patterns

1. Single monolithic database without scaling plan.
2. No cache for read-heavy traffic.
3. Stateful application servers.
4. Direct client access to database.
5. No load balancing.

---

# Advanced Level — Component Diagram

## Functional Requirements

1. Include distributed ID generation service.
2. Include Base62 encoding logic.
3. Include cache invalidation/update strategy.
4. Include database sharding mechanism.
5. Include replication and failover strategy.
6. Include analytics queue/event processing.
7. Include rate limiter and abuse prevention.
8. Include monitoring and observability components.
9. Include expiration cleanup mechanism.
10. Include hot key handling strategy.

## Non-Functional Requirements

1. Multi-region deployment awareness.
2. Fault tolerance and disaster recovery.
3. Consistency vs availability tradeoff discussion.
4. Scalability under extreme read traffic.
5. Reliability during node failures.
6. Efficient cache management.
7. Security against URL enumeration attacks.

## Anti-Patterns

1. Single point of failure.
2. No replication strategy.
3. Random alias generation without collision handling.
4. No database partitioning for large scale.
5. Synchronous analytics processing in request path.
6. No rate limiting or abuse prevention.
7. Storing analytics directly in primary database.
8. No monitoring or alerting strategy.
