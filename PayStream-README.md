# 🚀 PayStream --- Instant Payments Platform

Lloyds Bank Technology Hackathon Project\
Java 17 \| Spring Boot 3 \| Apache Kafka \| H2 \| Docker Compose

------------------------------------------------------------------------

# 📌 Overview

PayStream is a high-throughput Instant Payments Processing System
designed to simulate a real-world Faster Payments architecture.

It consists of two independent microservices:

-   payment-ingestor (8080) → Validates and publishes payment requests
-   payment-processor (8081) → Consumes, applies business rules,
    persists outcomes, and exposes reporting APIs

Kafka is used as the central asynchronous event backbone.

------------------------------------------------------------------------

# 🏗️ System Architecture

Client → payment-ingestor → Kafka → payment-processor → H2 DB +
Reporting APIs

------------------------------------------------------------------------

# ⚙️ Tech Stack

Java 17, Spring Boot 3, Kafka, Spring Data JPA, H2, Docker Compose, Bean
Validation

------------------------------------------------------------------------

# 🔁 Payment Flow

1.  Client sends payment request
2.  Ingestor validates accounts
3.  Publishes PaymentEvent to Kafka
4.  Processor consumes event
5.  Applies business rules
6.  Stores PaymentOutcome in H2
7.  Publishes processed event
8.  Metrics updated

------------------------------------------------------------------------

# 📡 Kafka Topics

-   payments.submitted (6 partitions)
-   payments.processed (6 partitions)

Partition Key: debitAccountId

------------------------------------------------------------------------

# 📥 payment-ingestor

Endpoints: - POST /api/payments - GET /api/accounts/{id}

Validations: - Account must exist - Must be ACTIVE - Duplicate paymentId
rejected

------------------------------------------------------------------------

# ⚙️ payment-processor

Endpoints: - /api/metrics/summary - /api/reports/summary -
/api/reports/activity - /api/accounts/{id}/history

Business Rules: - \> 250,000 → HELD - else → PROCESSED

------------------------------------------------------------------------

# 🧠 Design Principles

-   Event-driven architecture
-   Idempotent processing
-   Microservice isolation
-   Partition-based scaling
-   Async processing via Kafka

------------------------------------------------------------------------

# 🐳 Run

docker-compose up -d\
mvn spring-boot:run (both services)

------------------------------------------------------------------------

# 🚀 End
