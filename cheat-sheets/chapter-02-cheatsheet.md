## Chapter 2 Cheat Sheet — PIM, Managed Identities & RBAC

### PIM: Eligible vs Active
| Assignment Type | Access State | Requires Activation? |
|---|---|---|
| Eligible | Not active until activated | Yes — MFA, justification, approval (optional), time-bound |
| Active | Active immediately | No |

- Max activation duration: **1–24 hours** (default 8 hours), configurable per role.
- Activation settings configurable independently: MFA, justification, ticket number, approver.

### Managed Identities
| Type | Lifecycle | Reusable? | Use Case |
|---|---|---|---|
| System-assigned | Tied 1:1 to resource; deleted with resource | No | Single resource, simple auth |
| User-assigned | Standalone Azure resource | Yes, many:1 | Shared identity across multiple resources |

- Both eliminate need for stored secrets/credentials.
- Managed identity ≠ Service Principal with secret — no rotation needed.

### Service Principal vs App Registration
- **App registration**: global app definition in home tenant.
- **Service principal**: local identity instance used to grant access in a given tenant (one per tenant the app is used in).

### Azure RBAC Scope Hierarchy
```
Management Group > Subscription > Resource Group > Resource
```
- Permissions inherit downward.
- Assign at highest common scope to reduce assignment sprawl.

### Entra ID Roles vs Azure RBAC
| | Entra ID Roles | Azure RBAC |
|---|---|---|
| Controls | Directory objects (users, groups, app registrations, licenses) | Azure resources (VMs, storage, networking) |
| Example role | Password Administrator, Global Administrator | Owner, Contributor, Reader |
| Separate systems? | Yes — no automatic overlap | Yes |

### Azure Policy
| Component | Purpose |
|---|---|
| Definition | Single rule (e.g., allowed locations) |
| Initiative | Grouped set of definitions for a compliance goal |
| Assignment | Applies definition/initiative to a scope |

**Effects:**
| Effect | Behavior |
|---|---|
| Deny | Blocks non-compliant resource creation |
| Audit | Logs non-compliance, allows creation |
| Append | Adds fields/tags during creation, doesn't block |
| DeployIfNotExists | Deploys a related resource if missing |

### Management Groups
- Max hierarchy depth: **6 levels** (not counting root or subscription level).
- Used to apply Policy/RBAC inheritance across many subscriptions at once.

### Exam Traps
- Global Administrator (Entra ID role) does **not** grant Azure resource access automatically — must also assign Azure RBAC.
- System-assigned identity cannot be shared — pick user-assigned for shared workloads.
- Active PIM assignment with an expiration date is still standing access until expiry — not the same as requiring activation each use.
- Append vs DeployIfNotExists: Append modifies the same resource being created; DeployIfNotExists deploys a *separate* related resource.
