Here is your **100-Question Docker Master Sheet**, specifically tailored for a Junior/Mid-level Python Backend Developer interview at a top-tier service company like EPAM. 

Since you are a Python developer, I have included a dedicated section at the end for **Python-specific Docker scenarios**, which are highly likely to be asked in your specific review.

As requested, **there are no answers here**. This is your pure study syllabus.

---

### 🐧 Category 1: Core Docker & Linux Internals (1-10)
*Focus: Understanding what a container actually is under the hood.*
1. What is the fundamental difference between a Virtual Machine (VM) and a Docker Container?
2. What are Linux Namespaces? Explain the purpose of PID, NET, MNT, UTS, IPC, and USER namespaces.
3. What are Linux Cgroups (Control Groups)? How does Docker use them to restrict CPU and Memory?
4. Explain the UnionFS (Union File System) and OverlayFS. How do they enable Docker images to be lightweight?
5. What is the Copy-on-Write (CoW) strategy in Docker? How does it impact performance when a container modifies a file from the image layer?
6. What is the difference between the Docker Client and the Docker Daemon (`dockerd`)?
7. What is the exact difference between a Docker Image, a Docker Layer, and a Docker Container?
8. Can a container exist without an image? Can an image exist without a container?
9. What happens to the container's filesystem when the container is stopped and removed?
10. How does Docker achieve process isolation? If I run `top` or `ps` inside a container, what do I see?

### 🏗️ Category 2: Dockerfile Instructions & Mechanics (11-20)
*Focus: Writing correct and functional Dockerfiles.*
11. What is the difference between `CMD` and `ENTRYPOINT`? How do they interact when both are used?
12. What is the difference between the `COPY` and `ADD` instructions? When should you strictly avoid `ADD`?
13. What is the difference between `ARG` and `ENV`? Is an `ARG` visible in the final running container?
14. What does the `WORKDIR` instruction do? What happens if the directory doesn't exist?
15. What is the purpose of the `EXPOSE` instruction? Does it actually publish the port to the host machine?
16. How does the `VOLUME` instruction in a Dockerfile differ from creating a volume via the `docker run -v` CLI command?
17. What is the difference between the shell form and the exec form of `CMD` and `ENTRYPOINT`? (e.g., `CMD python app.py` vs `CMD ["python", "app.py"]`).
18. Why is the exec form (JSON array) recommended for `CMD` and `ENTRYPOINT` regarding OS signals (like SIGTERM)?
19. How do you pass environment variables to a container at runtime without hardcoding them in the Dockerfile?
20. What is the `.dockerignore` file? Why is it critical for both build performance and security?

### 📉 Category 3: Image Optimization & Best Practices (21-30)
*Focus: Making images small, fast, and secure.*
21. How do you minimize the number of layers in a Docker image? Give a practical example using `RUN`.
22. What is a Multi-Stage Build? Write a conceptual flow of how you would use it for a Python application.
23. Why is using the `alpine` Linux base image sometimes a bad idea for Python applications? (Hint: `musl libc` vs `glibc`).
24. What are "Distroless" images? Why are they considered a security best practice?
25. How does Docker's build cache work? How should you order your `COPY` and `RUN` instructions to maximize cache hits?
26. Why is it a bad practice to run `apt-get upgrade` or `pip install --upgrade` inside a Dockerfile?
27. How do you clean up package manager caches (like `apt` or `yum`) in the same `RUN` layer to reduce image size?
28. What is the impact of copying your entire source code (`COPY . .`) before installing dependencies? How do you fix this?
29. Why should you avoid installing unnecessary packages (like `curl`, `vim`, or `git`) in your final production image?
30. How do you handle `.pyc` files and `__pycache__` directories when building a Python Docker image?

### 💾 Category 4: Storage, Volumes & Persistence (31-40)
*Focus: Managing data that needs to survive container restarts.*
31. What is the difference between a Docker Volume, a Bind Mount, and a `tmpfs` mount?
32. When would you strictly use a Bind Mount over a Docker Volume?
33. What is the difference between a named volume and an anonymous volume?
34. Where are Docker volumes physically stored on the host Linux machine?
35. How do you share data between two different running containers?
36. How do you backup and restore a Docker volume?
37. If a container writes data to its writable layer (not a volume) and then crashes, is the data lost?
38. How do volume drivers work? Can you use an NFS or cloud storage (like AWS EFS) as a Docker volume?
39. What happens to a named volume when the container using it is deleted with `docker rm -v` vs just `docker rm`?
40. How do you restrict a container's write access to a volume (read-only mode)?

### 🌐 Category 5: Networking & Communication (41-50)
*Focus: How containers talk to each other and the outside world.*
41. What are the default Docker network drivers? Explain `bridge`, `host`, `none`, and `overlay`.
42. What is the difference between the default `bridge` network and a `user-defined bridge` network?
43. How does DNS resolution work in a user-defined Docker network? (e.g., how does Container A ping Container B by name?)
44. Why doesn't DNS resolution by container name work out-of-the-box on the default `bridge` network?
45. What is the difference between publishing a port (`-p 8000:80`) and exposing a port (`EXPOSE 80`)?
46. How do you allow a container to communicate with the host machine's localhost?
47. What is Docker MACVLAN? When would you use it to assign a physical MAC address to a container?
48. How do you restrict a container from accessing the external internet, while still allowing it to talk to other local containers?
49. What happens to the network interfaces and IP addresses when a container is restarted?
50. How do you debug network connectivity issues between two containers? (Tools and commands).

### 🎼 Category 6: Docker Compose & Local Development (51-60)
*Focus: Orchestrating multi-container local environments.*
51. What is Docker Compose? What problem does it solve that standard `docker run` cannot?
52. Explain the core sections of a `docker-compose.yml` file (services, networks, volumes).
53. What does the `depends_on` directive do? Does it wait for the dependent service to be *fully ready* (e.g., DB accepting connections) or just *started*?
54. How do you implement healthchecks in Docker Compose to ensure services are actually ready before starting dependent services?
55. How do you scale a specific service in Docker Compose (e.g., running 3 instances of a web worker)?
56. How do you manage environment variables in Docker Compose? Explain the use of the `.env` file and `env_file` directive.
57. How do you override the default `CMD` or `ENTRYPOINT` of an image specifically within the `docker-compose.yml` file?
58. What is the difference between `docker-compose up` and `docker-compose up -d`?
59. How do you force Docker Compose to rebuild images and ignore the cache?
60. How do you view the aggregated logs of all services in a Docker Compose setup?

### 🔒 Category 7: Security, Permissions & Secrets (61-70)
*Focus: Securing the container runtime and build process.*
61. Why is running a container as the `root` user considered a critical security vulnerability?
62. How do you run a container as a non-root user? Explain the `USER` instruction and the `--user` flag.
63. What are Linux Capabilities in Docker? Why should you use `--cap-drop=ALL` and only add back what is needed?
64. How do you prevent a container from escalating privileges to the host? (Explain `--security-opt=no-new-privileges`).
65. Why is it dangerous to pass secrets (API keys, DB passwords) using the `ENV` instruction in a Dockerfile?
66. How do you securely inject secrets into a running container without baking them into the image?
67. What is Docker Content Trust (DCT) and image signing? Why is it important in enterprise CI/CD?
68. How do you scan a Docker image for vulnerabilities? Name a few tools (e.g., Trivy, Snyk, Docker Scout).
69. What is a "Supply Chain Attack" in the context of Docker base images? How do you mitigate it?
70. How do you restrict a container from reading sensitive host files (like `/etc/shadow`)?

### 🐛 Category 8: Troubleshooting, Debugging & Exit Codes (71-80)
*Focus: What to do when things break in production or CI.*
71. What does Docker Exit Code `0` mean? What about `1`, `137`, `139`, and `255`?
72. Your container exits immediately with Code `137`. What exactly happened, and how do you fix it?
73. Your container exits immediately with Code `1`. How do you debug it if `docker logs` shows nothing?
74. How do you debug a container that keeps crashing on startup? (Hint: overriding the entrypoint).
75. What is the "PID 1 Zombie Reaping Problem" in Docker? How do `tini` or the `--init` flag solve it?
76. How do you execute a shell inside a running container? What if the container doesn't have `bash` or `sh` installed (like a distroless image)?
77. How do you copy a file from a crashed/exited container back to your host machine?
78. Your Python app inside Docker is running out of memory, but the host has plenty of RAM. How do you check and increase the container's memory limit?
79. How do you monitor the real-time resource usage (CPU/Memory/Network) of running containers?
80. What is the difference between `docker stop` and `docker kill`? How does the grace period work?

### 🚀 Category 9: CI/CD, Registries & Orchestration Basics (81-90)
*Focus: How Docker fits into the broader software delivery lifecycle.*
81. What is a Container Registry? Compare DockerHub, AWS ECR, and GitHub Container Registry.
82. What is the best practice for tagging Docker images in a CI/CD pipeline? (e.g., `latest` vs Git SHA vs Semantic Versioning).
83. Why is using the `latest` tag in production deployments considered a bad practice?
84. What is the difference between Docker Swarm, Kubernetes, and AWS ECS?
85. What is a "Sidecar" container pattern? Give a practical example (e.g., logging or proxy sidecar).
86. How do you implement a "Blue-Green" or "Canary" deployment using containers?
87. What is Infrastructure as Code (IaC) in the context of containers? How do tools like Terraform interact with Docker/K8s?
88. How do you handle database migrations in a containerized CI/CD pipeline? Should the app container run the migration, or a separate init container?
89. What is the difference between a stateless container and a stateful container? Why should databases generally not run in standard containers without orchestration?
90. How do you manage configuration differences (Dev vs Staging vs Prod) for the exact same Docker image?

### 🐍 Category 10: Python-Specific Docker Scenarios (91-100)
*Focus: The intersection of Python and Docker (Highly likely for your specific interview).*
91. Write/Explain the optimal Dockerfile for a FastAPI application. What base image do you choose and why?
92. How do you handle `pip install` caching in Docker so that dependencies aren't re-downloaded on every code change?
93. Why is it recommended to run Gunicorn or Uvicorn with multiple workers inside a Docker container? How do you calculate the optimal number of workers?
94. How does the GIL interact with Docker? If you run a multi-threaded Python app in a container, do you need to configure CPU limits differently than a multi-process app?
95. Your Python app uses `psycopg2` or `numpy`. Why might the `alpine` Docker image fail to build these, and how do you fix it?
96. How do you handle timezone differences in Python Docker containers? (e.g., ensuring `datetime.now()` returns the correct local time).
97. How do you run `pytest` inside a Docker container during the CI/CD build stage without baking the test dependencies into the final production image?
98. What is the impact of Python's memory allocator (PyMalloc) inside a container with strict memory limits? How do you prevent OOMKills?
99. How do you handle graceful shutdowns in a Python web app running in Docker? (Handling SIGTERM to close DB connections properly).
100. If your Python container's image size is 1.5GB, what are the exact steps you would take to reduce it to under 300MB?

---

### 💡 How to conquer Docker for your EPAM Interview:
1. **The "Bouncer" Questions:** Interviewers love asking about **Exit Code 137** (OOMKilled), **PID 1 Zombie Reaping**, and **CMD vs ENTRYPOINT exec form**. Memorize these.
2. **Python + Docker (Category 10):** Since you are a Python dev, they *will* ask you how to optimize a Python Dockerfile. Be ready to talk about multi-stage builds, copying `requirements.txt` before `COPY . .`, and why `python:3.11-slim` is usually better than `alpine` for Python.
3. **Verbalize the "Why":** Don't just say "I use multi-stage builds." Say, "I use multi-stage builds *to separate the heavy build-time dependencies (like C-compilers) from the lightweight runtime environment, which reduces the final image size and shrinks the security attack surface.*"
4. **Troubleshooting Mindset:** For Category 8, practice your debugging workflow. "First I check `docker logs`, then I inspect the exit code, then I check `docker inspect` for OOMKilled flags, and finally I might override the entrypoint to `/bin/sh` to debug the filesystem."

You have the ultimate Docker syllabus. Go crush this review! Let me know if you want to tackle AWS, FastAPI, or GenAI next.