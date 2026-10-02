## Chapter 11: Microsoft Sentinel & Securing AI Workloads — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | NRT (Near-Real-Time) analytics rule run frequency in Sentinel? | Every 1 minute, against a single table with no joins. Exam tip: choose NRT when sub-minute detection is required. |
| 2 | Scheduled analytics rule: minimum frequency and maximum lookback period? | Minimum frequency 5 minutes; maximum lookback 14 days. Exam tip: distinguishes scheduled from NRT (1-min) rules. |
| 3 | Automation rule vs. Playbook — what's the difference? | Automation rule = conditions + simple actions (assign owner, tag, run playbook, close incident), centrally ordered by priority. Playbook = the actual Logic App workflow performing remediation steps. |
| 4 | Which Logic Apps trigger is recommended for Sentinel playbooks today: Alert trigger or Incident trigger? | Incident trigger — exposes full incident context (all correlated alerts/entities). Alert trigger is legacy. |
| 5 | What does a Fusion rule detect? | Multi-stage attacks by correlating multiple low-fidelity alerts/anomalies across the kill chain using ML — not customizable like scheduled rules. |
| 6 | What are 'entities' in Sentinel used for? | Standardized objects (account, host, IP, file, URL, etc.) that Sentinel correlates across alerts to build the investigation graph. |
| 7 | What is Azure AI Content Safety Prompt Shields used for? | Detects and blocks prompt injection — both direct (user input) and indirect (embedded in documents/content, aka XPIA) — before/during LLM inference. |
| 8 | What does Microsoft Purview DSPM for AI monitor? | Sensitive-data oversharing and exposure risk in Copilot/AI app interactions — flags when users interact with unlabeled or sensitive content via AI. |
| 9 | Which service discovers 'shadow AI' apps used without sanction by employees? | Microsoft Defender for Cloud Apps — Cloud Discovery catalogs and risk-scores generative AI app usage from network/proxy logs. |
| 10 | What are Sentinel Workbooks built on? | Azure Monitor Workbooks — ARM-template based, KQL-driven interactive visualizations/dashboards. |
| 11 | How does automation rule execution order work when multiple rules match an incident? | Automation rules execute in the order of their configured priority (lower number = runs first). Exam tip: order matters when multiple rules could fire on the same incident. |
| 12 | What does Defender for Cloud's AI threat protection alert on for Azure OpenAI workloads? | Jailbreak/prompt-injection attempts and sensitive-data leakage detected in Azure OpenAI resource activity, surfaced as security alerts/incidents. |
