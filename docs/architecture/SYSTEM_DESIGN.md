# System Design Document - mystsh (Vercel + Supabase Tracker Model)

## 1. High-Level Architecture Overview

mystsh follows a mobile-first, serverless architecture. The system is designed for real-time transaction syncing and budget monitoring, primarily for display on a React Native (Expo) mobile dashboard.

### Component Diagram (Conceptual)
```mermaid
graph TD
    A[Teen & Parent Mobile App (React Native/Expo)] --> B[Supabase Real-time / Auth]
    C[Parent Web Dashboard (Next.js)] --> D[Vercel Serverless Functions]
    B --> E[(Supabase PostgreSQL Database)]
    D --> E
    D --> F[Aggregation Layer (Plaid/Wise API)]
    F --> G[External Banks (Wise, Revolut, KOHO)]
    D --> H[Gamification & Reward Engine]
    H --> B
```

## 2. Component Breakdown

### 2.1. Client Apps (Mobile-First)
- **Teen Mobile App (React Native):** The primary UI for balance tracking and gamified literacy. Subscribes to **Supabase Real-time** to instantly reflect new transactions.
- **Parent Mobile App (React Native):** Focused on real-time monitoring of teen spending and awarding "Stash Point" boosts.
- **Parent Web Dashboard (Next.js/Vercel):** A high-fidelity, data-rich view for managing sub-accounts and setting budgets.

### 2.2. Backend Services (Serverless & Real-time)
- **Supabase Auth:** Manages multi-tenant identity (parent and teen roles) with built-in MFA for parent accounts.
- **Vercel / Supabase Edge Functions:** Handles business logic for connecting Wise/Plaid, processing budget calculations, and manual "Boost" awards.
- **Aggregation Engine:** Listens for Wise/Plaid webhooks. When a webhook arrives, it updates the **Supabase PostgreSQL** database, which automatically pushes a real-time update to the mobile app.
- **Reward Engine:** Calculates "Stash Points" based on spending behavior and quest completion.

### 2.3. Data Storage
- **Supabase PostgreSQL:** Stores user profiles, encrypted bank tokens, and mirrored transaction history for instant access.
- **Supabase Storage:** Manages user avatars and literacy quest assets.

## 3. Key Technical Workflows

### 3.1. Real-time Transaction Pulse
1. A transaction occurs at Wise/KOHO.
2. The bank sends a webhook to a **Vercel Serverless Function**.
3. The function updates the `transactions` table in **Supabase**.
4. **Supabase Real-time** pushes a notification to the **React Native** app.
5. The teen's "Budget Meter" updates instantly on their screen.

### 3.2. Automated Reward Flow
1. The **Reward Engine** (Edge Function) detects an "On Budget" purchase.
2. It increments the `stash_points` column in the `user_profiles` table.
3. The app receives the real-time update and triggers a "Point Earned" animation and haptic feedback.

## 4. Security & Compliance
- **RLS (Row Level Security):** Supabase RLS ensures that teens can only see their own transactions, while parents can see all linked teen accounts.
- **Encryption:** Financial tokens are encrypted at the application layer before being stored in PostgreSQL.
- **Compliance:** Enforced parental consent flow via Supabase Auth metadata.
