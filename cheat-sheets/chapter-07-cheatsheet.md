## Chapter 7 Cheat Sheet — Securing VMs & Disk Encryption

### Encryption Methods Comparison
| Method | Layer | Covers Temp Disk/Cache | Key Vault Required | Notes |
|---|---|---|---|---|
| SSE (Storage Service Encryption) | Storage layer, on by default | No | No (Yes only for CMK) | Platform- or customer-managed key, transparent |
| Azure Disk Encryption (ADE) | Guest OS (BitLocker/DM-Crypt) | No | Yes, always | Protects against offline disk theft; VM must be running to encrypt/decrypt |
| Encryption at Host | Azure host | Yes | Only for CMK via Disk Encryption Set | No guest OS impact; mutually exclusive with ADE on same disk |

**Rule of thumb:** Need temp disk/cache covered → Encryption at Host. Need in-guest BitLocker/DM-Crypt semantics tied to Key Vault → ADE. Default baseline → SSE (always on).

### Just-in-Time (JIT) VM Access
- Requires: **Defender for Servers Plan 2**
- Default monitored ports: **22, 3389, 5985, 5986**
- Default max request window: **3 hours**
- Mechanism: temporary NSG allow rule scoped to requester IP, auto-reverts after window expires
- Common trap: JIT does NOT replace NSGs permanently — it creates a temporary exception

### Defender for Servers Plan Comparison
| Feature | Plan 1 | Plan 2 |
|---|---|---|
| Defender for Endpoint integration | ✔ | ✔ |
| Vulnerability assessment | ✔ | ✔ |
| JIT VM access | ✘ | ✔ |
| Adaptive application controls | ✘ | ✔ |
| File integrity monitoring | ✘ | ✔ |
| Adaptive network hardening | ✘ | ✔ |

### Azure Update Manager
- Compliance states: **Compliant / Non-Compliant / Unknown / Not Applicable**
- Supports: Azure VMs, on-prem, Azure Arc-enabled servers
- Hotpatching: available on **Windows Server 2022 Azure Edition** — fewer reboots
- Uses maintenance configurations for scheduled patch windows

### Managed Identities
| Type | Lifecycle | Shareable across VMs |
|---|---|---|
| System-assigned | Tied to VM (deleted with VM) | No |
| User-assigned | Independent | Yes |

### Key CLI/Feature Commands
```bash
az feature register --namespace Microsoft.Compute --name EncryptionAtHost
az vm update --enable-encryption-at-host --name <vm> -g <rg>
az vm encryption enable --name <vm> -g <rg> --disk-encryption-keyvault <kv>
```

### Common Exam Traps
1. Assuming ADE and Encryption at Host can stack — they cannot on the same disk.
2. Confusing SSE (always-on, transparent) with ADE (guest-level, needs Key Vault).
3. Forgetting JIT requires Defender for Servers **Plan 2**, not Plan 1.
4. Thinking system-assigned identities can be reused across multiple VMs — only user-assigned can.
