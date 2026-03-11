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
 
   <img width="434" height="497" alt="Image" src="https://github.com/user-attachments/assets/9d0d5a23-3e41-41f4-9b9f-93fb1aed089f" />
   
   <img width="1348" height="764" alt="Image" src="https://github.com/user-attachments/assets/03d2936a-0048-4875-91ff-88196c59d09a" />
   
<img width="1869" height="819" alt="Image" src="https://github.com/user-attachments/assets/c8c454e0-16c6-4be9-9197-cb661f47ab19" />

2. Attempt login on **Edge** with same credentials.
   
<img width="627" height="311" alt="Image" src="https://github.com/user-attachments/assets/d4211ea0-3c1c-41ab-a856-c27f79c4b477" />

3. The server detects a fingerprint mismatch, revokes the Chrome session, and grants access to Edge.
4. The Chrome "Heartbeat" detects the revocation within 3 seconds and triggers an automatic logout.
<img width="714" height="255" alt="Image" src="https://github.com/user-attachments/assets/0f36e20a-e523-40de-be6f-ffca925e67f1" />

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
