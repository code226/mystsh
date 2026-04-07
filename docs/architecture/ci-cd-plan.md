# CI/CD Deployment Architecture (Vercel + Supabase)

This document details the automated pipeline for the mystsh platform, optimized for a **mobile-first** experience using serverless and real-time technologies.

## 1. Pipeline Overview

We utilize a **Serverless + Mobile** pipeline that minimizes operational overhead and infrastructure costs.

### Environment Strategy
- **Development (GitHub PRs):** Ephemeral Vercel Preview deployments for the Web Dashboard and Edge Functions.
- **Production (main branch):** Stable environment for production users.

## 2. Platform Hosting (Free-Tier Optimized)

| Component | Platform | Role |
| :--- | :--- | :--- |
| **Mobile App UI** | **Expo (EAS)** | Building and distributing iOS/Android binaries. |
| **Web Dashboard** | **Vercel** | Hosting the Parent Management interface (Next.js). |
| **API & Edge Functions**| **Supabase / Vercel** | Executing business logic and bank API integrations. |
| **Real-time Database** | **Supabase** | Managed PostgreSQL with Real-time synchronization. |

## 3. Deployment Workflows

### Mobile App (React Native/Expo)
- **EAS Build:** Builds are triggered for production releases.
- **EAS Update:** Allows for "Over-the-Air" (OTA) updates for quick UI fixes without full App Store review.
- **OTA Strategy:** We use OTA updates for all non-native changes to maintain agility.

### Backend (Vercel Edge & Supabase)
- **Automatic Deployment:** Pushing to the `main` branch automatically deploys Edge Functions to **Vercel** and **Supabase**.
- **Database Migrations:** Managed via the Supabase CLI to ensure schema consistency between environments.

## 4. Quality & Security Gates

- **Linting & Formatting:** Turborepo manages linting across the mobile and web projects.
- **SAST Scanning:** CodeQL and Snyk for dependency and code vulnerability scanning on every PR.
- **Secret Management:** Sensitive keys (Wise API, Plaid Secrets) are managed via Vercel Environment Variables and Supabase Vault.

## 5. Monitoring & Performance
- **Vercel Analytics:** Real-time monitoring of Web Dashboard performance.
- **Supabase Logs:** Monitoring Edge Function execution and database health.
- **Expo Sentry:** Integrated for real-time error tracking on mobile devices.
