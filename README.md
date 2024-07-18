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
On the VM PC, run Command Prompt and type "ipconfig" to get the IPv4 Address. Our IP is 192.168.213.128.
<br />
<br />

![ipconfig](https://download-files.wixmp.com/raw/25f80d_01599ac489fa47f68e5f64b83fb39393.png?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ1cm46YXBwOmU2NjYzMGU3MTRmMDQ5MGFhZWExZjE0OWIzYjY5ZTMyIiwic3ViIjoidXJuOmFwcDplNjY2MzBlNzE0ZjA0OTBhYWVhMWYxNDliM2I2OWUzMiIsImF1ZCI6WyJ1cm46c2VydmljZTpmaWxlLmRvd25sb2FkIl0sImlhdCI6MTcyMTI5OTk2MCwiZXhwIjoxNzIxMzAwODcwLCJqdGkiOiI5N2ZiNmI1OC1kYzkzLTQ2ZTItOWFlOC1iZmRmMjdmZmNkNjkiLCJvYmoiOltbeyJwYXRoIjoiL3Jhdy8yNWY4MGRfMDE1OTlhYzQ4OWZhNDdmNjhlNWY2NGI4M2ZiMzkzOTMucG5nIn1dXSwiZGlzIjp7ImZpbGVuYW1lIjoiaXBjb25maWcucG5nIiwidHlwZSI6ImlubGluZSJ9fQ.H_vORo8ZT2EdqMpBt5UXRiZ0rm_-yxKYmiOV8Shyl6A)

<br />
Go to the VM PC and disable the Windows Firewall for all connections (Domain Profile, Private Profile & Public Profile) which would otherwise block all connection attempts from our host PC. 
<br />
<br />

![firewall](https://download-files.wixmp.com/raw/25f80d_34d7ed7cd1974f96aaa327fd1df349f6.png?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ1cm46YXBwOmU2NjYzMGU3MTRmMDQ5MGFhZWExZjE0OWIzYjY5ZTMyIiwic3ViIjoidXJuOmFwcDplNjY2MzBlNzE0ZjA0OTBhYWVhMWYxNDliM2I2OWUzMiIsImF1ZCI6WyJ1cm46c2VydmljZTpmaWxlLmRvd25sb2FkIl0sImlhdCI6MTcyMTMwMDAzMywiZXhwIjoxNzIxMzAwOTQzLCJqdGkiOiJjYTY5OGU5MC1iZDNiLTRlN2EtYTE2NS0xZjE3NGQwZmIyZTYiLCJvYmoiOltbeyJwYXRoIjoiL3Jhdy8yNWY4MGRfMzRkN2VkN2NkMTk3NGY5NmFhYTMyN2ZkMWRmMzQ5ZjYucG5nIn1dXSwiZGlzIjp7ImZpbGVuYW1lIjoiZmlyZXdhbGwucG5nIiwidHlwZSI6ImlubGluZSJ9fQ.AEx_L7DtKwFkzy4FGcgENyDJK7wFguyENoloJ9LGsj8)

<br />
On the host PC, run Command Prompt and ping the VM IP Adress to ensure that there is successful connection.
<br />
<br />

![ping](https://download-files.wixmp.com/raw/25f80d_e05e5d7ebf34493495a9b8f28cf50a6a.png?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ1cm46YXBwOmU2NjYzMGU3MTRmMDQ5MGFhZWExZjE0OWIzYjY5ZTMyIiwic3ViIjoidXJuOmFwcDplNjY2MzBlNzE0ZjA0OTBhYWVhMWYxNDliM2I2OWUzMiIsImF1ZCI6WyJ1cm46c2VydmljZTpmaWxlLmRvd25sb2FkIl0sImlhdCI6MTcyMTMwMDA4NywiZXhwIjoxNzIxMzAwOTk3LCJqdGkiOiJiNzJhODEzYy00OTk5LTQwOGEtYTExMi00NWI1NWUzM2M0OTgiLCJvYmoiOltbeyJwYXRoIjoiL3Jhdy8yNWY4MGRfZTA1ZTVkN2ViZjM0NDkzNDk1YTliOGYyOGNmNTBhNmEucG5nIn1dXSwiZGlzIjp7ImZpbGVuYW1lIjoicGluZy5wbmciLCJ0eXBlIjoiaW5saW5lIn19.KOigsPQP_gRzd8bI3leTH9kLC-CvEsn0ncdFTMWRrog)

<h2>Run scans</h2>
Go to the Nessus Essentials web page and on the "My Scans" page, click "Create a new scan", then select "Basic Network Scan". 
<br/>
<br/>

![nessus scan1](https://download-files.wixmp.com/raw/25f80d_2db61592ebbf4b12ba7541570f28d5b3.png?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ1cm46YXBwOmU2NjYzMGU3MTRmMDQ5MGFhZWExZjE0OWIzYjY5ZTMyIiwic3ViIjoidXJuOmFwcDplNjY2MzBlNzE0ZjA0OTBhYWVhMWYxNDliM2I2OWUzMiIsImF1ZCI6WyJ1cm46c2VydmljZTpmaWxlLmRvd25sb2FkIl0sImlhdCI6MTcyMTMwMDE2MSwiZXhwIjoxNzIxMzAxMDcxLCJqdGkiOiI3NzZjZDBmMi1hZjI0LTQ3YTktYjhiYi1jMWQwMzliNWE1MTMiLCJvYmoiOltbeyJwYXRoIjoiL3Jhdy8yNWY4MGRfMmRiNjE1OTJlYmJmNGIxMmJhNzU0MTU3MGYyOGQ1YjMucG5nIn1dXSwiZGlzIjp7ImZpbGVuYW1lIjoibmVzc3VzIHNjYW4xLnBuZyIsInR5cGUiOiJpbmxpbmUifX0.VChz2KUsp9lQu7qOFF420Ae2MA0n_qDBwCZ9AbOYTKQ)
<br />
<br />
We will name the scan "Windows 10" and in "Targets" we will enter the VM's IP address which in our case is 192.168.213.128.

![nessus scan config](https://download-files.wixmp.com/raw/25f80d_2553fce696ab479fbae5a294d22f56d7.png?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ1cm46YXBwOmU2NjYzMGU3MTRmMDQ5MGFhZWExZjE0OWIzYjY5ZTMyIiwic3ViIjoidXJuOmFwcDplNjY2MzBlNzE0ZjA0OTBhYWVhMWYxNDliM2I2OWUzMiIsImF1ZCI6WyJ1cm46c2VydmljZTpmaWxlLmRvd25sb2FkIl0sImlhdCI6MTcyMTMwMDQxNywiZXhwIjoxNzIxMzAxMzI3LCJqdGkiOiIxYWEzNzdhMS03NjViLTRmZmItYTc2OS00Y2E4NDBhYWE5MTQiLCJvYmoiOltbeyJwYXRoIjoiL3Jhdy8yNWY4MGRfMjU1M2ZjZTY5NmFiNDc5ZmJhZTVhMjk0ZDIyZjU2ZDcucG5nIn1dXSwiZGlzIjp7ImZpbGVuYW1lIjoibmVzc3VzIHNjYW4gY29uZmlnLnBuZyIsInR5cGUiOiJpbmxpbmUifX0.MdRQovkw87j2vbWGVxdDx4k82p8jfSVf5-9lOBdX59Q)

<br />
Click "Save" and "Launch" to begin the scan.
<br />
<br />

![Launch_newly_created_scan](https://user-images.githubusercontent.com/108043108/177888041-95c53001-b8d2-4355-9311-3ee2637dff94.JPG)

![Scan_Running](https://user-images.githubusercontent.com/108043108/177888049-661dddfc-ebe0-42cf-ad87-14bc5af53fe5.gif)

![Scan_Completed](https://user-images.githubusercontent.com/108043108/177888068-25d4a86a-c150-4e77-a993-9df4178c5ba1.JPG)

<br />
After a few minutes, the scan is completed. There is a total of 17 vulnerabilities and 32 total results, 30 of which are "Info". The "Info" results are usually not vulnerabilities but still something that you should be aware of. There is 1 medium vulnerability named "SMB Signing not required" which may be further explored and remediated.
<br/>
<br/>

![Results_Of_Scan](https://user-images.githubusercontent.com/108043108/177888196-3141c52f-df79-4c58-9fee-5daa68d78c5b.gif)

<br />
We have completed a non-credentialed scan. We will now configure the VM to be able to accept credentialed scans and rescan the VM to compare the results. Tenable Nessus recommends several steps before running the credentialed scans. Click on the links below for a step-by-step guide.

- [Enable Remote Registry](https://success.trendmicro.com/dcx/s/solution/1039259-configuring-the-remote-registry-service-to-automatically-start-upon-log-on?language=en_US)
- [Disable Windows User Account Control (UAC)](https://www.howtogeek.com/247/disable-user-account-control-uac-the-easy-way-on-windows/)
- [Disable UAC remote restrictions](https://learn.microsoft.com/en-us/troubleshoot/windows-server/windows-security/user-account-control-and-remote-restriction)

We will now go back to the Nessus webpage. On the "My Scans" page, click on "New Scan" and then "Basic Network Scan". We will name this scan "Windows 10 with credentials" and in "Targets" we will input our IP address (192.168.213.128). We will then go to the "Credentials" tab and enter our VM Windows 10 Username and Password. Click "Save" and "Launch" to begin the credentialed scan.
<br />

![Configure_Nessus](https://user-images.githubusercontent.com/108043108/177890138-e6420231-4ce8-4a2d-99fb-e1e992da6ebb.JPG)

![Adding_Credentials](https://user-images.githubusercontent.com/108043108/177890151-27496a20-72b8-4763-8c82-368a06a15d3f.gif)

<br />
<br />
The credentialed scan has revealed a total of 44 vulnerabilities and 348 total results including 37 critical vulnerabilities. The new scan is able to scan more in-depth compared to the non-credentialed scan. There are many vulnerabilities found because we have not updated the Windows 10 OS.


![new_scan_properly_credentialed](https://user-images.githubusercontent.com/108043108/177890582-7f4d0eec-3b5f-4a5f-b708-47b3ccfb5d83.JPG)

![Old_scan_not_credentialed](https://user-images.githubusercontent.com/108043108/177890589-e4e882ab-6733-4930-ad4c-1115a2c620b3.JPG)

<br />
<br />

We will now download and install old deprecated software of [Mozilla Firefox](https://ftp.mozilla.org/pub/firefox/releases/) (Version 1.0) and [VLC Media Player](https://www.videolan.org/vlc/releases/) (Version 2.0.0) inside the VM and run our Nessus scanner to see how many more vulnerabilities it will detect.
<br/>


![downloading_an_old_version_of_firefox](https://user-images.githubusercontent.com/108043108/177890787-5cd80be3-99a1-40a4-bddc-feb06ea9cda7.JPG)

<br />
<br />
This time the scan has revealed a total of 48 vulnerablilities and 585 total results including 130 critical vulberabilities!
<br/>


![Old_Firefox_Scan](https://user-images.githubusercontent.com/108043108/177890872-ed890db9-a15d-4de9-b3b3-6723dd161f22.JPG)

<br />
<br />
Many of the critical alerts are from Firefox with 84 critical vulnerabilities and VLC with 7 critical vulnerabilities.  
<br />

![Showing_Vulnerabilities](https://user-images.githubusercontent.com/108043108/177891162-cf86e335-0539-4f9f-abb2-7150b482e689.gif)


<h2>Remediation</h2>
 
We will now start the process of remediating the vulnerabilities by updating our Windows 10 to the latest version and uninstalling and deleting Firefox and VLC.
<br />

![Fixing_Vulnerabilities_Uninstall_Firefox](https://user-images.githubusercontent.com/108043108/177891363-17bdc0ea-c872-434f-95a6-4bf6e4694ddf.JPG)

<br />
<br />

![Remediating_Vulnerabilities_Updating_WIndows_1](https://user-images.githubusercontent.com/108043108/177891464-75d2b603-cadf-4923-bc1f-61409b11169d.gif)

![Remediating_Vulnerabilities_Updating_Windows](https://user-images.githubusercontent.com/108043108/177891436-a7b26e21-8376-4650-aaee-aaf4bc2e451e.JPG)

<br />
<br />
We will run a final Nessus scan to see the results after remediation.
<br/>


![VM_Up_To_date](https://user-images.githubusercontent.com/108043108/177891501-767d6764-8e4a-4bd0-85cc-6b70e48c62aa.JPG)

<br />
<br />
Most of the critical vulnerabilities have been remediated, though there is still 2 critical vulnerabilities. One of the vulnerabilities is due to the Windows browser still using Internet Explorer. We should change to Microsoft Edge to fix this issue.
<br />
<br />
Another critical vulnerability is from Microsoft 365 which may be remediated after running another Windows Update or installing the update manually.

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
