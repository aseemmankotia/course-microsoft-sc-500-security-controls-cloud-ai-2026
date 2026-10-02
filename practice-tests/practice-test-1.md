# Practice Test 1: SC-500: Azure Security Engineer Certification Prep

- **Questions:** 42
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-1.md`. Track results in `score-tracker.md`.

---

**Q1.** A company wants administrators to obtain Global Administrator privileges only when needed, require manager approval before activation, and automatically expire after 8 hours. Which solution BEST meets these requirements?

A) Assign Global Administrator as a permanent active role assignment
B) Create a Conditional Access policy requiring MFA for all Global Administrator sign-ins
C) Configure Microsoft Entra Privileged Identity Management (PIM) with an eligible assignment, approval required, and maximum activation duration of 8 hours
D) Enable Microsoft Entra Access Reviews on the Global Administrator role, recurring every 8 hours

---

**Q2.** An Azure Function App needs to read secrets from Azure Key Vault. The solution must avoid storing any credentials or secrets in code or application configuration. Which authentication method should you use?

A) A service principal with a client secret stored in application settings
B) System-assigned managed identity granted an appropriate Key Vault access policy or RBAC role
C) A shared access signature (SAS) token embedded in the connection string
D) An Azure AD application registered with a certificate uploaded to the Function App's file system

---

**Q3.** You need an Azure Policy assignment that prevents non-compliant storage accounts (for example, accounts with public blob access enabled) from being created at all, rather than just reporting them. Which policy effect should you configure?

A) Audit
B) Deny
C) Append
D) AuditIfNotExists

---

**Q4.** A company wants to require MFA for all users signing in from outside the corporate office IP range, while allowing sign-ins from the office without an additional MFA prompt. Which Conditional Access configuration meets this requirement?

A) Create a Conditional Access policy that requires MFA for all users and all locations
B) Enable Security Defaults for the tenant
C) Define a trusted named location for the corporate office IP range, then create a Conditional Access policy requiring MFA for all locations except that trusted named location
D) Configure an Identity Protection sign-in risk policy set to trigger at Low risk

---

**Q5.** Which statement correctly differentiates Microsoft Entra ID roles from Azure RBAC roles?

A) Microsoft Entra roles control access to Azure resources such as virtual machines and storage accounts, while Azure RBAC controls access to directory objects such as users and groups
B) Microsoft Entra roles and Azure RBAC roles are interchangeable and can be assigned at the same scope
C) Microsoft Entra roles control access to directory-level resources such as users, groups, and licenses, while Azure RBAC controls access to Azure resources such as subscriptions, resource groups, and individual resources
D) Azure RBAC roles can only be assigned to service principals, while Microsoft Entra roles can only be assigned to users

---

**Q6.** A company frequently grants external partners temporary access to specific Microsoft Teams, SharePoint sites, and applications for the duration of a project. Access must require approval, automatically expire after 90 days, and be recertified periodically. Which Microsoft Entra governance feature should you implement?

A) Microsoft Entra entitlement management access packages with an expiration policy and access reviews enabled
B) Microsoft Entra Privileged Identity Management (PIM) for Groups
C) Conditional Access policies scoped to external guest users
D) Azure Policy assigned at the management group level

---

**Q7.** A company requires that activation of the Global Administrator role in Microsoft Entra ID require approval from a designated security officer, and access must automatically expire after 8 hours. Which configuration meets these requirements?

A) Assign the user as Active in the Global Administrator role and configure a Conditional Access policy requiring MFA
B) Assign the user to a custom Azure RBAC role scoped to the subscription with a start and end date
C) Configure the user as Eligible for the Global Administrator role in Privileged Identity Management, and set role settings to require approval with a maximum activation duration of 8 hours
D) Add the user to a dynamic group that assigns Global Administrator via an Entra role-assignable group with an expiration policy

---

**Q8.** An organization has 30 Azure Functions that all need to authenticate to the same Azure SQL Database and Azure Key Vault without storing credentials. The identity must exist independently of any single function's lifecycle so it can be reused as functions are redeployed or deleted. Which identity type should be used?

A) System-assigned managed identity configured on each function
B) Service principal with a client secret stored in application settings
C) User-assigned managed identity shared across the functions
D) Microsoft Entra B2B guest account with RBAC scoped to the resource group

---

**Q9.** You need to ensure that every new storage account created across the organization has a 'CostCenter' tag applied automatically at creation time if the tag is missing, without blocking the deployment. Which Azure Policy effect should you use?

A) Deny
B) DeployIfNotExists
C) Audit
D) Append

---

**Q10.** A company works with external partners who need temporary access to a specific set of Microsoft 365 resources for the duration of a project. Access must be requested through a self-service process, approved by a resource owner, and automatically reviewed every 90 days, with access expiring if not re-approved. Which Microsoft Entra feature should be used?

A) Microsoft Entra entitlement management access package with a recurring access review policy
B) Conditional Access with a Terms of Use policy
C) Azure AD Connect with a custom organizational unit synchronization rule
D) Privileged Identity Management for group role assignment

---

**Q11.** A retail company must give an external logistics partner temporary read access to a single container in an Azure Storage account for the next 24 hours. The partner does not have an Azure AD account in the company's tenant, and the storage account key must never be shared. Which solution BEST meets this requirement?

A) Regenerate the storage account access key and send the new key to the partner via email
B) Generate a service SAS token scoped to the container with read permission and a 24-hour expiry
C) Enable public (anonymous) read access on the container for 24 hours, then disable it
D) Create a guest Azure AD B2B account for the partner and assign the Storage Blob Data Reader role

---

**Q12.** Contoso runs an Azure SQL Database and wants all traffic between the database and its VNets (including a VNet reachable only via ExpressRoute) to stay off any public IP address, with the database reachable via a private IP address inside the VNet. Which feature should be configured?

A) Virtual network service endpoint for Azure SQL Database
B) Private endpoint using Azure Private Link
C) Azure SQL firewall rule with a virtual network rule
D) Network security group rule allowing inbound traffic on port 1433

---

**Q13.** An administrator needs to configure Transparent Data Encryption (TDE) on an Azure SQL Database using a customer-managed key stored in Azure Key Vault (Bring Your Own Key). Which configuration step is REQUIRED before the key vault key can be set as the TDE protector?

A) Assign a managed identity to the SQL server and grant it Get, Wrap Key, and Unwrap Key permissions on the key vault
B) Enable Always Encrypted with secure enclaves on the database
C) Enable Advanced Threat Protection on the SQL server
D) Turn on Dynamic Data Masking for all sensitive columns

---

**Q14.** A compliance team wants Azure SQL Database to automatically discover columns containing sensitive data such as credit card numbers, label them appropriately, and generate audit records specifically when queries access those labeled columns, for a quarterly compliance report. Which combination of features should be enabled?

A) Data Discovery & Classification to label sensitive columns, plus SQL Auditing configured with sensitivity-label-based audit actions
B) Dynamic Data Masking on all numeric columns
C) Azure SQL Auditing writing all query logs to a storage account, with no classification
D) Microsoft Defender for SQL vulnerability assessment scans only

---

**Q15.** A public-facing web application sits behind an Application Gateway and has recently been targeted by SQL injection and cross-site scripting attempts at the HTTP request layer. Which service should be enabled to inspect and block these Layer 7 attacks using managed OWASP rule sets?

A) Web Application Firewall (WAF) on the Application Gateway
B) Network Security Group on the Application Gateway subnet
C) Azure DDoS Protection Standard
D) Azure Firewall with network rules

---

**Q16.** During the SC-500 exam, a question asks what specifically distinguishes Azure DDoS Protection Standard from the Basic tier that is enabled by default on every Azure virtual network. Which statement correctly describes a Standard tier capability?

A) Standard tier inspects HTTP payloads and blocks SQL injection attempts as part of its mitigation policies
B) Basic tier must be manually enabled and configured per resource before it provides any protection
C) Standard tier provides adaptive, real-time tuning based on the specific traffic patterns of the protected virtual network, along with cost protection and access to the DDoS Rapid Response support team during an attack
D) Standard tier protection only applies to resources deployed as classic (non-Resource Manager) virtual machines

---

**Q17.** A financial services company stores customer Social Security numbers in an Azure SQL Database column. Compliance requires that database administrators and anyone with elevated database permissions must NEVER be able to view the plaintext values, even when querying the table directly. The application must still be able to encrypt and decrypt values using a client-side driver. Which encryption approach BEST meets these requirements?

A) Transparent Data Encryption (TDE)
B) Dynamic Data Masking
C) SQL Database Auditing
D) Always Encrypted

---

**Q18.** A security team wants Azure SQL Database to automatically detect anomalous activities such as SQL injection attempts, brute-force login attempts, and unusual data access patterns, and generate actionable security alerts with remediation guidance. Which capability should they enable?

A) SQL Database Auditing
B) Dynamic Data Masking
C) Microsoft Defender for SQL
D) Transparent Data Encryption (TDE)

---

**Q19.** What does the Data Discovery & Classification feature in Azure SQL Database primarily provide?

A) Identifies sensitive columns and applies sensitivity labels for compliance reporting
B) Encrypts sensitive columns at rest automatically
C) Masks sensitive data from unauthorized query results
D) Scans the database schema for missing security patches and misconfigurations

---

**Q20.** A web application is published to the internet through Azure Application Gateway. The security team must protect the application from common web exploits such as SQL injection and cross-site scripting embedded in HTTP requests, using OWASP Core Rule Sets. Which control should they configure?

A) Network Security Group (NSG)
B) Azure Firewall
C) Azure DDoS Protection Standard
D) Web Application Firewall (WAF)

---

**Q21.** Which Azure DDoS Protection tier applies adaptive real-time tuning by analyzing a resource's actual traffic patterns to build resource-specific mitigation policies, and includes SLA-backed cost protection plus access to the DDoS Rapid Response support team during an active attack?

A) DDoS Protection Basic
B) Azure Firewall Premium
C) Web Application Firewall (WAF)
D) DDoS Protection Standard

---

**Q22.** A company requires that connections from its VNet to an Azure Storage account use a private IP address drawn from the VNet's own address space, and that the storage account's public endpoint can be fully disabled so it is completely isolated from the public internet. Which solution should be implemented?

A) Service Endpoint
B) Private Endpoint (Azure Private Link)
C) VNet Peering
D) Network Security Group (NSG)

---

**Q23.** A company runs Windows and Linux Azure VMs storing regulated financial data. A compliance requirement mandates that OS and data disk volumes be encrypted at the guest operating system level (not just at the storage platform level), using encryption keys the company controls in Azure Key Vault, and the encryption status must be verifiable from within the VM. Which solution should the security engineer implement?

A) Enable Azure Disk Encryption (ADE) using BitLocker/DM-Crypt with keys stored in Azure Key Vault
B) Enable Server-Side Encryption (SSE) with platform-managed keys on the managed disks
C) Enable Azure Storage Service Encryption for the storage account backing the disks
D) Configure Azure Backup to encrypt VM backups using a customer-managed key

---

**Q24.** A security team manages several Azure Kubernetes Service (AKS) clusters and needs to enforce, cluster-wide, that no pod can be deployed with a privileged security context, with the compliance status visible in Microsoft Defender for Cloud's regulatory dashboard. Which approach should they use?

A) Enable Microsoft Defender for Containers to detect and alert on privileged container deployments
B) Enable the Azure Policy Add-on for AKS and assign the built-in initiative that denies privileged containers
C) Create a Kubernetes NetworkPolicy that denies traffic from privileged pods
D) Configure Azure RBAC for Kubernetes Authorization to restrict which users can deploy pods

---

**Q25.** An application hosted on Azure App Service must read a database connection string containing a secret at runtime, without the secret ever being stored in source code, configuration files checked into source control, or deployment slot settings. Which configuration achieves this?

A) Store the connection string as an encrypted App Setting using the platform's default encryption at rest
B) Enable a system-assigned managed identity on the App Service, grant it 'Get' access to the secret in Key Vault, and reference it in App Settings using @Microsoft.KeyVault(SecretUri=...)
C) Store the connection string in an Azure Storage account container and read it at application startup
D) Set the connection string as a 'sticky' deployment slot setting so it never changes on swap

---

**Q26.** A company wants Microsoft Defender for Endpoint sensors automatically deployed to all Azure VMs, along with baseline OS-level threat detection, but explicitly does NOT need File Integrity Monitoring, Just-in-Time VM access, or adaptive application controls, and wants to minimize cost. Which Microsoft Defender for Cloud plan should be enabled?

A) Defender for Servers Plan 1
B) Defender for Servers Plan 2
C) Microsoft Defender for Cloud Apps
D) Microsoft Defender for Cloud free tier (Foundational CSPM)

---

**Q27.** Which Azure service provides a unified patch/update management experience across Azure VMs, Azure Arc-enabled servers, and on-premises machines using a native Azure Resource Manager–based control plane, without requiring a Log Analytics workspace?

A) Windows Server Update Services (WSUS)
B) Azure Automation Update Management (classic)
C) Microsoft Endpoint Configuration Manager
D) Azure Update Manager

---

**Q28.** A security engineer needs Azure Key Vault to automatically regenerate and manage the access keys of an Azure Storage account on a recurring schedule, entirely through native Key Vault functionality, without writing or maintaining any custom automation code. Which configuration meets this requirement?

A) Configure a custom Azure Function triggered by an Event Grid 'SecretNearExpiry' notification to regenerate the storage account keys
B) Set an expiration date on the Key Vault secret object that currently stores the storage account key value
C) Enable Key Vault's 'Managed Storage Account' feature, link the storage account, and define a regeneration period
D) Enable soft delete and purge protection on the storage account

---

**Q29.** A company runs a production AKS cluster shared by multiple development teams. The security team needs to automatically prevent any pod from being scheduled if its container spec sets 'privileged: true', across the entire cluster, without requiring developers to modify their deployment YAML manually each time. Which control should be configured?

A) Enable Microsoft Defender for Containers on the cluster to scan and block privileged container images
B) Configure Kubernetes RBAC ClusterRoleBindings to deny the 'create' verb on the pods resource for all developer accounts
C) Apply a Kubernetes NetworkPolicy that isolates pod-to-pod traffic within each namespace
D) Enable the Azure Policy Add-on for AKS and assign the built-in policy 'Kubernetes cluster should not allow privileged containers'

---

**Q30.** A legacy ASP.NET web app hosted on Azure App Service connects to Azure SQL Database using a username/password connection string (Azure AD authentication cannot be adopted due to a third-party driver limitation). The security team wants the connection string stored securely outside the app's source code and configuration, with the ability to rotate the secret centrally without redeploying or restarting the app to pick up hardcoded values. Which approach BEST meets these requirements?

A) Store the connection string as a plain-text App Service application setting under Configuration
B) Encrypt the connection string using ASP.NET protected configuration and store it directly in web.config
C) Store the secret in Azure Key Vault and reference it from App Service application settings using Key Vault reference syntax, granting the app's managed identity Get permission on secrets
D) Upload the connection string as a text file to an Azure Storage blob container secured with a SAS token

---

**Q31.** An organization has migrated Key Vault access management to Azure RBAC (enableRbacAuthorization set to true). A security engineer needs to grant a PKI team member permission to create, import, and delete cryptographic keys in the vault, but that person must NOT be able to read or manage secrets or certificates stored in the same vault. Which built-in role should be assigned at the Key Vault scope?

A) Key Vault Administrator
B) Key Vault Certificates Officer
C) Key Vault Secrets User
D) Key Vault Crypto Officer

---

**Q32.** A departing Key Vault administrator, who still had valid Key Vault Contributor access on their last day, permanently purged (hard-deleted) a critical encryption key before offboarding completed. Soft-delete was already enabled on the vault, but this did not stop the action. Which setting, if enabled in advance, would have blocked this hard-delete regardless of the administrator's assigned permissions?

A) Diagnostic logging sent to a Log Analytics workspace
B) Restricting network access to the vault using a private endpoint
C) Soft-delete retention period increased to 90 days
D) Purge protection

---

**Q33.** In Microsoft Defender for Cloud, a security team notices that two recommendations with similar remediation effort contribute very different point values toward the secure score. What determines the point value of a security recommendation?

A) The relative weight assigned to the security control based on its potential impact on overall security posture
B) The number of resources currently affected by the recommendation
C) The calendar date the recommendation was published in Defender for Cloud
D) The Azure Policy compliance state of the resource group containing the resource

---

**Q34.** A security team needs to onboard an AWS account to Microsoft Defender for Cloud to enable Defender for Servers and CSPM coverage on EC2 instances, but they want to avoid deploying and maintaining agents on every instance. Which onboarding approach should they use?

A) Manually install Azure Arc agent on every EC2 instance before connecting the account
B) Use the native cloud connector and enable agentless scanning during onboarding via the deployed CloudFormation template
C) Install the legacy Microsoft Monitoring Agent (MMA) on each instance through AWS Systems Manager
D) Enable Azure Policy guest configuration extensions directly on the EC2 instances

---

**Q35.** You want Microsoft Sentinel to automatically correlate multiple low-fidelity, seemingly unrelated alerts from different data sources into a single high-confidence incident using built-in machine learning correlation. Which analytics rule type should you enable?

A) Scheduled query rule
B) Near-real-time (NRT) rule
C) Fusion rule
D) Microsoft security rule

---

**Q36.** A SOC wants every new Microsoft Sentinel incident with severity High to automatically open a ServiceNow ticket and post a Teams alert, without requiring an analyst to manually trigger anything. Which configuration should they implement?

A) A scheduled analytics rule using a KQL query that runs on an hourly cadence
B) An automation rule with a condition of Severity equals High that runs a playbook when an incident is created
C) A workbook pinned to the Sentinel dashboard showing high-severity incident counts
D) A hunting query saved as a bookmark for later analyst review

---

**Q37.** In the Microsoft Defender for Cloud Regulatory Compliance dashboard, which standard is automatically enabled for every subscription by default and cannot be removed?

A) Microsoft cloud security benchmark (MCSB)
B) PCI DSS 4.0
C) NIST SP 800-53
D) ISO/IEC 27001

---

**Q38.** A company has deployed a chatbot using Azure OpenAI Service and wants Defender for Cloud to detect misconfigurations such as overly permissive network access and publicly exposed AI endpoints, as well as flag runtime threats like prompt injection attempts against the model. Which capability should they enable?

A) Defender for Storage
B) Defender for AI workloads (CSPM for AI plus threat protection for Azure AI services)
C) Defender for Key Vault
D) Defender for Resource Manager

---

**Q39.** A security team must onboard an AWS account to Microsoft Defender for Cloud to get CSPM recommendations and workload protection alerts. Company policy prohibits storing long-lived IAM access keys or secrets anywhere in Azure. Which onboarding method BEST meets this requirement?

A) Deploy the classic AWS connector and store the generated access key and secret in Azure Key Vault
B) Install Azure Arc agents on every EC2 instance and manage them as Azure Arc-enabled servers
C) Create a Microsoft Sentinel AWS S3 data connector and route CloudTrail logs into a Log Analytics workspace
D) Deploy the native cloud connector, which creates a CloudFormation stack that establishes a cross-account IAM role Defender for Cloud assumes via a trust relationship

---

**Q40.** A SOC is flooded with duplicate low-severity incidents generated every time a specific benign PowerShell script runs on a set of known DevOps servers. Analysts want these incidents automatically closed as benign positive and tagged, without writing a Logic App, whenever the matching analytics rule fires. Which Microsoft Sentinel feature should be configured?

A) A hunting query saved as a bookmark
B) An automation rule scoped to the specific analytics rule with a condition and a 'Close incident' action
C) A workbook with a KQL-based visualization filter
D) A watchlist containing the DevOps server names

---

**Q41.** You are creating a scheduled analytics rule in Microsoft Sentinel to detect a fast-moving credential-stuffing pattern. You need the rule to evaluate as frequently as the platform allows. What is the minimum run frequency you can configure for a scheduled query rule?

A) 5 minutes
B) 1 minute
C) 15 minutes
D) 1 hour

---

**Q42.** A company deploys Azure OpenAI-based generative AI applications and wants Defender for Cloud to surface misconfiguration recommendations, data exposure risks, and jailbreak/prompt-injection related security alerts specific to these AI workloads. Which capability should be enabled?

A) Microsoft Purview sensitivity labeling
B) Microsoft Sentinel User and Entity Behavior Analytics (UEBA)
C) Defender for APIs workload protection plan
D) Defender for Cloud's AI security posture management and AI threat protection plan

---

