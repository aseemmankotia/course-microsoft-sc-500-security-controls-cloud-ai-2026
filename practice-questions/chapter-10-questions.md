## Chapter 10: Microsoft Defender for Cloud: Secure Score & Workload Protection — Practice Questions

**Q1.** A subscription has a security recommendation with a maximum possible score of 10 points. It applies to 10 resources: 7 are healthy and 3 are unhealthy. What score does this recommendation currently contribute to the secure score?

A) 10 points
B) 3 points
C) 0 points
D) 7 points

<details>
<summary>Answer</summary>

**Correct: D**

Secure score contribution = max score × (healthy resources ÷ total applicable resources) = 10 × (7/10) = 7. Score is proportional to remediated resources, not all-or-nothing per recommendation.

**Why the others are wrong:**
- 10 points would require all resources to be healthy
- 3 points reflects the unhealthy count, not the credited (healthy) portion
- 0 points is only awarded if all resources are unhealthy

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Which Defender for Cloud plan should you enable to detect SQL injection attempts against an Azure SQL Managed Instance?

A) Defender for App Service
B) Defender for Databases (SQL)
C) Defender for Servers
D) Defender for Key Vault

<details>
<summary>Answer</summary>

**Correct: B**

Defender for Databases (the plan covering Azure SQL, SQL on VMs/Arc, and other DB engines) provides SQL-specific threat detection including SQL injection and anomalous access alerts.

**Why the others are wrong:**
- Defender for App Service protects web apps, not the database engine
- Defender for Servers protects VM/OS-level threats, not database query-layer attacks
- Defender for Key Vault protects secrets access, unrelated to SQL query threats

</details>

---

**Q3.** Your company runs workloads on AWS EC2 and wants Microsoft Defender for Cloud to assess vulnerabilities and provide endpoint protection recommendations for these instances. What must you configure first?

A) Create a multicloud connector to AWS, enable the Defender for Servers plan, and onboard EC2 instances via Azure Arc
B) Enable Defender for Servers directly from the AWS Console
C) Enable Microsoft Defender for Cloud Apps
D) Configure an Azure Policy assignment targeting the AWS account ID

<details>
<summary>Answer</summary>

**Correct: A**

AWS workload protection requires a native multicloud connector; enabling Defender for Servers on that connector auto-provisions Azure Arc and the Defender agent onto EC2 instances.

**Why the others are wrong:**
- Defender for Servers is an Azure/Defender for Cloud construct — it cannot be enabled from within AWS
- Defender for Cloud Apps is a CASB for SaaS app discovery, not IaaS workload protection
- Azure Policy alone cannot reach into an AWS account without the connector's underlying role/permissions setup

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** You want a specific engineer to receive reminders when a recommendation isn't remediated within a set number of days, with ownership auto-expiring after a defined period. Which Defender for Cloud feature configures this?

A) Governance rules
B) Workflow automation
C) Regulatory compliance dashboard
D) Azure Policy exemption

<details>
<summary>Answer</summary>

**Correct: A**

Governance rules assign an owner and due date to recommendations, trigger email notifications on approaching/missed due dates, and can escalate ownership — this is the exam-tested mechanism for recommendation accountability.

**Why the others are wrong:**
- Workflow automation triggers Logic Apps on alerts/recommendations creation, not owner/due-date tracking
- The compliance dashboard shows standard adherence, not individual recommendation ownership
- Policy exemptions remove a resource from a recommendation's scope entirely, not assign accountability

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** What is required to enable Attack Path Analysis and the Cloud Security Graph in Microsoft Defender for Cloud?

A) Defender for Servers Plan 1
B) Defender CSPM (Cloud Security Posture Management) plan
C) Microsoft Sentinel
D) Defender for Cloud Apps

<details>
<summary>Answer</summary>

**Correct: B**

Attack path analysis, Cloud Security Explorer, and agentless scanning are premium capabilities exclusive to the paid Defender CSPM plan — they are not part of foundational (free) CSPM.

**Why the others are wrong:**
- Defender for Servers Plan 1 only adds MDE integration, no graph/attack-path features
- Sentinel is a SIEM/SOAR product, unrelated to enabling this CSPM feature
- Defender for Cloud Apps is a CASB, not a posture management capability

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** Which regulatory compliance standard should you add to the compliance dashboard to demonstrate adherence to payment card data security requirements?

A) ISO 27001
B) NIST SP 800-53
C) PCI DSS
D) CIS Azure Foundations Benchmark

<details>
<summary>Answer</summary>

**Correct: C**

PCI DSS is specifically the payment card industry data security standard, directly mapped to cardholder data protection requirements.

**Why the others are wrong:**
- ISO 27001 is a general information security management standard, not payment-specific
- NIST SP 800-53 is a US federal control catalog, not payment industry specific
- CIS Azure Foundations Benchmark is an Azure hardening baseline, unrelated to payment card compliance

</details>

---

**Q7.** Your security team wants to protect Google Cloud Platform GKE clusters using Microsoft Defender for Containers. Which method connects GCP resources to Defender for Cloud?

A) Manually install the Azure Arc agent on each GKE node
B) Create an Azure Policy that queries the GCP API directly
C) Enable the Defender for Cloud Apps GCP connector
D) Use the native GCP multicloud connector's onboarding script, which deploys required GCP roles and the Arc-enabled Kubernetes extension

<details>
<summary>Answer</summary>

**Correct: D**

The GCP connector wizard provisions a service account/roles and runs an onboarding script (Cloud Shell or Terraform) that Arc-enables Kubernetes clusters so Defender for Containers can protect them.

**Why the others are wrong:**
- Manual per-node Arc installation is not the supported onboarding path for GKE clusters
- Azure Policy cannot directly query GCP APIs without the connector's underlying integration
- Defender for Cloud Apps is unrelated — it governs SaaS app access, not container workload protection

</details>

---

**Q8.** A recommendation doesn't apply to resources in a specific resource group, but you don't want it to negatively affect the secure score for those resources. What should you do?

A) Delete the resource group
B) Disable the entire Defender plan for the subscription
C) Create a governance rule with no assigned owner
D) Create an exemption for the recommendation scoped to the resource group with a documented justification

<details>
<summary>Answer</summary>

**Correct: D**

Exemptions remove specific resources/resource groups from a recommendation's applicable scope (with a required justification), which prevents them from counting as unhealthy in the score.

**Why the others are wrong:**
- Deleting the resource group is destructive and unrelated to score management
- Disabling the whole plan removes all its recommendations, losing other valid protections
- A governance rule without an owner still leaves resources counted as unhealthy — it doesn't exempt them

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

