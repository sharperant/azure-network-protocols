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
