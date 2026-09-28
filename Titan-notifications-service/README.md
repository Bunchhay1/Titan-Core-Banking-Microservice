# 🔔 Titan Notifications Service (`titan-notifications-service`)

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.3-brightgreen.svg)](https://spring.io/)
[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://openjdk.org/)
[![Kafka](https://img.shields.io/badge/Kafka-Consumer%20Group-black.svg)](https://kafka.apache.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue.svg)](https://postgresql.org/)

## 📖 Overview
The **Titan Notifications Service** is an asynchronous, event-driven microservice responsible for dispatching multi-channel alerts (SMS, Email, Push Notifications, In-App Notifications) triggered by banking domain events or direct API requests.

---

## ⚡ Core Technical Features
- **Kafka Event Consumer**: Listens to `banking.transactions.completed` under the consumer group `notification-service-group` with idempotent message handling.
- **Multi-Provider Strategy**:
  - **SMS**: Primary (Twilio) with automatic failover to Secondary (AWS SNS).
  - **Email**: Primary (SendGrid) with automatic failover to Secondary (AWS SES).
  - **Push**: Apple Push Notification service (APNs) & Firebase Cloud Messaging (FCM).
- **Dead-Letter Queue (DLQ) & Resilience**: Configured with Spring Retry and Resilience4j circuit breakers to forward persistent delivery failures to `banking.notifications.dlq`.
- **Dynamic Templating**: HTML & text email rendering using FreeMarker template engine with multi-language i18n support.

---

## 🛣️ Key REST Endpoints
- `POST /api/notify/send` - Direct programmatic notification dispatch
- `GET /api/preferences/{userId}` - Retrieve customer notification channel preferences
- `PUT /api/preferences/{userId}` - Update SMS/Email/Push notification opt-in settings
- `GET /api/audit/logs` - Query historical delivery status and provider audit trails
- `POST /api/webhooks/{provider}` - Webhook callback handler for delivery receipts (SendGrid, Twilio)

---

## 📦 Build & Run
```bash
# Build standalone fat JAR using Maven
mvn clean package -DskipTests

# Run with local profile
java -jar target/titan-notifications-service-0.0.1-SNAPSHOT.jar --spring.profiles.active=docker
```
