<p align="center">
  <img src="https://github.com/user-attachments/assets/7b65e021-0e08-42ae-8da2-f57cd11aceb7" width="300" height="168" alt="image" />
</p>

# Configuring On-Premises Active Directory within Azure VMs

This project documents the deployment of a traditional **on-premises Active Directory environment** hosted within **Microsoft Azure Virtual Machines**.
The goal is to demonstrate foundational identity, authentication, and domain management concepts using cloud-based infrastructure while preserving classic on-prem AD architecture.

---

## Environments and Technologies Used

- Microsoft Azure
- Azure Virtual Network
- Remote Desktop Protocol (RDP)
- Active Directory Domain Services (AD DS)
- PowerShell

---

## Lab Objective

- Deploy A Windows Server domain controller in Azure
- Install and configure Active Directory Domain Services
- Create and configure an Active Directory forest
- Join a Windows client to the domain
- Validate authentication and directory functionality

---

## Step-by-Step Summary

---

## 1) Create Azure Virtual Machines

### Domain Controller (DC)
- Image: Windows Server 2022 Datacenter
- Size: Minimum 2 vcpus

### Client Machine
- Image: Windows 10 Pro
- **Make sure that the DC and Client are on the same subnet**

<p align="center">
  <img width="1875" height="579" alt="drawing1 drawio" src="https://github.com/user-attachments/assets/bdb4940f-d0d3-4f76-8295-e72e90cfc1c8">
</p>

<p align="center">
  <img width="1284" height="490" alt="Drawing2 drawio" src="https://github.com/user-attachments/assets/7775f5a4-1e86-478b-85fb-b5babbef851c">
</p>

---

## 2) Make the DC's IP address Static

1. Select the **Domain Controller**
2. Select **Network Settings**
3. Open **Network Interface**

<p align="center">
  <img width="1626" height="533" alt="Drawing3 drawio" src="https://github.com/user-attachments/assets/3d2ec7e6-8b41-4d2c-8082-577b8f82d426">
</p>

4. Select ipconfig1
5. For Private IP address setting choose **Static**
6. Save

<p align="center">
  <img width="1870" height="762" alt="Drawing4 drawio" src="https://github.com/user-attachments/assets/b978ad18-23b4-420e-8dec-4edf7962d113" />
</p>

---

## 3) Attach the Client VM to the DC

1. Select **Client virtual machine**
2. Select **Network Settings**
3. Open **Network Interface**
4. Select **DNS Servers**
5. Choose **Custom**
6. Enter the **DC's Private IP address**
7. Save

<p align="center">
  <img width="1384" height="629" alt="Drawing5 drawio" src="https://github.com/user-attachments/assets/50e20109-3927-4b33-a3c9-eca327854bc1" />
</p>


---

## 4) Install Active Directory Domain Services

1. Log into the **Domain Controller**
2. Open **Server Manager**
3. Select **Add roles and features**
4. On the **Server Roles** tab check **Active Directory Domain Services**
5. Complete the installation

<p align="center">
  <img width="783" height="558" alt="Drawing6 drawio" src="https://github.com/user-attachments/assets/c9b654a1-ed65-4f29-b1fa-c34021be1262" />
</p>


---

## 5) Promote Server to Domain Controller

1. In **Server Manager**, click the notification flag
2. Select **Promote this server to a domain controller**

<p align="center">
  <img width="1921" height="784" alt="Drawing7 drawio" src="https://github.com/user-attachments/assets/1dde3344-4dd4-4051-bf4a-c71120f3a326" />
</p>


3. Choose **Add a new forest**
4. Set the root domain name

<p align="center">
  <img width="759" height="556" alt="Drawing8 drawio" src="https://github.com/user-attachments/assets/1fff2c8d-80e7-4574-98f3-9bea980308ef" />
</p>


5. Set the Directory Services Restore Mode (DSRM) password
6. Complete the wizard and reboot the server

---

## 6) Verify Domain Functionality

1. Log into the Client Virtual Machine
2. Open **Windows PowerShell**
3. Attempt to ping the DC's private IP address
4. Ensure the ping succeeded

<p align="center">
  <img width="858" height="396" alt="Drawing9 drawio" src="https://github.com/user-attachments/assets/e726fac9-d102-4c9b-93f6-c5e6f93eda7d" />
</p>


5. Enter **ipconfig /all** into Windows Powershell
6. Confirm the output for the client's DNS settings shows the DC's private IP address

<p align="center">
  <img width="859" height="561" alt="Drawing10 drawio" src="https://github.com/user-attachments/assets/cb116758-0992-466c-9230-885a7b8a4ebc" />
</p>


---


