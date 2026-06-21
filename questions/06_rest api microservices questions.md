Here is your **100-Question REST API, Microservices, FastAPI & Django Master Sheet**. 

As requested, I have dedicated **two massive, highly detailed sections** specifically to FastAPI and Django/DRF, diving deep into their internals, async behaviors, and framework-specific "bouncer" questions. 

As always, **there are no answers here**. This is your pure study syllabus.

---

### 🌐 Category 1: REST API, HTTP & API Design Fundamentals (1-15)
*Focus: Deep understanding of the HTTP protocol and true RESTful design.*
1. What exactly makes an HTTP method "safe" and/or "idempotent"? Map GET, POST, PUT, PATCH, and DELETE to these properties.
2. What is the difference between `PUT` and `PATCH`? If `PATCH` is not idempotent, how do you implement it to be idempotent?
3. Explain HTTP Content Negotiation. How do the `Accept`, `Accept-Charset`, and `Content-Type` headers work together?
4. What is HATEOAS? Is it strictly necessary for a modern REST API, and what are the practical drawbacks of implementing it?
5. Explain the Richardson Maturity Model. What level are most modern "REST" APIs actually at?
6. How do you handle API versioning? Compare URI versioning (`/v1/`), Header versioning, and Media Type versioning. Which is best for public vs. internal APIs?
7. What is the difference between HTTP caching using `ETag`/`If-None-Match` vs `Last-Modified`/`If-Modified-Since`?
8. Explain the `Cache-Control` directives: `no-store`, `no-cache`, `max-age`, and `s-maxage`. How do CDNs interpret them differently than browsers?
9. What is CORS (Cross-Origin Resource Sharing)? Explain the exact flow of a "preflight" `OPTIONS` request.
10. What is the difference between WebSockets and Server-Sent Events (SSE)? When would you strictly choose SSE over WebSockets for an API?
11. How do you implement cursor-based pagination vs offset/limit pagination? Why is cursor-based strictly better for high-traffic, constantly updating datasets?
12. What are HTTP Trailer headers? How are they used in chunked transfer encoding?
13. How do you handle partial successes in a batch API request? (e.g., sending 10 items, 5 succeed, 5 fail).
14. What is the difference between a 401 Unauthorized and a 403 Forbidden? When do you use 429 Too Many Requests vs 503 Service Unavailable?
15. How do you design an API to handle long-running processes? (Explain the Asynchronous Request-Reply pattern using 202 Accepted and a status endpoint).

---

### 🏗️ Category 2: Microservices Architecture & Distributed Systems (16-35)
*Focus: Designing, connecting, and maintaining distributed backend systems.*
16. What is the fundamental difference between a Monolith, a Service-Oriented Architecture (SOA), and Microservices?
17. What is the role of an API Gateway? How does it differ from a standard Load Balancer or a Reverse Proxy (like Nginx)?
18. Explain the **Saga Pattern** for distributed transactions. What is the difference between Choreography (event-driven) and Orchestration (command-driven)?
19. What is the **Outbox Pattern**? How does it solve the "dual-write problem" between a relational database and a message broker (like Kafka/RabbitMQ)?
20. Explain **CQRS** (Command Query Responsibility Segregation). When does separating the read and write models drastically improve system performance?
21. What is **Event Sourcing**? How does it pair with CQRS, and what are the debugging challenges associated with it?
22. What is the **Circuit Breaker pattern**? Explain the states (Closed, Open, Half-Open) and how it prevents cascading failures in microservices.
23. How do microservices discover each other? Compare Client-side discovery (e.g., Netflix Eureka) vs. Server-side discovery (e.g., AWS ALB, K8s DNS).
24. What is Distributed Tracing? How do concepts like Trace ID, Span ID, and tools like Jaeger/OpenTelemetry help debug a request across 5 microservices?
25. How do you implement **Idempotency** in a microservices architecture? Explain the use of Idempotency Keys in HTTP headers.
26. What is the **Strangler Fig pattern**? How do you use it to safely migrate a legacy monolith to microservices without a "big bang" rewrite?
27. How do you handle distributed configuration management across 50 microservices? (Config servers, feature flags, environment variables).
28. What is the difference between synchronous communication (REST/gRPC) and asynchronous communication (Message Queues/Event Buses)? When do you use which?
29. How do you secure inter-service communication in a microservices architecture? (mTLS, JWT propagation, API Gateways).
30. What is the "Database per Service" pattern? What are the massive challenges it introduces regarding joins and reporting?
31. How do you implement a distributed lock in a microservices environment? (Redis/Redlock, Postgres advisory locks, Zookeeper).
32. What is the difference between a "Smart Endpoint, Dumb Pipe" and a "Dumb Endpoint, Smart Pipe" architecture? Which one do Microservices favor?
33. How do you handle schema evolution and backward/forward compatibility in microservice APIs? (Explain Protobuf rules, API versioning).
34. What is Contract Testing (e.g., using Pact)? Why is it critical for microservices compared to traditional integration testing?
35. How do you deploy microservices without downtime? Explain Blue-Green, Canary, and Rolling deployments.

---

### ⚡ Category 3: FastAPI Deep Dive (Dedicated Section) (36-60)
*Focus: Internals, async behavior, Pydantic, and advanced framework features.*

**Core & Async Internals:**
36. How does FastAPI handle `async def` endpoints vs standard `def` endpoints under the hood? (Explain the ASGI server, event loop, and threadpool).
37. What happens if you call a blocking synchronous function (like `time.sleep()` or a synchronous DB query) inside an `async def` FastAPI endpoint? How do you fix it?
38. How does FastAPI achieve its high performance? Compare it to Flask and Django in terms of routing and request parsing.
39. What is the role of Starlette in FastAPI? What specific features does Starlette provide that FastAPI builds upon?
40. How do you run FastAPI in production? Explain the relationship between Uvicorn (ASGI server), Gunicorn (Process manager), and Uvicorn workers.

**Dependency Injection (DI) & Pydantic:**
41. How does FastAPI’s `Depends()` system resolve the dependency graph? How does it handle caching of dependencies within a single request?
42. How do you use `yield` in a FastAPI dependency to handle setup and teardown (e.g., database sessions)? What happens to the teardown code if the endpoint raises an exception?
43. How do you override dependencies in FastAPI for testing purposes? (`app.dependency_overrides`).
44. In Pydantic V2, what is the difference between `@model_validator` (root) and `@field_validator`? When do you use `mode='before'` vs `mode='after'`?
45. What is the difference between a Pydantic `BaseModel` and a `TypeAdapter`? When would you strictly use `TypeAdapter`?
46. How does Pydantic handle serialization and deserialization performance in V2 compared to V1? (Hint: Rust core).
47. How do you implement custom root models in Pydantic V2? (e.g., validating a direct list or dict instead of an object).

**Advanced Features & Middleware:**
48. How do `BackgroundTasks` work in FastAPI? When are they insufficient, and you *must* use a distributed task queue like Celery or ARQ?
49. How do you implement and stream Server-Sent Events (SSE) or WebSockets in FastAPI? How do you handle connection drops?
50. What is the execution order of Middleware in FastAPI? How do you write a custom middleware to measure request execution time?
51. How do you implement global exception handling in FastAPI? How do you override the default `RequestValidationError` handler?
52. How does FastAPI generate the OpenAPI (Swagger) schema automatically? How do you customize the schema for specific models or hide certain endpoints?
53. How do you implement rate limiting in FastAPI? (Explain `slowapi` or custom Redis-based token bucket middleware).
54. How do you handle CORS in FastAPI? What are the security implications of setting `allow_origins=["*"]` with `allow_credentials=True`?
55. How do you implement OAuth2 with JWT (JSON Web Tokens) in FastAPI? Explain the `OAuth2PasswordBearer` flow.

**Testing & Production Readiness:**
56. How do you test asynchronous FastAPI endpoints? Compare `TestClient` (synchronous) vs `httpx.AsyncClient` (asynchronous).
57. How do you mock a database dependency in a FastAPI test without hitting a real database?
58. How do you handle graceful shutdowns in FastAPI? (e.g., closing DB connections or flushing background tasks when receiving a SIGTERM).
59. How do you optimize a FastAPI application for high concurrency? (Connection pooling, async DB drivers like `asyncpg`, avoiding blocking calls).
60. What are the common security best practices when deploying a FastAPI app? (HTTPS, hiding server headers, validating all inputs, preventing path traversal).

---

### 🎸 Category 4: Django & Django REST Framework (DRF) Deep Dive (Dedicated Section) (61-85)
*Focus: ORM optimization, MVT lifecycle, DRF internals, and scaling Django.*

**Core Django & ORM:**
61. Explain the Django Request/Response lifecycle. At what exact stages do Middleware, URL routing, Views, and Templates interact?
62. What is the Django ORM's "Lazy Evaluation"? At what exact moments does the ORM hit the database to execute the SQL query?
63. Explain the N+1 query problem in Django. How do `select_related()` (SQL JOIN) and `prefetch_related()` (Python-level join) solve it? When do you strictly use one over the other?
64. What are Django Signals (`pre_save`, `post_save`, etc.)? Why are they often considered an anti-pattern in large codebases, and what are the alternatives?
65. How does Django handle database transactions by default in a view? How do you use `transaction.atomic()` and `select_for_update()` to prevent race conditions?
66. What is the difference between `django.db.models.Q` objects and `F` expressions? Give a scenario where an `F` expression prevents a race condition.
67. How do you implement a Custom User Model in Django? Why is it highly recommended to do this at the very beginning of a project?
68. What is the difference between Django's `TestCase` and `TransactionTestCase`? Why is `TestCase` much faster?
69. How does Django's caching framework work? Explain the difference between per-site, per-view, and low-level (template fragment) caching.
70. How do you write custom Django Middleware? Explain the difference between the old-style (pre-1.10) and new-style (`__init__` and `__call__`) middleware.

**Django REST Framework (DRF) Internals:**
71. Explain the DRF request lifecycle. How does the `APIView` initialize the request, perform authentication, check permissions, and handle content negotiation?
72. What is the difference between `APIView`, `GenericAPIView`, `ViewSet`, and `ModelViewSet`? When should you drop down to a basic `APIView`?
73. How do DRF Serializers work under the hood? How do you handle **writable nested relationships** (e.g., creating a User and their Profile in one POST request)?
74. What is the difference between `SerializerMethodField` and a standard `SerializerMethod`? Why is `SerializerMethodField` potentially dangerous for performance (N+1)?
75. How do you implement custom Pagination, Filtering, and Ordering classes in DRF? 
76. How does DRF handle Throttling (Rate Limiting)? Explain the difference between `AnonRateThrottle`, `UserRateThrottle`, and custom scoped throttles.
77. How do you implement complex, multi-field validation in a DRF Serializer? (Explain `validate()` vs `validate_<field_name>()`).
78. What are DRF Routers? How do `DefaultRouter` and `SimpleRouter` automatically generate URL patterns for ViewSets?
79. How do you handle file uploads (images/documents) in DRF? How do you integrate it with cloud storage like AWS S3 (using `django-storages`)?
80. How do you implement token-based authentication vs session-based authentication in DRF? When do you use JWTs (e.g., `djangorestframework-simplejwt`)?

**Advanced Django & Scaling:**
81. How do you integrate Celery with Django for asynchronous task processing? How do you handle task retries and dead-letter queues?
82. What is Django Database Routing? How do you use it to implement Read/Write splitting (sending reads to replicas and writes to the primary)?
83. How do you optimize a Django application that is experiencing high memory usage per worker? (Hint: `CONN_MAX_AGE`, iterator(), avoiding large querysets in memory).
84. How do you handle zero-downtime database migrations in Django? (Explain the Expand and Contract pattern, e.g., adding a nullable column, backfilling, then making it required).
85. What are the best practices for securing a Django application in production? (Secret key management, CSRF, XSS, Clickjacking, `SECURE_HSTS_SECONDS`).

---

### 🛡️ Category 5: API Security, Testing & Production Readiness (86-100)
*Focus: Keeping the API secure, tested, and running smoothly under load.*
86. Explain the OAuth2 flow. What is the difference between the Authorization Code flow, Client Credentials flow, and Implicit flow?
87. How do JSON Web Tokens (JWT) work? What is the difference between the Header, Payload, and Signature? Why shouldn't you store sensitive data in the payload?
88. How do you securely store JWTs on the client side? Compare LocalStorage (XSS vulnerable) vs HttpOnly Cookies (CSRF vulnerable) and how to mitigate those risks.
89. What is API Key authentication? When is it appropriate to use API keys instead of OAuth2/JWT?
90. How do you prevent SQL Injection, NoSQL Injection, and Command Injection in your backend APIs?
91. What is Mass Assignment (or Over-posting) vulnerability? How do frameworks like FastAPI (Pydantic) and DRF (Serializers) prevent it?
92. How do you implement automated API testing? Explain the Testing Pyramid for APIs (Unit vs Integration vs Contract vs E2E).
93. How do you load test an API? What tools do you use (Locust, JMeter, k6), and what metrics do you measure (Throughput, Latency, P99)?
94. What is API Mocking? How do tools like WireMock or Postman Mock Servers help frontend and backend teams work in parallel?
95. How do you handle API deprecation? What is the standard process for notifying clients and sunsetting an old API version?
96. What is an API Gateway? How does it handle rate limiting, authentication termination, and request transformation before the request hits the microservices?
97. How do you implement request validation at the edge (API Gateway) vs at the application level (FastAPI/Django)?
98. What is GraphQL? How does it differ from REST, and what is the "N+1 problem" in GraphQL resolvers?
99. How do you design an API for a mobile application vs a web application? (Considerations for payload size, batching, and offline capabilities).
100. If your API suddenly starts returning 500 Internal Server Errors at a rate of 100 per second, what is your exact step-by-step debugging process?

---

### 💡 How to conquer this for your EPAM Interview:

1. **The Framework Showdown:** Interviewers *love* to ask: *"When would you choose FastAPI over Django, and vice versa?"* 
   * *Your answer should be:* "Django is a 'batteries-included' monolith, perfect for rapid development, content-heavy sites, and when you need a built-in Admin panel, ORM, and Auth out of the box. FastAPI is a micro-framework built for high performance, async I/O, and building microservices or ML model APIs where speed, automatic OpenAPI docs, and strict data validation (Pydantic) are the top priorities."
2. **FastAPI Async Bouncers:** Make sure you deeply understand **Question 37**. If you put `requests.get()` (sync) inside an `async def` endpoint in FastAPI, it blocks the *entire event loop*, freezing all other concurrent requests. You must use `httpx` (async) or run it in a threadpool using `run_in_executor`.
3. **Django ORM Bouncers:** Master **Question 63**. Know exactly when to use `select_related` (Foreign Keys, One-to-One -> uses SQL `JOIN`) vs `prefetch_related` (Many-to-Many, Reverse Foreign Keys -> uses separate SQL queries and joins them in Python memory).
4. **Microservices Reality Check:** Don't just praise microservices. Be ready to answer **Question 16 & 30** by highlighting the *drawbacks*: distributed transactions are hard, debugging is a nightmare without distributed tracing, and "database per service" makes reporting incredibly complex.

You have the ultimate Backend & API syllabus. Go crush this! Let me know if you are ready for the AWS/Cloud or GenAI/LLM sections next.