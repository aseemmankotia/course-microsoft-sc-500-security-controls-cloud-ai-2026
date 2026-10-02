## Chapter 3: Securing Azure Storage Accounts — Practice Questions

**Q1.** A company needs to let an external partner (who has no Microsoft Entra ID account in the tenant) upload files to a single blob container for exactly 2 hours, without exposing the storage account key. Which solution BEST meets this requirement?

A) Generate a User Delegation SAS scoped to the container, signed with a user delegation key tied to an Entra ID identity with the appropriate RBAC role
B) Generate an Account SAS scoped to Blob and Queue services and email it to the partner
C) Generate a Service SAS tied to a stored access policy on the container, signed with the account key
D) Assign the partner's personal email as a guest user and grant the Storage Blob Data Contributor role

<details>
<summary>Answer</summary>

**Correct: A**

User Delegation SAS is signed with Entra ID credentials (via a user delegation key) instead of the storage account key, so the account key is never exposed. The bearer token itself can be used by the partner without them needing an Entra ID identity, and it can be scoped tightly with a short expiry.

**Why the others are wrong:**
- Account SAS is signed with the account key and grants broader, harder-to-scope permissions across services — overprivileged for this scenario
- Service SAS still relies on the account key for signing; if the key is ever compromised, all SAS tokens signed with it are compromised too
- Creating a guest account and RBAC assignment is unnecessarily complex, has no built-in time-boxed expiration, and requires B2B setup

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A financial services company must guarantee that a set of blobs cannot be deleted or altered for 7 years, even by a Global Administrator, to satisfy SEC 17a-4(f) requirements. Which feature should be configured?

A) Enable soft delete for blobs with a 365-day retention period
B) Place a legal hold on the container
C) Enable Azure Backup for the storage account with a 7-year retention rule
D) Configure a locked time-based retention immutability policy set to 7 years on the container

<details>
<summary>Answer</summary>

**Correct: D**

A locked time-based retention policy enforces WORM (Write Once, Read Many) at the storage engine level — once locked, the retention period can only be extended (up to 5 times), never shortened or removed, and it cannot be bypassed by any role including Owner.

**Why the others are wrong:**
- Soft delete only protects against accidental deletion for the configured window and can be disabled or the data purged by a privileged admin
- Legal hold has no fixed expiration and can be manually removed by an authorized user at any time, so it doesn't guarantee a fixed 7-year term
- Azure Backup protects against data loss but does not enforce immutability/WORM compliance at the blob level

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** After an admin sets the storage account firewall default action to Deny and adds only the corporate office IP range, an Azure Function App using a system-assigned managed identity (already granted Storage Blob Data Reader) can no longer read blobs. What is the BEST fix?

A) Add the Function App's outbound public IP address to the firewall IP allow list
B) Disable the storage account firewall entirely
C) Re-grant the Storage Blob Data Reader role to the managed identity
D) Add a network rule that permits the Function App's VNet/subnet (via service endpoint or resource instance) or deploy a private endpoint

<details>
<summary>Answer</summary>

**Correct: D**

Network firewall rules are evaluated before authentication/authorization. The RBAC role is already correct, so the fix is to open a valid network path — either a VNet rule (service endpoint) covering the Function App's subnet or a private endpoint.

**Why the others are wrong:**
- Function App outbound public IPs are often dynamic/shared and unreliable for firewall allow-listing
- Disabling the firewall removes the security control entirely instead of fixing the access path
- RBAC permissions were never the issue — the request is being blocked at the network layer before authorization is evaluated

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** An organization has on-premises servers connected via ExpressRoute that need to access a storage account without any traffic traversing the public internet, and requires the storage account to be reachable via a private IP address inside the VNet. Which feature satisfies this requirement?

A) VNet Service Endpoint for Microsoft.Storage
B) Storage account IP firewall rule allowing the ExpressRoute public peering range
C) Private Endpoint (Azure Private Link)
D) Point-to-site VPN gateway

<details>
<summary>Answer</summary>

**Correct: C**

Private Endpoint assigns a private IP address from the VNet to the storage account (via Private Link) and is reachable from on-premises networks over ExpressRoute or VPN using private DNS resolution.

**Why the others are wrong:**
- Service endpoints only work for traffic originating from within Azure VNets — they don't extend to on-premises networks and don't provide a private IP for the storage account
- IP firewall rules still route over the storage account's public endpoint, not fully private
- A point-to-site VPN provides individual client connectivity but doesn't itself provide private connectivity to a storage account

</details>

---

**Q5.** A team wants traffic from an Azure VNet subnet to reach a storage account over the Azure backbone instead of the public internet, but on-premises access is not required and cost must be minimized. Which feature is sufficient?

A) Private Endpoint
B) VNet Service Endpoint (Microsoft.Storage)
C) Azure Bastion
D) Network Security Group with a Storage service tag

<details>
<summary>Answer</summary>

**Correct: B**

Service endpoints are free and route traffic from within the specified VNet subnet over the Azure backbone to the storage account's public endpoint — sufficient when on-premises access isn't required.

**Why the others are wrong:**
- Private Endpoint incurs hourly and per-GB processing charges and is unnecessary if only VNet-originated traffic needs backbone routing
- Azure Bastion is for secure RDP/SSH to VMs, unrelated to storage networking
- An NSG rule with a storage service tag controls traffic flow but doesn't provide the optimized backbone routing that a service endpoint provides

</details>

---

**Q6.** Which storage account setting should be configured to prevent Shared Key authorization entirely and force all data-plane requests to use Microsoft Entra ID?

A) Enable 'Require secure transfer for REST API operations'
B) Enable soft delete for blobs and containers
C) Set 'Allow storage account key access' to Disabled
D) Configure customer-managed keys for encryption at rest

<details>
<summary>Answer</summary>

**Correct: C**

Disabling 'Allow storage account key access' turns off Shared Key authorization (including SAS tokens signed with the account key), forcing all requests to authenticate via Microsoft Entra ID RBAC.

**Why the others are wrong:**
- Secure transfer only enforces HTTPS, it does not affect the authentication method used
- Soft delete protects against data loss, unrelated to authentication method
- CMK controls encryption key management, not authentication method

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A security team is configuring customer-managed keys (CMK) for a storage account using an Azure Key Vault. Which action is mandatory on the Key Vault before CMK encryption can be enabled?

A) Enable soft delete AND purge protection on the Key Vault
B) Enable only HSM-backed (Premium tier) keys
C) Grant the storage account Contributor role on the Key Vault resource
D) Enable diagnostic logging on the Key Vault

<details>
<summary>Answer</summary>

**Correct: A**

Azure requires the Key Vault to have both soft delete and purge protection enabled before it can be used for storage account CMK, to prevent accidental or malicious permanent key deletion that would make encrypted data unrecoverable.

**Why the others are wrong:**
- HSM-backed keys are optional (Premium SKU), not mandatory for CMK to function
- The storage account needs a system-assigned/user-assigned managed identity with Key Vault access policy or RBAC 'Key Vault Crypto Service Encryption User' — not the reverse, and not Contributor
- Diagnostic logging is a monitoring best practice, not a prerequisite for CMK

</details>

---

**Q8.** Which statement about User Delegation SAS is correct?

A) It is signed with a user delegation key that has a maximum lifetime of 7 days and is supported only for Blob storage
B) It is signed with the storage account key and supports Blob, File, Queue, and Table services equally
C) It has no expiration limit and can be revoked instantly by rotating the account key
D) It is only usable by users who have an active Microsoft Entra ID session at the time of access

<details>
<summary>Answer</summary>

**Correct: A**

A user delegation key is obtained via Entra ID credentials and has a maximum validity of 7 days (168 hours); User Delegation SAS is only supported for the Blob service, not File, Queue, or Table.

**Why the others are wrong:**
- It is explicitly NOT signed with the account key — that's what makes it more secure than Service/Account SAS
- SAS tokens always have an expiration; rotating the account key does not affect a user delegation SAS since it isn't signed with the account key
- The bearer holding the SAS URL does not need an active Entra ID session — only the issuer needed Entra ID credentials to generate the delegation key

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

