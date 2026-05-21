# Project Trident

## Frontend Layer

* Angular 17
* TypeScript 5
* Angular Material
* Angular CDK
* SCSS
* RxJS
* NGINX

---

# Backend Platform

* Java 21 LTS
* Spring Boot 3
* Spring WebFlux
* Project Reactor
* Spring Cloud
* Spring Cloud Gateway
* Spring Security
* JWT Authentication
* Maven

---

# Core Microservices

* API Gateway Service
* Authentication Service
* Product Service
* Verification Service
* Review & Feedback Service
* Search Service
* Recommendation Service

---

# Data Layer

## MySQL

Used for:

* User management
* Authentication data
* Product catalog
* Vendor management
* Core transactional data
* Relational business workflows

---

## MongoDB

Used for:

* Reviews & feedback
* Verification evidence
* Recommendation metadata
* Audit history
* Flexible document storage
* AI-generated content metadata

---

## OpenSearch

Used for:

* Full-text search
* Semantic-ready discovery
* Autocomplete
* Fuzzy matching
* Dynamic filtering
* Intelligent ranking
* Technology-aware search experience

---

## Redis

Used for:

* Distributed caching
* Token blacklist management
* API rate limiting
* Session optimization
* Hot recommendation cache

---

# Messaging & Event Streaming

* Apache Kafka
* Zookeeper
* Event-Driven Communication
* Asynchronous Processing Pipelines

---

# AI / GenAI Stack

## AI Engineering & GenAI

* Generative AI (GenAI)
* AI Engineering
* Retrieval-Augmented Generation (RAG)
* Semantic Search
* Embedding-Based Retrieval
* AI-Assisted Recommendation Reasoning
* Explainable AI Recommendations

---

## AI Frameworks & Integration

* Spring AI
* LangChain4j
* OpenAI API
* Ollama (Local LLM Runtime)

---

## AI Vector Data Layer

### pgvector (PostgreSQL Extension)

or

### Qdrant

Used for:

* Vector embeddings
* Semantic retrieval
* Context-aware AI search
* Recommendation context storage
* Similarity search pipelines

---

# AI-Powered Features

* AI-powered technology discovery
* Semantic product search
* Intelligent product comparison
* AI-assisted recommendation reasoning
* Technology explanation generation
* AI verification summaries
* Context-aware recommendation assistance
* Future-ready AI search workflows

---

# AI Microservices

* AI Recommendation Service
* RAG Service
* Embedding Service

---

# Security Layer

* Spring Security Reactive
* JWT Authentication
* RBAC (Role-Based Access Control)
* API Gateway Security Policies
* Token-based Authorization

---

# Resilience & Reliability

## Resilience4j

* Circuit Breaker
* Retry
* Bulkhead
* Rate Limiter
* Fault Tolerance Patterns

---

# Monitoring & Observability

* Prometheus
* Grafana
* Micrometer
* Spring Boot Actuator

## AI Observability

* Langfuse
* Prompt Logging
* AI Trace Monitoring
* LLM Request Tracking

---

# Logging & Analytics

* Structured JSON Logging
* OpenSearch Dashboards
* Centralized Log Aggregation
* Logstash (Planned)

---

# API Documentation

* OpenAPI / Swagger
* SpringDoc OpenAPI

---

# DevOps & Infrastructure

* Docker
* Docker Compose
* Multi-stage Dockerfiles
* GitHub Actions
* Containerized Development Environment

---

# Testing Stack

* JUnit 5
* Mockito
* Testcontainers
* WireMock
* Integration & Contract Testing

---

# Developer Tooling

* Lombok
* MapStruct
* VS Code
* Cursor IDE

---

# Architecture Principles

* Reactive Microservices Architecture
* Event-Driven Architecture
* Polyglot Persistence
* API Gateway Pattern
* Search Projection Architecture
* AI-Enhanced Discovery Architecture
* Scalable Distributed System Design

---

# Final Infrastructure

```text
frontend-nginx

api-gateway
auth-service
product-service
verification-service
review-service
search-service
recommendation-service

ai-recommendation-service
rag-service
embedding-service

mysql
mongodb
redis

postgres-pgvector

kafka
zookeeper

opensearch
opensearch-dashboards

ollama

prometheus
grafana
langfuse
```

---

# High-Level System Flow

```text
Angular Frontend
        ↓
NGINX Reverse Proxy
        ↓
API Gateway
        ↓
----------------------------------------------------------------
| Auth | Product | Verification | Review | Search | Recommendation |
----------------------------------------------------------------
        ↓
MySQL + MongoDB + Redis
        ↓
Kafka Event Streaming Layer
        ↓
OpenSearch + Vector Search Layer
        ↓
AI Services (RAG + Embeddings + Recommendations)
        ↓
Monitoring, Logging & Observability Stack
```
