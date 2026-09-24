---
title : "Events Participated"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

### Event Report – First Cloud Journey (FCAJ)

---

### 1. Event Overview

* **Event Name**: First Cloud Journey – Cloud Computing, System Design & MLOps on AWS
* **Event Objectives**:
  * Deliver a comprehensive overview and practical roadmap for students and software engineers starting with AWS Cloud Computing.
  * Clarify system architecture principles from single-server setups to massive scale (System Design).
  * Dive deep into server hosting models across the Hosting Spectrum.
  * Build an end-to-end Data Science & MLOps pipeline from experimentation to production on Cloud infrastructure.
* **Speakers**:
  * **Phuong Nguyen Huu**: Topic *"The Very First Step into Cloud"*.
  * **Vu The Huy**: Data Engineer, topic *"Data Science & MLOps on AWS"*.
  * **Quang Pham**: DevOps Engineer, topic *"Right Server, Right Job – Comparing Hosting Types and Server Options"*.
  * **Le Thanh Dung (ltdungg)**: Lecturer / Author of *"System Design for Beginners"*.

---

### 2. Key Highlights

#### 2.1. The Very First Step into Cloud
* **Cloud Concepts & Economics**: 
  * Comparison between On-Premises and Cloud computing.
  * Shifting from fixed capital expenditure (CapEx) to flexible operational expenditure (OpEx).
  * Leveraging Economies of Scale and global scale in minutes.
* **Service Models & Shared Responsibility**: 
  * Clear distinctions between IaaS, PaaS, and SaaS.
  * The Shared Responsibility Model (Security *in* the Cloud by customer vs. Security *of* the Cloud by AWS).
* **AWS Global Infrastructure**: 
  * Regions, Availability Zones (AZs), and Edge Locations.
  * Management interfaces via AWS Console, AWS CLI, and AWS SDKs.

#### 2.2. System Design for Beginners
* **From a Single Server to Scaled Systems**: Analyzing the first three bottlenecks and points of failure when hosting a single-server photo-sharing platform.
* **Architecture Distinction**: 
  * High-Level Design (HLD) vs. Low-Level Design (LLD).
  * Defining Functional and Non-functional Requirements (NFRs).
  * Monolith vs. Microservices; Vertical vs. Horizontal Scaling.
* **Core Infrastructure & Data Optimization**: 
  * Mechanics of DNS/HTTPS, Load Balancers (Health checks, Reverse Proxy, routing algorithms), Stateful vs. Stateless servers.
  * Data Modeling strategies, SQL vs. NoSQL, Database Indexing, Caching (TTL, Cache Stampede), Database Replication, and Sharding.

#### 2.3. Right Server, Right Job: Comparing Hosting Types & Server Options
* **The Hosting Spectrum**: Comparing 5 hosting models: Shared Hosting, VPS, VDS, Dedicated Server, and On-Premises (mapped to AWS services such as Amplify/App Runner, EC2 T-series, EC2 Compute-Optimized, EC2 Dedicated Host, AWS Outposts).
* **Architectural Realities & Anti-patterns**:
  * Shared Hosting using cgroups/namespaces; VPS sharing CPU resources over Type-1 hypervisors causing CPU Steal.
  * VDS utilizing CPU pinning and NUMA-aligned RAM to avoid >50% performance degradation from Cross-Node Memory Access.
  * **AWS Nitro System**: Offloading all I/O, networking, and storage to dedicated ASIC hardware, returning virtually 100% CPU/RAM to virtual machines.
* **Production Case Study**: Athenahealth's Hybrid Cloud architecture blending on-premise datacenters, AWS Outposts, and AWS Local Zones to modernize legacy workloads while ensuring ultra-high availability.

#### 2.4. Data Science & MLOps on AWS
* **Big Picture (DE vs. DS vs. DA)**: Distinct roles of Data Engineer ("The Road Builder"), Data Scientist ("The Predictor"), and Data Analyst ("The Storyteller").
* **Real-world Data Scientist Workflow**: 70% spent on business framing, EDA, and Feature Engineering; 20% on model training and evaluation; 10% on deployment.
* **Churn Prediction Case Study & End-to-End Pipeline**:
  * **Data Lake & Data Catalog**: AWS S3, AWS Glue, and AWS Athena/EMR integration.
  * **Feature Management**: AWS SageMaker Feature Store ensuring online/offline synchronization and preventing Data Leakage.
  * **Model Serving & MLOps**: Real-time Inference using SageMaker Endpoints (REST API, Auto-scaling) and Batch Transform for large datasets; pipeline automation via SageMaker Pipelines and drift monitoring with SageMaker Model Monitor.
  * **XAI & Bias Detection**: SageMaker Clarify for model explainability and bias detection.

---

### 3. Key Takeaways & Knowledge Gained

* **Cloud & Infrastructure**:
  * Thorough comprehension of the Shared Responsibility Model for configuring security across operating systems, IAM, and data encryption.
  * Deep insight into the AWS Nitro System and Hybrid networking with AWS Outposts.
* **System Design**:
  * Key evaluation questions before designing: Scale, Read/Write ratio, Durability, Latency, and Cost.
  * Stateless architectures enabling seamless Horizontal Scaling alongside multi-tier caching and Load Balancers.
  * Mastery of database scalability techniques: Replication (lag, failover), Sharding (shard key, consistent hashing), and proper Indexing.
* **AI & Machine Learning (MLOps)**:
  * A trained model in a Jupyter Notebook is not a production solution; MLOps is mandatory for load handling, feature parity, and continuous retraining upon data drift.
  * Packaging models into REST APIs (FastAPI) or interactive frontends (Streamlit/Gradio) demonstrates true end-to-end engineering capability.

---

### 4. Event Impressions & Reflections

* The workshop sessions delivered practical, highly structured industry perspectives, connecting academic theory with enterprise production architectures.
* Detailed hardware analysis (CPU Steal on VPS, NUMA memory architectures on VDS, and the AWS Nitro System) cleared up widespread misconceptions in server selection.
* The comprehensive overview of MLOps on AWS SageMaker and systematic System Design principles formed a clear framework for building resilient applications capable of scaling to millions of users.

---

### 5. Lessons Learned

1. **Size servers according to actual workload**: Avoid over-engineering from day one; evaluate across 4 pillars: **Cost, Predictability, Compliance, and Scale**.
2. **Look beyond isolated machine learning notebooks**: Do not stop at Kaggle competitions or `.ipynb` files – build production-ready thinking (REST APIs, monitoring, Feature Stores, and CI/CD pipelines).
3. **Purposeful system design**: Introduce architectural components (Load Balancers, Caching, Read Replicas, Sharding) only when genuine bottlenecks emerge.
4. **Security is a shared responsibility**: Proactively manage encryption, security groups, and IAM policies rather than assuming the cloud provider covers all layers.
