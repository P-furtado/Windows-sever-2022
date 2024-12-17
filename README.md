<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Windows Sever: A Home Lab Guide to Active Directory, GPO, and Network File Sharing using VM Workstation PRO</h1>

<p>
</p>

<h2>Environments and Technologies Used</h2>

- Active Directory Domain Services(AD DS)
- Group Policy management Console(GPMC)
- SysInternals Tools
- File Server Resource Manager(FRSM)
- Vmware Workstation Pro
  

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 11 Enterprise (24H2)
  
<h2>Virtual Machine Setup</h2>


- 	  VMware Workstation Pro - 1.2 GB Disk Space and 64-bit OS


- 	  Windows Server 2022- 2GB Memory, 20GB Disk Space

- 	  Windows 11 Enterprise - 2GB Memory, 20GB Disk Space (minimum)

<h2>Lab Setup</h2>
<h3> Set Up a Virtual Lab Environment</h3>

-	  Use virtualization software like VMware Workstation, Hyper-V, or VirtualBox.
-	  Install Windows Server (preferably Windows Server 2019 or later) and configure it as a domain controller.
-         Install a couple of Windows client machines (e.g., Windows 10 or Windows 11 Enterprise of Pro) and join them to the domain.



   <h2>Hands-On Activities</h2>
-	  Rename the server hostname
	  
-	  Open Active Directory Users and Computers (ADUC)
	  
-	  Install Active Directory Tools and Promote as DC
  <h3>&#9312;  Creating Organizational Units (OUs)</h3>


<h3> Objective: Organize the directory structure</h3>

-	  Open Active Directory Users and Computers (ADUC).
-	  Create OUs for Different Geographical Locations (e.g., USA, Europe, Asia)
		○	Right-click the domain name and select New > Organizational Unit.
-	  Create a nested OU inside the locations (e.g., USA > Computers, Users, Service Accounts)
-	  Create a nested OU inside Computers (e.g., IT > Servers)
-	  Create a nested OU inside Users (e.g., Accounting, HR, IT)
	     <p>
<img width="700" alt="VM image" src="https://imgur.com/Z4W9hwj">
</p>

   <h3>&#9313;  Creating User Accounts</h3>
	 <h3> Objective: Create user accounts with specific attributes</h3>
	
-	  Navigate to the appropriate OU (e.g., HR).
-	  Right-click the OU and select New > User.
-	  Fill in the user details:
		○	First Name: John
		○	Last Name: Doe
		○	User Logon Name: jdoe
-	  Set a password and configure the account settings (e.g., password never expires).
- 	  Set a Description for John Doe (e.g., Recruiter)
- 	  Create more users for IT and Accounting OU following the steps above

  
    <p>
<img width="700" alt="VM image" src="https://imgur.com/a/lHkoUfz">
</p>

<h3>&#9314;  Creating Groups</h3>

<h3> Objective: Create security and distribution groups.</h3>
	
- 	  Navigate to an OU (e.g., HR)


- 	  Right-click the OU and select New > Group
	  
- 	  Name the group (e.g., #HR_Department)
		○	Select the group scope (e.g., Global) and type (e.g., Security).
	 <p>
<img width="700" alt="VM image" src="https://imgur.com/a/aPqXftZz">
</p>

<h3>&#9315;  Adding Users to Groups</h3>

<h3> Objective: Manage group memberships.</h3>

- 	 Open the properties of a user account (e.g., jdoe)

  
- 	 Go to the Member Of tab


- 	 Click Add and select the group (e.g., #HR_Department)


- 	 Verify the membership


- 	 Do the same for another user in the HR OU


- 	 Add user in the OU IT to Domain Admins Group

 <h3>&#9316;  Configure Network settings for the Server</h3>
 
- 	  Change the domain controller’s IP address to static IP


- 	  Change DNS Servers to loopback and google DNS
	  
 <h3>&#9317;  Join Windows Client to the Domains</h3>
 
- 	  Change the DNS server of the computer to the DC IP and google DNS


- 	  Join the computer to the domain and move the computer to the appropriate OU
   
     
- 	  Login with the user created in Active Directory (e.g., John Doe)
     
 <h3>&#9318;  Creating and Linking Group Policy Objects (GPOs)</h3>

<h3> Objective: Create and link policies to OUs.</h3>



- 	Open Group Policy Management Console (GPMC).

  
- 	Right-click the domain or an OU and select Create a GPO in this domain, and Link it here.

  
- 	Name the GPO (e.g., Password Policy).

  
- 	Edit the GPO and configure settings (e.g., minimum password length, password complexity).

   
- 	Link the GPO to the desired OU.

   
- 	Create more GPO to Restrict Control Panel Access, Block USB Drives and Set a default desktop wallpaper for all users
   

<h3>&#9319;  Configuring File sharing and Permissions</h3>
<h3> Objective: Set up file sharing within the AD environment.</h3>

	
	  -Create a network share (e.g., \\ServerName\SHARED). Create a folder named "SHARED" on the C: drive.

	  -Set Folder Properties
		○Right-click the folder and select "Properties."
		○Go to the "Sharing" tab


	  -Share   are the Folder
		○Click "Advanced Sharing."
		○Check "Share this folder" and provide a share name (e.g., "SharedFiles").
		○Click "Permissions" and set the share permissions (e.g., "Everyone" with "Read" access).


	  - Set   NTFS Permissions
		○Go   to the Security Tab. In the folder properties, go to the "Security" tab.
		○Edit Permissions
    		○Click "Edit" to modify the NTFS permissions.
    		○Add the appropriate users or groups and assign the necessary permissions (e.g., "Read & Execute," "Modify," etc.).


<h3>&#9320;  Map Network Drives via Group Policy</h3>

	  -Open Group Policy Management
		○On the domain controller, open the Group Policy Management Console (GPMC).

  
	  -Create a GPO
		○Create a new GPO (e.g., Mapped Drive).

	  -Configure Drive Mapping
		○Navigate to User Configuration -> Preferences -> Windows Settings -> Drive Maps.
		○Right-click and select "New" -> "Mapped Drive."
		○Set the location (e.g., \\ServerName\SHARED) and choose a drive letter.
		○Configure additional settings as needed (e.g., "Reconnect," "Label as," etc.).

  
	  -Link the GPO
		○Link the GPO to the appropriate Organizational Unit (OU) that contains the users who need access to the shared folder.


	  -Update Group Policy
		○On the client computers, update the group policy by running gpupdate /force in the command prompt or simply restart the computers.


<h3>&#9321;  Creating Service Accounts</h3>
<h3> Objective: Create and configure a service account.</h3>


	  -Navigate to the appropriate OU (e.g., Service Accounts).


	  -Right-click the OU and select New > User.


	  -Fill in the service account details (e.g., $Autologin) for name and set a Description. -Set a strong password and configure the account settings (e.g., password never expires, cannot change password).


	  -Assign the necessary permissions to the service account on the relevant resources.


	  -Set up with a client machine using Windows Autologon tool (sysinternals)



<h3>&#9322;  Configuring Account Lockout Policy</h3>
<h3> Objective: Set up account lockout policies to enhance security.</h3>
	
	  -Open GPMC and create a new GPO (e.g., Account Lockout Policy).


	  -Edit the GPO:
		○Navigate to Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
		○Configure the settings (e.g., Account lockout threshold, Account lockout duration, Reset account lockout counter after).

  
	  -Link the GPO to the desired OU.



<h2>Testing and Verification</h2>

	  -Verify User Logon: Log on to a client machine using one of the newly created user accounts.

	  -Check Group Membership:
		○Open a Command Prompt and run gpresult /r to verify applied policies and group memberships.
 
	  -Test GPOs:
		○Log on to a client machine with a user account that has GPOs configured and verify that the GPOs were applied.
 
	  -Test Network Drives:
		○Log on to a client machine with a user account that has Drive Mapping GPO configured and verify that they can access the network folder.
 
 





