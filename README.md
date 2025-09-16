# Windows Active Directory Lab (AWS EC2)  

This project demonstrates how I deployed a Windows Server Active Directory environment in AWS EC2. The lab simulates a real IT environment with a Domain Controller and a client machine joined to the domain.  

---

## 🔧 Tools & Technologies Used
- **Amazon Web Services (AWS)** → EC2 instances, Security Groups, Elastic IPs  
- **Windows Server 2019** → Domain Controller (AD DS, DNS)  
- **Windows 10 Pro (EC2)** → Client machine joined to the domain  
- **PowerShell** → Automated AD tasks (user, group, OU creation)  
- **RDP** → Remote administration  

---

## 🌐 Architecture Overview
[ My PC ] --RDP--> [ AWS EC2: DC01 (Windows Server 2019, AD DS, DNS) ]
|
v
[ AWS EC2: MEM01 (Windows 10 Pro Client) ]


---

## 🛠️ Project Tasks (Step by Step)

### 1. AWS Setup
- Launched 2 EC2 instances:  
  - `DC01` → Windows Server 2019  
  - `MEM01` → Windows 10 Pro  
- Created a **Security Group**:  
  - Allowed RDP (TCP/3389) from my IP only  
  - Allowed all traffic *within* the group (for DC ↔ Client communication)  
- Assigned an **Elastic IP** to `DC01` for stable connectivity  

### 2. Domain Controller Configuration
- Renamed the server:  
    powershell
  Rename-Computer -NewName "DC01" -Restart
  
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Install-WindowsFeature DNS -IncludeManagementTools


# Create OUs
New-ADOrganizationalUnit -Name "HR" -Path "DC=lab,DC=local"
New-ADOrganizationalUnit -Name "IT" -Path "DC=lab,DC=local"

# Create Users
New-ADUser -Name "Alice HR" -SamAccountName "alice.hr" -UserPrincipalName "alice.hr@lab.local" -Path "OU=HR,DC=lab,DC=local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force) -Enabled $true

New-ADUser -Name "Bob IT" -SamAccountName "bob.it" -UserPrincipalName "bob.it@lab.local" -Path "OU=IT,DC=lab,DC=local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force) -Enabled $true


