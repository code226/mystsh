# Product Requirements Document (PRD) - mystsh

## 1. Product Overview
**Name:** mystsh ("my stash")
**Tagline:** Financial freedom for the next generation.
**Vision:** To provide teenagers with a gamified window into their digital spending and savings by bridging the gap between parents' existing accounts (Wise, Revolut, Koho) and the teen's mobile dashboard.

## 2. Target Audience
- **Primary Users:** Teenagers aged 13-18 who use their existing digital wallets.
- **Decision Makers:** Parents or legal guardians seeking a simple way to monitor and reward financial responsibility.

## 3. Problem Statement
Teenagers lack a simple, fun way to track their spending and build healthy habits using the digital cards their parents have already given them. Parents struggle to keep their teens motivated to save and spend wisely in a cashless world.

## 4. Key Features

### 4.1. Real-time Monitoring & Sync
- **Funding Source Integration:** Connect the parent's Wise, Revolut, or Koho account via secure OAuth/Plaid.
- **Transaction Sync:** Automatically pull transaction data for the teen's specific card/sub-account.
- **Spending Categories:** Auto-categorize spending (e.g., Food, Entertainment, Gaming) for both teen and parent visibility.

### 4.2. Parent Monitoring Dashboard
- **Activity Feed:** Real-time list of teen purchases with merchant logos.
- **Spending Alerts:** Notifications when the teen spends over a certain amount or in specific categories.
- **Manual Rewards:** A "Boost" button to manually award Stash Points for good behavior.

### 4.3. Teen Dashboard & Gamification
- **Stash View:** A "Dark Mode" dashboard showing current balance and categorized spending.
- **Savings Goals:** Set and track progress towards personal targets.
- **Stash Points:** Automatically earn points for staying under a daily/weekly budget.
- **Literacy Quests:** Complete short, 2-minute interactive modules to earn points and level up financial knowledge.

### 4.4. Redemption Marketplace
- **Partner Rewards:** Redeem Stash Points for rewards like Amazon or App Store gift cards.

## 5. Non-Functional Requirements
- **Security:** AES-256 encryption for all financial tokens. No sensitive card data stored on-device.
- **Compliance:** Verifiable Parental Consent (VPC) for COPPA/GDPR compliance.
- **Simplicity:** The setup should take less than 2 minutes for both parent and teen.

## 6. User Journeys (Refined for Tracker Model)

### 6.1. Onboarding
1. Parent links their Wise/Revolut/Koho account.
2. Parent identifies which sub-account/card Alex is using.
3. Alex downloads the app and sees his "Stash" instantly.

### 6.2. The "Smart Reward"
1. Alex buys lunch for $8.00.
2. The app detects he is $2.00 under his daily budget.
3. Alex receives a notification: *"Budget Master! +5 Stash Points earned."*

## 7. Success Metrics
- **Engagement:** Frequency of teen checking their balance vs. the native bank app.
- **Literacy Impact:** Number of quests completed per month.
- **Retention:** Monthly active parent-teen pairs.
