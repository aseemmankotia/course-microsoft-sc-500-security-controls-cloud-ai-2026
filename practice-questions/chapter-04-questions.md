## Chapter 4: Securing Azure SQL and Databases — Practice Questions

**Q1.** A financial company requires full control over Azure SQL Database TDE encryption keys, including the ability to revoke a key to instantly render the database inaccessible for compliance reasons. Which configuration BEST meets this requirement?

A) Enable TDE with service-managed keys (default)
B) Enable Always Encrypted with randomized encryption
C) Enable TDE with a customer-managed key (BYOK) stored in Azure Key Vault
D) Enable Dynamic Data Masking on all sensitive columns

<details>
<summary>Answer</summary>

**Correct: C**

Customer-managed keys (BYOK) in Key Vault give the customer control of the key lifecycle, including revocation/disabling the key to make the database inaccessible.

**Why the others are wrong:**
- Service-managed keys are fully controlled and rotated by Microsoft — no customer revocation capability.
- Always Encrypted protects specific columns from server-side visibility, it does not control database-wide accessibility via key revocation.
- Dynamic Data Masking only obscures query results for non-privileged users; it does not encrypt data or control access at the key level.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A support team must be able to run troubleshooting queries against a customer database, but full credit card numbers must not appear in their query results. The underlying data must remain unchanged. Which feature should be implemented?

A) Always Encrypted with deterministic encryption
B) Transparent Data Encryption with customer-managed key
C) Dynamic Data Masking
D) Row-Level Security

<details>
<summary>Answer</summary>

**Correct: C**

Dynamic Data Masking obfuscates sensitive data in the result set for non-privileged users without altering the data stored on disk, requiring minimal application changes.

**Why the others are wrong:**
- Always Encrypted requires client-driver changes and would prevent the support team from querying the plaintext at all, breaking troubleshooting workflows.
- TDE with CMK protects data at rest and does not mask values in query results.
- Row-Level Security controls which rows a user can see, not which column values are masked.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A database column storing Social Security Numbers must remain encrypted from view of DBAs with sysadmin rights, but the application performs only equality lookups (WHERE SSN = @value) on that column. Which Always Encrypted configuration should be used?

A) Deterministic encryption
B) Randomized encryption
C) Service-managed TDE
D) Dynamic Data Masking

<details>
<summary>Answer</summary>

**Correct: A**

Deterministic encryption always produces the same ciphertext for the same plaintext, enabling equality comparisons, joins, and indexing on the encrypted column.

**Why the others are wrong:**
- Randomized encryption is more secure but does not support equality searches or joins, breaking the lookup query.
- Service-managed TDE does not hide data from sysadmins — it only protects data at rest from storage-level theft.
- Dynamic Data Masking does not prevent sysadmins from seeing plaintext; it is bypassed by privileged roles.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** An organization must ensure Azure SQL Database is reachable from an on-premises network over ExpressRoute but must have zero exposure to the public internet. Which solution should be implemented?

A) Private endpoint with public network access disabled
B) Server firewall rule to allow Azure services
C) Virtual network service endpoint only
D) Dynamic Data Masking on all columns

<details>
<summary>Answer</summary>

**Correct: A**

A private endpoint assigns a private IP from the customer's VNet to the SQL server, and disabling public network access removes any internet-facing endpoint entirely.

**Why the others are wrong:**
- Allowing Azure services opens access to any Azure tenant's resources over a public IP path, not zero exposure.
- Service endpoints restrict traffic to a VNet but the SQL server still has a public IP and is technically internet-facing.
- Dynamic Data Masking is unrelated to network connectivity.

</details>

---

**Q5.** A compliance policy requires that Azure SQL Server reject all SQL authentication attempts, including the sa account, and accept only Microsoft Entra ID credentials. Which setting achieves this?

A) Configure a Microsoft Entra admin for the server
B) Configure Dynamic Data Masking with UNMASK denied
C) Enable row-level security for all logins
D) Enable 'Support only Azure Active Directory authentication for this server'

<details>
<summary>Answer</summary>

**Correct: D**

This server-level setting fully disables all SQL authentication logins, including sa, allowing only Microsoft Entra ID authentication.

**Why the others are wrong:**
- Configuring a Microsoft Entra admin enables Entra auth alongside SQL auth — it does not disable SQL logins.
- Dynamic Data Masking has no relationship to authentication method enforcement.
- Row-level security controls row visibility per user, not the authentication mechanism.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** Which prerequisite MUST be configured on the Azure Key Vault before it can be used for TDE customer-managed key encryption?

A) Soft-delete and purge protection must both be enabled
B) RBAC access control must be disabled
C) The vault must reside in a different region than the SQL server
D) The key must be a symmetric AES-256 key

<details>
<summary>Answer</summary>

**Correct: A**

Azure requires soft-delete and purge protection enabled on the Key Vault before it can be used for TDE CMK, ensuring the key cannot be permanently deleted while in use.

**Why the others are wrong:**
- RBAC can be enabled or disabled independently — it is not a hard requirement for TDE CMK.
- Region co-location is not mandatory, though same-region is a best practice for latency, not a requirement.
- TDE CMK requires an RSA key (2048, 3072, or 4096-bit), not a symmetric key.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Which Dynamic Data Masking function replaces a numeric column's value with a random number within a defined minimum and maximum range?

A) Random masking function
B) Default masking function
C) Email masking function
D) Custom string masking function

<details>
<summary>Answer</summary>

**Correct: A**

The Random masking function is specifically designed for numeric data types and substitutes a random value within a configurable range.

**Why the others are wrong:**
- The Default masking function replaces numeric values with 0, not a random range.
- Email masking is designed for email-formatted string columns (e.g., aXX@XXXX.com).
- Custom String masking exposes a defined number of characters at the start/end with a padding character, used for strings, not numeric ranges.

</details>

---

**Q8.** What is the primary difference between Microsoft Defender for SQL and SQL auditing?

A) Defender for SQL provides threat detection and vulnerability assessment alerts, while auditing logs database events for compliance and forensic review
B) Auditing detects SQL injection attacks, while Defender for SQL only stores logs in Log Analytics
C) They are functionally identical and can be used interchangeably
D) Auditing only works when TDE is configured with a customer-managed key

<details>
<summary>Answer</summary>

**Correct: A**

Microsoft Defender for SQL performs active threat detection (SQL injection, brute force, anomalous access) and vulnerability scanning, while auditing captures a log trail of database events for compliance.

**Why the others are wrong:**
- This reverses the actual capabilities — SQL injection detection is a Defender for SQL feature, not auditing.
- They serve distinct, complementary purposes and are not interchangeable.
- Auditing has no dependency on TDE key management type.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

