Here is your **100-Question Database Master Sheet**, specifically tailored for a Junior/Mid-level Backend Developer interview at a top-tier service company like EPAM. It heavily emphasizes NoSQL, distributed theory (CAP/BASE), scenario-based decision-making, and deep SQL internals.

As requested, **there are no answers here**. This is your pure study syllabus.

---

### 📊 Category 1: Core SQL, Querying & Window Functions (1-10)
*Focus: Can you write complex queries and understand set-based operations?*
1. What is the exact difference between `WHERE` and `HAVING` clauses? At what stage of the SQL execution order do they run?
2. Explain the difference between `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `FULL OUTER JOIN`. What happens to unmatched rows in each?
3. What is a `CROSS JOIN`? Give a practical scenario where you would intentionally use it.
4. What is the difference between `UNION` and `UNION ALL`? Which one is faster and why?
5. Explain the difference between `RANK()`, `DENSE_RANK()`, and `ROW_NUMBER()` window functions. 
6. How do you find the top 3 highest-paid employees in *each* department using a single SQL query?
7. What is a Common Table Expression (CTE)? How does it differ from a temporary table or a subquery?
8. How do you find duplicate records in a table based on multiple columns?
9. Write a query to find the running total (cumulative sum) of sales for each day in a given month.
10. What is the difference between `TRUNCATE`, `DELETE`, and `DROP`? How do they affect transaction logs and auto-increment counters?

### 🏗️ Category 2: Database Internals, Indexing & Storage (11-20)
*Focus: How does the database actually store and retrieve data under the hood?*
11. How is a B-Tree index structured? What is the time complexity of a lookup, insert, and delete?
12. What is the difference between a Clustered Index and a Non-Clustered (Secondary) Index? How many of each can a table have?
13. How do Hash indexes work? Why can't they be used for range queries (e.g., `BETWEEN`, `>`, `<`) or `ORDER BY`?
14. What is a Composite (Multi-column) Index? Explain the "Leftmost Prefix Rule" and how column order impacts query performance.
15. What is Index Fragmentation? How does it happen during heavy `INSERT/UPDATE/DELETE` operations, and how do you fix it?
16. What is the difference between an Index Scan, an Index Seek, and a Full Table Scan?
17. What is a Covering Index? How does it prevent the database from having to read the actual table data (heap/clustered index)?
18. Explain the concept of Database Pages and Extents. How does the DB read data from the disk into memory?
19. What is the difference between a Heap table (no clustered index) and a table with a clustered index?
20. Why is using a `UUID` as a Primary Key often bad for B-Tree index performance compared to an auto-incrementing integer?

### 🔒 Category 3: Transactions, ACID & Isolation Levels (21-30)
*Focus: Data integrity, concurrency control, and preventing anomalies.*
21. Explain the ACID properties in deep technical detail. How does a database physically ensure Durability?
22. What is a Dirty Read, a Non-Repeatable Read, and a Phantom Read? Give a concrete example of each.
23. Explain the 4 Transaction Isolation Levels (Read Uncommitted, Read Committed, Repeatable Read, Serializable). Which anomalies does each level prevent?
24. What is the default isolation level in PostgreSQL/MySQL, and why was it chosen?
25. What is MVCC (Multi-Version Concurrency Control)? How does it allow readers to not block writers?
26. What is the difference between Pessimistic Locking (`SELECT ... FOR UPDATE`) and Optimistic Locking (using a `version` column)?
27. How do you detect and resolve a Deadlock in a relational database?
28. What is a Savepoint in a transaction? How do you roll back to a specific savepoint?
29. What is the difference between a Local Transaction and a Distributed Transaction (Two-Phase Commit / 2PC)?
30. Why is the `SERIALIZABLE` isolation level rarely used in high-traffic web applications? What is the performance cost?

### 📐 Category 4: Database Design, Normalization & Modeling (31-40)
*Focus: Structuring data for integrity, performance, and business logic.*
31. Explain the First, Second, Third, and Boyce-Codd Normal Forms (1NF, 2NF, 3NF, BCNF). Give an example of a violation for each.
32. When and why would you intentionally **denormalize** a database schema? What are the trade-offs?
33. What is the difference between a Natural Key and a Surrogate Key? When would you strictly use a Surrogate Key?
34. How do you model a Many-to-Many relationship in a relational database? 
35. What is a Soft Delete? What are the pros and cons of using a `is_deleted` boolean flag vs actually deleting the row?
36. How do you design an Audit Trail (tracking who changed what and when) in a relational database?
37. What is the difference between an Entity-Relationship (ER) diagram and a physical database schema?
38. How do you handle hierarchical data (e.g., a category tree or an org chart) in a relational database? (Adjacency list vs Nested sets vs Materialized path).
39. What is the difference between a Primary Key and a Unique Constraint? Can a table have multiple Unique Constraints? Can they accept NULLs?
40. How do you design a database schema to support multi-tenancy in a SaaS application? (Shared DB vs Shared Schema vs Schema per Tenant).

### 🌐 Category 5: NoSQL Fundamentals & Distributed Theory (41-50)
*Focus: CAP, BASE, and the theoretical foundations of distributed databases.*
41. Explain the **CAP Theorem**. What do Consistency, Availability, and Partition Tolerance mean in a distributed system?
42. According to CAP, why can a distributed database only guarantee two out of three? Why is "CP" vs "AP" a false dichotomy during normal operations (PACELC theorem)?
43. Explain the **BASE** properties (Basically Available, Soft state, Eventual consistency). How does BASE contrast with ACID?
44. What is Eventual Consistency? How do you handle a scenario where a user reads stale data due to eventual consistency?
45. What is Tunable Consistency (e.g., in Cassandra)? Explain the difference between `ONE`, `QUORUM`, and `ALL` consistency levels.
46. What is the difference between Strong Consistency (Linearizability) and Sequential Consistency?
47. What is a Vector Clock or a Version Vector? How do NoSQL databases use them to detect conflicting writes?
48. What is the "Last Write Wins" (LWW) conflict resolution strategy? What are its dangers?
49. Explain the concept of Quorum in distributed databases. How do you calculate the read and write quorum to ensure strong consistency?
50. What is the difference between a Push-based and Pull-based replication strategy in distributed databases?

### 🗄️ Category 6: Specific NoSQL Technologies & Scenarios (51-60)
*Focus: MongoDB, Redis, Cassandra, Elasticsearch, and Vector DBs.*
51. What are the core differences between Document (MongoDB), Key-Value (Redis), Wide-Column (Cassandra), and Graph (Neo4j) databases?
52. In MongoDB, what is the difference between embedding (nesting) documents and referencing them? When do you use which?
53. How does MongoDB's Aggregation Pipeline work? How is it similar to SQL `GROUP BY` and `JOIN`?
54. What is the WiredTiger storage engine in MongoDB? How does it handle document-level locking and compression?
55. Explain Redis persistence mechanisms: RDB (Snapshots) vs. AOF (Append Only File). What are the trade-offs between data safety and performance?
56. What are Redis Data Structures? How would you use Sorted Sets, Hashes, and HyperLogLogs in a real-world application?
57. How does Cassandra achieve high write throughput? Explain its write path (Memtable -> CommitLog -> SSTable).
58. What is a Wide-Column store? How does Cassandra's data model (Partition Key vs Clustering Column) differ from a relational primary key?
59. How does Elasticsearch use an Inverted Index to achieve fast full-text search? 
60. What is a Vector Database (e.g., Pinecone, Milvus, pgvector)? How does it store and query high-dimensional embeddings for GenAI/RAG?

### ⚡ Category 7: Caching Strategies & In-Memory Data Stores (61-70)
*Focus: Redis/Memcached integration, cache invalidation, and performance.*
61. Explain the Cache-Aside (Lazy Loading) pattern. What are its pros and cons?
62. What is the Write-Through caching strategy? How does it differ from Write-Back (Write-Behind)?
63. What is the "Cache Stampede" (or Thundering Herd) problem? How do you prevent it when a highly requested cache key expires?
64. Explain Redis eviction policies: `noeviction`, `allkeys-lru`, `volatile-lru`, `allkeys-lfu`. When would you use LFU over LRU?
65. How do you implement a distributed lock using Redis? What are the flaws in a simple `SETNX` approach, and how does Redlock solve them?
66. What is the difference between Redis and Memcached? When would you strictly choose Memcached?
67. How do you handle cache invalidation when the underlying database record is updated?
68. What is a "Cache Penetration" vs a "Cache Breakdown"? How do you solve Cache Penetration (e.g., caching nulls, Bloom filters)?
69. How do you serialize complex Python objects to store them in Redis? What are the trade-offs of using JSON vs Pickle vs MessagePack?
70. How do you monitor and measure the effectiveness of your caching layer? What metrics do you look at?

### 📈 Category 8: Scaling, Replication & Sharding (71-80)
*Focus: Handling massive data and high traffic.*
71. What is the difference between Vertical Scaling (Scale-Up) and Horizontal Scaling (Scale-Out) for databases?
72. Explain Master-Slave (Primary-Replica) replication. How do you route read vs write traffic in this setup?
73. What is Replication Lag? What causes it, and how does it impact application logic (e.g., reading from a replica right after a write)?
74. Explain Master-Master (Multi-Primary) replication. What is the "Split-Brain" problem, and how do tools like Patroni or etcd prevent it?
75. What is Database Sharding? How does it differ from Partitioning?
76. How do you choose a Shard Key? What makes a "good" shard key vs a "bad" shard key?
77. What is a "Hot Shard" (or Hotspot)? How do you prevent or resolve it?
78. Explain Consistent Hashing. How does it minimize data movement when adding or removing nodes in a distributed database/cache?
79. What is the difference between Application-level sharding and Database-native sharding (e.g., Citus, MongoDB sharded clusters)?
80. How do you perform a cross-shard query or a global secondary index lookup in a sharded database?

### 🐢 Category 9: Performance Tuning, Profiling & Troubleshooting (81-90)
*Focus: Finding and fixing slow queries and database bottlenecks.*
81. How do you read and interpret an `EXPLAIN` or `EXPLAIN ANALYZE` execution plan in PostgreSQL/MySQL?
82. What is the **N+1 Query Problem**? How do you detect it in an ORM (like SQLAlchemy/Django), and how do you fix it?
83. What is the difference between `select_related` (JOIN) and `prefetch_related` (separate query) in Django/SQLAlchemy? When do you use which?
84. Your database CPU is at 100%, but there are very few active queries. What could be the bottleneck? (Hint: Lock contention, connection exhaustion).
85. How do you identify and kill long-running or blocking queries in a production database safely?
86. What is Connection Pooling? Why is it critical for web applications, and what happens if the pool is exhausted? (Explain PgBouncer).
87. How does the database query optimizer work? Why might it choose a Full Table Scan over using an available Index?
88. What are Database Statistics (e.g., `ANALYZE` in Postgres)? Why is it important to keep them up to date?
89. How do you optimize an `INSERT` operation for millions of rows? (Batching, disabling indexes temporarily, `COPY` command).
90. What is the impact of having too many indexes on a table? How do you identify unused indexes?

### 🔄 Category 10: Application Integration, Migrations & Operations (91-100)
*Focus: The intersection of code and database, backups, and zero-downtime.*
91. What are the pros and cons of using an ORM (Object-Relational Mapper) vs writing raw SQL?
92. How do you handle database schema migrations in a CI/CD pipeline for a zero-downtime deployment? (Explain the Expand and Contract pattern).
93. What is the difference between a Logical Backup (e.g., `pg_dump`) and a Physical Backup (e.g., WAL archiving, PITR)?
94. Explain Point-in-Time Recovery (PITR). How does it use the Write-Ahead Log (WAL) to restore a database to a specific second?
95. How do you protect your database against SQL Injection at the application and database levels?
96. What is Row-Level Security (RLS) in PostgreSQL? When would you use it in a multi-tenant SaaS app?
97. How do you securely manage database credentials in a microservices architecture? (Why environment variables are bad, using AWS Secrets Manager/HashiCorp Vault).
98. What is a Database Proxy (e.g., ProxySQL, AWS RDS Proxy)? How does it help with connection pooling and read/write splitting?
99. How do you test database interactions in your application without hitting the actual production or even development database? (Explain Testcontainers, in-memory SQLite, or transaction rollback).
100. If you accidentally dropped a critical production table, what is your exact step-by-step recovery process?

---

### 💡 How to use this 100-Question Sheet:
1. **The "EPAM" Filter:** EPAM interviewers love **Category 3 (Isolation Levels)**, **Category 5 (CAP/BASE)**, and **Category 9 (N+1 / EXPLAIN plans)**. Master these first.
2. **NoSQL Deep Dive:** Don't just memorize what MongoDB is. Be ready to answer *why* you would choose Cassandra's wide-column model over MongoDB's document model for a specific scenario (Look at Q51, Q57, Q58).
3. **Live Coding Prep:** For Category 1 (SQL), actually open a SQL editor and write the queries for Q5, Q6, Q7, and Q9. You will likely be asked to write a Window Function or a CTE on a whiteboard/shared screen.
4. **Verbalize the Trade-offs:** For every "What is X?" question, force yourself to add "...and the trade-off is Y." (e.g., "Sharding increases write throughput, *but the trade-off is* it makes cross-shard joins and complex transactions incredibly difficult.")

You have the ultimate database syllabus. Get to work!