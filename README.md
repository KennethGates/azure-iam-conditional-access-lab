# Azure IAM Conditional Access Lab
Azure IAM Conditional Access lab implementing Zero Trust by blocking legacy authentication and analyzing sign-in logs.

---

## 🧭 Zero Trust Architecture Diagram
![Zero Trust Diagram](images/policy-01/zero-trust-diagram.png)

---

## 🔐 Policy 1 — Block Legacy Authentication

### 📌 Overview
Legacy authentication protocols (Exchange ActiveSync, SMTP, IMAP, POP3, and older Office clients) do not support modern authentication and cannot enforce MFA.

This makes them highly vulnerable to:
- Password spray attacks
- Credential stuffing
- Brute-force login attempts

This policy blocks all legacy authentication across the tenant using Conditional Access.

---

## ⚙️ Configuration Steps

1. Navigate to **Microsoft Entra ID → Conditional Access**
2. Click **New Policy**
3. Name the policy: `Block Legacy Authentication`
4. Set **Users** → All users
5. Set **Target Resources** → All resources
6. Configure **Client Apps**
   - Enable condition
   - Select:
     - Exchange ActiveSync clients
     - Other clients
7. Configure **Grant Controls**
   - Select **Block Access**
8. Set policy state to:
   - Report-only (testing phase)
9. Click **Create**

---

## 📸 Screenshots

### Step 1: Conditional Access Overview
![Step 1](images/policy-01/step1.png)

### Step 2: Create New Policy
![Step 2](images/policy-01/step2.png)

### Step 3: Assign Users (All Users)
![Step 3](images/policy-01/step3.png)

### Step 4: Target Resources (All Resources)
![Step 4](images/policy-01/step4.png)

### Step 5: Configure Client Apps (Legacy Auth)
![Step 5](images/policy-01/step5.png)

### Step 6: Configure Grant Control (Block Access)
![Step 6](images/policy-01/step6.png)

### Step 7: Policy Created (Report-Only)
![Step 7](images/policy-01/step7.png)

### Step 8: Policy Details View
![Step 8](images/policy-01/step8.png)

### Step 9: Policy Verification / Sign-in Logs
![Step 9](images/policy-01/step9.png)

---

## 🔄 Before vs After

**Before:**
- Legacy auth protocols allowed tenant-wide
- Accounts accessible via EAS/SMTP/IMAP protected by password alone
- MFA could be silently bypassed by falling back to a legacy client

**After:**
- All legacy auth client types blocked at the Conditional Access layer
- Authentication via non-modern clients rejected before credentials are evaluated
- MFA bypass vector eliminated across the tenant

---

## 🔍 Security Impact
Legacy authentication protocols cannot respond to MFA challenges, meaning
any account accessible via legacy auth is protected by password alone —
regardless of whether MFA is configured tenant-wide. Blocking these
protocols eliminates a primary attack vector for password spray and
credential stuffing attacks, enforces consistent authentication standards
across the tenant, and ensures no user can silently bypass MFA by
falling back to a legacy client.

---

### 🧪 Real-World Scenario
An attacker attempts a password spray attack using legacy protocols such as IMAP or SMTP, which do not support MFA. Without this policy, the attacker could successfully authenticate using only a valid password. With this policy in place, the authentication attempt is blocked entirely, preventing unauthorized access.

---

## 🧠 Key Skills Demonstrated

- Azure / Microsoft Entra ID
- Conditional Access Policies
- Identity Security (IAM)
- Zero Trust Architecture
- Security Monitoring & Logging

---

## 🚀 Future Improvements

- Enable policy (move from Report-only → On)
- Integrate with SIEM (Microsoft Sentinel)
- Add MFA enforcement policy
- Monitor risky sign-ins and alerts

---

## 👨🏾‍💻 Author
Kenneth Gates
Cybersecurity | IAM | Cloud Security

---

## 🔐 Policy 2 — Require MFA for All Users

### 📌 Overview
This policy enforces multifactor authentication for all users across all cloud resources in the tenant. A break-glass account is excluded to ensure emergency administrative access is never locked out.

Without MFA enforcement, accounts protected by password alone are vulnerable to:
- Credential stuffing
- Phishing attacks
- Brute-force login attempts

---

## ⚙️ Configuration Steps

1. Navigate to **Microsoft Entra ID → Conditional Access**
2. Click **New Policy**
3. Name the policy: `Require MFA — All Users`
4. Set **Users** → All users
   - Exclude: break-glass admin account
5. Set **Target Resources** → All resources
6. Configure **Grant Controls**
   - Select **Grant access**
   - Check **Require multifactor authentication**
7. Set policy state to **Report-only**
8. Click **Create**

---

## 📸 Screenshots

### Step 1: CA Policies List (Before)
![Step 1](images/policy-02/policy-02-step1-before-policies-list.png)

### Step 2: Policy Name Entered
![Step 2](images/policy-02/policy-02-step2-policy-name.png)

### Step 3: Users — All Users Selected (Include)
![Step 3](images/policy-02/policy-02-step3-users-all-users.png)

### Step 4: Break-Glass Account Excluded
![Step 4](images/policy-02/policy-02-step4-exclude-break-glass.png)

### Step 5: Target Resources — All Resources
![Step 5](images/policy-02/policy-02-step5-all-resources.png)

### Step 6: Grant — Require MFA Selected
![Step 6](images/policy-02/policy-02-step6-require-mfa.png)

### Step 7: Report-Only Confirmed Before Save
![Step 7](images/policy-02/policy-02-step7-report-only.png)

### Step 8: Policy Created — Report-Only in List
![Step 8](images/policy-02/policy-02-step8-policy-created.png)

### Step 9: Sign-In Logs — Policy Evaluated
![Step 9](images/policy-02/policy-02-step10-sign-in-logs.png)
---

## 🔄 Before vs After

**Before:**
- No MFA requirement enforced at the Conditional Access layer
- Users could authenticate with password alone across all cloud apps
- Phishing or credential theft provided immediate full account access

**After:**
- All users required to complete MFA for every cloud resource
- Break-glass account excluded to preserve emergency admin access
- Policy evaluated in Report-only mode to validate scope before enforcement

---

## 🔍 Security Impact

Passwords alone are insufficient against modern credential attacks. This policy closes the gap by requiring a second factor at the Conditional Access layer — independent of per-user MFA settings. The break-glass exclusion follows Microsoft's recommended best practice to ensure administrators retain emergency access if MFA infrastructure fails or a misconfiguration affects enforcement.

---

### 🧪 Real-World Scenario

An attacker obtains valid credentials through a phishing campaign. Without MFA enforcement, they authenticate successfully and access cloud resources immediately. With this policy in place, authentication is blocked at the Conditional Access layer until a second factor is verified — rendering stolen credentials alone insufficient for access.

---

## 🧠 Key Skills Demonstrated
- Microsoft Entra ID Conditional Access
- MFA Policy Design
- Break-Glass Account Strategy
- Zero Trust Identity Enforcement
- Report-Only Mode Validation

---

## 👨🏾‍💻 Author
Kenneth Gates  
Cybersecurity | IAM | Cloud Security
