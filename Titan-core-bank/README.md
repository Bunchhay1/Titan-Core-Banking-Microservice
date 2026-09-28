# 🏛️ Titan Core Banking Service (`titan-core-banking`)

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.3-brightgreen.svg)](https://spring.io/)
[![Java](https://img.shields.io/badge/Java-21%20Virtual%20Threads-orange.svg)](https://openjdk.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue.svg)](https://postgresql.org/)
[![Kafka](https://img.shields.io/badge/Kafka-Outbox%20Pattern-black.svg)](https://kafka.apache.org/)

## 📖 Overview
The **Titan Core Banking Service** is the central ledger engine of the Titan banking platform. It handles account management, double-entry bookkeeping, funds transfers, KHQR generation/parsing, ATM cardless withdrawals, fixed deposits, and bank statement generation.

---

## ⚡ Core Technical Features
- **Project Loom Virtual Threads**: Configured via `spring.threads.virtual.enabled=true` for ultra-high concurrency and low memory overhead under high transactions per second (TPS).
- **Double-Entry Ledger Architecture**: Every transfer executes balanced atomic debit and credit operations in PostgreSQL under strict `READ_COMMITTED` transaction isolation with row-level locks.
- **Real-Time AI Fraud Evaluation**: Integrates with `titan-ai-service` via high-speed gRPC (`risk_engine.proto`) protected by Resilience4j Circuit Breakers.
- **Transactional Outbox & Kafka Publisher**: Emits domain events (`banking.transactions.completed`, `banking.accounts.created`) reliably without dual-write inconsistency.
- **National QR (KHQR) & ATM Cardless Engine**: Generates and verifies cryptographic EMVCo KHQR payloads and one-time ATM withdrawal authorization codes.

---

## 🛣️ Key REST Endpoints

### 1. Authentication & Security
- `POST /api/v1/auth/register` - Create customer credentials & profile
- `POST /api/v1/auth/login` - Authenticate customer and issue signed JWT token
- `POST /api/auth/otp/generate` - Generate OTP for sensitive workflows

### 2. Accounts & Balances
- `GET /api/v1/accounts` - List all accounts for authenticated user
- `POST /api/v1/accounts` - Create savings / checking / multi-currency account
- `GET /api/v1/accounts/{accountNumber}/balance` - Real-time account balance

### 3. Transactions & Transfers
- `POST /api/v1/transactions/transfer` - Domestic/internal funds transfer
- `POST /api/v1/transactions/deposit` - Cash / check deposit simulation
- `POST /api/v1/transactions/withdraw` - Cash withdrawal
- `GET /api/v1/transactions/history` - Paginated transaction history

### 4. ATM & QR Code Payments
- `POST /api/v1/atm/generate` - Generate cardless ATM 6-digit withdrawal code
- `POST /api/v1/atm/redeem` - Redeem cardless cash at ATM terminal
- `POST /api/v1/qr/generate` - Generate dynamic KHQR payment payload
- `POST /api/v1/qr/pay` - Process payment against scanned KHQR string

---

## 📦 Build & Run
```bash
# Build standalone JAR
mvn clean package -DskipTests

# Run locally with active profile
java -jar target/titan-core-banking-2.0.0-SNAPSHOT.jar --spring.profiles.active=dev
```
