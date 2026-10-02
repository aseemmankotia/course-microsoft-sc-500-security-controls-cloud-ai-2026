## Chapter 3: Securing Azure Storage Accounts — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Max lifetime of a user delegation key (used for User Delegation SAS)? | 7 days (168 hours). Exam tip: if the key expiry requested exceeds 7 days, Azure caps it automatically. |
| 2 | Which storage services support User Delegation SAS? | Blob only (block, page, append blobs and containers). NOT supported for File, Queue, or Table. Common exam trap. |
| 3 | Setting to fully disable Shared Key authorization on a storage account? | 'Allow storage account key access' → Disabled. Forces all data-plane requests to use Microsoft Entra ID RBAC. |
| 4 | Order of evaluation: storage firewall network rules vs RBAC authorization? | Network rules are evaluated FIRST. A request blocked by the firewall never reaches the auth check, even with correct RBAC roles assigned. |
| 5 | Service Endpoint vs Private Endpoint — key difference? | Service Endpoint: routes VNet traffic over Azure backbone to storage's PUBLIC IP, free, no on-prem access. Private Endpoint: assigns a PRIVATE IP in the VNet via Private Link, supports on-prem access (VPN/ExpressRoute), billed per hour + per GB. |
| 6 | Private DNS zone names required for storage private endpoints? | privatelink.blob.core.windows.net, privatelink.file.core.windows.net, privatelink.queue.core.windows.net, privatelink.table.core.windows.net — one zone per sub-resource, each needing its own private endpoint. |
| 7 | Default encryption at rest for a new Azure Storage account? | Storage Service Encryption (SSE) with Microsoft-managed keys, AES-256, enabled automatically — no configuration needed. |
| 8 | Prerequisites on Key Vault before enabling Customer-Managed Keys (CMK) for storage? | Soft delete AND purge protection must both be enabled on the Key Vault, plus the storage account needs a managed identity with key access (Key Vault Crypto Service Encryption User role or access policy). |
| 9 | Default retention range for blob soft delete? | Configurable from 1 to 365 days. Exam tests recognizing this is a RANGE, not a fixed value — default when enabled via portal is often 7 days. |
| 10 | Locked immutability (time-based retention) policy — what can you change? | You can only EXTEND the retention period (up to 5 times) once locked; you can never shorten it or delete the data early. Max retention ~146,000 days (~400 years). |
| 11 | CLI command to rotate (renew) a storage account access key? | az storage account keys renew --account-name <name> --resource-group <rg> --key key1 (or key2). Rotate one key at a time to avoid downtime for apps still using the other key. |
| 12 | Service SAS vs Account SAS vs User Delegation SAS — signing key? | Service SAS & Account SAS: signed with the storage ACCOUNT KEY. User Delegation SAS: signed with a user delegation key derived from Entra ID credentials — no account key involved, most secure option. |
