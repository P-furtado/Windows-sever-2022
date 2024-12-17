<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Windows Sever: A Home Lab Guide Active Directory, GPO, and Network File Sharing usinf VM Workstation PRO</h1>

<p>Welcome to the inaugural project in a comprehensive series of tutorials focused on Azure and Active Directory implementation. This initial project serves as the foundational cornerstone and setup for the subsequent  parts of this tutorial series. The primary objective is to lay the groundwork for a simple lab environment on Azure to simulate the environment in which Active Directory is employed within an enterprise setting.
</p>

<h2>Overview </h2>

<h2>Key Objectives</h2>
<h3>Virtual Machine Setup</h3>
-   VMware Workstation Pro - 1.2 GB Disk Space and 64-bit OSC
-   Windows Server 2022- 2GB Memory, 20GB Disk Space
-   Windows 10 Pro - 2GB Memory, 20GB Disk Space (minimum)


<h3>Lab Setup</h3>

1. Set Up a Virtual Lab Environment:
-	  Use virtualization software like VMware Workstation, Hyper-V, or VirtualBox.
-	  Install Windows Server (preferably Windows Server 2019 or later) and configure it as a domain controller.
-	  Install a couple of Windows client machines (e.g., Windows 10 or Windows 11 Enterprise of Pro) and join them to the domain.


<h3>Hands-On Activities</h3>
1.	Rename the server hostname
2.	Install Active Directory Tools and Promote as DC
3.	Creating Organizational Units (OUs)
	●	Objective: Organize the directory structure.
1.	Open Active Directory Users and Computers (ADUC).
2.	Create OUs for Different Geographical Locations (e.g., USA, Europe, Asia)
	-	Right-click the domain name and select New > Organizational Unit.
3.	Create a nested OU inside the locations (e.g., USA > Computers, Users, Service Accounts)
4.	Create a nested OU inside Computers (e.g., IT > Servers)
5.	Create a nested OU inside Users (e.g., Accounting, HR, IT).
  
<p>
<img width="776" alt="Creating OUs" src="https://imgur.com/a/SEn9w8i">
</p>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Configuration Steps</h2>

<h3>&#9312; Create the Domain Controller</h3>

- Create a virtual machine on Azure.
- Name it DC-01 
- Select Windows Server 2022: Azure Edition - x64 Gen2 as the image


<p>
<img width="776" alt="VM image" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/f072cd7b-b547-4006-9ddb-ae6ba39c497e">
</p>
<p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<strong> NOTE: Make sure to select at least 2 vcpus and 16 GiB memory and take note of the vnet that the VM has created.</strong>
</p>
<br />

<p>
<img width="736" alt="DC-vm" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/323e78b9-4e86-46e3-b021-6ac529ccb600">
</p>
<p>
</p>
<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9313; Set the Domain Controller's Private IP to static </h3>

-  Once the VM has been deployed, proceed to the VM overview page and select "Networking" on the left side. 
<img width="692" alt="networking" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/a35e1aad-57e1-4c1c-9e4e-aefa4fcf31ea">
<br>
<br>
<br>

-  Select Network Interface Card -> IP configurations -> ipconfig1 and set Private IP address allocation to static.

<br>

<p>
<img width="518" alt="static" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/8629a747-9809-4329-859f-2d38896ec484">
</p>

<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9314; Create the client VM </h3>

- Once again create a new VM and we'll name it Client-01. We'll select Windows 10 as the image and make sure to select at least 2 vcpus and 16 GiB memory.
<img width="717" alt="VM 2 name " src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/a3005b2a-cc0a-49f6-8b9e-c6a594c2aba9">

<br>
<br>
<br>

<p><strong> NOTE: Make sure to select the same resource group and vnet from the DC-01 VM </strong></p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<img width="731" alt="VM2 vnet" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/d591d9b0-ce68-4e74-a466-cdd34886c74b">\

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

- Now finalize everything and wait for its deployment.

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9315; Ensure connectivity between Domain Controller and Client  </h3>

<p>To ensure connectivity between the two VM's, we will ping the domain controller from the client.</p>

- First login to the Client-01 using it's public ip address and remote desktop

<img width="993" alt="client 1 public ip" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/c12a5300-fd26-4ae7-b15b-b4fee053bece">


<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<img width="297" alt="remote desktop first login" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/97467245-a6b9-4922-a668-71fdf6f77989">

<br>
<br>
<br>
<br>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Find DC-01's private ip address in the Azure Portal and copy it. Proceed to Client-01 and open the terminal and type "ping -t (DC-01 private ip address)" </strong></p>


<img width="668" alt="perpetual ping" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/d83a1cbf-2619-4382-bc3c-7025ed246119">


<br>
<br>

<p> <strong> Now notice how the request timed out, this is because ICMP v4 traffic is blocked by default on DC-01's firewall. So we will have to enable inbound ICMP traffic to allow for Client-01's ping.</strong> </p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Login to DC-01 using remote desktop and open windows defender firewall and select advanced settings. Sort by protocol and find both ICMP echo requests and enable both these rules by right clicking and selecting enable rule.</strong></p>

<br>

<img width="668" alt="firewall" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/818f7ebe-2ec3-4bd5-b59a-2bc55c24a567">

<br>

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Now once the traffic has been enabled, you can check back with Client-01 and notice that the ping is now successful.</strong> </p>

<img width="334" alt="ping 2" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/ede5ce46-2d9d-49c6-82d7-5afc9796294b">

<h2> Final Thoughts </h2>

<p> We've completed the foundational setup for our Azure and Active Directory project series. By configuring two virtual machines, we've laid the groundwork for implementing the subsequent set of projects. In this project, we focused on establishing a Domain Controller and a Client machine, enabling remote access, and briefly examining network traffic between them. Moving forward, this foundation will help implement more advanced configurations and practical scenarios in Azure and Active Directory. </p>
