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


