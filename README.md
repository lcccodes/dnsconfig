<h1>DNS Configuration in Azure </h1>
This outlines some basics about DNS operations.<br />


<h2>Environments, Technologies and Languages Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop connections to a server and client
- Active Directory Domain Services
- Active Directory Users and Computers
- Windows command line 

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>Overview</h2>

- Part 1: Creating and Observing A-records
- Part 2: About the local DNS cache
- Part 3: About CNAME records
- Part 4: Where to find Root Hints
  
<h2>Deployment and Configuration Steps</h2>

<b>Part 1: Setup of two VMs (Windows server and client) on the same region and vNet.</b>
<p>

  ![image](https://github.com/lcccodes/configure-ad/assets/171904823/84e26543-c927-4985-ab01-1822238f46d2)

</p>
<p>
Once you've got your server and client machines on the same vNet within the same region, your Resource Group page will show all of the associated resources which were automatically created with these [above]. These include the vNICs and Network Security Groups.

Deleting your resource group will automatically delete all resources contained within it. So if you need to delete only a single resource, it's best to do it from its own blade directly.
<p>
**NB: The first time I went through, it took me countless attempts to be able to validate a second VM if I was trying to put it in the same region and the same vNet. The only thing which eventually worked (after trying all kinds of combinations of which order I was creating each machine in) --- was waiting even longer before clicking "Review and Create." Even after it's clear that the same vNet used for the server is ready --- I deliberately added extra waiting time in case one of the other elements was still creating (I still don't know if that's what was going on). That's what finally worked.
</p>
You'll also need to change the settings of the vNIC for the server from dynamic to static. Go to the NIC from within the Network Settings on the server's blade and navigate from there.<p></p>


![image](https://github.com/lcccodes/configure-ad/assets/171904823/ecbac8f6-e776-4af9-a77d-49ba57fa5551)

</p>
<br />


<b>Part 2: Checking connectivity.</b>
<p>

  ![image](https://github.com/lcccodes/configure-ad/assets/171904823/2f645421-5f75-4d02-ab86-41b9cbdefea0)

</p>
<p>
Through Windows Defender Firewall (Advanced Settings) on the server, you'll need to first "enable" incoming ICMP traffic before you can ping the server from the client. Here you only need to enable the two lines for "Echo Request."
</p>
<br />


<b>Part 3: Install Active Directory and promote to a domain controller.</b>
<p>

  ![image](https://github.com/lcccodes/configure-ad/assets/171904823/1ca6c8df-2291-4bb7-95ec-0194f36fcb72)

</p>
<p>
[ABOVE]: After Active Directory installs, you should see a yellow exclamation mark in the upper right -- if you click on this, you'll see the option to "promte this to a domain controller." Click on that.
</p>
<p>

![image](https://github.com/lcccodes/configure-ad/assets/171904823/aae613cc-efc0-41e9-afec-4f085257b34a)


</p>
<p>
[ABOVE]: This is where you'll need to choose "Add a new forest" and also choose the domain name for the controller. All users will belong to this domain, and from here on out, will need to login through the domain when logging into the domain controller and any joined clients.

**NB: ISSUES LOGGING BACK INTO THE DOMAIN CONTROLLER:
</p>
<p>
  
  ![image](https://github.com/lcccodes/configure-ad/assets/171904823/0b9dade2-1ac6-4e3a-9313-d9da0a0b9066)


</p>
<p>
You'll need to keep the IP address for the COMPUTER NAME, but in the USERNAME field, you'll need to input the FQDN (Fully Qualified Domain Name): it will look something like this (based on whatever you input in the step above):

<b>mydomain.com\username</b>

The point here is to make sure you're inputting this as the USERNAME and not as the COMPUTER NAME.
</p>
<br />


