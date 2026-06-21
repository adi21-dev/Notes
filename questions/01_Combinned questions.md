This is the ultimate, exhaustive master sheet tailored for an **EPAM Systems** interview (which heavily emphasizes engineering fundamentals, large-scale system design, legacy-to-modern migrations, and cross-domain integration). 

As requested, **there are no answers here**, and I have combined topics to reflect real-world architectural questions. There are **50+ deep-dive questions per category**, totaling over **450 questions**. 

Grab a coffee. This is your complete syllabus.

---

### 🐍 1. Python Core, Internals, Concurrency & Cross-Domain (50+)
**Memory & Internals:**
1. Explain the exact lifecycle of a Python object from creation to garbage collection.
2. How does Python’s cyclic garbage collector identify and clean up reference cycles? What are the three generations?
3. What is the difference between `__new__` and `__init__`? Write a scenario where overriding `__new__` is strictly necessary.
4. How are Python dictionaries implemented under the hood? How did Python 3.6+ change dict memory layout?
5. Explain hash collisions in Python dicts/sets and how they are resolved (open addressing vs chaining).
6. What are metaclasses? How do they differ from class decorators, and when would you use a metaclass over a decorator?
7. Explain the descriptor protocol (`__get__`, `__set__`, `__delete__`). How do `@property` and `@classmethod` use it?
8. What is the difference between `__getattr__`, `__getattribute__`, and `__setattr__`? How do you avoid infinite recursion in `__getattribute__`?
9. Explain Python's integer caching mechanism (the -5 to 256 range). How does `is` vs `==` behave outside this range?
10. What are weak references (`weakref`)? How do they interact with the garbage collector, and when are they useful (e.g., caching)?

**Advanced Features & Functional:**
11. How do closures capture variables? Explain the "late binding" gotcha in a loop of lambdas and how to fix it.
12. Write a decorator that accepts arguments, handles both sync and async functions, and preserves metadata.
13. What is the exact difference between an Iterable, an Iterator, and a Generator? How does `yield from` differ from `yield`?
14. Explain context managers. How do you implement one using a class vs `contextlib.contextmanager`? How does `contextlib.ExitStack` work?
15. What is the "mutable default argument" anti-pattern? How does Python evaluate default arguments at definition time vs runtime?
16. Explain `__slots__`. How does it save memory, and what limitations does it impose on inheritance and dynamic attributes?
17. What is monkey patching? Is it safe in production? How does `gevent` use it?
18. Explain the difference between `copy.copy()` and `copy.deepcopy()`. How does deepcopy handle circular references?
19. What are Python's magic methods for operator overloading? How do you implement a custom container (e.g., `__len__`, `__getitem__`)?
20. Explain type hinting in Python. What is the difference between `typing.Protocol` (structural subtyping) and standard inheritance (nominal subtyping)?

**Concurrency, GIL & Asyncio:**
21. Explain the GIL in CPython. Why was it introduced, and why is it so hard to remove completely?
22. How does Python 3.13’s experimental free-threading (PEP 703) change the concurrency model? What are the trade-offs?
23. Compare `threading`, `multiprocessing`, and `asyncio`. Give a strict rule for when to use each based on CPU-bound vs I/O-bound workloads.
24. How does the `asyncio` event loop work under the hood? What is the difference between cooperative and preemptive multitasking?
25. What happens if you call a blocking synchronous function (e.g., `time.sleep`, `requests.get`) inside an `async def`? How do you fix it (`run_in_executor`)?
26. Explain `asyncio.gather()` vs `asyncio.wait()` vs `asyncio.as_completed()`. When would you use `TaskGroup` (Python 3.11+)?
27. How do you achieve thread safety in Python? Explain `Lock`, `RLock`, `Semaphore`, `Condition`, and `Event`.
28. What is a race condition? How does the GIL mask race conditions in simple operations (e.g., `x += 1`), and why is it still unsafe?
29. Explain deadlocks in multithreading. How do you prevent them (lock ordering, timeouts)?
30. What is the difference between a coroutine and a task in `asyncio`? Why do you need to wrap coroutines in `asyncio.create_task()`?
31. How do you share state between multiple processes in Python? (Manager, Value, Array, multiprocessing.Queue). What are the performance implications?
32. Explain the Producer-Consumer pattern using `queue.Queue` (threads) vs `asyncio.Queue` (async).
33. How does `concurrent.futures.ThreadPoolExecutor` differ from `ProcessPoolExecutor`? How does `map` behave in both?
34. What is the difference between `asyncio.sleep()` and `time.sleep()`? Why is one non-blocking and the other blocking?
35. How do you handle exceptions in `asyncio` tasks? What happens if an exception is raised in a background task and never awaited?

**Python + DB/API Integration:**
36. How does SQLAlchemy handle connection pooling? How do you configure it for an async FastAPI application?
37. What is the N+1 query problem in SQLAlchemy/Django ORM? How do `select_related` and `prefetch_related` solve it?
38. How do you handle database transactions in Python? Explain `with engine.begin() as conn:` vs manual commit/rollback.
39. How do you prevent memory leaks in a long-running Python daemon processing a continuous stream of data?
40. Explain how Python's `pickle` module works. Why is it a security risk, and what are safer alternatives for serialization (JSON, MessagePack, Protobuf)?

---

### 🗄️ 2. Databases (Theory, Scenarios, Scaling & System Design) (50+)
**Core Theory & Internals:**
41. Explain the ACID properties in deep technical detail. How does a DB physically ensure Durability (WAL)?
42. Explain MVCC (Multi-Version Concurrency Control). How does it allow readers to not block writers in PostgreSQL?
43. Compare the 4 transaction isolation levels. What are dirty reads, non-repeatable reads, and phantom reads? Which level prevents which?
44. How do B-Tree indexes work? What is the difference between a clustered and non-clustered index?
45. How do Hash indexes work? Why can't they be used for range queries or sorting?
46. What is a composite index? Explain the "leftmost prefix" rule and how column order drastically affects query performance.
47. What is index fragmentation? How does it happen, and how do you fix it (REINDEX, VACUUM)?
48. Explain database normalization (1NF to BCNF). Give a concrete scenario where intentional denormalization is the correct architectural choice.
49. What is the Write-Ahead Log (WAL)? How does it facilitate crash recovery and replication?
50. Explain database checkpoints. Why are they necessary, and how do they impact write performance?

**NoSQL, Scenarios & "When to Choose What":**
51. Compare PostgreSQL, MongoDB, Cassandra, and Redis. Map each to a specific real-world use case.
52. You need to store 10 million IoT temperature readings per minute. Relational vs Time-Series (InfluxDB) vs NoSQL? Justify.
53. You are building a real-time leaderboard for a gaming app. What data structure and database do you use? (Redis Sorted Sets).
54. You need to store a social network's graph (users, friends, followers). Why is a Graph DB (Neo4j) better than SQL for "friends of friends" queries?
55. When would you choose a Document DB (MongoDB) over a Columnar DB (ClickHouse) for analytics?
56. Explain the CAP theorem. Can a system be strongly consistent and highly available during a network partition? (No). What is the PACELC extension?
57. What is eventual consistency? How do you implement it, and what are the user-facing implications?
58. Explain the difference between Master-Slave (Primary-Replica) and Master-Master replication. What is split-brain, and how is it resolved?
59. How does database sharding work? What makes a good shard key? What is a "hot shard" and how do you prevent it?
60. Explain consistent hashing. How is it used in distributed databases and caching (Memcached/Redis Cluster)?

**Advanced DB Scenarios & Optimization:**
61. What is connection pooling? Why is it critical for web apps, and what happens if the pool is exhausted?
62. Explain caching strategies: Cache-Aside, Write-Through, Write-Back, and Write-Around. When do you use each?
63. How do you handle cache invalidation? Explain the "cache stampede" problem and how to prevent it (locking, probabilistic early expiration).
64. What is the difference between logical and physical database backups? How do Point-in-Time Recovery (PITR) work?
65. How do you optimize a slow SQL query? Walk through your exact step-by-step process (EXPLAIN ANALYZE, indexes, query rewriting).
66. What are materialized views? When do you use them over standard views, and how do you refresh them?
67. Explain full-text search in databases. How do TSVECTOR (Postgres) or inverted indexes work? When do you switch to Elasticsearch?
68. What is database partitioning (horizontal) vs sharding? How do they differ?
69. How do you handle schema migrations in a zero-downtime deployment for a massive table (billions of rows)?
70. Explain the difference between optimistic and pessimistic locking. Give a code/SQL example of each.

---

### 🐳 3. Docker, Containerization & Orchestration (50+)
**Core Docker & Linux Internals:**
71. What are Linux Namespaces? Explain PID, Network, Mount, UTS, IPC, and User namespaces.
72. What are Linux Cgroups? How do they enforce resource limits (CPU, memory) on containers?
73. Explain UnionFS and OverlayFS. How does the Copy-on-Write (CoW) strategy work when a container modifies an image layer?
74. What is the exact difference between a Docker Image, a Layer, and a Container?
75. How does Docker handle networking by default? Explain the `docker0` bridge and NAT.
76. What is the difference between a Docker Volume, a Bind Mount, and a `tmpfs` mount? When do you use each?
77. How does Docker DNS resolution work for custom user-defined bridge networks? Why can containers ping each other by name?
78. Explain the Docker build cache. How does the order of `COPY` and `RUN` instructions affect cache invalidation?
79. What is a multi-stage build? Write a conceptual Dockerfile for a Python app using a builder stage and a distroless runtime stage.
80. Why is using `alpine` for Python containers sometimes a bad idea? (Explain musl libc vs glibc, and compilation issues for C-extensions).

**Optimization, Security & Best Practices:**
81. How do you minimize the size of a Docker image? (Combine RUN, use slim/distroless, clean apt caches, multi-stage).
82. How do you secure a Docker image? (Scan with Trivy, run as non-root user, drop capabilities, use distroless).
83. What is the `.dockerignore` file? Why is it critical for build performance and security?
84. How do you manage secrets in Docker? Why is `ENV` bad for secrets, and how do Docker Secrets or external vaults solve this?
85. Explain Docker healthchecks. How do you implement them, and how do orchestrators use them?
86. What is the difference between `ENTRYPOINT` and `CMD`? How do they interact when passing arguments at runtime?
87. How do you debug a container that keeps crashing immediately on startup? (`docker logs`, `docker inspect`, overriding entrypoint to `/bin/sh`).
88. What are Docker build args (`ARG`) vs environment variables (`ENV`)? When is data visible in the final image?
89. How do you handle logging in Docker? Explain the `json-file` driver vs shipping logs directly to ELK/Datadog via Fluentd.
90. What is rootless Docker? Why is it recommended for CI/CD and local development?

**Kubernetes & Orchestration (Combined):**
91. What is the difference between Docker Compose, Docker Swarm, and Kubernetes?
92. Explain K8s architecture: Control Plane (API Server, etcd, Scheduler, Controller Manager) vs Worker Nodes (kubelet, kube-proxy).
93. What is a Pod? Why does K8s use Pods instead of running containers directly? What is a sidecar container?
94. Explain K8s Deployments vs StatefulSets vs DaemonSets. When do you use each?
95. How does K8s Service discovery work? Explain ClusterIP, NodePort, and LoadBalancer.
96. What is an Ingress controller? How does it differ from a standard K8s Service?
97. Explain K8s ConfigMaps and Secrets. How do you update a ConfigMap without restarting the Pod?
98. What are K8s Probes? Explain Liveness, Readiness, and Startup probes. What happens if a Readiness probe fails?
99. How do you manage persistent storage in K8s? Explain PV (Persistent Volume), PVC, and StorageClasses.
100. What is Helm? Why is it called the "package manager for K8s", and how do Helm charts work?

---

### ☁️ 4. AWS Cloud, Infrastructure & CI/CD (50+)
**AWS Compute, Storage & Databases:**
101. Compare EC2, ECS Fargate, EKS, and AWS Lambda. Give a strict decision matrix for when to use each.
102. What are Lambda cold starts? How do you mitigate them? (Provisioned concurrency, keeping packages small, VPC considerations).
103. Explain S3 storage classes (Standard, IA, One Zone-IA, Glacier). How do S3 Lifecycle Policies work?
104. What is an S3 Presigned URL? How does it work securely without exposing AWS credentials to the client?
105. Compare EBS (Elastic Block Store) and EFS (Elastic File System). When do you use EBS volumes vs shared EFS?
106. Explain RDS Multi-AZ vs Read Replicas. How do they differ in terms of disaster recovery vs read scaling?
107. Compare DynamoDB and Aurora. When would you choose a NoSQL key-value store over a serverless relational DB?
108. What is DynamoDB DAX? How does it improve read performance?
109. Explain SQS (Standard vs FIFO) vs SNS. When do you use a queue vs a pub/sub topic?
110. What is Amazon EventBridge? How does it differ from SNS/SQS for event-driven architectures?

**AWS Networking, Security & Advanced:**
111. Explain the components of a VPC. What is the difference between a Public and Private subnet?
112. How do you allow a service in a Private subnet to access the internet (e.g., to download an S3 file) without exposing it to inbound traffic? (NAT Gateway).
113. What is the difference between an Internet Gateway (IGW) and a NAT Gateway?
114. Explain Security Groups vs Network ACLs (NACLs). Stateful vs Stateless?
115. What is AWS IAM? Explain the difference between an IAM User, IAM Role, and IAM Policy.
116. How does IAM AssumeRole work? How is it used for cross-account access or EC2/ECS accessing S3?
117. Compare AWS Secrets Manager and Systems Manager (SSM) Parameter Store. When do you use which?
118. What is AWS KMS? How do envelope encryption and customer-managed keys work?
119. Explain AWS WAF and AWS Shield. How do you protect an API Gateway from DDoS and SQL injection?
120. What is AWS CloudFront? How do you invalidate the cache, and what is Origin Access Identity (OAI)?

**CI/CD & Infrastructure as Code (IaC):**
121. Design a complete CI/CD pipeline for a FastAPI microservice. Detail every stage from `git push` to production traffic.
122. What is Infrastructure as Code (IaC)? Why is Terraform preferred over clicking in the AWS Console?
123. Compare Terraform and AWS CloudFormation. What are the pros and cons of each?
124. How does Terraform manage state? Why is remote state (S3 + DynamoDB locking) critical for teams?
125. What are Terraform modules? How do you version and share them across an organization?
126. Explain deployment strategies: Rolling, Blue-Green, and Canary. Which one minimizes rollback time?
127. What is immutable infrastructure? How do tools like Packer and AMI baking fit into this?
128. How do you manage database migrations in a CI/CD pipeline? (e.g., Alembic/Flyway running before the new app code deploys).
129. What is GitOps? How do tools like ArgoCD or Flux differ from traditional push-based CI/CD (Jenkins/GitHub Actions)?
130. How do you handle secrets in a CI/CD pipeline? (GitHub Secrets, AWS Secrets Manager injection, HashiCorp Vault).

---

### 🌐 5. REST, HTTP, Microservices, FastAPI & Django (50+)
**HTTP, REST & API Design:**
131. What makes an HTTP method idempotent? Which methods are idempotent, and which are safe? Give examples.
132. Explain HTTP status codes deeply. When to use 201 vs 200? 401 vs 403? 429? 502 vs 503 vs 504?
133. What is HATEOAS? What is the Richardson Maturity Model? Is HATEOAS strictly necessary for modern REST?
134. How do you handle API versioning? Compare URI (`/v1/`), Header, and Query param versioning. Pros and cons?
135. Explain HTTP caching. How do `Cache-Control`, `ETag`, and `Last-Modified` headers work?
136. What is CORS? Explain the preflight `OPTIONS` request. How do you configure it in FastAPI/Django?
137. Compare REST, GraphQL, and gRPC. When would you strictly choose gRPC for internal microservices?
138. How do you implement pagination in REST? Compare Offset/Limit vs Cursor-based pagination. Why is cursor better for large datasets?
139. What is the difference between WebSockets and Server-Sent Events (SSE)? When do you use each for real-time data?
140. How do you secure a REST API? Explain OAuth2, JWT, API Keys, and mTLS.

**FastAPI (Deep Dive):**
141. How does FastAPI’s Dependency Injection (`Depends`) work under the hood? How does it resolve the dependency graph?
142. How do you use `yield` in a FastAPI dependency to handle setup and teardown (e.g., DB sessions)? What happens if an exception occurs?
143. How does Pydantic validate data? What is the difference between `model_validator` (root) and `field_validator`?
144. How do you handle background tasks in FastAPI? When is `BackgroundTasks` insufficient, and you need Celery/RabbitMQ?
145. How do you implement custom exception handlers and global middleware in FastAPI?
146. How does FastAPI generate the OpenAPI (Swagger) schema automatically? How do you customize it?
147. How do you handle WebSockets in FastAPI? How do you manage connection lifecycles and broadcast messages?
148. What is the performance difference between `async def` and `def` endpoints in FastAPI? How does the thread pool handle sync endpoints?
149. How do you implement rate limiting in FastAPI? (SlowAPI, Redis-based token bucket).
150. How do you test FastAPI applications? Explain `TestClient` vs `httpx.AsyncClient` for async testing.

**Django & Django REST Framework (DRF):**
151. Explain Django's MVT (Model-View-Template) architecture. How does it differ from standard MVC?
152. What are Django Signals? Why are they considered an anti-pattern by some, and what are the alternatives?
153. How does Django's ORM handle lazy evaluation? When does the actual SQL query hit the database?
154. Explain DRF Serializers. How do you handle nested serialization and writable nested relationships?
155. Compare DRF `APIView`, `GenericAPIView`, `ViewSet`, and `ModelViewSet`. When do you use which?
156. How do you optimize Django ORM queries? Explain `select_related` (JOIN) vs `prefetch_related` (separate query).
157. How do you integrate Celery with Django for async task processing?
158. What is Django middleware? How do you write custom middleware, and in what order does it execute?
159. How does Django handle CSRF protection? How do you exempt an API endpoint from it?
160. Explain Django's caching framework. How do you cache a specific view, a template fragment, or the entire site?

**Microservices & Distributed Systems:**
161. What is the Saga pattern? Compare Choreography (event-driven) vs Orchestration (central coordinator) for distributed transactions.
162. What is CQRS (Command Query Responsibility Segregation)? When do you separate read and write models?
163. What is Event Sourcing? How does it differ from standard CRUD, and how does it pair with CQRS?
164. What is the role of an API Gateway? How does it differ from a Load Balancer?
165. Explain the Circuit Breaker pattern. Why is it crucial in microservices to prevent cascading failures?
166. What is Service Discovery? How do tools like Consul, Eureka, or K8s DNS solve the problem of dynamic IPs?
167. How do you implement distributed tracing in microservices? (OpenTelemetry, Jaeger, Zipkin). What is a trace ID and span?
168. How do you handle idempotency in microservices? Explain idempotency keys in HTTP headers.
169. What is the Strangler Fig pattern? How do you use it to migrate a monolith to microservices safely?
170. How do you manage configuration across 50 microservices? (Centralized config servers, environment variables, feature flags).

---

### 🏗️ 6. Software Engineering Principles, Patterns & Testing (50+)
**Core Principles:**
171. Explain SOLID. Give a concrete Python code example of violating the Liskov Substitution Principle (LSP) and how to fix it.
172. Explain the Dependency Inversion Principle (DIP). How do interfaces/Protocols in Python enable it?
173. What is the difference between DRY and WET? When is "copy-pasting" actually better than abstracting? (Premature abstraction).
174. Explain KISS and YAGNI. How do they prevent over-engineering in a startup vs enterprise environment?
175. What is the Law of Demeter (Principle of Least Knowledge)? Give an example of violating it (e.g., `a.getB().getC().doSomething()`).
176. Explain "Composition over Inheritance". Why is deep inheritance trees harmful, and how do mixins/decorators solve it?
177. What is "Separation of Concerns"? How does it apply to separating business logic from framework code (e.g., FastAPI routes)?
178. Explain "Tell, Don't Ask". Why is it better to tell an object to do something rather than asking for its state and deciding externally?
179. What is the difference between high cohesion and low coupling? Why are they the ultimate goals of software design?
180. Explain the concept of "Idempotency" in software engineering beyond just HTTP. How does it apply to message queues and database writes?

**Design Patterns (Creational, Structural, Behavioral):**
181. How does the Factory Method differ from the Abstract Factory? When would you use the Builder pattern over a Factory?
182. Why is the Singleton pattern often considered an anti-pattern? How do you make it thread-safe in Python?
183. Explain the Prototype pattern. When is cloning an object better than creating a new instance from scratch?
184. Explain the Adapter pattern. How would you use it to integrate a legacy synchronous API into a modern async codebase?
185. How does the Facade pattern simplify complex subsystems? Give a real-world example (e.g., a unified payment facade).
186. How does the Structural Decorator pattern differ from Python’s `@decorator` syntax? When do you use the OOP Decorator?
187. Explain the Proxy pattern. How is it used for lazy loading, access control, or remote method invocation?
188. Explain the Composite pattern. How do you use it to treat individual objects and compositions of objects uniformly (e.g., file system trees)?
189. Explain the Strategy pattern. How do you implement it in Python using first-class functions instead of OOP interfaces?
190. Explain the Observer pattern. How is it implemented in modern Python (e.g., `asyncio` events, or custom event emitters)?
191. Explain the Command pattern. How does it enable undo/redo functionality and queuing of operations?
192. Explain the State pattern. How does it differ from using a massive `if/else` or `switch` block for state transitions?
193. What is the Template Method pattern? How does it enforce an algorithm skeleton while allowing subclasses to override specific steps?
194. Explain the Visitor pattern. When is it useful for double dispatch, and why is it rarely used in Python?
195. What is the Null Object pattern? How does it eliminate the need for `if obj is not None:` checks?

**Testing & Quality Assurance:**
196. What is the difference between Unit, Integration, and End-to-End (E2E) testing? What is the Testing Pyramid?
197. Explain the difference between Mocks, Stubs, and Fakes. When should you use `unittest.mock` vs a real test database?
198. What are pytest fixtures? Explain `scope` (function, class, module, session) and how `yield` is used for teardown.
199. What is TDD (Test-Driven Development)? Explain the Red-Green-Refactor cycle.
200. What is BDD (Behavior-Driven Development)? How do tools like `behave` or `pytest-bdd` use Gherkin syntax?
201. How do you test asynchronous code in pytest? (Explain `pytest-asyncio`).
202. What is code coverage? Why is 100% coverage not necessarily a sign of good tests? (Mutation testing).
203. What is Contract Testing (e.g., Pact)? Why is it critical for microservices to ensure API compatibility?
204. How do you test database interactions without hitting a real DB? (Explain `testcontainers` or in-memory SQLite).
205. What is property-based testing (e.g., `hypothesis`)? How does it differ from example-based testing?

---

### 🏢 7. Low-Level Design (LLD) - OOD & Component Design (50+)
**Object-Oriented Design (OOD) Scenarios:**
206. **Design a Parking Lot:** Handle multiple vehicle types, multiple floors, pricing strategies (hourly, flat rate, dynamic), and find the nearest available spot.
207. **Design a Library Management System:** Handle books, members, borrowing limits, fine calculations, book reservations, and waitlists.
208. **Design a Splitwise-like Expense App:** Handle adding expenses, splitting equally/unequally/by percentage, and simplifying debts (minimum transactions).
209. **Design a Snake & Ladder Game:** Handle the board, players, turns, dice rolling, move validation, and game state.
210. **Design a Chess Game:** Handle the board, pieces, valid moves, check/checkmate detection, and turn management.
211. **Design an Elevator System:** Handle multiple elevators, scheduling algorithms (SCAN/LOOK), and internal/external buttons.
212. **Design a Movie Ticket Booking System:** Handle theaters, screens, showtimes, seat selection, concurrency (preventing double booking), and payments.
213. **Design a Hotel Management System:** Handle rooms, booking, check-in/check-out, room service, and billing.
214. **Design an Amazon Shopping Cart:** Handle adding/removing items, updating quantities, applying coupons, and calculating totals.
215. **Design a Traffic Light Controller:** Handle intersections, light states (Red/Yellow/Green), timers, and pedestrian crossings.
216. **Design a Coffee Vending Machine:** Handle inventory, coin insertion, selection, dispensing, and returning change.
217. **Design a Pub/Sub Messaging System (OOD):** Define Topics, Publishers, Subscribers, and message delivery semantics (at-most-once, at-least-once).
218. **Design a Food Delivery Service (Swiggy/UberEats):** Handle restaurants, menus, orders, delivery agents, and real-time tracking.
219. **Design a Logistics/Shipping System:** Handle packages, routes, hubs, tracking statuses, and delivery estimates.
220. **Design a Digital Wallet (Paytm/Venmo):** Handle users, balances, transfers, transaction history, and concurrency (preventing negative balances).

**Component, Data Structure & Utility Design:**
221. **Design an LRU Cache:** Implement it from scratch using a Hash Map and a Doubly Linked List for O(1) get and put.
222. **Design an LFU Cache:** Implement it using Hash Maps and frequency buckets.
223. **Design a Rate Limiter:** Implement the Token Bucket, Leaky Bucket, and Sliding Window algorithms in memory.
224. **Design an In-Memory File System:** Implement `ls`, `mkdir`, `addContentToFile`, and `readContentFromFile` using a Trie/Tree.
225. **Design a URL Shortener (Backend logic):** How do you generate unique short IDs? (Base62, Zookeeper, DB auto-increment). Handle collisions.
226. **Design a Thread Pool:** Implement a custom thread pool from scratch using a queue and worker threads.
227. **Design a Task Scheduler:** Implement a system to run tasks at specific times or intervals (like `cron` or `celery beat`).
228. **Design a Bloom Filter:** Implement it for fast probabilistic set membership checks. How do you handle false positives?
229. **Design a Consistent Hashing Ring:** Implement it for distributed caching/load balancing. Handle node additions/removals and virtual nodes.
230. **Design a Key-Value Store:** Implement an in-memory KV store with TTL (Time-To-Live) expiration for keys.
231. **Design a Merge Sort / Quick Sort:** Implement them and explain their time/space complexity and stability.
232. **Design a Trie (Prefix Tree):** Implement it for autocomplete functionality.
233. **Design a Graph:** Implement Adjacency List and Adjacency Matrix. Write BFS and DFS traversals.
234. **Design a Singleton Database Connection Pool:** Ensure it is thread-safe and handles connection limits.
235. **Design a Circuit Breaker:** Implement the state machine (Closed, Open, Half-Open) with failure thresholds and timeouts.

**Mini-System / Architecture Design (LLD level):**
236. **Design a Logging Framework:** Handle different log levels, formatters, and multiple outputs (console, file, network).
237. **Design a Configuration Manager:** Handle loading configs from files/env vars, hot-reloading, and type validation.
238. **Design an Event Bus:** Implement a simple in-memory event emitter where components can subscribe to and publish events.
239. **Design a Dependency Injection Container:** Build a simple IoC container that resolves class dependencies automatically.
240. **Design a Middleware Pipeline:** Implement a system where HTTP requests pass through a chain of middleware functions (like FastAPI/Django).

---

### 🤖 8. GenAI, LLMs, LangChain/LangGraph & RAG (50+)
**LLM Fundamentals & Prompt Engineering:**
241. What are tokens in LLMs? How does tokenization work (BPE, WordPiece), and why does it matter for context limits and cost?
242. Explain the Transformer architecture briefly. What is the self-attention mechanism, and why is it better than RNNs?
243. What are Temperature, Top-p (nucleus sampling), and Top-k? How do they affect the randomness and creativity of LLM outputs?
244. What is the context window? How do techniques like RoPE (Rotary Position Embedding) or ALiBi allow for extended context?
245. What are LLM hallucinations? What are the root causes, and how do you mitigate them architecturally?
246. Explain Zero-shot, Few-shot, and Chain-of-Thought (CoT) prompting. When do you use each?
247. What is prompt injection? How do you secure an LLM application against direct and indirect prompt injections?
248. What is the difference between a base model and an instruct/chat model? How does RLHF (Reinforcement Learning from Human Feedback) work?
249. What are embeddings? How do you choose an embedding model (e.g., OpenAI `text-embedding-3` vs open-source `BGE`/`E5`)?
250. How do you calculate similarity between embeddings? Compare Cosine Similarity, Dot Product, and Euclidean Distance.

**RAG (Retrieval-Augmented Generation):**
251. Explain the end-to-end RAG pipeline. What are the ingestion, retrieval, and generation phases?
252. What are the common document chunking strategies? Compare fixed-size, recursive character, and semantic chunking.
253. How do you handle chunk overlap? Why is it necessary, and what are the trade-offs?
254. What is a Vector Database? Compare Pinecone, Milvus, Weaviate, and pgvector. When do you use a dedicated vector DB vs pgvector?
255. What is the difference between semantic search (vector) and keyword search (BM25)? What is hybrid search, and why is it better?
256. What is metadata filtering in RAG? How do you use it to restrict retrieval to specific documents, dates, or users?
257. What is query transformation/rewriting? How do techniques like HyDE (Hypothetical Document Embeddings) or Multi-Query improve retrieval?
258. What is reranking in RAG? Why do you use a cross-encoder (e.g., Cohere Rerank) after the initial vector retrieval?
259. How do you handle multi-modal RAG (extracting text from tables, charts, and images in PDFs)?
260. What is the "lost in the middle" problem in LLMs, and how does it affect RAG context stuffing?

**LangChain, LangGraph & Agents:**
261. What is LCEL (LangChain Expression Language)? How do Runnables, `invoke`, `batch`, and `stream` work?
262. What is the core difference between LangChain (linear chains) and LangGraph (state machines/graphs)? Why use LangGraph for complex agents?
263. In LangGraph, how do you define state? How do nodes and edges communicate, and how do you implement conditional edges?
264. How do you handle cyclic graphs in LangGraph? (e.g., an agent that needs to retry a tool call if it fails or asks for clarification).
265. What is Tool Calling (Function Calling) in LLMs? How does LangChain structure tool schemas and parse the LLM's tool invocation?
266. Explain the ReAct (Reason + Act) agent pattern. What are its limitations, and how does Plan-and-Execute differ?
267. How do you implement memory in LangChain/LangGraph? Compare ConversationBufferMemory, ConversationSummaryMemory, and vector-based memory.
268. What is LangSmith? How do you use it for tracing, debugging, and monitoring LLM applications in production?
269. How do you stream responses from an LLM in FastAPI using LangChain? (Explain `astream_events` and Server-Sent Events).
270. How do you handle rate limits and retries when calling external LLM APIs in LangChain?

**Human-in-the-Loop (HITL) & Evaluation:**
271. How do you implement HITL in an LLM agent? (e.g., pausing execution before executing a destructive tool like a database delete).
272. How does LangGraph handle state persistence (checkpointing) to allow a human to review and resume a paused graph execution?
273. Why can't we use traditional unit tests (exact string matching) for LLM outputs? What are the challenges of non-determinism?
274. Explain how DeepEval (or Ragas) evaluates LLMs. What does the "LLM-as-a-judge" paradigm mean?
275. What do the RAG evaluation metrics *Faithfulness*, *Answer Relevancy*, and *Contextual Precision/Recall* actually measure?
276. How do you evaluate an LLM agent's tool-calling accuracy? (Did it pick the right tool? Did it pass the right arguments?)
277. What are LLM Guardrails? How do you use tools like NeMo Guardrails or Guardrails AI to prevent toxic or off-topic outputs?
278. How do you handle PII (Personally Identifiable Information) in LLM inputs and outputs? (Detection, masking, and unmasking).
279. How do you evaluate the latency and cost of an LLM application in production? What metrics do you track?
280. What is dataset synthesis? How do you use an LLM to generate training or evaluation data for another LLM?

---

### 🔄 9. Cross-Domain, EPAM Scenarios & Troubleshooting (50+)
**Combined Architecture Scenarios (The "EPAM" Style):**
281. **Python + Docker:** Your Python FastAPI app works locally but crashes with `MemoryError` in Docker. How do you debug and fix it? (cgroups limits, swap, memory leaks).
282. **FastAPI + DB:** Your FastAPI endpoint takes 5 seconds to respond. Walk me through your exact debugging steps from the HTTP layer down to the DB.
283. **AWS + Microservices:** You have 5 microservices in ECS. Service A calls Service B, which calls Service C. Service C fails. How do you prevent Service A from timing out and crashing? (Circuit breakers, timeouts, fallbacks).
284. **GenAI + FastAPI:** You need to stream an LLM response to a React frontend. How do you architect this using FastAPI WebSockets or SSE, and LangChain?
285. **Docker + CI/CD:** Your Docker build takes 15 minutes in GitHub Actions. How do you reduce it to under 3 minutes? (Layer caching, BuildKit, registry mirroring).
286. **AWS + DB:** Your RDS Postgres database is experiencing high CPU and slow queries during a marketing flash sale. What do you do immediately, and what do you architect for next time?
287. **Python + GenAI:** Your RAG application is returning hallucinated answers. How do you debug the retrieval phase vs the generation phase?
288. **Microservices + CI/CD:** How do you deploy a change to a database schema and the microservice code that relies on it without downtime? (Expand/Contract pattern).
289. **Docker + AWS:** How do you securely pass AWS IAM credentials to a Docker container running in ECS without hardcoding them in the image? (Task Roles).
290. **FastAPI + Testing:** How do you write an integration test for a FastAPI endpoint that writes to a database and sends a message to RabbitMQ?

**Troubleshooting & Debugging War Stories:**
291. "The application is returning 502 Bad Gateway." What are the possible causes, and how do you trace it?
292. "The database is locked / deadlocked." How do you identify the culprit query and resolve it?
293. "The Python app's memory usage keeps growing until it gets OOMKilled." How do you find the memory leak? (tracemalloc, objgraph).
294. "The API is extremely slow, but CPU and Memory are low." What is the bottleneck? (I/O wait, network latency, thread pool exhaustion, DB connection pool).
295. "Users are complaining that the data on the dashboard is outdated." How do you debug caching issues or replication lag?
296. "The Docker container starts and immediately exits with code 137." What does this mean? (OOMKilled). How do you fix it?
297. "The CI/CD pipeline fails intermittently (flaky tests)." How do you identify and fix flaky tests in a distributed system?
298. "The LLM agent is stuck in an infinite loop calling the same tool." How do you debug and prevent this in LangGraph?
299. "The AWS Lambda function is timing out." It works locally. What are the common AWS-specific reasons? (VPC config, cold starts, missing IAM permissions).
300. "The microservice is dropping messages from the SQS queue." How do you debug visibility timeouts and dead-letter queues (DLQ)?

**EPAM / Service-Based Company Behavioral & Process:**
301. How do you handle a situation where a client requests a feature that you know is technically a bad idea or will cause technical debt?
302. Explain your process for onboarding to a massive legacy codebase (e.g., a 10-year-old Django monolith) with no documentation.
303. How do you conduct a code review? What do you look for beyond just "does it work"? (Security, performance, readability, testing).
304. Describe a time you had to explain a complex technical concept (like microservices or GenAI) to a non-technical stakeholder or client.
305. How do you estimate the effort for a task when the requirements are vague or constantly changing?
306. What is your approach to Agile/Scrum? How do you handle sprint planning and daily stand-ups effectively?
307. How do you mentor a junior developer who is struggling to understand a core concept (e.g., async Python or Docker)?
308. Describe a time you made a mistake that brought down a production service. How did you handle the incident, and what was the post-mortem?
309. How do you balance delivering features quickly for a client vs maintaining high code quality and writing tests?
310. What do you do when you are blocked by another team or a third-party API during a sprint?

**Advanced Cross-Domain & Future Tech:**
311. How do you implement distributed locking in a microservices architecture? (Redis/Redlock, Postgres advisory locks, Zookeeper).
312. Explain the Outbox pattern. How does it solve the dual-write problem between a database and a message queue?
313. What is GraphQL federation? How does it differ from a standard GraphQL gateway in a microservices setup?
314. How do you implement feature flags in a microservices architecture? (LaunchDarkly, Unleash). How do you handle flag cleanup?
315. What is eBPF? How is it changing observability and security in Kubernetes and cloud-native environments?
316. Explain WebAssembly (Wasm). How could it be used in backend microservices or edge computing (e.g., Cloudflare Workers)?
317. What is the difference between a Service Mesh (Istio/Linkerd) and an API Gateway? When do you need a Service Mesh?
318. How do you implement multi-tenancy in a SaaS application? (Database per tenant, schema per tenant, shared schema with tenant_id).
319. What is Chaos Engineering? How do you use tools like Chaos Monkey to test the resilience of your AWS infrastructure?
320. Explain the concept of "Shift-Left" in security and testing. How do you implement it in a modern CI/CD pipeline?

---

### 💡 Final Advice for the Next 48 Hours:
You have **320+ deep, combined, scenario-based questions** here. This is more than enough to cover 99% of what an EPAM interviewer will throw at you.

1. **Do not try to memorize all of them.** Use this as a syllabus.
2. **Focus on the "Combined" sections (Section 9 and the cross-domain questions in 1-8).** EPAM loves asking: *"How does X interact with Y?"* (e.g., FastAPI + Docker + AWS).
3. **For LLD (Section 7):** Pick 3 OOD scenarios (Parking Lot, Splitwise, Elevator) and 3 Component designs (LRU Cache, Rate Limiter, Thread Pool) and **code them from scratch** in your IDE.
4. **Verbal Practice:** Stand in front of a mirror and explain the architecture of a RAG pipeline (GenAI) and a Microservices Saga pattern (Backend) out loud. 

You are fully equipped. Go ace this review!