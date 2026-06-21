Here is the final piece of your master preparation blueprint. Since you have a **Live Coding** and **Verbal Q&A** format for a **Junior role at EPAM**, this section focuses heavily on **Low-Level Design (Machine Coding)**, **Pattern-based DSA**, **Basic High-Level Design**, and **Behavioral/Execution Strategy**.

As always, **there are no answers here**. This is your actionable syllabus.

---

### 🏗️ Part 1: Low-Level Design (LLD) / Machine Coding
*Focus: Translating vague requirements into clean, extensible, Object-Oriented Python code. Interviewers will evaluate your use of SOLID principles, Design Patterns, and clean code practices.*

**Classic OOD Scenarios (Write the classes, interfaces, and core logic):**
1. **Design a Parking Lot:** Handle multiple vehicle types (Car, Bike, Truck), multiple floors, different parking spot sizes, dynamic pricing strategies, and finding the nearest available spot. *(Focus: Factory pattern for vehicles, Strategy pattern for pricing).*
2. **Design Splitwise (Expense Sharing):** Handle adding expenses, splitting equally/unequally/by percentage, and the core algorithm to "simplify debts" (minimize the number of transactions between users). *(Focus: Graph/Heap for debt simplification).*
3. **Design an Elevator System:** Handle multiple elevators, internal/external buttons, and implement a scheduling algorithm (like SCAN or LOOK) to optimize wait times. *(Focus: State pattern for elevator states, Observer pattern for buttons).*
4. **Design a Movie Ticket Booking System (BookMyShow):** Handle theaters, screens, showtimes, and the critical concurrency problem of two users trying to book the exact same seat at the exact same time. *(Focus: Pessimistic/Optimistic locking concepts, Singleton for theater management).*
5. **Design a Library Management System:** Handle books, members, borrowing limits, fine calculations, and book reservations/waitlists. *(Focus: Command pattern for issuing/returning books).*
6. **Design a Snake & Ladder / Chess Game:** Handle the board, players, turns, dice rolling/move validation, and game state. *(Focus: Strategy pattern for different piece movements or game rules).*

**Component & Data Structure Design (Write the actual data structures from scratch):**
7. **Design an LRU (Least Recently Used) Cache:** Implement it to achieve O(1) time complexity for both `get()` and `put()` operations. *(Hint: Hash Map + Doubly Linked List, or use `collections.OrderedDict`).*
8. **Design a Rate Limiter:** Implement the Token Bucket or Sliding Window algorithm in memory to restrict API calls.
9. **Design an In-Memory File System:** Implement functions like `ls`, `mkdir`, `addContentToFile`, and `readContentFromFile`. *(Hint: Trie or N-ary Tree).*
10. **Design a Pub/Sub Message Broker:** Create an in-memory system where publishers can send messages to topics, and subscribers can subscribe to topics and receive messages asynchronously.
11. **Design a Thread Pool / Task Queue:** Implement a custom thread pool from scratch using a queue and worker threads to execute async/sync tasks.
12. **Design a URL Shortener (Backend Logic):** How do you generate unique, short, non-colliding IDs? *(Hint: Base62 encoding, Zookeeper, or DB auto-increment).*

**💡 LLD Evaluation Criteria (What they look for):**
*   Did you use `abc.ABC` and `@abstractmethod` for interfaces?
*   Did you use `Enum` for fixed states (e.g., `VehicleType.CAR`)?
*   Did you use `@dataclass` for simple data carriers?
*   Is your code modular, or is it one giant 500-line script?
*   Did you handle edge cases and raise custom exceptions?

---

### 🧮 Part 2: Data Structures & Algorithms (DSA) for Live Coding
*Focus: LeetCode Easy to Medium. Since it's Python, you must know the "Pythonic" shortcuts for DSA (e.g., `heapq`, `deque`, `defaultdict`). Do not memorize code; memorize the **patterns**.*

**Pattern 1: Arrays & Strings (Two Pointers & Sliding Window)**
13. **Two Sum / 3Sum:** Find pairs/triplets that add up to a target. *(Hash Map vs Two Pointers).*
14. **Longest Substring Without Repeating Characters:** Classic sliding window.
15. **Product of Array Except Self:** Solve it in O(N) without using the division operator. *(Prefix and Suffix products).*
16. **Move Zeroes / Remove Duplicates:** In-place array manipulation.
17. **Valid Anagram / Group Anagrams:** Using character frequency arrays or Hash Maps.

**Pattern 2: Hash Maps & Sets (Frequency & Grouping)**
18. **Top K Frequent Elements:** Using Hash Map + Min-Heap (`heapq`).
19. **Find the Duplicate Number:** Floyd’s Tortoise and Hare (Cycle detection in an array).
20. **Subarray Sum Equals K:** Using Prefix Sum + Hash Map.

**Pattern 3: Linked Lists (Fast/Slow Pointers & Reversal)**
21. **Reverse a Linked List:** Iterative and Recursive approaches.
22. **Detect Cycle in a Linked List:** Floyd’s Cycle-Finding Algorithm.
23. **Merge Two Sorted Lists:** Standard pointer manipulation.
24. **Remove N-th Node From End of List:** Using the two-pointer gap technique.

**Pattern 4: Stacks & Queues (Monotonic & Validation)**
25. **Valid Parentheses:** Classic stack problem.
26. **Min Stack:** Design a stack that supports `push`, `pop`, `top`, and retrieving the minimum element in O(1) time.
27. **Daily Temperatures:** Monotonic decreasing stack to find the next greater element.

**Pattern 5: Trees & Graphs (BFS & DFS Basics)**
28. **Maximum Depth of Binary Tree:** Simple DFS.
29. **Invert Binary Tree:** Classic recursion.
30. **Number of Islands:** Grid traversal using BFS/DFS.
31. **Clone Graph:** Deep copy of a graph using Hash Map + DFS.
32. **Course Schedule:** Detecting cycles in a directed graph (Topological Sort / Kahn's Algorithm).

**🐍 Python DSA "Cheat Codes" you MUST know:**
*   **Heaps:** `import heapq`. Know `heapq.heappush()`, `heapq.heappop()`, and `heapq.heapify()`. (Python only has Min-Heaps; to use it as a Max-Heap, multiply values by -1).
*   **Queues:** `from collections import deque`. Never use `list.pop(0)` for queues (it's O(N)). Always use `deque.popleft()` (it's O(1)).
*   **Hash Maps:** `from collections import defaultdict`. Know how to initialize it with `int`, `list`, or `set`.
*   **Sorting:** Know how to use the `key` argument in `sorted()` or `.sort()` (e.g., `sorted(items, key=lambda x: x[1])`).

---

### 🌐 Part 3: High-Level Design (HLD) Basics (Verbal)
*Focus: For a junior role, they won't ask you to "Design Netflix". They will ask conceptual questions to see if you understand how backend systems scale.*

33. What is the difference between a Load Balancer (Layer 4 vs Layer 7) and an API Gateway?
34. Explain the difference between Horizontal Scaling and Vertical Scaling. When do you hit the limit of Vertical Scaling?
35. What is a Reverse Proxy (like Nginx)? How does it differ from a Forward Proxy?
36. How does a Message Queue (RabbitMQ/Kafka) decouple microservices? What is the difference between a Queue (Point-to-Point) and a Topic (Pub/Sub)?
37. Explain the "Database per Service" pattern in microservices. What is the biggest drawback of this pattern?
38. How do you scale a relational database when it can no longer handle the write traffic? (Sharding, Read Replicas).
39. What is the difference between a Stateful and a Stateless application? Why do we prefer Stateless apps in cloud environments?
40. How does a CDN (Content Delivery Network) like CloudFront work, and what is "Cache Invalidation"?

---

### 🗣️ Part 4: Behavioral, Agile & "EPAM" Scenarios
*Focus: Service-based companies heavily weight cultural fit, client handling, and adaptability. Use the **STAR method** (Situation, Task, Action, Result) for these.*

41. **Client Management:** "A client requests a feature that you know is technically a bad idea and will create massive technical debt. How do you handle this?"
42. **Vague Requirements:** "You are assigned a task, but the requirements document is missing or very vague. The client is unavailable. What do you do?"
43. **Legacy Code:** "You are onboarded to a 10-year-old Django monolith with zero documentation and no tests. What is your step-by-step approach to understanding it and making your first change safely?"
44. **Production Incident:** "You deploy a feature on Friday evening. On Saturday morning, you get a P1 alert that the production database is down. Walk me through your immediate actions."
45. **Code Reviews:** "A senior developer rejects your Pull Request and asks you to rewrite a large chunk of it, but you disagree with their approach. How do you resolve this?"
46. **Agile/Scrum:** "During the daily stand-up, you realize you are going to miss the sprint deadline because of an unexpected technical blocker. How and when do you communicate this?"
47. **Mentorship:** "How would you explain the concept of 'Asyncio' or 'Docker Containers' to a non-technical project manager?"
48. **Continuous Learning:** "The GenAI / LLM space changes every week. How do you keep yourself updated without getting overwhelmed?"

---

### 🎯 Part 5: The "Secret Sauce" - Live Coding Execution Strategy
*Focus: How you behave during the coding test is often more important than whether you get the perfect optimal solution. Follow this exact framework.*

**Step 1: Clarify (2-3 minutes)**
*   *Never start coding immediately.*
*   Repeat the question back to them.
*   Ask about edge cases: *"Should I handle empty inputs?", "Will the array contain negative numbers?", "Is the input already sorted?"*
*   Confirm the expected input/output format.

**Step 2: Brute Force & Optimize (2-3 minutes)**
*   State the brute force approach out loud: *"The naive way is to use two nested loops, which is O(N^2) time."*
*   Propose the optimization: *"We can optimize this to O(N) time by using a Hash Map to store the complements."*
*   **Crucial:** Ask the interviewer: *"Does that sound good, or would you prefer I start with the brute force?"* (They will almost always say "Go for the optimal one").

**Step 3: Think Out Loud While Coding (10-15 minutes)**
*   *Silence is a red flag.* Narrate your thoughts.
*   *"I'm going to use a `defaultdict` here because it handles missing keys gracefully."*
*   *"I'm initializing two pointers, one at the start and one at the end..."*
*   If you get stuck, say: *"I'm thinking of using a stack here, but I'm not sure how to handle the edge case where the stack is empty. Do you have a hint?"*

**Step 4: Dry Run / Manual Testing (3-5 minutes)**
*   *Never say "I'm done" immediately after writing the last line of code.*
*   Take a small test case (e.g., `[2, 7, 11, 15]`, target `9`).
*   Walk through your code line-by-line with that input. Update the variables on the whiteboard/screen as you go.
*   Catch your own bugs during this step. Interviewers *love* this.

**Step 5: Complexity Analysis (1 minute)**
*   State the Time Complexity: *"This runs in O(N) time because we iterate through the array exactly once, and Hash Map lookups are O(1) on average."*
*   State the Space Complexity: *"This takes O(N) extra space to store the Hash Map."*

---

### 🏁 Final 48-Hour Battle Plan

1.  **Hour 0-12:** Review the **Python Core** and **FastAPI/Django** sheets. These are your bread and butter.
2.  **Hour 12-24:** Review **Databases**, **Docker**, and **AWS/CI-CD**. Focus on the "Scenario" and "Troubleshooting" questions.
3.  **Hour 24-36:** Practice **DSA Patterns** (Arrays, Hash Maps, Linked Lists) and write the code for **2 LLD Scenarios** (Parking Lot, LRU Cache) from scratch in your IDE.
4.  **Hour 36-42:** Review **GenAI/LLMs** and **Software Design Principles**.
5.  **Hour 42-48:** Rest. Review your **Behavioral** stories (STAR method). Sleep.

You now have a **500+ question master syllabus** covering every single technology, framework, and concept required for this role. You know what they will ask, you know how they will ask it, and you know how to answer it.

Close the tabs, open your IDE, and start practicing. **You are going to crush this EPAM review.** Good luck!