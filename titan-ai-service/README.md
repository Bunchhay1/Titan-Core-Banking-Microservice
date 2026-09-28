# 🧠 Titan AI Risk Engine (`titan-ai-service`)

[![Python](https://img.shields.io/badge/Python-3.11-yellow.svg)](https://python.org/)
[![gRPC](https://img.shields.io/badge/gRPC-Protobuf%20v3-4285F4.svg)](https://grpc.io/)
[![FastAPI](https://img.shields.io/badge/HTTP-FastAPI%20%2F%20HTTP-009688.svg)](https://fastapi.tiangolo.com/)

## 📖 Overview
The **Titan AI Risk Engine** is a high-performance Python microservice designed for real-time transaction risk scoring and anomaly detection. It serves both synchronous **gRPC** calls for in-flight transaction evaluation and asynchronous **REST/HTTP** diagnostic reporting.

---

## ⚡ Core Technical Features
- **High-Speed gRPC Protocol**: Exposes port `50051` using Protobuf binary serialization to achieve sub-10ms evaluation latency for `titan-core-banking`.
- **Heuristic & Statistical Fraud Scoring**:
  - Velocity analysis (rapid consecutive transactions)
  - Amount deviation against historical baselines
  - Geolocation jump anomalies
  - Account blacklisting & suspicious pattern detection
- **Health Probing**: Supports both HTTP `/health` on port `8085` and native `grpc_health_probe` on port `50051`.

---

## 📜 Protobuf Definition (`risk_engine.proto`)
```protobuf
syntax = "proto3";
package titan.risk;

service RiskEngineService {
    rpc AssessRisk (RiskAssessmentRequest) returns (RiskAssessmentResponse);
    rpc CheckHealth (HealthCheckRequest) returns (HealthCheckResponse);
}

message RiskAssessmentRequest {
    string transaction_id = 1;
    string source_account = 2;
    string target_account = 3;
    double amount = 4;
    string currency = 5;
    string transaction_type = 6;
}

message RiskAssessmentResponse {
    double risk_score = 1;         // 0.0 (Safe) to 1.0 (Critical Risk)
    string decision = 2;           // "APPROVED", "FLAGGED", "REJECTED"
    string reason = 3;
    int64 latency_ms = 4;
}
```

---

## 📦 Build & Run
```bash
# Install dependencies
pip install -r requirements.txt

# Generate gRPC stubs
python -m grpc_tools.protoc -I. --python_out=./protos --grpc_python_out=./protos risk_engine.proto

# Start the service
python main.py
```
