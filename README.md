# System and Network Administration Project

**INTRODUCTION**

In this project, I chose to put together a few smaller projects together into one due to the simplicity behind each of these components. Each subcategory of the scope of the project are listed below. I will be describing the finely grained components to each throughout the sections. I will also compile various files and add them depending on how critical they are to this process.

I have recorded videos for the project that demonstrate system and network administrator techniques. They are linked to this project page by part. The links take you to youtube where the videos have been uploaded.

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


Part B:

2. Check Network Performance and Network Sniffing

![Drawing2](https://github.com/OmrSanchez/Network-Project/assets/54558041/39975629-5d83-4995-84ba-6584902d3689)

The steps taken are as follows:

**Network Performance and Sniffing**

**DC (Server 2019)**
1.	Verify IP address
2.	Mkdir C:\BigFiles (Creates folder named “BigFiles”)
3.	Net share BigFiles=C:\BigFiles /GRANT:Everyone,FULL (Defines who folder is shared with)
4.	Icacls “C:\BigFiles” /grant Everyone:F (Permissions, not adequate for security, current permissions assigned are due to Test Environment)
5.	Map Network Drive to Client PC
6.	Disconnect Network Drive
7.	Open Performance Monitor
8.	Create “NEW” data collector set with relevant markers
    a.	Name: Network Performance
    b.	Create manually (advanced)
    c.	Next  Create data logs > Performance counter  Next
    d.	Net Adapter: “Bytes Total/sec”, “Current Bandwidth”
    e.	TCPIP Performance Diagnostics: “TCP checksum errors”, “TCP timeouts”
    f.	TCPv4: Connections Active
    g.	Ok
    h.	Finish
9.	Save Template (Explain that this template can be used on other servers that perform similar functions)

**Client 1 (Windows 10)**
1.	Verify IP address
2.	Same subnet?
3.	Ping to DC to verify connectivity
4.	Mkdir C:\projects (Creates folder named project)
5.	CD C:\projects (changes powershell file directory to folder “projects”)
6.	Fsutil file createnew test1 1000000000000000 (creates a new file named test1)

**Transfer**
1.	[DC]: Open wireshark  select Internal Network Port  filter to IP  Start Capture
2.	[DC]: Open Performance Monitor  Select “Network Performance Template”  Right-click  Start
3.	[Client] Robocopy C:\projects \\DC-VB1\BigFiles (performs file transfer over the network between both devices, source = C:\projects, destination = \\DC10\BigFiles)

https://youtu.be/PmLN_881AZw?si=KJlqJVmmYMeExwWC

Part C:

3. Perform Host Discovery

![Drawing3](https://github.com/OmrSanchez/Network-Project/assets/54558041/31c81a2d-0862-4d3a-9880-cb7f591f86d7)

The steps taken are as follows:

**Host Discovery and Port Scanning** 

**Kali Linux**
1.	Ifconfig
2.	ip a
3.	ip route show (routes)
4.	arp -e (Ip to mac address table)
5.	arp -a (Ip to mac address table)
6.	ip neighbor (Similar to arp)
7.	Netdiscover -i eth0 -r “172.16.0.0/24” (Searches for hosts)
   
**DC**
1.	pathping 172.16.0.101  (Tests reliability of connection)
   
**Kali Linux**
1.	mmap localhost (Based on destination of search, identifies open ports)
2.	mmap “172.16.0.0/24” (Identify hosts, ports open on host, lists other hosts)
3.	sudo nmap -sS 172.16.0.1 (Targeted scan that scans the 1000 default port range)
4.	sudo nmap -A 172.16.0.1 (Targeted scan enabled OS detection, version detection, script scanning, and traceroute)

https://youtu.be/ccLNmBk0h44?si=Yu4WAzeCicawq5Hp




