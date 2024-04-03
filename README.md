# configure-ad
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
In this tutorial we will the simulate an on-premises Active Directory within Azure Virtual Machines. This will be a long and detialed tutorial so be patient and take your time with this one. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

STEP 1: Create Our 1st Virtual Machine 'the domain controller'

For this lab we will need 2 virtual machines. A domain controller and a client. 

Go to your Azure portal and click virtual machines. 



Next hover over to create then click create Azure virtual machine.

Name this first virtual machine DC-1 and while you are at it you can create a new resource group. I will call this resource group AD lab. Choose you desired region ensuring it's one that will allow you to create virtual machines that are powerful enough to do this lab. I will be using europe UK south. I recommend doing this lab with 2 machines that have 2vcpus. 



Go to the image section and down in the drop down menu till you find a windows server option. For this lab I will be using windows server 2022. I cant stress this enough, ensure that machine you are using has 2vcpus. I was stuck for 3 - 4 doings things the first time because my Virtual machine was really slow. I choose a cheap bur really weak machine that made doing this lab incredibly difficult. If you are unable to make both Virtual machines with 2vcpus then opt for the stronger and most exprensive image in the 1 vcpu category. 

Pick a user name and pass word. Honestly just keep it simple and make sure it's something that you can remember. 



At the bottom of the page remember to check the box that "would you like to use an existing windows server license.



Click next.



Then next again on the disk section till we get to networking. 


Ensure that you see the name of the vritual network and remember it. 



Then scroll to the bottom and click next to create this first virtual machine.


STEP 2: 

THIS STEP IS INCREDIBLY IMPORTANT. PLEASE TAKE NOTE TO ENSURE YOU DON'T RUN INTO AN ERROR LATER. 

Wait for 5 - 10 minutes. It sounds weird but there is a reason for this. I ran into this issue and a noticed a few guys in a discord server that were also doing a similar lab to me had the exact same issue. 
Bascially Virtual machine 1 'the domain controller' and virtual machine 2 'the client' need to be in the same virtual network for them to be connected. 
If you rush to making the 2nd virtual machine azure will make a new network for it. Separating the 2 machines. 
Make sure both machines are in the same virtual network which is why I told you to remember the name of the first virtual network. 

So go back to your Azure portal and click virtual machines. 



Next hover over to create then click create Azure virtual machine.


This time instead of creating a new resource group we are going to put this virtual machine in ths same resource group as the DC-1 virtual machine. Use the drop down menu in the resource group section to find the 'AD Lab resource group'. 



Let's name this Virtual machine client 1 and ensure it's also in the same region as the previous virtual machine. 



As for the imnage we will go for a windows 10 machine that has 2vcpus.


For the sake of simplicity I will be using the same user name and password as the previous virtual machine. 


At the bottom of the page remember to check the box that "would you like to use an existing windows server license.



Click next.



Then next again on the disk section till we get to networking. 


Now go to the virtual machine section and in the drop down menu you should see an option for the same virtual network that was made with the domain controller virtual machine. If you followed the same naming conventions as me you will see AD Lab vnet. If this isn't the case. Exit this virtual machine and wait 3 or 4 minutes and try this process again. If it still doesn't work maybe try redeploying the domain controlller virtual machine. 


Once this is done click review + create 



You should see a green message 'validation pass'. To finish the process click create.


STEP 3: Set The Domain Controllers NIC Private IP address to be static




Go back to virtual machines and click on your domain controller. 




Click on the networking tab that's on the left hand side. 




Click on the networking interface so be can change it's settings. 




Go back to the left hand side and click IP configurations. 




As you can see the IP address is dynamic and we want to change it to static. Click on it. 




Then toggle it to static and press save. 


STEP 4: Ensuring connectivity between the virtual machines using ping 

First off let's log into the client-1's server. Although we haven't opened up the firewall to ICMP traffic on the domain controller it will be good to observe how this change occurs. 

Go to virtual machines then click on client 1. Find the public IP address and copy it. 


We will use to IP address to login to our virtual machine using either microsoft remote desktop on mac or remote desktop connection on windows. 



Enter in your username and password that you made earlier when creating this virtual machine. I hope you haven't forgot it. Then login to the machine. 



While client one is loading we can go to the domain controller virtual machine and find it's private IP address so that we can ping it. 



Scroll down a bit and you should be able to find it on the DC-1 virtual machine page. Remember this number.


Go back to the client 1 virtual machine and click no for all of these annoying options. CLick accept to proceed. 


Go to the start menu and search for command prompt. Once it's opened we can attempt to ping the domain controller by typing ping -t 






















<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
