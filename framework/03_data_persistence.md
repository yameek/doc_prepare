[← Back to Index](./README.md)

# 3. Data Persistence (ORM / Query Builder)

How your application talks to the database. This is often the biggest bottleneck and source of complexity.

## Junior -> Mid: The Basics
**Goal:** Can perform CRUD (Create, Read, Update, Delete) operations using the framework's tools.

### 1. Models / Entities
- **Concept:** Code representation of a database table.
- **Key Skills:**
    - Defining a model class (e.g., `User` class maps to `users` table).
    - Defining basic fields (String, Integer, Boolean).
    - Understanding Primary Keys (IDs).

### 2. Basic Querying
- **Concept:** Getting data without writing SQL.
- **Key Skills:**
    - **Find by ID:** `User.find(1)`.
    - **Simple Filters:** `User.where(email='bob@example.com')`.
    - **Saving/Updating:** `user.name = 'Alice'; user.save()`.
    - **Deleting:** `user.delete()`.

### 3. Relationships (Basic)
- **Concept:** Linking tables.
- **Key Skills:**
    - **One-to-Many:** A User has many Posts.
    - **Many-to-One:** A Post belongs to a User.
    - Accessing related data (e.g., `user.posts`).

---

## Mid -> Senior: Optimization & Reliability
**Goal:** Writes efficient queries, manages schema changes, and handles concurrency.

### 1. Migrations
- **Concept:** Version control for your database schema.
- **Key Knowledge:**
    - **Up/Down Scripts:** Writing scripts to apply and revert changes.
    - **CI/CD Integration:** Running migrations automatically during deployment.
    - **Seed Data:** Populating the DB with initial data for development.

### 2. Advanced Querying & Performance
- **Concept:** Avoiding "N+1" problems and slow queries.
- **Key Knowledge:**
    - **Eager Loading:** Fetching related data in one query (`User.include('posts')`) vs N queries.
    - **Indexing:** Knowing when and how to add indexes to columns.
    - **Pagination:** Efficiently fetching pages of data (`limit` / `offset` vs cursor-based).
    - **Transactions:** Ensuring atomicity (all or nothing) for multi-step operations.

### 3. Connection Management
- **Concept:** Efficiently using database resources.
- **Key Knowledge:**
    - **Connection Pooling:** Why we reuse connections instead of opening a new one for every request.
    - **Timeouts:** Handling DB connection failures gracefully.

---

## Senior -> Lead: Scale & Complexity
**Goal:** Designs data layers for high-scale, distributed systems.

### 1. Advanced Patterns
- **Concept:** Beyond simple CRUD.
- **Key Knowledge:**
    - **Repository Pattern:** Abstracting the data source so you can swap SQL for NoSQL or an external API.
    - **Unit of Work:** Tracking changes to multiple objects and committing them all at once.
    - **Soft Deletes:** Marking records as deleted (`deleted_at` timestamp) instead of removing them.

### 2. Scaling Strategies
- **Concept:** Handling massive data volumes.
- **Key Knowledge:**
    - **Read Replicas:** Directing read queries to slave DBs and writes to the master.
    - **Sharding:** Splitting data across multiple servers (e.g., by User ID).
    - **Caching Strategies:** Write-through, Write-back, and Cache-aside patterns with Redis/Memcached.

### 3. Complex Data Integrity
- **Concept:** Ensuring data correctness in complex scenarios.
- **Key Knowledge:**
    - **Optimistic vs Pessimistic Locking:** Handling concurrent updates to the same record.
    - **Event Sourcing:** Storing the sequence of state-changing events instead of just the current state.
    - **Polyglot Persistence:** Using the right DB for the job (e.g., Postgres for relational, Mongo for documents, Neo4j for graphs).
