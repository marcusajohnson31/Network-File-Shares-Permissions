<p align="center">
<img src="https://imgur.com/IEvEHpp.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Network File Shares & Permissions</h1>
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
Folder: "accounting" 
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
Create an “ACCOUNTANTS” Security Group (you can do this by right clicking your forest-> new -> orgnizational units), assign permissions( choose a user to grant access right click the users name -> properties -> member of -> add -> domain admins -> check names -> apply -> ok, an test access
Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
On the “accounting” folder you created earlier, set the following permissions:
Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”
</p>
<br />



<p>
<img src="https://imgur.com/5spOFxv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, as  <someuser>, try to access the accountants folder. It should fail. 
Log out of Client-1 as  <someuser>

</p>
<br />



<p>
<img src="https://imgur.com/jpUxFAu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log out of Client-1 as  <someuser>
On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group
Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - 

</p>
<br />



<p>
<img src="https://imgur.com/V1BFEvN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This is just proof that the access works on the new user account. 
</p>
<br />



