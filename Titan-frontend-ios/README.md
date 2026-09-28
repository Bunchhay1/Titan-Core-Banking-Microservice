# 📱 Titan Native iOS Banking App (`Titan-frontend-ios`)

[![Swift](https://img.shields.io/badge/Swift-5.10-F05138.svg)](https://swift.org/)
[![iOS](https://img.shields.io/badge/iOS-17.0%2B%20%7C%20iPhone%2017%20Pro%20Max-000000.svg)](https://developer.apple.com/ios/)
[![SwiftUI](https://img.shields.io/badge/UI-SwiftUI%20%2B%20Combine-blue.svg)](https://developer.apple.com/xcode/swiftui/)
[![Xcode](https://img.shields.io/badge/Xcode-15%2B%20%2F%2016%2B-1575F9.svg)](https://developer.apple.com/xcode/)

## 📖 Overview
The **Titan iOS Application** is a production-grade native banking client engineered with SwiftUI, Combine, and modern Swift concurrency (`async/await`). It interfaces directly with the Titan API Gateway on port `8088`.

---

## ⚡ Core Client Features
- **Gateway Single-Entry Point (`APIClient.swift`)**:
  - Automatically targets `http://localhost:8088` on iOS Simulator.
  - Automatically targets Mac LAN IP (e.g. `http://10.30.0.53:8088`) when running on physical iPhone test devices.
- **Biometric Security & Keychain Storage**: Secure enclave authentication via Face ID / Touch ID and encrypted JWT bearer token storage.
- **Interactive Banking Workflows**:
  - Real-time balance visualization and multi-currency accounts
  - Double-entry funds transfer with beneficiary management
  - Dynamic KHQR code generation and camera scanning
  - ATM Cardless cash withdrawal code generation
  - In-app notification center and promotional quest progression
- **Modern iOS 17+ / iPhone 17 Pro Max UI**: Dynamic Island notifications, haptic feedback, dark mode, smooth spring animations, and offline caching.

---

## 🚀 Running on iPhone 17 Pro Max Simulator

### Option A: Command Line Build & Run
```bash
# Build the project for iPhone 17 Pro Max Simulator
xcodebuild -scheme Titan_Banking \
  -destination 'platform=iOS Simulator,name=iPhone 17 Pro Max' \
  build
```

### Option B: Xcode Interactive IDE
1. Open `Titan_Banking.xcodeproj` in Xcode:
   ```bash
   open Titan_Banking.xcodeproj
   ```
2. In the top toolbar, select **Titan_Banking** scheme and target **iPhone 17 Pro Max**.
3. Press **`Cmd + R`** to compile and launch the application in the simulator.
