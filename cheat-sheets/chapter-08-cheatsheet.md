# Chapter 8 Cheat Sheet — Securing Containers & AKS

## Network Policy Engines
| Feature | Azure NPM | Calico |
|---|---|---|
| Linux node support | ✅ | ✅ |
| Windows node support | ❌ | ✅ |
| Standard k8s NetworkPolicy objects | ✅ | ✅ |
| Extended policies (GlobalNetworkPolicy) | ❌ | ✅ |
| Changeable after cluster creation | ❌ (requires new cluster) | ❌ (requires new cluster) |

Create: `az aks create --network-plugin azure --network-policy [azure|calico]`

## Microsoft Defender for Containers
- Scans ACR images via Microsoft Defender Vulnerability Management engine.
- Rescans images as new CVEs are disclosed (continuous reassessment).
- Runtime protection via DaemonSet-deployed sensor + Azure Policy add-on (Gatekeeper) for data-plane hardening.
- Requires the **Defender for Containers plan** enabled at subscription level — ACR access alone is not enough.

## Workload Identity vs Pod Identity
| | AAD Pod Identity | Microsoft Entra Workload Identity |
|---|---|---|
| Status | Deprecated/retired | Current, supported |
| Auth mechanism | NMI intercepts IMDS calls | OIDC federation, projected SA token exchange |
| Secrets stored in cluster | No (but complex, extra components) | No |
| Enable | N/A | `--enable-oidc-issuer --enable-workload-identity` |

SA annotation required: `azure.workload.identity/client-id: <app-client-id>`

## AKS Private Cluster vs Authorized IP Ranges
| | Private Cluster | Authorized IP Ranges |
|---|---|---|
| Public IP on API server | None | Yes, filtered by source IP |
| Access requirement | VNet peering/VPN/ExpressRoute/jumpbox | Any listed public IP |
| Enable | `--enable-private-cluster` | `--api-server-authorized-ip-ranges <cidrs>` |

## Pod Security Standards (PSA)
- Profiles: **Privileged → Baseline → Restricted**
- Enforced via namespace labels, e.g.: `pod-security.kubernetes.io/enforce: restricted`
- PSP removed in Kubernetes **v1.25** — PSA is the built-in replacement.
- Custom/org-specific policy → use **Azure Policy Add-on for AKS** (Gatekeeper/OPA), not PSA.

## Secrets Management — Key Vault CSI Driver
- Mounts secrets as files via `SecretProviderClass`.
- `secretObjects` block syncs mounted values into native Kubernetes Secrets.
- Rotation: `--enable-secret-rotation`, default poll interval **2 minutes**.
- Prefer Workload Identity for the driver's Key Vault access (no static credentials).

## Exam Traps
- Choosing Azure NPM for a mixed Linux/Windows cluster (only Calico supports Windows).
- Assuming authorized IP ranges removes the public IP entirely — it does not; only private cluster does.
- Recommending AAD Pod Identity in 2026 scenarios — it's retired; answer is Workload Identity.
- Believing CSI driver mount automatically creates a Kubernetes Secret — it doesn't without `secretObjects`.
