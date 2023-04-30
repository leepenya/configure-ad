<p align="center">
<img src= "https://imgur.com/1xkHO5p.png" height="60%" width="40%" alt="AD-Logo"/>
</p>
<h1>Configuring Active Directory in the Cloud</h1>
Summary: The following is a walk-through of the key points in installing and configuring Active Directory on Microsoft's cloud platorm, Azure.<br />

<h2>Requirements</h2>

- Computer with internet connection
- Microsoft Azure account
  - Credit card to set up the account
  
 <h2>Environments & Technologies Used</h2>
 
 - Microsoft Azure (virtual machines)
 - Remote Desktop
 - Microsoft Active Directory
 - Windows command line & PowerShell
  
 <h2>Operating Systems Used</h2>
 - Windows 10 (Client-1)
</br>
 - Windows Server 2022 (DC-1)
 
  <h2>High-Level Steps</h2>
  
  1. Create a client virtual machine ("Client-1") and a domain controller virtual machine ("DC1," with a static private IP address) in a network within Azure and ensure connectivity between them.
  2. Install Active Directory ("AD") on DC1.
  3. Create an administrator account and a normal user account in AD.
  4. Join Client-1 to the domain.
  5. Set up Remote Desktop for non-administrative users on Client-1. 
  6. Create multiple additional users and log into Client-1 with one of them.
  

<h2>Specific Steps</h2>
<img src= "https://imgur.com/m3Pbgx8.png" height="80%" width="80%" alt="Topology"/>
1. First, I created a client virtual machine ("Client-1") and a domain controller virtual machine ("DC-1," with a static private IP address) in Azure and viewed the resulting network topology (see above).
</br>
</br>
<p>
<img src= "https://imgur.com/EMgJzwp.png" height="80%" width="80%" alt="ICMP-Traffic"/>
</p>
2. I then pinged from Client-1 to DC-1 to verify connectivity between them.
</br>
</br>

<p>
<img src= "https://imgur.com/dasvFlI.png" height="80%" width="80%" alt="Install-ADDS"/>
</p>
3. Next, I installed Active Directory Domain Services on DC-1.
</br>
</br>

<p>
<img src= "https://imgur.com/OD74fd3.png" height="80%" width="80%" alt="Promote-Server"/>
</p>
4. At this point, I promoted server DC-1 to a Domain Controller and set up a new forest in Active Directory.
</br>
</br>

<p>
<img src= "https://imgur.com/mTNnY5d.png" height="80%" width="80%" alt="Create-User"/>
</p>
5. I then created two organizational units (_EMPLOYEES and _ADMINS) and a user and added the user to the Domain Admins security group.
</br>
</br>

<p>
<img src= "https://imgur.com/t6KXrc4.png" height="80%" width="80%" alt="Join-Client-1"/>
</p>
6. Next, I joined Client-1 to the new domain on DC-1 by making it a member of the domain I had set up on DC-1. 
</br>
</br>

<p>
<img src= "https://imgur.com/l2099O0.png" height="80%" width="80%" alt="Client-1-ADUC"/>
</p>
7. I then verified that Client-1 showed up in Active Directory Users and Computers.  
</br>
</br>

<p>
<img src= "https://imgur.com/Ywl1n8x.png" height="80%" width="80%" alt="RDP-Non-Admin"/>
</p>
8. In this step, I set up remote access to Client-1 for non-administrative users by allowing Domain Users access to Remote Desktop. 
</br>
</br>

<p>
<img src= "https://imgur.com/3EPmIiG.png" height="80%" width="80%" alt="Create-Users"/>
</p>
8. I then logged into DC-1 as the user I had created in step 5. Using PowerShell_ISE as an administrator, I ran a script that created 500 users, assigned a password to them, and added them to the Employees organizational unit. I opened Active Directory Users and Computers (ADUC) and verified that accounts for the users created in step 8 had been created in the Employees organizational unit.
</br>
</br>

<p>
<img src= "https://imgur.com/UYUqVgZ.png" height="80%" width="80%" alt="User-Login"/>
</p>
9. Finally, I attemped to log into Client-1 with one of the accounts created in Step 8. My login attempt succeeded, as indicated above.
</br>
</br>
Thanks for checking out my Active Directory in the Cloud lab!
</br>







