# Practice Test 2: SC-500: Azure Security Engineer Certification Prep

- **Questions:** 42
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-2.md`. Track results in `score-tracker.md`.

---

**Q1.** A security team configures Privileged Identity Management (PIM) so that the 'Cloud App Administrator' role is eligible for assignment to 5 admins. Activation must require Azure MFA, a business justification, and approval from a designated security lead before the role becomes active, and no admin should ever hold the role permanently. Which PIM configuration satisfies ALL of these requirements?

A) Assign the role as a permanent active assignment to all 5 admins and enable Conditional Access requiring MFA for the role
B) Assign the role as eligible with no activation requirements, then rely on Access Reviews every 90 days to remove unused assignments
C) Assign the role as active but time-bound to 8 hours per day using Conditional Access sign-in frequency
D) Assign the role as eligible with maximum activation duration set, require MFA on activation, require justification, and enable 'Require approval to activate' with the security lead set as approver

---

**Q2.** An organization's CI/CD pipeline running in GitHub Actions must deploy resources to Azure. Security policy prohibits storing any client secrets, certificates, or long-lived credentials in the pipeline. Which solution meets this requirement?

A) Configure a federated identity credential on a user-assigned managed identity or app registration, trusting the GitHub Actions OIDC issuer for the specific repo and branch
B) Create a service principal with a client secret and store the secret as a GitHub encrypted repository secret
C) Create an app registration, generate a self-signed certificate, and upload the certificate to the app registration for use by the pipeline
D) Assign the Contributor role directly to the GitHub organization using Azure RBAC without creating an identity object

---

**Q3.** You must ensure that all users assigned the Global Administrator and Exchange Administrator roles authenticate using only phishing-resistant methods (FIDO2 security key, certificate-based authentication, or Windows Hello for Business) — SMS and standard push MFA must NOT satisfy this requirement. Which Conditional Access grant control should you configure?

A) Require multifactor authentication
B) Require authentication strength, and select the built-in 'Phishing-resistant MFA' authentication strength
C) Require device to be marked as compliant
D) Require approved client app

---

**Q4.** A tenant has multiple Global Administrators. One Global Administrator needs to modify Azure RBAC role assignments at the root management group scope to grant Owner access on a subscription, but currently receives an 'Insufficient privileges' error when attempting this in the Azure portal. What is the cause and correct fix?

A) The user needs the Privileged Role Administrator role added in addition to Global Administrator
B) The user's PIM eligible assignment for Global Administrator has expired and must be reactivated with MFA
C) By default, Global Administrator has no access to Azure resources; the admin must use the 'Global Administrator: Access management for Azure resources' elevation setting, which grants User Access Administrator at root scope
D) Azure RBAC role assignments can only be performed by the subscription's original creator account, regardless of Entra role

---

**Q5.** Your organization enforces an Azure Policy at the tenant root management group that denies resource deployment outside the 'East US' and 'West Europe' regions. A compliance testing team in a specific subscription has an approved, time-boxed exception to deploy a single resource type in 'North Europe' for 30 days. What should you configure to allow this without weakening the policy for any other subscription?

A) Modify the policy assignment's parameter to add 'North Europe' to the allowed locations list at the management group scope
B) Move the compliance testing subscription out of the management group so the policy no longer applies to it
C) Create a policy exemption scoped to the specific subscription and resource, with a 'waiver' category and an expiration date set to 30 days
D) Apply a resource lock on the subscription to prevent the policy from evaluating it during the testing window

---

**Q6.** External auditors from a partner organization need temporary access to a finance application for a 90-day engagement. Access must require approval from the finance resource owner, automatically expire after 90 days, and be subject to a recurring access review to confirm continued need. Guest accounts should be created only when access is approved, not in advance. Which capability should you configure?

A) Configure an Entra ID entitlement management access package with a policy requiring resource-owner approval, an assignment expiration of 90 days, and an attached access review
B) Create guest B2B invitations manually for each auditor and assign them directly to the Azure RBAC role on the finance application
C) Add the auditors to a Conditional Access named location and require MFA for that location
D) Use Microsoft Purview Information Barriers to segment finance data from other departments

---

**Q7.** A company requires that activation of the eligible Global Administrator role in Privileged Identity Management (PIM) must require a business justification, mandatory Azure MFA at the moment of activation, and approval from a designated security approver. The activation must also automatically expire after 8 hours. Which configuration BEST meets these requirements?

A) Assign the role as an Active, permanent assignment and enforce a Conditional Access policy requiring MFA for the role
B) Configure a recurring Access Review on the role that runs every 8 hours
C) Create a Conditional Access policy that enforces a sign-in frequency of 8 hours for users assigned the Global Administrator role
D) In the role's PIM settings, set the maximum activation duration to 8 hours, and enable requirements for justification, MFA on activation, and approval with a specified approver

---

**Q8.** A security team must require phishing-resistant authentication (such as FIDO2 security keys or Windows Hello for Business) specifically when users in directory admin roles access the Azure portal, while all other users continue using standard Microsoft Authenticator push MFA. Which configuration meets this with the LEAST administrative effort?

A) Enable Security defaults for the tenant to enforce MFA for all administrator accounts
B) Configure per-user MFA (legacy) on the admin accounts to require certificate-based authentication
C) Create a Conditional Access policy targeting the Azure portal cloud app, assigned to the directory admin roles, requiring the 'Phishing-resistant MFA' authentication strength
D) Create an Identity Protection user risk policy that forces a password reset for admin accounts

---

**Q9.** A GitHub Actions workflow running on GitHub-hosted runners needs to deploy resources to an Azure subscription. The security requirement states that NO secrets, certificates, or client secrets may be stored in GitHub, and authentication must use short-lived tokens exchanged via OIDC scoped to a single app registration. Which solution meets this requirement?

A) Add a federated identity credential to the app registration's service principal, configured to trust GitHub's OIDC token issuer for the specific repository and branch
B) Assign a system-assigned managed identity to the app registration used by the workflow
C) Generate a client secret for the app registration and store it as an encrypted GitHub Actions secret
D) Provision a user-assigned managed identity and reference it directly in the GitHub Actions YAML using the azure/login action

---

**Q10.** A compliance team finds that a specific storage account violates an Azure Policy requiring customer-managed key encryption. The business needs a documented, time-boxed waiver for 30 days while migration work completes, but the resource must continue to be evaluated by the policy and reported as non-compliant during that period — it must NOT simply be removed from evaluation. Which action satisfies this?

A) Add the storage account's resource ID to the policy assignment's 'Not scope' (exclusions) list
B) Change the policy assignment's enforcement mode to 'DoNotEnforce'
C) Create a Policy exemption with category 'Waiver', scoped to the specific storage account, with an expiration date 30 days out
D) Apply a ReadOnly resource lock to the storage account for 30 days

---

**Q11.** A financial services company stores highly sensitive SSN values in an Azure SQL Database column. Neither application developers nor DBAs with database access should ever see the plaintext values, but the application must still perform LIKE pattern-matching and range comparisons directly against the encrypted column without decrypting data on the client first. Which solution BEST meets these requirements?

A) Transparent Data Encryption (TDE)
B) Dynamic Data Masking
C) Always Encrypted with secure enclaves
D) Always Encrypted (without secure enclaves)

---

**Q12.** Your organization needs to inspect outbound HTTPS traffic leaving a virtual network to detect and block exploit attempts against known CVEs, including decrypting and inspecting the TLS payload for malicious content. The solution must integrate with the existing Azure Firewall deployment. Which feature should you enable?

A) Azure Firewall Standard with application rules
B) Network Security Groups with application security groups
C) Azure Web Application Firewall on Application Gateway
D) Azure Firewall Premium with TLS inspection and IDPS in Alert and Deny mode

---

**Q13.** A company hosts 200 public IP addresses across several virtual networks, but only 5 of those IPs host mission-critical services requiring volumetric DDoS mitigation, cost protection, and mitigation reporting. Enabling full protection on all 200 IPs is cost-prohibitive. Which DDoS protection approach should you implement?

A) Azure DDoS Protection Standard (Network Protection tier) enabled on all affected virtual networks
B) Rely on Basic DDoS protection (default, always-on) for all resources
C) Configure Azure Firewall rules to mitigate DDoS attacks on the affected subnets
D) Azure DDoS IP Protection tier applied only to the 5 critical public IP addresses

---

**Q14.** You create a private endpoint for the blob service of an Azure Storage account inside a hub virtual network. On-premises clients connect over ExpressRoute and use their own on-premises DNS servers rather than Azure DNS. Name resolution for the storage account FQDN from these on-premises clients must return the private endpoint's private IP address. What should you configure?

A) Configure conditional forwarding on the on-premises DNS servers to an Azure DNS Private Resolver that forwards queries to the privatelink.blob.core.windows.net zone
B) Enable 'Integrate with private DNS zone' when creating the private endpoint using the default Azure-hosted privatelink.blob.core.windows.net zone
C) Add a manual public DNS A record on the on-premises DNS server pointing to the private endpoint's private IP address
D) Disable the storage account's public endpoint and rely on Azure's default DNS resolution

---

**Q15.** You must configure customer-managed keys (CMK) for encryption at rest on an Azure Storage account, using a key stored in Azure Key Vault. Which combination of configurations is REQUIRED before the storage account can successfully use the CMK?

A) Enable infrastructure encryption on the storage account and store the key using Azure AD Connect
B) Create a Shared Access Signature scoped to the Key Vault and reference it in the storage account's encryption settings
C) Grant the storage account the Owner role on the Key Vault's resource group
D) Enable the storage account's managed identity, grant it Key Vault permissions for get, wrapKey, and unwrapKey, and enable Key Vault soft-delete and purge protection

---

**Q16.** An Application Gateway WAF_v2 deployment protecting a public web app is generating frequent false-positive blocks from the OWASP Core Rule Set (CRS) against one legitimate query string parameter. Separately, you must block any single client IP address that exceeds 100 requests per minute. Which combination of WAF configuration changes addresses BOTH requirements?

A) Enable Prevention mode globally and increase the CRS sensitivity level
B) Switch the CRS rule set to Detection mode and add a custom geo-filtering rule
C) Add a managed rule exclusion for the specific query string parameter, and create a custom rate-limiting rule that matches requests per minute per IP
D) Disable the OWASP Core Rule Set entirely and rely only on custom rules

---

**Q17.** A storage account contains a container with blobs shared externally using ad-hoc SAS tokens with a 30-day expiry. The security team discovers one token was leaked and is being used by an unauthorized third party. The token has 12 days remaining before it expires, and rotating the storage account keys would break dozens of other active integrations. What should have been configured in advance to allow immediate revocation of only the compromised token without regenerating account keys?

A) A stored access policy on the container, associated with the SAS, which can be modified or deleted to immediately invalidate the token
B) Azure AD Conditional Access policy scoped to the storage account resource provider
C) A shorter default TTL enforced via Azure Policy on all storage accounts
D) Customer-managed keys with Azure Key Vault so the key can be disabled

---

**Q18.** A healthcare application stores patient SSNs in an Azure SQL Database column. Compliance requires that even database administrators with full db_owner rights must never be able to view the plaintext SSN values, while the application must still be able to perform equality lookups on that column for record matching. Which control meets this requirement?

A) Dynamic Data Masking on the SSN column
B) Always Encrypted with secure enclaves, using deterministic encryption on the SSN column
C) Transparent Data Encryption (TDE) with a customer-managed key
D) Row-Level Security combined with an Azure AD security group for DBAs

---

**Q19.** A company deploys a private endpoint for an Azure SQL server, and the associated Private DNS Zone is linked to the VNet. Cloud-hosted VMs resolve the private endpoint FQDN correctly, but on-premises servers connected via ExpressRoute cannot resolve the same FQDN to the private IP and instead reach the public endpoint. What should be configured to fix on-premises name resolution?

A) Add a static hosts file entry for the private endpoint FQDN on every on-premises server
B) Re-link the Private DNS Zone to a second virtual network peered with on-premises
C) Disable the public endpoint on the SQL server so DNS falls back to the private IP automatically
D) Deploy Azure DNS Private Resolver with an inbound endpoint, and configure on-premises DNS with a conditional forwarder to that inbound endpoint's IP for the privatelink zone

---

**Q20.** A security team needs to inspect outbound internet-bound TLS traffic from a hub VNet for malware signatures and known bad IOCs at the network layer, decrypting and re-encrypting the traffic transparently for all VMs behind the firewall. Which capability should they enable?

A) Azure Web Application Firewall custom rules on Application Gateway
B) Azure Firewall Premium with TLS inspection and IDPS in alert-and-deny mode
C) Network Security Group flow logs analyzed by Microsoft Sentinel
D) Azure Firewall Standard with FQDN-based application rules

---

**Q21.** An Azure WAF policy using the OWASP Default Rule Set is blocking legitimate customer requests because a specific request header contains a value that matches a SQL injection signature in rule 942100, even though the field is a harmless product SKU. Blocking has caused a spike in support tickets. What is the recommended remediation that fixes the false positive with minimal reduction in overall protection?

A) Set the entire WAF policy to Detection mode instead of Prevention mode
B) Add a rule exclusion that excludes the specific request header from evaluation by rule 942100 only
C) Disable rule group SQLi (942) entirely across the policy
D) Increase the WAF anomaly scoring threshold to 20 for all requests

---

**Q22.** A startup runs a single public-facing VM with one static public IP and wants cost-effective protection against volumetric and protocol DDoS attacks without paying for tenant-wide, multi-resource DDoS coverage across an entire virtual network. Which Azure offering best fits this requirement?

A) Azure DDoS Network Protection (formerly DDoS Protection Standard)
B) Azure DDoS IP Protection
C) Basic (infrastructure-level) DDoS protection only
D) Azure Firewall Premium IDPS

---

**Q23.** A company runs an AKS cluster where multiple pods need to retrieve secrets from Azure Key Vault without embedding any credentials in container images or Kubernetes Secrets objects. Microsoft Entra Pod Identity has already been retired. Which approach should you implement?

A) Enable Azure AD Pod Identity (preview) and assign a managed identity to the node pool
B) Store the Key Vault secrets as base64-encoded Kubernetes Secrets objects synced via a CronJob
C) Deploy the Azure Key Vault Provider for Secrets Store CSI Driver and configure Azure AD Workload Identity with a federated credential for the pod's service account
D) Grant the AKS cluster's system-assigned managed identity the Key Vault Reader role and reference secrets via environment variables in the pod spec

---

**Q24.** A financial services company requires that all managed disks attached to its Azure VMs be encrypted twice at rest — once with a Microsoft platform-managed key and once with a customer-managed key stored in Azure Key Vault — with no changes required inside the guest operating system. Which feature should you enable?

A) Server-side encryption (SSE) with customer-managed keys plus infrastructure (double) encryption
B) Azure Disk Encryption (ADE) with BitLocker
C) Azure Storage Service Encryption with Microsoft-managed keys
D) Encryption at host with Microsoft-managed keys only

---

**Q25.** You configure an Azure App Service web app to retrieve a database connection string from Key Vault using a Key Vault reference in an app setting. The app has a system-assigned managed identity enabled and the setting is formatted as @Microsoft.KeyVault(SecretUri=https://contoso-kv.vault.azure.net/secrets/dbConn/). The reference fails to resolve at runtime. What is the most likely missing configuration?

A) Enable Key Vault soft-delete and purge protection
B) Configure the App Service to use a user-assigned managed identity instead, since system-assigned identities cannot access Key Vault
C) Add the Key Vault's private endpoint IP address to the App Service inbound IP restrictions
D) Grant the App Service managed identity the "Key Vault Secrets User" RBAC role on the vault and set the app setting value to @Microsoft.KeyVault(SecretUri=...)

---

**Q26.** Your organization has 200 on-premises Windows servers with no existing connection to Azure. They must be enrolled in Microsoft Defender for Endpoint and appear in Microsoft Defender for Cloud with vulnerability assessment and unified security recommendations. What should you do first?

A) Install the Log Analytics agent (MMA) directly and connect it to a Defender for Cloud workspace
B) Connect the servers to Azure Arc-enabled servers, then enable Defender for Servers Plan 2
C) Directly onboard servers to Microsoft Defender for Endpoint using the local onboarding script only
D) Deploy Azure Automanage machine configuration for on-premises servers

---

**Q27.** Which statement accurately differentiates "Encryption at Host" from "Azure Disk Encryption (ADE)" on Azure VMs?

A) ADE encrypts the VM host's local cache while Encryption at Host only encrypts OS disks
B) Encryption at Host requires Azure Key Vault while ADE does not support customer-managed keys
C) ADE and Encryption at Host are mutually required and must both be enabled together on every VM
D) Encryption at Host encrypts data on the VM host machine, including temp disks and caches, without needing an in-guest agent, while ADE relies on BitLocker/DM-Crypt inside the guest OS

---

**Q28.** A company runs Azure VMs and on-premises Azure Arc-enabled servers across several subscriptions. They need centralized, schedule-based patch orchestration with cross-environment compliance reporting, replacing the retired Azure Automation Update Management solution. Which service should they adopt?

A) Microsoft Endpoint Configuration Manager only
B) Azure Automation Desired State Configuration (DSC)
C) Azure Update Manager (formerly Azure Automation Update Management)
D) Microsoft Defender for Cloud regulatory compliance dashboard

---

**Q29.** A financial services company runs highly sensitive workloads on Azure VMs. Compliance requires that data in memory and CPU register state remain encrypted and inaccessible to Microsoft operators, the hypervisor, and host administrators at all times, even if the underlying host is compromised. Which solution should you implement?

A) Azure Disk Encryption (ADE) with customer-managed keys
B) Encryption at host
C) Azure Confidential VMs using AMD SEV-SNP
D) Server-side encryption of managed disks with platform-managed keys

---

**Q30.** An organization requires FIPS 140-2 Level 3 validated HSM-backed keys used for digital signing, running in a single-tenant, dedicated HSM pool isolated from other customers, with permanent deletion prevented even for users holding the Owner role. Which solution meets all these requirements?

A) Azure Key Vault Standard tier with soft-delete enabled
B) Azure Key Vault Premium tier with purge protection enabled
C) Azure Key Vault Managed HSM with purge protection enabled
D) Azure Key Vault Premium tier using both RBAC and access policies simultaneously

---

**Q31.** An AKS cluster hosts multiple team namespaces on a single node pool using Azure CNI. You must ensure that pods in the 'finance' namespace accept inbound traffic only from pods in the 'reporting' namespace, and reject all other pod-to-pod traffic, without affecting VM-level or subnet-level routing. Which feature should you configure?

A) Azure Firewall network rules applied to the AKS subnet
B) Kubernetes NetworkPolicy objects enforced by Azure Network Policy Manager
C) Application security groups (ASGs) applied to AKS node NICs
D) Network security groups (NSGs) applied to the AKS subnet

---

**Q32.** A web app hosted on Azure App Service must retrieve a database connection string secret from Azure Key Vault at runtime. The solution must avoid storing the secret value directly in app settings and must not embed any static credentials for authenticating to Key Vault. Which configuration meets these requirements?

A) Mount Azure Key Vault as an Azure Files share on the App Service and read the secret from the mounted file
B) Enable a system-assigned managed identity on the App Service, grant it Key Vault access, and use a Key Vault reference in application settings
C) Use a service principal with a client secret stored in the deployment pipeline to fetch the secret at build time
D) Store the secret in App Service application settings, encrypted using a customer-managed key

---

**Q33.** A security engineer connects an AWS account to Microsoft Defender for Cloud using the native cloud connector with the Defender CSPM plan enabled. Six hours later, no AWS resources appear under Inventory. The engineer confirms the connector shows a 'Connected' status. What is the MOST likely cause?

A) The AWS account has not deployed the CloudFormation template that grants Defender for Cloud the required IAM role and permissions
B) Defender for Cloud only supports Azure Arc-enabled AWS EC2 instances, not native connectors
C) The AWS account region must match the Azure subscription's primary region before resources sync
D) Defender CSPM requires Microsoft Sentinel to be provisioned in the same tenant before AWS resources are indexed

---

**Q34.** A CISO wants specific Defender for Cloud recommendations automatically assigned to named resource owners with a 14-day remediation deadline, and wants email reminders sent as the deadline approaches. Which feature should be configured?

A) Governance rules
B) Workflow automation triggered on recommendation creation
C) Secure score exemptions with a review date
D) Azure Policy remediation tasks scoped to the recommendation

---

**Q35.** Your organization deployed Azure OpenAI-based generative AI applications through Azure AI Foundry. Security needs real-time detection of prompt injection attempts and sensitive data leakage happening at the model prompt/response layer. Which capability should be enabled?

A) Microsoft Defender for Cloud AI threat protection (Defender for AI Services)
B) Microsoft Purview sensitivity labels applied to the AI Foundry workspace
C) Microsoft Defender for Cloud CSPM attack path analysis
D) Microsoft Sentinel Fusion analytics rule for anomalous sign-ins

---

**Q36.** A SOC lead wants an automation rule in Microsoft Sentinel that automatically closes incidents as 'False Positive' ONLY when they originate from a specific analytic rule named 'Test Detection - Dev Sandbox' AND have a severity of Informational. Where must this logic be configured?

A) In the analytic rule's alert suppression settings using KQL filters
B) In the automation rule's conditions section, filtering on Analytic rule name and Severity before the 'Change status' action runs
C) In a Logic App playbook triggered on incident creation with a conditional branch
D) In Sentinel's incident settings under grouping and alert clustering rules

---

**Q37.** During a Defender for Cloud review, an analyst wants to see which internet-exposed VM could be used by an attacker to laterally move to a VM hosting a database containing sensitive data, based on network configuration, identity permissions, and vulnerability data combined. Which Defender for Cloud capability provides this?

A) Regulatory compliance dashboard
B) Secure score recommendations list
C) Microsoft Sentinel entity behavior analytics
D) Attack path analysis

---

**Q38.** A resource owner insists a flagged Defender for Cloud recommendation for a legacy VM is a known, accepted risk that should stop lowering the subscription's secure score, while still remaining visible for audit purposes with a documented justification and expiry date. What should the security engineer configure?

A) Create an exemption for the specific resource with a reason category and expiration date
B) Disable the recommendation at the policy definition level
C) Delete the recommendation from the regulatory compliance dashboard
D) Set the recommendation's severity to Low in the assessment policy

---

**Q39.** You onboarded an AWS account to Microsoft Defender for Cloud using the native cloud connector and enabled the Defender for Servers Plan 2 plan. After six weeks, the connector shows status 'Connected', but all EC2 instances display 'Not applicable' for vulnerability assessment recommendations. No Log Analytics agent was ever deployed to the instances. What should you do to get vulnerability findings for these EC2 instances?

A) Manually install the Log Analytics (MMA) agent on each EC2 instance and restart the connector
B) Move the EC2 instances into an Azure subscription using Azure Migrate before enabling scanning
C) Enable the Microsoft Defender for Cloud Apps connector for AWS to extend coverage to EC2
D) Enable the Azure Arc auto-provisioning and Microsoft Defender for Endpoint extension auto-provisioning options in the connector's configuration settings

---

**Q40.** Your security team wants a specific Defender for Cloud recommendation to NOT immediately count against the secure score, to automatically assign an owner based on the resource's 'Owner' tag, and to trigger an email reminder if the recommendation isn't remediated within 14 days. Which Defender for Cloud capability should you configure?

A) Workflow automation using a Logic App triggered on recommendation creation
B) A governance rule applied to that recommendation
C) An Azure Policy exemption scoped to the resource group
D) A custom security contact with subscription-level alert notifications

---

**Q41.** Your SOC wants Microsoft Sentinel to automatically correlate an anomalous sign-in with a subsequent unusual resource deployment across different data connectors, using Microsoft's built-in machine learning to detect the multistage attack pattern — without your team writing custom KQL joins across tables. Which analytics rule type should be enabled?

A) A Fusion rule
B) A Near-real-time (NRT) analytics rule
C) A Microsoft security incident creation rule
D) A scheduled query rule with a 5-minute run frequency

---

**Q42.** Your organization deployed Azure OpenAI Service and wants Defender for Cloud to detect prompt injection and jailbreak attempts in real time, and to include the AI workload and its connected data stores in attack path analysis. Which Defender for Cloud plan should you enable?

A) Defender for App Service
B) Defender for AI Services
C) Defender for Storage with malware scanning enabled
D) Microsoft Purview sensitivity labels applied to the AI resource group

---

