![](images/ActiveDirectory.png)
# How to setup a Windows Active Directory (within Virtual Box) to create a corporate network.
### Learning Objectves:
1. We will learn how to provision multiple virutal machines.
2. Configure a basic Windows networking environment with Active Directory.
3. Execute PowerShell script to further our Active Directory environment. 


### Technologies and Protocols:
* Oracle Virutal Box
* Window's Active Directory
* Window's networking: Domain controler, DHCP and NAT
* Powershell 


### Overview:
![](images/WindowsADdrawIO.png)
Pictured above is a high-level overview of our corporate network. First, we are going to download Virtual Box, Windows 10 and Windows server 2019 ISO files (**see below**). Then, we are going to create our first virtual machine with Windows server 2019 installed. This will act as our doamin controller (DC) and where we will house Active Directory (AD). We are going to give our DC two network interface cards (NICs): one will connect to the external ![#f03c15](https://via.placeholder.com/15/f03c15/f03c15.png) `internet` the other will be for the ![#1589F0](https://via.placeholder.com/15/1589F0/1589F0.png) `internal` network so that the Windows 10 clients can connect through and reach the internet.

We will assign IP addressing for the internal network, while the external network automatically gets IP addressing from your home network. After assinging IPs we will create our domain thorugh Active Directory, configure network address translation (NAT) and setup Dynamic Host Configuration Protocol (DHCP) for internet connectivity.

Finally, we will download and run a PowerShell script that will automatically create +1k users in Active Directory to simumlate our enterprise users. 

After completing our DC virtual machine, we will create another virtual machine that will be our Windows 10 client. This client machine will connect to our ![#1589F0](https://via.placeholder.com/15/1589F0/1589F0.png) `internal` network through our DC's domain name (eventually reaching the ![#f03c15](https://via.placeholder.com/15/f03c15/f03c15.png) `internet`). 



## Step 1: [Download: Virtual Box](https://www.virtualbox.org/wiki/Downloads "Virtual Box"), [Windows '19 server ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019 "Windows '19 server ISO") and [Windows 10 ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019 "Windows 10 ISO").
- Virtual box (download ‘VM Virtual Box Extension Pack’ found on the same page as Virtual Box for your host machine download )
- ISO: Windows Server and Windows 10
    - Set RAM (2048 MB is fine enough) and memory (30 GB is fine) to your needs.
- Create a virtual hard disk now
- VDI
- Dynamically allocate
    - Under settings > general > advance set ‘shared clipboard’ and ‘drag’n’drop’ to bidirectional (drag files + copy/paste from host machine)
    
![](images/Home%20Lab%20-DC/DomainController/DC1.png) 

## Step 2: Our goal is to have two NICs (network interface cards); one for the intranet and one for the internet.
- Under settings > network > Adapter 2 tab: select Internal Network. This will connect our machine to the intranet (internal network).
- The Adapter 1 tab is set to NAT network by default (our connection to the internet).
       
![](images/Home%20Lab%20-DC/DomainController/DC2.png)

## Step 3: Upload ISO server onto our newly created domain controller VM.
- Go to settings > storage and click the blue disk/CD image. 
- Click ‘Choose a disk file…’ and upload the server ISO from where you saved it to.

![](images/Home%20Lab%20-DC/DomainController/DC3.png)

## Step 4 Configure your new Windows server machine (selecting standard desktop experience).
- This may take a while

![](images/Home%20Lab%20-DC/DomainController/DC4.png)

> Windows DC
> 
> **Username: Administrator**
>
> **Password: Password1**
> 
> If asked to Press Ctrl+Alt+Delete to Unlock the home page click Input from the top of the page > keyboard > Insert Ctrl+Alt+Delete (these instructions are for a Mac host machine, but similar instructions for a Windows Host).

## Step 5: Install windows guest additions 64
- First, click Devices (found on top of the screen, on Mac) > insert guest additions CD image
- Click file explorer > this pc and double click CD Drive (D:) Virtual Box Guest Additions
- Double click and install BoxWindowsAdditions-amd64

![](images/Home%20Lab%20-DC/DomainController/DC5.png)

## Step 6: Set up NIC - internal connection 
- Click the little computer symbol found in the bottom right of the screen
- Choose ‘undefined network’ > change adapter options
- We should see two networks on this machine. Re-name the left most inter-net and the second one intra-net.
- *Inter-net is our NIC to the internet and intra-net is our NIC to our internal network.*

![](images/Home%20Lab%20-DC/DomainController/DC6.png)

## Step 7: After re-naming, we need to assign an IP to intra-net (DHCP automatically gives inter-net an IP).
- Right-click intra-net > properties  > double click internet protocol version (TCP/IPv4)
- Assign IPs as seen in screenshot below:

![](images/Home%20Lab%20-DC/DomainController/DC7.png)

## Step 8: Re-name this PC
- Right-click the start window found at the bottom left > system > rename this pc
- Re-name to DC (domain controller)
- Restart your VM

![](images/Home%20Lab%20-DC/DomainController/DC8.png)

## Step 9A: Install Active Directory Domain Services
- Search for server manager > click Add roles and features and click next
- Under installation, type click role-based or feature-based installation and click next
- Under server, select ‘select a server from the server pool’ and choose our only server option and click next

![](images/Home%20Lab%20-DC/DomainController/DC9a.png)

## Step 9B: Under server roles, click Active Directory Domain Services and click Add Features
- Under Features, click next to skip, and under AD DS click next to skip. 
- Under the Confirmation tab, click Install

![](images/Home%20Lab%20-DC/DomainController/DC9b.png)

## Step 10A: Create our domain after installing the domain service software
- Open the Server Manager dashboard, click on the yellow notification icon on top and click Promote this server to a domain controller
- Under Deployment Configuration, select Add a new forest and name the Root domain mydomain.com. Click next.
- Under Domain Controller Options, input and confirm your password (**Password1**). Click next

![](images/Home%20Lab%20-DC/DomainController/DC10a.png)

## Step 10B: Under DNS Options, click next to skip.
- Under Additional Options, click next to skip.
-  Under Paths, click next to skip.
-  Under Review Options, click next to skip.
-  Finally, under Prerequisites Check,  click Install. The system will restart.
-  Sign in to the newly created MYDOMAIN\Administrator account **Password1**

![](images/Home%20Lab%20-DC/DomainController/DC10b.png)

## Step 11A: Create a dedicated Admin Account
- Click Start > Windows Administrative Tools > Active Directory Users and Computers 
- Right-click mydomain.com and click > New > Organizational Unit. Uncheck the box, and name it Admins.
- Right-click the new folder Admins and click > New > User

![](images/Home%20Lab%20-DC/DomainController/DC11a.png)

11B: Fill out first and last name. Choose and confirm the password **Password1**, uncheck User must change the password at next logon, and *CHECK* Password never expires. Click next. Click Finish.

![](images/Home%20Lab%20-DC/DomainController/DC11b.png)





