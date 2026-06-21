Here is your **100-Question GenAI, LLMs, LangChain, LangGraph & RAG Master Sheet**. 

Since you are interviewing as a **Backend/Python Developer**, this sheet is heavily skewed toward **Applied GenAI**. It focuses on how to build, orchestrate, evaluate, and deploy LLM applications in production using FastAPI, rather than the underlying math of transformer models.

As requested, **there are no answers here**. This is your pure study syllabus.

---

### 🧠 Category 1: LLM Fundamentals & Prompt Engineering (1-10)
*Focus: Understanding the raw building blocks of Large Language Models.*
1. What exactly is a "token" in the context of LLMs? How does tokenization (e.g., BPE, WordPiece) impact context limits and API costs?
2. Explain the difference between a "Base" model and an "Instruct/Chat" model. What is RLHF (Reinforcement Learning from Human Feedback)?
3. How do the `temperature`, `top_p` (nucleus sampling), and `top_k` parameters affect the output of an LLM? When would you set temperature to 0 vs 0.8?
4. What is the "Context Window" of an LLM? How do techniques like RoPE (Rotary Position Embedding) allow models to handle longer contexts?
5. What are LLM "hallucinations"? What are the architectural root causes, and how do you mitigate them without just saying "I will prompt it better"?
6. Explain Zero-shot, Few-shot, and Chain-of-Thought (CoT) prompting. When do you strictly use CoT over standard prompting?
7. What is Prompt Injection? Explain the difference between Direct Prompt Injection and Indirect Prompt Injection (e.g., via a retrieved document).
8. How do text embeddings work? What is the difference between dense embeddings (OpenAI) and sparse embeddings (BM25)?
9. How do you calculate the similarity between two embedding vectors? Compare Cosine Similarity, Dot Product, and Euclidean Distance.
10. What is the difference between a generative model (like GPT-4) and an embedding model (like `text-embedding-3-small`)? Why can't you use them interchangeably?

---

### 📚 Category 2: RAG (Retrieval-Augmented Generation) Architecture (11-25)
*Focus: Designing, optimizing, and debugging production-grade RAG pipelines.*
11. Walk me through the end-to-end RAG pipeline. What are the exact steps in the Ingestion, Retrieval, and Generation phases?
12. What are the common document chunking strategies? Compare fixed-size, recursive character, and semantic chunking.
13. How do you handle chunk overlap in RAG? Why is it necessary, and what are the performance trade-offs?
14. What is a Vector Database? Compare dedicated vector DBs (Pinecone, Milvus) with pgvector. When would you strictly choose pgvector?
15. What is "Hybrid Search"? Why is combining semantic search (vectors) with keyword search (BM25) drastically better than using vectors alone?
16. What is metadata filtering in RAG? How do you use it to restrict retrieval to specific users, dates, or document types?
17. What is Query Transformation/Rewriting? Explain how HyDE (Hypothetical Document Embeddings) or Multi-Query retrieval improves search results.
18. What is "Reranking" in RAG? Why do you use a Cross-Encoder (e.g., Cohere Rerank) after the initial vector retrieval, and what is the latency trade-off?
19. How do you handle multi-modal RAG? (e.g., extracting text, tables, and charts from complex PDF documents).
20. What is the "Lost in the Middle" problem in LLMs? How does it affect RAG when you stuff 20 retrieved chunks into the context window?
21. How do you handle a scenario where the retrieved context does not contain the answer? How do you force the LLM to say "I don't know" instead of hallucinating?
22. What is "Parent-Child" (or Small-to-Big) retrieval? How does it solve the problem of chunks being too small for context but too large for precise retrieval?
23. How do you evaluate the quality of your chunking strategy before even running the LLM?
24. What is the difference between a naive RAG pipeline and an Advanced/Modular RAG pipeline?
25. How do you handle versioning of your vector database when you update your embedding model or chunking strategy?

---

### 🔗 Category 3: LangChain & LCEL (LangChain Expression Language) (26-35)
*Focus: The foundational framework for chaining LLM components.*
26. What is LCEL (LangChain Expression Language)? How does the `|` (pipe) operator work under the hood?
27. What is a `Runnable` in LangChain? Explain the difference between `invoke`, `batch`, `stream`, and `ainvoke`.
28. How do you implement a simple sequential chain using LCEL? (e.g., Prompt -> LLM -> OutputParser).
29. What is the difference between `RunnablePassthrough` and `RunnableLambda`? When do you use each?
30. How does LangChain handle Tool Calling (Function Calling)? How does it structure the tool schemas and parse the LLM's JSON output?
31. What are the different types of Memory in LangChain? Compare `ConversationBufferMemory`, `ConversationSummaryMemory`, and `VectorStoreRetrieverMemory`.
32. How do you implement a custom Retriever in LangChain that wraps a proprietary internal search API?
33. How do you handle rate limits and automatic retries when calling external LLM APIs in LangChain?
34. What is the `RunnableParallel` primitive? How do you use it to fan out multiple retrievals or LLM calls concurrently?
35. How do you stream the output of an LCEL chain token-by-token to a frontend application?

---

### 🕸️ Category 4: LangGraph & Agentic Workflows (36-50)
*Focus: Moving from linear chains to stateful, cyclic, multi-agent systems.*
36. What is the fundamental difference between LangChain (linear chains) and LangGraph (state machines/graphs)? Why use LangGraph for complex agents?
37. In LangGraph, how do you define the `State`? What is the role of the `StateGraph` and the `TypedDict` or Pydantic model?
38. How do Nodes and Edges communicate in LangGraph? How do you update the state from within a node?
39. How do you implement Conditional Edges in LangGraph? (e.g., routing to a different node based on the LLM's output or a tool's success).
40. How do you handle cyclic graphs in LangGraph? Give an example of an agent that needs to retry a tool call if it fails or asks the user for clarification.
41. What is the ReAct (Reason + Act) agent pattern? How is it implemented in LangGraph compared to the legacy LangChain `create_react_agent`?
42. What is the difference between ReAct and Plan-and-Execute agents? When would you strictly use Plan-and-Execute?
43. How do you implement a Multi-Agent system in LangGraph? (e.g., a Supervisor agent delegating tasks to a Researcher agent and a Coder agent).
44. What is a "Subgraph" in LangGraph? How do you use it to modularize complex agent workflows?
45. How does LangGraph handle state persistence (Checkpointing)? What is the role of the `MemorySaver` or `SqliteSaver`?
46. How do you compile a LangGraph graph, and what is the purpose of the `checkpointer` argument during compilation?
47. What is the difference between `graph.invoke()` and `graph.stream()` in LangGraph? How does streaming work at the node level?
48. How do you pass runtime configuration (like a specific user ID or LLM model) to a LangGraph execution without hardcoding it in the state?
49. How do you handle infinite loops in a LangGraph agent? (e.g., setting a `recursion_limit`).
50. What is the "Command" primitive in LangGraph, and how does it simplify combining state updates with edge routing?

---

### 🛑 Category 5: Human-in-the-Loop (HITL) (51-60)
*Focus: Pausing, reviewing, and modifying agent execution in production.*
51. What is Human-in-the-Loop (HITL) in the context of LLM agents? Why is it critical for production deployments?
52. How do you implement HITL in LangGraph? Explain the `interrupt_before` and `interrupt_after` parameters when adding a node.
53. What happens to the graph execution when an interrupt is triggered? How is the state saved?
54. How does a human user actually "approve" or "reject" an action in a paused LangGraph? (Explain updating the state and calling `graph.invoke(None, config)`).
55. How do you implement a scenario where the human needs to *edit* the LLM's proposed tool arguments before execution?
56. What is "Time Travel" or "Debugging" in LangGraph? How do you use the checkpoint history to replay or branch off from a previous state?
57. How do you handle long-running HITL approvals? (e.g., the human takes 3 days to approve. How do you ensure the state isn't lost or timed out?)
58. How do you implement a "breakpoint" in LangGraph that pauses execution only if a specific condition is met (e.g., cost exceeds $5, or a destructive tool is called)?
59. How do you test HITL workflows in unit tests without actually requiring a human to click "approve"?
60. What are the security implications of HITL? How do you ensure that the human reviewing the state has the proper authorization to approve the action?

---

### 📊 Category 6: Evaluation, Observability & DeepEval (61-70)
*Focus: Proving your GenAI app actually works and doesn't just "look" like it works.*
61. Why can't we use traditional unit tests (exact string matching or regex) for LLM outputs? What are the challenges of non-determinism?
62. What is the "LLM-as-a-judge" paradigm? How do frameworks like DeepEval or Ragas use a secondary LLM to evaluate the primary LLM?
63. Explain the DeepEval metric **Faithfulness**. What exactly does it measure, and how does it prevent hallucinations?
64. Explain the DeepEval metric **Answer Relevancy**. How does it ensure the LLM is actually answering the user's prompt?
65. Explain the DeepEval metrics **Contextual Precision** and **Contextual Recall**. How do they evaluate the retrieval phase of a RAG pipeline?
66. How do you evaluate an LLM agent's Tool Calling accuracy? (Did it pick the right tool? Did it pass the correct arguments based on the schema?)
67. What is "Hallucination" evaluation in DeepEval, and how does it differ from "Faithfulness"?
68. How do you create an evaluation dataset for your RAG pipeline? What is "Dataset Synthesis" using LLMs?
69. How do you track latency, token usage, and cost in a production GenAI application? What tools do you use (LangSmith, Arize Phoenix, OpenLLMetry)?
70. How do you implement automated regression testing for your LLM prompts? (e.g., ensuring a prompt tweak didn't degrade the Faithfulness score by 10%).

---

### ⚡ Category 7: Backend Integration (FastAPI + GenAI) (71-85)
*Focus: The intersection of your Python backend code and the AI models.*
71. How do you stream an LLM response from a FastAPI backend to a React frontend? Compare using WebSockets vs. Server-Sent Events (SSE).
72. How do you implement SSE in FastAPI using LangChain's `astream_events` or `astream_tokens`?
73. What happens if you call a synchronous LLM API (like the standard OpenAI Python client) inside an `async def` FastAPI endpoint? How do you fix it?
74. How do you handle background tasks in a GenAI FastAPI app? When is `BackgroundTasks` insufficient, and you *must* use Celery/ARQ/RabbitMQ?
75. How do you implement caching for LLM responses in FastAPI? (e.g., caching exact prompt matches in Redis to save API costs).
76. How do you manage connection pooling for your Vector Database (e.g., pgvector, Pinecone) in a FastAPI application using Dependency Injection?
77. How do you handle rate limiting from the LLM provider (e.g., OpenAI 429 errors) at the FastAPI middleware level?
78. How do you secure a GenAI FastAPI endpoint? (e.g., ensuring User A cannot query the Vector DB and retrieve User B's private documents).
79. How do you implement asynchronous batch processing for document ingestion in FastAPI? (e.g., user uploads a 500-page PDF).
80. How do you handle graceful shutdowns in a FastAPI GenAI app? (e.g., ensuring in-flight LLM streams or vector DB inserts are completed or safely rolled back when receiving SIGTERM).
81. What is the difference between `httpx` (async) and `requests` (sync) when calling external LLM APIs in FastAPI?
82. How do you structure your FastAPI project to separate the HTTP routing layer from the complex LangGraph/LangChain orchestration layer?
83. How do you handle file uploads (PDFs, CSVs) in FastAPI for RAG ingestion, and how do you pass them to the processing pipeline?
84. How do you implement API versioning for a GenAI endpoint when you upgrade from GPT-3.5 to GPT-4o, which might change the output format?
85. How do you write integration tests for a FastAPI GenAI endpoint without actually calling the OpenAI API and incurring costs? (Mocking LLMs).

---

### 🛡️ Category 8: Security, Guardrails & Production Scenarios (86-100)
*Focus: Keeping the AI safe, compliant, and running smoothly in the real world.*
86. What are LLM Guardrails? How do you use tools like NeMo Guardrails or Guardrails AI to prevent toxic, biased, or off-topic outputs?
87. How do you handle PII (Personally Identifiable Information) in LLM inputs and outputs? Explain the architecture for PII detection, masking, and unmasking.
88. Your RAG application is returning highly hallucinated answers. Walk me through your exact debugging process to determine if it's a Retrieval failure or a Generation failure.
89. Your LangGraph agent is stuck in an infinite loop, repeatedly calling the same tool and burning through API credits. How do you detect, prevent, and fix this?
90. How do you implement "Shadow Testing" or "A/B Testing" for a new LLM prompt in production without affecting live users?
91. What is the "Out-of-Memory" (OOM) risk when loading large embedding models or running local LLMs (like Llama 3) in a Docker container? How do you mitigate it?
92. How do you ensure compliance with data privacy laws (GDPR/CCPA) when sending user data to third-party LLM APIs? (Zero-retention APIs, local deployments).
93. Your vector database is returning irrelevant chunks because the user's query is too short or vague (e.g., "tell me about it"). How do you fix this at the query level?
94. How do you handle the "Cold Start" problem for a GenAI application deployed on AWS Lambda or Serverless containers?
95. What is the difference between fine-tuning an LLM and using RAG? When would you strictly choose to fine-tune (e.g., LoRA/QLoRA) instead of just improving the RAG prompt?
96. How do you monitor the "drift" of an LLM application in production? (e.g., the model provider silently updates the base model, changing the output style).
97. How do you implement a "Fallback" mechanism in LangChain/LangGraph if the primary LLM (e.g., GPT-4) goes down or times out?
98. What is the impact of JSON mode / Structured Outputs in modern LLMs? How do you enforce strict Pydantic schema validation on LLM outputs?
99. How do you optimize the cost of a GenAI application that processes 10,000 documents a day? (Routing, caching, using smaller models for simple tasks).
100. **The Ultimate Scenario:** A client complains that your RAG chatbot is "too slow" (taking 15 seconds to reply) and "sometimes makes things up." Walk me through your exact architectural changes to reduce latency to < 3 seconds and eliminate hallucinations.

---

### 💡 How to conquer GenAI for your EPAM Interview:

1. **The "Backend" Advantage:** Most GenAI candidates are data scientists who struggle with productionization. **You are a backend developer.** Lean into Categories 7 and 8. When they ask about RAG, talk about *FastAPI streaming, Redis caching, async vector DB connections, and Docker memory limits*. That will blow them away.
2. **LangChain vs. LangGraph:** This is the #1 most asked framework question right now. 
   * *Your answer:* "LangChain/LCEL is for deterministic, linear, or simple branching pipelines. LangGraph is for non-deterministic, cyclic, stateful agents where the LLM needs to loop, use tools, recover from errors, and require Human-in-the-Loop approvals."
3. **DeepEval Metrics:** Memorize the big three: **Faithfulness** (Is the answer grounded in the context? Prevents hallucinations), **Answer Relevancy** (Does it answer the prompt?), and **Contextual Precision/Recall** (Did we retrieve the right chunks?). 
4. **The "I don't know, but..." Rule:** GenAI moves incredibly fast. If they ask about a brand new LangGraph feature released yesterday, say: *"I haven't used that specific new primitive yet, but based on how LangGraph handles state and checkpointing, I would assume it works by..."*

You now have the complete, exhaustive blueprint for **Python, Databases, Docker, Design Principles, APIs/Microservices, AWS/CI-CD, and GenAI**. 

You are 100% equipped for this review. Get some sleep, review your weak spots, and go ace this interview!