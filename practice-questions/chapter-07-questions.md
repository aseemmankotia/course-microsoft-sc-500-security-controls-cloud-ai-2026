## Chapter 7: Securing Virtual Machines and Disk Encryption — Practice Questions

**Q1.** A company runs Linux VMs in Azure and wants to protect data on the OS and data disks from offline attacks (e.g., disk theft) using volume-level encryption managed inside the guest OS, integrated with Key Vault for key storage. Which solution BEST meets this requirement?

A) Server-Side Encryption (SSE) with platform-managed keys
B) Azure Disk Encryption (ADE) using DM-Crypt with a Key Vault
C) Encryption at Host with a platform-managed key
D) Azure Storage Service Encryption with customer-managed keys only

<details>
<summary>Answer</summary>

**Correct: B**

ADE uses DM-Crypt on Linux (BitLocker on Windows) to encrypt disk volumes inside the guest OS, and it requires an Azure Key Vault to store the encryption keys/secrets — this is the only option that performs in-guest volume encryption against offline disk theft.

**Why the others are wrong:**
- SSE with platform-managed keys encrypts data at the storage layer transparently but does not perform in-guest volume encryption and doesn't use Key Vault.
- Encryption at Host encrypts data at the Azure host level (covers temp disk/cache too) but is not an in-guest BitLocker/DM-Crypt solution and typically doesn't require Key Vault for platform-managed keys.
- Storage Service Encryption with CMK still operates at the storage layer, not inside the guest OS, so it doesn't match the 'volume-level encryption managed inside the guest OS' requirement.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An administrator enables Encryption at Host on a VM that already has Azure Disk Encryption (ADE) applied to its data disk. What happens?

A) Both encryption layers apply simultaneously, providing double encryption
B) ADE is automatically disabled and replaced by Encryption at Host
C) Encryption at Host silently ignores the request and takes no action
D) The operation fails because ADE and Encryption at Host cannot be enabled on the same VM/disk

<details>
<summary>Answer</summary>

**Correct: D**

Azure Disk Encryption and Encryption at Host are mutually exclusive on the same disk — attempting to enable both results in an error, since they operate on overlapping encryption boundaries.

**Why the others are wrong:**
- There is no supported 'double encryption' combination of ADE + Encryption at Host — that stacking is done with Disk Encryption Sets (platform + customer-managed key), not ADE + EaH.
- Enabling Encryption at Host does not automatically disable ADE; the operation is blocked instead.
- The platform does not silently ignore the request — it returns a conflict/error.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A security team wants to reduce the attack surface of RDP (3389) and SSH (22) on production VMs while still allowing administrators temporary, approved access when needed. Which Microsoft Defender for Cloud feature should they enable?

A) Just-in-Time (JIT) VM access
B) Adaptive network hardening only
C) Microsoft Defender for Endpoint integration
D) Azure Update Manager maintenance configuration

<details>
<summary>Answer</summary>

**Correct: A**

JIT VM access, part of Microsoft Defender for Servers Plan 2, locks down management ports by default and opens them only for a limited time window (default max 3 hours) upon an approved request, directly satisfying the requirement.

**Why the others are wrong:**
- Adaptive network hardening recommends NSG rule tightening based on traffic analysis, but it does not provide the temporary, request-based access model.
- Defender for Endpoint integration provides EDR telemetry, not port-level access control.
- Azure Update Manager handles patch compliance, not network port exposure.

</details>

---

**Q4.** A company wants VMs to automatically authenticate to Azure Key Vault to retrieve secrets, without storing any credentials in code or configuration files, and the identity must be independently manageable and assignable to multiple VMs. Which authentication method should be used?

A) System-assigned managed identity
B) User-assigned managed identity
C) Service principal with a client secret stored in Key Vault
D) Shared access signature (SAS) token embedded in the app config

<details>
<summary>Answer</summary>

**Correct: B**

A user-assigned managed identity has a lifecycle independent of any single VM and can be assigned to multiple VMs, matching the requirement for an identity that is reusable and independently manageable.

**Why the others are wrong:**
- System-assigned managed identity is tied 1:1 to the VM lifecycle and is deleted when the VM is deleted — it cannot be shared across multiple VMs.
- A service principal with a stored client secret reintroduces a credential management problem, violating the 'no stored credentials' requirement.
- A SAS token is a storage access mechanism, not an identity, and still represents an embedded credential.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** Which Microsoft Defender for Servers plan tier is required to use Just-in-Time VM access, adaptive application controls, and file integrity monitoring?

A) Defender for Servers Plan 1
B) Defender for Cloud free tier
C) Defender for Servers Plan 2
D) Microsoft Defender for Endpoint standalone license

<details>
<summary>Answer</summary>

**Correct: C**

Defender for Servers Plan 2 includes JIT VM access, adaptive application controls, adaptive network hardening, and file integrity monitoring, in addition to everything in Plan 1.

**Why the others are wrong:**
- Plan 1 provides Microsoft Defender for Endpoint integration and vulnerability assessment only, not JIT/adaptive controls/FIM.
- The free tier of Defender for Cloud provides only basic security posture recommendations with no advanced threat protection features.
- A standalone Defender for Endpoint license provides EDR but not the Defender for Cloud-specific capabilities like JIT access.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** An administrator runs 'az feature register --namespace Microsoft.Compute --name EncryptionAtHost' before enabling Encryption at Host on a VM. Why is this step necessary?

A) Encryption at Host is a subscription-level preview/opt-in feature that must be registered before it can be enabled on supported VM sizes
B) Encryption at Host requires an Azure Key Vault linked to the subscription before use
C) The command installs the BitLocker extension required for Encryption at Host
D) The command grants the VM's managed identity access to Key Vault keys

<details>
<summary>Answer</summary>

**Correct: A**

Encryption at Host must be registered as a feature at the subscription level, and the target VM size must support it, before the setting can be enabled — this is a one-time subscription enablement step, distinct from Key Vault or extensions.

**Why the others are wrong:**
- Encryption at Host with platform-managed keys does not require a Key Vault at all; Key Vault is only needed if using customer-managed keys via a Disk Encryption Set.
- Encryption at Host does not use the BitLocker guest extension — that's ADE's mechanism, not Encryption at Host's.
- This command has nothing to do with managed identity role assignments to Key Vault.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A company migrating from Update Management Center wants centralized, scheduled patch orchestration across on-premises and Azure Arc-enabled servers, with patch compliance reporting. Which service should they use?

A) Azure Automation State Configuration
B) Azure Policy guest configuration
C) Azure Update Manager
D) Microsoft Defender for Cloud secure score

<details>
<summary>Answer</summary>

**Correct: C**

Azure Update Manager is the current unified service for patch orchestration, scheduled maintenance windows, and compliance reporting across Azure, on-premises, and Azure Arc-enabled machines, replacing the older Update Management solution.

**Why the others are wrong:**
- Azure Automation State Configuration manages DSC configuration drift, not OS patch orchestration.
- Azure Policy guest configuration audits/enforces in-guest settings but is not the patch scheduling/compliance engine.
- Secure score is a posture metric in Defender for Cloud, not a patching service.

</details>

---

**Q8.** What is the primary architectural difference between Server-Side Encryption (SSE) of Azure managed disks and Encryption at Host?

A) SSE encrypts only OS disks; Encryption at Host encrypts only data disks
B) SSE encrypts data on the managed disk at rest; Encryption at Host additionally encrypts data on the temp disk and host caches
C) SSE requires Key Vault; Encryption at Host never uses Key Vault under any configuration
D) SSE only works on Windows VMs; Encryption at Host only works on Linux VMs

<details>
<summary>Answer</summary>

**Correct: B**

SSE (enabled by default) encrypts managed disk storage at rest, but temp disks and host-level caches remain unencrypted by SSE alone. Encryption at Host extends encryption to the temp disk and OS/data disk caches at the host level, providing end-to-end coverage.

**Why the others are wrong:**
- Both SSE and Encryption at Host apply to OS and data disks — neither is restricted to only one disk type.
- Encryption at Host CAN use Key Vault-backed customer-managed keys via a Disk Encryption Set, so 'never' is incorrect.
- Both features are OS-agnostic and work on both Windows and Linux VMs.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

