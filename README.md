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
<img width="80%" height="562" alt="slide1" src="https://github.com/user-attachments/assets/eb12ece2-5c98-4479-8dad-37e71c62e8ba" />
</p>
<p>
Then, I deployed a Windows 10 virtual machine, selecting the previously created Resource Group and allowing Azure to generate a new Virtual Network (VNet) and Subnet. I used the password authentication option for the administrator account.
</p>
<p>
<img width="80%" height="1556" alt="slide2" src="https://github.com/user-attachments/assets/2d367f19-462e-4f08-adb6-4a615aa20d2c" />
</p>
<p>
Next, I created a Linux (Ubuntu) virtual machine, again using the same Resource Group and allowing Azure to manage the networking components. Password authentication was selected here as well.
</p>
<p>
<img width="80%" height="1552" alt="slide3" src="https://github.com/user-attachments/assets/dad0eee8-379e-46ba-ad5c-aab98d9a540c" />
</p>
<p>
Observe Your Virtual Network within Network Watcher:
</p>
<p>
<img width="80%" height="1566" alt="slide4" src="https://github.com/user-attachments/assets/97714654-e099-4e13-a426-0ab5e5e920ec" />
</p>
<p>
Monitor ICMP Traffic with Wireshark. I connected to the Windows VM via Remote Desktop, installed Wireshark, and applied a filter to display ICMP traffic only.
</p>
<p>
<img width="80%" height="500" alt="slide5" src="https://github.com/user-attachments/assets/6b45326f-dc7e-46b5-8487-305e0d59f496" />
</p>
<p>
From the Windows machine, I located the private IP address of the Ubuntu VM and sent ping requests to it. I was able to observe both requests and replies in Wireshark, confirming successful communication over the private network.
</p>
<p>
<img width="80%" height="1560" alt="slide6" src="https://github.com/user-attachments/assets/afcc85bf-c0bc-4741-b245-9a9b497dcd94" />
</p>
<p>
<img width="80%" height="1718" alt="slide7" src="https://github.com/user-attachments/assets/2ab4a380-1fa2-41e6-84ca-d54cb6c5b4f6" />
</p>
<p>
I also pinged a public site like www.google.com, and Wireshark displayed ICMP packets showing traffic going out to the internet and returning responses.
</p>
<p>
<img width="80%" height="1718" alt="slide8" src="https://github.com/user-attachments/assets/3380b4a4-b665-4e9a-814d-ecb8c071c7c3" />
</p>
<p>
To simulate continuous monitoring, I initiated a perpetual ping to the Ubuntu VM from the Windows command line and watched the constant flow of ICMP packets in Wireshark.
</p>
<p>
<img width="80%" height="1720" alt="slide9" src="https://github.com/user-attachments/assets/6acdcf99-f269-4bdd-addb-72d1c5da4d90" />
</p>
<p>
I then navigated to the Ubuntu VM’s Network Security Group in the Azure portal and disabled inbound ICMP traffic by adding a new rule. Back on the Windows VM, I observed that ping replies stopped appearing, and Wireshark confirmed the lack of incoming traffic.
</p>
<p>
<img width="80%" height="1562" alt="slide10" src="https://github.com/user-attachments/assets/29a16f86-b9c9-4552-8549-fe126b5860b1" />
</p>
<p>
<img width="80%" height="1712" alt="slide11" src="https://github.com/user-attachments/assets/c601d62c-8c8e-43fe-a6e8-205f44e31bf6" />
</p>
<p>
After that, I removed the ICMP block rule in the NSG, and the ping started responding again, which was visible both on the command line and in Wireshark.
</p>
<p>
<img width="80%" height="1560" alt="slide12" src="https://github.com/user-attachments/assets/529615f3-31d7-4443-99be-cddffe7c9d45" />
</p>
<p>
Observe SSH Traffic. In Wireshark, I changed the filter to display SSH traffic only. From the Windows VM, I SSH'd into the Ubuntu machine using its private IP. As I typed commands like ls and pwd, I saw SSH packet activity appear in Wireshark. I ended the SSH session by typing exit, closing the secure shell connection.
</p>
<p>
<img width="80%" height="1712" alt="slide13" src="https://github.com/user-attachments/assets/1ecb78ed-8332-48f1-ba05-424ef09db5fd" />
</p>
<p>
Analyze DHCP Traffic. I updated the Wireshark filter to capture DHCP traffic. On the Windows VM, I opened the command prompt and typed ipconfig /renew to request a new IP address from the DHCP server. In Wireshark, I observed the DHCP request and response process, showing the renewal of the machine’s IP address.
</p>
<p>
<img width="80%" height="1712" alt="slide14" src="https://github.com/user-attachments/assets/a8264b84-d662-4cf8-968a-22f2f40c26ba" />
</p>
<p>
Inspect DNS Traffic. With Wireshark now set to display DNS packets, I used the nslookup command in the Windows command line to query the IP addresses of google.com and disney.com. Each query generated visible DNS traffic in Wireshark, showing resolution requests and the resulting IP addresses.
</p>
<p>
<img width="80%" height="1714" alt="slide15" src="https://github.com/user-attachments/assets/fe8bab10-9e9f-42f3-9eac-fd536888c553" />
</p>
<p>
Review RDP Traffic. Lastly, I filtered Wireshark to show RDP traffic only using the expression tcp.port==3389. I noticed a constant stream of RDP packets, which is expected because Remote Desktop Protocol continuously sends data to maintain a live visual connection between the host and client.
</p>
<p>
<img width="2880" height="1720" alt="slide16" src="https://github.com/user-attachments/assets/7cbf89c4-94c1-4024-b204-b891e9cb6734" />
</p>
<p>
Clean up Azure Environment Once all observations were complete, I closed the Remote Desktop session, returned to the Azure portal, and deleted the Resource Group to ensure no lingering resources would incur extra charges.
