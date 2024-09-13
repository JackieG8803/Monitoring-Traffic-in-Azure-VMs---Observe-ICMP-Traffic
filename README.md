<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Monitoring Traffic in Azure VMs - Observe ICMP Traffic</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- ICMP Network Protocol
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro
- Ubuntu Server 22.04

<h2>Actions and Observations</h2>

<p>
<img src="https://github.com/user-attachments/assets/ff39cf3c-65c4-4035-acce-89a2fd0f5283" height="80%" width="80%" alt="Remote Desktop"/>
</p>
<p>
Get Remote Desktop ready. You can type mstsc.exe into your search bar (if running Windows) or download Microsoft Remote Desktop on Mac.
  Make sure you copy the PUBLIC IP address of your Windows VM and paste it into Remote Desktop Connection. Log in with your created Administrator Account. Click "yes" to continue and you should now be connecting to your Windows VM. 

  Next, we are going to download WireShark (Network Protocol Analyzer) to view our network activity between our VMs.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/64fc53c1-92d9-4fa7-a185-b68a39c6dfd6" height="80%" width="80%" alt="WireShark"/>
</p>
<p>
Go ahead and install WireShark - just make sure to install NPcap (allows us to capture packets). Open WireShark.

  Now we want to filter to view only ICMP traffic, otherwise we will be spammed with all network traffic.
  
  Click Ethernet to expand the view. In "Add a display filter" type "ICMP" and press Enter. 
Now, we will only view ICMP traffic.
![Screenshot 2024-09-13 153225](https://github.com/user-attachments/assets/41c602e9-8a70-4c82-b9a6-9b46352cd38d)

Next, we will "ping" to our Linux VM to view the network activity between the two VMs. 

Navigate to your Azure Portal > Virtual Machines > Select Linux VM > copy PRIVATE IP Address

Go back to your Windows VM, open PowerShell, type Ping [Linux Private IP]

Hit Enter.
![Screenshot 2024-09-13 153446](https://github.com/user-attachments/assets/bf1cd0a0-478c-426e-a349-95d31d7670ee)

Now we will see an influx of information in WireShark. Take note of the following information: Source, Destination, and Request/Reply.

![Screenshot 2024-09-13 153520](https://github.com/user-attachments/assets/9d92f1ff-8948-4bae-bb03-dbe04f7a44c7)

Notice that your Windows VM is the Source sending requests, and the Linux VM is sending replies. 
We can confirm this with the "ipconfig" command in PowerShell.
Navigate back to PowerShell and type "ipconfig /all"

Take note of the Physical Address.

In WireShark, you can confirm the MAC address of your Windows VM in the bottom-left pane, under Ethernet II > Source.

![Screenshot 2024-09-13 154211](https://github.com/user-attachments/assets/c9e58caa-b269-4dd2-b03b-638e6f9fb73d)

That's it! Now we have observed network traffic between our two VMs!
