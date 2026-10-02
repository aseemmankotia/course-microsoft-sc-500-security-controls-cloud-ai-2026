## Defender for Cloud — Secure Score & Workload Protection

### Secure Score Formula
`Recommendation contribution = Max points × (Healthy resources ÷ Total applicable resources)`
Overall score = Sum(current points across all controls) ÷ Sum(max points) × 100

### Defender Plans (per-resource-type)
| Plan | Protects | Notes |
|---|---|---|
| Servers (P1) | VMs/on-prem via Arc | MDE integration only |
| Servers (P2) | VMs/on-prem via Arc | + vuln assessment, adaptive app control, FIM, adaptive network hardening |
| Storage | Blob/Files/ADLS | Malware scanning, anomalous access alerts |
| Databases | Azure SQL, SQL on VM/Arc, other DB engines | SQL injection, anomalous access |
| Containers | AKS, ACR, multicloud K8s | Runtime + image scanning + config recs |
| Key Vault | Vaults | Anomalous secrets/keys access |
| App Service | Web/API/Function apps | Web shell, suspicious outbound calls |

### CSPM Tiers
| Tier | Cost | Includes |
|---|---|---|
| Foundational CSPM | Free | Secure score, basic recommendations, all connected resources |
| Defender CSPM | Paid | Agentless scanning, Attack Path Analysis, Cloud Security Explorer, sensitive data discovery, Cloud Security Graph |

### Regulatory Compliance Dashboard
- Default standard: Microsoft cloud security benchmark (MCSB)
- Add manually: ISO 27001, PCI DSS, SOC 2, NIST SP 800-53, CIS Azure Foundations Benchmark, etc.
- Maps controls → recommendations → pass/fail status per standard

### Multicloud Connectors
| Cloud | Onboarding | Plans available |
|---|---|---|
| AWS | Native connector → CloudFormation template (IAM roles) | Servers, Containers, Databases (RDS), Defender CSPM |
| GCP | Native connector → Cloud Shell/Terraform script | Servers, Containers, Defender CSPM |

Exam trap: You cannot enable a workload plan from inside AWS/GCP consoles — always via the Azure-side connector.

### Governance Rules vs Workflow Automation
| Feature | Governance Rules | Workflow Automation |
|---|---|---|
| Purpose | Assign owner + due date to recommendations | Trigger Logic App on new alert/recommendation |
| Notifies | Email reminders/escalation | Any downstream automation (ticket, Teams, SIEM) |
| Scope | Recommendation ownership/accountability | Event-driven response |

### Attack Path Analysis / Cloud Security Graph
- Requires **Defender CSPM** plan
- Uses graph of resources + exposures + network reachability to compute exploitable paths
- Cloud Security Explorer = query builder over the same graph

### Exemptions vs Disabling a Plan
- **Exemption**: scoped to resource/RG, requires justification, removes resource from applicable count (protects score)
- **Disabling a plan**: removes ALL its recommendations/protections — avoid unless plan is truly not needed

### Common Exam Traps
1. Assuming secure score is per-recommendation pass/fail (it's proportional to healthy resource ratio)
2. Trying to enable Defender plans from within AWS/GCP consoles instead of the connector
3. Confusing Governance Rules (ownership/due dates) with Workflow Automation (event-triggered Logic Apps)
4. Assuming Attack Path Analysis works with Foundational (free) CSPM — it requires the paid Defender CSPM plan
