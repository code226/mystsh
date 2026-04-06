# CI/CD Deployment Architecture

This document details the automated pipeline for the mystsh platform, ensuring high availability, security, and rapid delivery.

## 1. Pipeline Overview

We utilize **GitHub Actions** as our primary CI provider, orchestrated via **Turborepo** for optimized task execution.

### Environment Strategy
- **Development (Ephemeral):** Created for every PR to test isolated features.
- **Staging (Branch: `main`):** Shared environment for UAT and final testing.
- **Production (Tagged Releases):** Stable environment serving end-users.

## 2. Security Gates & Compliance

Security is integrated into every step of the pipeline.

### Static Analysis (SAST)
- **CodeQL:** Runs on every push to identify security vulnerabilities.
- **Snyk:** Scans all `package.json` dependencies for known vulnerabilities.

### Secret Management
- **Provider:** AWS Secrets Manager / HashiCorp Vault.
- **Rule:** No secrets or sensitive keys are ever stored in `.env` files or hardcoded. Deployment keys are injected at runtime via GitHub Action Secrets.

### PCI-DSS Automated Audits
- Automated scripts verify that no PAN (Primary Account Number) data is logged or stored in plaintext before any deployment to Production.

## 3. Continuous Deployment (CD) Workflows

### Backend (AWS ECS)
- **Strategy:** Blue/Green Deployments.
- **Flow:** New containers are spun up and verified via health checks before traffic is shifted from the "Blue" (old) to "Green" (new) cluster.

### Mobile Applications (EAS)
- **EAS Build:** Builds signed binaries for iOS (.ipa) and Android (.aab).
- **EAS Submit:** Automatically uploads builds to TestFlight and Google Play Console Internal tracks once CI passes.

## 4. Rollback & Monitoring

- **Auto-Rollback:** If AWS CloudWatch detects a 5% increase in error rates post-deployment, the ECS service automatically reverts to the previous stable task definition.
- **Health Checks:** `/health` endpoints are monitored every 30 seconds across all services.
