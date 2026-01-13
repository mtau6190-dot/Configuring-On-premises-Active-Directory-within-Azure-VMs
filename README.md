<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
Project Summary:<br />
<br />
This project demonstrates the setup and configuration of IT infrastructure in Microsoft Azure. It includes Active Directory deployment, DNS configuration, network security, file sharing, and application installation.<br />

<h2>Environments and Technologies Used</h2>

Tutorial & Implementation Walkthrough:<br/>
- **Languages Used:** PowerShell, CMD
- **Environments:** Azure, Windows Server 2022, Windows 11
- **Technologies/Services:** Azure Virtual Machines, Remote Desktop, Network Security Groups (NSGs), DNS, File Shares, osTicket

<h2>Operating Systems Used </h2>

- Windows Server 2022 Datacenter: Azure Edition - x64 Gen2
- Windows 11 Pro (25H2) - x64 Gen2

<h2>High-Level Deployment and Configuration Steps</h2>

Step 1: Prepared AD Infrastructure in Azure Environment<br>
Step 2: Deployed Active Directory<br>
Step 3: Created Users with Powershell<br>
Step 4: Created Group Policy and Managed Accoounts<br>

<h2>Deployment and Configuration Steps</h2>

<h3>Step 1 - Prepared the Active Directory Infrastructure in Azure Environment</h3><br/>
- 1.1 - Created a Resource Group in Azure & named it "AD-Lab"
  <img width="1912" height="676" alt="image" src="https://github.com/user-attachments/assets/b662c551-3f43-49a1-928f-78d9c11913fb" />
A resource group is like a container that holds related resources (VMs, networks, storage, etc.) for a project. It is easier to organize, secure, manage, and clean up.
<br>
<br>
- 1.2 - Created a Virtual Network & Subnet
<img width="1542" height="755" alt="image" src="https://github.com/user-attachments/assets/8cb27c56-44e9-42dc-ab6d-f10e3f1c4e38" />
Created a Virtual Network (VNet) in Azure and named it "AD-VNet". It is a private network for my resources.
This Virtual Network will keep my VMs and services secure from the public internet and allows the VMs to talk to each other privately.
By creating the Virtual Network, I can define subnets, IP ranges, and apply security rules (NSGs).
My "AD‑VNet" is the foundation that connects and secures all resources in my Active Directory lab.
<br />
<br/>
- 1.3 - Created the Domain Controller VM (Windows Server 22) & named it "dc-1" & also created the Client VM (Windows 11 Pro) & named it "Client-1".<br>
dc-1 VM:
<img width="1938" height="920" alt="image" src="https://github.com/user-attachments/assets/68e2d74b-9d12-411e-a752-3f928cbe4db7" />
client-1 VM:
<img width="1949" height="936" alt="image" src="https://github.com/user-attachments/assets/ace9c816-c7a2-459b-bb64-6e8b9aa0c5ec" />
Successfully created two VMs (DC‑1 and Client‑1) in Azure gives me:<br>
Domain Controller (DC‑1): Runs Windows Server, provides Active Directory, DNS, and authentication services.<br>
Client‑1: Runs Windows 10, acts as a workstation to join and test the domain.<br>
Together, they simulate an on‑premises AD environment inside Azure, letting me practice real IT infrastructure tasks like DNS, domain joins, and security.
<br />
<br>
-1.4 - Set Domain Controller's NIC Private Address to be Static. <br>
From Dynamic to Static: <br>
<img width="735" height="867" alt="image" src="https://github.com/user-attachments/assets/6b728d0c-e5ec-40fe-862d-a34a0b8ff721" /></b>
<br>
<img width="730" height="862" alt="image" src="https://github.com/user-attachments/assets/2a83104e-ff9b-4a63-a64e-9463876d9a1b" />
<p>Successfully set DC‑1’s IP address to static so it remains fixed and reliable. A Domain Controller must always be reachable at the same address because client machines depend on it for DNS resolution and authentication. If the IP were dynamic, it could change after a restart, breaking connectivity and causing domain join failures. By making it static, I ensure stability, consistency, and proper functioning of my Active Directory environment.</p><br>
-1.5 - Copied "dc-1"s Public IP Address, then logged into "dc-1" via Remote Desktop, and disabled the windows Firewall for testing connectivity.<br>
<img width="1915" height="796" alt="image" src="https://github.com/user-attachments/assets/55886a9b-0974-40a0-804e-bb0ca7129def" />
<img width="1112" height="647" alt="image" src="https://github.com/user-attachments/assets/46df8be8-17b1-4b9f-bbab-a72cbe91ca70" /><br>
I used DC‑1’s public IP to connect via Remote Desktop so I could access the server. Once inside, I disabled the Windows Firewall temporarily to ensure that network traffic (like ping and DNS requests) could pass through without being blocked. This step is only for testing connectivity between my VMs; later, the firewall should be re‑enabled with proper rules for security.
<br>
<br>
-1.6 - I then set "client-1"s DNS Settings to "dc-1"s private IP Address. Then Logged into "client-1" via remote desktop connection, and then ping dc-1s private IP Address to ensure ping succeeded.<br>
<img width="895" height="766" alt="image" src="https://github.com/user-attachments/assets/aae7f01b-295f-48a3-8fe8-e63049b996c5" />

<img width="1600" height="687" alt="image" src="https://github.com/user-attachments/assets/a9a4af3b-45dd-4855-837a-5aeb5629c1a5" /><br>

<img width="936" height="776" alt="image" src="https://github.com/user-attachments/assets/490907a8-f9d1-476c-a7b7-0690d70ca14e" /><br>
Successfully configured Client‑1’s DNS to point to DC‑1’s private IP, ensuring it uses the Domain Controller for name resolution. After logging into Client‑1 via RDP, I tested connectivity by pinging DC‑1’s private IP. The successful ping confirmed that both VMs are on the same network, DNS is correctly set, and Client‑1 can reliably communicate with DC‑1.<br>

-1.7 - From client-1, I ran the command "ipconfig /all" to check and confirm that client-1s dns is dc-1s private IP Address. Therefore,making this Active Directory preparation a success.
<img width="951" height="866" alt="image" src="https://github.com/user-attachments/assets/fd4bc315-717f-4bc9-ac53-901fdf51aac3" /><br>
<P>Running ipconfig /all on Client‑1 allowed me to view its full network configuration, including the DNS server settings. By confirming that Client‑1’s DNS points to DC‑1’s private IP address, I verified that the client is correctly configured to use the Domain Controller for name resolution. This successful check, combined with the earlier ping test, proves that the network setup and DNS integration are working as intended, completing the Active Directory preparation phase successfully.</P>

<h3>Step 2 - Deployed Active Directory</h3>
<h4>PART 1</h4>

-2.1 - Installed Active Directory in "dc-1". This VM serves as the Windows Server 2022 and then promoted the Server as the Domain Controller (DC): Set up a new forest as "mydomain.com". Restarted and logged back in as: "mydomain.com\labUser"
<img width="1309" height="896" alt="image" src="https://github.com/user-attachments/assets/c3cf7247-33da-4d3a-9265-13643f04686c" />
<img width="923" height="712" alt="image" src="https://github.com/user-attachments/assets/c2342f01-683c-47af-bd9a-19b32b0707f0" />
<p>I installed Active Directory on DC‑1 (Windows Server 2022) and promoted it to a Domain Controller by creating a new forest called mydomain.com. This established the domain structure and centralized authentication. After the server restarted, I logged in using the domain account mydomain.com\labUser, confirming that the domain was successfully created and functional.</p>

<br>
-2.2 - Created an Admin & Normal User Account in Active Directory Users & Computers(ADUC).<br>
<img width="831" height="572" alt="image" src="https://github.com/user-attachments/assets/fe78d843-fd9e-4768-9013-a4d131a88f0d" />
<img width="890" height="643" alt="image" src="https://github.com/user-attachments/assets/246bff58-b55f-47bc-800f-6a9e50b7c0ea" />
<img width="615" height="523" alt="image" src="https://github.com/user-attachments/assets/9c5aa835-610a-4d3e-9ea4-6468d0a30f61" />
<img width="567" height="693" alt="image" src="https://github.com/user-attachments/assets/3f59c76c-565e-4f52-95c6-d864d380bd02" />

<P>I organized Active Directory by creating two OUs: _EMPLOYEES and _ADMINS. Then I added a new user, Reece Walsh with the username reece_admin, and elevated them by adding to the Domain Admins group. Finally, I logged back into DC‑1 using mydomain.com\reece_admin, confirming the account’s admin privileges and making it the primary account for your project.</P>


-2.3 - Joined Client-1 to my domain (mydomain.com).
<img width="940" height="841" alt="image" src="https://github.com/user-attachments/assets/a54c0f0d-82b7-4273-a465-6df2f736094a" />
<img width="400" height="247" alt="image" src="https://github.com/user-attachments/assets/81a1b061-6bc0-4ea5-922e-87d2747cf3b4" />
<img width="957" height="938" alt="image" src="https://github.com/user-attachments/assets/f38985c4-208e-48d9-b738-1317880201df" />
<img width="942" height="467" alt="image" src="https://github.com/user-attachments/assets/bbc21f21-d8dc-47d6-8e04-05d274f003a4" />
<p>I joined Client‑1 to the domain by logging in as the local admin and connecting it to mydomain.com, which required a restart. Back on DC‑1, I confirmed Client‑1 appeared in Active Directory Users and Computers (ADUC), proving the join was successful. Finally, I created a new OU called _CLIENTS and moved Client‑1 into it, organizing domain resources for easier management.</p>

<h3>Step 3 - Created Users with Powershell</h3>
<h4>PART 2</h4>
-2.4 - Setup Remote Desktop for Non-Administrative Users on Client-1(Windows 11).
<img width="952" height="872" alt="image" src="https://github.com/user-attachments/assets/3f0fd3c3-02e9-4fb0-908e-bf2fcc01ba00" />
<p>I enabled Remote Desktop access for domain users on Client‑1 so that non‑administrative accounts can log in remotely. This ensures regular employees can connect to the workstation through the domain, supporting centralized access and testing Active Directory functionality beyond just admin accounts.</p>
<br>
<br>
-3.1 - Created additional users and attempted to log into "client-1" with one of the users.
<img width="957" height="911" alt="UsersCreated" src="https://github.com/user-attachments/assets/bdea4236-03ac-4d67-813e-b3703ea9f945" />
<img width="777" height="582" alt="image" src="https://github.com/user-attachments/assets/0a5e40c8-bbd0-46a0-8ef5-8484c5ac381a" />
<img width="563" height="693" alt="image" src="https://github.com/user-attachments/assets/4802fb87-beaa-466e-ae51-c4a4ef95fc54" />
<img width="772" height="580" alt="image" src="https://github.com/user-attachments/assets/411cd525-c14c-4414-90ac-6f38f47c6d24" />

<p>I ran the PowerShell script on DC‑1 to automate user account creation and place them in the _EMPLOYEES OU, ensuring consistency and efficiency in managing accounts. Tested a login on Client‑1 with one of those accounts verified that domain authentication works correctly, proving the accounts were active and integrated into the domain environment.In the second image, you can see that I'm in the Active Directory Users & Computers, and in the _EMPLOYEES group, you can see the users created. Finally, I randomly picked a user to log into client-1 as a user for that account and it was a success.</p>

<h3>Step 4 - Group Policy & Managing Accounts</h3>
-4.1 -Dealing with Account Lockouts
<img width="1186" height="689" alt="image" src="https://github.com/user-attachments/assets/4ed190b2-36f5-42a8-8ee2-db15230785d9" />
<p>My test showed that even after multiple failed logins, the account was still accessible once the correct password was entered. This means the Account Lockout Policy is not configured in Active Directory. Without this policy, repeated failed attempts don’t trigger a lockout, leaving accounts vulnerable to brute‑force attacks. Configuring it enforces security by locking accounts after a set number of failed attempts.</p><br>

-4.2 -Configured the domain account Lockout Policy
<img width="1463" height="852" alt="image" src="https://github.com/user-attachments/assets/f7ac6521-8fdd-4fc4-8fe0-0b96d9bf7dbf" />
<img width="681" height="170" alt="image" src="https://github.com/user-attachments/assets/d783ea34-fb05-46d7-8b5f-ccdc511d8a2e" />

<p>I logged into DC‑1 and used the Group Policy Management Console to edit the default domain policy. By navigating to the Account Policy settings, I configured the Account Lockout Policy. This ensures that after a set number of failed login attempts, user accounts will be locked, protecting the domain against brute‑force attacks and strengthening overall security.
I configured the Account Lockout Policy with these settings:

Lockout Duration: 10 minutes → accounts remain locked for 10 minutes before unlocking.

Threshold: 5 invalid attempts → after 5 failed logins, the account is locked.

Administrator lockout enabled → even admin accounts can be locked, increasing security.

Reset counter after 10 minutes → if fewer than 5 failed attempts occur, the counter resets after 10 minutes.

Together, these settings protect against brute‑force attacks while allowing accounts to recover automatically after a short period.</p><br>

-4.3 -Updated the Group Policy by using CMD:
<img width="907" height="502" alt="image" src="https://github.com/user-attachments/assets/767f3778-abcc-4abf-9996-95aeed19fe02" />
<p>I ran gpupdate /force on Client‑1 to immediately apply the updated Group Policy settings from the domain. This ensures that the Account Lockout Policy and any other changes made on DC‑1 are enforced without waiting for the next automatic refresh. It’s a crucial step to validate that my security configurations are active and working as intended.</p>








