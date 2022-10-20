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





