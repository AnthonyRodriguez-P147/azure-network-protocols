# azure-network-protocols
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

<h2>High-Level Steps</h2>

- Create our Virtual Machines
- Configuring a Firewall (Network Security Group)
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Start by configuring Azure IP addresses in the virtual machines. Mark the virtual machines in Azure that were off the previous day. 
</p>                 
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To start working with virtual machines (VMs), press Start. Create a Resource Group -> Use the Resource Group to create a Windows 10 Virtual Machine (VM) -> Make the necessary adjustments -> Create -> Permit the creation of a new Virtual Network (Vnet) and Subnet during the VM's creation.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select the previously formed Resource Group and Virtual Network (the Virtual Network MUST BE THE SAME) when constructing a Linux (Ubuntu) virtual machine. The type of authentication Password and username NOT the SSH public key -> Next -> Next -> A virtual network or subnet should contain both virtual machines. 
</p>
<br />

<p>
Install Microsoft Remote Desktop if you're using a Mac. Connect to the Windows 10 virtual machine using Remote Desktop by entering the IP address into the Microsoft virtual machine. Get Wireshark installed -> Launch Wireshark and begin capturing packets. 


  
</p>
