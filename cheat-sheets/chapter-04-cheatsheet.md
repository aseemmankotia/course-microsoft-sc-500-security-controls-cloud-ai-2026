# Chapter 4 Cheat Sheet: Securing Azure SQL and Databases

## Authentication Modes
| Mode | MFA/CA Support | Notes |
|---|---|---|
| SQL Authentication | No | Username/password stored in DB; disable when compliance requires MFA |
| Microsoft Entra ID Auth | Yes | Supports MFA, Conditional Access, RBAC |
| Entra-only Enforcement | Yes | Setting: 'Support only Azure AD authentication for this server' — disables ALL SQL logins incl. sa, server-level only |

## TDE Key Management
| Type | Managed By | Revocation Control | Key Vault Requirement |
|---|---|---|---|
| Service-managed (default) | Microsoft | No | None |
| Customer-managed (BYOK) | Customer | Yes | Soft-delete + purge protection MUST be enabled; RSA 2048/3072/4096-bit key |

## Always Encrypted
| Encryption Type | Supports Equality/Joins | Security Level |
|---|---|---|
| Deterministic | Yes | Lower (patterns guessable) |
| Randomized | No | Higher |

Key hierarchy: **CMK** (client-side store: Key Vault/cert store) encrypts **CEK** (encrypts actual column data, stored in DB metadata). Requires Always Encrypted-enabled driver.

## Dynamic Data Masking Functions
| Function | Behavior |
|---|---|
| Default | Full mask by data type (XXXX for strings, 0 for numeric, 1900-01-01 for dates) |
| Email | aXX@XXXX.com format |
| Custom String | Reveals defined prefix/suffix chars, pads middle |
| Random | Random number in a defined range (numeric only) |

Bypass: `db_owner` role or users granted `UNMASK` permission. DDM does NOT encrypt — display-layer only.

## Auditing & Microsoft Defender for SQL
- **Auditing destinations:** Storage account, Log Analytics, Event Hub (multiple allowed)
- **Defender for SQL:** Vulnerability Assessment (config scans) + Advanced Threat Protection (SQL injection, brute force, anomalous access alerts)
- Alerts surface in Microsoft Defender for Cloud

## Data Classification
- Powered by **SQL Information Protection**, integrated with **Microsoft Purview** sensitivity labels
- Auto-recommends labels based on column name/data pattern (e.g., SSN, credit card → Confidential/Highly Confidential)

## Network Access
| Method | Public IP Exposure | Use Case |
|---|---|---|
| Firewall rule (IP allow-list) | Yes | Simple, limited scenarios |
| Allow Azure services | Yes (any Azure tenant) | Avoid for strict compliance |
| VNet Service Endpoint | Yes (still public IP) | Restrict traffic source, server still has public IP |
| Private Endpoint + Public Access Disabled | No | Zero internet exposure, private IP from VNet, works with ExpressRoute/VPN |

## Exam Traps
- Confusing TDE (at rest) with Always Encrypted (in use/column-level) or TLS (in transit)
- Forgetting purge protection requirement for TDE CMK
- Assuming DDM prevents privileged users (db_owner) from seeing real data — it does not
- Choosing deterministic encryption for high-security columns that never need joins/searches (should use randomized)
