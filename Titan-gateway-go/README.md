# 🛡️ Titan API Gateway (`Titan-gateway-go`)

[![Golang](https://img.shields.io/badge/Go-1.22-blue.svg)](https://golang.org/)
[![JWT](https://img.shields.io/badge/Auth-HMAC--SHA256%20JWT-black.svg)](https://jwt.io/)
[![Reverse Proxy](https://img.shields.io/badge/Net-ReverseProxy-success.svg)](https://pkg.go.dev/net/http/httputil)

## 📖 Overview
The **Titan API Gateway** is a blazing-fast, lightweight edge reverse proxy written in Go. It serves as the single unified entry point for all mobile (iOS), web, and external partner traffic, providing centralized authentication, rate limiting, and request routing.

---

## ⚡ Core Technical Features
- **Zero-Latency Reverse Proxying**: Built with Go's `net/http/httputil.ReverseProxy` with connection pooling and automated header enrichment (`X-Gateway`, `X-Real-IP`, `X-Forwarded-Host`).
- **Sliding-Window Rate Limiter & IP Jail**: Tracks client IP request frequency within configurable sliding windows (e.g. 100,000 req / 60s) and automatically jails abusers.
- **Stateless HMAC-SHA256 JWT Verification**: Validates token signatures in memory without hitting the database on every request, bypassing public routes (e.g., `/api/v1/auth/login`, `/health`).
- **Dynamic Upstream Discovery**: Routes path prefixes seamlessly to Docker container DNS names or local ports.

---

## 🛣️ Routing Table

| Path Pattern | Target Upstream Service | Auth Requirement |
| :--- | :--- | :--- |
| `/api/v1/auth/**` | `titan-core-banking` (:8080) | Public |
| `/api/auth/otp/**` | `titan-core-banking` (:8080) | Public |
| `/api/v1/accounts/**` | `titan-core-banking` (:8080) | Bearer JWT |
| `/api/v1/transactions/**` | `titan-core-banking` (:8080) | Bearer JWT |
| `/api/v1/atm/**` | `titan-core-banking` (:8080) | Bearer JWT |
| `/api/v1/qr/**` | `titan-core-banking` (:8080) | Bearer JWT |
| `/api/notify/**` | `titan-notifications-service` (:8084) | Bearer JWT |
| `/api/preferences/**` | `titan-notifications-service` (:8084) | Bearer JWT |
| `/api/v1/promotions/**`| `titan-promotions-service` (:8083) | Bearer JWT |
| `/api/quests/**` | `titan-promotions-service` (:8083) | Bearer JWT |
| `/api/referrals/**` | `titan-promotions-service` (:8083) | Bearer JWT |
| `/api/ai/**` | `titan-ai-service` (:8085) | Bearer JWT |
| `/health` | Gateway Local Health Endpoint | Public |

---

## 📦 Build & Run
```bash
# Run locally using Go
go run main.go

# Build standalone binary
go build -o titan-gateway .
./titan-gateway
```
