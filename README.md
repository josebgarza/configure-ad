<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>(On-Premises) Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resources
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

![Screen Shot 2024-12-28 at 5 57 16 PM](https://github.com/user-attachments/assets/b6c3610b-5946-4623-901a-bb46bbc56983)

![Screen Shot 2024-12-28 at 6 01 43 PM](https://github.com/user-attachments/assets/e39312a1-2908-49df-98c2-65e215afc3ec)

First, create a new Resource Group (RG) and Virtual Network
</p>
<br />

![Screen Shot 2024-12-28 at 6 07 23 PM](https://github.com/user-attachments/assets/37370888-3ada-4604-8fc0-2f0f4fbf7590)

Create the Domain Controller VM (Windows Server 2022) named “DC-1”
</p>
<br />

![Screen Shot 2024-12-28 at 6 21 33 PM](https://github.com/user-attachments/assets/3846d4e4-ae36-4f9b-87bb-b70c286557c7)

Create the Client VM (Windows 10) named “Client-1”
</p>
<br />

![Screen Shot 2024-12-28 at 6 32 44 PM](https://github.com/user-attachments/assets/a23c8764-34bf-41f6-ba0a-f6ecd646b0d1)

Set Domain Controller’s NIC Private IP address to be static:
</p>
<br />

![Screen Shot 2024-12-28 at 6 36 23 PM](https://github.com/user-attachments/assets/ce1cf6c3-8c41-4830-80ed-3ff3c07dea53)

![Screen Shot 2024-12-28 at 6 39 20 PM](https://github.com/user-attachments/assets/cab63291-edf7-4564-a259-588520d6a8ad)

Log into the VM and disable the Windows Firewall (for testing connectivity)
</p>
<br />

![Screen Shot 2024-12-28 at 6 43 32 PM](https://github.com/user-attachments/assets/fb9effae-f34e-48a3-8bfd-2b28ac8f18a2)

Set Client-1’s DNS settings to DC-1’s Private IP address
</p>
<br />

![Screen Shot 2024-12-28 at 6 49 04 PM](https://github.com/user-attachments/assets/69b8ce9f-5fcf-42af-b941-87e7aaee8aea)

Login to Client-1 and attempt to ping DC-1’s private IP address to ensure connectivity

</p>
<br />

![Screen Shot 2024-12-28 at 6 58 52 PM](https://github.com/user-attachments/assets/ad465d35-b48e-4317-8a77-a7479bd4e11b)

![Screen Shot 2024-12-28 at 6 59 30 PM](https://github.com/user-attachments/assets/3bea5bf9-a2a8-4753-8c9b-1595a06be77b)

![Screen Shot 2024-12-28 at 7 01 03 PM](https://github.com/user-attachments/assets/bea86b90-ecae-4e2c-9cb0-02c15912f786)

Once connectivity is confirmed, login to DC-1 and install Active Directory Domain Services
</p>
<br />

![Screen Shot 2024-12-28 at 7 04 20 PM](https://github.com/user-attachments/assets/3b55c004-f353-4822-ae4a-14942e670db5)

Promote as a Domain Controller
</p>
<br />

![Screen Shot 2024-12-28 at 7 05 35 PM](https://github.com/user-attachments/assets/7360235a-c3ed-46c6-b67f-0f5680070b42)

![Screen Shot 2024-12-28 at 7 07 00 PM](https://github.com/user-attachments/assets/2c102f34-64f9-4c94-ab66-0ebb1b692d81)

Setup a new forest as mydomain.com (can be anything, just remember what it is). I did "mydomain.com" as an example. Install the program.
</p>
<br />

![Screen Shot 2024-12-28 at 7 27 44 PM](https://github.com/user-attachments/assets/de729c19-561d-4fd9-aaa3-2c959e59ca8a)

![Screen Shot 2024-12-28 at 7 28 53 PM](https://github.com/user-attachments/assets/3429abc0-c304-46e4-9e5a-286a8099ed01)

In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” and another one called "_ADMINS"
</p>
<br />

![Screen Shot 2024-12-28 at 7 31 34 PM](https://github.com/user-attachments/assets/026ceccf-479d-48d0-b947-7bb029ffd814)

![Screen Shot 2024-12-28 at 7 32 27 PM](https://github.com/user-attachments/assets/8bee698e-59fb-4af9-8be9-2be0e10ec413)

Create a new employee in "_ADMINS" named “Jane Doe”. Make note of the username and password.
</p>
<br />

![Screen Shot 2024-12-28 at 7 34 56 PM](https://github.com/user-attachments/assets/c3951ba6-66d5-435c-b216-f3f2d1fe3866)

![Screen Shot 2024-12-28 at 7 35 11 PM](https://github.com/user-attachments/assets/bbc2dccd-9248-45a8-bddc-5546dc94eca0)

Add jane_admin to the “Domain Admins” Security Group
</p>
<br />

![Screen Shot 2024-12-28 at 7 41 30 PM](https://github.com/user-attachments/assets/2b37557f-453d-452b-88f2-45c7bbd93395)

Log out/close the connection to DC-1 and log back in as “mydomain.com\jane_admin”. Use jane_admin as your admin account from now on.

</p>
<br />

![Screen Shot 2024-12-28 at 7 48 02 PM](https://github.com/user-attachments/assets/5284fa3f-1158-4fd8-8591-c5cf34aca5a9)

Now, we'll join Client-1 to your domain (mydomain.com). Login to Client-1 as the original local admin (labuser) and join it to the domain (computer will restart)
</p>
<br />

![Screen Shot 2024-12-28 at 7 51 43 PM](https://github.com/user-attachments/assets/53bd788a-5587-4963-a70b-d2de615bc91f)

Login to the Domain Controller (Windows App) and verify Client-1 shows up in Active Directory Users and Computers (ADUC).
</p>
<br />

![Screen Shot 2024-12-28 at 7 53 33 PM](https://github.com/user-attachments/assets/90531d6f-2ba8-4f20-b850-8db5299af87e)

Create a new OU named “_CLIENTS” and drag Client-1 into there.
</p>
<br />

![Screen Shot 2024-12-28 at 8 01 50 PM](https://github.com/user-attachments/assets/ed0f69d9-1b42-4700-a956-7488a0a778e0)

Next, setup Remote Desktop for non-administrative users on Client-1. To do this, we need to do the following:
  
  Log into Client-1 as mydomain.com\jane_admin
  
  Open system properties
  
  Click “Remote Desktop”
  
  Allow “domain users” access to remote desktop
  
  You can now log into Client-1 as a normal, non-administrative user now. Normally you’d want to do this with Group Policy that allows you to change MANY systems at once.


</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
For the final portion of this demonstration, we will create a bunch of additional users and attempt to log into client-1 with one of the users. To do this we must:

Login to DC-1 as jane_admin

Open PowerShell_ise as an administrator

Create a new file and paste the contents of this script (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into it.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
