# How-to-deploy-AD-and-create-OUs-and-Users


<h1>Configuring Windows Server Domain Controllers and OUs in Azure</h1>

<h2>Description</h2>
This lab will guide you through a step-by-step process of deploying a Windows Server Domain Controller in Azure, structuring the directory with Organizational Units (OUs), and managing user accounts and administrative permissions.
<br />


<h2>Utilities Used</h2>

- <b>Azure</b>
- <b>Powershell</b> 
- <b>Active Directory</b>

<h2>Environments Used </h2>

- <b>Windows Server 2022</b>
- <b>Windows 10 Enterprise</b>

<h2>Prerequisites </h2>

- <b>An Azure Account/Subscription (paid or free)</b>
- <b>Pre-created Resource Group in Azure</b> <br/>
    (See Lab: <a href="https://github.com/Active-Directory-Labs/Building-a-Foundational-AD-Environment-in-Microsoft-Azure/blob/main/README.md"> See "Creating the Resource Group" Section</a>)
- <b>2 Pre-created Windows Virtual Machines(VM) on the same subnet in Azure (1 Windows Server 2022 VM + 1 Windows 10 Enterprise VM) </b> <br/>
    (See Lab: <a href="https://github.com/Active-Directory-Labs/Building-a-Foundational-AD-Environment-in-Microsoft-Azure/blob/main/README.md"> How to create two Virtual Machine(s) in the same subnet</a>)

<h2>Keywords </h2> 

- <b>OS = Operating System </b> </br>

- <b>OU(s) = Organizational Unit(s)</b> </br>

- <b>VM = Virtual Machine</b> </br>

- <b>AD = Active Directory</b> </br>

- <b>ADUC = Active Directory Users and Computers</b> </br>

- <b>DNS = Domain Name Server</b> </br>

- <b>DC = Domain Controller</b> </br>

- <b>VNet = Virtual Network</b> </br>

- <b>RG = Resource Group</b> </br>


<h2>Labs walk-through:</h2>

<h3>Installing Active Directory Domain Services on VM:</h3>

<p align="center">
1. Log into the Pre-created DC VM and install Active Directory Domain Services. To do so, open Server Manager in the DC VM and click on Add roles and features: <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/1.%20Open%20the%20DC%20VM%20and%20install%20Active%20Directory%20Domain%20Services..png" width="80%" alt=""/>
<br />
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/1.0%20To%20do%20so%20open%20Server%20manager%20in%20the%20DC%20VM%20and%20click%20on%20Add%20roles%20and%20features.png" width="80%" alt="1.0"/>
<br />
</p>

<h4>During Installation:</h4>

<p align="center">
2. You will then be prompted for the installation of certain features, and during the installation setup, make sure the server is the exact server, or better put the exact Private IP address of the DC:
    <br/>
<br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/2YOUWI~1.PNG" height="80%" width="80%" alt=""/>
<br />
<br />
</p>

<p align="center">
3. While setting up the installation, click on Active Directory Domain Services under Server roles:  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/3.%20While%20setting%20up%20the%20installation%20click%20on%20Active%20Directory%20Domain%20Services%20under%20Server%20roles.png" height="80%" width="80%" alt=""/>
<br />
<br />
</p>

<p align="center">
4. A pop-up screen will appear when you select Active Directory Domain Services. On the pop-up, click on Add features.:<br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/4.%20A%20pop%20up%20screen%20will%20appear%20when%20you%20select%20Active%20Directory%20Domain%20Services%2C%20on%20the%20pop%20up%20click%20on%20Add%20features..png" alt=""/>
<br />
<br />
</p>

<p align="center">
5. After that, you can install. After the installation, click on close:  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/5.%20After%20that%20you%20can%20install.png" height="80%" width="80%" alt=""/>
<br />
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/5.1%20After%20the%20insall%20Click%20on%20close.png" height="80%" width="80%" alt="5.1"/>
<br />
</p>

<h3>Promoting DC/DC 1/a Virtual Machine to actual Domain Controller:</h3>

<p align="center">
6. Now we are going to promote this/the DC VM to an actual Domain Controller. To do so, click on the Flag with a caution mark on the right-hand corner and then click on the Promote this server to Domain C:  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/6NOWWE~1.PNG" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
7. A pop-up window will appear where you can input your domain's name or join it to an already existing one. Click on add new forest as we are creating a new domain, and add your custom domain name: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/7APOPU~1.PNG" width="80%"/>
<br />
<br />
</p>

<p align="center">
8. Under Domain Controller Options, input a Password you can remember, leave the other settings as is, and click on Next: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/8.%20Under%20Domain%20Controller%20Options%20input%20a%20Password%20you%20can%20remember%2C%20leave%20the%20other%20settings%20as%20is%20and%20click%20on%20Next.png" height="80%" width="80%"/>
<br />
<br />
</p>

<h3>During Installation Disable DNS Delegation:</h3>

<p align="center">
9. Under DNS Options, disable DNS Delegation. A DNS delegation is essentially a pointer in a parent DNS zone that tells clients/users/computers connected to the DC where to find the authoritative DNS servers for a child zone. For example, if your parent zone is present and you’re creating a child domain, the wizard can automatically add a delegation pointing to the DNS server for guidance. This helps DNS queries flow correctly from parent to child zones without manual configuration. So, since this DNS server is not a child server that will be linked to a parent server, there is no need to have the DNS delegation option on. When DNS delegation is disabled, the checkbox should be unchecked. (It should look like the second image below.) <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/9.%20Under%20DNS%20Options%20disable%20DNS%20Delegation..png" height="80%" width="80%"/>
<br />
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/9.0%20DNS%20delegation%20disabled.png" height="80%" width="80%" alt="9.0"/>
<br />
</p>

<p align="center">
10. Click next until you reach the final installation page, and then install the VM. It will restart, and you will have to re-login: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/10CLIC~1.PNG" height="80%" width="80%"/>
<br />
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/10.0%20After%20Install%20restart.png" height="80%" width="80%" alt="10.0"/>
<br />
</p>


<p align="center">
11. When logging back into the DC VM, you will now need to indicate the context of who is logging in, like so: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/11.%20When%20logging%20back%20into%20the%20the%20DC%20VM%20you%20will%20now%20need%20to%20indicate%20context%20of%20who%20is%20logging%20in%20like%20so.png" height="80%" width="80%"/>
<br />
<br />
</p>

<h3>Connecting the client/user VM to the newly promoted Domain Controller:</h3>

<p align="center">
12. Now we have to connect the other Pre-created VM to the Domain Controller ,to do so, launch and log into the Client VM connected to the same subnet and go to the About settings of the VM: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/12.%20Open%20%26%20Launch%20the%20Client%20VM%20connected%20to%20the%20same%20subnet%20and%20go%20to%20the%20About%20settings%20of%20the%20VM.png" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
13. Click on Advanced System settings, which will open a pop-up window. From there, go to Computer Name and click on Change: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/13.%20Click%20on%20Advanced%20System%20settings%2C%20it%20will%20open%20a%20pop%20up%20window.%20From%20there%20go%20to%20Computer%20Name%20and%20click%20on%20Change.png" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
14. When you click on change another Window will pop up. From that window, click on Domain and input the domain name we initialized in the Domain controller when promoting the DC VM (Step 7): <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/14WHEN~1.PNG" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
15. Another pop-up window will appear, prompting you to input your login details. Input the same details the same way you did when logging into the Domain controller after it was promoted: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/15ANOT~1.PNG" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
16. If everything checks out, this message should appear: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/16.%20If%20everything%20checks%20out%20this%20message%20should%20appear.png" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
17. After the Client VM will initiate a restart to update the changes: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/17.%20After%20the%20Client%20VM%20will%20restart%20to%20update%20the%20changes.png" height="80%" width="80%"/>
<br />
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/17.0%20Restart.png" height="80%" width="80%" alt="17.0"/>
<br />
</p>

<h3>Check if Client VM is connected to DC:</h3>

<p align="center">
18. Now, to check if the Client VM is connected to the Domain. Go to the Domain Controller VM and open the ADUC - Active Directory Users and Computers: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/18NOWT~1.PNG" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
19. In ADUC, you will see the name of your domain. Click on it and go to the Computers OU. Under the Computers OU, you should see the Name of the newly added VM: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/19INAD~1.PNG" height="80%" width="80%"/>
<br />
<br />
</p>

<h3>Creating OUs for new user storage:</h3>

<p align="center">
20. Now we are going to create a new user, but first we need to create an organizational unit (OU) for the employees. To do so, go to the action bar in ADUC and click on New and then OU: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/20NOWW~1.PNG" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
21. You will then be prompted to input a name for the OU. I suggest using an underscore if you plan on bulk adding users via a PowerShell script: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/21.%20You%20will%20then%20be%20prompted%20to%20Input%20a%20name%20for%20the%20OU%2C%20I%20suggest%20using%20an%20underscore%20if%20you%20plan%20on%20bulk%20adding%20users%20using%20Powershell.png" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
22. Untick the Protect from Accident deletion unless you want to give yourself a lengthy task of giving users permissions to delete the file and also having to disable this later: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/22UNTI~1.PNG" height="80%" width="80%"/>
<br />
<br />
</p>

<h3>Create New user:</h3>

<p align="center">
23. Now, to create a new user, you need to click on the Action bar, click on New, and then User: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/23.%20Now%20to%20create%20a%20new%20user%20you%20need%20to%20click%20on%20the%20Action%20bar%20click%20on%20New%20and%20then%20User.png" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
24. You will be prompted to fill in the user details such as their name and initials: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/24.%20You%20will%20be%20prompted%20to%20fill%20in%20the%20user%20details%20such%20as%20their%20name%20and%20initials.png" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
25. Next, you will input the user's login details. I ticked the "Password never expires" box just for convenience, but this SHOULD NEVER BE DONE. Passwords should be changed regularly to avoid successful brute force attacks from Bad Actors: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/25.%20Next%20you%20will%20input%20the%20user's%20login%20details%20I%20ticked%20the%20Password%20never%20expires%20just%20for%20convenience%20but%20this%20SHOULD%20NEVER%20BE%20DONE.png" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
26. Now the user should appear in the OU they were created in.: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/26.%20Now%20the%20user%20should%20appear%20in%20the%20OU%20they%20were%20created%20in..png" height="80%" width="80%"/>
<br />
<br />
</p>

<h3>Add new user to Domains Security Group:</h3>

<p align="center">
27. To add a user to the Domain Admins security group, right-click on the User and go to properties. From Properties, click Members of. You should be able to see what OUs/groups they are a part of from there: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/27TOAD~1.PNG" height="80%" width="80%"/>
<br />
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/27.1%20Click%20Member%20of.png" height="80%" width="80%" alt="27.1"/>
<br />
</p>

<p align="center">
28. If they are not part of the Admins, then you can manually add them by clicking add and searching for the Domain Admins OU. This can be done by a simple search in the Advanced search option: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/28IFTH~1.PNG" height="80%" width="80%"/>
<br />
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/28.0%20This%20is%20advanced%20search.png" height="80%" width="80%" alt="28.0"/>
<br />
</p>

<p align="center">
29. Once you've found the OU, click OK, the new OU should appear in the list of OUs the User is a part of. The new list of OUs or Groups should now be displayed and will show which group the User is a part of: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/29.%20Once%20you've%20found%20the%20OU%20click%20OK%2C%20the%20new%20OU%20should%20appear%20in%20the%20list%20of%20OUs%20the%20User%20is%20a%20part%20of..png" width="80%"/>
<br />
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/29.0%20New%20List%20of%20OUs%20or%20Groups%20User%20is%20a%20part%20of.png" width="80%" alt="29.0"/>
<br />
</p>

<p align="center">
30. Once you're done, click apply to set the new changes: <br />
  <br/>
<img src="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/Zwelakhe-Y-LAB-2-image-resources/30.%20Once%20you're%20done%20click%20apply%20to%20set%20the%20new%20changes.png" height="80%" width="80%"/>
<br />
<br />
</p>


<p align="center">
<b> And you're done, you have now successfully deployed Active Directory Domain Services + Domain Controller and created a new user and Organizational Units within ADUC. Don't forget to disable/stop your virtual machine on Azure once done(remember you pay as you use): </b>  <br/>
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

