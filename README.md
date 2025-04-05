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
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
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


<h2>Step 1: Create our Resources in Microsoft Azure</h2>
<p>
  <ol>
  <li>Create a Resource Group (RS-NSG)</li>
    <img width="461" alt="image" src="https://github.com/user-attachments/assets/3fc126e1-6ca0-4db8-b7ac-2e675101b9b0" />

  <li>Create a Windows 10 Virtual Machine (VM)</li>
    <ul>
  <li>While creating the VM (Windows-VM), select the previously created Resource Group (RS-NSG)</li>
    <img width="494" alt="image" src="https://github.com/user-attachments/assets/8d69c74c-be70-4235-83b4-b02ce794eebb" />

  <li>For Image, choose Windows 10. For Size, choose at least 2vcpus or DS2sv</li>
  <img width="520" alt="Screenshot 2025-04-04 070032" src="https://github.com/user-attachments/assets/d6a1c2c9-5b2b-4e99-8263-52eadeb0df16" />

  <li>Enter a username and password (username: labuser  password: Cyberlab123!)</li>
  <img width="518" alt="Screenshot 2025-04-04 070314" src="https://github.com/user-attachments/assets/15eb8459-e5fc-4321-9f4a-6bcdc01eb775" />

  <li>Do not change any other settings</li>
  <li>While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet, by clicking "Review and Create"</li>
 <img width="478" alt="image" src="https://github.com/user-attachments/assets/82519c5e-bb82-4a8d-9c38-6afcdc3400eb" />

  <img width="320" alt="image" src="https://github.com/user-attachments/assets/10add3ab-c9f7-4c21-8961-48de72ea46da" />


  <li>Click "Create"</li>
</ul>
  <li>Create a Linux (Ubuntu) VM</li>
    <ul>
  <li>While creating the VM (Linux-VM), select the previously created Resource Group (RS-NSG)</li>
      <img width="506" alt="image" src="https://github.com/user-attachments/assets/22d016db-ce67-45a9-bdde-508c11acccf5" />

  <li>For Image, choose Ubuntu Server 22.04 LTS - x64 Gen2 or 24. For Size, choose at least 2vcpus or DS2sv</li>
  <img width="497" alt="image" src="https://github.com/user-attachments/assets/ab72af90-922f-4420-8e1a-1cb79660230a" />

  <li>For Authentication type, choose Password.  Enter a username and password (username: labuser  password: Cyberlab123!) </li>
  <img width="542" alt="image" src="https://github.com/user-attachments/assets/691404a2-7720-461e-92c6-1dc854d93fc2" />
  <img width="518" alt="image" src="https://github.com/user-attachments/assets/ccb6fbd2-58e6-4810-9004-9cbb9bfab934" />


  <li>Do not change any other settings</li>
  <li>Click Next: Disks.  Click: Next: Networking</li>
  <img width="298" alt="image" src="https://github.com/user-attachments/assets/f1262388-03c9-4aa7-8420-a93a15ff4b84" />

  <li>Inside Networking, confirm correct Virtual Network and Subnet that was created in Windows-VM</li>
  <img width="350" alt="image" src="https://github.com/user-attachments/assets/7dafc92d-f07e-4b94-a4aa-f085d4daf9eb" />


  <li>Click "Review and Create"</li>
  <img width="288" alt="image" src="https://github.com/user-attachments/assets/4cae5865-bb3a-43af-a9ba-a6680cbc2d56" />

  <li>Click "Create"</li>
</ul>
  <li>Observe your Virtual Machines</li>
  <img width="805" alt="image" src="https://github.com/user-attachments/assets/dc353543-b89b-40b3-8572-a139e00014cb" />
</ol>
</p>

<p>
<h2>Step 2: Observe ICMP Traffic</h2>
<p>
  <ol>
  <li>Use Remote Desktop to connect to your Windows 10 Virtual Machine (VM)</li>
    <ul>
      <li>Open and paste the Windows-VM Public IP Address. </li>
      <img width="792" alt="image" src="https://github.com/user-attachments/assets/d6f4a0b8-8093-4089-a369-c6fbf7291630" />
      <li>Go to Search inside Windows desktop and search for "Remote Desktop Connection" </li>  
      <li>You can ignore random username, then click "Connect"</li>
      <img width="309" alt="image" src="https://github.com/user-attachments/assets/53ea929b-c637-46a2-bcbd-7b342887de59" />
      <li>Enter your credentials - User name: labuser  Password: Cyberlab123!. Click "Yes" on Security Certificate prompt </li>
      <img width="284" alt="image" src="https://github.com/user-attachments/assets/9bea4db6-1e78-4be6-905e-1c1557741752" />
      <img width="263" alt="image" src="https://github.com/user-attachments/assets/1caa83ec-7d18-429f-b92a-6f69ab0b3dff" />
     </ul>
   <li>Within your Windows 10 VM, install Wireshark. Use all default settings. Then close browser.</li>
      <img width="163" alt="image" src="https://github.com/user-attachments/assets/30595dac-d136-4b2d-a2bc-5530768b6892" />

   <li>Open Wireshark, double click on Ethernet line. Filter for ICMP traffic only</li>
      <img width="442" alt="image" src="https://github.com/user-attachments/assets/d287f0b2-b7a8-4d52-ae07-a844fd7fd6f9" />
      <img width="476" alt="image" src="https://github.com/user-attachments/assets/a3f3b857-a9df-4f23-be4c-0ebeb5b34cd9" />

   <li>Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM</li>
     <ul>
      <img width="619" alt="image" src="https://github.com/user-attachments/assets/2b325b19-c8b9-4573-ab5b-240f6d7ac412" />
       <li>From the Windows 10 VM, open command line or PowerShell </li>
       <img width="490" alt="image" src="https://github.com/user-attachments/assets/322a72b5-0c4c-4371-aff2-ba4d0484c42a" />
       <li>Attempt to ping Ubuntu VM and observe the traffic in Wireshark. Observe ping requests and replies within Wireshark.</li>
      <img width="721" alt="icmp" src="https://github.com/user-attachments/assets/2589b441-96ee-4636-b85c-1f6250198701" />  
      </ul>
  <li>Attempt to ping a public website (such as www.google.com) and observe the traffic in Wireshark.</li>
    <img width="726" alt="pingprivIP_pinggoogle" src="https://github.com/user-attachments/assets/7584dd0e-7896-42c2-8caa-b42889f02136" />
  <li>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM </li>
    <ul>
      <li>Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic</li>
      <img width="970" alt="image" src="https://github.com/user-attachments/assets/0163e326-7182-42ea-9c88-ee43426298c9" />
      <img width="434" alt="image" src="https://github.com/user-attachments/assets/e62db2f3-176b-40a5-ae6b-e7834becf52e" />
      <img width="440" alt="image" src="https://github.com/user-attachments/assets/5ca54dd2-bde0-4a57-8d7b-4725844ad9b0" />
      <li>Back in the Windows 10 VM, observe the ICMP traffic in Wireshark and the command line ping activity</li>
      <img width="718" alt="image" src="https://github.com/user-attachments/assets/d61fbf6c-5f9e-4d73-b784-f372497e2a90" />
      <li>Re-enable the ICMP traffic for the Network Security Group your Ubuntu VM is using, by deletion</li>
      <img width="1026" alt="Screenshot 2025-03-27 052450" src="https://github.com/user-attachments/assets/8b987871-917c-4671-9640-d49b3c725a81" />
      <li>Back in the Windows 10 VM, observe the ICMP traffic in Wireshark and the command line ping activity (should start working)</li>
      <img width="677" alt="Screenshot 2025-03-27 052623" src="https://github.com/user-attachments/assets/06540a92-1f7c-440f-b2e9-16d52d7c5a9f" />
      <li>Stop the ping activity, Ctrl + C. Inside Wireshark, stop captures.</li>
    </ul>
</ol>
</p>

<h2>Step 3: Observe SSH Traffic</h2>
<p>
  <ol>    
    <li>From your Windows 10 VM, "SSH into" your Ubuntu Virtual Machine (via its private IP address)</li>
      <ul>
        <img width="215" alt="image" src="https://github.com/user-attachments/assets/5a84e236-66fc-492b-a234-fb8c636c5da9" />
        <li>Type commands (username, password, etc.) into the Linux SSH connection. Note when typing password nothing appears. After typing, password press "Enter"</li>
          <img width="332" alt="image" src="https://github.com/user-attachments/assets/3e63b1e2-7f53-49d1-bc2d-c1d576419849" /> <br>
          <img width="338" alt="image" src="https://github.com/user-attachments/assets/3e7828d1-f788-4187-b160-7163537bf480" />
        <li>Back in Wireshark, filter for SSH traffic only. Observe SSH traffic spam in Wireshark</li>
          <img width="478" alt="image" src="https://github.com/user-attachments/assets/9a9fe27d-6c03-44ea-95c3-f0c30b14dbb1" />
        <li>Exit the SSH connecton by typing "exit" and pressing "Enter"</li>
          <img width="151" alt="image" src="https://github.com/user-attachments/assets/0c7f16b6-4959-4582-9b1f-d31ff206ef67" />
      </ul>
  </ol>
</p>
<h2>Step 4: Observe DHCP Traffic</h2>
<p>
  <ol>  
    <li>Create and Run a DHCP Trigger Script in Windows 10 VM</li>
     <ul>
        <li>Open Notepad and add the following code: ipconfig /release "Enter", ipconfig /renew</li>
        <img width="167" alt="image" src="https://github.com/user-attachments/assets/81698410-1763-484a-a9f7-912ab79766fd" />
        <li>Save on Desktop as a .bat file. Name it: dhcp_trigger.bat. Save as type: All Files</li>
        <img width="475" alt="image" src="https://github.com/user-attachments/assets/cfe13887-74ac-4216-b960-b7587d8de116" />
      </ul>
    <li>From the Windows 10 VM, open command line or PowerShell as "Administrator" </li>
      <img width="278" alt="image" src="https://github.com/user-attachments/assets/3d7ded07-a9d5-4443-9942-eaf423f98dba" />
    <li>Make sure Wireshark is running before you run the script </li>
    <li>Run the .bat file from Powershell</li>
      <ul>
        <li>Navigate to the directory where dhcp_trigger.bat is saved, then run it.</li>
        <img width="167" alt="image" src="https://github.com/user-attachments/assets/2183ae76-0b6b-4ca6-9925-10f26f6424f9" />
        <img width="430" alt="image" src="https://github.com/user-attachments/assets/664e7733-f389-4cce-835e-c413339382e1" />
        <li>Save on Desktop as a .bat file. Name it: dhcp_trigger.bat. Save as type: All Files</li>
      </ul>
    <li>From the Windows 10 VM, open command line or PowerShell "Administrator" </li>
    <li>From the Windows 10 VM, open command line or PowerShell "Administrator" </li>
    <li>From the Windows 10 VM, open command line or PowerShell "Administrator" </li>  
    <li>From your Windows 10 VM, attempt to issue your VM a new IP address from the command line </li>
      <ul>
        <li>Identify Your Network Interface</li>     
        <img width="430" alt="image" src="https://github.com/user-attachments/assets/664e7733-f389-4cce-835e-c413339382e1" />
        <img width="488" alt="image" src="https://github.com/user-attachments/assets/0ee90433-3858-474b-bd98-f640e4ab4dfb" />


        <li>Renew the DHCP Lease - ipconfig /renew</li>
        <li>Use this Wireshark filter to isolate DHCP traffic: bootp</li>
        <li>Observe the DHCP traffic appearing in Wireshark: DHCP Discover, DHCP Offer, DHCP Request, DHCP ACK</li>
        <li>Back in Wireshark, filter for DHCP traffic only</li>
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
