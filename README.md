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
</p>
<p>
Then, I deployed a Windows 10 virtual machine, selecting the previously created Resource Group and allowing Azure to generate a new Virtual Network (VNet) and Subnet. I used the password authentication option for the administrator account.
</p>
<p>
<img width="2878" height="1556" alt="slide2" src="https://github.com/user-attachments/assets/2d367f19-462e-4f08-adb6-4a615aa20d2c" />
</p>
<p>
Next, I created a Linux (Ubuntu) virtual machine, again using the same Resource Group and allowing Azure to manage the networking components. Password authentication was selected here as well.
</p>
<p>
<img width="2862" height="1552" alt="slide3" src="https://github.com/user-attachments/assets/dad0eee8-379e-46ba-ad5c-aab98d9a540c" />
</p>
<p>
Observe Your Virtual Network within Network Watcher:
</p>
<p>
<img width="2880" height="1566" alt="slide4" src="https://github.com/user-attachments/assets/97714654-e099-4e13-a426-0ab5e5e920ec" />
</p>
<p>
Monitor ICMP Traffic with Wireshark. I connected to the Windows VM via Remote Desktop, installed Wireshark, and applied a filter to display ICMP traffic only.
</p>
<p>
