# System Design Document - mystsh

## 1. High-Level Architecture Overview

mystsh follows a mobile-first, cloud-native architecture. The system is designed to be highly secure, real-time, and scalable.

### Component Diagram (Conceptual)
```mermaid
graph TD
    A[Teen Mobile App (React Native/Flutter)] --> B[API Gateway (Kong/AWS)]
    C[Parent Web/Mobile App] --> B
    B --> D[Backend Services (Node.js/Go)]
    D --> E[(Main Database: PostgreSQL)]
    D --> F[(Cache/Session: Redis)]
    D --> G[External Card Issuer API (Stripe/Marqeta)]
    D --> H[Digital Wallet APIs (Apple/Google Pay)]
    G --> I[Transaction Webhook Listener]
    I --> D
    D --> J[Notification Service (Firebase/OneSignal)]
```

## 2. Component Breakdown

### 2.1. Client Apps
- **Teen App:** Focuses on low-friction payments and gamified literacy. Features native device wallet integration.
- **Parent App:** Heavy on management and monitoring. Provides high-level insights and granular control settings.

### 2.2. Backend Services
- **Auth Service:** Manages multi-tenant identity (parent and teen roles), OAuth2/OIDC, and biometric verification.
- **Card Provisioning Service:** Orchestrates communication with third-party card issuers (e.g., Marqeta, Stripe Issuing) to create virtual sub-cards.
- **Transaction Engine:** Processes real-time transaction webhooks from the card network, applies parent-defined rules, and updates account balances.
- **Literacy & Gamification Service:** Manages educational content (quests), point balances, and reward redemption.
- **Notification Service:** Dispatches real-time push notifications to both parent and teen devices for every spend event.

### 2.3. Data Storage
- **PostgreSQL:** Primary relational store for user profiles, account relationships, transaction logs, and spending rules.
- **Redis:** Used for session management, real-time transaction caching (to ensure rapid authorization), and task queues.

## 3. Key Technical Workflows

### 3.1. Virtual Card Provisioning
1. Parent requests a new card for the teen.
2. Backend calls the external issuer's API (e.g., Marqeta) to create a "Child Account" and issue a virtual card.
3. The issuer returns a tokenized card representation.
4. mystsh backend provides the encrypted card data to the teen app.
5. Teen app uses the Apple/Google Pay SDKs to "Add to Wallet."

### 3.2. Real-time Transaction Flow
1. Teen makes a purchase via Apple Pay.
2. The card network (Visa/Mastercard) notifies the card issuer (Stripe/Marqeta).
3. The issuer sends a webhook to the mystsh `Webhook Listener`.
4. The `Transaction Engine` verifies the spending rules (limits, category restrictions).
5. If allowed, the transaction is logged, the parent is notified, and the teen app reflects the update instantly via WebSockets or push.

## 4. Security & Compliance

### 4.1. Data Security
- **Encryption at Rest:** All sensitive user data is encrypted in the database using AES-256.
- **Encryption in Transit:** All API communication is secured via TLS 1.3.
- **Tokenization:** mystsh NEVER stores raw PANs (Primary Account Numbers) or CVVs. All card data is handled via issuer-provided tokens.

### 4.2. Identity & Access
- **Multi-Factor Authentication (MFA):** Mandatory for all parent accounts.
- **Parent-Child Logic:** Strict RBAC (Role-Based Access Control) to ensure teens cannot modify their own spending limits.

### 4.3. Compliance
- **PCI-DSS Level 1:** Adherence to all standards for payment data handling.
- **COPPA/GDPR Compliance:** Ensuring data privacy for users under 18, including verifiable parental consent for data processing.

## 5. Scalability & Performance
- **Microservices:** Decoupled services to allow independent scaling of the high-traffic transaction engine.
- **Read Replicas:** Database read replicas to handle analytics and reporting queries without impacting transaction performance.
- **Event-Driven Architecture:** Using Kafka or RabbitMQ for non-critical paths like logging and reward point updates.
