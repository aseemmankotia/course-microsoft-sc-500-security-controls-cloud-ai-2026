## Chapter 11 Cheat Sheet: Sentinel & AI Workload Security

### Analytics Rule Types
| Rule Type | Frequency | Notes |
|---|---|---|
| Scheduled | Min 5 min, max 14-day lookback | Custom KQL, joins allowed |
| NRT | Every 1 min | Single table, no joins, lowest latency |
| Fusion | Continuous/ML | Multi-stage attack correlation, not customizable |
| Microsoft Security | Passthrough | Mirrors alerts from connected MS products |
| ML Behavior Analytics | Built-in ML | Anomaly detection (e.g., anomalous sign-in) |

### Automation Rules vs. Playbooks
| Feature | Automation Rule | Playbook |
|---|---|---|
| Purpose | Conditions + simple actions | Logic App workflow (remediation) |
| Triggered by | Incident/alert creation or update | Called by automation rule (or manually) |
| Actions | Assign owner, tag, close, run playbook | API calls, notifications, ticketing, containment |
| Order | Executes by priority (low # first) | N/A |
| Recommended trigger | — | Incident trigger (not legacy Alert trigger) |

### Investigation & Visualization
- **Entities**: accounts, hosts, IPs, files, URLs — link alerts into the investigation graph.
- **Incidents**: container for correlated alerts + entities + automation history.
- **Workbooks**: ARM-based, KQL-driven dashboards for custom visualization/trend analysis.

### AI Workload Security Mapping
| Concern | Service | Function |
|---|---|---|
| Prompt injection (direct/indirect/XPIA) | Azure AI Content Safety – Prompt Shields | Detect/block malicious prompts |
| Sensitive data oversharing via Copilot/AI | Microsoft Purview – DSPM for AI | Posture & exposure monitoring |
| Data labeling/DLP for AI-referenced content | Microsoft Purview – Sensitivity labels, DLP | Prevent exfiltration via AI responses |
| Shadow AI app discovery | Defender for Cloud Apps – Cloud Discovery | Identify unsanctioned GenAI app usage |
| Azure OpenAI resource threat alerts | Microsoft Defender for Cloud – AI threat protection | Jailbreak attempts, data leakage alerts |
| SIEM correlation of AI activity | Microsoft Sentinel (OpenAI/AI data connector) | Ingest AI logs into analytics rules/incidents |

### Exam Gotchas
- NRT ≠ Scheduled: NRT is 1-minute/no-join; scheduled min is 5 minutes.
- Alert trigger (legacy) vs Incident trigger (current best practice) — exam favors Incident trigger.
- Prompt Shields ≠ DSPM for AI: one blocks malicious prompts, the other monitors sensitive-data exposure posture.
- Fusion rules cannot be freely customized like scheduled rules — common wrong-answer trap.
- Workbooks visualize; Automation rules act — don't confuse the two on scenario questions.
