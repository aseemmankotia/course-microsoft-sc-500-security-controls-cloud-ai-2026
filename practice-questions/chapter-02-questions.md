## Chapter 2: Privileged Access: PIM, Managed Identities & RBAC — Practice Questions

**Q1.** A company runs 12 Azure Function Apps that all need identical access to the same Key Vault. The security team wants to manage that permission in one place and have it survive if any single Function App is deleted and redeployed. Which solution BEST meets these requirements?

A) Create a user-assigned managed identity, grant it Key Vault access once, and attach it to all 12 Function Apps
B) Configure a system-assigned managed identity on each Function App and grant each identity Key Vault access individually
C) Create a service principal with a client secret and store the secret in each Function App's application settings
D) Register an app in Entra ID and authenticate using a certificate stored in each Function App's file system

<details>
<summary>Answer</summary>

**Correct: A**

User-assigned managed identities are standalone Azure resources that can be attached to many resources (many-to-one), so permissions are managed once and persist independently of any single Function App's lifecycle.

**Why the others are wrong:**
- System-assigned identities are 1:1 with their resource — you'd have to grant Key Vault access 12 separate times and re-grant it after redeployment.
- Client secrets require manual rotation and storage, creating leakage risk — exactly what managed identities exist to avoid.
- Certificate-based app registration auth also requires manual credential lifecycle management and adds unnecessary complexity.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Your security team wants Global Administrator access to require justification, MFA, and manager approval before use, and any activated session must automatically expire after 8 hours. Which configuration achieves this?

A) Assign Global Administrator as a permanent active assignment with an 8-hour Conditional Access session control
B) Assign Global Administrator as an active assignment with an expiration date set 8 hours in the future
C) Assign Global Administrator as an eligible assignment in PIM, requiring approval, MFA, and justification, with maximum activation duration set to 8 hours
D) Block Global Administrator entirely and rely only on custom Entra ID roles

<details>
<summary>Answer</summary>

**Correct: C**

PIM eligible assignments require explicit activation, and per-role settings can mandate approval, MFA, justification, and a bounded maximum activation duration — matching every requirement stated.

**Why the others are wrong:**
- Active assignment grants standing access immediately; Conditional Access session controls don't enforce PIM's activation/approval workflow.
- An active assignment with an expiration date still grants continuous access until it expires — it doesn't require activation, MFA, or approval each use.
- Blocking the role entirely prevents legitimate use and doesn't satisfy the requirement for controlled, approved access.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A finance department has 6 subscriptions. The security team needs to enforce a mandatory tagging policy consistently across all of them, and new subscriptions added to finance in the future must automatically inherit the same policy. Which approach BEST meets these requirements?

A) Assign the tagging policy initiative separately to each of the 6 subscriptions
B) Create a custom Azure RBAC role at the resource group level that requires tags before resource creation
C) Create an Entra ID administrative unit and assign the policy to it
D) Create a management group containing all finance subscriptions and assign the tagging policy initiative at the management group scope

<details>
<summary>Answer</summary>

**Correct: D**

Management groups let you assign a policy initiative once at a scope above subscriptions; policy inherits down to all current and future subscriptions placed under that management group, satisfying the auto-inheritance requirement.

**Why the others are wrong:**
- Assigning per-subscription works today but does not automatically cover future subscriptions and creates management overhead.
- Azure RBAC controls permissions, not resource compliance rules — it cannot enforce tagging requirements at deployment time.
- Administrative units are an Entra ID construct for scoping directory object management (users/groups) — they don't apply to Azure Policy.

</details>

---

**Q4.** A virtual machine needs to authenticate to Azure Storage. The identity must exist only for the lifetime of that specific VM and must not be reusable by any other resource. Which identity type should be used?

A) User-assigned managed identity
B) Service principal with a certificate
C) System-assigned managed identity
D) App registration with a client secret

<details>
<summary>Answer</summary>

**Correct: C**

System-assigned managed identities are automatically created and tied 1:1 to the resource's lifecycle — deleted automatically when the VM is deleted, and not shareable.

**Why the others are wrong:**
- User-assigned identities are standalone resources meant to be shared across multiple resources — the opposite of what's required here.
- Service principals with certificates require manual credential management, which managed identities are designed to eliminate.
- App registrations with client secrets require secret storage and rotation and are not automatically tied to a VM's lifecycle.

</details>

---

**Q5.** A security administrator needs to grant a helpdesk user the ability to reset passwords for standard users in Entra ID, without granting any access to Azure resources such as VMs or storage. Which role type should be assigned?

A) Azure RBAC "Contributor" role at the tenant root management group
B) Azure RBAC custom role scoped to the subscription
C) Entra ID "Password Administrator" role
D) Entra ID "Owner" role

<details>
<summary>Answer</summary>

**Correct: C**

Entra ID roles govern directory-level tasks like password resets; Password Administrator is a built-in Entra ID role scoped exactly to this task without granting any Azure resource permissions.

**Why the others are wrong:**
- Azure RBAC Contributor grants broad Azure resource management rights and has no bearing on Entra ID password reset capability — RBAC and Entra ID roles are separate systems.
- A custom Azure RBAC role still only controls Azure resources, not Entra ID directory operations like password resets.
- "Owner" is not a valid built-in Entra ID role name — Entra ID's directory role system does not include an "Owner" role (that's an Azure RBAC role).

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** When configuring a PIM role setting, what is the valid range for the maximum activation duration a role can be set to?

A) Fixed at 8 hours, not configurable
B) 1–24 hours
C) 30 minutes–12 hours
D) Cannot be configured, always inherits tenant default

<details>
<summary>Answer</summary>

**Correct: B**

PIM role activation settings allow the maximum activation duration to be configured per role, from 1 up to 24 hours, with 8 hours as the common default.

**Why the others are wrong:**
- 8 hours is only the default value, not a fixed limit — administrators can configure a different duration within the allowed range.
- There is no 30-minute–12-hour restriction; the actual configurable range extends up to 24 hours.
- Maximum activation duration is explicitly configurable per role in PIM role settings, not tenant-wide only.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A compliance team wants every new resource missing a required cost-center tag to automatically have that tag added during deployment, without blocking the deployment. Which Azure Policy effect should be used?

A) Deny
B) Audit
C) Append
D) DeployIfNotExists

<details>
<summary>Answer</summary>

**Correct: C**

The Append effect adds specified fields (like a tag) to a resource during creation or update without failing the deployment.

**Why the others are wrong:**
- Deny would block the deployment entirely if the tag is missing, which violates the requirement to not block deployment.
- Audit only logs non-compliance for reporting — it does not modify the resource or add the tag.
- DeployIfNotExists triggers deployment of a related associated resource (e.g., a diagnostic setting), not adding a field like a tag to the resource itself.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the primary distinction between Azure RBAC roles and Entra ID roles?

A) They are the same permission system, just labeled differently in the portal
B) Entra ID roles only apply to legacy on-premises Active Directory
C) Azure RBAC roles only apply within a single resource group and cannot be scoped higher
D) Azure RBAC controls access to Azure resources (VMs, storage, networking); Entra ID roles control access to Entra ID/directory resources (users, groups, app registrations)

<details>
<summary>Answer</summary>

**Correct: D**

Azure RBAC and Entra ID roles are two separate authorization systems — RBAC manages Azure resource-plane access, while Entra ID roles manage directory-plane operations like user, group, and app registration management.

**Why the others are wrong:**
- They are distinct systems with separate role definitions, assignment models, and scopes — not the same system.
- Entra ID roles govern the modern Entra ID (Azure AD) directory, not on-premises AD, which uses AD DS group policy/ACLs instead.
- Azure RBAC roles can be scoped at management group, subscription, resource group, or individual resource level — resource group is not the only option.

</details>

---

