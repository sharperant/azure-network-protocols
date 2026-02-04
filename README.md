<p align="center">
<img width="1027" height="359" alt="vmlogo" src="https://github.com/user-attachments/assets/b8a33cb8-7b03-47f0-b1a6-b0b48e9d4997" />

</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
</p>
<p>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups.
</p>
<p>
</p>
<p>
</p>
<p>
<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />
</p>
<p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)
<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04</b>
</p>
<p>
<h2>Actions and Observations</h2>
</p>
<p>
Welcome to my tutorial on Network Security Groups and Inspecting Network Protocols. First you will need to create two VMs on Azure. One machine will be a Linux machine and the other will be a Windows 10 machine. Both will have two cpus and they must be on the same VNET. Once that is done go on the Windows machine and download Wireshark. I will attatch a link to the wireshark download. https://www.wireshark.org/download.html Once installed open Wireshark and filter for ICMP Traffic only. ICMP is a network layer protocol that relays messages concerning network connection issues. Ping uses this protocol, ping tests connectivity between hosts. When we filter wirehsark to only capture ICMP packets and ping the private IP address of our linux machine we can visually see the packets on wireshark.
</p>
<p>
<img width="1634" height="559" alt="slide1" src="https://github.com/user-attachments/assets/00007f54-841f-4751-b2de-63e4dfd77658" />
</p>
<p>
We can inspect each individual packet and see the actual data that is being sent in each ping. the picture below demonstrates just that.
</p>
<p>
<img width="1634" height="337" alt="slide2" src="https://github.com/user-attachments/assets/348518e0-b44d-4eee-9703-435a8d03910d" />
</p>
<p>
In the next portion of the lab we will perpetually ping the Linux machine with the command ping -t. This will continually ping the machine until we decide to stop it, while the Windows machine is pinging the Linux machine we will go to the Linux machine and block inbound ICMP traffic on it's firewall. Once we do that we will stop recieving echo replys from the Linux machine. We will block ICMP by creating a new Network Security Group on the Linux machine that will be set to block ICMP. We can allow the traffic by allowing ICMP on the Linux Network Security Groups page on Azure.
</p>
<p>
<img width="1637" height="416" alt="slide3" src="https://github.com/user-attachments/assets/26d51627-f3fb-4c31-9d85-b48391d0a941" />
</p>
<p>
<img width="1634" height="364" alt="slide4" src="https://github.com/user-attachments/assets/51c1305b-759e-4aee-98c4-3a5cf6d283f1" />
</p>
<p>
Next we will use our Windows machine to SSH to the Linux machine. SSH has no GUI it just gives the user access to the machines CLI. We will set the wireshark filter to capture SSH packets only. When we ssh into the Linux machine with the command prompt "ssh labuser@10.0.0.5" we can see that wireshark starts to immediately capture SSH packets.
</p>
<p>
<img width="1634" height="583" alt="slide5" src="https://github.com/user-attachments/assets/28ff7e16-1ab4-44c2-9dfb-77cec65876f4" />
</p>
<p>
Now we will use wireshark to filter for DHCP. DHCP is the Dynamic Host Configuration Protocol this works on ports 67/68. It is used to assign IP addresses to machines. We will request a new ip address with the command "ipconfig /renew". Once we enter the command wireshark will capture DHCP traffic.
</p>
<p>
<img width="1635" height="404" alt="slide6" src="https://github.com/user-attachments/assets/3e498909-8121-4989-9b37-d1b84f54a75d" />
</p>
</p>
<p>
Time to filter DNS traffic. We will set wireshark to filter DNS traffic. We will initiate DNS traffic by typing in the command "nslookup www.google.com" this command essentially asks our DNS server what is google's IP address.
</p>
<p>
<img width="1628" height="845" alt="slide7" src="https://github.com/user-attachments/assets/45298f01-1eb5-4062-94fc-d90d5ca3463f" />
</p>
<p>
Lastly we will filter for RDP traffic. When we enter tcp.port==3389 traffic is spammed non stop because we are using Remote Desktop Protocol to connect to our Virtual Machine.
</p>
<p>
<img width="1635" height="679" alt="slide8" src="https://github.com/user-attachments/assets/e123fb69-a5e8-47cb-841e-177a16c4c53f" />


