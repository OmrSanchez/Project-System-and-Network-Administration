# Network-Project

**INTRODUCTION**

In this project, I chose to put together a few smaller projects together into one due to the simplicity behind each of these components. Each subcategory of the scope of the project are listed below. I will be describing the finely grained components to each throughout the sections. I will also compile various files and add them depending on how critical they are to this process.

This project showcases various commands in Powershell and Linux. It also familarizes us with Windows Server 2019 and skills required by system administrators. 
Skills Demonstrated are as follows:
  
  -Virtualization
  
    -Installed:
    
      •  Windows Server 2019
      
      •  Windows 10 Pro
      
      •  Kali Linux
      
      •  Type 2 Hypervisor (VirtualBox)
  
  -DHCP Server creation and hosting
  
  -DNS Server creation and hosting
  
  -Active Directory creation and management
  
  -DC creation and management
  
  -Organizational Unit creation and management
  
  -User accounts creation and management
  
  -Security Groups creation and management
  
  -Group Policy creation and management
  
  -Joining clients to Domain
  
  -Powershell/Command Prompt/Linux CLI
  
  -Troubleshooting
  
  -Network Administration
  
    -Static IP assignment
    
    -NAT
    
    -DHCP IP assignment
    
    -Troubleshooting
    
    -Host Discovery
    
    -Port Scanning
    
    -Network Sniffing

Part A:
1. Manage Access Controls in Windows Server
![Drawing4](https://github.com/OmrSanchez/Network-Project/assets/54558041/e53df0b7-1aa3-4d55-81ec-2c7d928f4791)

The steps taken are as follows:
**Manage Access Controls in Windows Server**
DC (Server 2019)
1.	whoami /user (Displays SID – tracks user accounts)
2.	get-aduser -identity administrator -properties * (Displays account information)
3.	Server Manager -> Active Directory Users and Computers -> Create New OU -> Create New User -> Create New Security Group -> Assign User to Security Group
4.	Manually Add computer to Computers OU
5.	Create a new windows image -> Join to DC and verify addition of PC -> Name different from manually added PC.
6.	get-adcomputer -filter * | out-file C:\computers.txt (Create a file listing all computer associated with DC)
7.	Server Manager -> Tools -> Group Policy Management -> Default Domain Policy (Single password policy) -> right-click  Edit -> Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Settings -> Password Policy
8.	Policy Requirements Based on Company Requirements:
    a.	Min Pass Length: 14
    b.	Complexity: Enabled
    c.	Max Pass: 90 days
    d.	Min Pass: 1 day
    e.	Enforce Pass History: 20
    f.	Enforce Reversible Encryption: Disabled
9.	(Before:) gpresult /H C:\passwords-gpresults-current.html
10.	gpupdate (Sets the current policy to the DC)
11.	(After:) gpresult /H C:\passwords-gpresults-new.html

https://youtu.be/O_UtfeGBw7o?si=OU9X4BufpdzcgLQW



2. Check Network Performance and Network Sniffing


3. Perform Host Discovery

https://youtu.be/O_UtfeGBw7o?si=OU9X4BufpdzcgLQW
