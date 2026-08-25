# AZ-104-Exam-Prep-Practice-Questions-and-Study-Guide

# Microsoft Azure Administrator (AZ-104) Exam Preparation Guide & Resources

Welcome to the comprehensive community study repository for the **[Microsoft Certified: Azure Administrator Associate AZ-104](https://www.certsvault.com/exams/microsoft/az-104)** exam. This repository is curated to provide cloud engineers, system administrators, and IT professionals with a structured roadmap, official documentation references, study strategies, and scenario-based practice questions.

---

## 📌 Exam Overview

* **Exam Code:** AZ-104
* **Certification:** Microsoft Certified: Azure Administrator Associate
* **Format:** Multiple-choice, multiple-response, case studies, drag-and-drop, and hot area questions
* **Duration:** 100–120 minutes
* **Passing Score:** 700 / 1000
* **Target Audience:** IT professionals responsible for implementing, managing, and monitoring identity, governance, storage, compute, and virtual networks in Microsoft Azure.

---

## 🎯 Exam Objectives & Domain Breakdown

| Domain | Exam Weight | Key Focus Areas |
|---|---|---|
| **Manage Azure identities and governance** | 20% – 25% | Microsoft Entra ID (users/groups), RBAC, Azure Policy, resource locks, management groups, subscriptions, and cost management. |
| **Implement and manage storage** | 15% – 20% | Storage accounts, Blob access tiers, lifecycle management rules, Azure Files, file shares, SAS tokens, and Storage firewalls. |
| **Deploy and manage Azure compute resources** | 20% – 25% | Azure Virtual Machines (VMs), VM Scale Sets (VMSS), Availability Sets & Zones, Azure Container Instances (ACI), Azure Container Apps (ACA), Azure App Service plans. |
| **Implement and manage virtual networking** | 15% – 20% | Virtual Networks (VNets), subnets, VNet peering, Network Security Groups (NSGs), Azure Bastion, User Defined Routes (UDRs), Azure DNS, and Azure Load Balancer. |
| **Monitor and maintain Azure resources** | 10% – 15% | Azure Monitor metrics and log analytics, alert rules, Action Groups, Network Watcher, and Azure Backup / Recovery Services vaults. |

---

## 📚 Official Microsoft Study Resources

To build a solid foundational and practical understanding, review the official Microsoft Learn paths and guides:

* [Microsoft Learn: Official AZ-104 Exam Overview & Skills Measured](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-104)
* [AZ-104: Prerequisites for Azure Administrators](https://learn.microsoft.com/en-us/training/paths/az-104-administrator-prerequisites/)
* [AZ-104: Manage Identities and Governance in Azure](https://learn.microsoft.com/en-us/training/paths/az-104-manage-identities-governance/)
* [AZ-104: Implement and Manage Storage in Azure](https://learn.microsoft.com/en-us/training/paths/az-104-manage-storage/)
* [AZ-104: Deploy and Manage Azure Compute Resources](https://learn.microsoft.com/en-us/training/paths/az-104-deploy-manage-compute-resources/)
* [AZ-104: Configure and Manage Virtual Networks for Azure Administrators](https://learn.microsoft.com/en-us/training/paths/az-104-manage-virtual-networks/)
* [AZ-104: Monitor and Back Up Azure Resources](https://learn.microsoft.com/en-us/training/paths/az-104-monitor-backup-resources/)
* [Azure Architecture Center: Best Practices & Reference Architectures](https://learn.microsoft.com/en-us/azure/architecture/)

---

## 📝 Practice Questions by CertsVault

Evaluate your readiness with these realistic, scenario-based practice questions aligned with the latest AZ-104 objectives.

---

### Question 1: Azure Governance & Policy
**Scenario:** Your company has three subscriptions linked to the same Microsoft Entra tenant. You must ensure that virtual machines in all subscriptions can only be deployed in the `East US` and `West US` regions. If an administrator attempts to deploy a VM in any other region, the deployment must fail immediately.

What should you configure?

* A) Create an Azure Policy definition with the `Deny` effect and assign it at the Root Management Group level.
* B) Apply a ReadOnly Resource Lock to each Resource Group across all subscriptions.
* C) Create an Azure Role-Based Access Control (RBAC) role assignment with a custom `NotActions` condition.
* D) Configure an Azure Advisor recommendation and attach an Action Group with a webhook.

<details>
<summary><b>View Answer & Explanation</b></summary>

**Correct Answer:** **A) Create an Azure Policy definition with the `Deny` effect and assign it at the Root Management Group level.**  
**Explanation:**  
* **Azure Policy** is designed to enforce organizational governance and compliance at scale. Using the built-in "Allowed locations" policy with a **Deny** effect prevents resource creation outside approved regions.
* Assigning this policy at the **Management Group** level ensures it inherits downward across all underlying subscriptions automatically.
* Resource locks prevent accidental deletion or modification of existing resources, not regional placement of new resources.
</details>

---

### Question 2: Storage Account Lifecycle Management
**Scenario:** You manage an Azure General-purpose v2 storage account containing billions of log files in block blob storage. The compliance policy states:
1. Logs are accessed frequently during the first 30 days.
2. Logs are accessed infrequently between day 31 and day 90.
3. Logs must be retained for 7 years for auditing, after which they must be deleted.
4. Storage costs must be minimized.

What is the best lifecycle management rule configuration?

* A) Transition blobs to Archive tier after 30 days, then delete blobs after 2555 days (7 years).
* B) Transition blobs to Cool tier after 30 days, transition blobs to Archive tier after 90 days, and delete blobs after 2555 days.
* C) Transition blobs to Cold tier after 30 days and delete blobs after 90 days.
* D) Use an Azure Function triggered daily to run an AzCopy script moving blobs between container tiers.

<details>
<summary><b>View Answer & Explanation</b></summary>

**Correct Answer:** **B) Transition blobs to Cool tier after 30 days, transition blobs to Archive tier after 90 days, and delete blobs after 2555 days.**  
**Explanation:**  
* **Hot Tier:** Optimal for active data (first 30 days).
* **Cool Tier:** Lower storage cost, ideal for infrequently accessed data (days 31–90).
* **Archive Tier:** Lowest storage cost for long-term historical records that can tolerate retrieval latency (days 91 through year 7).
* Native **Azure Blob Lifecycle Management** automates tier transitions and scheduled deletion without requiring custom scripts or Azure Functions.
</details>

---

### Question 3: Virtual Network Routing & Traffic Inspection
**Scenario:** You have two subnets in `VNet1`: `Subnet-Web` (`10.0.1.0/24`) and `Subnet-DB` (`10.0.2.0/24`). You deploy a Network Virtual Appliance (NVA) firewall into `Subnet-DMZ` at IP address `10.0.0.4`. You need to ensure all traffic originating from `Subnet-Web` destined for `Subnet-DB` routes through the NVA firewall.

What should you implement?

* A) Create a Network Security Group (NSG) rule on `Subnet-Web` allowing traffic only to `10.0.0.4`.
* B) Create a Route Table (User Defined Route) with a route for prefix `10.0.2.0/24` with Next Hop Type `Virtual appliance` (`10.0.0.4`), and associate the route table with `Subnet-Web`.
* C) Enable Virtual Network Peering between `Subnet-Web` and `Subnet-DB` using Gateway Transit.
* D) Configure an Azure Application Gateway with URL path-based routing.

<details>
<summary><b>View Answer & Explanation</b></summary>

**Correct Answer:** **B) Create a Route Table (User Defined Route) with a route for prefix `10.0.2.0/24` with Next Hop Type `Virtual appliance` (`10.0.0.4`), and associate the route table with `Subnet-Web`.**  
**Explanation:**  
* By default, Azure routes all subnet-to-subnet traffic directly using system routes.
* To force traffic through a firewall or NVA, you must configure a **User-Defined Route (UDR)** inside a Route Table targeting the destination subnet (`10.0.2.0/24`) with the next hop set to **Virtual Appliance** (`10.0.0.4`), then associate that Route Table to the source subnet (`Subnet-Web`).
</details>

---

### Question 4: Azure Compute & High Availability
**Scenario:** You are deploying a mission-critical web application on Azure Virtual Machines. The application requires a 99.99% composite SLA for compute availability. The chosen Azure region supports Availability Zones.

How should you distribute the virtual machines?

* A) Deploy the VMs across two or more Availability Zones within the same Azure region.
* B) Deploy all VMs inside a single Availability Set with 3 Fault Domains and 5 Update Domains.
* C) Deploy all VMs in a single subnet with Proximity Placement Groups enabled.
* D) Deploy the VMs in an unmanaged scale set across multiple resource groups.

<details>
<summary><b>View Answer & Explanation</b></summary>

**Correct Answer:** **A) Deploy the VMs across two or more Availability Zones within the same Azure region.**  
**Explanation:**  
* Azure provides an SLA of **99.99%** for VMs when two or more instances are deployed across two or more **Availability Zones** in the same region.
* Deploying inside an **Availability Set** provides an SLA of up to **99.95%**, which does not meet the 99.99% SLA requirement.
</details>

---

### Question 5: Azure Monitor & Alerting
**Scenario:** An administrator needs to receive an SMS notification and automatically trigger an Azure Automation Runbook whenever any Virtual Machine's CPU utilization exceeds 85% for five consecutive minutes.

Which two components of Azure Monitor must be configured? (Choose two)

* A) A Metric Alert Rule targeting the Virtual Machine scope with a condition of CPU > 85% over a 5-minute aggregation period.
* B) An Action Group containing both an SMS notification receiver and an Automation Runbook receiver.
* C) An Azure Log Analytics Data Collection Rule (DCR) with an Event Log filter.
* D) An Application Insights Webhook ping test.

<details>
<summary><b>View Answer & Explanation</b></summary>

**Correct Answer:** **A and B**  
**Explanation:**  
* **Metric Alert Rules** in Azure Monitor evaluate resource metrics (such as `Percentage CPU`) at regular intervals against specified threshold conditions.
* **Action Groups** define the collection of notification preferences (SMS, Email, Push) and automated actions (Runbooks, Logic Apps, Webhooks) triggered when an alert fires.
</details>

---

## 🛠️ Recommended Study Strategy

1. **Build Hands-On Experience:** Use an [Azure Free Account](https://azure.microsoft.com/en-us/free/) or Visual Studio Developer subscription to practice provisioning resources, configuring VNet peering, setting up Azure Bastion, and configuring Storage lifecycle rules.
2. **Complete the GitHub Interactive Labs:** Work through the [MicrosoftLearning/AZ-104-MicrosoftAzureAdministrator](https://github.com/MicrosoftLearning/AZ-104-MicrosoftAzureAdministrator) hands-on lab repository.
3. **Master Azure CLI & PowerShell:** Practice deploying resources via both the Azure Portal and CLI commands (`az vm create`, `az network vnet create`).
4. **Reinforce Knowledge with Practice Assessments:** Test your scenario-analysis skills and time management using curated practice questions by CertsVault.

---

## 🤝 Contributing

Contributions are welcome! If you have suggestions for new practice questions, updated documentation links, or architectural diagrams, please open a pull request or file an issue.
