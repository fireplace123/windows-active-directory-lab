# Windows Active Directory Lab (AWS EC2)  

This project demonstrates setting up a Windows Server environment with Active Directory on AWS EC2 instances, simulating a cloud-based corporate IT setup.  

---

## 🔧 Tools & Technologies Used
- **Amazon Web Services (AWS)**  
  - **EC2 Instances** → Hosted Windows Server and Windows 10 machines in the cloud  
  - **Security Groups** → Configured inbound/outbound firewall rules  
  - **Elastic IPs** → Assigned static IPs for reliable domain and DNS resolution  
- **Windows Server 2019 (EC2)** → Configured as Domain Controller (AD DS, DNS, DHCP roles)  
- **Windows 10 Pro (EC2)** → Joined to the Active Directory domain  
- **Active Directory Users and Computers (ADUC)** → Managed users, groups, and organizational units  
- **Group Policy Management Console (GPMC)** → Applied policies for security and configuration  
- **RDP (Remote Desktop Protocol)** → Connected to servers and client machines securely  

---

## 🛠️ Project Tasks (Real-World Simulation)
1. **AWS Setup**  
   - Launched two EC2 instances:  
     - **Windows Server 2019** (Domain Controller)  
     - **Windows 10 Pro** (Client)  
   - Created **Security Groups** to allow RDP and DNS between instances  
   - Attached **Elastic IPs** to ensure consistent connectivity  

2. **Domain Controller Configuration**  
   - Promoted Windows Server 2019 instance to **Domain Controller**  
   - Deployed a new forest: `lab.local`  
   - Installed **DNS** role to support name resolution  

3. **User & Group Management**  
   - Created OUs: `HR`, `IT`, `Sales`  
   - Added user accounts (`alice.hr`, `bob.it`, `carol.sales`)  
   - Configured shared folders and permissions based on security groups  

4. **Group Policy Deployment**  
   - Applied password complexity, expiration, and account lockout policies  
   - Restricted access to Control Panel for non-IT users  
   - Configured a custom login banner for compliance testing  

5. **Client Domain Join**  
   - Updated Windows 10 client’s DNS to point to the Domain Controller EC2 instance  
   - Joined client to `lab.local` domain  
   - Verified user logins with domain accounts  

---
---

## 📝 Troubleshooting Experience
- **RDP Connectivity Issues** → Adjusted AWS Security Group inbound rules (allowed TCP 3389 only from my IP)  
- **Domain Join Failures** → Fixed by pointing client DNS to the DC’s **private IP** instead of AWS public DNS  
- **GPO Not Applying** → Ran `gpupdate /force` and verified using `gpresult /r`  
- **Time Sync Issues** → Configured NTP on Windows Server to keep domain time aligned with AWS  

---

## 📚 Key Takeaways
- Practical experience deploying **Windows Server Active Directory in the cloud**  
- Learned how to manage **AWS networking (security groups, Elastic IPs, private DNS)**  
- Strengthened troubleshooting skills across **DNS, RDP, and domain joins**  
- Demonstrated ability to replicate **enterprise IT environments on AWS**  

---
