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
 
<h4>1.1 - Created a Resource Group in Azure & named it "AD-Lab"</h4>
  <p>Azure Portal -> Click "Resource Groups"</p>
  <img width="1908" height="353" alt="image" src="https://github.com/user-attachments/assets/74542719-c1c0-4cf2-8b90-8439a27972c1" />
  
  <p>Click "Create"</p>
  <img width="1919" height="800" alt="image" src="https://github.com/user-attachments/assets/4ccbc846-814c-4e27-9190-5c6c2caa8021" /><br>
  <br>
  
  <p>Resource Group name "AD-Lab" -> Select region "Southeast Asia" -> Click Review + Create</p>
  <img width="1075" height="871" alt="image" src="https://github.com/user-attachments/assets/049acc0b-9206-4dce-95d2-716b8d550722" />
  <br>
  
  <p>The filled out form -> Click Create</p>
  <img width="721" height="867" alt="image" src="https://github.com/user-attachments/assets/4250750c-dd45-44bc-8841-a869959bc1d0" />
  <br>
  <br>
  Successfully Created a Resource Group. 
  <img width="1912" height="676" alt="image" src="https://github.com/user-attachments/assets/b662c551-3f43-49a1-928f-78d9c11913fb" />
  <h4>SUMMARY</h4>
  A resource group is like a container that holds related resources (VMs, networks, storage, etc.) for a project. It is easier to organize, secure, manage, and clean up.
<br>
<br>

<h4>1.2 - Created a Virtual Network & Subnet</h4>
<p>Azure Portal -> Click "Virtual Networks"</p> 
<img width="1383" height="306" alt="image" src="https://github.com/user-attachments/assets/786bc252-e11b-4c7b-833a-3965b35e9997" />
 
<p>Click "Create"</p> 
<img width="1944" height="600" alt="image" src="https://github.com/user-attachments/assets/1cc4a79d-55af-4736-bb42-51964a745caf" />

<p>Virtual Network name "AD-VNet" -> Resource Group Name Select "AD-Lab" Region "Southeast Asia" -> Click Review + Create</p>
<img width="1030" height="867" alt="image" src="https://github.com/user-attachments/assets/51b4964a-848c-4e90-b4dc-4b25d4a89624" />

<p>The filled out form -> Click Create</p>  
<img width="768" height="903" alt="image" src="https://github.com/user-attachments/assets/d9cf1f97-ce22-4f7a-b3e2-7c05fa7b6669" />

<p>Created a Virtual Network (VNet) in Azure and named it "AD-VNet". It is a private network for my resources.</p>
<img width="1541" height="711" alt="image" src="https://github.com/user-attachments/assets/de7331a5-f9be-4794-ae2f-62c078dfde2b" />

<h4>SUMMARY</h4>
<p>This Virtual Network will keep my VMs and services secure from the public internet and allows the VMs to talk to each other privately.
By creating the Virtual Network, I can define subnets, IP ranges, and apply security rules (NSGs).
My "AD‑VNet" is the foundation that connects and secures all resources in my Active Directory lab.</p>
<br>

<h4>1.3 - Created Two  VMs: Windows Server 22 VM as the Domain Controller & Windows 11 VM as the Client</h4>

<p>Azure Portal -> Click "Virtual Machines"</p> 
<img width="1397" height="340" alt="image" src="https://github.com/user-attachments/assets/0c2675a7-65c5-405e-9587-15a71fcba573" />
<br>
<p>Click "Create"</p> 
<img width="1926" height="591" alt="image" src="https://github.com/user-attachments/assets/74b2ce61-7836-4395-afb4-61d98e274d35" />
<br>

<p>Click Virtual Machine</p>
<img width="632" height="680" alt="image" src="https://github.com/user-attachments/assets/b787bf03-4629-4f9c-8410-6b5dc98e5a8f" />
<br>
<br>
<p>Resource name "AD-Lab" -> Virtual Name "dc-1" -> Region "Southeast Asia"</p>
<img width="1056" height="812" alt="image" src="https://github.com/user-attachments/assets/0082c148-6d01-4a38-8011-6d18e7c05755" />
<br>
<p>Select Image "Windows Server 2022"</p>
<img width="992" height="646" alt="image" src="https://github.com/user-attachments/assets/7ccebfb0-77c6-49d5-bff7-617e9eff98af" />
<br>
<p>Enter Username -> Set Password & Confirm -> Check the Box to confirm -> Click "Next"</p>
<img width="1085" height="764" alt="image" src="https://github.com/user-attachments/assets/8377a6e5-de9f-49cc-a0d1-a75017f8bbec" />
<img width="688" height="275" alt="image" src="https://github.com/user-attachments/assets/f2b0b8b3-615c-4aac-8c2f-766e39a0805e" />
<br>

<p>Virtual Network Select "AD-VNet" -> Click Review + Create</p>
<img width="1065" height="731" alt="image" src="https://github.com/user-attachments/assets/5fa7821c-bc2c-4638-9e9f-cf593c94fd86" />
<br>

<p>Validation Passed -> Now Click "Create"</p>
<img width="1030" height="841" alt="image" src="https://github.com/user-attachments/assets/da33c23a-6c60-40e7-8574-16e6dfab0bcb" />
<br>
<br>

<p>Windows Server VM (dc-1) Successfully Created</p>
<img width="1938" height="920" alt="image" src="https://github.com/user-attachments/assets/68e2d74b-9d12-411e-a752-3f928cbe4db7" />

<p>This VM is the foundation. By configuring dc‑1 as the domain controller, I establish the central authority for authentication and resource management. All other machines in the lab (like client PCs or member servers) will join the domain controlled by dc‑1.</p>

<p>Azure Portal -> Click "Virtual Machines"</p> 
<img width="1419" height="353" alt="image" src="https://github.com/user-attachments/assets/0571a318-5de5-4763-a30f-c210838a88c0" />

<p>Click "Create"</p> 
<img width="1956" height="642" alt="image" src="https://github.com/user-attachments/assets/2c92177b-3b5d-495b-87f4-353f65bc4da6" />

<p>Click Virtual Machine</p>
<img width="453" height="644" alt="image" src="https://github.com/user-attachments/assets/d562a27e-75c2-4406-9f3f-464253612db2" />

<p>Resource name "AD-Lab" -> Virtual Name "client-1" -> Region "Southeast Asia"</p>
<img width="1043" height="785" alt="image" src="https://github.com/user-attachments/assets/26b4c0ac-12fc-41a0-b3b9-50d10411ecf0" />
<br>
<p>Select Image "Windows 11 Pro" -> Enter Username -> Set Password & Confirm -> </p>
<img width="995" height="660" alt="image" src="https://github.com/user-attachments/assets/b799bff7-20c6-4cf8-ae82-d4a498419cac" />

<p>Check the Box to confirm -> Click "Next"</p>
<img width="631" height="303" alt="image" src="https://github.com/user-attachments/assets/797582a8-9ecb-4d93-9945-2ff113377d3d" />

<p>Virtual Network Select "AD-VNet" -> Click Review + Create</p>
<img width="1009" height="732" alt="image" src="https://github.com/user-attachments/assets/923c1284-0e28-434b-b9c4-ab3c3a6e8ae2" />

<p>Validation Passed -> Now Click "Create"</p>
<img width="979" height="842" alt="image" src="https://github.com/user-attachments/assets/f4c45c00-916e-415b-9000-a9ee53401dca" />
<br>
<br>
<p>Windows 11 VM (client-1) Successfully Created</p>
<img width="1949" height="936" alt="image" src="https://github.com/user-attachments/assets/ace9c816-c7a2-459b-bb64-6e8b9aa0c5ec" />

<h4>SUMMARY</h4>
Successfully created two VMs (DC‑1 and Client‑1) in Azure gives me:<br>
Domain Controller (DC‑1): Runs Windows Server, provides Active Directory, DNS, and authentication services.<br>
Client‑1: Runs Windows 10, acts as a workstation to join and test the domain.<br>
Together, they simulate an on‑premises AD environment inside Azure, letting me practice real IT infrastructure tasks like DNS, domain joins, and security.
<br />
<br>

<h4>1.4 - Set Domain Controller's NIC Private Address to be Static. <br></h4>

<p>Azure Portal -> Click "Virtual Machines -> Click on "dc-1" VM</p>
<img width="1919" height="712" alt="image" src="https://github.com/user-attachments/assets/a718b0fe-a000-4e21-bebb-ccea66019f93" />

<p>Click on "Netwroking" -> Click "Network Settings" -> Click on "Network Interface/IP Configuration</p>
<img width="1231" height="861" alt="image" src="https://github.com/user-attachments/assets/f3810bdb-3500-49ec-9d48-e119721f5126" />

<p>Click Settings -> Click IP Configurations -> Click ipconfig1</p>
<img width="1454" height="775" alt="image" src="https://github.com/user-attachments/assets/bda9a803-8afd-4b90-a756-88337d2b3589" />
<br>
<br>
<p>Uncheck Dynamic</p> 
<img width="753" height="886" alt="image" src="https://github.com/user-attachments/assets/fcb84c9e-a0a0-4717-bd12-151489ce6345" />
<br>
<p>Check Static -> Click "Save"</p> 
<img width="723" height="889" alt="image" src="https://github.com/user-attachments/assets/d27aaa44-3033-4822-b370-acbfbf6057f9" />
<br>
<p>Successfully set DC‑1’s IP address to static so it remains fixed and reliable.</p>
<img width="1451" height="764" alt="image" src="https://github.com/user-attachments/assets/ebd624c4-8f7c-427d-a538-9893ee037083" />


<h4>SUMMARY</h4>
<p>A Domain Controller must always be reachable at the same address because client machines depend on it for DNS resolution and authentication. If the IP were dynamic, it could change after a restart, breaking connectivity and causing domain join failures. By making it static, I ensure stability, consistency, and proper functioning of my Active Directory environment.</p><br>

<h4>1.5 - Temporarily disabled the windows Firewall for testing connectivity.<br></h4>

<p>Azure Portal -> Click Virtual Machines -> Copied "dc-1s" Public IP Address</p>
<img width="1966" height="648" alt="image" src="https://github.com/user-attachments/assets/8d8fbfd3-a8a4-48fd-8e55-e7d505666fbe" />
<br>
<p>Click Windows + R -> Click "Ok" to Open Remote Desktop Connection</p>
<img width="467" height="281" alt="image" src="https://github.com/user-attachments/assets/42fb5d06-22f1-4ce1-b18d-a8a0a663baec" />
<br>
<p>Paste the IP Address for "dc-1" -> Click "Connect"</p>
<img width="1462" height="538" alt="image" src="https://github.com/user-attachments/assets/68ddb3a1-bc07-433e-aca2-4fe57fdcc084" />
<br>
<p>Enter Credentials ->Click "ok"</p>
<img width="583" height="499" alt="image" src="https://github.com/user-attachments/assets/921799fc-8fe1-4db7-8d28-9978a6f5d74f" />
<br>
<p>Click "Yes"</p>
<img width="525" height="497" alt="image" src="https://github.com/user-attachments/assets/a7c926f7-3300-4e66-bf83-34c8a2b13169" />
<br>

<p>In the "dc-1" VM ->Go to Start Button -> Search + Click "Windows Defender Firewall with Advanced Security</p>
<img width="958" height="1021" alt="image" src="https://github.com/user-attachments/assets/36638c88-ef45-4369-ae5c-1f242096814b" />
<br>
<p>Click "Windows Defender Firewall Properties</p>
<img width="1222" height="717" alt="image" src="https://github.com/user-attachments/assets/374079c2-ae80-4a63-b7ac-c8a2cad53fab" />
<br>
<p>Click Domain Profile -> Click "off"</p>
<img width="1013" height="529" alt="image" src="https://github.com/user-attachments/assets/44fe5354-904b-4b68-93eb-8822951ccb35" />
<br>
<p>Click Private Profile -> Click "off"</p>
<img width="1015" height="549" alt="image" src="https://github.com/user-attachments/assets/d7b6b04c-39c8-4421-a5ed-e46dce9a489d" />
<br>
<p>Click Public Profile -> Click "off" ->Click "Apply" ->CLick "ok"</p>
<img width="507" height="620" alt="image" src="https://github.com/user-attachments/assets/c7969600-2527-44f9-a300-3a5f727dc8f6" />
<br>
<img width="1127" height="682" alt="image" src="https://github.com/user-attachments/assets/0604473a-ab97-4bba-b42b-69870371339a" />
<br>
<h4>SUMMARY</h4>
<p>Successfully disabled the Windows Firewall temporarily to ensure that network traffic (like ping and DNS requests) could pass through without being blocked. This step is only for testing connectivity between my VMs; later, the firewall should be re‑enabled with proper rules for security.</p>
<br>
<br>

<h4>1.6 - Set "client-1"s DNS Settings to "dc-1"s private IP Address</h4>
<p>Azure Portal -> Click on "Virtual Machines" -> Click "client-1" VM</p>
<img width="1911" height="675" alt="image" src="https://github.com/user-attachments/assets/66d7476f-c4e7-4aaf-882c-862a9351f241" />
<br>
<p>Click "Networking" -> Click "Network Settings" -> Click "Network Interface/IP Configurations </p>
<img width="1187" height="856" alt="image" src="https://github.com/user-attachments/assets/182f2668-fae0-437a-8317-a56505ec6d42" />
<br>
<p>Click "Settings" -> Click "DNS Servers" -> Ckeck "Customs" -> Enter "dc-1"s Private IP Address ->Click "Save"</p>
<img width="1640" height="828" alt="image" src="https://github.com/user-attachments/assets/c3fff6ca-1355-4b54-96fc-4f162d738b90" />
<br>
<p>Successfully saved DNS settings for network interface 'client-1'.</p>
<img width="578" height="256" alt="image" src="https://github.com/user-attachments/assets/747f87f6-d160-46b0-958e-d0f2f17b4a36" />
<br>

<h4>1.7 Client-1 Test Connectivity by Pinging DC-1s Private IP</h4>
<p>Azure Portal -> Click "Virtual Machines" -> Copied "Client-1"s Public IP Address</p>
<img width="1999" height="811" alt="image" src="https://github.com/user-attachments/assets/6966f844-0aa3-4bea-a8ac-0e8673c1d01f" />
<br>
<p>Click Windows + R -> Click "Ok" to open Remote Desktop Connection</p>
<img width="462" height="279" alt="image" src="https://github.com/user-attachments/assets/d9368a95-8965-4bef-bd68-5194fafa48c9" />
<br>
<p>Paste "client-1"s IP Address -> Click "ok" -> Enter Credentials -> Click "ok"</p>
<img width="1162" height="497" alt="image" src="https://github.com/user-attachments/assets/dba0070a-2e3e-4e86-a4c2-b781b8b4b78c" />
<br>

<p>Click "Yes" -> </p>
<img width="522" height="496" alt="image" src="https://github.com/user-attachments/assets/d98e7997-11a7-420d-8ccc-d4bbd078d664" />
<br>

<p>Click on "Start Button" -> Type in "cmd" -> </p>




<h4>SUMMARY</h4>
<p>Successfully configured Client‑1’s DNS to point to DC‑1’s private IP, ensuring it uses the Domain Controller for name resolution.</p>

<h4>1.8 - From client-1, I ran the command "ipconfig /all" to check and confirm that client-1s dns is dc-1s private IP Address. Therefore,making this Active Directory preparation a success.</h4>

<img width="951" height="866" alt="image" src="https://github.com/user-attachments/assets/fd4bc315-717f-4bc9-ac53-901fdf51aac3" /><br>
<P>Running ipconfig /all on Client‑1 allowed me to view its full network configuration, including the DNS server settings. By confirming that Client‑1’s DNS points to DC‑1’s private IP address, I verified that the client is correctly configured to use the Domain Controller for name resolution. This successful check, combined with the earlier ping test, proves that the network setup and DNS integration are working as intended, completing the Active Directory preparation phase successfully.</P>

<h3>Step 2 - Deployed Active Directory</h3>
<h4>PART 1</h4>

<h4>2.1 - Installed Active Directory in "dc-1". This VM serves as the Windows Server 2022 and then promoted the Server as the Domain Controller (DC): Set up a new forest as "mydomain.com". Restarted and logged back in as: "mydomain.com\labUser"</h4>

<img width="1309" height="896" alt="image" src="https://github.com/user-attachments/assets/c3cf7247-33da-4d3a-9265-13643f04686c" />
<img width="923" height="712" alt="image" src="https://github.com/user-attachments/assets/c2342f01-683c-47af-bd9a-19b32b0707f0" />
<p>I installed Active Directory on DC‑1 (Windows Server 2022) and promoted it to a Domain Controller by creating a new forest called mydomain.com. This established the domain structure and centralized authentication. After the server restarted, I logged in using the domain account mydomain.com\labUser, confirming that the domain was successfully created and functional.</p>

<br>
<h4>2.2 - Created an Admin & Normal User Account in Active Directory Users & Computers(ADUC).<br></h4>
<img width="831" height="572" alt="image" src="https://github.com/user-attachments/assets/fe78d843-fd9e-4768-9013-a4d131a88f0d" />
<img width="890" height="643" alt="image" src="https://github.com/user-attachments/assets/246bff58-b55f-47bc-800f-6a9e50b7c0ea" />
<img width="615" height="523" alt="image" src="https://github.com/user-attachments/assets/9c5aa835-610a-4d3e-9ea4-6468d0a30f61" />
<img width="567" height="693" alt="image" src="https://github.com/user-attachments/assets/3f59c76c-565e-4f52-95c6-d864d380bd02" />

<P>I organized Active Directory by creating two OUs: _EMPLOYEES and _ADMINS. Then I added a new user, Reece Walsh with the username reece_admin, and elevated them by adding to the Domain Admins group. Finally, I logged back into DC‑1 using mydomain.com\reece_admin, confirming the account’s admin privileges and making it the primary account for your project.</P>


<h4>2.3 - Joined Client-1 to my domain (mydomain.com).</h4>
<img width="940" height="841" alt="image" src="https://github.com/user-attachments/assets/a54c0f0d-82b7-4273-a465-6df2f736094a" />
<img width="400" height="247" alt="image" src="https://github.com/user-attachments/assets/81a1b061-6bc0-4ea5-922e-87d2747cf3b4" />
<img width="957" height="938" alt="image" src="https://github.com/user-attachments/assets/f38985c4-208e-48d9-b738-1317880201df" />
<img width="942" height="467" alt="image" src="https://github.com/user-attachments/assets/bbc21f21-d8dc-47d6-8e04-05d274f003a4" />
<p>I joined Client‑1 to the domain by logging in as the local admin and connecting it to mydomain.com, which required a restart. Back on DC‑1, I confirmed Client‑1 appeared in Active Directory Users and Computers (ADUC), proving the join was successful. Finally, I created a new OU called _CLIENTS and moved Client‑1 into it, organizing domain resources for easier management.</p>

<h3>Step 3 - Created Users with Powershell</h3>
<h3>PART 2</h3>
<h4>3.1 - Setup Remote Desktop for Non-Administrative Users on Client-1(Windows 11).</h4>

<img width="952" height="872" alt="image" src="https://github.com/user-attachments/assets/3f0fd3c3-02e9-4fb0-908e-bf2fcc01ba00" />
<p>I enabled Remote Desktop access for domain users on Client‑1 so that non‑administrative accounts can log in remotely. This ensures regular employees can connect to the workstation through the domain, supporting centralized access and testing Active Directory functionality beyond just admin accounts.</p>
<br>
<br>
<h4>3.2 - Created additional users and attempted to log into "client-1" with one of the users.</h4>
<img width="957" height="911" alt="UsersCreated" src="https://github.com/user-attachments/assets/bdea4236-03ac-4d67-813e-b3703ea9f945" />
<img width="777" height="582" alt="image" src="https://github.com/user-attachments/assets/0a5e40c8-bbd0-46a0-8ef5-8484c5ac381a" />
<img width="563" height="693" alt="image" src="https://github.com/user-attachments/assets/4802fb87-beaa-466e-ae51-c4a4ef95fc54" />
<img width="772" height="580" alt="image" src="https://github.com/user-attachments/assets/411cd525-c14c-4414-90ac-6f38f47c6d24" />

<p>I ran the PowerShell script on DC‑1 to automate user account creation and place them in the _EMPLOYEES OU, ensuring consistency and efficiency in managing accounts. Tested a login on Client‑1 with one of those accounts verified that domain authentication works correctly, proving the accounts were active and integrated into the domain environment.In the second image, you can see that I'm in the Active Directory Users & Computers, and in the _EMPLOYEES group, you can see the users created. Finally, I randomly picked a user to log into client-1 as a user for that account and it was a success.</p>

<h3>Step 4 - Group Policy & Managing Accounts</h3>
<h4>4.1 -Dealing with Account Lockouts</h4>

<img width="1186" height="689" alt="image" src="https://github.com/user-attachments/assets/4ed190b2-36f5-42a8-8ee2-db15230785d9" />
<p>My test showed that even after multiple failed logins, the account was still accessible once the correct password was entered. This means the Account Lockout Policy is not configured in Active Directory. Without this policy, repeated failed attempts don’t trigger a lockout, leaving accounts vulnerable to brute‑force attacks. Configuring it enforces security by locking accounts after a set number of failed attempts.</p><br>

<h4>4.2 -Configured the domain account Lockout Policy</h4>
<img width="1463" height="852" alt="image" src="https://github.com/user-attachments/assets/f7ac6521-8fdd-4fc4-8fe0-0b96d9bf7dbf" />
<img width="681" height="170" alt="image" src="https://github.com/user-attachments/assets/d783ea34-fb05-46d7-8b5f-ccdc511d8a2e" />

<p>I logged into DC‑1 and used the Group Policy Management Console to edit the default domain policy. By navigating to the Account Policy settings, I configured the Account Lockout Policy. This ensures that after a set number of failed login attempts, user accounts will be locked, protecting the domain against brute‑force attacks and strengthening overall security.
I configured the Account Lockout Policy with these settings:

Lockout Duration: 10 minutes → accounts remain locked for 10 minutes before unlocking.

Threshold: 5 invalid attempts → after 5 failed logins, the account is locked.

Administrator lockout enabled → even admin accounts can be locked, increasing security.

Reset counter after 10 minutes → if fewer than 5 failed attempts occur, the counter resets after 10 minutes.

Together, these settings protect against brute‑force attacks while allowing accounts to recover automatically after a short period.</p><br>

<h4>4.3 -Updated the Group Policy by using CMD:</h4>
<img width="907" height="502" alt="image" src="https://github.com/user-attachments/assets/767f3778-abcc-4abf-9996-95aeed19fe02" />
<p>I ran gpupdate /force on Client‑1 to immediately apply the updated Group Policy settings from the domain. This ensures that the Account Lockout Policy and any other changes made on DC‑1 are enforced without waiting for the next automatic refresh. It’s a crucial step to validate that my security configurations are active and working as intended.</p>
<img width="661" height="721" alt="image" src="https://github.com/user-attachments/assets/7418581d-dbcc-4781-813f-ae16f485c338" />

<p>I ran gpresult /r on DC‑1 to confirm that Group Policy settings—like the Account Lockout Policy—were successfully applied to the user reece_admin. The output shows that the policy was pulled from dc-1.mydomain.com, and the user is located in the _ADMINS OU, verifying that my Group Policy configuration is active and targeting the correct domain objects. This confirms my domain’s security policies are now enforced.</p>

<h4>4.4 -Enabled & Disabled Accounts</h4>
<img width="696" height="180" alt="image" src="https://github.com/user-attachments/assets/f1563217-ab66-4738-b211-e0414003e163" />
<p>My test confirmed that the Account Lockout Policy is now active. After multiple failed login attempts using the rosaf.nada account, Remote Desktop displayed a lockout warning, preventing access. This proves that the Group Policy settings—especially the lockout threshold and duration—are successfully enforced across the domain, strengthening security against unauthorized access.</p>
<img width="505" height="670" alt="image" src="https://github.com/user-attachments/assets/a4727e56-0ada-4566-bb31-bab3cef124dc" />

I unlocked the rosaf.nada account in Active Directory after it was locked due to too many failed login attempts. This confirms that my Account Lockout Policy is functioning correctly, and that I—as a domain admin—can manually restore access when needed. It’s a key part of managing user security and ensuring controlled recovery from lockouts.<br>







