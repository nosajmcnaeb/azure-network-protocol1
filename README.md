# azure-network-protocol1
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2> Six Observation Steps</h2>

- Step 1
Create Virtual Machines and Resource groups in Azure
- Step 2
Download & Install and Run Wireshark
- Step 3
(Observe ICMP Traffic)
- Step 4
(Observe SSH Traffic)
- Step 5
(Observe DHCP Traffic)
- Step 6
 (Observe DNS Traffic)
- Step 7
(Observe RDP Traffic)
- Step 8
Clean up Resources


<h2>Actions and Observations</h2>


Step 1
 
Create a Resource Group
 <p>
<img src="https://i.imgur.com/FSN4J0C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a Windows 10 Virtual Machine (VM)
While creating the VM, select the previously created Resource Group
While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
Create a Linux (Ubuntu) VM
 <p>
<img src="https://i.imgur.com/v3qZhrC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
While create the VM, select the previously created Resource Group and Vnet
Observe Your Virtual Network within Network Watcher

Step 2
Use Remote Desktop to connect to your Windows 10 Virtual Machine
Within your Windows 10 Virtual Machine, 
 <p>
<img src="https://i.imgur.com/kcgxuQf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Install Wireshark
  <p>
<img src="https://i.imgur.com/l1SyDKT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open Wireshark and filter for ICMP traffic only
  <p>
<img src="https://i.imgur.com/nRhFze9.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
Observe ping requests and replies within WireShark
  <p>
<img src="https://i.imgur.com/TGMkrPg.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) 
 and observe the traffic in WireShark
  <p>
<img src="https://i.imgur.com/5KV4sXI.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
  <p>
<img src="https://i.imgur.com/aNMjeuU.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
  <p>
<img src="https://i.imgur.com/R5txShY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
Stop the ping activity
 <p>
<img src=" https://i.imgur.com/n1NnN0D.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
Back in Wireshark, filter for SSH traffic only
  <p>
<img src="https://i.imgur.com/LJTtnQm.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
Exit the SSH connection by typing ‘exit’ and pressing [Enter]

.
</p>
<br />

 
Back in Wireshark, filter for DHCP traffic only
 <p>
<img src="https://i.imgur.com/TMIQFRZ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
Observe the DHCP traffic appearing in WireShark

  <p>
<img src="https://i.imgur.com/ZCDHXJg.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back in Wireshark, filter for DNS traffic only
  <p>
<img src="https://i.imgur.com/z72rGVA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
Observe the DNS traffic being show in WireShark


Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
  <p>
<img src="https://i.imgur.com/VgWNl1I.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted


 
Close your Remote Desktop connection
Delete the Resource Group(s) created at the beginning of this lab
Verify Resource Group Deletion
  <p>
<img src="https://i.imgur.com/InYL64m.gif" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 


</p>
<br />
