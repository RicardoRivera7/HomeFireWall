<h1>Home FireWall With Pfsense</h1>


<h2>Description</h2>
This is a project to create your own firewall environment at home using Pfsense and a virtualbox environment
<br />

<h2>Prerequisites</h2>
- <b>Know how to use Virtualbox and be able to create new machines</b> 

<h2>Software Used</h2>

- <b>Virtualbox </b> 
- <b>Pfsense</b>

<h2>Environments Used </h2>

- <b>Linux</b>

<h2>Downloads</h2>

-[Virtualbox](https://www.virtualbox.org/wiki/Downloads)

<b></b>
-[Pfsense](https://www.pfsense.org/download/)


<h2>Network Diagram</h2>
<img src="https://i.imgur.com/5EpzDZa.png" height="80%" width="80%" alt="Firewall Steps"/>
<br />
<br />



<h2>Setup Walk-through:</h2>

<p align="left">
Click the download link and download the correct pfsense version you need (AMD64 version works for most users) <br/> 
Select the DVD ISO Installer option: <br/>
<img src="https://i.imgur.com/iYxlJRu.png" height="80%" width="80%" alt="Firewall Steps"/>
<br />
<br />

  
In Virtualbox create a new machine and complete the following (once done click finish):  <br/>
Set Type to BSD <br/>
Set Version to FreeBSD(64-bit) <br/>
Allocate at least 2gb of Basse Memory <br/>
Allocate at least 19gb of virtual hard disk space <br/>
<img src="https://i.imgur.com/v7deaWG.png" height="80%" width="80%" alt="Firewall Steps"/> 
<br />
  
<img src="https://i.imgur.com/JwEvz2n.png" height="80%" width="80%" alt="Firewall Steps"/>
<br />
<br />

  
Select the machine and Click settings the click the network tab. Here we will be creating the network interfaces, adpater 1 will be our LAN, adpater 2 is our WAN, adapter 3 is our DMZ <br/>
For all adpaters make sure that "Enable Network Adaptor" is checked and do the following: <br/>
Adapter 1 Attached to is NAT <br/>
Adapter 2 Attached to is Internal Network <br/>
Adapter 3 Attached to is Internal Network and under name put it as: DMZ <br/>
<img src="https://i.imgur.com/FKv6KgG.png" height="80%" width="80%" alt="Firewall Steps"/>
<br />
  
<img src="https://i.imgur.com/1tYim7v.png" height="80%" width="80%" alt="Firewall Steps"/>
<br />
<br />

  
Start the Virtual Machine and start the installation <br/>
<img src="https://i.imgur.com/BmDRGKu.png" height="80%" width="80%" alt="Firewall Steps"/>
<br />
<br />

  
Choose all the default options and make sure you select the checkbox for the ZFS Configuration section:  <br/>
<img src="https://i.imgur.com/VZVpugG.png" height="80%" width="80%" alt="Firewall Steps"/>
<br />
<br />

  
Select Yes for the next option and wait until installation is complete, once you get the complete box you must unmount the ISO or it will cycle through the boot process again:  <br/>
At the top bar of the Virtualbox go to Devices -> Optical Drives -> select your pfsense ISO -> Click Force Unmount <br/>
Click Reboot <br/>
<img src="https://i.imgur.com/io57SG0.png" height="80%" width="80%" alt="Firewall Steps"/>
<br />
<br />
  
Create and install another virtual machine for Linux or Windows whichever you prefer (I used Linux)  <br/>
Edit the adapter 1 to be Attached to Internal Network and launch the new VM <br/>
Open the command line and type ifconfig (linux) or ipconfig (windows) <br/>
Check to see that the inet ip matches your LAN ip thats on PFsense 
<img src="https://i.imgur.com/9rRPKPU.png" height="80%" width="80%" alt="Firewall Steps"/>
<br/>

<img src="https://i.imgur.com/GA4Rpbg.png" height="80%" width="80%" alt="Firewall Steps"/>
<br/>
<br/>

You can try to ping the LAN ip in the command line to see if you get a response back <br/>
<img src="https://i.imgur.com/u3qFSN0.png" height="80%" width="80%" alt="Firewall Steps"/>
<br/>
<br/>

Open a web browser and type in the LAN ip, you will get a warning since there is no certificate, you can just ignore that an advance <br/>
<img src="https://i.imgur.com/AP54rb3.png" height="80%" width="80%" alt="Firewall Steps"/> 
<br/>
<br/>

Login using the default credentials all lowercase for the username and password: <br/> 
Username is admin <br/>
Password is pfsense <br/>
<img src="https://i.imgur.com/nhHiR0V.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

Go through the installation wizard and then you have your firewall all setup using pfsense!
<br/>
<br/>


<h1>Adding a DMZ (optional)</h1> <br/>


<h2>Setting up DMZ on Pfsense Interface</h2>
Once fully logged in and installed you should be on the dashboard <br/>
If you scroll down you can see your two interfaces: WAN and LAN <br/>
<img src="https://i.imgur.com/IQslNaF.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

To add our DMZ, on the top tool bar select "Interfaces" -> click on "Assignments" <br/>
Click the green "Add" button and you should see a new line called "OPT1" added <br/>
<img src="https://i.imgur.com/epYVOjC.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

Click on the blue OPT1 text so we can edit it <br/>
Let's do the following: <br/>
<em>In the description setting, rename it to "DMZ" <br/>
Turn on the box for "Enable Interface" <br/>
In the IPv4 Configuration Type select "Static IPv4" <br/>
Under the "Static IPv4 Configuration" section set the  IPv4 Address (I used 192.168.2.1) and set the subnet mask to "/24" <br/>
Click Save </em> <br/>
<img src="https://i.imgur.com/oPgRHLm.png" height="80%" width="80%" alt="Firewall Steps"/>
<img src="https://i.imgur.com/eSWjkfZ.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

Click the green "Apply Changes" button <br/>
<img src="https://i.imgur.com/8dv08bH.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

On the top tool bar click on "Services" -> click "DHCP Server" <br/>
There should be a DMZ section, click on it <br/>
<img src="https://i.imgur.com/xOnURQo.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

Do the following: <br/>
<em> Turn on the box for "Enable DHCP Server on DMZ Interface" <br/>
Under the "Primary Adress Pool" section, go to the "Adress Pool Range area" <br/>
Enter two different ip ranges, but make sure they fit within the Subnet range which is shown directly above it <br/>
(Note: I selected the range of 192.168.2.100 - 192.168.2.199 so that I know anything within the 100 range was assigned by DHCP) <br/>
Click Save </em> <br/>
<img src="https://i.imgur.com/1UIbfuT.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

Click the green "Apply changes" button <br/>
<img src="https://i.imgur.com/cLCj1I6.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

If you go back to your Dashboard, in the interfaces section you should see the newly added DMZ <br/>
<img src="https://i.imgur.com/6dGVFTl.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

Let's add a firewall fule to allow DMZ traffic <br/>
On the top tool bar click on "Firewall" -> then click on "rules" and select DMZ <br/>
Click the green "Add" button to add a rule <br/> <br/> <br/>

Do the following:
<em> Make sure action is set as Pass <br/>
Set Protocol to ANY <br/>
Set Source as DMZ subnet <br/>
Set Destination as ANY <br/>
Put any description you see fit such as "Allow outbound traffic" <br/>
Click Save </em> <br/>
<img src="https://i.imgur.com/nsKhMb7.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

Click the green "Apply changes" button <br/>
Your firewall rules should be all set! <br/>




<h2>Setting up DMZ Machine</h2> 

Set up another machine, can be Ubuntu or whatever you prefer (I just cloned my current Ubuntu machine that I setup for the LAN) <br/>
Go to the settings and go to the network settings <br/> 
Select the network attached to: Internal network <br/>
Name it as the same thing you did for the pfsense adpater 3, in my case I name it DMZ <br/>
<img src="https://i.imgur.com/oWtHpn0.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/>
<br/>

Run the machine and open the terminal <br/>
Let's see if the ip assigned is one of the DMZ ones <br/>
Type ifconfig <br/>
Check to see if the ip assigned is within the previous range you gave it, for me its 192.168.2.100 so it's within range <br/> 
<img src="https://i.imgur.com/8jqEidK.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/> 
<br/>

Let's check if its able to connect to the DMZ IP <br/>
Type ping 192.168.2.1 (or whatever you set up as your DMZ IP) <br/> 
You should get a response if successful <br/>
<img src="https://i.imgur.com/JF1YddA.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/> 
<br/>

Now let's test if it can connect to the internet <br/>
Type ping 8.8.8.8 <br/>
You should get a response if successful <br/>
<img src="https://i.imgur.com/uzgBv7w.png" height="80%" width="80%" alt="Firewall Steps"/>  
<br/> 
<br/>

Congrats you fully setup a firewall with DMZ!






  
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
