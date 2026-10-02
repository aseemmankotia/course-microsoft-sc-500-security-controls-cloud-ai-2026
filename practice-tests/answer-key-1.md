# Answer Key — Practice Test 1

**Q1. Correct: C**

PIM eligible assignments with approval workflows and configurable maximum activation duration provide true just-in-time, time-bound, approved privileged access — exactly what the scenario requires.

---

**Q2. Correct: B**

A system-assigned managed identity is automatically managed by Azure AD with no secrets to store or rotate manually, and can be granted least-privilege access to Key Vault via RBAC or access policy.

---

**Q3. Correct: B**

The Deny effect blocks the resource write request outright when it violates the policy rule, preventing creation of non-compliant storage accounts.

---

**Q4. Correct: C**

Named locations let you define the office IP range as trusted, and a Conditional Access policy can exclude that trusted location from the MFA requirement, enforcing MFA only for sign-ins outside the office.

---

**Q5. Correct: C**

Microsoft Entra roles (e.g., Global Administrator, User Administrator) govern directory-level administrative actions, while Azure RBAC roles (e.g., Owner, Contributor) govern management-plane access to Azure resources at management group, subscription, resource group, or resource scope.

---

**Q6. Correct: A**

Entitlement management access packages let you bundle resources like Teams, SharePoint sites, and apps into a single request, apply approval workflows, set automatic expiration, and attach recurring access reviews for recertification.

---

**Q7. Correct: C**

PIM eligible assignments require the user to activate the role on demand, and PIM role settings support requiring approval from designated approvers plus a configurable maximum activation duration (e.g., 8 hours), after which the role automatically deactivates.

---

**Q8. Correct: C**

A user-assigned managed identity is created as a standalone Azure resource with its own lifecycle, independent of any compute resource it's attached to. It can be assigned to multiple Azure Functions simultaneously, meeting the requirement for a shared, reusable identity that survives redeployment.

---

**Q9. Correct: D**

The Append effect adds specified fields, such as tags, to a resource during the creation or update request itself, so the CostCenter tag is inserted automatically without blocking or failing the deployment.

---

**Q10. Correct: A**

Entitlement management access packages bundle resources (like Microsoft 365 groups/Teams/apps) into a single request, support self-service requests with owner approval, allow expiration policies, and integrate with recurring access reviews to re-certify or auto-remove access every 90 days — directly meeting all stated requirements.

---

**Q11. Correct: B**

A service SAS scoped to the container, restricted to read permission, and time-boxed to 24 hours grants exactly the access needed without exposing the account key and without requiring an identity in the tenant.

---

**Q12. Correct: B**

Private Link provisions a private endpoint with a private IP address from the VNet's address space, bringing SQL Database traffic entirely onto the Microsoft backbone with no public IP exposure, and it is reachable from on-premises over ExpressRoute or VPN.

---

**Q13. Correct: A**

TDE with a customer-managed key requires the SQL server's managed identity to have Get, Wrap Key, and Unwrap Key permissions on the Key Vault key so the server can retrieve and use the key as the TDE protector.

---

**Q14. Correct: A**

Data Discovery & Classification identifies and labels sensitive columns, and SQL Auditing can be configured to specifically log access to data carrying those sensitivity labels, giving the compliance team targeted audit records tied to the labeled sensitive data.

---

**Q15. Correct: A**

WAF on Application Gateway inspects HTTP/HTTPS requests at Layer 7 and can apply OWASP managed rule sets to detect and block SQL injection, XSS, and other web-based attacks.

---

**Q16. Correct: C**

DDoS Protection Standard adds VNet-specific adaptive tuning of mitigation policies, cost protection for scale-out costs incurred during a documented attack, and access to the DDoS Rapid Response support team, none of which are available in the always-on Basic tier.

---

**Q17. Correct: D**

Always Encrypted encrypts data client-side using keys held by the client driver (backed by a key store such as Key Vault), so plaintext values never appear inside the database engine — protecting the data even from DBAs and Microsoft support staff.

---

**Q18. Correct: C**

Microsoft Defender for SQL (formerly Advanced Threat Protection) analyzes database telemetry using built-in threat detection to raise alerts for anomalous activity such as SQL injection or brute-force attempts, along with recommended remediation actions.

---

**Q19. Correct: A**

Data Discovery & Classification scans table columns, recommends sensitivity labels (e.g., Confidential - GDPR) for columns likely to hold sensitive data such as credit card numbers, and stores that classification metadata for auditing and compliance reporting — it does not encrypt or mask any data itself.

---

**Q20. Correct: D**

Web Application Firewall (WAF), deployed on Application Gateway or Front Door, inspects HTTP/S request content against OWASP Core Rule Sets to block SQL injection, XSS, and other application-layer exploits.

---

**Q21. Correct: D**

DDoS Protection Standard provides always-on traffic monitoring, adaptive tuning based on the protected resource's own traffic baseline, attack analytics and alerting, cost protection guarantees, and access to the DDoS Rapid Response (DRR) team during attacks.

---

**Q22. Correct: B**

A Private Endpoint (Azure Private Link) provisions a network interface with a private IP address from the VNet directly into the storage account, allowing the account's public endpoint to be disabled entirely while all traffic stays on the private network path.

---

**Q23. Correct: A**

Azure Disk Encryption (ADE) uses BitLocker (Windows) or DM-Crypt (Linux) inside the guest OS to encrypt volumes, integrates with Azure Key Vault for key storage/management, and can be verified from within the VM — satisfying the guest-level encryption requirement with customer-controlled keys.

---

**Q24. Correct: B**

The Azure Policy Add-on for AKS installs the Gatekeeper admission controller, which can preventively enforce (not just detect) constraints such as 'Kubernetes cluster should not allow privileged containers,' and compliance results surface in Defender for Cloud's regulatory compliance dashboard.

---

**Q25. Correct: B**

Using a Key Vault reference in App Settings, backed by the App Service's managed identity, retrieves the secret directly from Key Vault at runtime — the secret is never persisted in app config, code, or source control, and identity-based RBAC/access policy governs access.

---

**Q26. Correct: A**

Defender for Servers Plan 1 provides the core protections including automatic Microsoft Defender for Endpoint integration/onboarding and threat detection, at a lower price point than Plan 2, without the extra features (FIM, JIT, adaptive application controls) the company doesn't need.

---

**Q27. Correct: D**

Azure Update Manager is the current unified Azure-native patch management solution, operating through Azure Resource Graph and ARM rather than a Log Analytics workspace, and it supports Azure VMs, Arc-enabled servers, and hybrid machines from a single pane.

---

**Q28. Correct: C**

Key Vault's built-in 'Managed Storage Account' feature natively links to a storage account and automatically regenerates its access keys on a defined schedule, storing the new key as a Key Vault secret version — no custom code or Function App required.

---

**Q29. Correct: D**

The Azure Policy Add-on installs Gatekeeper (OPA) as an admission controller in the cluster. Assigning the built-in Azure Policy definition for privileged containers enforces the rule at admission time, blocking any pod spec that violates it cluster-wide, with no manifest changes needed by developers.

---

**Q30. Correct: C**

Key Vault references (@Microsoft.KeyVault(SecretUri=...)) let App Service resolve the current version of a secret at runtime using its system- or user-assigned managed identity. Rotating the secret in Key Vault updates the value the app receives without code changes or redeployment, and the secret itself is never stored in app code or plain configuration.

---

**Q31. Correct: D**

Key Vault Crypto Officer grants full management permissions (create, import, update, delete) over keys only, without granting access to secrets or certificates, matching the least-privilege requirement.

---

**Q32. Correct: D**

Purge protection enforces a mandatory retention period (default 90 days) during which soft-deleted objects cannot be permanently purged by anyone, including users with elevated RBAC permissions or the vault's own administrators, and it cannot be disabled once turned on.

---

**Q33. Correct: A**

Secure score points are calculated per security control, and each control has a fixed weight representing its relative importance to your overall security posture. A control's total points are distributed across the recommendations within it based on the proportion of healthy resources, so higher-weighted controls yield higher point values even for similarly effortful fixes.

---

**Q34. Correct: B**

Defender for Cloud's native AWS connector uses a CloudFormation template to deploy the required roles, and agentless scanning (via disk snapshot analysis) provides vulnerability and malware coverage for VMs without installing any agent on the instance itself.

---

**Q35. Correct: C**

Fusion rules use machine learning to correlate anomalous or low-fidelity activities from multiple products/data sources over time, generating a single high-fidelity incident that represents a probable multi-stage attack. This is their specific purpose in Sentinel.

---

**Q36. Correct: B**

Automation rules in Sentinel let you define trigger conditions (such as incident creation with Severity = High) and automatically invoke a playbook (Logic App) that can create a ServiceNow ticket and post a Teams message, all without analyst intervention.

---

**Q37. Correct: A**

The Microsoft cloud security benchmark (MCSB, formerly Azure Security Benchmark) is the default standard applied to every subscription in Defender for Cloud and forms the foundation of the secure score and recommendations engine; it cannot be disabled.

---

**Q38. Correct: B**

Defender for Cloud's AI security posture management and threat protection for AI workloads specifically discover AI resources like Azure OpenAI deployments, surface posture recommendations (e.g., network exposure, permission issues), and provide runtime detections for threats such as prompt injection, jailbreak attempts, and sensitive data leakage through prompts.

---

**Q39. Correct: D**

The native cloud connector (the current, recommended AWS/GCP onboarding method in Defender for Cloud) deploys a CloudFormation template that provisions a cross-account IAM role with a trust policy, letting Defender for Cloud assume the role temporarily. No access keys or secrets are stored, satisfying the credential requirement.

---

**Q40. Correct: B**

Automation rules run centrally in Sentinel whenever an incident is created or updated by a specified analytics rule. They support conditions and built-in actions such as changing status, setting classification (benign positive), tagging, and assigning owners — all without needing a Logic App playbook.

---

**Q41. Correct: A**

Scheduled analytics rules in Microsoft Sentinel support a minimum run frequency of 5 minutes, allowing near real-time detection for high-priority scenarios like credential stuffing.

---

**Q42. Correct: D**

Defender for Cloud provides AI security posture management (CSPM recommendations for Azure AI Services/AI Foundry resources) plus a dedicated AI threat protection capability that generates alerts for risks such as jailbreak attempts, prompt injection, and sensitive data leakage in generative AI workloads.

---

