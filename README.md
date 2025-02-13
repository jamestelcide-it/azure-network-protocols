<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a Resource Group
- Create a Virtual Machine
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

<h2>Set up Your Virtual Environment</h2>

<img src="https://github.com/user-attachments/assets/ac952f84-f6e7-4129-9f4b-a91fdf6c9553" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/ac952f84-f6e7-4129-9f4b-a91fdf6c9553) -->
<p>
First we can create our resource group inside Azure.
</p>
<br />

<img src="https://github.com/user-attachments/assets/2bbbd491-ba5e-450d-89df-1d5ba4559f17" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/2bbbd491-ba5e-450d-89df-1d5ba4559f17) -->

<img src="https://github.com/user-attachments/assets/3441e7f0-c458-484d-89c3-25e19b87e864" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/3441e7f0-c458-484d-89c3-25e19b87e864) -->

<p>
Now we can create our Windows Virtual Machine. We will also create a new Virtual Network (VNet) that will be shared with our second virtual machine.
</p>
<br />

<img src="https://github.com/user-attachments/assets/a2bc422d-c65c-48c4-84d0-f1571cf52c3a" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/a2bc422d-c65c-48c4-84d0-f1571cf52c3a) -->
<p>
Next we create our Ubuntu virtual machine using the same Resource Group that the windows machine is on.
</p>
<br />

<h2>Observing ICMP Traffic</h2>

<img src="https://github.com/user-attachments/assets/3b9baea1-4afd-4ea3-a0ed-207bcd316b07" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/3b9baea1-4afd-4ea3-a0ed-207bcd316b07) -->
<p>
We can now use remote desktop to get into our Windows 10 Virtual Machine, install Wireshark, and within the application filter for ICMP traffic only. To get the traffic we retrieve the private IP address of the Ubuntu virtual machine and attempt to ping it from the windows 10 virtual machine.
</p>
<br />

<img src="https://github.com/user-attachments/assets/4834b743-6cac-4f06-a6ef-b6954bd68d08" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/4834b743-6cac-4f06-a6ef-b6954bd68d08) -->
<p>
We can also attempt to ping a public website for example google.com and observe this traffic in wireshark as well.
</p>
<br />

<img src="https://github.com/user-attachments/assets/b584852b-5b06-467c-9e78-468267e5268c" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/b584852b-5b06-467c-9e78-468267e5268c) -->
<p>
Currently we can send a perpetual request to our linux vm and receive a reply.
</p>
<br />

<img src="https://github.com/user-attachments/assets/806f137a-f1c2-4a43-ba62-3ae263f8617d" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/806f137a-f1c2-4a43-ba62-3ae263f8617d) -->

<img src="https://github.com/user-attachments/assets/74565bae-83f4-40ae-a7ec-4a7ae35e5882" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/74565bae-83f4-40ae-a7ec-4a7ae35e5882) -->

<img src="https://github.com/user-attachments/assets/6c51834c-0862-4495-877a-4fce2f116810" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/6c51834c-0862-4495-877a-4fce2f116810) -->

<p>
If we open the Network Security Group for our linux vm we can add an inbound security rule to disable ICMP traffic, this will change how what we will see in wireshark and the response we get from Powershell. We can remove the inbound security rule later to re-enable icmp traffic.
</p>
<br />

<h2>Observing SSH Traffic</h2>

<img src="https://github.com/user-attachments/assets/720aee99-902f-4bc1-82fa-ba8a30c9d2ea" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/720aee99-902f-4bc1-82fa-ba8a30c9d2ea) -->

<img src="https://github.com/user-attachments/assets/56cee4db-c9cc-4068-b627-104b7ae10836" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/56cee4db-c9cc-4068-b627-104b7ae10836) -->
<p>
Back in Wireshark we can filter for SSH (Secure Shell Protocol) traffic from our Windows 10 vm. We then can SSH into our linux virtual machine through its private IP address and type the commands ls, pwd, etc. and observe the traffic in wireshark. We also can notice for every key stroke SSH traffic is sent in wireshark.
</p>
<br />

<h2>Observing DHCP Traffic</h2>

<img src="https://github.com/user-attachments/assets/a5401421-a0bd-495c-8a0d-9f4800b245fd" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/a5401421-a0bd-495c-8a0d-9f4800b245fd) -->
<p>
Now in wireshark if we filter for DHCP traffic only we can attempt to issue a new IP address from the command line using ipconfig /renew
</p>
<br />

<h2>Observing DNS Traffic</h2>

<img src="https://github.com/user-attachments/assets/1a824eb4-7804-44ca-a82b-4706026c53bc" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/1a824eb4-7804-44ca-a82b-4706026c53bc) -->
<p>
In Wireshark we can filter for DNS traffic only and to do this in our windows vm we can use the command line and use nslookup on for example google.com's ip address to observe the DNS traffic being shown in Wireshark.
</p>
<br />

<h2>Observing RDP Traffic</h2>

<img src="https://github.com/user-attachments/assets/0e9a2599-7c34-4e98-9d3c-bcd23cc2f32d" height="80%" width="80%" />
<!-- ![image](https://github.com/user-attachments/assets/0e9a2599-7c34-4e98-9d3c-bcd23cc2f32d) -->
<p>
Finnally we will filter for RDP traffic by using "tcp.port==3389" to observe a non-stop stream of traffic because we are currently using RDP to access the windows vm.
</p>
<br />
