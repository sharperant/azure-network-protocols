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
<img width="852" height="500" alt="slide5" src="https://github.com/user-attachments/assets/6b45326f-dc7e-46b5-8487-305e0d59f496" />
</p>
<p>
From the Windows machine, I located the private IP address of the Ubuntu VM and sent ping requests to it. I was able to observe both requests and replies in Wireshark, confirming successful communication over the private network.
</p>
<p>
<img width="2880" height="1560" alt="slide6" src="https://github.com/user-attachments/assets/afcc85bf-c0bc-4741-b245-9a9b497dcd94" />
</p>
<p>
<img width="2878" height="1718" alt="slide7" src="https://github.com/user-attachments/assets/2ab4a380-1fa2-41e6-84ca-d54cb6c5b4f6" />
</p>
<p>
I also pinged a public site like www.google.com, and Wireshark displayed ICMP packets showing traffic going out to the internet and returning responses.
</p>
<p>
<img width="2880" height="1718" alt="slide8" src="https://github.com/user-attachments/assets/3380b4a4-b665-4e9a-814d-ecb8c071c7c3" />
</p>
<p>
To simulate continuous monitoring, I initiated a perpetual ping to the Ubuntu VM from the Windows command line and watched the constant flow of ICMP packets in Wireshark.
</p>
<p>
<img width="2880" height="1720" alt="slide9" src="https://github.com/user-attachments/assets/6acdcf99-f269-4bdd-addb-72d1c5da4d90" />
</p>
<p>
I then navigated to the Ubuntu VM’s Network Security Group in the Azure portal and disabled inbound ICMP traffic by adding a new rule. Back on the Windows VM, I observed that ping replies stopped appearing, and Wireshark confirmed the lack of incoming traffic.
</p>
<p>
<img width="2880" height="1562" alt="slide10" src="https://github.com/user-attachments/assets/29a16f86-b9c9-4552-8549-fe126b5860b1" />
</p>
<p>
<img width="2874" height="1712" alt="slide11" src="https://github.com/user-attachments/assets/c601d62c-8c8e-43fe-a6e8-205f44e31bf6" />
</p>
<p>
