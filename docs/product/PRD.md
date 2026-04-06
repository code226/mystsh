# Product Requirements Document (PRD) - mystsh

## 1. Product Overview
**Name:** mystsh ("my stash")
**Tagline:** Financial freedom for the next generation.
**Vision:** To provide teenagers with safe, educational, and rewarding access to digital payments by bridging the gap between parents' existing financial accounts (Wise, Revolut, Koho) and the teen's digital wallet.

## 2. Target Audience
- **Primary Users:** Teenagers aged 13-18 who want digital payment access and rewards.
- **Decision Makers:** Parents or legal guardians seeking a secure way to teach financial literacy.

## 3. Problem Statement
Teenagers under 18 face barriers to financial independence:
- They cannot legally own most credit cards.
- They live in a cashless society where digital wallets are the standard.
- Traditional youth bank accounts lack modern features and integration.
- Parents struggle to monitor and teach financial responsibility in a digital-first environment.

## 4. Key Features

### 4.1. Digital Wallet Integration
- **Virtual Card Issuance:** Provisioning of virtual sub-cards linked to a parent's funding source (e.g., Wise, Revolut, Koho).
- **Apple/Google Pay Support:** Seamlessly add virtual cards to native device wallets.
- **Contactless Payments:** Enable tap-to-pay at physical and online merchants.

### 4.2. Parent Control Dashboard
- **Funding Source Management:** Securely connect parent cards via tokenization.
- **Granular Spending Controls:** Set daily/weekly/monthly limits.
- **Merchant & Category Controls:** Toggle permissions for specific categories (e.g., Food & Dining, Gaming, Entertainment).
- **Real-time Monitoring:** Instant push notifications for every transaction.
- **Instant Freeze:** Ability to disable/enable the teen's card instantly with one tap.

### 4.3. Teen Dashboard & Financial Tracking
- **Modern UI:** High-energy "Dark Mode" aesthetic with Neon Green and Electric Blue accents.
- **Balance & Spending View:** Intuitive UI showing current balance and real-time transaction history.
- **Request Extra Funds:** A "Financial Handshake" flow allowing teens to request money from parents for specific needs (e.g., cinema tickets).
- **Savings Goals:** Set and track progress towards specific targets with visual progress bars.

### 4.4. Financial Literacy & Rewards
- **Literacy Quests:** Gamified interactive modules (e.g., "The Magic of Compounding").
- **Stash Points:** Earn points for completing quests or meeting savings goals.
- **Redemption Marketplace:** Redeem points for partner rewards (e.g., Amazon gift cards) or "savings boosts."

## 5. Non-Functional Requirements
- **Security:** PCI-DSS Level 1 compliance, AES-256 encryption at rest, TLS 1.3 in transit.
- **Compliance:** Verifiable Parental Consent (VPC) for COPPA/GDPR adherence.
- **Accessibility:** WCAG 2.1 AA compliance (high contrast, touch target optimization).
- **Scalability:** Event-driven architecture to handle high-volume transaction webhooks.

## 6. User Journeys (Refined)

### 6.1. Onboarding (Parent & Teen)
1. Parent downloads mystsh, completes identity verification, and links a Wise/Revolut/Koho card.
2. Parent sends a secure invite to the teen.
3. Teen accepts, profiles are linked, and the parent approves the virtual card provisioning.

### 6.2. The "Financial Handshake"
1. Teen requests $15 for a cinema ticket via the app.
2. Parent receives a real-time notification with the request and reason.
3. Parent taps "Approve," and funds are instantly accessible in the teen's digital wallet.

### 6.3. Daily Literacy Quest
1. Teen completes a 2-minute "Spotting Scams" module.
2. Teen earns 50 Stash Points and sees progress towards their next reward.

## 7. Success Metrics
- **User Growth:** Number of active parent-teen pairs.
- **Literacy Impact:** Percentage of users who complete at least one quest per month.
- **Engagement:** Daily active users (DAU) and frequency of "Financial Handshake" requests.
