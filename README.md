# Azure Helpdesk Ticketing System Lab

*I built this lab to demonstrate real-world IT service delivery using Microsoft Azure and osTicket, replicating what you'd expect from an enterprise helpdesk support role.*

An end-to-end simulation of a cloud-based IT service desk deployed on Microsoft Azure, showcasing core competencies in cloud administration, IT support, and systems management.

---

## ✨ Core Competencies Demonstrated

* **Cloud Infrastructure:** Provisioned and secured Azure VMs, Networking (VNet, NSG), and Static IPs.
* **IT Service Management (ITSM):** Configured a multi-tiered support structure, defined agent roles, created SLA policies, and automated ticket routing.
* **System Administration:** Deployed and managed a full LAMP stack (Linux, Apache, MySQL, PHP) on an Ubuntu server.
* **Technical Documentation:** Created detailed resolution notes simulating professional IT reporting standards.
* **Security & Incident Response:** Performed a simulated security investigation based on a suspicious login alert.
* **Cloud FinOps:** Implemented cost management best practices by deallocating resources and setting up budget alerts.

---

## ⚙️ Phased Implementation

### Phase 1: Azure Infrastructure Provisioning

* **Resource Group:** TicketingLab-RG
* **Virtual Machine:** TicketingLab-VM (Standard B2s size)
* **Operating System:** Ubuntu Server 22.04 LTS
* **Networking:** Configured VNet, NSG, and a Static Public IP
* **Security:** Created NSG inbound rules for HTTP (80), HTTPS (443), and SSH (22)

### Phase 2: LAMP Stack & osTicket Installation

* Installed Apache2, MySQL Server, and PHP v8.1 with required extensions
* Secured the MySQL instance and created a dedicated `osticket_db` database
* Deployed osTicket v1.18.1 to `/var/www/html` and completed the web installation

### Phase 3: Service Desk Configuration

* **Departments:** Tier 1 Support, Tier 2 Support, Tier 3 Security
* **Roles & Permissions:** Created granular roles for Agents to ensure proper access controls
* **Agents:** Configured three agent accounts (Alice - T1, Bob - T2, Eve - T3)

### Phase 4: SLA & Workflow Automation

* **SLA Plans:** Established a "1-Hour Response" SLA to ensure timely support
* **Automation:** Configured help topics to automatically route new tickets to the appropriate department

### Phase 5: Live Ticket Simulation

* **Password Reset (Tier 1):** Assigned to Alice, resolved without escalation
* **VPN Issue (Tier 2):** Tier 1 attempted resolution, then escalated to Bob in Tier 2 for specialized support
* **Suspicious Login (Tier 3):** Assigned directly to Eve for security investigation, which included log review and documentation

---

## 🖼️ Screenshots & Walkthrough

*(\*Insert actual screenshots below. The captions describe what each screenshot should show.)*

1. **Azure VM Configuration:**

   * Azure Portal showing TicketingLab-VM details, including its public IP, size, and resource group

2. **osTicket Admin Panel:**

   * osTicket admin dashboard, providing an overview of the system configuration sections

3. **Department & Agent Setup:**

   * Configured departments (Tier 1–3) and list of agents (Alice, Bob, Eve) with assigned roles

4. **Live Ticket Lifecycle:**

   * Composite or series of screenshots showing a ticket's journey from creation to resolution

---

## 💸 Cleanup & Cost Management

* **De-allocation:** VM was shut down from the Azure portal when not in use to stop compute charges
* **Resource Deletion:** Upon project completion, the entire `TicketingLab-RG` was deleted to remove all associated resources
