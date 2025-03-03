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
  
![image](https://github.com/user-attachments/assets/d60c7f12-e978-4933-bbc1-927145d06581)

</p>
<p>
Start by configuring Azure IP addresses in the virtual machines. Mark the virtual machines in Azure that were off the previous day. 
</p>                 
<br />

<p>
  
![image](https://github.com/user-attachments/assets/831f1468-2946-40e4-a321-f1d11df65da5)

</p>
<p>
To start working with virtual machines (VMs), press Start. Create a Resource Group -> Use the Resource Group to create a Windows 10 Virtual Machine (VM) -> Make the necessary adjustments -> Create -> Permit the creation of a new Virtual Network (Vnet) and Subnet during the VM's creation.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/9695327b-598b-480e-bcc3-074a8f49c8ac)
![Screenshot 2025-03-03 012604](https://github.com/user-attachments/assets/73f7911d-9f8c-4f35-8712-c1fefb608499)

</p>
<p>
Select the previously formed Resource Group and Virtual Network (the Virtual Network MUST BE THE SAME) when constructing a Linux (Ubuntu) virtual machine. The type of authentication Password and username NOT the SSH public key -> Next -> Next -> A virtual network or subnet should contain both virtual machines. 

![image](https://github.com/user-attachments/assets/3422af1a-4f55-4482-aef8-fb685e93aced)

![image](https://github.com/user-attachments/assets/b8f9c12f-79db-425c-9b1b-fe946244e1d4)

  
</p>
<br />

<p>
Install Microsoft Remote Desktop if you're using a Mac. Connect to the Windows 10 virtual machine using Remote Desktop by entering the IP address into the Microsoft virtual machine. 
  
![image](https://github.com/user-attachments/assets/342fc2d5-f81a-4c24-b351-132682879b51)


We will now install wireshark on our windows vm

![image](https://github.com/user-attachments/assets/cf383adc-8081-48c2-984c-46f13e01cd35)

Download the windows version

 ![image](https://github.com/user-attachments/assets/d614d2c9-5fa5-4237-959a-8bd4e7f5e26c)

 when wireshark is done downloading it should look like this

 ![image](https://github.com/user-attachments/assets/be308b06-9792-4981-98f0-d12c13ea88a1)

</p>

<br />

<p>
   Open Wireshark and start packet capture 
  
![image](https://github.com/user-attachments/assets/7e20fe96-9bbd-48d4-bc33-b1690ea4ad0c)

Now, filter Wireshark to only show ICMP traffic on the search bar, using power shell we will try to ping the Ubuntu virtual machine (linux-vm) from within the Windows 10 virtual machine (VM) after retrieving its private IP address. 

![image](https://github.com/user-attachments/assets/c948204d-0ee7-4b17-9a1c-084d0b9b772c)

  ![image](https://github.com/user-attachments/assets/a8606fb8-1e41-4b48-8945-3a04ea11ab53)

  ![image](https://github.com/user-attachments/assets/cb32eff1-3e0c-4ab0-bbe7-cb9f66cc7cbf)


</p>

<br />
<p>
  
</p>
<h2>
  Configuring a Firewall 
</h2>

<br />
<p>

Next we go abck into Azure and go to the linux-vm and to network settings and to network security group. And to inbound security rules and create a new rule.

![image](https://github.com/user-attachments/assets/5ecb7a2f-5acf-486f-b714-be0b607382dd)

  ![image](https://github.com/user-attachments/assets/60ff0420-a313-461d-8e55-77994c7d40d0)

crate a new rule and put a * for both the source port ranges and destination port ranges, make the protocol ICMPv4 and the Action deny and priority 290, so the rule will be evaluated first.

![image](https://github.com/user-attachments/assets/bb8ac589-1c01-42ba-884f-c47465e4c1b1)

Back to PSh you will see in the terminal that "Request Timed out" means that the rule has been applied even though we are still pinging the vm ip address but no replys will come because the firewall is blocking them.

![image](https://github.com/user-attachments/assets/c8ae91ca-c40e-400d-9607-1bdd9d725107)

</p>
<br />

<p>


  
</p>

<br />

<p>
For this example we can delete this ICMP rule 

![Screenshot 2025-03-03 030320](https://github.com/user-attachments/assets/f7f81ce8-e2ea-4e28-ac1f-97f2367ab164)

![image](https://github.com/user-attachments/assets/cc44bafd-c1ef-4192-bf48-e4a34b76b673)

  
</p>

<br />

<p>

  Example using ssh azureuser@10.0.0.5
  ![image](https://github.com/user-attachments/assets/0c57648b-7ca4-41db-978f-bb3ab95d3227)

Example: Filter tcp.port == 22 and enter exit into power shell will show us from the windows vm to the linux vm that a restart packet was sent
  ![image](https://github.com/user-attachments/assets/edb6dd27-0277-4a4f-ac5e-97f5f55f13f4)

![image](https://github.com/user-attachments/assets/d147451d-d2a1-4968-bd0b-e48e4b37cc35)

</p>
