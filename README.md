<p align="center">
<img width="1027" height="359" alt="vmlogo" src="https://github.com/user-attachments/assets/b8a33cb8-7b03-47f0-b1a6-b0b48e9d4997" />

</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
</p>
<p>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups.
</p>
<p>
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
<h2>High-Level Steps</h2>

  - Create a Resource Group

  - Create a Virtual Machine

- Observe ICMP Traffic

- Observe SSH Traffic

- Observe DHCP Traffic

- Observe DNS Traffic

- Observe RDP Traffic 
</p>
<p>
<h2>Actions and Observations</h2>
</p>
<p>
Set up the virtual environment. First, I created a Resource Group in my Azure subscription to organize all related resources.
</p>
<p>
<img width="1037" height="562" alt="slide1" src="https://github.com/user-attachments/assets/eb12ece2-5c98-4479-8dad-37e71c62e8ba" />


