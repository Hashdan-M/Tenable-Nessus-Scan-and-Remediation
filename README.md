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

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04/53863828912/in/dateposted-public/" title="ipconfig"><img src="https://live.staticflickr.com/65535/53863828912_0dc0010103_b.jpg" width="1022" height="769" alt="ipconfig"/></a>

<br />
Go to the VM PC and disable the Windows Firewall for all connections (Domain Profile, Private Profile & Public Profile) which would otherwise block all connection attempts from our host PC. 
<br />
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04" title=""><img src="https://live.staticflickr.com/65535/53864749111_12e9219e0d_c.jpg" width="817" height="710" alt=""/></a>

<br />
On the host PC, run Command Prompt and ping the VM IP Adress to ensure that there is successful connection.
<br />
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04/53865165230/in/dateposted-public/" title="ping"><img src="https://live.staticflickr.com/65535/53865165230_d34438fb27_b.jpg" width="983" height="513" alt="ping"/></a>

<h2>Run scans</h2>
Go to the Nessus Essentials web page and on the "My Scans" page, click "Create a new scan", then select "Basic Network Scan". 
<br/>
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04/53865167730/in/dateposted-public/" title="nessus scan1"><img src="https://live.staticflickr.com/65535/53865167730_1d35afab73_b.jpg" width="1024" height="581" alt="nessus scan1"/></a>
<br />
<br />
We will name the scan "Windows 10" and in "Targets" we will enter the VM's IP address which in our case is 192.168.213.128.

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04/53864757071/in/dateposted-public/" title="nessus scan config"><img src="https://live.staticflickr.com/65535/53864757071_03d24369a7_b.jpg" width="1024" height="613" alt="nessus scan config"/></a>

<br />
Click "Save" and "Launch" to begin the scan.
After a few minutes, the scan is completed. There is a total of 17 vulnerabilities and 32 total results, 30 of which are "Info". The "Info" results are usually not vulnerabilities but still something that you should be aware of. There is 1 medium vulnerability named "SMB Signing not required" which may be further explored and remediated.
<br/>
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04" title=""><img src="https://live.staticflickr.com/65535/53864760126_9b5f860ee3_b.jpg" width="1055" height="216" alt=""/></a>

<br />
We have completed a non-credentialed scan. We will now configure the VM to be able to accept credentialed scans and rescan the VM to compare the results. Tenable Nessus recommends several steps before running the credentialed scans. Click on the links below for a step-by-step guide.
<br />
<br />

- [Enable Remote Registry](https://success.trendmicro.com/dcx/s/solution/1039259-configuring-the-remote-registry-service-to-automatically-start-upon-log-on?language=en_US)
- [Disable Windows User Account Control (UAC)](https://www.howtogeek.com/247/disable-user-account-control-uac-the-easy-way-on-windows/)
- [Disable UAC remote restrictions](https://learn.microsoft.com/en-us/troubleshoot/windows-server/windows-security/user-account-control-and-remote-restriction)

We will now go back to the Nessus webpage. On the "My Scans" page, click on "New Scan" and then "Basic Network Scan". We will name this scan "Windows 10 with credentials" and in "Targets" we will input our IP address (192.168.213.128). We will then go to the "Credentials" tab and enter our VM Windows 10 Username and Password. 
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04" title=""><img src="https://live.staticflickr.com/65535/53864770416_32fd5bac0e_b.jpg" width="977" height="380" alt=""/></a>

<br />
Click "Save" and "Launch" to begin the credentialed scan. 
<br />
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04" title=""><img src="https://live.staticflickr.com/65535/53865027028_8d8d4d29c4_b.jpg" width="993" height="213" alt=""/></a>

The credentialed scan has revealed a total of 44 vulnerabilities and 348 total results including 37 critical vulnerabilities. The new scan is able to scan more in-depth compared to the non-credentialed scan. There are many vulnerabilities found because we have not updated the Windows 10 OS.

<br />

We will now download and install old deprecated software of [Mozilla Firefox](https://ftp.mozilla.org/pub/firefox/releases/) (Version 1.0) and [VLC Media Player](https://www.videolan.org/vlc/releases/) (Version 2.0.0) inside the VM and run our Nessus scanner to see how many more vulnerabilities it will detect.

<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04/53865035303/in/dateposted-public/" title="install firefox and vlc"><img src="https://live.staticflickr.com/65535/53865035303_d51cc0350f_b.jpg" width="1016" height="765" alt="install firefox and vlc"/></a>

<br />
This time the scan has revealed a total of 48 vulnerablilities and 585 total results including 130 critical vulnerabilities!
<br/>
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04" title=""><img src="https://live.staticflickr.com/65535/53865040893_e88d10833c_b.jpg" width="988" height="204" alt=""/></a>

<br />
Many of the critical alerts are from Firefox with 84 critical vulnerabilities and VLC with 7 critical vulnerabilities.  
<br />
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04/53864803386/in/dateposted-public/" title="firefox critical"><img src="https://live.staticflickr.com/65535/53864803386_f40457aac9_b.jpg" width="999" height="675" alt="firefox critical"/></a>

<h2>Remediation</h2>
 
We will now start the process of remediating the vulnerabilities by updating our Windows 10 to the latest version and uninstalling and deleting Firefox and VLC.
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04" title=""><img src="https://live.staticflickr.com/65535/53863912822_a45e8c760f_b.jpg" width="1024" height="768" alt=""/></a>

<br />
We will run a final Nessus scan to see the results after remediation.
<br/>
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04" title=""><img src="https://live.staticflickr.com/65535/53863917122_e3a96c441c_b.jpg" width="992" height="209" alt=""/></a>

<br />
Most of the critical vulnerabilities have been remediated, though there is still 2 critical vulnerabilities. One of the vulnerabilities is due to the Windows browser still using Internet Explorer which is no longer supported. We should change to Microsoft Edge to fix this issue.
<br />
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04" title=""><img src="https://live.staticflickr.com/65535/53865075143_0588ff61a8_b.jpg" width="917" height="739" alt=""/></a>

Another critical vulnerability is from Microsoft 365 which may be remediated after upgrading the app in the Microsoft Store.

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201091502@N04" title=""><img src="https://live.staticflickr.com/65535/53864834811_ee71c8f4f4_b.jpg" width="936" height="624" alt=""/></a>

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
