# 🌐 Networking & Troubleshooting Lab – Documentation  
**Created by:** Anthony Coronel  
**Tools Used:** Windows 10/11, Windows Server 2022, CMD, PowerShell, Hyper-V

---

## 📌 Overview
This networking lab simulates a small virtual environment used to practice real-world troubleshooting skills.  
The setup includes:

- A Domain Controller (DC01) running Windows Server 2022  
- A client machine (CLIENT01) running Windows 10/11  
- Both systems connected via a Hyper-V internal virtual switch  

This lab focuses on diagnosing connectivity issues, testing DNS, and validating network paths — the same skills required in IT Support and Help Desk roles.

---

## 🧱 1. Lab Network Setup

### **DC01 – Windows Server 2022**
- IP: **192.168.1.10**
- Subnet: **255.255.255.0**
- DNS: **192.168.1.10** (self)

### **CLIENT01 – Windows 10/11**
- Initially DHCP, later assigned static settings for testing
- DNS set to **192.168.1.10** to allow domain join

### **Hyper-V Configuration**
- Both VMs connected to an **Internal Virtual Switch**
- Network isolation ensured for consistent testing

---

## 🔍 2. Basic Connectivity Tests

### ✔ **Test 1: Ping Domain Controller**
ping 192.168.1.10

yaml
Copy code
- Result: Successful replies  
- Verified physical/virtual network connection to DC

---

### ✔ **Test 2: DNS Lookup for Domain**
nslookup coronel.local

yaml
Copy code
- Confirmed DNS server responding properly  
- Verified domain name resolution

---

### ✔ **Test 3: Ping Domain Name**
ping coronel.local

yaml
Copy code
- Tested A record and DNS resolution  
- Ensured domain was reachable by hostname

---

### ✔ **Test 4: Traceroute**
tracert 192.168.1.10

markdown
Copy code
- Single hop confirmed clean routing inside lab environment

---

## ⚠️ 3. Troubleshooting Scenarios Practiced

### **Scenario 1 – CLIENT01 Fails to Join Domain**
**Symptoms:**
- “Cannot contact domain controller”  
- DNS-related errors  

**Diagnosis:**
- Ran `ipconfig /all`  
- DNS was pointing to external DNS instead of the DC  

**Fix:**
1. Set DNS to **192.168.1.10**  
2. Flushed DNS cache:
ipconfig /flushdns

yaml
Copy code
3. Retried domain join → Successful  

---

### **Scenario 2 – Intermittent Packet Loss**
**Symptoms:**
- Pings dropped intermittently  

**Diagnosis:**
- Checked VM network adapter  
- CLIENT01 was using the wrong Hyper-V switch  

**Fix:**
- Switched to internal lab network  
- Verified 0% packet loss  

---

### **Scenario 3 – User Cannot Access Shared Folder**
**Symptoms:**
- Permission denied  
- Network connectivity confirmed  

**Diagnosis:**
- Verified share path: `\\DC01\Shared`  
- Identified missing NTFS permissions  

**Fix:**
- Added correct group to folder permissions  
- Retested user access → Success  

---

## 🧪 4. Networking Skills Practiced

- Configuring static and dynamic IP addressing  
- Using `ipconfig`, `ping`, `tracert`, `nslookup` for diagnostics  
- DNS troubleshooting and domain connectivity  
- Hyper-V network adapter configuration  
- Firewall and permission-based access testing  
- Understanding how DNS affects domain join processes  

---

## 🏁 5. Summary

This networking lab reinforced the fundamentals of IT Support troubleshooting, including:

- DNS configuration  
- Connectivity testing  
- VM networking setup  
- Resolving domain join issues  
- Permission and share-based troubleshooting  

These are real skills used daily by Help Desk and IT Support technicians.

---

## 🎯 Next Steps

- Add DHCP Role to Windows Server  
- Introduce a second subnet for routing practice  
- Create a PowerShell network diagnostic script  
- Expand documentation with screenshots for portfolio enhancement  
