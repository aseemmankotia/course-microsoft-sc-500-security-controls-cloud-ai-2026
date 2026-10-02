## Chapter 9: App Service, Serverless & Key Vault Secrets Management — Practice Questions

**Q1.** A web app needs to retrieve a database password from Key Vault at runtime without storing any credential in code or configuration files. Which approach BEST meets this requirement?

A) Store the password in an encrypted connection string inside web.config
B) Enable a System-assigned managed identity on the App Service, grant it the 'Key Vault Secrets User' RBAC role on the vault, and reference the secret via @Microsoft.KeyVault() in application settings
C) Store the password as a certificate in an Azure AD app registration
D) Inject the password into a deployment slot during CI/CD pipeline execution

<details>
<summary>Answer</summary>

**Correct: B**

Managed identity plus RBAC role assignment plus a Key Vault reference in App Settings is the standard, code-free, credential-free retrieval pattern the exam expects.

**Why the others are wrong:**
- Encrypted connection strings still store a static secret that must be managed and rotated manually
- App registration certificates authenticate identities, not application secrets like DB passwords
- Deployment slot injection still requires the secret to exist somewhere in pipeline config, defeating the goal

</details>

---

**Q2.** A Key Vault has soft-delete and purge protection both enabled. A Key Vault Administrator attempts to permanently purge a secret 10 days after it was soft-deleted, while the retention period is set to 90 days. What happens?

A) The purge succeeds because the user holds the Key Vault Administrator role
B) The purge fails; purge protection blocks permanent deletion until the retention period expires, regardless of role
C) The purge succeeds only if the vault uses the access policy permission model instead of RBAC
D) The secret is automatically re-created with a new version and the purge is silently ignored

<details>
<summary>Answer</summary>

**Correct: B**

Purge protection overrides any role's ability to purge until the soft-delete retention window fully elapses — this is a tenant-wide safeguard against malicious or accidental deletion.

**Why the others are wrong:**
- No role, including Owner or Key Vault Administrator, can bypass purge protection
- Purge protection behavior is identical under both RBAC and access policy permission models
- Key Vault does not auto-recreate purged/soft-deleted objects; it simply blocks the purge action

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A company currently uses Key Vault access policies granting 'Get' and 'List' on secrets to an app's managed identity. Compliance now requires that permissions be manageable through Azure Policy and audited via Azure AD PIM. What should you do?

A) Add additional access policy entries covering keys and certificates as well
B) Switch the vault to the Azure RBAC permission model and assign a built-in role such as Key Vault Secrets User scoped to the resource group
C) Apply Conditional Access policies directly to the Key Vault resource
D) Grant the managed identity the Owner role at the subscription level

<details>
<summary>Answer</summary>

**Correct: B**

Only the Azure RBAC permission model integrates with Azure AD role assignments, PIM, and Azure Policy auditing; access policies do not support these governance features.

**Why the others are wrong:**
- Expanding access policy scope does not add PIM or Azure Policy support
- Conditional Access governs sign-in conditions, not object-level data plane permissions in Key Vault
- Owner at subscription scope is excessive privilege and unrelated to the compliance requirement

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Which Azure Functions configuration eliminates the need to store a storage account connection string when a Function needs blob access?

A) Identity-based connections: enabling managed identity on the Function App and assigning a data-plane RBAC role such as Storage Blob Data Owner
B) A shared access signature saved in local.settings.json
C) A function key defined in host.json
D) A client secret from an Azure AD app registration stored in Key Vault

<details>
<summary>Answer</summary>

**Correct: A**

Identity-based bindings use the Function App's managed identity plus an RBAC role assignment on the target resource, removing the need for any stored secret.

**Why the others are wrong:**
- SAS tokens are still secrets that require secure storage and rotation
- Function keys authenticate callers of the HTTP trigger, not the Function's outbound access to Storage
- A client secret is itself a credential that must be protected — it does not remove secret management overhead

</details>

---

**Q5.** A company requires Key Vault to be completely inaccessible from the public internet, reachable only from inside its VNet, while still allowing Azure Backup (a trusted Microsoft service) to access it for automated key operations. Which configuration meets this requirement?

A) Enable the Key Vault firewall to allow specific virtual networks only, with no private endpoint
B) Configure Network Security Group rules on the subnet and leave the Key Vault firewall at its default (allow all)
C) Deploy a Private Endpoint for the Key Vault, set public network access to Disabled, and enable 'Allow trusted Microsoft services to bypass this firewall'
D) Place Azure Front Door with WAF in front of the Key Vault endpoint

<details>
<summary>Answer</summary>

**Correct: C**

A private endpoint removes public exposure, disabling public network access enforces private-only connectivity, and the trusted-services bypass flag is required specifically to let services like Azure Backup continue functioning.

**Why the others are wrong:**
- Firewall-only VNet rules still leave a public endpoint reachable unless public access is disabled
- NSG rules control subnet traffic but do not restrict the Key Vault's own public endpoint
- Front Door/WAF is designed for HTTP web workloads, not Key Vault's data-plane REST API security model

</details>

---

**Q6.** Which App Service Key Vault reference syntax ensures the app always retrieves the LATEST version of a secret automatically after rotation?

A) @Microsoft.KeyVault(SecretUri=https://myvault.vault.azure.net/secrets/mysecret/abc123version)
B) @KeyVault(myvault/mysecret)
C) https://myvault.vault.azure.net/secrets/mysecret
D) @Microsoft.KeyVault(VaultName=myvault;SecretName=mysecret)

<details>
<summary>Answer</summary>

**Correct: D**

Omitting the version and using VaultName;SecretName causes App Service to always resolve the current/latest secret version at each refresh cycle.

**Why the others are wrong:**
- Including a specific version in SecretUri pins the app to that exact version, requiring manual updates after rotation
- This is not valid Key Vault reference syntax recognized by App Service
- A raw URL is not evaluated as a Key Vault reference — it would be treated as a literal string value

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** You configure a rotation policy on an RSA key in Key Vault with an expiry time of 90 days, a notify time of 30 days before expiry, and action type 'Rotate'. What occurs automatically?

A) Key Vault emails the administrator 30 days before expiry, but rotation must still be triggered manually
B) Key Vault generates a new key version automatically at the expiry time; an Event Grid notification fires 30 days before expiry
C) Key Vault disables the key at expiry until someone manually rotates it
D) The rotation policy applies only to certificates, not keys

<details>
<summary>Answer</summary>

**Correct: B**

With action type 'Rotate', Key Vault natively auto-generates a new key version at the configured expiry, while the notify time independently triggers an Event Grid event for downstream automation or alerting.

**Why the others are wrong:**
- Manual triggering is not required when action type is set to Rotate — this describes the 'Notify'-only action type instead
- Keys are not disabled at expiry; a new version is created and the old version remains usable until removed
- Key rotation policies apply to Key Vault keys; certificate renewal is a separate, similar mechanism scoped to certificates

</details>

---

**Q8.** What is the primary structural difference between Key Vault access policies and Azure RBAC for Key Vault?

A) Access policies support Conditional Access while RBAC does not
B) Access policies grant object-level permissions (keys/secrets/certificates) at the whole-vault scope; RBAC provides fine-grained, resource/RG/subscription-scoped role assignments integrated with Azure AD
C) RBAC is a legacy model being replaced by access policies
D) Access policies can be scoped to an individual secret while RBAC cannot be scoped below the vault

<details>
<summary>Answer</summary>

**Correct: B**

Access policies apply uniformly across the entire vault per object type, with no finer scoping, whereas RBAC leverages Azure AD's hierarchical scope model (management group down to individual resource) for granular, auditable access.

**Why the others are wrong:**
- Conditional Access is unrelated to either permission model; it governs identity sign-in, not data-plane authorization
- RBAC is the newer, Microsoft-recommended model — access policies are the legacy mechanism
- Access policies cannot scope to individual objects; RBAC can, via custom role definitions with data actions

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

