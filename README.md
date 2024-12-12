<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we analyze various network traffic flows to and from Azure Virtual Machines using Wireshark and explore the functionality of Network Security Groups.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Windows and Linux Command Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 22.04

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/EwX8Y7s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/JGhlxJJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create two VMs in the Azure portal: one using a Windows 10 Pro image and the other using a Linux image, each with 2 vCPUs. Ensure both VMs are attached to the same virtual network during setup. Use RDP to access the Windows machine.
</p>
<br />

<p>
<img src="https://i.imgur.com/1BYvdJZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Download and install Wireshark from https://www.wireshark.org. This tool will be used to observe network traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/3gTUIDW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After installing Wireshark, open the application and filter for ICMP traffic in the search bar. ICMP is used by network devices to send error messages and check connectivity.
</p>
<br />

<p>
<img src="https://i.imgur.com/HgLp5AR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open PowerShell and use the ping command to test the connectivity to the private IP address of the Linux machine, which is on the same network. You can find the Linux machine's private IP address in the Azure portal under the VM's network settings.
</p>
<br />

<p>
<img src="https://i.imgur.com/nurPwTN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You can view each packet sent while pinging the machine in Wireshark, displaying the ICMP traffic for analysis. 
</p>
<br />

<p>
<img src="https://i.imgur.com/X4yfgee.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, use the ping -t command to continuously ping the Linux machine. Then, go to the Linux VM in Azure, navigate to Network Settings, and create an inbound port rule to deny ICMP traffic, effectively blocking it on the firewall.
</p>
<br />

<p>
<img src="https://i.imgur.com/UvdXvva.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After blocking ICMP traffic on the Linux machine’s firewall, check Wireshark to see that the pings no longer receive replies. In PowerShell, you’ll see a message saying "Request Timed Out."
</p>
<br />

<p>
<img src="https://i.imgur.com/QstVuqS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Afterward, delete the inbound port rule to allow ICMP traffic again. To stop the continuous pinging, press Ctrl + C in PowerShell. 
</p>
<br />

<p>
<img src="https://i.imgur.com/5sVds9j.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we will filter SSH traffic using Wireshark. By now, you should have a basic understanding of how to navigate Wireshark. To proceed, open the command prompt on your Windows machine and establish an SSH connection to the Linux machine using the command: ssh labuser2@10.0.0.5. Once this command is executed, Wireshark will display the SSH traffic, allowing you to observe and analyze it in real time.You can type "exit" to end the linux SSH connection when you're done.
</p>
<br />

<p>
<img src="https://i.imgur.com/WlKABeY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we'll filter DNS traffic in Wireshark. Start by setting Wireshark to display only DNS traffic. To generate DNS activity, use the command nslookup www.yahoo.com, which queries the DNS server for Yahoo's IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/afL911f.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, we'll use Wireshark to filter DHCP traffic. DHCP, or Dynamic Host Configuration Protocol, assigns IP addresses to devices. To generate DHCP traffic, enter the command ipconfig /renew in PowerShell, which requests a new IP address. Wireshark will capture this DHCP activity for analysis.
</p>
<br />

<p>
<img src="https://i.imgur.com/KUhVqBe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, we'll filter for RDP traffic in Wireshark. Since we're using Remote Desktop Protocol to connect to our virtual machine, RDP traffic will appear continuously, providing ample data for analysis.
</p>
<br />
