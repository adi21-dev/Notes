This is the ultimate **110-Question Python Master Sheet**. I have deeply integrated every single specific topic from your uploaded PDF (including the highly specific bouncers like PyMalloc, TimSort, `sys.getrefcount` quirks, Walrus operator, and `else` clauses) and combined them with advanced EPAM-style system and backend questions.

As requested, **there are no answers here**. This is your pure study syllabus. If you can confidently answer or code these, you will ace the Python portion of your interview.

---

### 🟢 Category 1: Core Basics, Syntax & "Gotchas" (The Bouncers)
*These are the tricky questions designed to catch you off guard if you only know surface-level Python.*

1. What is the exact difference between `==` and `is`? How does Python’s small integer caching (-5 to 256) affect the `is` operator?
2. What is the output of modifying a list inside a tuple? `t = ([1,2], [3,4]); t[0].append(5); print(t)`. Why doesn't it throw an error?
3. Explain the `else` clause in a `for` loop and a `try/except` block. Under what exact conditions does the `else` block execute?
4. What is the Walrus operator (`:=`)? Give a practical scenario where it drastically improves code readability and performance.
5. What is the difference between `range` (Python 3) and `xrange` (Python 2)? Why is `range` in Py3 considered a sequence type and not a generator?
6. How does Python handle argument passing? Explain "pass by object reference" vs "call by value" vs "call by reference".
7. What is the difference between `del`, `remove()`, and `pop()`? When would you use each?
8. Explain the LEGB rule for scope resolution. How does the `nonlocal` keyword differ from `global`?
9. Are f-strings faster than `.format()` and `%` formatting? Why, at the bytecode/evaluation level?
10. What is the output of `bool("False")`? How do you properly and safely evaluate a string to a boolean?
11. Explain the difference between `type()` and `isinstance()`. Why is `isinstance` generally preferred?
12. What is "duck typing"? How does it relate to the Zen of Python and Python's philosophy on interfaces?
13. How do you define and access "private" variables in Python? Explain name mangling (`__var`).
14. What is the exact purpose of `if __name__ == "__main__":`? How does the `__name__` variable change when a script is imported vs run directly?
15. What is the difference between `__str__` and `__repr__`? When does Python use `__repr__` as a fallback?

### 🧠 Category 2: Data Structures, Memory & Internals (Deep Dive)
*EPAM loves asking how things work under the hood. These questions test your knowledge of CPython internals.*

16. How is a dictionary implemented under the hood in Python? How does it handle hash collisions (open addressing vs chaining)?
17. What makes an object "hashable"? Why can't lists or dicts be dictionary keys, but tuples can (and when can't they)?
18. Explain Python's memory management architecture: Private Heap, PyMalloc, Arenas, Pools, and Blocks.
19. How does Reference Counting work? What is the exact output of `sys.getrefcount(1)` vs `sys.getrefcount([])` and why is there a discrepancy?
20. Explain the Generational Garbage Collector (Gen 0, 1, 2). How does it decide when to run, and how are thresholds calculated?
21. What is the difference between shallow copy and deep copy? How does `copy.deepcopy()` handle circular references internally?
22. Why does Python not return freed memory to the OS immediately? What are "free lists" and how do they optimize performance?
23. What is string interning and small integer caching? How do they optimize memory, and how can you manually intern a string?
24. How do you identify and fix memory leaks in Python? What tools do you use (`tracemalloc`, `objgraph`, `gc`)?
25. What is the difference between a Python `list` and an `array.array`? When would you strictly use `array` over `list`?
26. Explain the time complexity of `list.sort()` vs `sorted()`. What algorithm does Python use (Timsort), and why is it stable?
27. How do you sort a dictionary by its values? How do you sort a list of dictionaries by a specific nested key?
28. How do you sort a list of elements based on the frequency of each element using a dictionary or `collections.Counter`?
29. Why don't we need to import the `collections` module for basic data structures (list, dict, set, tuple)? Where do they actually live in CPython?
30. What are the differences between `defaultdict`, `OrderedDict`, and standard `dict`? (Note: standard dict maintains insertion order in 3.7+).
31. What is the process of compilation and linking in Python? What are `.pyc` files and the `__pycache__` directory?
32. What are Python "wheels" (`.whl`) and "eggs"? How do they differ from source distributions (`.tar.gz`)?
33. How does Python's `set` operation work under the hood? What is the time complexity of intersection, union, and difference?
34. What happens when you mutate a dictionary while iterating over it? How do you safely add/remove keys during iteration?
35. Explain the difference between `zip()`, `map()`, and `enumerate()`. How do they handle iterables of unequal lengths?

### 🏗️ Category 3: OOP, Magic Methods & Metaprogramming
*Testing your ability to design clean, extensible, and Pythonic object-oriented code.*

36. What is the difference between `__new__` and `__init__`? When would you strictly override `__new__`?
37. Explain the Method Resolution Order (MRO). How does Python's C3 Linearization algorithm solve the diamond problem?
38. What are descriptors (`__get__`, `__set__`, `__delete__`)? How do `@property`, `@classmethod`, and `@staticmethod` use the descriptor protocol?
39. What is the difference between a metaclass and a class decorator? When would you use a metaclass over a decorator?
40. How do you restrict the creation of dynamic attributes in a class to save memory? Explain `__slots__` and its limitations with inheritance.
41. What is a mixin class? How does it differ from standard multiple inheritance, and what are the best practices for using them?
42. Explain Abstract Base Classes (ABCs). How do you enforce method implementation in subclasses using `abc.ABC` and `@abstractmethod`?
43. What is the difference between composition and inheritance? Give a Python example where composition is strictly better.
44. How do you implement a Singleton pattern in Python? Why is it considered an anti-pattern, and how do you make it thread-safe?
45. What is monkey patching? Give a scenario where it is useful (e.g., `gevent`), and explain why it is dangerous in production.
46. What is the `__call__` magic method? How do you use it to make an object behave like a function?
47. What are destructors in Python (`__del__`)? Why are they unreliable for critical resource cleanup compared to context managers?
48. How do you implement custom context managers using classes (`__enter__`, `__exit__`) vs using `contextlib.contextmanager`?
49. What is Dependency Injection? How do you implement it in pure Python without a framework?
50. Explain the Factory and Adapter design patterns with Python code examples.
51. What is the fundamental difference between design principles (like SOLID) and design patterns?
52. How do you implement a custom exception class? What is the best practice for raising and catching custom exceptions in a large codebase?
53. What is the difference between `@staticmethod`, `@classmethod`, and instance methods? When do you use each?
54. How does Python handle multiple inheritance? What is the diamond problem and how does MRO solve it?
55. What is metaprogramming in Python? Give an example of writing code that generates or modifies code dynamically.

### ⚙️ Category 4: Functional, Iterators, Generators & Decorators
*Crucial for writing clean, memory-efficient, and reusable code.*

56. What is the exact difference between an Iterable, an Iterator, and a Generator?
57. How does the `yield` keyword work? What is the difference between `yield` and `yield from`?
58. What is a closure in Python? Explain the "late binding" gotcha in a loop of lambdas and how to fix it.
59. How do you write a parameterized decorator (a decorator that takes arguments)?
60. How do you write a decorator that can handle both synchronous and asynchronous functions seamlessly?
61. What is the purpose of `functools.wraps`? What metadata is lost if you don't use it?
62. What is a generator expression vs a list comprehension? When should you strictly use a generator expression?
63. How do you use lazy evaluation to read an excessively large file (e.g., 50GB) in Python without running out of memory?
64. Explain functional programming concepts in Python. How do `map`, `filter`, `reduce`, and `functools.partial` work?
65. What are type hints in Python? Explain `Any`, `Union`, `Optional`, `Iterable`, and `TypeVar`.
66. What is the difference between static type checking (`mypy`) and runtime type checking (Pydantic)?
67. How do you implement a custom iterator class from scratch? (Hint: `__iter__` and `__next__`).
68. What is the `itertools` module? Explain `chain`, `groupby`, and `islice`.
69. How do you implement a memoization decorator from scratch using the concepts behind `functools.lru_cache`?
70. What is the difference between `map()` and a list comprehension? Which is more "Pythonic" and why?

### 🚀 Category 5: Concurrency, GIL, Asyncio & Multithreading
*The most common area for "senior-level" bouncer questions for junior/mid roles.*

71. What exactly is the Global Interpreter Lock (GIL)? Why does it exist in CPython, and why is it so hard to remove?
72. How does the GIL affect CPU-bound vs I/O-bound tasks? When do you strictly use `threading` vs `multiprocessing`?
73. What is the fundamental difference between multithreading and `asyncio`? How does the context switch differ between them?
74. How does the `asyncio` event loop work under the hood? What is cooperative multitasking?
75. What happens if you put a blocking synchronous call (like `time.sleep()` or `requests.get()`) inside an `async def`? How do you fix it?
76. Explain `asyncio.gather()`, `asyncio.wait()`, and `asyncio.as_completed()`. When do you use `TaskGroup` (Python 3.11+)?
77. How do you share data between different processes in `multiprocessing`? (Manager, Value, Queue). What are the performance costs?
78. What is thread safety? How do you achieve it in Python using `Lock`, `RLock`, and `Semaphore`?
79. What is a race condition? Does the GIL completely prevent race conditions? (Explain why `x += 1` is not atomic).
80. How do you prevent deadlocks in multithreading? Explain lock ordering and timeouts.
81. What is the difference between a coroutine and a Task in `asyncio`? Why use `asyncio.create_task()`?
82. How do you handle exceptions in `asyncio` tasks? What happens if an exception is raised in a background task and never awaited?
83. How does `concurrent.futures.ThreadPoolExecutor` differ from `ProcessPoolExecutor`?
84. What is the difference between `asyncio.sleep()` and `time.sleep()`?
85. How do you run a synchronous blocking function in an `asyncio` event loop without blocking it? (`run_in_executor`).

### 🏢 Category 6: Advanced Backend, System Design & Profiling
*Connecting Python to the real world of backend engineering.*

86. How do you profile Python code to find bottlenecks? Explain `cProfile`, `line_profiler`, and `memory_profiler`.
87. How do frameworks like FastAPI implement Dependency Injection using `Depends` under the hood?
88. How do you design a scalable Python backend system? What are the common Python-specific bottlenecks?
89. How do you implement caching (LRU cache, Redis) in a Python backend?
90. How do you implement rate limiting in an API? (Token bucket, sliding window).
91. What are the common security best practices in Python backends? (SQLi, XSS, CSRF, Pickle vulnerabilities).
92. How do you handle retries and failures in Python? (Explain the `tenacity` library or custom exponential backoff).
93. How do you access a module written in Python from C, and vice versa? (Cython, ctypes, CPython API).
94. How do you speed up existing Python code? (Cython, PyPy, multiprocessing, C-extensions).
95. How do you handle high traffic systems in Python? (Gunicorn/Uvicorn workers, async, caching, message queues).

### 💻 Category 7: Live Coding & Practical Scenarios
*These are the questions they will actually ask you to code on a whiteboard or shared IDE.*

96. Write a function to flatten a deeply nested list of arbitrary depth.
97. Write a custom decorator that retries a function `n` times with exponential backoff if it raises an exception.
98. Implement a thread-safe Singleton class in Python.
99. Write a generator that yields the Fibonacci sequence infinitely.
100. Write a function to find the first non-repeating character in a string in O(N) time.
101. Implement an LRU Cache from scratch using `collections.OrderedDict` (or a Dict + Doubly Linked List).
102. Write a context manager that measures and prints the execution time of a block of code.
103. Write a function to merge two dictionaries. (Show the Py3.9+ `|` operator, `update()`, and `{**d1, **d2}`).
104. Write a script to read a 50GB log file line-by-line and count the occurrences of a specific error string without loading it into memory.
105. Implement a custom `map` function from scratch using generators.
106. Write a function to check if a string of brackets `()[]{}` is balanced.
107. Write an async function that fetches 5 URLs concurrently and returns the result of the first one that succeeds.
108. Write a decorator that caches the results of a function based on its arguments (basic memoization without `lru_cache`).
109. Given a list of integers, write a function to move all zeroes to the end while maintaining the relative order of non-zero elements (in-place, O(N)).
110. Write a Python snippet to demonstrate the "mutable default argument" gotcha, and then write the correct way to handle it.

---

### 💡 How to conquer this in 48 hours:
1. **Triage:** Skim all 110. Mark them 🟢, 🟡, 🔴.
2. **Focus on the Bouncers (Cat 1 & 2):** Interviewers at service-based companies love asking the "gotcha" questions (like Q2, Q3, Q19, Q22) to separate those who just memorized syntax from those who understand the engine.
3. **Code the Live Coding (Cat 7):** Do not just read them. Open your IDE and type out Q96, Q97, Q101, and Q107 from memory. Muscle memory is crucial for live coding.
4. **Verbalize:** For the GIL and Asyncio questions (Cat 5), practice explaining them out loud. If you stumble, review the concepts.

You have the ultimate cheat sheet now. Go crush this EPAM review! Let me know if you want to do a mock verbal round on any specific category.