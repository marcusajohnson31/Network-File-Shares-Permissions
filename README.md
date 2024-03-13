<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial shows how to create and test some security groups within Active Directory I will not be adding how to configure the lab since this is an addition to what you can do using active directory.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- File Explorer

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Domain Controller VM
- Create Client 1 VM
- Install Active Directory Domain Services
- Add OUs, Admin Account, multiple user employee accounts

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://imgur.com/LgL2PiV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”

</p>
<br />

<p>
<img src="https://imgur.com/isCS4Q4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 Set the following permissions (share the folder) for the “Domain Users” group:
Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
(Skip accounting for now)
</p>
<br />

<p>
<img src="https://imgur.com/eNUOLoZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Attempt to access file shares as a normal user
On Client-1, navigate to the shared folder (start, run, \\dc-1)
Try to access the folders you just created.


</p>
<br />


<p>
<img src="https://imgur.com/3cdxTiI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
An example of what happens when you try to access a file without permissions. 
</p>
<br />


<p>
<img src="https://imgur.com/IQHDRV7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create an “ACCOUNTANTS” Security Group, assign permissions, an test access
Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”

</p>
<br />



<p>
<img src="https://imgur.com/bPdC8JE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
Right click on mydomain.com -> new -> user
</p>
<br />



<p>
<img src="https://imgur.com/4gsVqai.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Add jane_admin to the “Domain Admins” Security Group
Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
User jane_admin as your admin account from now on
Right click on jane doe -> properties -> member of -> add -> type in domain admins -> find. Then add her in. 
</p>
<br />



<p>
<img src="https://imgur.com/Z4UsZMN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Join Client-1 to your domain (mydomain.com)
From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
From the Azure Portal, restart Client-1

</p>
<br />



<p>
<img src="https://imgur.com/24qYJAX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
</p>
<br />



<p>
<img src="https://imgur.com/v6Nws39.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into Client-1 as mydomain.com\jane_admin and open system properties
Click “Remote Desktop”

</p>
<br />



<p>
<img src="https://imgur.com/s5CJtQA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Allow “domain users” access to remote desktop
You can now log into Client-1 as a normal, non-administrative user now
Normally you’d want to do this with Group Policy that allows you to change MANY systems at once 

</p>
<br />


<p>
<img src="https://imgur.com/vVrhhgd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a bunch of additional users and attempt to log into client-1 with one of the users
Login to DC-1 as jane_admin
Open PowerShell_ise as an administrator
Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

</p>
<br />



<p>
<img src="https://imgur.com/BjNVEcG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Run the script (hit the play button) and observe the accounts being created



</p>
<br />



<p>
<img src="https://imgur.com/sFzAiip.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> Image of what the script is doing while creating accounts



</p>
<br />


<p>
<img src="https://imgur.com/J1oHPgE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> Head to Active Directory Uses and Comptuers, select an account you want to login to and save the username. 



</p>
<br />


<p>
<img src="https://imgur.com/IiEmpE5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> attempt to log into Client-1 with one of the accounts (take note of the password in the script)


</p>
<br />




