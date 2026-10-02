## Chapter 5: Network Perimeter Controls: NSGs, Azure Firewall, WAF, DDoS — Practice Questions

**Q1.** A company's hub VNet needs to allow outbound HTTPS traffic only to a specific list of approved SaaS domains (e.g., *.salesforce.com), while also providing full stateful L3-L7 inspection and centralized logging for all hub-spoke traffic. Which solution BEST meets these requirements?

A) NSG rules using Service Tags on the hub subnet
B) Web Application Firewall (WAF) on Application Gateway
C) Azure Firewall Premium with TLS inspection enabled
D) Azure Firewall Standard with application rules for FQDN filtering

<details>
<summary>Answer</summary>

**Correct: D**

Azure Firewall Standard supports application rules that filter outbound traffic by FQDN over HTTP/S, and provides stateful, centralized filtering ideal for hub-spoke topologies.

**Why the others are wrong:**
- Service Tags only cover Microsoft/Azure service IP ranges, not arbitrary third-party SaaS FQDNs.
- WAF protects inbound web traffic to published applications, not outbound hub-spoke traffic.
- Premium adds TLS inspection and IDPS, unnecessary and costlier when FQDN filtering alone is required (Standard already supports this).

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A global e-commerce site running on Azure App Service in multiple regions needs protection against SQL injection and cross-site scripting with the lowest possible latency for users worldwide. Which solution should be used?

A) NSG rules applied to the App Service subnet
B) Azure Firewall Standard in each region
C) WAF policy attached to Azure Front Door
D) WAF policy attached to a regional Application Gateway

<details>
<summary>Answer</summary>

**Correct: C**

Front Door is a global, edge-based service; attaching a WAF policy provides OWASP-based protection (SQLi, XSS) with low latency via Microsoft's global PoP network.

**Why the others are wrong:**
- App Service is PaaS and typically not deployed into a subnet with NSGs enforcing L7 protection.
- Azure Firewall filters network/application traffic but does not provide OWASP-based web application protection.
- Application Gateway WAF is regional, so it can't provide global low-latency protection across regions.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A security team is rolling out a new WAF Custom Rule Set on Application Gateway and wants to observe rule matches without blocking any legitimate production traffic during the initial rollout. Which WAF mode should be configured?

A) Prevention mode
B) Disable the WAF policy
C) Detection mode
D) Prevention mode with a custom rule set to Allow

<details>
<summary>Answer</summary>

**Correct: C**

Detection mode logs all rule matches to Diagnostic Logs without blocking traffic, allowing safe tuning before switching to Prevention.

**Why the others are wrong:**
- Prevention mode actively blocks matching requests, risking false positives during rollout.
- Disabling the WAF removes all protection and logging, defeating the purpose of testing.
- There is no 'Allow' action for Prevention mode that also logs matches the same way Detection does.

</details>

---

**Q4.** An organization has a web tier that autoscales VMs frequently. They want NSG rules to allow traffic from web tier VMs to database tier VMs without manually updating IP addresses each time a VM is added or removed. What should they configure?

A) NSG rules using individual VM IP addresses
B) NSG rules using Application Security Groups (ASGs)
C) NSG rules using the Internet service tag
D) Azure Firewall IP Groups referencing the subnet CIDR

<details>
<summary>Answer</summary>

**Correct: B**

ASGs let you group VM NICs by application role (e.g., 'WebTier', 'DBTier') and reference the group as source/destination in NSG rules, scaling automatically as VMs are added or removed.

**Why the others are wrong:**
- Individual IPs require manual updates every time VMs scale, which is what the requirement seeks to avoid.
- The Internet service tag represents public internet ranges, unrelated to internal tier segmentation.
- IP Groups are an Azure Firewall feature, not an NSG rule source/destination option.

</details>

---

**Q5.** A company needs to protect a set of public IP addresses attached to VMs in a VNet from large-scale volumetric DDoS attacks, and requires a cost protection SLA plus access to the DDoS Rapid Response support team during an active attack. Which solution should be deployed?

A) Azure DDoS Protection Basic
B) Azure DDoS Network Protection
C) Azure DDoS IP Protection
D) Azure Firewall Premium with IDPS

<details>
<summary>Answer</summary>

**Correct: B**

DDoS Network Protection (the VNet-scoped, full-featured tier, formerly called 'Standard') includes cost protection SLA credits, DDoS Rapid Response engineering support, and tuned ML-based mitigation policies.

**Why the others are wrong:**
- Basic is automatically enabled and free, but offers only platform-level protection with no SLA, cost protection, or Rapid Response access.
- IP Protection is a lower-cost, per-IP SKU without the cost protection SLA or Rapid Response engagement included in Network Protection.
- Azure Firewall inspects and filters traffic at L3-L7 but is not a DDoS mitigation service and provides no DDoS cost protection SLA.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** An administrator needs to create a custom NSG rule that is evaluated BEFORE the default AllowVNetInBound rule (priority 65000). Which priority value is valid for the custom rule?

A) 65001
B) 4097
C) 100
D) 0

<details>
<summary>Answer</summary>

**Correct: C**

Custom NSG rules must use a priority between 100 and 4096, with lower numbers evaluated first. A priority of 100 is valid and will be evaluated before the default rule at 65000.

**Why the others are wrong:**
- 65001 falls in the reserved default-rule range, not the valid custom rule range, and is also numerically after 65000.
- 4097 exceeds the maximum allowed custom priority of 4096.
- 0 is below the minimum allowed custom priority of 100.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Azure Firewall's Threat Intelligence feature is set to 'Alert and Deny' mode. What happens when traffic matches a known malicious IP address or domain from Microsoft Threat Intelligence feeds?

A) The traffic is logged but still allowed to pass
B) The traffic bypasses all NSG rules automatically
C) Azure Firewall automatically disables itself
D) The traffic is blocked and an alert is logged

<details>
<summary>Answer</summary>

**Correct: D**

'Alert and Deny' mode both blocks traffic matching threat intelligence indicators and generates an alert/log entry for the event.

**Why the others are wrong:**
- Logging without blocking describes 'Alert only' mode, not 'Alert and Deny'.
- Azure Firewall and NSGs operate independently; matching threat intel does not affect NSG evaluation.
- There is no self-disabling behavior in Azure Firewall based on threat intelligence matches.

</details>

---

**Q8.** What is the primary architectural distinction between a Network Security Group (NSG) and Azure Firewall?

A) NSGs cost more than Azure Firewall per hour
B) NSGs are a distributed, stateless-style 5-tuple filter applied per subnet/NIC, while Azure Firewall is a centralized, stateful managed service supporting FQDN filtering and threat intelligence
C) Azure Firewall can only protect PaaS resources, not IaaS VMs
D) NSGs natively support FQDN-based filtering, making Azure Firewall redundant

<details>
<summary>Answer</summary>

**Correct: B**

NSGs enforce simple 5-tuple allow/deny rules at the subnet or NIC level, while Azure Firewall is a fully managed, stateful, centralized firewall offering FQDN filtering, threat intelligence, and application-layer rules across the entire hub.

**Why the others are wrong:**
- NSGs are free; Azure Firewall has an hourly + data processing cost, the opposite of this statement.
- Azure Firewall can protect traffic to and from both IaaS and PaaS resources deployed within a VNet.
- NSGs do NOT support FQDN filtering — this is a distinguishing feature reserved for Azure Firewall.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

