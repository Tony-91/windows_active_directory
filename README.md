![](images/Windows_Active_Directory_Domain_Services-2.png)
# How to setup a Windows AD (within a VM) to create a corporate network.

## Overview:
![](images/WindowsADdrawIO.png)
Pictured above is a high-level overview of our corporate network. First, we are going to download Virtual Box, Windows 10 and Windows server 2019 ISO files (**see below**). Then, we are going to create our first virtual machine with Windows server 2019 installed. This will act as our doamin controller (DC) and where we will house Active Directory. We are going to give our DC two network interface cards (NICs): one will connect to the external ![#f03c15](https://via.placeholder.com/15/f03c15/f03c15.png) `internet` the other will be for the ![#1589F0](https://via.placeholder.com/15/1589F0/1589F0.png) `internal` network the clients connect to and reach the internet.




## Technologies and Protocols:
* Window's Active Directory
* Window's networking: Domain controler, DHCP, and NAT
* Oracle Virutal Box
* Powershell 

## Learning Objectves:
1. 

![](images/Home%20Lab%20-DC/DomainController/DC1.png) 
