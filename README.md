# azure-network-protocols<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe  network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Resource Group
- Create Virtual Machine (windows)
- Create Virtual Machine (linux)
- Install Wireshark

<h2>Actions and Observations</h2>

<p>
<img src="https://imgur.com/4onsF8D.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The first step is to create the resource group, next create Create a Windows 10 Virtual Machine (VM). Next create a Linux (Ubuntu) VM .
While creating the VM, select the previously created Resource Group and allow it to create a new Virtual Network (Vnet) and Subnet.
Observe Your Virtual Network within Network Watcher

</p>
<br />

<p>
<img src="https://imgur.com/rgBUtRS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Use Remote Desktop to connect to your Windows 10 Virtual Machine, Install Wireshark on the Windows VM.
Open Wireshark and filter for ICMP traffic only. Retrieve the private IP address of the Ubuntu VM. Open PowerShell and attempt to ping it from within the Windows 10 VM
notice the ping requests and replies within WireShark, attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark. Start a perpetual ping(-t) from Windows 10 VM to your Ubuntu VM.
Open the Network Security Group your Ubuntu VM is using and make a new rule to disable incoming ICMP traffic.Go back into the Windows 10 VM, notice the ICMP traffic in WireShark and the command line Ping activity.
Restart ICMP traffic for the Network Security Group your Ubuntu VM. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
Stop the ping activity.
.
</p>
<br />

<p>
<img src="https://imgur.com/jnLNLw6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://imgur.com/xxU9URi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
Go into Wireshark and filter for SSH traffic only, now from your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
Type commands (ls, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
Exit the SSH connection by typing ‘exit’ and pressing [Enter]
Now go into Wireshark and  filter for DHCP traffic only, now from your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
Observe the DHCP traffic appearing in WireShark. Once in Wireshark, filter for DNS traffic only.
From your Windows 10 VM within a command line, use nslookup to see the IP address for google.com and disney.com, observe the DNS traffic in WireShark
Go back to Wireshark and filter for RDP traffic only (tcp.port == 3389).  RDP (protocol) is constantly showing you a live stream from one computer to another, traffic is always being transmitted.

After you observed the traffic, you can now disconnect  your remote desktop connection and delete the Resource Group that was created at the beginning of this lab
.
</p>
<br />
