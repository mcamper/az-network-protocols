<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

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

- Step 1: Create our Resources
- Step 2: Observe ICMP Traffic
- Step 3: Observe SSH Traffic
- Step 4: Observe DHCP Traffic
- Step 5: Observe DNS Traffic
- Step 6: Observe RDP Traffic
- Step 7: Cleanup

<h2>Actions and Observations</h2>

<p>
<img width="952" alt="Screenshot 2025-03-27 045909" src="https://github.com/user-attachments/assets/db66094d-263d-4908-bb9e-5878ecabff0f" />

</p>
<h2>Step 1: Create our Resources</h2>
<p>
  <ol>
  <li>Create a Resource Group</li>
  <li>Create a Windows 10 Virtual Machine (VM)</li>
    <ul>
  <li>While creating the VM, select the previously created Resource Group</li>
  <li>While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet</li>
</ul>
  <li>Create a Linux (Ubuntu) VM</li>
    <ul>
  <li>While creating the VM, select the previously created Resource Group and Vnet</li>
</ul>
  <li>Observe your Virtual Network within Network Watcher</li>
</ol>

</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>Step 2: Observe ICMP Traffic</h2>
<p>
  <ol>
  <li>Use Remote Desktop to connect to your Windows 10 Virtual Machine (VM)</li>
  <li>Within your Windows 10 VM, intall Wireshark</li>
  <li>Open Wireshark and filter for ICMP traffic only</li>
  <li>Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM</li>
    <ul>
  <li>Observe ping requests and replies within Wirehhark.</li>
    </ul>
  <li>From the Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in Wireshark.</li>
  <li>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM </li>
    <ul>
      <li>Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic</li>
      <li>Back in the Windows 10 VM, observe the ICMP traffic in Wireshark and teh command line ping activity</li>
      <li>Re-enable the ICMP traffic for the Network Security Group your ubuntu VM is using</li>
      <li>Back in the Windows 10 VM, observe the ICMP traffic in Wireshark and the command line ping activity (should start working)</li>
      <li>Stop the ping activity, Ctrl + C</li>
    </ul>
</ol>
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br /># az-network-protocols
