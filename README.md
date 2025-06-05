<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (RDH, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Getting Started</h2>

- Create both VM's with their respected OS and be sure to connect both VM's to same Virtual Netowrk
- Open both VM's using Remote Desktop

<h2>Observing ICMP Traffic</h2>
Within The Windows 10 VM, open wireShark.org and dowload the program

<<img width="305" alt="image" src="https://github.com/user-attachments/assets/b186a878-b32f-4ef0-b86d-b76572952b01" />
>
Open WireShark and click on ethernet, then, click the blue fin at the top left to beging obsserving traffic between the two VM's. Also, known as a packet capture.

<<img width="335" alt="image" src="https://github.com/user-attachments/assets/bd17aa41-a816-4c17-8617-830c88e661ec" />
>
Next, in the search bar filter for "ICMP" traffic. There will not be any traffic coming through. Get the private IP address of the Ubuntu VM. Go back to the Windows VM and open up PowerShell and type "ping *private IP adress of the Ubuntu VM*" You should then see ping traffic between the two VM's. 

<img width="554" alt="image" src="https://github.com/user-attachments/assets/1681b821-e8d6-4892-8baa-2591e286194f" />

<img width="479" alt="image" src="https://github.com/user-attachments/assets/69606e3a-1c1f-46e4-a019-48a8f3cc04d8" />

<img width="824" alt="image" src="https://github.com/user-attachments/assets/ef82ca00-8c94-4b16-ad7b-92ebb80134b9" />

<h2>Observing RPD Traffic</h2>

In Wireshark, filter for RDP traffic only (tcp.port == 3389)

<img width="871" alt="image" src="https://github.com/user-attachments/assets/106f4098-f4ed-4828-9b0c-c599eaf6358d" />

RDP traffic is spamming through WireShark because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted
<br />
<h2>Configuring a Firewall [Network Security Group]</h2>
Starting in the Windows VM, start a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM.
<>

  <img width="310" alt="image" src="https://github.com/user-attachments/assets/8d6f13d9-8a45-4f8d-9c6b-4d3521be71a1" />

Next, Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
  
Inside Azure go to Ubuntu VM network settings and click on the Network Security Group and then go to settings and then click on *Inbound Security Rules*
  
Click "Add" set destination port ranges to * , for the protocool set it to ICMPv4. for the action select *Deny* , and for the priority set to *290*

<img width="254" alt="image" src="https://github.com/user-attachments/assets/160362c7-6564-4c2b-abce-a3bda14d383b" />

Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity

<img width="386" alt="image" src="https://github.com/user-attachments/assets/a15c5e3b-16fd-4981-b2a7-2ff1c2e5eb4b" />

<img width="814" alt="image" src="https://github.com/user-attachments/assets/0a48875e-a618-445b-8b2f-7415a226feaa" />

To re-enable ICMP traffic for the Network Security Group your Ubuntu VM, delete the rule made in Azure.

<img width="779" alt="image" src="https://github.com/user-attachments/assets/72a51b7f-4372-4310-8d23-56630c0b6a25" />


</p>
<p>

</p>
<br />
