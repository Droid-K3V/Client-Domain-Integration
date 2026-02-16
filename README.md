# Windows Client Domain Intergration
A practical Active Directory workstation intergration project.

## 📃 Overview
This project demonstrates the complete process of intergrating a Windows 10 client into an Active Directory domain. It covers DNS validation, domain join operations, OU organization, Group Policy application, and verification steps that reflect real-world enterprise administration.

This project is part of a broader homelab series designed to simulate professional IT infrastructure environments. 
---

## 🧪 Lab Environment
- Windows Server 2019 (Domain Controller)
- Windows 10 Client VM
- Domain: kevinlab.local
- Domain Controller IP: 10.0.0.252
- DNS: Windows 10 client pointed to the Domain Controller
---

## 🎯 Objectives
- Validate DNS and network configuration
- Join a Windows 10 client to the domain
- Authenticate using domain credentials
- Organize Active Directory structure using OUs
- Apply a baseline workstation Group Policy Object
- Verify GPO processing and domain connectivity
---
## Phase 1 - DNS & Network Validation
The Windows 10 client must use the Domain Controller as its DNS server.

**Windows 10 DNS configuration:**
- Preferred DNS 10.0.0.252
- Alternate DNS: (leave blank)

Correct DNS ensures the client can locate the domain controller during the join process. 
---
## Phase 2 - Rename the Windows 10 Client
1. Open System Properties ('sysdm.cpl')
2. Navigate to the Computer Name tab
3. Select "Change..."
4. Rename the machine to:
WIN10-CLIENT

A reboot is not required yet; the domain join will trigger one.
---
## Phase 3 - Join the Domain
1. Open System Properties again and select "Change..."
2. Choose "Domain"
3. Enter:
kevinlab.local
4. Authenticate using:
kevinlab\administrator
5. Restart the Windows 10 client when prompted.
---
## Phase 4 - First Domain Login
At the login screen:
1. Select "Other user"
2. Log in using a domain account such as:
kevinlab\administrator
or
kevinlab\mbrown

Successful login confirms domain connectivity and authentication.
---
## Phase 5 - Create Workstations OU & Move the Client
On the Domain Controller:
1. Open Active Directory Users and Computers
2. Create a new Organizational Unit named:
Workstations
3. Move the Windows 10 client into this OU
This mirrors real enterprise AD structure and prepares the workstation for targeted GPOs.
---
## Phase 6 - Create Baseline Workstation GPO
In Group Policy Management:
1. Right-click the Workstations OU
2. Create a new GPO named:
Baseline - Workstations
3. Edit the GPO and configure the following:
## Login Banner
Path:
Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options 
Enable:
- Interactive logon: Message title
- Interactive logon: Message text
### Screensaver Policy 
Path:
User Configuration -> Policies -> Administrative Templates -> Control Panel -> Personalization
Configure:
- Enable screen saver
- Password protect the screen saver
- Screen svaer timeout (900 seconds)
### Windows Update Policy 
Path:
Computer Configuration -> Administrative Templates -> Windows Components -> Windows Update 

Configure:
- Automatic Updates -> Enabled -> Auto download and notify
---
## Phase 7 - Apply & Verify GPO
On the Windows 10 Client:
Run:
gpupdate /force
Verify:
gpresult /r
Confirm that the "Baseline - Workstations" GPO appears under Applied Group Policy Objects. 
---
## ✅ Final Results
By completing this project:
- The Windows 10 client is successfully joined to the kevinlab.local domain
- DNS is correctly configured
- Domain authentication works for both admin and standard users
- The workstation is organized within a proper OU
- A baseline workstation GPO is applied
- GPO processing is verified through gpresult
This project demonstrates foundational Active Directory administration and workstation lifecycle management.
---
## ➡️ Next Project
**Begin Networking Fundamentals**
Scheduled for the next session.
---
## Connect
Explore more homelab projects or connect with me on LinkedIn for updates and future builds. 
