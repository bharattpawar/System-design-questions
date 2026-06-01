Problem Name

Design a URL Shortener (e.g., TinyURL / Bitly)

Problem Description

Design a distributed URL shortening service similar to TinyURL or Bitly.

The system should accept a long URL and generate a short, unique alias that can be shared easily. When a user visits the shortened URL, the service should quickly redirect them to the original long URL.

The platform should support custom aliases, configurable expiration times, analytics tracking, and high scalability for billions of redirections.

The design should focus on scalability, reliability, low latency, database design, caching strategy, API design, and distributed system trade-offs.

Topic Tags

System Design, Distributed Systems, API Design, Database Design, Caching, Scalability, Hashing & Encoding, Load Balancing

Expected Architecture Structure

Client → CDN → Load Balancer → API Servers → Cache → Database

Additional optional components:

Rate Limiter
Analytics Service
Message Queue
Monitoring & Logging
URL Encoding Service
Distributed ID Generator
Difficulty Level Notes
Beginner — Context Diagram

Focus on:

Users interacting with the URL shortening system
High-level system boundary
URL creation flow
URL redirection flow
External actors and APIs

Candidates should identify:

User
URL Shortener Service
Database
Browser / Client
Intermediate — Container Diagram

Focus on:

Internal services and communication
API layer
Cache usage
Database partitioning
Read-heavy optimization
URL generation strategy

Candidates should explain:

Load balancer
Stateless API servers
Cache (Redis)
Primary database
Read replicas
Analytics pipeline
Advanced — Component Diagram

Focus on:

Detailed internals and scalability
Cache invalidation
Distributed unique ID generation
Base62 encoding
Database sharding
Replication & failover
Rate limiting
Hot key handling
Security & abuse prevention

Candidates should discuss:

Consistent hashing
Bloom filters
Async analytics processing
Multi-region deployment
Disaster recovery
Monitoring & observability
Functional Requirements
Given a long URL, the system should generate a short and unique alias.
Users should be redirected to the original URL when accessing the short link.
Users should optionally be able to create custom aliases.
Users should be able to specify expiration times for links.
The system should prevent duplicate aliases.
The service should support analytics such as click counts.
The system should validate URLs before shortening them.
The service should support API-based access for external applications.
Non-Functional Requirements
High Availability — URL redirection should continue even during failures.
Low Latency — Redirection should happen within milliseconds.
Scalability — The system should support billions of redirects.
Durability — URL mappings should not be lost.
Fault Tolerance — System should recover from server/database failures.
Security — Short URLs should be difficult to predict.
Reliability — The redirect service should maintain high uptime.
Observability — Monitoring, metrics, and logging should be available.
Constraints
Traffic: Assume 100 million new URLs are created per month.
Read/Write Ratio: Assume a 100:1 read-to-write ratio.
Redirections: Approximately 10 billion redirects per month.
Storage Duration: URLs are stored for 5 years.
Total Records: Approximately 6 billion URL mappings.
Data Size: Each record is approximately 500 bytes.
Estimated Storage: Total storage required is around 3 TB.
Write Throughput: Approximately 40 writes per second.
Read Throughput: Approximately 4,000 reads per second.
System should support horizontal scaling.
Hints & Guidance
Consider using Base62 encoding for short URL generation.
Think about how to avoid collisions while generating aliases.
Consider Redis caching for frequently accessed URLs.
How would you scale a read-heavy workload?
Think about database sharding strategies.
How would you handle expired links efficiently?
Consider asynchronous analytics processing using queues.
How would you prevent abuse or malicious URL spam?
Think about failover strategies for high availability.
How can CDN improve redirection latency?
Evaluation Spec (Stage B)
Beginner Level — Context Diagram
Functional Requirements
System should show URL creation flow.
System should show URL redirection flow.
System should identify external users/clients.
System should include persistent storage.
System should include the main URL shortening service.
Non-Functional Requirements
Basic scalability awareness.
Basic reliability understanding.
Clear system boundary representation.
Anti-Patterns
Missing database component.
No redirect flow shown.
Ambiguous system boundaries.
Mixing low-level implementation details in context diagram.
Intermediate Level — Container Diagram
Functional Requirements
Include Load Balancer.
Include Stateless API Servers.
Include Cache layer (Redis/Memcached).
Include Database layer.
Show URL generation mechanism.
Include analytics processing flow.
Include read/write data flow.
Non-Functional Requirements
Read-heavy optimization.
Horizontal scalability.
Low latency design.
High availability consideration.
Cache usage explanation.
Anti-Patterns
Single monolithic database without scaling plan.
No cache for read-heavy traffic.
Stateful application servers.
Direct client access to database.
No load balancing.
Advanced Level — Component Diagram
Functional Requirements
Include distributed ID generation service.
Include Base62 encoding logic.
Include cache invalidation/update strategy.
Include database sharding mechanism.
Include replication and failover strategy.
Include analytics queue/event processing.
Include rate limiter and abuse prevention.
Include monitoring and observability components.
Include expiration cleanup mechanism.
Include hot key handling strategy.
Non-Functional Requirements
Multi-region deployment awareness.
Fault tolerance and disaster recovery.
Consistency vs availability tradeoff discussion.
Scalability under extreme read traffic.
Reliability during node failures.
Efficient cache management.
Security against URL enumeration attacks.
Anti-Patterns
Single point of failure.
No replication strategy.
Generating random aliases without collision handling.
No database partitioning for large scale.
Synchronous analytics processing in request path.
No rate limiting or abuse prevention.
Storing all traffic logs in primary database.
No monitoring or alerting strategy.
