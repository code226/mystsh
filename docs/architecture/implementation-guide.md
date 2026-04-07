# Wise OAuth 2.0 Implementation Guide (Tracker Model)

This document provides the technical blueprints for implementing the secure connection between the parent's Wise account and the mystsh platform.

---

## 1. Prerequisites (Wise Developer Portal)
Before coding, you must register your application at [Wise Developer Portal](https://wise.com/developer/):
- **Client ID:** `YOUR_WISE_CLIENT_ID`
- **Client Secret:** `YOUR_WISE_CLIENT_SECRET`
- **Redirect URI:** `https://api.mystsh.com/v1/auth/wise/callback` (Production) or `exp://localhost:19000/--/wise-auth` (Development/Expo).

---

## 2. Step 2: Launching the Secure Redirect (Mobile App)
In the **Teen/Parent Mobile App** (React Native/Expo), use `expo-auth-session` to initiate the "Handshake."

### Code Snippet: `src/hooks/useWiseAuth.ts`
```typescript
import * as AuthSession from 'expo-auth-session';
import { makeRedirectUri } from 'expo-auth-session';

const CLIENT_ID = process.env.EXPO_PUBLIC_WISE_CLIENT_ID;
const authUrl = "https://wise.com/oauth/authorize";

export const useWiseAuth = () => {
  const redirectUri = makeRedirectUri({
    scheme: 'mystsh',
    path: 'wise-auth'
  });

  const linkWiseAccount = async () => {
    const result = await AuthSession.startAsync({
      authUrl: `${authUrl}?client_id=${CLIENT_ID}&redirect_uri=${encodeURIComponent(redirectUri)}&response_type=code&scope=balances:read transactions:read`
    });

    if (result.type === 'success') {
      const { code } = result.params;
      // Send this code to your Vercel/Supabase backend to exchange for a token
      return code;
    }
  };

  return { linkWiseAccount };
};
```

---

## 3. Step 3: The Permission Request (Handled by Wise)
Once the user is redirected to Wise, they will log in and see the **Wise-hosted Permission Screen**.
- **User Action:** Maria (Parent) reviews the requested scopes (`balances:read`, `transactions:read`) and taps **"Authorise"**.
- **System Action:** Wise redirects Maria back to your app's `redirect_uri` with a temporary `code` appended to the URL.

---

## 4. Step 4: Exchanging the Code for a Token (Backend)
Your **Vercel Serverless Function** receives the `code` and swaps it for a permanent `access_token`.

### Code Snippet: `api/v1/auth/wise/callback.ts`
```typescript
import { createClient } from '@supabase/supabase-js';

const supabase = createClient(process.env.SUPABASE_URL, process.env.SUPABASE_SERVICE_ROLE_KEY);

export default async function handler(req, res) {
  const { code, state } = req.query;

  // 1. Exchange the temporary code for a permanent access_token
  const response = await fetch('https://api.wise.com/oauth/token', {
    method: 'POST',
    headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
    body: new URLSearchParams({
      grant_type: 'authorization_code',
      client_id: process.env.WISE_CLIENT_ID,
      client_secret: process.env.WISE_CLIENT_SECRET,
      code,
      redirect_uri: process.env.WISE_REDIRECT_URI,
    }),
  });

  const data = await response.json();
  const { access_token, refresh_token, profile_id } = data;

  // 2. Encrypt the access_token (Implementation of AES-256-GCM recommended)
  const encryptedToken = encrypt(access_token);

  // 3. Save to Supabase linked_accounts table
  const { error } = await supabase
    .from('linked_accounts')
    .insert([{ 
      user_id: state, // Parent's Supabase User ID passed in 'state'
      provider: 'WISE',
      access_token: encryptedToken,
      refresh_token: encrypt(refresh_token),
      external_profile_id: profile_id,
      status: 'ACTIVE'
    }]);

  res.status(200).json({ message: 'Wise Account Linked Successfully!' });
}
```

---

## 5. Security Checklist
1. **State Parameter:** Always use a unique `state` parameter in the initial redirect to prevent CSRF (Cross-Site Request Forgery) attacks.
2. **Token Encryption:** **NEVER** store the `access_token` in plaintext in your database. Use application-level encryption (AES-256).
3. **Environment Variables:** Keep your `CLIENT_SECRET` in **Vercel Environment Variables** or **Supabase Vault**, never in the source code.
