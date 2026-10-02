## Chapter 8: Securing Containers and Azure Kubernetes Service — Practice Questions

**Q1.** A company runs an AKS cluster with a mix of Linux and Windows Server 2022 node pools. They need Kubernetes NetworkPolicy objects to be enforced consistently across both operating systems. Which network policy engine must be selected?

A) Azure Network Policy Manager (Azure NPM)
B) Calico network policy
C) Azure Firewall Manager
D) Network Security Groups (NSGs) on the subnet

<details>
<summary>Answer</summary>

**Correct: B**

Calico is the only AKS network policy engine that supports both Linux and Windows Server node pools.

**Why the others are wrong:**
- Azure NPM only enforces network policy on Linux nodes — Windows pods are unprotected.
- Azure Firewall operates at the perimeter/egress layer, not pod-to-pod traffic inside the cluster.
- NSGs filter traffic at the subnet/NIC level and cannot enforce Kubernetes label-based NetworkPolicy objects.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A security team wants continuous vulnerability scanning of container images stored in Azure Container Registry, including rescans when new CVEs are disclosed, without deploying a third-party scanner. Which service should they enable?

A) Azure Policy built-in initiative for ACR
B) Microsoft Sentinel connector for ACR
C) Microsoft Defender for Containers
D) Azure Monitor Container insights

<details>
<summary>Answer</summary>

**Correct: C**

Microsoft Defender for Containers integrates Microsoft Defender Vulnerability Management to scan images in ACR and rescan them as new vulnerabilities are disclosed.

**Why the others are wrong:**
- Azure Policy can require registries to be scanned but does not itself perform vulnerability scanning.
- Sentinel is a SIEM/SOAR platform for log analytics and detections, not an image scanner.
- Container insights collects performance/log telemetry, not vulnerability findings.

</details>

---

**Q3.** AKS pods must authenticate to Azure Key Vault using an Azure AD identity without storing any secrets or certificates inside the cluster, using OIDC federation to replace a deprecated pod-identity solution. Which feature satisfies this requirement?

A) AAD Pod Identity
B) Managed identity assigned directly to the VMSS node pool
C) Kubernetes ServiceAccount token with a stored client secret
D) Microsoft Entra Workload Identity

<details>
<summary>Answer</summary>

**Correct: D**

Microsoft Entra Workload Identity federates a Kubernetes service account with an Entra app registration via OIDC, issuing short-lived tokens with no secrets stored in the cluster; it is the supported replacement for AAD Pod Identity.

**Why the others are wrong:**
- AAD Pod Identity has been retired and is no longer the supported approach.
- A node-level managed identity grants the identity to every pod on that node, violating least privilege and pod-level scoping.
- Storing a client secret in a ServiceAccount defeats the goal of a secretless authentication model.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A team needs Key Vault secrets mounted into pods as files AND automatically synced to native Kubernetes Secret objects so legacy apps can consume them as environment variables, with periodic refresh when the secret value changes in Key Vault. Which component should they configure?

A) Kubernetes native Secrets created manually via kubectl
B) Azure App Configuration references in the deployment YAML
C) ConfigMap populated by an Azure Function on a timer trigger
D) Azure Key Vault Provider for Secrets Store CSI Driver with secretObjects and rotation enabled

<details>
<summary>Answer</summary>

**Correct: D**

The Secrets Store CSI Driver mounts Key Vault secrets as files and, when secretObjects is defined with rotation enabled, syncs them into Kubernetes Secrets and refreshes on a poll interval.

**Why the others are wrong:**
- Manually created Secrets require manual updates and don't stay in sync with Key Vault.
- App Configuration references values but doesn't natively sync to Kubernetes Secret objects for pod consumption.
- A custom Function-based ConfigMap sync is an unsupported, unofficial workaround not tested on the exam.

</details>

---

**Q5.** A company requires that the AKS API server never be exposed with a public IP address, and cluster management traffic must only traverse their private network via ExpressRoute. Which configuration meets this requirement?

A) Enable authorized IP ranges on the API server
B) Restrict the AKS load balancer to internal only
C) Enable an AKS private cluster
D) Apply an NSG rule denying 0.0.0.0/0 on the API server subnet

<details>
<summary>Answer</summary>

**Correct: C**

An AKS private cluster provisions the API server with a private endpoint and private DNS zone, eliminating any public IP for the control plane.

**Why the others are wrong:**
- Authorized IP ranges still leave the API server on a public IP, just filtered by source address — it does not remove public exposure.
- Internal load balancer settings affect application services, not the control plane API server endpoint.
- NSGs cannot be applied to the managed API server resource, which lives outside the customer's controllable subnet in a non-private cluster.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** Which Azure CLI flag, used at cluster creation, configures Calico as the AKS network policy engine?

A) --network-policy calico
B) --network-policy azure
C) --enable-calico
D) --network-plugin calico

<details>
<summary>Answer</summary>

**Correct: A**

The correct flag is --network-policy calico, specified alongside --network-plugin during az aks create.

**Why the others are wrong:**
- This value selects the Azure Network Policy Manager engine instead of Calico.
- This flag does not exist; Calico is not enabled with a dedicated boolean flag.
- --network-plugin controls the CNI (kubenet/azure), not the network policy engine.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** What is the default rotation poll interval for the Azure Key Vault Provider for Secrets Store CSI Driver when secret rotation is enabled?

A) 30 seconds
B) 15 minutes
C) 2 minutes
D) 24 hours

<details>
<summary>Answer</summary>

**Correct: C**

The default rotationPollInterval is 2 minutes when --enable-secret-rotation is set on the add-on.

**Why the others are wrong:**
- 30 seconds is faster than the documented default and would cause unnecessary Key Vault call volume.
- 15 minutes is not the configured default value.
- 24 hours is far too infrequent for the documented default rotation behavior.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Since PodSecurityPolicy (PSP) was removed in Kubernetes 1.25, which built-in Kubernetes mechanism now enforces the Privileged, Baseline, and Restricted profiles at the namespace level in AKS?

A) Azure RBAC for Kubernetes authorization
B) Network Policy admission webhook
C) Kubernetes ResourceQuota
D) Pod Security Admission (PSA)

<details>
<summary>Answer</summary>

**Correct: D**

Pod Security Admission is the built-in, in-tree Kubernetes admission controller that replaced PSP, enforcing the three standard Pod Security Standards profiles via namespace labels.

**Why the others are wrong:**
- Azure RBAC controls who can perform actions on the API, not pod-level security context enforcement.
- Network policy webhooks control network traffic, not pod security context fields like privilege escalation.
- ResourceQuota limits compute/object counts, not security posture of pod specs.

</details>

---

