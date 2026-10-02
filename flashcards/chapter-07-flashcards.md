## Chapter 7: Securing Virtual Machines and Disk Encryption — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | ADE vs Encryption at Host: can both be enabled on the same disk? | No — mutually exclusive. Enabling one where the other is active causes an error. Exam tip: pick ONE encryption strategy per disk. |
| 2 | Which encryption method covers the temp disk and host caches, not just the persistent disk? | Encryption at Host. SSE and ADE do not encrypt temp disk/caches by default. Exam tip: 'temp disk' + 'cache' in a question = Encryption at Host. |
| 3 | Does Azure Disk Encryption (ADE) require Azure Key Vault? | Yes — ADE always requires a Key Vault to store BitLocker (Windows) / DM-Crypt (Linux) keys/secrets. |
| 4 | Does Encryption at Host require Azure Key Vault? | Only if using customer-managed keys via a Disk Encryption Set. With platform-managed keys (default), no Key Vault is required. |
| 5 | JIT VM access — default maximum access request time? | 3 hours (default max request window). Exam tip: JIT opens NSG rules temporarily, then reverts to deny. |
| 6 | JIT VM access default monitored ports | 22 (SSH), 3389 (RDP), 5985/5986 (WinRM). Exam tip: these are the ports Defender for Cloud flags as 'exposed' by default. |
| 7 | Which Defender for Servers plan is required for JIT VM access? | Defender for Servers Plan 2. Plan 1 only gives Defender for Endpoint integration + vulnerability assessment. |
| 8 | CLI command to register the Encryption at Host feature on a subscription | az feature register --namespace Microsoft.Compute --name EncryptionAtHost Exam tip: one-time subscription opt-in; VM size must also support it. |
| 9 | System-assigned vs user-assigned managed identity lifecycle | System-assigned: tied 1:1 to the VM, deleted with the VM. User-assigned: independent lifecycle, can be reused across multiple VMs. |
| 10 | Azure Update Manager patch compliance states | Compliant, Non-Compliant, Unknown, Not Applicable. Exam tip: 'Unknown' means assessment hasn't run yet, not that the machine is unpatched. |
| 11 | What replaced Azure Update Management Center as the current patch orchestration service? | Azure Update Manager — supports Azure VMs, on-prem, and Azure Arc-enabled servers with maintenance configurations and scheduled patching. |
| 12 | Which Windows edition supports hotpatching via Azure Update Manager (fewer reboots)? | Windows Server 2022 Datacenter: Azure Edition. Exam tip: hotpatch applies security updates without a full reboot cycle. |
