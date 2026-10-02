## Chapter 6: Private Connectivity & Network Segmentation — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Private DNS zone name for Azure Blob Storage private endpoints? | privatelink.blob.core.windows.net. Exam tip: must be linked to the VNet for the public FQDN to resolve to the private IP. |
| 2 | Private DNS zone name for Azure SQL Database private endpoints? | privatelink.database.windows.net. Exam tip: same pattern applies to other SQL family services with their own privatelink zone. |
| 3 | Private DNS zone name for Azure Key Vault private endpoints? | privatelink.vaultcore.azure.net — NOT privatelink.vault.azure.net. Public FQDN stays vault.azure.net; only the private-link zone changes to vaultcore. |
| 4 | Service Endpoint vs Private Endpoint: which reaches PaaS from on-premises over VPN/ExpressRoute? | Private Endpoint (has a private IP reachable via any VNet-connected path). Service Endpoints generally do NOT support on-prem access without extra NAT/public-IP configuration. |
| 5 | Service Endpoint vs Private Endpoint: which assigns a private IP to the PaaS resource? | Private Endpoint — creates a NIC with a private IP in your subnet. Service Endpoint keeps the resource's public IP and only restricts/optimizes access from selected subnets. |
| 6 | Is VNet peering transitive by default? | No. Peering is non-transitive — Spoke A peered to Hub and Spoke B peered to Hub does NOT let Spoke A talk to Spoke B automatically. |
| 7 | How do you enable inspected spoke-to-spoke traffic in a hub-and-spoke design? | Use User Defined Routes (UDRs) on spoke subnets pointing traffic to the hub's Azure Firewall/NVA private IP — do not create direct spoke peering. |
| 8 | Is ExpressRoute private peering traffic encrypted by default? | No. ExpressRoute private peering is NOT encrypted by default — add IPsec over ExpressRoute or MACsec (with ExpressRoute Direct) if encryption is required. S2S VPN, by contrast, is IPsec-encrypted by default. |
| 9 | ExpressRoute SLA availability? | 99.95% — applies when the circuit is configured with redundant connections at diverse peering locations. |
| 10 | What does Azure Bastion eliminate the need for on target VMs? | A public IP address on the VM and open inbound NSG rules for RDP (3389)/SSH (22) from the internet — access is brokered over TLS port 443. |
| 11 | VPN Gateway approximate aggregate throughput: Basic vs VpnGw1? | Basic ≈ 100 Mbps; VpnGw1 ≈ 650 Mbps. Exam tip: Basic SKU also has no SLA and lacks some feature support (e.g., no active-active, no BGP transit in some configs). |
| 12 | How does DNS resolve a Private Endpoint's public FQDN to its private IP? | Azure creates a CNAME from the public FQDN to a privatelink FQDN; the linked Private DNS zone then resolves that privatelink FQDN to the endpoint's private IP. |
