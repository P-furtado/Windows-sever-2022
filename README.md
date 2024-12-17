<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Windows Sever: A Home Lab Guide Active Directory, GPO, and Network File Sharing usinf VM Workstation PRO</h1>

<p>Welcome to the inaugural project in a comprehensive series of tutorials focused on Azure and Active Directory implementation. This initial project serves as the foundational cornerstone and setup for the subsequent  parts of this tutorial series. The primary objective is to lay the groundwork for a simple lab environment on Azure to simulate the environment in which Active Directory is employed within an enterprise setting.
</p>

<h2>Virtual Machine Setup</h2>


- 	  VMware Workstation Pro - 1.2 GB Disk Space and 64-bit OS


- 	  Windows Server 2022- 2GB Memory, 20GB Disk Space

- 	  Windows 10 Pro - 2GB Memory, 20GB Disk Space (minimum)

<h2>Lab Setup</h2>
<h3> Set Up a Virtual Lab Environment</h3>

-	  Use virtualization software like VMware Workstation, Hyper-V, or VirtualBox.
-	  Install Windows Server (preferably Windows Server 2019 or later) and configure it as a domain controller.
-         Install a couple of Windows client machines (e.g., Windows 10 or Windows 11 Enterprise of Pro) and join them to the domain.


<h2>Hands-On Activities</h2>
<h3>Rename the server hostname</h3>

<h3>&#9312;  Rename the server hostname</h3>

-	  Open Active Directory Users and Computers (ADUC)
   <h3>&#9313;  Install Active Directory Tools and Promote as DC</h3>
  <h3>&#9314;  Creating Organizational Units (OUs)</h3>


Objective: Organize the directory structure
-	  Open Active Directory Users and Computers (ADUC).
-	  Create OUs for Different Geographical Locations (e.g., USA, Europe, Asia)
	○	Right-click the domain name and select New > Organizational Unit.
-	  Create a nested OU inside the locations (e.g., USA > Computers, Users, Service Accounts)
-	  Create a nested OU inside Computers (e.g., IT > Servers)
-	  Create a nested OU inside Users (e.g., Accounting, HR, IT)
-	  2.	Creating User Accounts
	 
	●	Objective: Create user accounts with specific attributes.
	○Navigate to the appropriate OU (e.g., HR).
	○Right-click the OU and select New > User.
	○Fill in the user details:
		○	First Name: John
		○	Last Name: Doe
		○	User Logon Name: jdoe
	○	Set a password and configure the account settings (e.g., password never expires).
	○	Set a Description for John Doe (e.g., Recruiter)
	○	Create more users for IT and Accounting OU following the steps above

  
    <p>
<img width="700" alt="VM image" src="https://imgur.com/Z4W9hwj">
</p>
2.	Creating User Accounts
	●	Objective: Create user accounts with specific attributes.
	○Navigate to the appropriate OU (e.g., HR).
	○Right-click the OU and select New > User.
	○Fill in the user details:
		○	First Name: John
		○	Last Name: Doe
		○	User Logon Name: jdoe
	○	Set a password and configure the account settings (e.g., password never expires).
	○	Set a Description for John Doe (e.g., Recruiter)
	○	Create more users for IT and Accounting OU following the steps above
  <p>
<img width="700" alt="VM image" src="https://imgur.com/a/lHkoUfz">
</p>
3.	Creating Groups
	●	Objective: Create security and distribution groups.
		○	Navigate to an OU (e.g., HR).
		○	Right-click the OU and select New > Group. 3.	Name the group (e.g., #HR_Department).
		○	Select the group scope (e.g., Global) and type (e.g., Security).
	 <p>
<img width="700" alt="VM image" src="https://imgur.com/a/aPqXftZz">
</p>
4.	Adding Users to Groups
	●	Objective: Manage group memberships.
	○	Open the properties of a user account (e.g., jdoe).
	○	Go to the Member Of tab.
	○	Click Add and select the group (e.g., #HR_Department).
	○	Verify the membership.
	○	Do the same for another user in the HR OU
	○	Add user in the OU IT to Domain Admins Group
5.Configure Network settings for the Server
	○	Change the domain controller’s IP address to static IP
	○	Change DNS Servers to loopback and google DNS
6.Join Windows Client to the Domain
	○	Change the DNS server of the computer to the DC IP and google DNS
	○	Join the computer to the domain and move the computer to the appropriate OU
	○	Login with the user created in Active Directory (e.g., John Doe)
7.	○	Creating and Linking Group Policy Objects (GPOs)
●Objective: Create and link policies to OUs.
	○	Open Group Policy Management Console (GPMC).
	○	Right-click the domain or an OU and select Create a GPO in this domain, and Link it here.
	○	Name the GPO (e.g., Password Policy).
	○	Edit the GPO and configure settings (e.g., minimum password length, password complexity).
	○	Link the GPO to the desired OU.
	○	Create more GPO to Restrict Control Panel Access, Block USB Drives and Set a default desktop wallpaper for all users
8.Configuring File Sharing and Permissions
	●	Objective: Set up file sharing within the AD environment
Create a network share (e.g., \\ServerName\SHARED). Create a folder named
"SHARED" on the C: drive.
Set Folder Properties
-	Right-click the folder and select "Properties."
-	Go to the "Sharing" tab
Share the Folder
-	Click "Advanced Sharing."
-	Check "Share this folder" and provide a share name (e.g., "SharedFiles").
-	Click "Permissions" and set the share permissions (e.g., "Everyone" with "Read" access).
Set NTFS Permissions
-	Go to the Security Tab. In the folder properties, go to the "Security" tab.
-	Edit Permissions
❖	Click "Edit" to modify the NTFS permissions.
❖	Add the appropriate users or groups and assign the necessary permissions (e.g., "Read & Execute," "Modify," etc.).
9.Map Network Drives via Group Policy
	Open Group Policy Management
		a.	On the domain controller, open the Group Policy Management Console (GPMC).
	Create a GPO
		a.	Create a new GPO (e.g., Mapped Drive).
	Configure Drive Mapping
		a.	Navigate to User Configuration -> Preferences -> Windows Settings -> Drive Maps.
		b.	Right-click and select "New" -> "Mapped Drive."
		c.	Set the location (e.g., \\ServerName\SHARED) and choose a drive letter.
		d.	Configure additional settings as needed (e.g., "Reconnect," "Label as," etc.).
	Link the GPO
		-	Link the GPO to the appropriate Organizational Unit (OU) that contains the users who need access to the shared folder.
	Update Group Policy
		-	On the client computers, update the group policy by running gpupdate /force in the command prompt or simply restart the computers.
10.Creating Service Accounts
	●	Objective: Create and configure a service account.
			Navigate to the appropriate OU (e.g., Service Accounts).
			Right-click the OU and select New > User.
			Fill in the service account details (e.g., $Autologin) for name and set a Description.
			Set a strong password and configure the account settings (e.g., password never expires, cannot change password).
			Assign the necessary permissions to the service account on the relevant resources.
			Set up with a client machine using Windows Autologon tool (sysinternals)
11.Configuring Account Lockout Policy
	●	Objective: Set up account lockout policies to enhance security.
		Open GPMC and create a new GPO (e.g., Account Lockout Policy).
	Edit the GPO:
		○	Navigate to Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
		○	Configure the settings (e.g., Account lockout threshold, Account lockout duration, Reset account lockout counter after).
3.	Link the GPO to the desired OU.

<h2>Testing and Verification</h2>
1.Verify User Logon: Log on to a client machine using one of the newly created user accounts.
2.Check Group Membership:
	○	Open a Command Prompt and run gpresult /r to verify applied policies and group memberships.
3.Test GPOs:
	○	Log on to a client machine with a user account that has GPOs configured and verify that the GPOs were applied.
4.Test Network Drives:
	○	Log on to a client machine with a user account that has Drive Mapping GPO configured and verify that they can access the network folder.




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
