## Chapter 1: Entra ID Identity Fundamentals & Conditional Access — Practice Questions

**Q1.** A company requires that all users assigned the Global Administrator role complete MFA when signing in from any network location, but the two designated break-glass emergency access accounts must never be blocked by policy misconfiguration. Which design BEST meets this requirement?

A) Enable Security Defaults tenant-wide and rely on its built-in admin MFA enforcement
B) Enable per-user MFA on the two break-glass accounts so they are protected the same as admins
C) Create a Conditional Access policy that blocks all sign-ins outside named locations for Global Administrators
D) Create a Conditional Access policy targeting the Global Administrator role with grant control 'Require MFA', and explicitly exclude a dedicated break-glass group from this and all other CA policies

<details>
<summary>Answer</summary>

**Correct: D**

Microsoft's documented best practice is a role-targeted CA policy enforcing MFA, with break-glass accounts placed in an excluded group referenced by every CA policy so a policy error can never lock out all admins.

**Why the others are wrong:**
- Security Defaults is all-or-nothing, cannot exclude break-glass accounts, and offers no granular targeting
- Enabling per-user MFA on break-glass accounts defeats their purpose — they must remain usable even if MFA/CA services fail
- Blocking outside named locations does not address the MFA requirement and would also lock out admins traveling, with no exclusion mentioned

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Identity Protection flags a user as 'High' user risk due to leaked credentials found in a known breach. The security team wants sign-in to be automatically blocked until the user proves the credential is no longer compromised by setting a new password. Which policy accomplishes this?

A) A user risk Conditional Access policy set to 'High' risk requiring secure password change
B) A sign-in risk Conditional Access policy set to 'High' risk requiring MFA
C) A Conditional Access policy with a Named Location condition set to block all countries
D) An Identity Protection risk detection alert with no automated remediation control

<details>
<summary>Answer</summary>

**Correct: A**

User risk policies target the likelihood the identity itself is compromised (e.g., leaked credentials) and the standard remediation control is 'Require password change', which resets the compromised credential.

**Why the others are wrong:**
- Sign-in risk policies evaluate the session/sign-in event, not the identity compromise, and MFA alone does not remediate a leaked password
- Named location blocking is unrelated to credential compromise and does not force remediation
- An alert-only detection does not enforce any access control or remediation

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** Identity Protection reports a 'Medium' sign-in risk for a user due to an unfamiliar sign-in property, and a separate 'High' sign-in risk for another sign-in from a known malicious IP address. The company wants medium risk sign-ins to require MFA and high risk sign-ins to be blocked entirely. What is the correct configuration?

A) One sign-in risk CA policy with risk level set to 'Medium and above' requiring MFA only
B) A single user risk policy set to 'High' with grant control Block access
C) A Named Location policy excluding malicious IP ranges
D) Two separate sign-in risk CA policies: one at 'Medium and above' requiring MFA, one at 'High' with grant control set to Block access

<details>
<summary>Answer</summary>

**Correct: D**

Achieving differentiated response per risk level requires two distinct sign-in risk policies with different risk-level scopes and grant controls — MFA for Medium+, Block for High.

**Why the others are wrong:**
- A single 'Medium and above' policy would also apply MFA (not block) to High risk sign-ins, not meeting the block requirement
- User risk policy evaluates identity compromise likelihood, not the session/sign-in risk event described here
- Named locations do not dynamically respond to real-time risk signals like malicious IP detections

</details>

---

**Q4.** A financial services company wants to enforce passwordless authentication that is resistant to phishing attacks, including AiTM (adversary-in-the-middle) proxy attacks. Which authentication method should be enforced?

A) Microsoft Authenticator push notifications
B) SMS-based one-time passcode
C) FIDO2 security keys
D) Voice call verification

<details>
<summary>Answer</summary>

**Correct: C**

FIDO2 security keys use public-key cryptography bound to the origin domain, making them resistant to phishing and AiTM proxy attacks, unlike OTP or push-based methods.

**Why the others are wrong:**
- Authenticator push notifications (without number matching context awareness) can still be susceptible to MFA fatigue and some proxy relay attacks
- SMS OTP can be intercepted, SIM-swapped, or relayed through a phishing proxy
- Voice call verification carries the same interception and social engineering weaknesses as SMS

</details>

---

**Q5.** Which Microsoft Entra ID license is required to configure risk-based Conditional Access policies driven by Identity Protection sign-in risk and user risk detections?

A) Microsoft Entra ID P2
B) Microsoft Entra ID Free
C) Microsoft Entra ID P1
D) Microsoft 365 Business Basic

<details>
<summary>Answer</summary>

**Correct: A**

Identity Protection risk detections and risk-based Conditional Access (sign-in risk and user risk policies) require Microsoft Entra ID P2 licensing.

**Why the others are wrong:**
- Entra ID Free only supports Security Defaults, not custom CA or risk policies
- Entra ID P1 enables standard Conditional Access but not Identity Protection risk-based policies
- Microsoft 365 Business Basic does not include Entra ID P1 or P2 features

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** An administrator creates a Named Location in Entra ID representing the corporate office IP range and marks it as 'trusted'. What is the direct effect of marking a named location as trusted?

A) It is used as a signal by Identity Protection risk detections (e.g., reduces false positives for atypical travel) and can be referenced as a condition in Conditional Access policies
B) It automatically satisfies any Conditional Access MFA requirement for sign-ins from that range
C) It grants all users in that range Global Administrator privileges
D) It disables Conditional Access entirely for that IP range

<details>
<summary>Answer</summary>

**Correct: A**

Trusted named locations feed into risk detection logic (reducing atypical-travel/anomaly false positives) and can be referenced as a location condition inside CA policies, but they do not themselves grant or bypass access.

**Why the others are wrong:**
- Trusted status does not automatically satisfy MFA — a CA policy must still be explicitly configured to use it as a condition
- Named locations have no relationship to role assignment
- Marking a location trusted does not disable Conditional Access evaluation

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Which practice is recommended by Microsoft for configuring emergency access (break-glass) accounts in Entra ID?

A) Synchronize the accounts from on-premises Active Directory so they follow the same password policy
B) Create at least two cloud-only accounts excluded from all Conditional Access policies, with strong unique passwords stored securely and sign-in activity actively monitored
C) Register the accounts for standard MFA using the same Authenticator app as regular admins
D) Store the account credentials in a shared Teams channel accessible to the helpdesk

<details>
<summary>Answer</summary>

**Correct: B**

Microsoft's documented guidance: create at least two cloud-only break-glass accounts, exclude them from all CA policies to prevent lockout, use strong long passwords, and monitor sign-ins with alerts.

**Why the others are wrong:**
- Cloud-only accounts are required — on-prem sync introduces a dependency that could fail during an AD outage, defeating the purpose
- Standard MFA tied to a personal device risks lockout if the device/service is unavailable, which is exactly the scenario break-glass accounts must survive
- Storing credentials in an easily accessible chat channel is a major security risk, not a recommended practice

</details>

---

**Q8.** In the structure of a Conditional Access policy, which category defines what happens AFTER the assignments and conditions have been evaluated and matched — for example, requiring MFA or blocking access?

A) Assignments
B) Conditions
C) Named locations
D) Access controls (grant/block/session)

<details>
<summary>Answer</summary>

**Correct: D**

Access controls (grant controls like Require MFA/compliant device, block access, and session controls like sign-in frequency) determine the enforcement action once assignments and conditions match.

**Why the others are wrong:**
- Assignments define who/what the policy applies to (users, groups, cloud apps)
- Conditions define signals evaluated to decide if the policy applies (risk, location, device platform, client app)
- Named locations are one specific type of condition input, not the enforcement mechanism itself

</details>

---

