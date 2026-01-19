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

<h4>SUMMARY</h4>
<p>Successfully configured Client‑1’s DNS to point to DC‑1’s private IP, ensuring it uses the Domain Controller for name resolution.</p>

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

<p>Click on "Start Button" -> Type in "cmd" ->Click "cmd" to open</p>
<img width="971" height="903" alt="image" src="https://github.com/user-attachments/assets/792fa6f9-7d0e-4b08-ae8d-08e0aad4a64b" />
<br>

<p>Type "ping 10.0.0.4" ->Click "enter"</p>
<img width="831" height="906" alt="image" src="https://github.com/user-attachments/assets/53a758d2-45cf-44b4-a1c4-2b9e6fdbae55" />

<h4>SUMMARY</h4>
<P>This confirms that Client‑1 can reach DC‑1 over the private Azure network. By pinging DC‑1’s private IP (10.0.0.4), we verify network connectivity between the client and the domain controller. This is critical because Active Directory requires reliable communication with the domain controller for authentication, DNS resolution, and domain join operations. A successful ping ensures the environment is correctly configured and ready for domain integration.</P>
<br>

<h4>1.8 Further confirmation by running the ipconfig /all on "client-1" VM.</h4>

<P>Restart Client-1 in the Azure Portal</P>
<img width="1752" height="642" alt="image" src="https://github.com/user-attachments/assets/809097c8-87c3-4135-abd1-2a08a4bd9c5d" />
<img width="593" height="131" alt="image" src="https://github.com/user-attachments/assets/90673a42-c733-47f1-9723-02d0d87a8b20" />
<br>
<p>Click Windows + R -> Click "Ok" to open Remote Desktop Connection</p>
<img width="462" height="279" alt="image" src="https://github.com/user-attachments/assets/d9368a95-8965-4bef-bd68-5194fafa48c9" />
<br>
<p>Paste "client-1"s IP Address -> Click "ok" -> Enter Credentials -> Click "ok"</p>
<img width="1162" height="497" alt="image" src="https://github.com/user-attachments/assets/dba0070a-2e3e-4e86-a4c2-b781b8b4b78c" />
<br>
<p>On "client-1" -> Go to start button -> type in "cmd" -> Click on "cmd"</p>
<img width="813" height="850" alt="image" src="https://github.com/user-attachments/assets/a7a917cb-b90b-4c8d-857b-a4929a6c0988" />
<br>
<p>Type ipconfig /all -> Click "enter"</p>
<img width="1478" height="797" alt="image" src="https://github.com/user-attachments/assets/d9ec0da9-b444-4c78-9650-39f79b9ecfc4" />

<P>Running ipconfig /all on Client‑1 allowed me to view its full network configuration, including the DNS server settings. By confirming that Client‑1’s DNS points to DC‑1’s private IP address, I verified that the client is correctly configured to use the Domain Controller for name resolution. This successful check, combined with the earlier ping test, proves that the network setup and DNS integration are working as intended, completing the Active Directory preparation phase successfully.</P>

<h3>Step 2 - Deployed Active Directory</h3>

<h4>2.1 - Installed Active Directory in "dc-1" (Windows Server 2022)</h4>
<P>Logged into "dc-1" as the Domain Controller-> Open the Server Manager -> CLick "Add Roles & Features under "Configure this local Server".</P>
<img width="1440" height="749" alt="image" src="https://github.com/user-attachments/assets/a2004327-4675-4316-a6f3-0934b4585669" />
<br>
<p>Select "Role-Based or Feature-Based Installation -> Click "Next"</p>
<img width="1004" height="704" alt="image" src="https://github.com/user-attachments/assets/5a6d45db-a391-4734-91ad-bf184f31f730" />
<br>
<p>Select "Select a server for the server pool<-> Click "Next"/p>
<img width="988" height="708" alt="image" src="https://github.com/user-attachments/assets/9c020867-47c1-4dae-ab13-ac800b606d3b" />
<br>
<p>Click "Active Directory Domain Services -> Click "Add Features" ->Click "Next"</p>
<img width="1278" height="656" alt="image" src="https://github.com/user-attachments/assets/26726537-1806-4391-bc41-cb139b108a96" />
<br>
<p>Click "Next</p>
<img width="991" height="702" alt="image" src="https://github.com/user-attachments/assets/c77857d9-e9a7-4427-a466-ddadd859c86e" />
<br>
<p>Click "Next"</p>
<img width="985" height="706" alt="image" src="https://github.com/user-attachments/assets/15a54590-5e93-4ec3-8045-cdce800a97af" />
<br>
<p>Check "Restart the destination server checkbox" -> Click "Yes" ->Click "Install" </p>
<img width="1192" height="717" alt="image" src="https://github.com/user-attachments/assets/f525a457-731b-4eb2-91f4-b86e31cb5fda" />
<br>
<p>Wait for the Installation Progress ->Click "Close"</p>
<img width="978" height="697" alt="image" src="https://github.com/user-attachments/assets/fde6cb33-3d39-4446-bcc3-f866a9dbf25e" />
<img width="982" height="708" alt="image" src="https://github.com/user-attachments/assets/d1617ce8-c704-402c-a30f-3780b3a3250c" />
<br>
<h4>SUMMARY</h4>
<p>Installed Active Directory Domain Services (AD DS) on dc‑1 is essential because it promotes the server to a Domain Controller. This enables centralized authentication, user and group management, and policy enforcement across the network. Without AD DS, client machines cannot join the domain or leverage Active Directory features.</p>

<h4>2.2 -Promoted the Active Directory Server to the Domain Controller and Created a new Forest<br></h4>
<p>Click on the Flag -> Click "Promote this Server to the Domain Controller" </p>
<img width="1426" height="755" alt="image" src="https://github.com/user-attachments/assets/eaaf37df-4369-46a1-805c-8494499c3513" />
<br>
<p>Check "Add a New Forest" checkbox -> Enter your Root Domain Name "mydomain.com"-> Click "Next" </p>
<img width="965" height="707" alt="image" src="https://github.com/user-attachments/assets/2ac19e49-2314-45f2-b317-47f88a885b3a" />
<br>
<p>Enter your AD Password -> Click "next"</p>
<img width="965" height="706" alt="image" src="https://github.com/user-attachments/assets/d18fd37a-f097-424f-88ed-d9b55e1dd367" />
<br>
<p>Uncheck "DNS Delegation" Checkbox -> Click "Next"</p>
<img width="960" height="708" alt="image" src="https://github.com/user-attachments/assets/c41b81c0-822c-4569-8882-5d47f3060ed4" />
<br>
<p>Click "next"</p>
<img width="969" height="710" alt="image" src="https://github.com/user-attachments/assets/2d9eb802-e73c-471a-95fd-d54acc53cd63" />
<br>
<p>Click "Next"</p>
<img width="962" height="707" alt="image" src="https://github.com/user-attachments/assets/165e0cc4-6014-4e86-9bb6-a5ab45056d88" />
<br>
<p>Click "Next"</p>
<img width="955" height="704" alt="image" src="https://github.com/user-attachments/assets/f44482b1-c900-427d-9fdb-d8fd51320c3c" />
<br>
<p>Pre-requisites Passed Successfully ->Click "Install"</p>
<img width="942" height="697" alt="image" src="https://github.com/user-attachments/assets/c9958605-d57d-4bc8-865a-f9d6894060b7" />
<br>
<p>Installation in Progress</p>
<img width="952" height="697" alt="image" src="https://github.com/user-attachments/assets/ebda74b7-3f6c-4418-8900-68fb69b596c9" />
<br>
<p>Successful Installation</p>
<p>Log in as the domain controller in "dc-1" using my new forest domain "mydomain.com\labUser"</p>
<img width="1110" height="709" alt="image" src="https://github.com/user-attachments/assets/e1d4500b-3224-46b5-a2e2-9918e81e1e5b" />
<img width="815" height="473" alt="image" src="https://github.com/user-attachments/assets/08d6843b-476e-4b72-85f0-4e1099fd8bc1" />
<br>
<h4>SUMMARY</h4>
<p>I installed Active Directory on DC‑1 (Windows Server 2022) and promoted it to a Domain Controller by creating a new forest called mydomain.com. This established the domain structure and centralized authentication. After the server restarted, I logged in using the domain account mydomain.com\labUser, confirming that the domain was successfully created and functional.</p>
<br>

<h4>2.3 - Create a Domain Admin user within the Domain.<br></h4
<p>Go to Start->Go to "Windows Adminstrative Tools"->Click on "Active Driectory Users & Computers"</p>
<img width="812" height="998" alt="image" src="https://github.com/user-attachments/assets/8a071dbb-095e-4729-9a09-1e00048c2033" />
<br>
<p>Right-Click on Forest "(mydomain.com)"->Click "New" ->Click "Organizational Unit(OU)</p>
<img width="949" height="671" alt="image" src="https://github.com/user-attachments/assets/10af94e6-6981-48e9-86fe-ccc762cb8bc0" />
<br>
<p>Type _EMPLOYEES -> Click "ok"</p>
<img width="550" height="474" alt="image" src="https://github.com/user-attachments/assets/96041f66-7747-46f5-8176-d376f772e9a8" />
<br>
<p>Right-Click on Forest "(mydomain.com)"->Click "New" ->Click "Organizational Unit(OU)</p> </p>
<img width="954" height="670" alt="image" src="https://github.com/user-attachments/assets/8ede60e1-5c1e-4ba6-bc1a-de18a74b21d2" />
<br>
<p>Type _ADMINS -> Click "ok"</p>
<img width="550" height="474" alt="image" src="https://github.com/user-attachments/assets/96041f66-7747-46f5-8176-d376f772e9a8" />
<img width="952" height="672" alt="image" src="https://github.com/user-attachments/assets/60495324-3df7-4a1c-bb70-31800a53843c" />
<br>
<p>Right-Click on "_ADMINS"->Select "New" -> Select "User" </p>
<img width="945" height="677" alt="image" src="https://github.com/user-attachments/assets/8a93b3a8-d753-4102-a1a9-8a3cbc7dad88" />
<br>
<p>Fill out the form -> Click "next"</p>
<img width="548" height="473" alt="image" src="https://github.com/user-attachments/assets/429ed0ef-86c9-4e2c-8f89-f351deb3a8d1" />
<br>
<p>Enter New Password & Confirm->Click "Next"</p>
<img width="546" height="477" alt="image" src="https://github.com/user-attachments/assets/ada757de-d6a3-4efb-951a-38e53c5eca26" />
<br>
<p>Click "Finish"</p>
<img width="546" height="476" alt="image" src="https://github.com/user-attachments/assets/cde62870-7a1d-4f62-8a98-56082d296dee" />
<br>
<p>Right-Click on the new User -> Select "Properties"</p>
<img width="944" height="663" alt="image" src="https://github.com/user-attachments/assets/255370eb-2a25-47ef-95dd-71e975f32193" />
<br>
<p>Click "Member of"</p></p>
<img width="517" height="692" alt="image" src="https://github.com/user-attachments/assets/8db5fcfd-ad41-413a-a782-479574e1221f" />
<br>
<p>Click "Add"</p>
<img width="514" height="696" alt="image" src="https://github.com/user-attachments/assets/777e5d2e-69f0-4310-9ed0-6d3503c87213" />
<br>
<p>Type in "Domain Admins" ->Click "Check Names"-> Click "ok"</p>
<img width="583" height="320" alt="image" src="https://github.com/user-attachments/assets/5e742491-06f9-417c-ad33-15b4fa474ae1" />
<br>
<p>Click "Apply" -> Click "Ok"</p>
<img width="507" height="688" alt="image" src="https://github.com/user-attachments/assets/762a5ed5-8198-41fd-bab6-eb766cd98bcb" />
<br>
<p>Log Out -> Sign in as the new Admin User-> Enter your new admin credentials->Click "Ok"-> Click "Yes"</p>
<img width="817" height="995" alt="image" src="https://github.com/user-attachments/assets/576a0400-c553-4aad-9506-e4161b992477" />
<img width="562" height="720" alt="image" src="https://github.com/user-attachments/assets/80f5ebbe-5025-4a60-82a9-a2a0bfa2967f" />
<img width="511" height="487" alt="image" src="https://github.com/user-attachments/assets/8d12b321-954b-4c5a-82c5-adbe94e071d2" />
<br>
<p>Successful Login</p>
<img width="864" height="529" alt="image" src="https://github.com/user-attachments/assets/3f2e9f7f-c02f-4939-b040-083d40b2ef66" />
<br>
<h4>SUMMARY</h4>
<P>I organized Active Directory by creating two OUs: _EMPLOYEES and _ADMINS. Then I added a new user, Reece Walsh with the username reece_admin, and elevated them by adding to the Domain Admins group. Finally, I logged back into DC‑1 using mydomain.com\reece_admin, confirming the account’s admin privileges and making it the primary account for your project.</P>
<br>

<h4>2.4 - Joined Client-1 to my domain (mydomain.com).</h4>
<p>From the Azure Protal -> Go to Virtual Machines-> Copy the "client-1" Public IP Address, and paste it on Remote Desktop Connection ->Click "Connect"</p>
<img width="1915" height="718" alt="image" src="https://github.com/user-attachments/assets/f5460478-c22d-4df8-ba3b-bd3913b68fea" />
<br>
<p>Enter "client-1"s original local Admin Credentials-> Click "Ok"</p>
<img width="569" height="556" alt="image" src="https://github.com/user-attachments/assets/18d3306f-8384-48a7-acbe-66159a0a1425" />
<br>
<p>Click "Yes"</p>
<img width="520" height="485" alt="image" src="https://github.com/user-attachments/assets/21d8c8f8-6f79-4269-aae6-0f9ae9e18b27" />
<br>
<p>Go to Start->Type "System" -> Click on System -></p>
<img width="968" height="863" alt="image" src="https://github.com/user-attachments/assets/16432237-123a-454f-882e-df7b95034737" />
<br>
<p>Click on "Advanced System Settings" -> Under "Computer Name" -> Click on "Change"</p>
<img width="1287" height="653" alt="image" src="https://github.com/user-attachments/assets/438dd10c-d262-4ebf-9ada-84992766da60" />
<p>Check the "Domain" Checkbox -> Type the Domain Name "mydomain.com"-> Click "Ok"</p>
<img width="552" height="580" alt="image" src="https://github.com/user-attachments/assets/f40bdeba-91ae-4079-bc41-54d13cff01e2" />
<br>
<p>Enter the "dc-1" Domain Controller credentails when it pops up -> Click "Ok". This pop up confirms that it found the Domain that was created. So we are good to go. </p>
<img width="568" height="511" alt="image" src="https://github.com/user-attachments/assets/0e5cdb91-69b1-455f-978e-bf9ed9d2830a" />
<br>
<p>Click "Ok"</p>
<img width="374" height="215" alt="image" src="https://github.com/user-attachments/assets/7f3ca0d8-6b74-4005-8a46-958277618242" />
<br>
<p>Click "Ok"</p>
<img width="451" height="238" alt="image" src="https://github.com/user-attachments/assets/a0921f68-e193-4aa1-bf55-190336539876" />
<br>
<img width="544" height="572" alt="image" src="https://github.com/user-attachments/assets/e13f6005-2b82-40e4-ab33-d42832468ce4" />
<p>Click "Yes" to Restart the "client-1" VM.</p>
<img width="452" height="225" alt="image" src="https://github.com/user-attachments/assets/c455c2cf-ec9c-4489-9faf-7d5afa32cc40" />
<br>
<h4>SUMMARY</h4>
<p>Joined Client‑1 to the domain (mydomain.com) is critical because it enables centralized authentication, policy enforcement, and resource access through the domain controller (dc‑1). This step validates that DNS and Active Directory are configured correctly, and ensures Client‑1 can fully participate in the managed domain environment.</p>

<h4>2.5 -Logged in to Domain Controller to Verify and Confirm</h4>
<p>From the Azure Portal -> Go to Virtual Machines -> Copy "dc-1" Public IP Address</p>
<img width="1918" height="601" alt="image" src="https://github.com/user-attachments/assets/132c20de-4032-4fca-8002-34d9fb74f381" />
<br>
<p>Enter Credentials -> Click "Ok"</p>
<img width="1109" height="520" alt="image" src="https://github.com/user-attachments/assets/3c60a8a4-ba14-4c5d-8bc7-85b08f36bca2" />
<br>
<p>Click "Yes"</p>
<img width="523" height="501" alt="image" src="https://github.com/user-attachments/assets/81677b04-bbf4-42b0-a37a-91dccb87f572" />
<br>
<p>Go to start -> Click on "Administartive tools" -> Click on Active Directory Computers & Users</p>
<img width="816" height="707" alt="image" src="https://github.com/user-attachments/assets/bfda30d1-1811-41ce-95a8-f72d078b8725" />
<br>
<p>Click "mydomain" ->Click on "Computers" to verify and confirm</p>
<img width="947" height="666" alt="image" src="https://github.com/user-attachments/assets/ea6e3db0-0aac-472f-abb7-bbc13090a2a5" />
<br>
<p>Richt-click "mydomain.com" -> Click on "New" -> CLick on "Organizational Unit" </p>
<img width="949" height="671" alt="image" src="https://github.com/user-attachments/assets/cc70fd25-68a2-47b7-94aa-ff450ecf1185" />
<br>
<p>Created new "OU" and named it "_CLIENTS" ->Click "Ok"</p>
<img width="545" height="481" alt="image" src="https://github.com/user-attachments/assets/de09c229-d8d9-4b4a-82ff-84cc3cbb3891" />
<br>
<p>Click on "Computers" -> Drag "client-1" into the new OU Created "_CLIENTS"</p>
<img width="684" height="679" alt="image" src="https://github.com/user-attachments/assets/093e7d1b-eb57-475b-86a7-d4b24248e410" />
<br>
<p>Click "Yes"</p>
<br>
<p>Confirm Folder. Click on "_CLIENTS</p>
<img width="680" height="450" alt="image" src="https://github.com/user-attachments/assets/49add050-ef50-40b3-a311-73e0760191b1" />
<br>
<h4>SUMMARY</h4>
Verifyied Client‑1 in Active Directory Users and Computers (ADUC) confirms that the domain join was successful. Creating the _CLIENTS Organizational Unit and moving Client‑1 into it establishes a structured environment for centralized management.
<br>

<h4>2.6 Setup Remote Desktop for non-administrative users on Client-1</h4>
<p>Logged in using "Client-1" using the "domain.com" domain</p>
<img width="1120" height="708" alt="image" src="https://github.com/user-attachments/assets/33f206a3-d530-453e-b371-7f023ffeca6a" />
<br>
<p>Successful Login</p>
<img width="1101" height="806" alt="image" src="https://github.com/user-attachments/assets/c80c6d4e-c9b3-4b0d-8ce6-e1760d8511d6" />
<br>
<p>Go to Start -> Type "System" -> Click on "System"</p>
<img width="1076" height="936" alt="image" src="https://github.com/user-attachments/assets/9e66665f-cb45-473b-a62f-b2eee236905e" />
<br>
<p>Click on "Remote Desktop"</p>
<img width="1283" height="932" alt="image" src="https://github.com/user-attachments/assets/fb7a703f-bc07-4fab-a12b-4a8328c46ec4" />
<br>
<p>Click on "Remote Desktop Users"</p>
<img width="1281" height="931" alt="image" src="https://github.com/user-attachments/assets/6f13cba4-ab80-425b-a97d-c6f7d05756b0" />
<br>
<p>Click on "Add"</p>
<img width="510" height="415" alt="image" src="https://github.com/user-attachments/assets/b4dde6bf-1f01-4f65-a74f-5215fb8393ee" />
<br>
<p>Type "Domain User" -> Ckick on "Check Names" -> Click "Ok"</p>
<img width="625" height="354" alt="image" src="https://github.com/user-attachments/assets/1515fa73-b71d-4d89-9be4-c0c773f94583" />
<br>
<p>Click "Ok"</p>
<img width="505" height="415" alt="image" src="https://github.com/user-attachments/assets/9ed8ffa3-4e78-4a8c-8622-fc99d3eb2e46" />
<br>
<h4>SUMMARY</h4>
<p>Configured Remote Desktop for non‑administrative domain users on Client‑1 ensures secure remote access while maintaining least‑privilege principles. By adding domain users to the Remote Desktop Users group, they can connect remotely without requiring administrative rights, confirming proper domain integration and controlled access management.</p>
<br>

<h3>Step 3 - Created Users with Powershell</h3>

<h4>3.1 Create Users and Test Login on Client‑1 with New User</h4>
<p>From the Azure Portal -> Go to Virtual Machines -> Copy "dc-1" Public IP Address</p>
<img width="1918" height="601" alt="image" src="https://github.com/user-attachments/assets/132c20de-4032-4fca-8002-34d9fb74f381" />
<br>
<p>Enter Credentials -> Click "Ok"</p>
<img width="1109" height="520" alt="image" src="https://github.com/user-attachments/assets/3c60a8a4-ba14-4c5d-8bc7-85b08f36bca2" />
<br>
<p>Click "Yes"</p>
<img width="523" height="501" alt="image" src="https://github.com/user-attachments/assets/81677b04-bbf4-42b0-a37a-91dccb87f572" />
<br>
<p>Go to start-> Type "Powershell" -> Right-Click on "Windows Powershell ISE"->Click on "Run as Administrator"</p>
<img width="1041" height="965" alt="image" src="https://github.com/user-attachments/assets/fd828db2-6f5e-44ef-b095-17eeee6e1ef2" />
<br>
<p>Click "Yes"</p>
<img width="567" height="397" alt="image" src="https://github.com/user-attachments/assets/9de490d4-26c1-4831-b909-62b1aef414d0" />
<br>
<p>Click on "File"-> Click "New"</p>
<img width="1714" height="941" alt="image" src="https://github.com/user-attachments/assets/cbe629cf-a312-45de-8903-a60698e0c4c6" />
<br>
<p>Click on "File" again -> Click on "Save as"</p>
<img width="1719" height="894" alt="image" src="https://github.com/user-attachments/assets/77eea8e8-f210-4d69-8d86-08741372a1d2" />
<br>
<p>Type the file name "Script-Users" (You can name the file whatever you want)-> Click "Desktop" for saved Path -> Click "Save"</p>
<img width="949" height="593" alt="image" src="https://github.com/user-attachments/assets/3c82f5cd-d503-4bb1-b69f-2153fea49c2a" />
<br>
<p>Write a script that creates users</p>
<img width="1270" height="897" alt="image" src="https://github.com/user-attachments/assets/d98b3993-6f4b-41fa-9f0c-9b2af9dcff64" />
<br>
<p>Notice the Users all have the Password "Password1" and "10,000" of them will be created using this script.</p>
<img width="1021" height="378" alt="image" src="https://github.com/user-attachments/assets/a0603645-b338-4fec-8709-77e16d93be99" />
<br>
<p>Scroll down, and you will notice the "path" where the users will be created and gets stored in "_EMPLOYEES" Organizational Unit (OU) -> Click on "Run" to run the script.</p>
<img width="1708" height="934" alt="image" src="https://github.com/user-attachments/assets/cd94afca-2bc0-475f-a07d-4cf0b652973e" />
<img width="1697" height="797" alt="image" src="https://github.com/user-attachments/assets/21375c8e-3265-439c-9154-146c77f49f65" />
<br>
<p>This pop message will show. Click "Yes"</p>
<img width="568" height="142" alt="image" src="https://github.com/user-attachments/assets/2697fb83-6bfb-4f58-8833-3b006c68299c" />
<br>
<p>The Users are being created now. Notice the user "kade.folo" user, I will later verify and confirm the user in Active Directory Computers & Users</p>
<img width="1018" height="897" alt="image" src="https://github.com/user-attachments/assets/896ff288-aae8-4d95-8e8e-6b915c33a656" />
<br>
<p>Go to Start ->Type "Active Directory Users & Computer" ->Click on it (ADUC).</p>
<img width="1048" height="973" alt="image" src="https://github.com/user-attachments/assets/a01c2950-a1e8-4b3a-8a89-6409bad4e7d7" />
<br>
<p>Click on mydomain.com ->Click on "_EMPLOYEES" -> Right-Click-> Click on "Find"</p>
<img width="1106" height="682" alt="image" src="https://github.com/user-attachments/assets/933b8422-b405-4606-ad9d-65d848ae16bc" />
<br>
<p>Type the user we said verify and confirm "kade.folo"-> Click on "Find Now". Notice below that we found the user</p>
<img width="648" height="667" alt="image" src="https://github.com/user-attachments/assets/99929dea-4ccc-48fd-b4e2-6f785acc9e4e" />
<br>
<p>Double Click on the user to show details</p>
<img width="882" height="679" alt="image" src="https://github.com/user-attachments/assets/b197bee3-a6b3-4105-828b-ef0321b2d8d9" />
<br>
<p>Azure Portal -> Click "Virtual Machines" -> Copied "Client-1"s Public IP Address</p>
<img width="1999" height="811" alt="image" src="https://github.com/user-attachments/assets/6966f844-0aa3-4bea-a8ac-0e8673c1d01f" />
<br>
<p>Click Windows + R -> Click "Ok" to open Remote Desktop Connection</p>
<img width="462" height="279" alt="image" src="https://github.com/user-attachments/assets/d9368a95-8965-4bef-bd68-5194fafa48c9" />
<br>
<p>Side Note: Notice in the "kade.folo" Properties, the User is in the mydomain.com" domain.</p>
<img width="523" height="691" alt="image" src="https://github.com/user-attachments/assets/07cbf216-3b6b-4f75-87b9-49ad2d915c4f" />
<br>
<p>Paste "client-1"s IP Address -> Click "ok" -> Enter the User "kade.folo" Credentials and Remember, the password is "Password1" -> Click "ok"</p>
<img width="1103" height="703" alt="image" src="https://github.com/user-attachments/assets/104e1611-5d7c-44d9-8a8a-67d97ae76b09" />
<br>
<p>Click "Yes" -> </p>
<img width="522" height="496" alt="image" src="https://github.com/user-attachments/assets/d98e7997-11a7-420d-8ccc-d4bbd078d664" />
<br>
<p>Successful Login</p>
<img width="540" height="574" alt="image" src="https://github.com/user-attachments/assets/e3cb2179-6568-47af-a13e-ad35595e8fe2" />
<br>
<h4>SUMMARY</h4>
<p>Created users with PowerShell in "dc-1" demonstrating automation and scalability in Active Directory. By provisioning thousands of accounts into the _EMPLOYEES OU and successfully logging into Client‑1 with one of them ("kade.folo"), I confirmed proper domain authentication and centralized user management.</p>


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







