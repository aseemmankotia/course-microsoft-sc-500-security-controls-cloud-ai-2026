## Entra ID Identity Fundamentals & Conditional Access — Cheat Sheet

### Conditional Access Policy Anatomy
| Component | Purpose | Examples |
|---|---|---|
| Assignments | Who/what it targets | Users/groups, roles, cloud apps, workload identities |
| Conditions | Signals evaluated | Sign-in risk, user risk, device platform, location, client app |
| Access Controls | Enforcement action | Grant (MFA, compliant device, hybrid join, T&C), Block, Session controls |

### Risk Policy Quick Reference
| Policy Type | Detects | Typical Remediation | License |
|---|---|---|---|
| Sign-in risk | Session-level anomaly (anonymous IP, atypical travel, malicious IP) | Require MFA (Medium+); Block (High) | Entra ID P2 |
| User risk | Identity compromise (leaked creds, threat intel) | Require secure password change (High) | Entra ID P2 |

### MFA / Passwordless Methods (strongest → weakest against phishing)
1. FIDO2 security key / Windows Hello for Business — phishing-resistant
2. Microsoft Authenticator (passwordless phone sign-in, number matching) — strong
3. Authenticator push (no number matching) — moderate, MFA-fatigue risk
4. OATH hardware/software token — moderate
5. SMS / Voice call — weakest, interceptable

### Named Locations
- IP ranges (IPv4/IPv6 CIDR) marked **Trusted** → reduces false-positive risk detections (e.g., atypical travel), usable as a CA condition.
- Country/Region — determined by IP mapping by default, or GPS if configured.
- Trusted ≠ automatic MFA bypass — must be explicitly referenced in a policy.

### Break-Glass Accounts — Checklist
- Minimum 2 accounts, cloud-only (no on-prem sync/federation dependency)
- Excluded from **every** Conditional Access policy
- Strong, long, unique passwords in secure physical/vault storage
- Not enrolled in standard device-based MFA (avoid single point of failure)
- Sign-in activity monitored with alerting (e.g., Log Analytics/Sentinel)

### License Requirements
| Feature | License |
|---|---|
| Security Defaults | Free |
| Custom Conditional Access | Entra ID P1 |
| Identity Protection risk policies | Entra ID P2 |

### Common Exam Traps
- Security Defaults is all-or-nothing — cannot coexist with granular CA design questions.
- Confusing sign-in risk (session) with user risk (identity) — remediation controls differ (MFA vs password change).
- Assuming a trusted named location automatically satisfies an MFA grant control — it does not.
- Forgetting break-glass exclusion in a NEW CA policy → tenant lockout scenario in scenario questions.
