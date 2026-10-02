## Chapter 4: Securing Azure SQL and Databases — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Setting name to enforce Entra-only authentication on Azure SQL Server? | 'Support only Azure Active Directory authentication for this server' — server-level setting, disables all SQL logins including sa. Exam tip: cannot be undone without re-enabling SQL auth explicitly. |
| 2 | TDE customer-managed key: Key Vault prerequisites? | Soft-delete AND purge protection must both be enabled. Exam tip: setup fails without purge protection — this is a favorite exam trap. |
| 3 | Always Encrypted: Deterministic vs Randomized — which supports equality joins/searches? | Deterministic supports equality comparisons, joins, and grouping. Randomized is more secure but blocks all comparisons. Exam tip: pick deterministic for indexed/searchable columns. |
| 4 | Always Encrypted key hierarchy — two key types? | Column Master Key (CMK): stored client-side (Key Vault, cert store). Column Encryption Key (CEK): encrypts the data, itself encrypted by the CMK and stored in DB metadata. |
| 5 | Who can bypass Dynamic Data Masking and see unmasked values? | db_owner role members and users explicitly granted UNMASK permission. Exam tip: DDM is a display control, not real encryption/security. |
| 6 | Dynamic Data Masking — the 4 masking function types? | Default (full mask by data type), Email (aXX@XXXX.com), Custom String (partial reveal with padding), Random (numeric range). Exam tip: Random only applies to numeric types. |
| 7 | Does TDE protect data in transit or in use? | No — TDE only protects data at rest. Use TLS for in-transit, Always Encrypted for in-use/column-level protection. Exam tip: exam scenario keywords 'at rest' vs 'in use' point to different features. |
| 8 | Private endpoint vs Service endpoint for Azure SQL — key difference? | Private endpoint assigns a private IP from your VNet to the SQL server and can disable public access entirely. Service endpoint keeps the server's public IP but restricts traffic via VNet rule. Exam tip: private endpoint when public access must be fully removed. |
| 9 | Microsoft Defender for SQL — two main capabilities? | Vulnerability Assessment (scans for misconfigurations) + Advanced Threat Protection (detects SQL injection, brute force, anomalous access). Exam tip: alerts surface in Microsoft Defender for Cloud. |
| 10 | SQL Auditing — supported log destinations? | Storage account, Log Analytics workspace, Event Hub. Exam tip: multiple destinations can be selected simultaneously. |
| 11 | Where do Azure SQL sensitivity labels/data classification come from? | SQL Information Protection, integrated with Microsoft Purview sensitivity labels (e.g., Confidential, Highly Confidential). Exam tip: recommendations auto-generate based on column names/data patterns like SSN or credit card. |
| 12 | Entra ID auth vs SQL auth — which supports MFA and Conditional Access? | Only Microsoft Entra ID authentication. SQL authentication (username/password) has no MFA or Conditional Access support. Exam tip: compliance scenarios requiring MFA point to Entra-only enforcement. |
