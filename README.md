![](images/Windows_Active_Directory_Domain_Services-2.png)
# How to setup a Windows AD (within Virtual Box) to create a corporate network.

## Overview:
![](images/WindowsADdrawIO.png)
Pictured above is a high-level overview of our corporate network. First, we are going to download Virtual Box, Windows 10 and Windows server 2019 ISO files (**see below**). Then, we are going to create our first virtual machine with Windows server 2019 installed. This will act as our doamin controller (DC) and where we will house Active Directory. We are going to give our DC two network interface cards (NICs): one will connect to the external ![#f03c15](https://via.placeholder.com/15/f03c15/f03c15.png) `internet` the other will be for the ![#1589F0](https://via.placeholder.com/15/1589F0/1589F0.png) `internal` network so that the Windows 10 clients can connect and reach the internet.

We will assign IP addressing for the internal network, while the external network automatically gets IP addressing from your home network. After assinging IPs we will create our doamin thorugh Active Directory, configure network address translation (NAT) and setup Dynamic Host Configuration Protocol (DHCP) for internet connectivity.

Finally, we will download and run a PowerShell script that will automatically create +1k users in Active Directory to simumlate our enterprise users. 

After completing our DC virtual machine, we will create another virtual machine that will be our Windows 10 client. This client machine will connect to our ![#1589F0](https://via.placeholder.com/15/1589F0/1589F0.png) `internal` network through our DC's doamin name (eventually reaching the ![#f03c15](https://via.placeholder.com/15/f03c15/f03c15.png) `internet`). 



## Technologies and Protocols:
* Window's Active Directory
* Window's networking: Domain controler, DHCP, and NAT
* Oracle Virutal Box
* Powershell 

## Learning Objectves:
1. 

![](images/Home%20Lab%20-DC/DomainController/DC1.png) 
