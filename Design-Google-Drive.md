# Design Google Drive

---

# Problem Description

Design a cloud-based file storage and synchronization system similar to Google Drive, Dropbox, or OneDrive.

The system should allow users to upload, download, store, synchronize, and share files across multiple devices. Users should be able to access files from web and mobile applications seamlessly.

The design should focus on:

* Scalability
* Reliability
* File synchronization
* Distributed storage
* Consistency
* High availability
* Metadata management
* Efficient bandwidth usage

The platform should support millions of users and petabytes of storage while ensuring fast synchronization and reliable file access.

---

# Topic Tags

* System Design
* Distributed Systems
* Cloud Storage
* File Synchronization
* Database Design
* API Design
* Scalability
* Caching
* Load Balancing
* Consistency

---

# Expected Architecture Structure

```text
Client Applications
        ↓
Load Balancer
        ↓
API Servers
        ↓
Metadata Cache
        ↓
Metadata Database
        ↓
Block Servers
        ↓
Cloud Storage (S3/GCS)
```

Additional optional components:

* Notification Service
* Offline Backup Queue
* CDN
* Analytics Service
* Monitoring & Logging
* Cold Storage
* Authentication Service

---

# Difficulty Level Notes

## Beginner — Context Diagram

Focus Areas:

* User interaction with the cloud storage system
* File upload and download flow
* Basic synchronization flow
* System boundary

Expected Components:

* User
* Google Drive System
* Cloud Storage
* Database

---

## Intermediate — Container Diagram

Focus Areas:

* Internal services and communication
* File upload/download pipeline
* Metadata handling
* Notification system
* Caching layer
* Block storage architecture

Expected Components:

* Load Balancer
* API Servers
* Metadata Database
* Cache Layer
* Block Servers
* Notification Service
* Cloud Storage

---

## Advanced — Component Diagram

Focus Areas:

* Delta sync
* Chunking and block storage
* Compression and encryption
* Multi-region replication
* Strong consistency
* Conflict resolution
* Failure handling
* Cold storage optimization

Expected Concepts:

* Block-level storage
* Long polling/WebSocket
* Replication & failover
* Queue-based recovery
* Metadata consistency
* Deduplication
* Distributed caching

---

# Functional Requirements

1. Users should be able to upload files.
2. Users should be able to download files.
3. Files should sync automatically across devices.
4. Users should be able to view file revision history.
5. Users should be able to share files with others.
6. Users should receive notifications when files are updated/shared/deleted.
7. The system should support resumable uploads.
8. The system should support any file type.
9. Files should be encrypted before storage.
10. The system should support mobile and web applications.

---

# Non-Functional Requirements

1. High Availability — The system should remain operational during failures.
2. Reliability — File loss is unacceptable.
3. Scalability — The system should support millions of users and petabytes of storage.
4. Low Latency — File synchronization should happen quickly.
5. Strong Consistency — Users should see the latest file version consistently.
6. Bandwidth Optimization — Minimize unnecessary data transfer.
7. Durability — Files should remain safe even during regional outages.
8. Security — Files and metadata should be encrypted and protected.

---

# Constraints

1. Assume 50 million registered users.
2. Assume 10 million daily active users (DAU).
3. Each user gets 10 GB free storage.
4. Average user uploads 2 files per day.
5. Average file size is 500 KB.
6. Read/Write ratio is 1:1.
7. Total storage allocation is approximately 500 PB.
8. Upload QPS is approximately 240 requests/second.
9. Peak upload QPS is approximately 480 requests/second.
10. Maximum file size supported is 10 GB.

---

# Hints & Guidance

1. Consider splitting large files into smaller blocks.
2. Think about resumable uploads for unstable networks.
3. Consider delta sync to reduce bandwidth usage.
4. Think about metadata consistency strategies.
5. Consider block deduplication for storage optimization.
6. Think about multi-region replication for durability.
7. Consider long polling or WebSocket for notifications.
8. Think about handling sync conflicts.
9. Consider cold storage for inactive files.
10. Think about database sharding and replication.

---

# Evaluation Spec (Stage B)

---

# Beginner Level — Context Diagram

## Functional Requirements

1. Show file upload flow.
2. Show file download flow.
3. Include users/devices.
4. Include cloud storage.
5. Include metadata/database storage.

## Non-Functional Requirements

1. Basic scalability awareness.
2. Basic reliability understanding.
3. Clear system boundary representation.

## Anti-Patterns

1. Missing storage component.
2. No synchronization flow.
3. No metadata/database representation.
4. Mixing low-level implementation details in context diagram.

---

# Intermediate Level — Container Diagram

## Functional Requirements

1. Include Load Balancer.
2. Include API Servers.
3. Include Metadata Database.
4. Include Cache layer.
5. Include Block Servers.
6. Include Notification Service.
7. Include Cloud Storage.
8. Show upload and download flows.

## Non-Functional Requirements

1. Horizontal scalability.
2. Fast synchronization.
3. Reliable storage design.
4. High availability consideration.
5. Efficient bandwidth usage.

## Anti-Patterns

1. Storing large files directly in database.
2. No caching layer.
3. Single point of failure.
4. No load balancing.
5. No replication strategy.

---

# Advanced Level — Component Diagram

## Functional Requirements

1. Include block chunking mechanism.
2. Include compression and encryption flow.
3. Include delta synchronization logic.
4. Include metadata consistency strategy.
5. Include replication and failover mechanisms.
6. Include file versioning system.
7. Include conflict resolution mechanism.
8. Include offline backup queue.
9. Include deduplication logic.
10. Include cold storage handling.

## Non-Functional Requirements

1. Multi-region deployment awareness.
2. Strong consistency guarantees.
3. Disaster recovery support.
4. Fault tolerance during server failures.
5. Optimized bandwidth usage.
6. Efficient metadata caching.
7. Reliable synchronization across devices.
8. Secure file storage and transfer.

## Anti-Patterns

1. No replication for storage.
2. No backup strategy.
3. Uploading entire file on every update.
4. No conflict resolution handling.
5. Storing binary files inside metadata database.
6. No cache invalidation strategy.
7. No failure recovery plan.
8. No encryption support.
