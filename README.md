<h1>Active Directory Home Lab</h1>



<h2>Description</h2>
In this home lab we're going to walk through how to create an Active Directory home lab Enviroment using Oracle Virtual Box. Configuring an running this lab will help develop your understanding of how active directory and windows networking works, so I'd highly recommend running through it a couple times. Please ask questions where any part becomes unclear, and eventually try to build it on your own.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Diskpart</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Create Our Virtual Machines: <br/>
<img src="https://i.imgur.com/Myacauv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select new and name your machine:  <br/>
<img src="https://i.imgur.com/kEmlaLA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the amount of RAM(2 GB is recommended): <br/>
<img src="https://i.imgur.com/cwu8IPy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Create a Virtual hard disk:  <br/>
<img src="https://i.imgur.com/9Td8qUs.png?1" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
(On the VR created click settings and navigate to network) The first adapter will be attached to "NAT" This will be dedicated to the Internet  <br/>
<img src="https://i.imgur.com/Wv5SEsC.png?1" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 The second adapter will be attached to "Internal network" This will be dedicated to the internal VMware<br/>
<img src="https://i.imgur.com/0jATViN.png?1" height="80%" width="80%" alt="Disk Sanitization Steps"/> 


<br />
<br />

- <b>Double click your newly created VM</b> 
- <b>Choose the virtual optical disk file and select the server that youve downloaded(sever2019 iso)</b>
- <b>After installation is complete, you must complete the windows setup</b>
- <b> Once complete, You will be prompt to create a administration account.(enter a password)</br>
<br />
<br />
Set up Internal IP address:<br />
- <b> Navigate to the network icon at the bottom right of your screen</br>
- <b>Click network<br />
- <b>Click change adapter options<br />
- <b> Name your networks(Internet & Internal)<br />
- <b> To figure out which network Internet & which is the Internal right click and select properties. <br />
- <b> Now you must give the internal network an ip address. <br />
- <b> right click the internal network and select properties<br />
- <b> Click Internet Protocal Version 4(TCP/IPv4) <br />
- <b> Assign a IP address(172.16.0.1) and subnet mask(255.255.255.0) <br />
- <b> For the preferred DNS server enter its IP address(172.16.0.1) <br />
<img src="https://i.imgur.com/LT7cdsg.png?1" height="80%" width="80%" alt="Disk Sanitization Steps"/>


Install Active Directory Domain Serves: <br />
- <b> Navigate to server manager dashboard by clicking on the start menu then clicking server manager </br>
- <b> Click add roles and features</br>
<img src="https://i.imgur.com/fOYce8T.png?1" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b> Pick the server you want to install</br>
<img src="https://i.imgur.com/KZpRXWn.png?1" height="80%" width="80%" alt="Disk Sanitization Steps"/>





 Rename this PC: <br />
  - <b> Right click the start menu and click system<br />
   - <b> Click rename this PC<br />
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
