# Answer Key — Practice Test 2

**Q1. Correct: D**

PIM eligible assignments combined with activation settings (require MFA, require justification, require approval with a named approver) are the only configuration that enforces just-in-time, approved, justified activation while never granting permanent standing access.

---

**Q2. Correct: A**

Workload identity federation lets GitHub Actions exchange a short-lived OIDC token for an Azure AD access token via a federated identity credential, eliminating the need to store any secret or certificate in the pipeline.

---

**Q3. Correct: B**

Authentication strength lets you restrict which specific combinations of authentication methods satisfy a Conditional Access policy; the built-in 'Phishing-resistant MFA' strength includes only FIDO2, certificate-based auth, and Windows Hello for Business, excluding SMS and standard push.

---

**Q4. Correct: C**

Entra ID roles like Global Administrator do not automatically grant Azure resource (subscription/management group) permissions; a Global Admin must explicitly elevate access, which temporarily assigns User Access Administrator at the tenant root management group scope to manage Azure RBAC.

---

**Q5. Correct: C**

Policy exemptions allow a specific scope (subscription, resource group, or resource) to be excluded from a policy or initiative assignment for a defined reason and time period without altering the underlying policy definition or assignment for everyone else.

---

**Q6. Correct: A**

Entitlement management access packages combine automated B2B guest provisioning on approval, time-bound expiration policies, and integrated access reviews — exactly matching the approval, auto-expiry, and review requirements in a single governed workflow.

---

**Q7. Correct: D**

PIM role activation settings let you configure activation duration, mandatory justification, MFA enforcement at activation, and an approval workflow with named approvers all in one place — this is the only option that satisfies every stated requirement together.

---

**Q8. Correct: C**

Conditional Access authentication strengths let you require a specific set of methods — including the built-in 'Phishing-resistant MFA' strength (FIDO2, Windows Hello for Business, certificate-based auth) — scoped to a specific app and a specific set of directory roles, exactly matching the requirement without affecting other users.

---

**Q9. Correct: A**

Workload identity federation lets you add a federated credential to an app registration's service principal that trusts GitHub's OIDC issuer for a given repo/branch/environment, allowing GitHub Actions to obtain short-lived Azure AD tokens with zero stored secrets.

---

**Q10. Correct: C**

Azure Policy exemptions with the 'Waiver' category let you excuse a specific scope from enforcement for a defined, expiring period while the resource continues to be evaluated and shows up in compliance reporting as exempted — meeting the requirement for documentation and continued visibility.

---

**Q11. Correct: C**

Secure enclaves allow rich operations such as pattern matching and range comparisons to be performed server-side inside a hardware-protected enclave, while the data remains encrypted and unreadable to DBAs or anyone without enclave access — plaintext never leaves the enclave.

---

**Q12. Correct: D**

Azure Firewall Premium supports TLS inspection (decrypt, inspect, re-encrypt) combined with IDPS (Intrusion Detection and Prevention System) which can be set to Alert and Deny mode to actively block traffic matching known exploit and CVE signatures.

---

**Q13. Correct: D**

DDoS IP Protection is a pay-per-protected-IP tier introduced to let customers apply advanced DDoS mitigation, cost protection, and telemetry to specific individual public IPs, which is far more cost-effective than protecting an entire virtual network when only a handful of IPs are critical.

---

**Q14. Correct: A**

On-premises DNS servers cannot query an Azure Private DNS zone directly. Deploying an Azure DNS Private Resolver and configuring conditional forwarding from on-prem DNS to it allows on-premises clients to correctly resolve the privatelink zone and receive the private endpoint's IP.

---

**Q15. Correct: D**

CMK requires the storage account's managed identity to authenticate to Key Vault with wrapKey/unwrapKey/get permissions, and Azure enforces that the Key Vault has soft-delete and purge protection enabled as a mandatory prerequisite to prevent accidental key loss that would make encrypted data unrecoverable.

---

**Q16. Correct: C**

WAF supports managed rule exclusions to exempt specific request fields (like a named query string parameter) from CRS evaluation, eliminating the false positive without weakening overall protection, and custom rate-limiting rules can threshold requests per client IP per time window — directly satisfying both stated requirements.

---

**Q17. Correct: A**

SAS tokens tied to a stored access policy can be revoked instantly by changing or deleting the policy on the container, invalidating that specific SAS without affecting account keys or other tokens.

---

**Q18. Correct: B**

Always Encrypted keeps the SSN encrypted at rest, in transit, and in memory inside SQL — the database engine, and therefore any DBA querying directly, only ever sees ciphertext. Deterministic encryption preserves the ability to perform equality comparisons for lookups, and secure enclaves allow richer server-side operations without exposing plaintext outside the enclave.

---

**Q19. Correct: D**

On-premises DNS servers cannot query Azure Private DNS Zones directly. Azure DNS Private Resolver provides an inbound endpoint with an IP address that on-premises DNS can conditionally forward privatelink.* zone queries to, resolving the FQDN to the private endpoint IP over ExpressRoute/VPN.

---

**Q20. Correct: B**

Azure Firewall Premium is required for TLS inspection (decrypting outbound TLS to inspect payloads) and IDPS (signature-based intrusion detection and prevention), which together detect malware and known malicious indicators in outbound traffic before re-encrypting it.

---

**Q21. Correct: B**

Rule exclusions let you scope out a specific match variable (such as a named request header, cookie, or query string argument) from evaluation by one or more specific rules, eliminating the false positive while leaving that rule active for all other traffic and preserving overall protection.

---

**Q22. Correct: B**

Azure DDoS IP Protection is a pay-per-protected-IP tier designed for scenarios with a small number of public IPs, offering the same core mitigation capabilities as Network Protection at a lower, per-IP cost, without requiring the tenant-wide commitment.

---

**Q23. Correct: C**

Azure AD Workload Identity is the supported, GA replacement for the retired Pod Identity project. It federates a Kubernetes service account's OIDC token with a Microsoft Entra app/managed identity, and when paired with the Secrets Store CSI Driver's Key Vault provider, secrets are mounted as volumes at runtime with per-pod, least-privilege identity — no credentials ever touch the image or etcd.

---

**Q24. Correct: A**

SSE with customer-managed keys handles the CMK layer at the platform/storage level, and enabling infrastructure (double) encryption adds a second, independent encryption layer using a platform-managed key — together satisfying a double-encryption-at-rest requirement entirely outside the guest OS.

---

**Q25. Correct: D**

Key Vault references require the App Service identity (system- or user-assigned) to have get/list permission on secrets, granted either via Key Vault access policies or the RBAC role "Key Vault Secrets User" (when the vault uses the Azure RBAC permission model). Without this grant, App Service cannot decrypt/read the secret and the reference stays unresolved even though the syntax is correct.

---

**Q26. Correct: B**

Azure Arc projects non-Azure machines into the Azure Resource Manager control plane, which is the prerequisite for Defender for Cloud to manage, assess, and monitor them the same way as native Azure VMs. Enabling Defender for Servers Plan 2 on the Arc-connected machines then provisions Microsoft Defender for Endpoint integration, vulnerability assessment, and full recommendation coverage.

---

**Q27. Correct: D**

Encryption at Host encrypts data at the Azure host level — including temporary disks, disk caches, and data flowing between the VM and storage — without any in-guest agent or OS dependency. ADE, by contrast, uses BitLocker (Windows) or DM-Crypt (Linux) running inside the guest OS via a VM extension.

---

**Q28. Correct: C**

Azure Update Manager is the Microsoft-recommended, Azure-native replacement for the retired Automation Update Management solution. It provides unified patch orchestration, scheduling, and compliance reporting across both Azure VMs and Arc-enabled hybrid servers from a single pane.

---

**Q29. Correct: C**

Azure Confidential VMs use a hardware-based Trusted Execution Environment (AMD SEV-SNP) that encrypts VM memory and isolates guest OS state and CPU registers from the hypervisor and host operator, meeting the requirement that even Microsoft cannot access memory/CPU state.

---

**Q30. Correct: C**

Managed HSM provisions a dedicated, single-tenant FIPS 140-2 Level 3 validated HSM pool exclusively for the customer, and purge protection prevents permanent deletion of keys even by users with high-privilege roles until the retention period expires.

---

**Q31. Correct: B**

Kubernetes NetworkPolicy resources, enforced through Azure Network Policy Manager with Azure CNI, provide pod-level ingress/egress filtering based on namespace and label selectors — the only option operating at the required granularity.

---

**Q32. Correct: B**

A system-assigned managed identity eliminates the need for stored credentials, and Key Vault references (@Microsoft.KeyVault(...) syntax) let App Service resolve the secret value at runtime via the identity's Key Vault access, so no secret value or credential is stored in app settings.

---

**Q33. Correct: A**

Even when the connector status shows 'Connected', the CloudFormation (or Terraform) template must be deployed in AWS to create the cross-account IAM role that grants Defender for Cloud read/scan permissions. Without it, discovery and recommendations never populate even though the connector object itself exists.

---

**Q34. Correct: A**

Governance rules in Defender for Cloud let you define owner assignment logic, remediation SLAs (deadlines), and automated reminder notifications directly tied to specific recommendations or recommendation severities — this is exactly the scenario described.

---

**Q35. Correct: A**

Defender for Cloud's AI threat protection (part of the Defender for AI Services / Defender CSPM for AI capability) monitors Azure OpenAI and AI Foundry workloads for prompt injection, jailbreak attempts, and sensitive data exposure in real time, generating security alerts specific to generative AI usage.

---

**Q36. Correct: B**

Automation rules support condition blocks that can filter on specific properties like the triggering analytic rule name and incident severity. Only when both conditions match does the rule execute its action (Change status to Closed, classification False Positive) — no playbook or code is needed for this simple conditional logic.

---

**Q37. Correct: D**

Attack path analysis (available with Defender CSPM enabled) uses the cloud security graph to correlate exposure, permissions, vulnerabilities, and network reachability, visually mapping exploitable paths from an internet-facing resource to a sensitive data store.

---

**Q38. Correct: A**

Exemptions let you exclude a specific resource (or subscription/management group) from a recommendation's score impact while keeping it visible with a documented reason (e.g., 'Risk accepted') and optional expiration date — exactly matching the audit-with-justification requirement.

---

**Q39. Correct: D**

Defender for Servers on AWS/GCP connectors relies on Azure Arc-enabled servers plus the MDE extension to deliver Microsoft Defender Vulnerability Management data. These auto-provisioning components are configured per-connector and are not enabled by default just because the plan is turned on — if they were left off, the Arc agent and MDE extension never get pushed to the EC2 instances, so no findings appear.

---

**Q40. Correct: B**

Governance rules let you assign owners (including by resource tag), set a remediation timer/grace period before a recommendation impacts the secure score, and configure notifications for overdue items — exactly matching all three requirements in one feature.

---

**Q41. Correct: A**

Fusion is Sentinel's built-in ML-based correlation engine specifically designed to detect multistage attacks by combining low-fidelity signals from different sources into a single high-confidence incident, and it requires no custom KQL authoring — you simply enable/tune it.

---

**Q42. Correct: B**

Defender for AI Services is the Defender for Cloud plan purpose-built for generative AI workloads; it detects threats such as prompt injection, jailbreak, and sensitive data leakage on Azure AI/OpenAI resources, and surfaces the AI workload in the cloud security graph and attack path analysis.

---

