## Chapter 6: Private Connectivity & Network Segmentation — Practice Questions

**Q1.** A company has an Azure SQL Database. Requirements: (1) block all public internet access, (2) allow access from an on-premises datacenter connected via Site-to-Site VPN, (3) applications must keep using the existing public FQDN without code changes. Which solution BEST meets these requirements?

A) Configure a Service Endpoint for Microsoft.Sql restricted to the application subnet
B) Deploy a Private Endpoint for the SQL server and link the privatelink.database.windows.net Private DNS zone to the VNet
C) Keep the public endpoint and add a SQL firewall rule allowing the on-premises public IP
D) Deploy Azure Bastion in front of the SQL server

<details>
<summary>Answer</summary>

**Correct: B**

Private Endpoint assigns a private IP to the SQL server reachable over the S2S VPN, and linking the privatelink.database.windows.net zone makes the existing public FQDN resolve to that private IP transparently — no app changes needed.

**Why the others are wrong:**
- Service Endpoints only restrict traffic from inside the VNet's address space as seen by Azure — on-premises traffic arriving via VPN/ExpressRoute is not natively recognized, so on-prem access would still be blocked.
- Keeping a public endpoint with a firewall rule still exposes the database to the internet, violating requirement #1.
- Azure Bastion provides secure RDP/SSH to VMs, not connectivity to PaaS databases.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An architect designs a hub-and-spoke topology with Spoke A and Spoke B both peered to the Hub VNet. No peering exists directly between Spoke A and Spoke B. What is the expected traffic behavior between Spoke A and Spoke B by default?

A) They can communicate freely because peering is transitive
B) They can communicate only over ExpressRoute
C) They can communicate only if both have Service Endpoints enabled
D) They cannot communicate because VNet peering is non-transitive by default

<details>
<summary>Answer</summary>

**Correct: D**

VNet peering is non-transitive: a peering relationship exists only between the two directly peered VNets. Spoke-to-spoke traffic requires either direct peering or routing through a hub NVA/Azure Firewall via UDRs.

**Why the others are wrong:**
- Peering does not chain automatically — this is a top exam trap.
- ExpressRoute is for on-prem-to-Azure connectivity, not spoke-to-spoke routing.
- Service Endpoints control PaaS access from a subnet; they have no effect on VNet-to-VNet routing.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** Which Private DNS zone must be linked to a VNet so applications correctly resolve a Private Endpoint for Azure Key Vault?

A) privatelink.vault.azure.net
B) privatelink.keyvault.azure.net
C) privatelink.vaultcore.azure.net
D) privatelink.core.windows.net

<details>
<summary>Answer</summary>

**Correct: C**

Azure Key Vault Private Link uses the privatelink.vaultcore.azure.net zone, while the public endpoint remains vault.azure.net — the mismatch is intentional and heavily tested.

**Why the others are wrong:**
- This matches the public FQDN suffix, not the private-link zone — a classic distractor.
- This zone name does not exist for Key Vault.
- This suffix is used for Azure Storage, not Key Vault.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A company requires the highest-bandwidth, SLA-backed, private connection between its on-premises datacenter and Azure that does not traverse the public internet and offers predictable low latency for a mission-critical workload. Which connectivity option should be selected?

A) Site-to-Site VPN over the internet
B) ExpressRoute
C) Point-to-Site VPN
D) Azure Bastion

<details>
<summary>Answer</summary>

**Correct: B**

ExpressRoute is a private, provider-facilitated connection with a 99.95% SLA (when configured with redundant connections at diverse peering locations) that bypasses the public internet entirely, offering the highest bandwidth and lowest jitter/latency of the listed options.

**Why the others are wrong:**
- S2S VPN traverses the public internet (encrypted via IPsec) and has lower guaranteed throughput/SLA than ExpressRoute.
- P2S VPN is designed for individual client connectivity, not site-to-site or bulk enterprise connectivity.
- Azure Bastion is a jump-host service for VM management, unrelated to site-to-site connectivity.

</details>

---

**Q5.** Security requires that administrators RDP and SSH into Azure VMs without assigning public IP addresses to the VMs or opening inbound NSG rules for ports 3389/22 from the internet. Which Azure service satisfies this requirement?

A) Azure Bastion
B) Point-to-Site VPN
C) Service Endpoint
D) Network Security Group rules alone

<details>
<summary>Answer</summary>

**Correct: A**

Azure Bastion is deployed in the VNet and provides RDP/SSH connectivity over TLS on port 443 directly through the Azure Portal (or native client), so target VMs never need a public IP or open inbound management ports.

**Why the others are wrong:**
- P2S VPN requires client configuration and still typically opens direct RDP/SSH ports once connected — it does not remove the need for careful NSG design.
- Service Endpoints apply to PaaS resource access, not VM management sessions.
- NSG rules alone cannot eliminate the need for a public IP if direct RDP/SSH is still required from outside the VNet.

</details>

---

**Q6.** What is the core architectural difference between a Service Endpoint and a Private Endpoint for an Azure PaaS resource?

A) Service Endpoints assign a private IP from the VNet to the PaaS resource; Private Endpoints keep the resource's public IP
B) Private Endpoints assign a private IP from the VNet to a NIC representing the PaaS resource; Service Endpoints route traffic over the Azure backbone to the resource's public IP while restricting access to selected subnets
C) They are functionally identical and differ only in price
D) Service Endpoints work only with Azure SQL Database while Private Endpoints work with all services

<details>
<summary>Answer</summary>

**Correct: B**

This is the defining distinction: Private Endpoint brings the service INTO the VNet with a private IP; Service Endpoint extends the VNet's identity OUT to the (still publicly addressed) service over the Microsoft backbone.

**Why the others are wrong:**
- This reverses the actual behavior of the two features.
- They differ significantly in DNS handling, on-prem reachability, and network exposure, not just price.
- Service Endpoints support many PaaS services (Storage, SQL, Cosmos DB, Key Vault, etc.), not just SQL.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A storage account already has a Private Endpoint configured for the blob service, but applications in the VNet still resolve the storage account FQDN to a public IP address. What is the MOST likely fix?

A) Link the privatelink.blob.core.windows.net Private DNS zone to the VNet (or configure custom DNS forwarding) so the private endpoint's private IP is returned
B) Delete and recreate the storage account
C) Add an NSG rule permitting DNS traffic on port 53
D) Enable a Service Endpoint for Microsoft.Storage on the subnet

<details>
<summary>Answer</summary>

**Correct: A**

Private Endpoints do not change DNS resolution automatically — the associated Private DNS zone (or equivalent custom DNS record) must be linked/registered so the public FQDN's CNAME resolves to the private endpoint's private IP.

**Why the others are wrong:**
- Recreating the resource does not fix a DNS configuration gap.
- NSG rules control traffic flow, not name resolution outcomes.
- Adding a Service Endpoint alongside a Private Endpoint does not fix DNS resolution and is generally unnecessary/conflicting.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** In a hub-and-spoke design, Spoke A must occasionally communicate with Spoke B, but all inter-spoke traffic must first be inspected by a central Azure Firewall deployed in the hub. Which configuration achieves this?

A) Create direct VNet peering between Spoke A and Spoke B with gateway transit enabled
B) Establish a Site-to-Site VPN tunnel directly between Spoke A and Spoke B
C) Configure User Defined Routes (UDRs) on each spoke subnet sending inter-spoke traffic to the Azure Firewall's private IP in the hub, with no direct spoke-to-spoke peering
D) Enable a Service Endpoint for Microsoft.Network on both spokes

<details>
<summary>Answer</summary>

**Correct: C**

Forcing inter-spoke traffic through the hub firewall requires UDRs that override the default system route, directing traffic to the firewall's private IP for inspection — direct spoke peering would bypass inspection entirely.

**Why the others are wrong:**
- Direct peering creates a path that bypasses the hub firewall, defeating the inspection requirement.
- A VPN tunnel between spokes is unnecessary within the same Azure region/VNet estate and also bypasses inspection.
- Service Endpoints govern PaaS resource access, not VNet-to-VNet traffic routing.

</details>

---

