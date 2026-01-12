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

- Step 2
- Step 3
- Step 4

