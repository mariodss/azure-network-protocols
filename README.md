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

- Create two Virtual Machines
- Observe ICMP Traffic
- Configuring a Firewall [Network Security Group]
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

<p>
<img width="356" height="143" alt="image" src="https://github.com/user-attachments/assets/7e9337dc-0d75-4bed-9454-0bc7ebe6b483" />

</p>
<p>
<b>1) Create two Virtual Machines</b>

</p>
<p><b>1.1) </b>Create a Resource Group</p>
<br />

<p>
<img width="362" height="277" alt="image" src="https://github.com/user-attachments/assets/76aafc94-08fc-4952-a000-a4c2e3c8356a" />
<img width="295" height="205" alt="image" src="https://github.com/user-attachments/assets/94aff3d6-0826-4113-a42b-a40178fd14b5" />
<img width="325" height="223" alt="image" src="https://github.com/user-attachments/assets/1338e86a-4a97-457e-9dd5-c5642b0817f1" />


</p>
<p>
<p><b>1.2) </b>Create a Windows 10 Virtual Machine (VM).</p>
<p>-While creating the VM, select the previously created Resource Group.</p>
<p>-While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet.</p>

</p>
<br />

<p>
<img width="342" height="311" alt="image" src="https://github.com/user-attachments/assets/bd2394b4-0d35-42a1-af36-abb062390054" />
<img width="353" height="202" alt="image" src="https://github.com/user-attachments/assets/4b3b6730-8715-492c-a9b4-357c2f35a6fa" />
<img width="367" height="260" alt="image" src="https://github.com/user-attachments/assets/055946dc-e1e0-455e-abaf-dc99c210dc38" />


</p>
<p><b>1.3) </b>Create a Linux (Ubuntu) VM.</p>
<p>-While creating the VM, select the previously created Resource Group and Virtual Network—the Virtual Network MUST BE THE SAME.</p>
<br />

<p>
<img width="682" height="154" alt="image" src="https://github.com/user-attachments/assets/91213f38-8550-4141-be2f-2f508ce63c36" />
<img width="686" height="128" alt="image" src="https://github.com/user-attachments/assets/2ce5b835-6ad6-45ed-9a11-2ea89e20e551" />

</p>
<p><b>1.4) </b>Ensure both VMs are in the same Virtual Network / Subnet.</p>


<br />

<p>
<img width="304" height="106" alt="image" src="https://github.com/user-attachments/assets/52c89081-6266-48e7-a1a2-f13acffa302b" />
<img width="169" height="92" alt="image" src="https://github.com/user-attachments/assets/fbf70eeb-b502-454b-9cb9-a9b1d1e25e32" />
<img width="633" height="295" alt="image" src="https://github.com/user-attachments/assets/59c51778-0bb2-4a04-a002-cc99f1c9f92d" />


</p>
<p><b>2) Observe ICMP Traffic</b></p>
<p><b>2.1) </b>Use Remote Desktop to connect to your Windows 10 Virtual Machine. You will need to provide your public IP Address and username/password you created (If using Mac, install Microsoft Remote Desktop).</p>

<br />


<p>
<img width="635" height="349" alt="image" src="https://github.com/user-attachments/assets/2e4f1cfe-97fb-44cc-997b-ed224b9d878b" />
<img width="407" height="231" alt="image" src="https://github.com/user-attachments/assets/35487c6a-cd45-44ff-aaf8-e731c20cc2fe" />

</p>
<p><b>2.2) </b>Within your Windows 10 Virtual Machine, Install Wireshark</p>

<br />

<p>
<img width="656" height="242" alt="image" src="https://github.com/user-attachments/assets/1735f455-4493-4559-ae22-4642ff9e3a4c" />
<img width="654" height="363" alt="image" src="https://github.com/user-attachments/assets/ec93560a-8d3a-49c0-aca5-830a57c9e29f" />


</p>
<p><b>2.3) </b>Open Wireshark and start packet capture.</p>

<br />

<p>
<img width="530" height="233" alt="image" src="https://github.com/user-attachments/assets/c65ba471-a234-43f8-975b-699d806b164f" />


</p>
<p><b>2.4) </b>Within Wireshark, filter for ICMP traffic only.
</p>

<br />

<p>
<img width="595" height="329" alt="image" src="https://github.com/user-attachments/assets/40108dec-1bf5-460a-a844-0479f88f3667" />
<img width="548" height="308" alt="image" src="https://github.com/user-attachments/assets/3e6bf7c3-0a36-4a2e-9a2e-68449ee59173" />
<img width="631" height="374" alt="image" src="https://github.com/user-attachments/assets/9c2cd003-45d4-4779-a6b4-d7161d63992c" />


</p>
<p><b>2.5) </b>Retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM.
</p>
<p>-Observe ping requests and replies within WireShark</p>

<p><b>Observations</b></p>
<p>-ICMP, or Internet Control Message Protocol, is used for network diagnostics and error reporting. It operates at the network layer and is primarily used by network devices to send error messages and operational information. </p>
<p>-After pinging the Linux private IP address, we observe four events in the PowerShell terminal. However, in the Wireshark window, we see eight events. This occurs because Wireshark captures both the request packets from the Windows computer (10.0.0.4) and the reply packets from the Linux computer (10.0.0.5).</p>
<p>-If we click on either a request or a reply packet in the Wireshark interface, we can examine their specifications. When we click on the first request packet, we can view the source MAC address (Windows) and the destination MAC address (Linux) within the Internet Protocol Version 4 section. This represents OSI Layer 2 information.</p>
<p>-If we go to the Internet Control Message Protocol section, we can observe the actual payload(chunk of data) that was sent in the ping. This is not important since this ping was performed to test connectivity between two devices.</p>
<p>If we click on the second packet, we can inspect the Echo Reply from the Linux computer. Examining its specifications, we see almost the same information as before, but reversed. This time, the source is the Linux machine, and the destination is the Windows machine.</p>

<br />

<p>

<img width="646" height="317" alt="image" src="https://github.com/user-attachments/assets/ecdd94da-bc97-4111-8cd5-9db95d64a4bb" />


</p>
<p><b>3) Configuring a Firewall [Network Security Group]</b></p>
<p><b>3.1) </b>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM.</p>
</p>


<br />

<p>
<img width="562" height="194" alt="image" src="https://github.com/user-attachments/assets/17220507-d128-42d4-8f59-492d612a4293" />
<img width="568" height="331" alt="image" src="https://github.com/user-attachments/assets/2b46c1ef-6b07-4733-94e2-c3922d11470c" />


</p>

<p><b>3.2) </b>Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic.</p>

<br />

<p>
<img width="665" height="305" alt="image" src="https://github.com/user-attachments/assets/7c9b6f7e-88fc-4cb0-81f9-6222ec1ab2f6" />
<img width="554" height="191" alt="image" src="https://github.com/user-attachments/assets/e9f33bd4-319a-4ef5-93a5-d8a14b2f1d00" />


</p>

<p><b>3.3) </b>Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity.</p>

<br />

<p>
<img width="536" height="225" alt="image" src="https://github.com/user-attachments/assets/ba3140ce-3577-4201-94f7-9c6221fd14b7" />


</p>

<p><b>3.4) </b>Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using.</p>

<br />

<p>
<img width="611" height="188" alt="image" src="https://github.com/user-attachments/assets/0dbc9406-e587-4fe7-91b1-54927a03d11c" />

</p>

<p><b>3.5) </b>Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working).</p>

<br />

<p>
<img width="611" height="304" alt="image" src="https://github.com/user-attachments/assets/c2ceffab-e1b1-41d8-aa7a-40a40aec6c1e" />

</p>

<p><b>3.6) </b>Stop the ping activity</p>

<p><b>Observations</b></p>
<p>-By creating an inbound security rule for our Linux machine we can block ICMP traffic from any source. After applying this rule to our machine, if we ping the Linux machine through PowerShell, we observe the ping traffic timing out.</p>
<br />

<p>
<img width="493" height="266" alt="image" src="https://github.com/user-attachments/assets/7b3ab3ca-5cda-4250-b2bf-1770a336c9a2" />
<img width="260" height="164" alt="image" src="https://github.com/user-attachments/assets/2a5d7629-2096-4b6e-83a7-a24aade16449" />


</p>

<p><b>4) Observe SSH Traffic</b></p>
<p><b>4.1) </b>Back in Wireshark, start a packet capture and filter for SSH traffic only.
</p>

<br />

<p>
<img width="592" height="318" alt="image" src="https://github.com/user-attachments/assets/16da601a-179c-48cc-8e44-cb946bf33946" />
<img width="477" height="115" alt="image" src="https://github.com/user-attachments/assets/908aa86e-228d-4729-8ee5-6f14a7ec0b6f" />
<img width="604" height="323" alt="image" src="https://github.com/user-attachments/assets/7a2dcf33-7a23-4dcb-946e-978d9efeb731" />

</p>

<p><b>4.2) </b>From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address).</p>
<p><b>4.3) </b>Open PowerShell, and type: ssh labuser@<private IP address>.</p>
<p>-Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark</p>
<p>-Exit the SSH connection by typing ‘exit’ and pressing [Enter]</p>

<p><b>Observations</b></p>
<p>-SSH (Secure Shell) is used to make a secure connection with other computer. SSH uses TCP port 22. </p>
<p>-By entering the following command in PowerShell: ssh username@<private IP Adress>, we can connect remotely to another computer. We will need to provide a password as well. In our case we connected to the Linux machine from our Windows machine.</p>
<p>-We are able to use our Linux machine remotely. It is possible to interact with the Linux system by typing commands such as id, uname -a, touch file.txt, etc </p>
<p>-In Wireshark we observe the SSH traffic happening in the background. All traffic is encrypted. If we observe the SSH section, we see the encrypted payload that was transmitted.</p>
<p>-To terminate the connection, the exit command is entered in the PowerShell terminal.</p>
  
<br />


<p>
<img width="659" height="328" alt="image" src="https://github.com/user-attachments/assets/f68e6624-7e02-4575-9759-17efdc89a9b5" />
<img width="492" height="155" alt="image" src="https://github.com/user-attachments/assets/3fbdfbc2-2ea5-48b0-8e1f-ff3ae6b3bfea" />
<img width="386" height="370" alt="image" src="https://github.com/user-attachments/assets/ee771a4f-f971-4c66-a6e8-3cb14b14aee6" />
<img width="443" height="385" alt="image" src="https://github.com/user-attachments/assets/d6bad91e-b84f-4854-a423-a67972aca787" />
<img width="358" height="145" alt="image" src="https://github.com/user-attachments/assets/997ec591-c951-4f8a-866d-d12034e43ade" />


</p>

<p><b>5) Observe DHCP Traffic</b></p>
<p><b>5.1) </b>Back in Wireshark, filter for DHCP traffic only.</p>
<p><b>5.2) </b>From your Windows 10 VM, attempt to issue your VM a new IP address from the command line.</p>
<p>-Open PowerShell as admin and run: ipconfig /renew</p>
<p>-Observe the DHCP traffic appearing in WireShark</p>

<p><b>Observations</b></p>
<p>-The command ipconfig /release is the one that drops (releases) the current IP address.</p>
<p>-The command ipconfig /renew is used to request a new IP address from the DHCP server.</p>
<p>DHCP uses UDP ports 67 and 68.</p>
<p>There is a method by which we can activate both release and renew commands in PowerShell. We do this by creating a .bat file in the notepad application. We need to type both commands within the file and then if we type the command <filename.bat> in PowerShell, we should be able to release and renew at the same time. This is done to observe DHCP traffic in Wireshark.</p>
<p>By following the previous method, we can observe all the packets from the IP release/renewal process in the Wireshark interface. There are a total of five packets: Release, Discover, Offer, Request, and ACK. In summary, the IP address was released, and a process known as a broadcast began, in which a source address of 0.0.0.0 requested a new IP address from a DHCP server. After this, the DHCP server offered the IP address, and the computer accepted it.</p>
  
<br />


<p>
<img width="362" height="131" alt="image" src="https://github.com/user-attachments/assets/a0f0cc1a-687f-4dc0-9056-a0237a07943e" />
<img width="550" height="310" alt="image" src="https://github.com/user-attachments/assets/6d668130-1fa2-4c60-a4d8-35de23d578d3" />
<img width="548" height="209" alt="image" src="https://github.com/user-attachments/assets/d6f37c6b-7e53-4763-bcd1-5500e9254818" />

</p>

<p><b>6) Observe DNS Traffic</b></p>
<p><b>6.1) </b>Back in Wireshark, filter for DNS traffic only.</p>
<p><b>6.2) </b>From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are</p>
<p>-Observe the DNS traffic being show in WireShark</p>

<p><b>Observations</b></p>
<p>nslookup (short for Name Server Lookup) is a command-line tool used to query Domain Name System (DNS) servers to obtain information about domain names, IP addresses, or DNS records.</p>
<p>By using the nslookup command, we can obtain the IP addresses associated with domains such as pixar.com or google.com.</p>
<p>DNS uses UDP port 53 and TCP port 53.</p>




<br />

<p>
<img width="545" height="275" alt="image" src="https://github.com/user-attachments/assets/d313b296-5f54-49f8-a4c0-75018cb0ca44" />


</p>

<p><b>7) Observe RDP Traffic</b></p>
<p><b>7.1) </b>Back in Wireshark, filter for RDP traffic only (tcp.port == 3389).</p>
<p><b>7.2) </b>Observe the immediate non-stop spam of traffic</p>
<p><b>Observations</b></p>
<p>- RDP (Remote Desktop protocol) is constantly showing you a live stream from one computer to another.Therefore, traffic is always being transmitted.</p>
<p>The difference between SSH and RDP is that SSH only sends traffic when a command is entered and executed on the Linux (or other) server. In contrast, RDP is more bandwidth-intensive because it continuously transmits graphical data — essentially sending a live stream of the remote desktop’s display.</p>

<br />
