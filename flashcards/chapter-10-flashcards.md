## Chapter 10: Microsoft Defender for Cloud: Secure Score & Workload Protection — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Secure score formula for a single recommendation? | Contribution = Max points × (Healthy resources ÷ Total applicable resources). Exam tip: score is proportional, not all-or-nothing. |
| 2 | Defender for Servers Plan 1 vs Plan 2 — key difference? | Plan 1 = Microsoft Defender for Endpoint (MDE) integration only. Plan 2 = adds vulnerability assessment, adaptive application control, file integrity monitoring, adaptive network hardening. |
| 3 | What plan is required for Attack Path Analysis and Cloud Security Explorer? | Defender CSPM (paid). Not available in foundational (free) CSPM. Exam tests this exclusivity directly. |
| 4 | How do you onboard an AWS account to Defender for Cloud? | Create a native multicloud connector; AWS deploys a CloudFormation template granting the required IAM roles. Exam tip: this is the ONLY supported onboarding path. |
| 5 | How do you onboard a GCP project to Defender for Cloud? | Create a native GCP connector; run the provided Cloud Shell/Terraform onboarding script to grant roles and Arc-enable Kubernetes. |
| 6 | What is the default regulatory standard shown in the compliance dashboard? | Microsoft cloud security benchmark (MCSB) — applied by default to every subscription; other standards (ISO 27001, PCI DSS, NIST 800-53, SOC 2, CIS) are added manually. |
| 7 | What does a Governance Rule configure? | Assigns an owner + due date to recommendations, triggers email reminders/escalation on overdue items. Exam tests this as the accountability mechanism, distinct from workflow automation. |
| 8 | Foundational CSPM vs Defender CSPM — what's free vs paid? | Foundational CSPM (free): basic secure score + recommendations for all connected resources. Defender CSPM (paid): agentless scanning, attack path analysis, sensitive data discovery, Cloud Security Explorer. |
| 9 | What is the Cloud Security Graph? | A contextual graph of resources, exposures, and connections used to compute attack paths — powers Attack Path Analysis and Cloud Security Explorer queries. Requires Defender CSPM plan. |
| 10 | Which Defender plan protects Kubernetes/container images across Azure, AWS, and GCP? | Defender for Containers — covers runtime threat detection, registry image scanning, and Kubernetes configuration recommendations across all connected clouds. |
| 11 | What does Defender for Key Vault protect against? | Anomalous/suspicious access attempts and usage patterns to secrets, keys, and certificates stored in Key Vault (e.g., unusual IP, high-volume access, Tor exit node access). |
| 12 | How do you exempt a resource from a recommendation without hurting secure score? | Create an Exemption (with justification) scoped to the resource/resource group — removes it from the applicable resource count so it can't count as unhealthy. |
