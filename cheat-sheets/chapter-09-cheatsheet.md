# Chapter 9 Cheat Sheet — App Service, Serverless & Key Vault

## Permission Model: Access Policies vs RBAC
| Feature | Access Policy | Azure RBAC |
|---|---|---|
| Scope | Whole vault only | Resource / RG / Subscription / Mgmt Group |
| Governance | Manual only | Azure Policy, PIM, Activity Log audit |
| Granularity | Object type (keys/secrets/certs) | Data-action level via built-in/custom roles |
| Toggle | `enableRbacAuthorization=false` | `enableRbacAuthorization=true` |
| Coexistence | Vault uses ONE model at a time | Same |

## Soft-Delete & Purge Protection
| Setting | Behavior |
|---|---|
| Soft-delete | Mandatory, 7–90 days retention (default 90), cannot disable |
| Purge protection | Optional but recommended; once ON cannot be turned OFF; blocks purge for ALL roles during retention |
| Recovery | `az keyvault secret recover` (or key/cert) during retention window |

## Key Vault Reference Syntax (App Service)
```
@Microsoft.KeyVault(SecretUri=https://vault.vault.azure.net/secrets/name/version)   -- pinned version
@Microsoft.KeyVault(VaultName=vault;SecretName=name)                                -- always latest
```
Requires: Managed Identity + `Key Vault Secrets User` role (RBAC) or Get/List (access policy).

## Built-in RBAC Roles (Key Vault Data Plane)
| Role | Capability |
|---|---|
| Key Vault Administrator | Full data-plane control |
| Key Vault Secrets Officer | Manage secrets (set/delete) |
| Key Vault Secrets User | Read secret values only |
| Key Vault Reader | Read metadata, NOT values |

## Key/Certificate Rotation
- **Keys**: rotation policy with `expiryTime` + `notifyTime`; action type `Rotate` auto-generates new version at expiry; `Notify` fires Event Grid event only.
- **Secrets**: no native rotation — build via Event Grid + Azure Function/Automation.
- **Certificates**: auto-renew only with integrated CA issuer (e.g., DigiCert/GlobalSign); self-signed = manual.

## Network Restrictions
| Goal | Config |
|---|---|
| VNet-only access | Private Endpoint + Public network access = Disabled |
| Allow trusted MS services (Backup, etc.) | Firewall: "Allow trusted Microsoft services to bypass" = Yes |
| IP allowlist without private endpoint | Firewall rule with specific IP ranges (still has public endpoint) |

## App Service / Functions Identity Patterns
- **Easy Auth**: platform-level auth sidecar, zero code, supports Azure AD/social IdPs, token store, `/.auth/login/<provider>`.
- **Managed Identity → Key Vault**: assign RBAC/access-policy permission to the identity, not the app registration.
- **Functions identity-based bindings**: replace connection strings with Managed Identity + RBAC role (e.g., Storage Blob Data Owner) using `__serviceUri` + `Credential=ManagedIdentity` settings.

## Common Exam Traps
- Purge protection cannot be disabled once enabled — permanent commitment.
- Pinned SecretUri version ≠ auto-updating reference (must omit version for latest).
- Access policies and RBAC cannot both govern the same vault simultaneously.
- Native key rotation ≠ native secret rotation (secrets need custom automation).
- Trusted-services firewall bypass is independent of private endpoint deployment.
