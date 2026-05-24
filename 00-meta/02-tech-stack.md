# Project Trident
## Frontend

- Angular 17
    
- TypeScript 5
    
- Angular Material
    
- Angular CDK
    
- SCSS
    
- RxJS
    
- NGINX
    

---

# Backend

- Java 21 LTS
    
- Spring Boot 3
    
- Spring WebFlux
    
- Project Reactor
    
- Spring Cloud
    
- Spring Cloud Gateway
    
- Spring Security
    
- JWT Authentication
    
- Maven
    

---

# Microservices

- API Gateway Service
    
- Auth Service
    
- Product Service
    
- Verification Service
    
- Review & Feedback Service
    
- Search Service
    
- Recommendation Service
    

---

# Databases

## MySQL

Used for:

- users
    
- auth
    
- products
    
- vendors
    
- transactional/core relational data
    

---

## MongoDB

Used for:

- reviews
    
- verification evidence
    
- recommendation metadata
    
- audit history
    
- flexible documents/content
    

---

## OpenSearch

Used for:

- full-text search
    
- autocomplete
    
- fuzzy search
    
- filtering
    
- ranking
    
- technology-aware discovery
    

---

## Redis

Used for:

- caching
    
- token blacklist
    
- rate limiting
    
- hot recommendation cache
    

---

# Messaging & Streaming

- Apache Kafka
    
- Zookeeper
    

---

# Monitoring & Observability

- Prometheus
    
- Grafana
    
- Micrometer
    
- Spring Boot Actuator
    

---

# Logging Stack

- OpenSearch Dashboards
    
- Logstash (later)
    
- Structured JSON Logging
    

---

# Resilience

- Resilience4j
    
    - Circuit Breaker
        
    - Retry
        
    - Bulkhead
        
    - Rate Limiter
        

---

# API Documentation

- OpenAPI / Swagger
    
- SpringDoc OpenAPI
    

---

# Security

- Spring Security Reactive
    
- JWT
    
- RBAC
    

---

# DevOps & Infrastructure

- Docker
    
- Docker Compose
    
- Multi-stage Dockerfiles
    
- GitHub Actions
    

---

# Testing

- JUnit 5
    
- Mockito
    
- Testcontainers
    
- WireMock
    

---

# Developer Tooling

- Lombok
    
- MapStruct
    
- VS Code / Cursor
    

---

# Architecture Style

- Reactive Microservices
    
- Event-Driven Architecture
    
- Polyglot Persistence
    
- API Gateway Pattern
    
- Search Projection Architecture

- Change By KV

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

mysql
mongodb
redis

kafka
zookeeper

opensearch
opensearch-dashboards

prometheus
grafana
```

---

# Final System Flow

```text
Angular Frontend
        ↓
NGINX
        ↓
API Gateway
        ↓
------------------------------------------------
| Auth | Product | Verification | Review |
| Search | Recommendation |
------------------------------------------------
        ↓
MySQL + MongoDB + Redis
        ↓
Kafka Event Streaming
        ↓
OpenSearch Search Layer
        ↓
Monitoring & Dashboards
```
