## Chapter 6 Cheat Sheet: Private Connectivity & Network Segmentation

### Private Endpoint vs Service Endpoint
| Feature | Private Endpoint | Service Endpoint |
|---|---|---|
| IP assigned | Private IP (NIC) in your subnet | None — resource keeps public IP |
| On-prem access via VPN/ER | Yes (native) | No (needs extra NAT/allowlisting) |
| DNS change required | Yes — link Private DNS zone | No |
| Cost | Per-endpoint hourly + data | Free |
| Data exfil protection | Strong (traffic never leaves private IP space) | Moderate (still public IP, but VNet-restricted) |

### Common Private DNS Zone Names
| Service | Zone |
|---|---|
| Blob Storage | privatelink.blob.core.windows.net |
| Azure SQL DB | privatelink.database.windows.net |
| Key Vault | privatelink.vaultcore.azure.net (public FQDN stays vault.azure.net) |
| App Service | privatelink.azurewebsites.net |
| Cosmos DB (SQL API) | privatelink.documents.azure.com |

**Rule:** DNS resolution requires linking/registering the correct privatelink zone to the VNet — a Private Endpoint alone does not redirect DNS.

### VPN vs ExpressRoute
| Criteria | Site-to-Site VPN | ExpressRoute |
|---|---|---|
| Path | Public internet (IPsec encrypted) | Private, provider circuit (no internet) |
| Encryption | Yes, by default | No, by default (add IPsec/MACsec) |
| SLA | 99.9–99.95% (gateway-dependent; Basic SKU excluded) | 99.95% (redundant circuit config) |
| Bandwidth | ~100 Mbps (Basic) up to ~10 Gbps (VpnGw5) | 50 Mbps up to 10 Gbps (100 Gbps w/ Direct) |
| Best for | Lower cost, quick setup, moderate bandwidth | Mission-critical, high-bandwidth, low-latency hybrid links |

### Hub-and-Spoke Rules
- VNet peering is **non-transitive** — Spoke A ↔ Hub and Spoke B ↔ Hub does NOT enable Spoke A ↔ Spoke B.
- To allow inspected spoke-to-spoke traffic: use **UDRs** routing traffic to the hub's Azure Firewall/NVA private IP — do not peer spokes directly if inspection is required.
- Hub typically hosts: VPN/ExpressRoute Gateway, Azure Firewall, DNS resolver/forwarder.
- Gateway Transit lets spokes reach on-prem via the hub's gateway without their own gateway.

### Azure Bastion
- Deployed in a dedicated `AzureBastionSubnet` (min /26).
- Provides RDP/SSH over **port 443** via the portal or native client — VM needs **no public IP**, no inbound 3389/22 from internet.
- SKUs: Basic and Standard (Standard adds host scaling, native client support); check current SKU list for latest tiers before exam if updated.

### Exam Traps
1. Assuming Service Endpoints work for on-prem access — they generally don't without extra config.
2. Forgetting to link the Private DNS zone after creating a Private Endpoint (stale public IP resolution).
3. Assuming VNet peering is transitive.
4. Confusing vault.azure.net (public) with vaultcore.azure.net (private link) for Key Vault.
5. Assuming ExpressRoute is encrypted by default like VPN.
