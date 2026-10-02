# Chapter 5 Cheat Sheet: Network Perimeter Controls

## NSG Rule Evaluation
| Item | Value |
|---|---|
| Custom rule priority range | 100–4096 (lower = higher priority) |
| Default rule priorities (inbound) | AllowVNetInBound=65000, AllowAzureLB=65001, DenyAllInBound=65500 |
| Evaluation logic | First matching rule wins; processing stops |
| Default max rules/NSG | 1000 (raisable to 4096 via support) |
| Association scope | Subnet or NIC |

**ASGs**: Group VM NICs by role (e.g., WebTier/DBTier) for use as NSG rule source/destination — scales automatically, no IP maintenance.

## Azure Firewall SKUs
| SKU | Throughput | Key Features |
|---|---|---|
| Basic | ~250 Mbps | SMB/branch, DNS proxy, basic threat intel (alert) |
| Standard | Up to 30 Gbps | FQDN filtering, Threat Intel (Alert/Deny), NAT, app+network rules |
| Premium | Up to 100 Gbps | + TLS inspection, IDPS, URL filtering, web categories |

**Threat Intelligence modes**: Off / Alert only / Alert and Deny.

## NSG vs Azure Firewall vs WAF
| Control | Layer | Scope | Best For |
|---|---|---|---|
| NSG | L3/L4 (5-tuple) | Subnet/NIC | Simple allow/deny between tiers/subnets |
| Azure Firewall | L3-L7 | VNet/Hub | Centralized egress control, FQDN filtering, threat intel |
| WAF (App Gateway) | L7 (HTTP/S) | Regional | OWASP protection for regional web apps |
| WAF (Front Door) | L7 (HTTP/S) | Global edge | OWASP protection with low global latency |

## WAF Modes & Rule Sets
- **Detection**: logs matches only, no blocking — use for tuning.
- **Prevention**: blocks + logs matches — production default.
- App Gateway: OWASP CRS (latest 3.2).
- Front Door: Default Rule Set (DRS, latest 2.1) + Bot Manager Rule Set.

## DDoS Protection Tiers
| Tier | Cost | Cost Protection SLA | Rapid Response Team |
|---|---|---|---|
| Basic | Free (automatic) | No | No |
| Network Protection | Fixed monthly (VNet-scoped) | Yes | Yes |
| IP Protection | Pay-per-IP | No | No |

## Hub-Spoke Pattern
Hub VNet = shared services (Azure Firewall, VPN/ExpressRoute Gateway). Spokes peer to hub; all inter-spoke and outbound traffic routes through hub for centralized inspection/logging.

## Exam Traps
- Assuming NSGs support FQDN filtering (they don't — that's Firewall/WAF).
- Confusing Alert-only vs Alert-and-Deny threat intel modes.
- Picking Premium Firewall when Standard already satisfies FQDN filtering requirement.
- Forgetting DDoS Basic has no SLA/cost protection — Network Protection required for that.
- Believing NSG evaluates ALL matching rules instead of stopping at first match.
