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


<img width="1268" alt="Screenshot 2024-04-03 at 16 10 55" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/c66a89ae-fce4-4b13-9d2c-268eeaf44c44">


Next hover over to create then click create Azure virtual machine.



<img width="1109" alt="Screenshot 2024-04-03 at 16 11 56" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/c29e64a1-7bb4-4f4e-9635-9810528dfb45">



Name this first virtual machine DC-1 and while you are at it you can create a new resource group. I will call this resource group AD lab. 



<img width="934" alt="Screenshot 2024-04-03 at 16 39 13" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/88ba1a82-4786-4375-b5c9-2467516e72e2">



Choose you desired region ensuring it's one that will allow you to create virtual machines that are powerful enough to do this lab. I will be using europe UK south. I recommend doing this lab with 2 machines that have 2vcpus. 


<img width="441" alt="Screenshot 2024-04-03 at 16 40 20" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/c274e4d3-82ee-48c6-a4c2-37c1718537ce">


Go to the image section and down in the drop down menu till you find a windows server option. For this lab I will be using windows server 2022. I cant stress this enough, ensure that machine you are using has 2vcpus. I was stuck for 3 - 4 doings things the first time because my Virtual machine was really slow. I choose a cheap bur really weak machine that made doing this lab incredibly difficult. If you are unable to make both Virtual machines with 2vcpus then opt for the stronger and most exprensive image in the 1 vcpu category. 

<img width="730" alt="Screenshot 2024-04-03 at 16 41 13" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/f7699617-7a67-4650-9547-ba0bb9b06c29">


Pick a user name and pass word. Honestly just keep it simple and make sure it's something that you can remember. 


<img width="733" alt="Screenshot 2024-04-03 at 16 41 38" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/de1dfb64-01e1-4f58-933d-776cb7deedbd">



At the bottom of the page remember to check the box that "would you like to use an existing windows server license.


Click next.


<img width="387" alt="Screenshot 2024-04-03 at 16 42 04" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/5f34cd03-9ced-424e-a8d0-29dc673de87e">


Then next again on the disk section till we get to networking. 


<img width="394" alt="Screenshot 2024-04-03 at 16 42 21" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/7de4ce61-4fb2-4783-b7a7-b02e0ec14f5a">


Ensure that you see the name of the vritual network and remember it. 


<img width="707" alt="Screenshot 2024-04-03 at 16 43 16" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/c8761667-286d-4834-b6d8-474c39940bdf">



Then scroll to the bottom and click next to create this first virtual machine.


<img width="671" alt="Screenshot 2024-04-03 at 16 43 51" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/f157a45f-394f-4514-a786-23a093195f45">



STEP 2: 

THIS STEP IS INCREDIBLY IMPORTANT. PLEASE TAKE NOTE TO ENSURE YOU DON'T RUN INTO AN ERROR LATER. 


<img width="1001" alt="Screenshot 2024-04-03 at 16 44 59" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/5e9fa806-09dd-406b-84ee-d86128f92ffd">


Wait for 5 - 10 minutes. It sounds weird but there is a reason for this. I ran into this issue and a noticed a few guys in a discord server that were also doing a similar lab to me had the exact same issue. 
Bascially Virtual machine 1 'the domain controller' and virtual machine 2 'the client' need to be in the same virtual network for them to be connected. 
If you rush to making the 2nd virtual machine azure will make a new network for it. Separating the 2 machines. 
Make sure both machines are in the same virtual network which is why I told you to remember the name of the first virtual network. 

So go back to your Azure portal and click virtual machines. 


<img width="1054" alt="Screenshot 2024-04-03 at 16 54 56" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/27ea0e9b-3e8a-4dc1-91bb-11cd496cf7bb">


Next hover over to create then click create Azure virtual machine.


<img width="1054" alt="Screenshot 2024-04-03 at 16 55 50" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/b3fef576-dce6-43fb-b469-a287848ae6e2">


This time instead of creating a new resource group we are going to put this virtual machine in ths same resource group as the DC-1 virtual machine. Use the drop down menu in the resource group section to find the 'AD Lab resource group'. 


<img width="677" alt="Screenshot 2024-04-03 at 16 56 24" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/4b4cfede-ce42-4338-ad9f-84d34f22b6af">


Let's name this Virtual machine client 1 and ensure it's also in the same region as the previous virtual machine. 


<img width="680" alt="Screenshot 2024-04-03 at 16 57 19" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/2e0657d7-e3ca-4f48-9e84-df572aa3b38c">



As for the imnage we will go for a windows 10 machine that has 2vcpus.



<img width="715" alt="Screenshot 2024-04-03 at 16 58 02" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/6e291d1f-2a66-4521-a2c5-89739a135deb">



For the sake of simplicity I will be using the same user name and password as the previous virtual machine. 



<img width="716" alt="Screenshot 2024-04-03 at 16 59 08" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/3fff06ff-3807-4450-9ee4-9eab765e03ee">



At the bottom of the page remember to check the box that "would you like to use an existing windows server license.



<img width="490" alt="Screenshot 2024-04-03 at 16 59 28" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/fe5e5045-a556-4cd5-8d46-e0ab79cc7ae0">



Click next.



<img width="494" alt="Screenshot 2024-04-03 at 16 59 46" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/b043aba3-1d2e-4e60-8d1c-922662ac53e3">



Then next again on the disk section till we get to networking. 



<img width="494" alt="Screenshot 2024-04-03 at 17 00 03" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/6d076035-6730-4543-a76d-c8381cf5be1a">



Now go to the virtual machine section and in the drop down menu you should see an option for the same virtual network that was made with the domain controller virtual machine. If you followed the same naming conventions as me you will see AD Lab vnet. If this isn't the case. Exit this virtual machine and wait 3 or 4 minutes and try this process again. If it still doesn't work maybe try redeploying the domain controlller virtual machine. 



<img width="723" alt="Screenshot 2024-04-03 at 17 00 47" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/466f9e3d-c6a9-4d8c-9496-2f869a645aed">



Once this is done click review + create 


<img width="422" alt="Screenshot 2024-04-03 at 17 02 02" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/b56c261f-66fb-47b1-bb2c-262ff8028a23">



You should see a green message 'validation pass'. To finish the process click create.



<img width="755" alt="Screenshot 2024-04-03 at 17 04 49" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/cd3072ea-8b81-4444-9f5e-94dc2734ae9c">



STEP 3: Set The Domain Controllers NIC Private IP address to be static





Go back to virtual machines and click on your domain controller. 



<img width="1148" alt="Screenshot 2024-04-03 at 17 12 12" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/86042954-900a-4dee-ab59-89e998dd999b">



Click on the networking tab that's on the left hand side. 



<img width="234" alt="Screenshot 2024-04-03 at 17 12 43" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/f7c46d1d-c6f7-45f4-88be-9947b4559d67">



Click on the networking interface so be can change it's settings. 



<img width="729" alt="Screenshot 2024-04-03 at 17 13 11" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/75804e0f-b6bf-4b67-a4bf-a23d44f52880">



Go back to the left hand side and click IP configurations. 


<img width="245" alt="Screenshot 2024-04-03 at 17 13 52" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/bf480da2-9a0a-45cc-83fb-f69031eb2c1c">


As you can see the IP address is dynamic and we want to change it to static. Click on it. 



<img width="1198" alt="Screenshot 2024-04-03 at 17 14 16" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/2dc4bf90-1e45-42f2-a504-3e1a0f0d9d57">



Then toggle it to static and press save. 



<img width="521" alt="Screenshot 2024-04-03 at 17 14 45" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/dd8024d9-aa32-4d97-9ec9-bbcc2e2c2f43">



STEP 4: Ensuring connectivity between the virtual machines using ping 

First off let's log into the client-1's server. Although we haven't opened up the firewall to ICMP traffic on the domain controller it will be good to observe how this change occurs. 


<img width="1005" alt="Screenshot 2024-04-04 at 15 39 27" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/d66926da-5d7a-4f36-8579-641096f44e2d">


Go to virtual machines then click on client 1. Find the public IP address and copy it. 


<img width="1018" alt="Screenshot 2024-04-04 at 15 42 24" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/39e03782-a3f8-4f39-8cfd-e639750b4ee1">


We will use to IP address to login to our virtual machine using either microsoft remote desktop on mac or remote desktop connection on windows. 
Enter in your username and password that you made earlier when creating this virtual machine. I hope you haven't forgot it. Then login to the machine. While client one is loading we can go to the domain controller virtual machine and find it's private IP address so that we can ping it. 
Scroll down a bit and you should be able to find it on the DC-1 virtual machine page. Remember this number.


Go back to the client 1 virtual machine. Go to the start menu and search for command prompt. 



<img width="787" alt="Screenshot 2024-04-04 at 15 44 20" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/95163786-630c-472f-b336-f743ddd7e4cc">


Once it's opened we can attempt to ping the domain controller by typing ping -t 10.0.0.4



<img width="973" alt="Screenshot 2024-04-04 at 15 45 08" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/6685cef5-e766-4234-9071-0d31fe267d22">



You'll see that the request keeps timing out. This is because the Domain controllers firewall is block ICMP traffic.


To fix this we need to go to DC-1 and copy the public IP Address. 
<img width="973" alt="Screenshot 2024-04-04 at 15 45 44" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/710c4703-95e5-46f4-aa95-037e69418226">


Then we can enter in the username and password we made earlier when creating this virtual machine. Once logged in go to the start menu and type in 'wf.msc'


<img width="393" alt="Screenshot 2024-04-04 at 15 49 14" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/5451de4b-5095-4594-bd2a-41dbf22eacf7">


One the left side plane click inbound rules. Then sort this list by protocol. 


<img width="1045" alt="Screenshot 2024-04-04 at 15 49 42" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/5c1e6223-c6fa-4b98-81a3-e67763fbefd3">


Find the icmpv4 files and enable both of them by righ clicking and selecting enable rule. 


<img width="721" alt="Screenshot 2024-04-04 at 15 50 19" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/130beecf-de29-4337-9898-b7644efbcb45">



<img width="721" alt="Screenshot 2024-04-04 at 15 50 55" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/73f9a25e-05a2-45bc-9dd0-cd1163c5928a">



<img width="363" alt="Screenshot 2024-04-04 at 15 52 20" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/fd5ff8fa-7739-4770-b2e2-4335dfc654b5">



Check back to client 1 and you see that the ping has started working. 



<img width="980" alt="Screenshot 2024-04-04 at 15 53 05" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/fd04f0f7-56f5-4e5f-adc9-13b1ac46bcc7">



To stop this ping press control + c. 



<img width="589" alt="Screenshot 2024-04-04 at 15 54 35" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/d493304f-25d7-4954-be7a-a53fb58cbd5f">


Step 5: Install Active dicertory domain services. 



Go back to DC-1 and open the server manager. Then click add roles and services so that we can begin to install active directory on DC-1. 


<img width="746" alt="Screenshot 2024-04-04 at 15 58 37" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/ba3d5638-ac69-4283-a4d8-08797d0e5d75">



You should see a text box like this. 
Then click next> next> next. 


<img width="787" alt="Screenshot 2024-04-04 at 15 58 59" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/37000991-47d7-4966-a211-222a3205d43c">


One this drop down menu make sure to click active directory doman services. 


Then add feature > next>  next > install. Then wait for the install to finish. 


<img width="327" alt="Screenshot 2024-04-04 at 16 00 15" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/835c5872-4f20-4ee3-a20b-84a47b5a4daf">


<img width="787" alt="Screenshot 2024-04-04 at 16 01 16" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/56a8983e-c48d-4f50-b4ca-f91d15934669">


Look at the for the flag at the top of the server manger and click on it. Find promote this servver into a domain controller and click on it. 



<img width="345" alt="Screenshot 2024-04-04 at 16 02 55" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/2a348176-db5a-4d06-9d2d-065836f18f94">



You should see a window like this. We can now name the server. I will name the server mydomain.com and click next.


<img width="344" alt="Screenshot 2024-04-04 at 16 05 25" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/5f0a5d51-8753-496f-b20f-17f2bd92cb0c">


![image](https://github.com/JospehAdetifa/configure-ad/assets/165278529/bc718de9-2cef-4b16-a6e2-9a1e4251abd0)


On the next page create a simple password that you can remember then click next. 


<img width="759" alt="Screenshot 2024-04-04 at 16 07 11" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/ad285003-50ce-4714-8f99-b3ea8b798f82">

<img width="759" alt="Screenshot 2024-04-04 at 16 08 27" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/1cb3e163-ab81-44e0-9da9-d1d0c18436e0">


Click Next a few more times and you should come to a final install screen like this. 


<img width="759" alt="Screenshot 2024-04-04 at 16 08 53" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/32a88f3c-7b49-4561-9f99-86a69c14001c">


Once the installation is finished you'll be promoted to sign out. Sign out the relog into the Domain controller using it's public IP address. Ensure that you look in with the conect of the domain. You can do this by entering the domain name \ user. 


<img width="442" alt="Screenshot 2024-04-04 at 16 13 37" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/8ee73aa5-2c97-4dcf-b399-e037b4879380">


STEP 7: Create Orginisational Units. 

Click start and search active directory. You'll see a screen like this. 


<img width="755" alt="Screenshot 2024-04-04 at 16 19 37" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/a889d2b3-572d-44ed-aeff-4e00ef7b57b1">


We are going to create our first organisational unit. Just think of these organisational units like folders. Right click on mydomain.com on the sidebar. Find new then click on organisational unit.  


<img width="755" alt="Screenshot 2024-04-04 at 16 20 16" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/eeb35804-35eb-4027-aef0-5dba4f715661">



We are going to make our first organisational unit called employees. Repeat this again and make one for admins. 


<img width="438" alt="Screenshot 2024-04-04 at 16 21 27" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/20a8cbee-b03f-4d92-aabd-da1897e18890">


STEP 8: Create another administrative account


Click on the admins organisational unit. Then right click the open space. Find new then go to user.


<img width="495" alt="Screenshot 2024-04-04 at 16 22 43" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/cc31f2ab-2a87-4ef6-95d3-279ad2f504cb">


Give this admin a username. My will be jane_admin. 


<img width="441" alt="Screenshot 2024-04-04 at 16 23 45" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/f2f464d8-c690-417a-b9d6-60718deb083b">


Then set the password and uncheck the box user must change the password at next login for the purposes of this tutorial. Then click next, then finsh to create the user.


<img width="441" alt="Screenshot 2024-04-04 at 16 24 11" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/11a6d9b3-a162-41ac-a517-3eda37b5018c">



Although we have created a user account it's not a admin yet its just a user. We need to give it permisssions. We need to assign it to the domain admins group. To do this right click jane.doe and go to properties.


<img width="269" alt="Screenshot 2024-04-04 at 16 24 44" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/c2c53426-8dc9-4796-ab68-82262a9c6a3f">


Click add then type in domains. Click check names to find the appropiate group to put jane in. 


<img width="415" alt="Screenshot 2024-04-04 at 16 25 04" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/f3dee38d-031c-4223-bb55-94b8c6e7f70d">

<img width="470" alt="Screenshot 2024-04-04 at 16 25 21" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/cf0e8b54-0d03-4586-ac99-0b425c3301f9">


Selcect domain admins then click ok. Finalise this update by clicking apply then ok. 


<img width="574" alt="Screenshot 2024-04-04 at 16 25 46" src="https://github.com/JospehAdetifa/configure-ad/assets/165278529/48e72ee2-a9b6-4e0f-8974-603b66ec021d">


STEP 9: Login as jane_admin 

From this point on we are going to log in as our own unique user instead of a generic on. First off Log out of the domain controller. Go back to the Azure portal and get the public IP address. Paste that into Remote desktop and now we are going to login using the detials we created for jane_admin. 


STEP 10: Join Client 1 to the domain


This will enable us to login to client one as jane_admin or any other account we make that is on the server. To do this we are going to we are going to set client 1 dns settings to the domain controllers private IP address. 




Go to DC-1 in the azure portal and find the private IP Address under NIC private IP. Remember this number. 


Go back to client 1. 


Go to networking and click change virtual NIC. 




On the side tab click DNS Servers. Click custom then paste DC-1 private IP address into the DNS section. Press save to contine and wait for it to save. 


Go to client-1 and click restart at the top. Be patient and wait for it to restart. 



Once it has restarted copy Client-1's public IP address from the Azure portal then login. 


Now we are ready to connect the 2 virtual machines. Right click the start menu and go to settings. 


You should see a screen like this 



































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
