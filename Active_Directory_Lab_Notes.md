# 🖥️ Active Directory Home Lab – Documentation  
**Created by:** Anthony Coronel  
**Tools Used:** Hyper-V, Windows Server 2022, Windows 10/11, ADUC, DNS Manager, Group Policy Management

---

## 📌 Overview
This lab simulates a small enterprise environment to practice real-world system administration tasks using Windows Server 2022.  
The setup includes a Domain Controller (DC) and a Windows client machine joined to the domain.

---

## 🧱 1. Lab Environment Setup

### **Hyper-V Configuration**
- Created two virtual machines:
  - **DC01** – Windows Server 2022  
  - **CLIENT01** – Windows 10/11 Pro
- Configured internal virtual switch for lab networking
- Assigned static IP to the Domain Controller  
  - Example:  
    - IP: 192.168.1.10  
    - Subnet: 255.255.255.0  
    - DNS: 192.168.1.10 (self)

---

## 🏰 2. Domain Controller Installation

### **Server Roles Installed**
- Active Directory Domain Services (AD DS)
- DNS Server

### **Promoted Server to Domain Controller**
- Created new forest/domain:
  - **Domain Name:** `coronel.local`  
- Restarted server to complete configuration

---

## 👥 3. Active Directory Users & Groups

Using **Active Directory Users and Computers (ADUC)**:

### **Organizational Units Created**
- **Users**
- **Groups**
- **Computers**
- **IT**
- **Accounting**
- **Sales**

### **Users Created**
- `ACoronel` – Admin user
- `TestUser01`
- `TestUser02`

### **Security Groups Created**
- `ITGroup`
- `AccountingGroup`
- `SalesGroup`

### **Group Memberships**
- ITGroup: ACornel, TestUser01  
- AccountingGroup: TestUser02  

---

## 🖥️ 4. Joining CLIENT01 to the Domain

### **Steps Completed**
1. Set DNS on CLIENT01 to **192.168.1.10**  
2. Renamed machine to `CLIENT01`  
3. Joined domain: `coronel.local`  
4. Rebooted  
5. Verified domain login using:
   - `coronel\TestUser01`

### **Verification**
- CLIENT01 appeared under **Computers** OU  
- Successful domain login confirmed proper DNS + domain config

---

## 🛠️ 5. Group Policy Configuration (GPO)

Using **Group Policy Management Console (GPMC)**:

### **GPO #1 – Password Policy**
- Minimum length: 8  
- Enforce password history  
- Password complexity enabled

### **GPO #2 – Desktop Restrictions**
- Disable Control Panel  
- Disable Task Manager  
- Block Command Prompt

### **GPO #3 – Security Settings**
- Enabled Windows Firewall  
- Enabled User Account Control (UAC)

### **Testing & Validation**
- Forced update using:
gpupdate /force

yaml
Copy code
- Logged in as TestUser01 on CLIENT01  
- Verified restrictions were applied

---

## 🧪 6. Troubleshooting Scenarios Practiced

### **Scenario 1 – DNS Misconfiguration**
- Issue: CLIENT01 couldn’t join the domain  
- Root Cause: DNS pointing to external DNS instead of DC  
- Fix:
- Set DNS to **192.168.1.10**
- Reattempted join → Success

---

### **Scenario 2 – User Account Lockout**
- Issue: TestUser01 repeatedly locked out  
- Tools Used:
- ADUC → Users Folder  
- Event Viewer → Security Logs  
- Fix:
- Reset password  
- Unlocked account  
- Educated user on password rules

---

### **Scenario 3 – Permission Denied on Shared Folder**
- Created test share on DC  
- Removed “Everyone” access  
- Gave AccountingGroup access  
- Verified TestUser02 could access  
- Tested denial for TestUser01

---

## 📄 7. Summary of Skills Practiced

- Installed and configured Windows Server 2022  
- Promoted server to Domain Controller  
- Managed Active Directory Users, Groups, and OUs  
- Created and applied Group Policy Objects  
- Configured DNS and DHCP basics  
- Joined Windows client to domain  
- Performed user lifecycle tasks  
- Practiced troubleshooting using Event Viewer, ADUC, and GPMC  
- Simulated real help desk scenarios (permissions, DNS, lockouts)

---

## 🎯 Next Steps

- Create PowerShell automation scripts for AD user creation  
- Expand lab into multi-site domain with additional servers  
- Add documentation for Windows Server DHCP Role  
- Connect AD lab to a networking lab environment

---
