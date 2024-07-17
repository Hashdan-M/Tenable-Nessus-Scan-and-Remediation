<h1>Vulnerability Management With Tenable Nessus</h1>

<h2>Description</h2>
This project involves creating an interactive vulnerability management lab that simulates real-world cybersecurity scenarios. We will use Tenable Nessus Essentials as the vulnerability management software and VMWare as the virtualization software. Inside a virtual machine running Windows 10, we'll install old deprecated software by Mozilla Firefox and VLC Media Player to simulate typical security vulnerabilities. Through comprehensive vulnerability scans, we'll identify and analyze potential risks within the system. The final phase of the project will concentrate on implementing effective remediation strategies, providing hands-on experience in vulnerability management.
<br />

<h2>Utilities</h2>

- [<b>Tenable Nessus Essentials</b>](https://www.tenable.com/products/nessus/nessus-essentials) 
- [<b>VMWare</b>](https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html.html)
- [<b>Windows 10</b> ISO](https://www.microsoft.com/en-us/software-download/windows10)
- [<b>Mozilla Firefox</b>](https://ftp.mozilla.org/pub/firefox/releases/)
- [<b>VLC Media Player</b>](https://www.videolan.org/vlc/releases/)

<h2>Download software</h2>

Download and install [<b>VMWare Workstation Player</b>](https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html.html) and [<b>Windows 10</b> ISO](https://www.microsoft.com/en-us/software-download/windows10). Go to [<b>Tenable Nessus Essentials</b>](https://www.tenable.com/products/nessus/nessus-essentials) website to register for an account. On the downloads page, select "Tenable Nessus" and choose the version which has your host operating system. Click on "Connect via SSL" and create username and password. Run VMWare and create new virtual machine using the Windows 10 ISO. Ensure to click on "Customize Hardware" and select "Network Adapter" and change to "Bridged" so that the virtual machine will connect directly to the same network as the host machine. Install Windows 10 Pro on the virtual machine.

<h2>IP and Firewall Configuration</h2>
On the VM PC, run Command Prompt and type "ipconfig" to get the IPv4 Address. My IP is 192.168.213.128.
<br />
<br />

![ipconfig](https://raw.githubusercontent.com/Hashdan-M/images/main/ipconfig.PNG?token=GHSAT0AAAAAACU4JCPDPO342NBI3DNG66PIZUXSDMA)

<br />
Go to the VM PC and disable the Windows Firewall for all connections (Domain Profile, Private Profile & Public Profile) which would otherwise block all connection attempts from our host PC. 
<br />
<br />
On the host PC, run Command Prompt and ping the VM IP Adress to ensure that there is successful connection.
<br />
<br />

![Ping_works](https://user-images.githubusercontent.com/108043108/177887412-f8078e7b-13a3-4480-b000-5ae84108cfab.JPG)

<h2>Run scans</h2>
Go to the Nessus Essentials web page and on the "My Scans" page, click "Create a new scan", then select "Basic Network Scan". 
<br/>
<br/>

![basic_network_scan](https://user-images.githubusercontent.com/108043108/177887672-2d955508-edf1-4735-b78a-2836a81d2c9f.JPG)
<br />
<br />
Give a name to the scan and in "Targets" enter the VM's IP address which in my case is 192.168.213.128.

![Scan_VM_IP](https://user-images.githubusercontent.com/108043108/177887914-87a2da10-be51-481c-a672-ec1104e3df7a.JPG)

<br />
Click "Save" and "Launch" to begin the scan.
<br />
<br />

![Launch_newly_created_scan](https://user-images.githubusercontent.com/108043108/177888041-95c53001-b8d2-4355-9311-3ee2637dff94.JPG)

![Scan_Running](https://user-images.githubusercontent.com/108043108/177888049-661dddfc-ebe0-42cf-ad87-14bc5af53fe5.gif)

![Scan_Completed](https://user-images.githubusercontent.com/108043108/177888068-25d4a86a-c150-4e77-a993-9df4178c5ba1.JPG)

<br />
<br />
After a few minutes, the scan is completed. There is a total of 17 vulnerabilities and 32 total results, 30 of which are info. The info results are usually not vulnerabilities but still something that you should be aware of. There is 1 medium vulnerability named "SMB Signing not required" which may be further explored and remediated.
<br/>

![Results_Of_Scan](https://user-images.githubusercontent.com/108043108/177888196-3141c52f-df79-4c58-9fee-5daa68d78c5b.gif)

<br />
<br />
We have completed a non-credentialed scan. We will now configure the VM to be able to accept credentialed scans and rescan the VM to compare the results. Tenable Nessus recommends several steps before running the credentialed scans. Click on the links below for a step-by-step guide

- [Enable Remote Registry](https://success.trendmicro.com/dcx/s/solution/1039259-configuring-the-remote-registry-service-to-automatically-start-upon-log-on?language=en_US)
- [Disable Windows User Account Control (UAC)](https://www.howtogeek.com/247/disable-user-account-control-uac-the-easy-way-on-windows/)
- [Disable UAC remote restrictions](https://learn.microsoft.com/en-us/troubleshoot/windows-server/windows-security/user-account-control-and-remote-restriction)

<br />
<br />
With the registry configured, it is now time to go back into Nessus and configure the scan I created. I have to add the Credentials to the scan so it can work properly. The credentials I'm talking about is the username and password of the VM. This will allow Nessus to use those credentials in places where it is required in the VM registry.




![Configure_Nessus](https://user-images.githubusercontent.com/108043108/177890138-e6420231-4ce8-4a2d-99fb-e1e992da6ebb.JPG)

![Adding_Credentials](https://user-images.githubusercontent.com/108043108/177890151-27496a20-72b8-4763-8c82-368a06a15d3f.gif)

<br />
<br />
<p align="center">
<b>After the scan is properly configured with the right credentials, I run it again.</b> <br/>
</p>

![Run_The_Scan_Again](https://user-images.githubusercontent.com/108043108/177890377-b412d84a-d8e2-40da-9995-dddbd3c4d388.JPG)

<br />
<br />
<p align="center">
<b>This new scan has given us a lot more vulnerabilities than the first one because it is able to scan deeper into the VM due to having credentials. The top picture is the new credentialed scan and the bottom picture is from the first non-credentialed scan. Most of the vulnerabilities found is probably because the version of Windows 10 this VM is running is not up to date.</b> <br/>
</p>

![new_scan_properly_credentialed](https://user-images.githubusercontent.com/108043108/177890582-7f4d0eec-3b5f-4a5f-b708-47b3ccfb5d83.JPG)

![Old_scan_not_credentialed](https://user-images.githubusercontent.com/108043108/177890589-e4e882ab-6733-4930-ad4c-1115a2c620b3.JPG)

<br />
<br />
<p align="center">
<b>I want to see how powerful this Nessus Scanner is so I'm going to download a very old version of Firefox which probably has many vulnerabilities and see if Nessus can discover them (I'm sure it will.)</b><br/>
</p>

![downloading_an_old_version_of_firefox](https://user-images.githubusercontent.com/108043108/177890787-5cd80be3-99a1-40a4-bddc-feb06ea9cda7.JPG)

<br />
<br />
<p align="center">
<b>After a deprecated version of Firefox is downloaded, I run another scan. We can see many new alerts and vulnerabilities just from Firefox! 68 Critical!</b> <br/>
</p>

![Old_Firefox_Scan](https://user-images.githubusercontent.com/108043108/177890872-ed890db9-a15d-4de9-b3b3-6723dd161f22.JPG)

<br />
<br />
<p align="center">
<b>A comparison between scans to show the progression of alerts and vulnerabilities.</b>  <br/>
</p>

![Vulnerability_Comparison](https://user-images.githubusercontent.com/108043108/177890918-c2fc7078-34b9-4120-a430-f096169ae177.jpg)

<br />
<br />
<p align="center">
<b>Showing what some of the alerts and vulnerabilites look like. We can see most of the Critical alerts are just from Firefox. A few ways we can remediate some of the vulnerabilities is by either Updated Firefox, which will probably remediate a lot of them, or we can simply delete Firefox.</b>  <br/>
</p>

![Showing_Vulnerabilities](https://user-images.githubusercontent.com/108043108/177891162-cf86e335-0539-4f9f-abb2-7150b482e689.gif)

<br />
<br />
<p align="center">
<b>To start the process of remediating vulnerabilities, I elect to just delete Firefox. That will instantly fix a lot of these issues.</b>  <br/>
</p>

![Fixing_Vulnerabilities_Uninstall_Firefox](https://user-images.githubusercontent.com/108043108/177891363-17bdc0ea-c872-434f-95a6-4bf6e4694ddf.JPG)

<br />
<br />
<p align="center">
<b>To remediate the Windows vulnerabilities, I choose to update Windows. This version is old so it takes a few restarts to get it up to date.</b>  <br/>
</p>

![Remediating_Vulnerabilities_Updating_WIndows_1](https://user-images.githubusercontent.com/108043108/177891464-75d2b603-cadf-4923-bc1f-61409b11169d.gif)

![Remediating_Vulnerabilities_Updating_Windows](https://user-images.githubusercontent.com/108043108/177891436-a7b26e21-8376-4650-aaee-aaf4bc2e451e.JPG)

<br />
<br />
<p align="center">
<b>After a few restarts, Windows is finally up to date. I run one more Nessus scan to find if the steps I took to remediate some of the alerts worked.</b>  <br/>
</p>

![VM_Up_To_date](https://user-images.githubusercontent.com/108043108/177891501-767d6764-8e4a-4bd0-85cc-6b70e48c62aa.JPG)

<br />
<br />
<p align="center">
<b>Here is a final comparison between the four scans I took while doing this lab. The last picture is the after remediation scan. There we can see a lot of the vulnerabilities that were being alerted are gone! Still a 1 critical but I'll remediate that another time!</b>  <br/>
</p>

![After_Vulnerability_Remediation](https://user-images.githubusercontent.com/108043108/177891719-3066c9bb-38dd-4b10-b8bb-6f9dd8a45a09.JPG)

<br />
<br />


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
