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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

<p>
<img width="356" height="143" alt="image" src="https://github.com/user-attachments/assets/7e9337dc-0d75-4bed-9454-0bc7ebe6b483" />

</p>
<p>
<b>1) </b>Create two Virtual Machines

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
<p><b>2) </b>Observe ICMP Traffic</p>
<p><b>2.1) </b>Use Remote Desktop to connect to your Windows 10 Virtual Machine. You will need to provide your public IP Address and username/password you created (If using Mac, install Microsoft Remote Desktop)</p>


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
<p><b>2.3) </b>Open Wireshark and start packet capture</p>

<br />

<p>
<img width="530" height="233" alt="image" src="https://github.com/user-attachments/assets/c65ba471-a234-43f8-975b-699d806b164f" />


</p>
<p><b>2.4) </b>Within Wireshark, filter for ICMP traffic only
</p>

<br />

<p>
<img width="595" height="329" alt="image" src="https://github.com/user-attachments/assets/40108dec-1bf5-460a-a844-0479f88f3667" />
<img width="548" height="308" alt="image" src="https://github.com/user-attachments/assets/3e6bf7c3-0a36-4a2e-9a2e-68449ee59173" />
<img width="631" height="374" alt="image" src="https://github.com/user-attachments/assets/9c2cd003-45d4-4779-a6b4-d7161d63992c" />


</p>
<p><b>2.5) </b>Retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM
</p>
<p>-Observe ping requests and replies within WireShark</p>
<br />

<p>

<img width="646" height="317" alt="image" src="https://github.com/user-attachments/assets/ecdd94da-bc97-4111-8cd5-9db95d64a4bb" />


</p>
<p><b>3) </b>Configuring a Firewall [Network Security Group]
</p>
<p><b>3.1) <b/>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM.</p>

<br />

<p>
<img width="562" height="194" alt="image" src="https://github.com/user-attachments/assets/17220507-d128-42d4-8f59-492d612a4293" />
<img width="568" height="331" alt="image" src="https://github.com/user-attachments/assets/2b46c1ef-6b07-4733-94e2-c3922d11470c" />


</p>

<p><b>3.2) <b/>Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic.</p>

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

<p>Stop the ping activity.</p>

<br />
