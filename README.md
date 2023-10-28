# AD-Setup
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
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

- Configure resources in Azure
- Ensure conectivity between resources
- Install Active Directory on Domain Controller
- Create a User and assign Admin position.
- Join Client to Domain Controller
- Setup Remote Desktop for non admins and create other Users 

<h2>Deployment and Configuration Steps</h2>

<p>
<img <a href="https://imgur.com/OIrurPm"><img src="https://i.imgur.com/OIrurPm.png" title="source: imgur.com" /></a>
<a href="https://imgur.com/ZT6Qq0w"><img src="https://i.imgur.com/ZT6Qq0w.png" title="source: imgur.com" /></a>
</p>
<p>
I Start by creating both a Windows Domain Controller (DC-1) and a Virtual Machine (VM) all inside a resource group and virtual network/subnet in Azure.  Once Created I set the domain controller's NIC IP to static and check the network watcher to ensure both DC-1 and the VM are in the same resoure group.  Once that is confirmed we log into the VM and initiate a ping to DC-1's private IP with Powershell. Logging into DC-1 we enable ICMPv4 to make sure the ping goes through in firewall settings.  Now both Machines are communicating. 
</p>
<br />

<p>
<img <a href="https://imgur.com/QBvO3SU"><img src="https://i.imgur.com/QBvO3SU.png" title="source: imgur.com" /></a>
<a href="https://imgur.com/YoVmtsd"><img src="https://i.imgur.com/YoVmtsd.png" title="source: imgur.com" /></a>
</p>
<p>
Next I login to DC-1 and install active directory domain services.  Then I Promote and setup a new forest(domain can be anything).  Once it restarts log back in as that domain and the username you created when you made DC-1.  Once logged back into DC-1(under the new domain) we log into Active Directory Users and Computers (ADUC) to create several organizational units.  After that I create an user named Jane Doe, with a login of jane_doe then add that user name to the domain admins security group.  Next I log back into my new Domain as Jane.  We will use Jane's login for DC-1 for the rest of the lab.
</p>
<br />

<p>
<img <a href="https://imgur.com/MSsQ26c"><img src="https://i.imgur.com/MSsQ26c.png" title="source: imgur.com" /></a>
<a href="https://imgur.com/Xl5L6gm"><img src="https://i.imgur.com/Xl5L6gm.png" title="source: imgur.com" /></a>
<a href="https://imgur.com/i7SeYQV"><img src="https://i.imgur.com/i7SeYQV.png" title="source: imgur.com" /></a>
</p>
<p>
To finish I head to Azure set the DNS server of my vM to the same IP and DC-1's Private IP.  Then I restart to VM to ensure the change went through.  Next I connect the VM to our domain on DC-1.  After thats done we check DC-1 ADUC computers container to make sure the computer is visible on DC-1.  Next I will login to the VM with Jane Doe and the domain we just connected it to.  After login i head to system properties and remote desktop setting to allow domain users to access remote desktop.  Last we head to DC-1 and create said users with Powershell ISE.  
</p>
<br />
