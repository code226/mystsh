# Data Privacy & Compliance Documentation

The mystsh platform is designed with "Privacy by Design" principles to protect our users, especially teenagers.

## 1. COPPA & GDPR Compliance

### Children's Online Privacy Protection Act (COPPA)
- **Parental Consent:** We enforce a "Verifiable Parental Consent" flow where a parent must link a valid financial account before any teen profile can be fully activated.
- **Data Collection:** We only collect the minimum amount of data required to provide the service (e.g., name, birthdate).

### General Data Protection Regulation (GDPR)
- **Data Subject Rights:** Users can request a full export of their data or request total erasure (Right to be Forgotten) directly through the Profile settings.

## 2. Data Minimization & Storage

- **PII Protection:** All Personally Identifiable Information is encrypted at rest using AES-256.
- **Log Sanitation:** Automated filters ensure that sensitive data (like card tokens or birthdates) are masked in server logs.

## 3. Encryption & Security

| State | Protocol |
| :--- | :--- |
| **In Transit** | TLS 1.3 |
| **At Rest** | AES-256 (AWS EBS/RDS Encryption) |
| **Inter-Service** | Mutual TLS (mTLS) for microservices |

## 4. Financial Compliance

- **PCI-DSS Level 1:** We never store raw card numbers. All card data is tokenized by our issuer partner (Stripe/Marqeta).
- **Audit Logs:** Immutable logs are kept for all financial adjustments to ensure a clear audit trail.
