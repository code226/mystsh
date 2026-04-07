# Financial Integrations Guide: Wise, Revolut, & KOHO

This document details the technical implementation for connecting and managing parent funding sources within the mystsh platform.

---

## 1. Integration Matrix

| Partner | Integration Type | Connectivity Method | Webhook Support | Latency |
| :--- | :--- | :--- | :--- | :--- |
| **Wise** | **Direct API** | OAuth 2.0 (Native) | Native Wise Webhooks | < 500ms |
| **Revolut** | **Open Banking / Aggregator** | Plaid / Direct OAuth | Plaid Webhooks | 1 - 3s |
| **KOHO** | **Aggregator** | Plaid / Flinks | Aggregator Webhooks | 2 - 5s |

---

## 2. Wise Integration (Direct Path)
**Strategy:** Utilize the Wise Platform API for near-instant transaction processing and funding pulls.

### Implementation Details:
- **Auth:** Redirect parent to Wise OAuth portal. Request `transfers:create`, `balances:read`, and `webhooks:all` scopes.
- **Webhook Setup:** Programmatically register `https://api.mystsh.com/v1/webhooks/wise` upon successful OAuth.
- **Funding Pull:** Use the Wise "Balance to Balance" transfer for immediate settlement of teen transactions.

---

## 3. Revolut Integration (Open Banking Path)
**Strategy:** Use **Plaid** as the primary gateway for Revolut Retail accounts to ensure compliance with Open Banking regulations (PSD2).

### Implementation Details:
- **Auth:** Launch Plaid Link with `Revolut` as the targeted institution.
- **Data Sync:** Subscribe to Plaid `TRANSACTIONS` webhooks.
- **Funding Pull:** Use Plaid **Signal** to evaluate the risk of a funding pull (ACH/EFT) from the Revolut account to the mystsh settlement account.

---

## 4. KOHO Integration (Aggregator Path)
**Strategy:** Since KOHO lacks a public API, we utilize **Plaid** (or **Flinks** for deeper Canadian market coverage) as the bridge.

### Implementation Details:
- **Auth:** Maria (Parent) logs in via Plaid Link using her KOHO credentials + MFA.
- **Balance Verification:** Perform a real-time `/accounts/balance/get` call via Plaid before authorizing any teen transaction over $20.00.
- **Webhooks:** Rely on Plaid's `DEFAULT_UPDATE` to sync transaction history into the Parent Dashboard.

---

## 5. Unified Funding Source Schema (Normalizing the Data)
Regardless of the source, all external accounts are mapped to a standard `FundingSource` object in our PostgreSQL database:

```typescript
interface FundingSource {
  id: string; // UUID
  parentId: string;
  provider: 'WISE' | 'REVOLUT' | 'KOHO';
  externalAccountId: string; // Tokenized ID from Wise/Plaid
  accessToken: string; // Encrypted
  balance: number;
  currency: string;
  lastSyncedAt: Date;
  status: 'ACTIVE' | 'PENDING' | 'DISCONNECTED';
}
```

---

## 6. Security & Token Management
- **Encryption:** All `access_tokens` are encrypted at the application layer using **AES-256-GCM** before being stored in RDS.
- **Rotation:** Automatic token refresh logic is implemented for Wise and Plaid to ensure continuous connectivity without re-authentication.
- **Audit Logs:** Every funding pull or balance check is logged with a unique `trace_id` for PCI-DSS compliance and dispute resolution.
