## Chapter 3 Cheat Sheet: Securing Azure Storage Accounts

### Authentication Methods
| Method | Signed With | Best For |
|---|---|---|
| Shared Key | Account key | Legacy/admin tools; disable in production |
| Microsoft Entra ID (RBAC) | Entra ID token | Preferred; roles: Storage Blob Data Reader/Contributor/Owner, Storage Queue Data Contributor, Storage Table Data Contributor |
| SAS (Service/Account) | Account key | Time-boxed delegated access, still key-dependent |
| SAS (User Delegation) | Entra ID user delegation key | Most secure SAS; Blob only |

**Kill switch:** `Allow storage account key access = Disabled` → forces Entra ID only, invalidates Shared Key & key-signed SAS.

### SAS Types
| Type | Scope | Services | Signed By | Max Key Life |
|---|---|---|---|---|
| Service SAS | Single resource (container/blob/queue/table) | One service | Account key | N/A (set expiry in token) |
| Account SAS | Multiple services/operations | Blob, File, Queue, Table | Account key | N/A |
| User Delegation SAS | Container/blob | Blob only | User delegation key (Entra ID) | 7 days |

### Network Security
| Feature | Private IP? | On-Prem Access? | Cost |
|---|---|---|---|
| Firewall IP rules | No | Yes (by IP) | Free |
| VNet Service Endpoint | No | No | Free |
| Private Endpoint | Yes | Yes (VPN/ExpressRoute) | Hourly + per GB |

**Order of evaluation:** Network rules → then authentication/RBAC. A firewall Deny blocks requests before RBAC is even checked — classic exam trap.

Separate private endpoints required per sub-resource: blob, file, queue, table, web, dfs (each own privatelink DNS zone).

### Encryption at Rest
- Default: SSE, Microsoft-managed keys, AES-256 — always on, no config.
- CMK (Customer-Managed Keys): stored in Key Vault; **requires Key Vault soft delete + purge protection enabled**; storage account needs managed identity with key access.
- Infrastructure encryption: optional second encryption layer (must be set at account creation, cannot be added later).

### Data Protection
| Feature | Purpose | Can Admin Bypass? |
|---|---|---|
| Soft delete (blob/container/file) | Undo accidental delete, 1–365 days | Yes, can be disabled/purged |
| Versioning | Keep prior blob versions | Yes |
| Legal hold | Indefinite hold, manually removable | Yes, removable anytime |
| Locked immutability policy (WORM) | Fixed/extendable retention, true compliance | **No** — cannot shorten or delete early |

### Key Rotation
- Two keys (key1/key2) enable zero-downtime rotation.
- `az storage account keys renew --key key1`
- Automate via Key Vault + Event Grid/Automation for scheduled rotation.
- Best practice: eliminate keys entirely by disabling Shared Key access and using Entra ID + Managed Identities.

### Exam Traps
1. RBAC role assigned but access still fails → check network firewall rules first.
2. User Delegation SAS attempted on File/Queue/Table → unsupported, Blob only.
3. Soft delete assumed to be compliance-grade WORM → it isn't; use locked immutability policy instead.
