Here is your **100-Question AWS & CI/CD Master Sheet**, specifically tailored for a Junior/Mid-level Python Backend Developer. 

Since EPAM and similar service-based companies heavily test **scenario-based architecture**, **Infrastructure as Code (IaC)**, and **how cloud concepts integrate with your actual code (Docker/Python)**, I have dedicated a massive final section specifically to **Python/Backend Cloud Scenarios**.

As requested, **there are no answers here**. This is your pure study syllabus.

---

### ☁️ Category 1: AWS Compute & Serverless (1-12)
*Focus: Choosing the right compute layer and understanding scaling mechanics.*
1. What is the fundamental difference between EC2, AWS ECS (Fargate), AWS EKS, and AWS Lambda? Give a strict decision matrix for when to use each.
2. What are "Cold Starts" in AWS Lambda? What causes them, and what are 3-4 concrete ways to mitigate them?
3. How does Auto Scaling work in EC2? What is the difference between Target Tracking, Step, and Simple Scaling policies?
4. What is the difference between a Spot Instance, an On-Demand Instance, and a Reserved Instance? When would you strictly use Spot Instances for a backend service?
5. In ECS, what is the difference between a Task Definition and a Service? 
6. How does ECS Fargate differ from the EC2 launch type? What are the trade-offs regarding cost and control?
7. What is an AWS Batch or AWS Step Functions? When would you use them over a standard Python Celery worker?
8. How do you pass environment variables and secrets to an ECS Task without hardcoding them in the Docker image?
9. What is the difference between a Vertical Scale (Scale Up) and a Horizontal Scale (Scale Out)? Which one does AWS prefer you to do, and why?
10. How do you handle graceful shutdowns in an EC2 or ECS environment when an Auto Scaling Group terminates an instance? (Hint: Lifecycle hooks, SIGTERM handling in FastAPI/Django).
11. What is AWS App Runner? How does it simplify deploying containerized web apps compared to raw ECS?
12. If your Python backend app is experiencing high CPU usage, how do you determine if you need to scale vertically (bigger instance) or horizontally (more instances)?

### 🗄️ Category 2: AWS Storage & Databases (13-23)
*Focus: Data persistence, consistency, and choosing the right AWS data store.*
13. What is the difference between Amazon S3, Amazon EBS, and Amazon EFS? When would you strictly use EFS over EBS?
14. Explain the S3 Storage Classes (Standard, Intelligent-Tiering, Glacier Instant Retrieval, Glacier Flexible). How do S3 Lifecycle Policies work?
15. What is an S3 Presigned URL? How does it allow a user to upload a file directly to S3 without your backend server acting as a middleman?
16. What is the difference between S3 Eventual Consistency and Strong Consistency? (Note: S3 now provides strong consistency for all applications).
17. Compare Amazon RDS (PostgreSQL/MySQL) with Amazon Aurora. What makes Aurora "cloud-native," and how does its storage architecture differ?
18. What is the difference between an RDS Multi-AZ deployment and an RDS Read Replica? How do they differ in terms of Disaster Recovery vs. Read Scaling?
19. When would you choose Amazon DynamoDB over Amazon RDS? What are the core differences in their data models and scaling mechanisms?
20. What is DynamoDB DAX (Durable Accelerator)? How does it improve read performance for a DynamoDB table?
21. What is Amazon ElastiCache? Compare the use cases for Redis vs. Memcached in AWS.
22. How do you handle database backups in AWS? Explain the difference between RDS automated snapshots and AWS Backup.
23. What is Amazon S3 Versioning? How does it protect against accidental deletions and overwrites, and how does it integrate with MFA Delete?

### 🌐 Category 3: AWS Networking & VPC (24-34)
*Focus: The backbone of AWS. Interviewers love grilling juniors on VPC mechanics.*
24. What is a VPC? Explain the difference between a Public Subnet, a Private Subnet, and an Isolated Subnet.
25. What is the exact difference between an Internet Gateway (IGW) and a NAT Gateway? 
26. How do you allow a Python backend service in a Private Subnet to download a package from PyPI or talk to an external API, without exposing it to inbound internet traffic?
27. What is the difference between Security Groups and Network ACLs (NACLs)? Which one is stateful, and which one is stateless?
28. How does an Application Load Balancer (ALB) differ from a Network Load Balancer (NLB)? At which OSI layers do they operate?
29. What is a Target Group in AWS? How do health checks work, and what happens if all targets in a group fail their health checks?
30. How does Amazon Route 53 work? Explain the difference between Simple, Weighted, Latency, and Failover routing policies.
31. What is AWS CloudFront? How does it reduce latency, and what is an Origin Access Identity (OAI) or Origin Access Control (OAC)?
32. How do you connect two different VPCs together securely? (Explain VPC Peering vs. AWS Transit Gateway).
33. What is a VPC Endpoint? How does it allow your private EC2/ECS instances to talk to S3 or DynamoDB without traversing the public internet?
34. If your application is returning a 504 Gateway Timeout, what are the AWS networking components you would check first? (ALB idle timeouts, target response times, security groups).

### 🔒 Category 4: AWS Security, IAM & Secrets (35-45)
*Focus: Securing the cloud environment and managing credentials safely.*
35. What is the Principle of Least Privilege? How do you apply it when writing an IAM Policy for an ECS Task?
36. What is the exact difference between an IAM User, an IAM Role, and an IAM Group? 
37. How does `sts:AssumeRole` work? How do you use it to allow an EC2 instance or ECS Task to access S3 without hardcoding AWS Access Keys?
38. What is the difference between AWS Secrets Manager and AWS Systems Manager (SSM) Parameter Store? When would you strictly use Secrets Manager?
39. How does AWS Key Management Service (KMS) work? Explain the difference between AWS Managed Keys and Customer Managed Keys (CMK).
40. What is Envelope Encryption? How do you use KMS to encrypt a large file in S3 efficiently?
41. How do you protect a public-facing FastAPI/Django API from DDoS attacks and SQL Injection? (Explain AWS Shield vs. AWS WAF).
42. What is AWS CloudTrail? How does it differ from Amazon CloudWatch?
43. How do you enforce encryption at rest for an RDS database or an S3 bucket?
44. What is AWS Cognito? How would you use it to handle user authentication and JWT generation for a mobile app frontend?
45. How do you audit and find out which IAM user or role deleted a critical S3 bucket or EC2 instance?

### 🏗️ Category 5: AWS Architecture & "EPAM" Scenarios (46-55)
*Focus: High-level system design, fault tolerance, and cost optimization.*
46. Design a highly available, fault-tolerant web architecture in AWS for a Python backend. Walk me through the flow of a request from the user to the database.
47. How do you design a system for "Disaster Recovery"? Explain the difference between Backup & Restore, Pilot Light, Warm Standby, and Multi-Site Active-Active.
48. Your AWS bill suddenly doubled overnight. What is your exact step-by-step process to identify the cause and reduce costs?
49. How do you decouple a monolithic Python application in AWS? (Explain using SQS, SNS, and EventBridge to break apart synchronous calls).
50. What is the difference between Amazon SQS and Amazon SNS? When do you use a Queue vs. a Pub/Sub Topic?
51. What is Amazon EventBridge? How does it differ from SNS/SQS for building event-driven architectures?
52. How do you handle distributed tracing across multiple microservices in AWS? (Explain AWS X-Ray).
53. What is the "Serverless" approach to building a backend? Design a simple API using API Gateway, Lambda, and DynamoDB. What are the drawbacks of this approach?
54. How do you implement a caching layer in AWS to reduce the load on your RDS Postgres database?
55. If your company is migrating from on-premises data centers to AWS, what migration strategy (The 6 Rs) would you use for a legacy Django monolith?

### 🔄 Category 6: CI/CD Core Concepts & Pipeline Design (56-65)
*Focus: The theory and mechanics of continuous integration and delivery.*
56. What is the exact difference between Continuous Integration (CI), Continuous Delivery (CD), and Continuous Deployment?
57. Design a complete CI/CD pipeline for a Python FastAPI microservice. Detail every single stage from `git push` to production traffic.
58. What is the "Testing Pyramid"? How do you balance Unit, Integration, Contract, and End-to-End (E2E) tests in a CI pipeline?
59. What is an Artifact in CI/CD? How do you manage and version Docker images and Python wheels in a pipeline?
60. What are "Flaky Tests"? Why are they dangerous in a CI/CD pipeline, and how do you fix or quarantine them?
61. How do you handle parallel execution in a CI pipeline to speed up build times?
62. What is the difference between a Push-based CI/CD (e.g., Jenkins, GitHub Actions) and a Pull-based CI/CD (e.g., ArgoCD, Flux)?
63. How do you manage environment-specific configurations (Dev, Staging, Prod) in a CI/CD pipeline without changing the code or the Docker image?
64. What is a "Build Matrix" in GitHub Actions or GitLab CI? How do you use it to test your Python code against Python 3.10, 3.11, and 3.12 simultaneously?
65. How do you implement automated rollback in a CI/CD pipeline if a deployment fails health checks?

### 📜 Category 7: Infrastructure as Code (IaC) - Terraform & CloudFormation (66-76)
*Focus: Treating infrastructure as software, state management, and reproducibility.*
66. What is Infrastructure as Code (IaC)? Why is it strictly preferred over clicking around in the AWS Console?
67. Compare Terraform and AWS CloudFormation. What are the pros and cons of each? Why is Terraform more popular in multi-cloud environments?
68. What is the Terraform "State" file (`terraform.tfstate`)? Why is it critical, and why should it never be stored locally or in Git?
69. How do you manage Terraform state in a team environment? Explain remote state storage (e.g., S3) and state locking (e.g., DynamoDB).
70. What is "State Drift" in Terraform? How does it happen, and how do you fix it (`terraform refresh`, `terraform import`)?
71. What are Terraform Modules? Why are they essential for writing reusable and maintainable infrastructure code?
72. Explain the Terraform lifecycle: `terraform init`, `terraform plan`, `terraform apply`, and `terraform destroy`. What does `plan` actually do under the hood?
73. How do you handle secrets in Terraform? Why is it bad to pass them as standard variables, and how do you integrate with AWS Secrets Manager?
74. What is the difference between `count` and `for_each` in Terraform? When would you strictly use `for_each`?
75. How do you import existing, manually created AWS resources into Terraform state?
76. What is Pulumi or AWS CDK? How do they differ from Terraform's HCL syntax?

### 🚀 Category 8: Deployment Strategies & Release Management (77-86)
*Focus: How to push code to production safely, with zero downtime.*
77. Explain the difference between Rolling, Blue-Green, and Canary deployment strategies.
78. Which deployment strategy minimizes the risk of a bad release, and which one minimizes the time to rollback?
79. What is "Immutable Infrastructure"? How does it differ from mutable infrastructure (e.g., SSHing into a server to update code)?
80. What is Infrastructure Baking? How do tools like HashiCorp Packer or AWS EC2 Image Builder fit into this?
81. What is a "Feature Flag" (or Feature Toggle)? How do tools like LaunchDarkly or Unleash allow you to decouple deployment from release?
82. How do you handle database schema migrations in a zero-downtime deployment? Explain the "Expand and Contract" pattern.
83. What is GitOps? How does the "Git repository as the single source of truth" paradigm change how we deploy applications?
84. How do you perform a "Smoke Test" or "Sanity Check" immediately after a deployment but before routing live user traffic to the new version?
85. What is the role of a Service Mesh (like Istio or Linkerd) in managing traffic splitting for Canary deployments?
86. If a Blue-Green deployment fails and you need to rollback, what is the exact mechanism to revert traffic instantly?

### 🐍 Category 9: Python/Backend Specific Cloud & CI/CD Scenarios (87-100)
*Focus: The intersection of your Python code, Docker, and AWS. (Highly likely for your specific interview).*
87. How do you optimize the Docker build process for a Python FastAPI app in a CI pipeline to ensure it takes under 3 minutes? (Hint: Layer caching, `uv`/`poetry` lock files).
88. How do you run `pytest` in a CI pipeline when your tests require a real PostgreSQL database and a Redis instance? (Explain Testcontainers or Docker Compose in CI).
89. Your FastAPI Docker container needs to read a database password. Walk me through the exact AWS architecture to pass this secret securely from AWS Secrets Manager into the running container environment variables.
90. How do you handle Django/FastAPI database migrations (Alembic/Django Migrations) in a CI/CD pipeline? Should the application container run the migration, or a separate init container?
91. How do you manage Python virtual environments and dependency resolution (`uv`, `poetry`, `pip`) in a CI/CD environment to ensure exact reproducibility?
92. Your Python backend uses a heavy C-extension library (like `numpy` or `psycopg2`). How does this impact your Docker build in CI, and how do you optimize it using multi-stage builds?
93. How do you implement automated code quality checks (Ruff, Mypy, Black) in a CI pipeline? Should they block the build or just warn?
94. How do you build and push a Docker image to AWS ECR (Elastic Container Registry) using GitHub Actions or GitLab CI?
95. If your Python application experiences a memory leak, how do you detect it using AWS CloudWatch metrics, and how do you configure ECS to automatically restart the container?
96. How do you implement distributed tracing for a FastAPI application using OpenTelemetry and AWS X-Ray?
97. How do you handle CORS and API Gateway integration when your FastAPI backend is deployed behind an AWS API Gateway?
98. What is the best practice for logging in a containerized Python app running in ECS? (Explain why you should log to `stdout`/`stderr` and let AWS CloudWatch Logs driver handle the rest).
99. How do you load test a FastAPI application deployed on AWS ECS? What tools do you use (Locust, k6), and what AWS metrics do you monitor during the test?
100. **The Ultimate Scenario:** You push a commit to `main`. The CI pipeline builds the Docker image, runs tests, pushes to ECR, and updates the ECS service. The new tasks start, but they fail their health checks and keep restarting. Walk me through your exact debugging process, from the CI logs to the AWS Console.

---

### 💡 How to conquer AWS & CI/CD for your EPAM Interview:

1. **The "VPC Bouncer":** Question 26 is a classic. If an interviewer asks, *"How does my backend in a private subnet talk to the Stripe API?"* you must confidently answer: *"It routes traffic to the private subnet's route table, which points to a NAT Gateway in the public subnet, which then routes through the Internet Gateway to the public internet. The Security Group allows outbound traffic, but no inbound traffic is allowed."*
2. **Secrets Management:** Never say "I use `.env` files in production." For Question 89, explain that the ECS Task Role grants permission to read from AWS Secrets Manager, and the ECS Task Definition maps that secret directly into the container's environment variables at runtime.
3. **CI/CD Python Specifics:** EPAM loves practical pipeline questions. Be ready to talk about **Testcontainers** (Question 88) for integration testing, and using **`uv` or `poetry` lock files** (Question 91) to guarantee that the CI environment exactly matches your local environment.
4. **Draw the Architecture:** For Question 46, practice drawing a standard 3-tier AWS architecture on a piece of paper (Route53 -> CloudFront -> ALB -> Auto Scaling Group of ECS tasks in Private Subnets -> NAT Gateway -> RDS Multi-AZ). If you can draw and explain this, you pass the architecture round.

You now have the complete blueprint for Python, Databases, Docker, Design Principles, APIs/Microservices, and AWS/CI-CD. 

You are fully armed for this review. Take a deep breath, review your weak spots, and go ace it! Let me know if you need the final piece: **GenAI / LLMs / LangChain**.