# 📦 Titan Event Consumer Library (`titan-event-consumer-lib`)

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://openjdk.org/)
[![Spring Kafka](https://img.shields.io/badge/Spring%20Kafka-3.1.2-brightgreen.svg)](https://spring.io/projects/spring-kafka)

## 📖 Overview
The **Titan Event Consumer Library** is a shared Java library providing a standard framework for consuming Kafka events across Titan microservices (`titan-notifications-service`, `titan-promotions-service`, etc.).

---

## ⚡ Core Technical Features
- **`BaseEventConsumer<T>`**: Reusable template consumer with pre-configured JSON deserialization, MDC trace logging, and exception boundaries.
- **Automated DLQ & Poison Pill Handling**:
  - Automatically isolates unparseable payloads to `banking.transactions.dlq`.
  - Routes fatal consumer errors to `banking.transactions.poison` without interrupting continuous topic streaming.
- **Standard Kafka Configuration**: Consistent concurrency, backoff retry policies, and SSL/PLAINTEXT negotiation across microservices.

---

## 📦 Integration
Include in any Titan Spring Boot microservice `pom.xml`:
```xml
<dependency>
    <groupId>com.titan</groupId>
    <artifactId>titan-event-consumer-lib</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```
