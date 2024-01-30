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
 - <b> Under roles select Active Directory Domain Services<br />
- <b>click next<br />
- <b>click install<br />
- <b>On the dashboard click on the flag in the upper right corner<br />
- <b>Click promote the server to a domain controller<br />
- <b>In the deployment configuration click add a new forest <br />
- <b>Give your domain a name (mydomain.com) <br />
- <b>In the Domain Controller Options enter a password<br />
- <b>Click next(3), and then install <br />
- <b>Now that the Active Directory Domain Service was installed the computer will automatically restart<b/>
- <b> Log in with your admin account password<br />

<h2>Creating your custom admin account</h2>
 
- <b>Click start icon(bottom left corner) <br />
 - <b>Select Windows Administrative tools > Active Directory Users and Computers <br />
  - <b>Create a organizational unit by right clicking mydomain.com, then seledt New > Organization Unit<br />
   - <b>Name it _Admins<br />
  - <b>Right click the _Admins folder to create a new user </b>
  - <b>Insert you first and last name(example: Jameson Young)<br />
  - <b>The User logon name is commonly configured as initial, "-", last name(example j-young)
  - <b>Next select a password<br />
  - <b>To make the new user an admin right click the new user and go to properties > member of > add <br />
  - <b>Inside the lower box enter "Domain Admins" and click Check names, then click okay and apply </b>
   - <b>Now log out and this time log in as "Other user"</b>
   - <b>Here you will insert the new user and password you just created(example:j-young, Password1)<br/>

 <h2>Installing RAS/NAS</h2>
 
  This will allow the Windows10 client to be on this private virtual network but still be able to acess the internet through the domain controller <br />
  <ul>
  <li>Click Manage at the top right of the dashboard and select "add roles and features"</li>
    <li>select Role-based or feature-based installation</li>
    <li>Next select the server from the Server pool box and and click next</li>
      <li> Under roles select Remote Access</li>
       <li>Next under roles services check off (RAS) and click add feature</li>
      <li>Click next and install</li>
      <li>Navigate to the dashboard and select the tools drop down menu and click on routing and remote access</li>
     <li>Right click DC (local) and select configure and enable routing and remote access</li>
     <li>Select Network address translation(NAT)</li>
      <li>Next select the interface named _INTERNET_(this will be the interface used to connect to the internet)</li>
      <li>Select next then click finish</li>
  </ul>
  <ul>
      <h2>Setting up a DHCP server on the main controller </h2>
      <li>This will allow the Windows10 client to get a IP address that will let them access the internet</li>
     <li>Navigate to the dashboard and select add roles and features</li>
     <li>Click next then make sure "Role-based or feature-based installion" is selected then click next</li>
     <li>Select "DC mydomain.com" server from the server pool and click next</li>
     <li>Select DHCP Server under Roles and click next, next, next, install</li>
     </ul>
     
<h2>Setting the Scope</h2>
<ul>
      <li>The purpose of DHCP is to allow client computers on the network to automatically get there IP addresses </li>
       <li>Navigate to the dashboard and click on tools and select DHCP</li>
  <li>Click "dc.mydoman.com" to expand the menu, select IPv4 and select New Scope</li>
   <li>Name the scope.You can name it after whatever the IP range is.(example 172.16.0.100-200) then click next</li>
    <li>Insert the start IP address(172.16.0.100) and the End IP address(172.16.0.200) Length(24) subnet mask(255.255.255.0) then click next</li>
    <li>Lease duration is how long a computer can have that ip address before it needs to be refreshed(for this example we wil leave it at 8)</li>
     <li>Configure DHCP Options(you will select yes, i want to configure these options now) this tells the client which server to use for DNS and Gateway</li>
      <li>For Router(Default Gateway) insert IP address 172.16.0.1 and click add</li>
      <li>Click Next, You need to add an ip address for a router used by clients(this is where you will enter the domain controller's ip address 172.16.0.1)</li>
  <li> Click Add, then click next</li>
 <li>Next you will specify the parent domain(mydomain.com) you want the client computers on your network to use for DNS name resolution </li>
 <li>Click Next skipping WINS server</li>
  <li>Select yes  i want toactivate the scope now and click next and finish</li>
   <li>You may need to right click the dhcp server and select authorize</li>
    <li>Right click IPv4 and select refresh(IPv4 should now be green)</li>

 <li>Now were going to use powershell scipt to create a whole list of sample users</li>
 <li>Navigate to the domain controller dashboard</li>
  <li>Click configure this local server and then were going to disable the internet explorer enhanced security</li>
 <li>Click ON, then turn off Administrators and Users and click okay</li>
  <li>Copy the link to the source code for the  powershell script</li>
 <li>Go to the domain controller and open up internet explorer and click okay</li>
  <li>Then paste the link and press enter</li>
   <li>download the file and save as to the desktop so its easy to find</li>
 <li>Extract the script on the desktop</li> 
 <li>Open the folder and open the text file called names</li>
 <li>At the top place your name(first and last) then save and close</li>
<li>Were going to this file to programmatically create all the sample users</li>
<li>Next click on the start menu and navigate to windows powershell</li> 
<li>Under the drop down menu select Windows Powershell ISE, right click and go to more and run as administrator </li>

 <li>Click on open script and go to the desktop and open up the powershell script </li>
 <li>Next we have to enable the execution of all scripts on this server</li>
 <li>Enter "Set-ExecutionPolicy Unrestricted" into the terminal and click enter</li>
 <li> Say yes to all</li>




  

   
</p>
