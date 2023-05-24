<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<!--- <h2>Video Demonstration</h2>(coming soon!) -->

<!--- - ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com) -->

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Creating Resources (VMs)
- Observing ICMP traffic
- Observe SSH traffic
- Observe DHCP traffic
- Observe DNS traffic
- Observe RDP traffic

<h2>Actions and Observations</h2>

#### Part 1 (Create our Resources)
- Create a Resource Group
- Create a Windows 10 Virtual Machine (VM)
    - While creating the VM, select the previously created Resource Group
    - While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
- Create a Linux (Ubuntu) VM
    - While create the VM, select the previously created Resource Group and Vnet
- Observe Your Virtual Network within Network Watcher

<br />

#### NSG Resource Group.
<p>
<img src="https://i.imgur.com/VXfIPeR.png" height="80%" width="80%" alt="Network Security Group Resource Group"/>
</p>

#### CMD Line Interface inside VM.
<p>
<img src="https://i.imgur.com/c5nnvsR.png" height="80%" width="80%" alt="CMD Line Interface inside VM"/>
</p>

#### Wireshark Pack Analyzer inside VM.
<p>
<img src="https://i.imgur.com/Jr8GE8D.png" height="80%" width="80%" alt="Wireshark Packet Analyzer inside VM"/>
</p>

<br />

#### Part 2 (Observe ICMP Traffic)
- Use Remote Desktop to connect to your Windows 10 Virtual Machine
- Within your Windows 10 Virtual Machine, Install Wireshark
- Open Wireshark and filter for ICMP traffic only
- Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
    - Observe ping requests and replies within WireShark
- From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
- Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
    - Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
    - Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
    - Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
    - Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
    - Stop the ping activity

<br />

#### ICMP to VM2.
<p>
<img src="https://i.imgur.com/ZC96aiy.png" height="80%" width="80%" alt="ICMP to VM2"/>
</p>

#### ICMP to www.google.com.
<p>
<img src="https://i.imgur.com/DwQReRc.png" height="80%" width="80%" alt="ICMP to www.google.com"/>
</p>

#### NSG rule-set blocking ICMP traffic in VM2.
<p>
<img src="https://i.imgur.com/bT0prNp.png" height="80%" width="80%" alt="NSG rule-set blocking ICMP traffic in VM2"/>
</p>

#### ICMP being blocked by VM2 NSG.
<p>
<img src="https://i.imgur.com/FBIcPi0.png" height="80%" width="80%" alt="ICMP being blocked by VM2 NSG"/>
</p>

</br>

#### Part 3 (Observe SSH Traffic)
- Back in Wireshark, filter for SSH traffic only
- From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
    - Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
    - Exit the SSH connection by typing ‘exit’ and pressing [Enter]

<br />

#### SSH to VM2.
<p>
<img src="https://i.imgur.com/2pAEi2y.png" height="80%" width="80%" alt="ssh to VM2"/>
</p>

#### SSH traffic analysis between VM1 and VM2.
<p>
<img src="https://i.imgur.com/S4mbBs3.png" height="80%" width="80%" alt="ssh traffic analysis between VM1 and VM2"/>
</p>

#### Manipulating VM2 inside of VM1.
<p>
<img src="https://i.imgur.com/t5b5Qwd.png" height="80%" width="80%" alt="manipulating VM2 inside VM1"/>
</p>

</br>

#### Part 4 (Observe DHCP Traffic)
- Back in Wireshark, filter for DHCP traffic only
- From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
    - Observe the DHCP traffic appearing in WireShark

<br />

#### DHCP traffic.
<p>
<img src="https://i.imgur.com/0yFhKGA.png" height="80%" width="80%" alt="DHCP traffic"/>
</p>

</br>

#### Part 3 (Observe DNS Traffic)
- Back in Wireshark, filter for DNS traffic only
- From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
    - Observe the DNS traffic being show in WireShark

<br />

#### DNS traffic.
<p>
<img src="https://i.imgur.com/1VUm5Xo.png" height="80%" width="80%" alt="DNS traffic"/>
</p>

</br>

#### Part 3 (Observe RDP Traffic)
- Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
- Oserve the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
    - Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted

<br />

#### RDP traffic.
<p>
<img src="https://i.imgur.com/lOd79nz.png" height="80%" width="80%" alt="RDP traffic"/>
</p>
