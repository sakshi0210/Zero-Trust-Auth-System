# Zero-Trust-Auth-System
# Practical Zero Trust Authentication System

A full-stack web application implementing **Zero Trust Security** principles. This project moves beyond traditional static authentication by enforcing **Continuous Verification** and **Identity-Device Binding**.

## 🚀 The Core "Novelty"
Unlike standard login systems, this project implements:
- **Continuous Authentication:** Verifies every API request via a 3-second heartbeat.
- **Hardware Fingerprinting:** Binds JWT sessions to specific browser hardware profiles using `FingerprintJS`.
- **Contextual Trust Scoring:** Dynamically calculates a security score based on IP stability and User-Agent profiles.
- **Single Device Policy:** Automatically revokes sessions in real-time if a login is detected on a new browser/device.

## 🛠️ Tech Stack
- **Frontend:** React.js, React Router, Context API
- **Backend:** Node.js, Express.js
- **Database:** PostgreSQL
- **Security:** JWT (JSON Web Tokens), FingerprintJS, Bcrypt

## ⚙️ Methodology
The system follows a three-step enforcement stack:
1. **Identity Check:** Validates the cryptographic signature of the JWT.
2. **Device Identity Check:** Matches the incoming hardware fingerprint against the database.
3. **Trust Scoring:** Subtracts points for "Contextual Drift" (IP or User-Agent changes). If the score falls below 40%, access is denied.

## 📸 Demo Scenarios
### The "Kill-Switch" Demonstration
1. Login on **Chrome**. Dashboard access is granted (Trust Score: 100%).
2. Attempt login on **Edge** with same credentials.
3. The server detects a fingerprint mismatch, revokes the Chrome session, and grants access to Edge.
4. The Chrome "Heartbeat" detects the revocation within 3 seconds and triggers an automatic logout.

## 🛠️ Installation & Setup

### Prerequisites
- Node.js installed
- PostgreSQL database running

### Server Setup
1. Navigate to `/server`
2. Install dependencies: `npm install`
3. Create a `.env` file based on `.env.example`.
4. Run the database schema: `psql -f schema.sql`
5. Start the server: `node app.js`

### Client Setup
1. Navigate to `/client`
2. Install dependencies: `npm install`
3. Start the application: `npm start`

## 🔒 Security Principles Applied
- **Never Trust, Always Verify:** No session is trusted based on a cookie alone.
- **Least Privilege:** Role-based access control (RBAC) via JWT claims.
- **Explicit Verification:** Hardware-bound identity verification.
