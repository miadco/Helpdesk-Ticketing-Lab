# 🧾 Azure Helpdesk Ticketing Lab (osTicket Deployment)

This lab demonstrates the deployment and configuration of **osTicket** — an open-source support ticket system — on an **Azure-hosted Ubuntu Server**. It simulates a production-level IT support environment, complete with ticket automation, SLA management, and email integration.

---

## 📚 Table of Contents

- ✅ Prerequisites
- 🎯 Objectives
- 🧱 Lab Architecture
- 🚀 Phase 1: Provision Azure VM
- 🛠️ Phase 2: LAMP Stack + osTicket Setup
- 🗃️ Phase 3: MySQL and Apache Configuration
- 🌐 Phase 4: Web Configuration
- ⚙️ Phase 5: Post-Install Configuration
- 🧪 Phase 6: Simulated IT Support Scenarios
- ✉️ Phase 7: Email Integration (Optional)
- 📸 Screenshots
- 🧠 Lessons Learned
- 🧰 Technologies Used

## ✅ Prerequisites

Before you begin:

- 🔑 **Azure Subscription** with sufficient credits
- 💻 **SSH client** (e.g., Terminal, PuTTY, VS Code Remote)
- 🧠 **Basic Linux command-line knowledge**
- 📤 Optional: Gmail or Outlook account (for SMTP setup)



## 🎯 Objectives

- Deploy a secure and scalable **Ubuntu Server VM** in Azure
- Install and configure **LAMP stack** and **osTicket**
- Simulate realistic IT support operations including:
  - Identity-related ticket handling
  - Canned responses and SLA workflows
  - Email-to-ticket conversion (SMTP)
  - Audit trails and support logs
- Document and showcase ITSM knowledge with GitHub

---

## 🧱 Lab Architecture

```plaintext
┌─────────────────────┐
│ Azure Ubuntu VM     │
│ (osTicket Server)   │
├─────────────────────┤
│ Apache2             │
│ MySQL               │
│ PHP Modules         │
│ osTicket v1.18.1    │
└─────────────────────┘
         ▲
         │
  Public IP Address
         │
     Web Browser
```

📌 *Consider replacing with a visual diagram from [diagrams.net](https://www.diagrams.net) for more polish*

---

## 🚀 Phase 1: Provision Azure VM

- **Image**: Ubuntu Server 22.04 LTS
- **Size**: Standard B1ms (1 vCPU, 2 GiB RAM)
- **Resource Group**: `TicketingLab-RG`
- **VM Name**: `TicketLab-VM`
- **Open Ports**:
  - 22 (SSH)
  - 80 (HTTP)

---

## 🛠️ Phase 2: LAMP Stack + osTicket Setup

SSH into the VM and run:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2 mysql-server php php-mysqli php-imap php-apcu php-intl php-gd php-mbstring php-xml php-cli php-common unzip wget -y
```

Download and install osTicket:

```bash
cd /var/www/html
sudo wget https://github.com/osTicket/osTicket/releases/download/v1.18.1/osTicket-v1.18.1.zip
sudo unzip osTicket-v1.18.1.zip
sudo mv upload osticket
sudo chown -R www-data:www-data /var/www/html/osticket
sudo chmod -R 755 /var/www/html/osticket
```

---

## 🗃️ Phase 3: MySQL and Apache Configuration

### Configure MySQL:

```bash
sudo mysql -u root -p
```

```sql
CREATE DATABASE osticket;
CREATE USER 'ostuser'@'localhost' IDENTIFIED BY 'StrongPassword123!';
GRANT ALL PRIVILEGES ON osticket.* TO 'ostuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

> ⚠️ **Security Note:** Replace `'StrongPassword123!'` with a secure, randomly generated password for real-world deployments.

### Configure Apache:

```bash
sudo nano /etc/apache2/sites-available/osticket.conf
```

Paste:

```apache
<VirtualHost *:80>
    DocumentRoot /var/www/html/osticket
    <Directory /var/www/html/osticket>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

Then run:

```bash
sudo a2ensite osticket.conf
sudo a2enmod rewrite
sudo systemctl restart apache2
```

---

## 🌐 Phase 4: Web Configuration

1. Visit `http://<your-public-ip>/` in your browser
2. Complete the osTicket installer:
   - DB Name: `osticket`
   - DB User: `ostuser`
   - DB Password: `StrongPassword123!`
3. Post-install cleanup:
```bash
sudo rm -rf /var/www/html/osticket/setup
```

---

## ⚙️ Phase 5: Post-Install Configuration

After the initial setup, configure the osTicket platform to simulate a functional helpdesk environment.

🔗 Admin Panel: `http://<your-public-ip>/scp`

### Configure the following:

- **Agents & Roles**  
  Create IT support staff (Agents). Define Roles to control visibility and permissions (e.g., Admin, Tier 1 Support).

- **Departments**  
  Route tickets by department:  
  - IT Support  
  - Identity & Access Management  
  - Network Operations

- **Help Topics**  
  Predefined issue types to streamline automation:  
  - Password Reset  
  - Account Lockout  
  - General Inquiry

- **SLA Plans**  
  Service targets for response and resolution:  
  - Standard: 24hr  
  - Urgent: 4hr  
  - Critical: 1hr

- **Canned Responses**  
  Pre-written replies for:
  - Account provisioning
  - Welcome emails
  - Ticket closures

- **User Directory**  
  Register test end-users to simulate ticket submissions and trigger workflows.

---

## 🧪 Phase 6: Simulated IT Support Scenarios

| Ticket Type                  | Description                                         |
|-----------------------------|-----------------------------------------------------|
| Password Reset              | Identity ticket with ownership validation           |
| Account Lockout             | Support workflow involving audit log review         |
| Access Request              | Simulates entitlement approval                      |
| Email Integration Failure   | SMTP/IMAP troubleshooting scenario                  |
| Trend Analysis              | Export and review of ticket data                   |

---

## ✉️ Phase 7: Email Integration (Optional)

- Configure SMTP using Gmail or Outlook
- Enable email piping in Admin Panel
- Send test emails and verify auto-ticket creation

---

## 📸 Screenshots

> Replace each placeholder below with your actual screenshots:

### Dashboard
![osTicket Dashboard](screenshots/dashboard.png)

### Ticket Workflow
![Ticket Creation and Response](screenshots/ticket_workflow.png)

### Email-to-Ticket Trigger
![Email Integration](screenshots/email_trigger.png)

### SLA and Help Topics
![SLA Configuration](screenshots/sla_help_topics.png)

### Exported Reports
![Support Report](screenshots/exported_report.png)

---

## 🧠 Lessons Learned

- Built a cloud-hosted ITSM platform from scratch
- Practiced realistic IT support workflows
- Strengthened skills in Linux, MySQL, and Apache2
- Simulated Tier 1–2 operational scenarios
- Integrated email-based automation

---

## 🧰 Technologies Used

- Microsoft Azure
- Ubuntu Server 22.04 LTS
- osTicket v1.18.1
- Apache2
- MySQL
- PHP 8.x
- Gmail SMTP (optional)

---
