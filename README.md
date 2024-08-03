<img src="https://forgesecure.com/wp-content/uploads/2024/03/NessusEssentials.jpg" width=50% height=50%>

<h1>Tenable Nessus Scan and Remediation</h1>

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

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893436540/in/dateposted-public/" title="ipconfig"><img src="https://live.staticflickr.com/65535/53893436540_24300f41f6_b.jpg" width="1022" height="769" alt="ipconfig"/></a>

<br />
Go to the VM PC and disable the Windows Firewall for all connections (Domain Profile, Private Profile & Public Profile) which would otherwise block all connection attempts from our host PC. 
<br />
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893024601/in/dateposted-public/" title="firewall"><img src="https://live.staticflickr.com/65535/53893024601_0440baab20_o.png" width="817" height="710" alt="firewall"/></a>

<br />
On the host PC, run Command Prompt and ping the VM IP Adress to ensure that there is successful connection.
<br />
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893354834/in/dateposted-public/" title="ping"><img src="https://live.staticflickr.com/65535/53893354834_32547e5020_b.jpg" width="983" height="513" alt="ping"/></a>

<h2>Run scans</h2>
Go to the Nessus Essentials web page and on the "My Scans" page, click "Create a new scan", then select "Basic Network Scan". 
<br/>
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893354849/in/dateposted-public/" title="nessus scan1"><img src="https://live.staticflickr.com/65535/53893354849_f44f11c692_b.jpg" width="1024" height="581" alt="nessus scan1"/></a>
<br />
<br />
We will name the scan "Windows 10" and in "Targets" we will enter the VM's IP address which in our case is 192.168.213.128.

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893354904/in/dateposted-public/" title="nessus scan config"><img src="https://live.staticflickr.com/65535/53893354904_25162cce3d_b.jpg" width="1024" height="613" alt="nessus scan config"/></a>

<br />
Click "Save" and "Launch" to begin the scan.
After a few minutes, the scan is completed. There is a total of 17 vulnerabilities and 32 total results, 30 of which are "Info". The "Info" results are usually not vulnerabilities but still something that you should be aware of. There is 1 medium vulnerability named "SMB Signing not required" which may be further explored and remediated.
<br/>
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893354854/in/dateposted-public/" title="nessus scan w10"><img src="https://live.staticflickr.com/65535/53893354854_138e105361_b.jpg" width="1024" height="210" alt="nessus scan w10"/></a>

<br />
We have completed a non-credentialed scan. We will now configure the VM to be able to accept credentialed scans and rescan the VM to compare the results. Tenable Nessus recommends several steps before running the credentialed scans. Click on the links below for a step-by-step guide.
<br />
<br />

- [Enable Remote Registry](https://success.trendmicro.com/dcx/s/solution/1039259-configuring-the-remote-registry-service-to-automatically-start-upon-log-on?language=en_US)
- [Disable Windows User Account Control (UAC)](https://www.howtogeek.com/247/disable-user-account-control-uac-the-easy-way-on-windows/)
- [Disable UAC remote restrictions](https://learn.microsoft.com/en-us/troubleshoot/windows-server/windows-security/user-account-control-and-remote-restriction)

We will now go back to the Nessus webpage. On the "My Scans" page, click on "New Scan" and then "Basic Network Scan". We will name this scan "Windows 10 with credentials" and in "Targets" we will input our IP address (192.168.213.128). We will then go to the "Credentials" tab and enter our VM Windows 10 Username and Password. 
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893261988/in/dateposted-public/" title="nessus w10 username password"><img src="https://live.staticflickr.com/65535/53893261988_d3f3bbd9f8_b.jpg" width="1024" height="398" alt="nessus w10 username password"/></a>

<br />
Click "Save" and "Launch" to begin the credentialed scan. 
<br />
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893436505/in/dateposted-public/" title="nessus scan w10 with credentials"><img src="https://live.staticflickr.com/65535/53893436505_31d3c670ed_b.jpg" width="1024" height="220" alt="nessus scan w10 with credentials"/></a>

The credentialed scan has revealed a total of 44 vulnerabilities and 348 total results including 37 critical vulnerabilities. The new scan is able to scan more in-depth compared to the non-credentialed scan. There are many vulnerabilities found because we have not updated the Windows 10 OS.

<br />

We will now download and install old deprecated software of [Mozilla Firefox](https://ftp.mozilla.org/pub/firefox/releases/) (Version 1.0) and [VLC Media Player](https://www.videolan.org/vlc/releases/) (Version 2.0.0) inside the VM and run our Nessus scanner to see how many more vulnerabilities it will detect.

<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893024611/in/dateposted-public/" title="install firefox and vlc"><img src="https://live.staticflickr.com/65535/53893024611_22e9861699_b.jpg" width="1016" height="765" alt="install firefox and vlc"/></a>

<br />
This time the scan has revealed a total of 48 vulnerablilities and 585 total results including 130 critical vulnerabilities!
<br/>
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893262018/in/dateposted-public/" title="nessus scan w10 with credentials and deprecated files"><img src="https://live.staticflickr.com/65535/53893262018_cc042a6df0_b.jpg" width="1024" height="211" alt="nessus scan w10 with credentials and deprecated files"/></a>

<br />
Many of the critical alerts are from Firefox with 84 critical vulnerabilities and VLC with 7 critical vulnerabilities.  
<br />
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893436545/in/dateposted-public/" title="firefox critical"><img src="https://live.staticflickr.com/65535/53893436545_1fcaa4feb3_b.jpg" width="1024" height="692" alt="firefox critical"/></a>

<h2>Remediation</h2>
 
We will now start the process of remediating the vulnerabilities by updating our Windows 10 to the latest version and uninstalling and deleting Firefox and VLC.
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53892104432/in/dateposted-public/" title="windows update"><img src="https://live.staticflickr.com/65535/53892104432_2d78df2061_b.jpg" width="1024" height="771" alt="windows update"/></a>

<br />
We will run a final Nessus scan to see the results after remediation.
<br/>
<br/>

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893354869/in/dateposted-public/" title="nessus scan w10 remediate"><img src="https://live.staticflickr.com/65535/53893354869_84e7133b73_b.jpg" width="1024" height="216" alt="nessus scan w10 remediate"/></a>

<br />
Most of the critical vulnerabilities have been remediated, though there is still 2 critical vulnerabilities. One of the vulnerabilities is due to the Windows browser still using Internet Explorer which is no longer supported. We should change to Microsoft Edge to fix this issue.
<br />
<br />

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893354899/in/dateposted-public/" title="nessus scan w10 remediate critical"><img src="https://live.staticflickr.com/65535/53893354899_31feec6547_b.jpg" width="917" height="739" alt="nessus scan w10 remediate critical"/></a>

Another critical vulnerability is from Microsoft 365 which may be remediated after upgrading the app in the Microsoft Store.

<a data-flickr-embed="true" href="https://www.flickr.com/photos/201152865@N02/53893354929/in/dateposted-public/" title="nessus scan w10 remediate critical 1"><img src="https://live.staticflickr.com/65535/53893354929_0687aa9f5b_b.jpg" width="936" height="624" alt="nessus scan w10 remediate critical 1"/></a>

<h2>Conclusion</h2>

This experience has underscored the critical importance of proactive and thorough security measures in safeguarding our systems and data. Through conducting these scans, we have gained invaluable insights into the diverse vulnerabilities that can exist within our infrastructure.

The process has not only deepened our understanding of vulnerability management tools and techniques but has also highlighted the significance of timely updates and diligent patch management. By implementing remediation actions such as updating Windows and uninstalling deprecated software, we have taken concrete steps towards mitigating potential risks and enhancing our overall security posture.

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
