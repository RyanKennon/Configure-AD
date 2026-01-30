<p align="center">
  <img src="https://github.com/user-attachments/assets/7b65e021-0e08-42ae-8da2-f57cd11aceb7" width="300" height="168" alt="image" />
</p>

# Active Directory Domain Setup

This project documents the deployment of a functional **Active Directory environment** hosted within **Microsoft Azure**. I deployed two virtual machines, configured a static IP address for the domain controller, installed Active Directory Domain Services, promoted the server to a domain controller, and verified domain functionality by attaching a Windows client to the new domain. This project demonstrates the foundational steps required to build a Windows Server–based domain environment.

---

## Environments and Technologies Used

- Microsoft Azure
- Azure Virtual Network
- Remote Desktop Protocol (RDP)
- Active Directory Domain Servies (AD DS)
- Active Directory Users and Computers
- PowerShell

---

## Lab Objective

- Deploy a Windows Server domain controller in Azure
- Install and configure Active Directory Domain Services
- Create and configure an Active Directory forest
- Join a Windows client to the domain
- Validate authentication and directory functionality

---

## Step-by-Step Walkthrough

---

### 1) Environment Setup

- **Platform:** Microsoft Azure
- **Domain Controller:** Windows Server 2022 Datacenter (Azure VM)
- **Client Machine:** Windows 10 Pro (Azure VM)
- **Make sure that the DC and Client are on the same subnet**

<p align="center">
  <img width="1875" height="579" alt="Drawing1 drawio (1)" src="https://github.com/user-attachments/assets/b8b5aca5-67de-41b0-8b77-e8abeff3c428" />
</p>

<p align="center">
  <img width="1284" height="490" alt="Drawing2 drawio" src="https://github.com/user-attachments/assets/7775f5a4-1e86-478b-85fb-b5babbef851c">
</p>

---

### 2) Make the DC's IP address Static

1. Select the **Domain Controller**
2. Select **Network Settings**
3. Open **Network Interface**

<p align="center">
  <img width="1626" height="533" alt="Drawing3 drawio" src="https://github.com/user-attachments/assets/3d2ec7e6-8b41-4d2c-8082-577b8f82d426">
</p>

4. Select **ipconfig1**
5. For Private IP address setting choose **Static**
6. Save

<p align="center">
  <img width="1870" height="762" alt="Drawing4 drawio" src="https://github.com/user-attachments/assets/b978ad18-23b4-420e-8dec-4edf7962d113" />
</p>

---

### 3) Attach the Client VM to the DC

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

8. Restart the client VM

---

### 4) Install Active Directory Domain Services

1. Log into the **Domain Controller**
2. Open **Server Manager**
3. Select **Add roles and features**
4. On the **Server Roles** tab check **Active Directory Domain Services**
5. Complete the installation

<p align="center">
  <img width="783" height="558" alt="Drawing6 drawio (1)" src="https://github.com/user-attachments/assets/501c6406-cc17-46e2-9f33-6abc957f1de4" />
</p>

---
### 5) Promote Server to Domain Controller

1. In **Server Manager**, click the **notification flag**
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
6. Complete the install and reboot the VMM

---

### 6) Verify Domain Functionality

1. Log into the **Client Virtual Machine** as the **Domain Administrator
2. Open **Windows PowerShell**
3. Attempt to ping the DC's private IP address
4. Ensure the ping succeeded

<p align="center">
  <img width="858" height="396" alt="Drawing9 drawio" src="https://github.com/user-attachments/assets/e726fac9-d102-4c9b-93f6-c5e6f93eda7d" />
</p>


5. Enter the command **ipconfig /all** into Windows Powershell
6. Confirm the output for the client's DNS settings shows the DC's private IP address

<p align="center">
  <img width="859" height="561" alt="Drawing10 drawio" src="https://github.com/user-attachments/assets/cb116758-0992-466c-9230-885a7b8a4ebc" />
</p>

---

### 7) Enable Remote Dial-In for Non-Administrative Users

1. In the **Client Virtual Machine** right click the **Start Button** and select **System**
2. Navigate to the **About** page
3. Select **Rename this PC (advanced)
4. Click **Change**
5. Check the **Member of Domain** box and enter the name of the **domain**
6. Apply the changes

<p align="center">
  <img width="1638" height="1079" alt="Previous1 drawio (1)" src="https://github.com/user-attachments/assets/490a7c5f-43c2-4692-836e-791d75116410" />
</p>

---

### 8) Give remote Desktop Permissions to Domain Users

1. On the **Client Virtual Machine** right click the **Start Button** and select **Computer Management**
2. Go to **Local Users and Groups** and open the **Groups** folder
3. Select **Remote Desktop Users** and click **Add**
4. Type **Domain Users** in the box and click **Check Names**
5. Apply the changes

<p align="center">
  <img width="1315" height="835" alt="Untitled Diagram drawio" src="https://github.com/user-attachments/assets/0e47978d-ae31-48e5-b0ee-769e49cf6ae9" />
</p>

9. Restart the VM

---

### 9) Verify the Virtual Machines are Connected

1. Open the **Server Manager** on the **Domain Controller**
2. Select **Tools** then **Active Directory Users and Computers**

<p align="center">
  <img width="1921" height="746" alt="Previous2 drawio (2)" src="https://github.com/user-attachments/assets/3a758583-b630-4971-839f-a02f0c974cab" />
</p>

3. Expand the **Domain** then click **Computers**
4. The client VM should be inside

<p align="center">
  <img width="754" height="529" alt="Previous3 drawio" src="https://github.com/user-attachments/assets/8ce7e5f3-34c7-4138-98ce-e09fe37048f9" />
</p>

---

## Outcome

- Deployed a Windows Server domain controller and a Windows client VM in Microsoft Azure  
- Configured a static IP address for the domain controller to ensure consistent DNS and domain availability  
- Established a functioning Active Directory Domain Services (AD DS) environment  
- Promoted the server to a domain controller and created a new domain for the lab  
- Joined the client VM to the domain and confirmed domain connectivity  
- Verified that domain authentication and basic domain functionality were working as expected

---

## Skills Demonstrated

- Deploying Azure Virtual Machines for server and client environments  
- Configuring static IP addresses in Azure for reliable domain controller DNS resolution  
- Connecting and configuring virtual machines within the same Azure virtual network  
- Installing and managing Active Directory Domain Services (AD DS)  
- Promoting a Windows Server to a domain controller and creating a new domain  
- Joining Windows client machines to a domain  
- Verifying domain functionality, including DNS, authentication, and domain connectivity  
- Using Azure Portal and Windows Server administration tools to manage cloud-hosted infrastructure
