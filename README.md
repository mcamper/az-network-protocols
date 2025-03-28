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
<p>
<img width="952" alt="Screenshot 2025-03-27 045909" src="https://github.com/user-attachments/assets/db66094d-263d-4908-bb9e-5878ecabff0f" />

</p>
<br />

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
<p>
<img width="319" alt="remote" src="https://github.com/user-attachments/assets/9c5eee0d-1157-4acc-83af-331eba9b5f62" /></p>

<br />
<img width="721" alt="icmp" src="https://github.com/user-attachments/assets/2589b441-96ee-4636-b85c-1f6250198701" />

<br />
<img width="726" alt="pingprivIP_pinggoogle" src="https://github.com/user-attachments/assets/7584dd0e-7896-42c2-8caa-b42889f02136" />
<img width="934" alt="Screenshot 2025-03-27 051000" src="https://github.com/user-attachments/assets/cce3c915-7c0a-4bc3-80d8-bb85105477c1" />
<img width="649" alt="Screenshot 2025-03-27 051733" src="https://github.com/user-attachments/assets/5dbc2fe1-f7b1-45ef-b73b-68af633b5a96" />
<img width="1026" alt="Screenshot 2025-03-27 052450" src="https://github.com/user-attachments/assets/8b987871-917c-4671-9640-d49b3c725a81" />
<img width="677" alt="Screenshot 2025-03-27 052623" src="https://github.com/user-attachments/assets/06540a92-1f7c-440f-b2e9-16d52d7c5a9f" />

</p>
<br />

</p>
<h2>Step 3: Observe SSH Traffic</h2>
<p>
  <ol>
    <li>Back in Wireshark, filter for SSH traffic only</li>
    <li>From your Windows 10 VM, "SSH into" your Ubuntu Virtual Machine (via its private IP address)</li>
      <ul>
        <li>Type commands (username, password, etc.) into the Linux SSH connection and observe SSH traffic spam in Wireshark/li>
        <li>Exit the SSH connecton by typing "exit" and pressing "Enter"</li>
      </ul>
  </ol>
</p>
<p>
<img width="224" alt="Screenshot 2025-03-27 053108" src="https://github.com/user-attachments/assets/2af8079d-dfe7-491a-b0c9-73a7537b83e8" />
<img width="338" alt="Screenshot 2025-03-27 053249" src="https://github.com/user-attachments/assets/912aaef2-5bfe-4c6d-87c7-51f7fc3e3929" />
<img width="802" alt="Screenshot 2025-03-27 053317" src="https://github.com/user-attachments/assets/a1eccd23-e404-4378-ab7b-857d00771a58" />
<img width="810" alt="Screenshot 2025-03-27 053644" src="https://github.com/user-attachments/assets/f8ebda7c-3be9-4d80-a19e-9acd5027b967" />
<img width="334" alt="Screenshot 2025-03-27 054230" src="https://github.com/user-attachments/assets/30e6a3c6-c87c-42bb-9c9e-ca2a03407f65" />
</p>
<br />

</p>
<h2>Step 4: Observe DHCP Traffic</h2>
<p>
  <ol>
    <li>Back in Wireshark, filter for DHCP traffic only</li>
    <li>From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)</li>
      <ul>
        <li>Observe the DHCP traffic appearing in Wireshark</li>
      </ul>
  </ol>
</p>  
<p>
<img width="511" alt="dhcpcopy" src="https://github.com/user-attachments/assets/55d291f9-3fc9-479c-9710-f68649da4764" />

</p>
<br />

</p>
<h2>Step 5: Observe DNS Traffic</h2>
<p>
  <ol>
    <li>Back in Wireshark, filter for DNS traffic only</li>
    <li>From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com's IP addresses are</li>
      <ul>
        <li>Observe the DNS traffic being shown in Wireshark</li>
      </ul>
  </ol>
</p>  
<p>
<img width="169" alt="Screenshot 2025-03-27 054955" src="https://github.com/user-attachments/assets/abe34408-627b-4d9f-8193-a4a8fb9032be" />
<img width="667" alt="Screenshot 2025-03-27 055025" src="https://github.com/user-attachments/assets/a8bbd644-6023-4034-b2f8-259111a55c72" />
</p>
<br />

</p>
<h2>Step 6: Observe RDP Traffic</h2>
<p>
  <ol>
    <li>Back in Wireshark, filter for RDP traffic only (tcp.port==3389)</li>
    <li>Observe the immediate non-stop spam of traffic. </li>
  </ol>
</p> 
<p>
<img width="484" alt="Screenshot 2025-03-27 055356" src="https://github.com/user-attachments/assets/11971178-b129-4c28-a0d2-09418e026010" />

</p>
<br />

<h2>Step 7: Lab Cleanup (A MUST!)</h2>
<p>
  <ol>
    <li>Close your Remote Desktop connection</li>
    <li>Delete the Resource Group(s) created at the beginning of this lab</li>
    <li>Verify Resource Group Deletion</li>
  </ol>
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br /># az-network-protocols
