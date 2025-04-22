---
title: Secure Authentication & Authorization Exercises 
description: these exercises will help you understand API authentication
publishDate: '21 Apr 2025'
tags: ['cryptography', 'exercises']
---



Each exercise includes:

- **Scenario**
- **Initial Information**
- **Problem Statement**
- **Tasks** for the student
- **Bonus Challenges** for deeper thinking

---

## **Section 1: OAuth 2.0 + PKCE (for Public Clients)**

### **Exercise 1.1 – SPA Login with PKCE**
**Scenario**: A single-page React app needs to authenticate users using Google OAuth 2.0 and PKCE.

**Initial Info**:
- No client secret is used.
- The React app uses the Authorization Code Flow with PKCE.
- You control both the SPA and the backend.

**Tasks**:
1. Sketch the full flow of OAuth 2 + PKCE: which party does what, in what order?
2. At each step, identify:
   - What data the client has
   - What data the auth server has
   - What is transmitted between them
3. Identify the attack vector if PKCE were omitted.
4. What prevents a malicious attacker from using a stolen authorization code?

**Bonus**:
- What happens if someone tries to reuse a `code_verifier`?
- Why must the `code_verifier` be random for each session?

---

## **Section 2: OAuth 2.0 – Client Credentials with mTLS or JWT**

### **Exercise 2.1 – Microservice Authorization with JWT Assertion**
**Scenario**: A backend microservice wants to authenticate to an OAuth 2.0 authorization server using a JWT assertion.

**Initial Info**:
- The client (service) uses its private key to sign a JWT.
- The auth server validates the JWT using the public key.
- No user is involved.

**Tasks**:
1. Draw the data flow for:
   - Generating the JWT
   - Requesting the access token
   - Using the token
2. Define what claims should go in the JWT (e.g. `aud`, `iss`, `sub`, `exp`).
3. What would happen if the JWT had a future `exp` (expiry) date but no `nbf` (not before)?
4. How is replay of JWTs prevented?

**Bonus**:
- Why is this better than a static API key?

---

### **Exercise 2.2 – Client Credentials + mTLS**
**Scenario**: Your OAuth 2.0 client authenticates using mutual TLS.

**Initial Info**:
- The client presents a TLS client certificate.
- The server only issues tokens to known, valid certs.

**Tasks**:
1. Map the steps for a successful client credentials + mTLS token request.
2. How does the server verify the client identity?
3. What protects this flow from token theft?

**Bonus**:
- What does the server store for each client to support mTLS?
- What are the tradeoffs between mTLS and JWT assertion?

---

## **Section 3: WebAuthn / FIDO2**

### **Exercise 3.1 – Passwordless Login with WebAuthn**
**Scenario**: A user wants to log into a web app using their YubiKey or fingerprint scanner.

**Initial Info**:
- The app supports WebAuthn.
- Registration was previously completed.

**Tasks**:
1. Step through the authentication flow:
   - Who generates the challenge?
   - What’s stored server-side vs. client-side?
2. How does the server know it's talking to the right authenticator?
3. What prevents phishing or replay attacks?

**Bonus**:
- What is "attestation" and when is it useful?
- How does WebAuthn support multiple devices?

---

## **Section 4: JWT Issuance, Refresh, and Revocation**

### **Exercise 4.1 – JWT + Refresh Tokens in a Mobile App**
**Scenario**: A mobile app uses short-lived JWTs and long-lived refresh tokens for authentication.

**Initial Info**:
- Access token lifespan: 15 mins.
- Refresh token lifespan: 30 days.
- Backend supports rotation and revocation.

**Tasks**:
1. Show the steps from:
   - First login
   - Access token use
   - Token refresh
2. Where are the tokens stored in the client?
3. What happens if a refresh token is stolen?

**Bonus**:
- Implement **refresh token rotation**: how does it work?
- How would you detect and respond to reuse of an old refresh token?

---

## **Section 5: Threat Modeling & Mixed Auth**

### **Exercise 5.1 – API with 3 Client Types**
**Scenario**: Your API is used by:
- A SPA frontend
- A native mobile app
- A backend microservice

Each needs a different auth flow.

**Tasks**:
1. For each client, choose:
   - OAuth flow (PKCE, client credentials, etc.)
   - Token format (JWT, opaque, PoP?)
   - Credential storage method
2. Create a **matrix** showing:
   - Who gets what data at each step
   - Who stores what
   - Where revocation and refresh happen

**Bonus**:
- Add WebAuthn to the SPA: how does that change the model?
- Add a CLI tool that needs to login via browser.

---

## **Section 6: Proof-of-Possession Tokens (Advanced)**

### **Exercise 6.1 – DPoP Protection**
**Scenario**: A client uses DPoP (OAuth Proof of Possession) to bind tokens to a session.

**Initial Info**:
- DPoP involves signing a request with a private key.
- The server issues a DPoP-bound access token.

**Tasks**:
1. Describe what goes into the DPoP JWT header and payload.
2. Map the flow of:
   - DPoP keypair generation
   - Token request
   - Protected resource access
3. What happens if the DPoP token is intercepted?
4. What limits abuse if the token is leaked but not the private key?

**Bonus**:
- Why is DPoP better than bearer tokens in public clients?

