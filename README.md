# Azure IAM Conditional Access Lab

Azure IAM Conditional Access lab implementing Zero Trust by blocking legacy authentication and analyzing sign-in logs.

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
![Step 1](images/policy-01/policy-01/step1.png)

### Step 2: Create New Policy
![Step 2](images/policy-01/policy-01/step2.png)

### Step 3: Assign Users (All Users)
![Step 3](images/policy-01/policy-01/step3.png)

### Step 4: Target Resources (All Resources)
![Step 4](images/policy-01/policy-01/step4.png)

### Step 5: Configure Client Apps (Legacy Auth)
![Step 5](images/policy-01/policy-01/step5.png)

### Step 6: Configure Grant Control (Block Access)
![Step 6](images/policy-01/policy-01/step6.png)

### Step 7: Policy Created (Report-Only)
![Step 7](images/policy-01/policy-01/step7.png)

### Step 8: Policy Details View
![Step 8](images/policy-01/policy-01/step8.png)

### Step 9: Policy Verification / Sign-in Logs
![Step 9](images/policy-01/policy-01/step9.png)
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
