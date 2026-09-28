# 🎁 Titan Promotions & Gamification Service (`titan-promotions-service`)

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.3-brightgreen.svg)](https://spring.io/)
[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://openjdk.org/)
[![PostGIS](https://img.shields.io/badge/Spatial-PostGIS%203.4-blue.svg)](https://postgis.net/)
[![Kafka](https://img.shields.io/badge/Kafka-Streams%20%26%20Consumer-black.svg)](https://kafka.apache.org/)

## 📖 Overview
The **Titan Promotions Service** orchestrates banking rewards, real-time cashback calculation, gamified customer quests, referral incentives, and merchant-partner geolocation campaigns.

---

## ⚡ Core Technical Features
- **Kafka Event Streaming**: Consumes `banking.transactions.completed` to instantly evaluate cashback eligibility and quest completion criteria.
- **PostGIS Geofencing**: Uses spatial indexes in PostgreSQL (`geometry(Point, 4326)`) to trigger nearby merchant discounts when users initiate transactions in partner zones.
- **Redisson Distributed Locks**: Prevents race conditions during limited-quantity promotional coupon redemption and budget quota depletion.
- **Referral Graph Engine**: Multi-tier referral tracking rewarding both referrers and newly onboarded customers upon qualifying activity.

---

## 🛣️ Key REST Endpoints
- `GET /api/v1/promotions/active` - List all active marketing campaigns and cashback offers
- `POST /api/v1/promotions/claim` - Claim eligible voucher or reward code
- `GET /api/quests` - View customer banking quests, challenges, and progress
- `POST /api/quests/{questId}/claim` - Collect rewards for completed quests
- `GET /api/referrals/my-code` - Get customer referral invite code and link
- `GET /api/referrals/stats` - View referral hierarchy and earnings

---

## 📦 Build & Run
```bash
# Build standalone fat JAR with Maven
mvn clean package -DskipTests

# Run with local config
java -jar target/titan-promotions-service-0.0.1-SNAPSHOT.jar
```
