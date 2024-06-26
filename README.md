<h1>DNS Configuration in Azure </h1>
This outlines some basics about DNS operations. Remember that DNS translates between IP addresses and human-readable names. It works using TCP/UDP port 53.<br />


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
  
<h2>Navigation and Configuration</h2>

<b>Part 1: Creating and observing A-records</b>
<p>

  ![image](https://github.com/lcccodes/configure-ad/assets/171904823/84e26543-c927-4985-ab01-1822238f46d2)

</p>
<p>
A-records are the trail that gets left behind in the DNS cache after it resolves various addresses. In this sense, it's basically a dictionary of internet addresses.

</p>
<br />


<b>Part 2: About the local DNS cache</b>
<p>

  ![image](https://github.com/lcccodes/configure-ad/assets/171904823/2f645421-5f75-4d02-ab86-41b9cbdefea0)

</p>
<p>
Through Windows Defender Firewall (Advanced Settings) on the server, you'll need to first "enable" incoming ICMP traffic before you can ping the server from the client. Here you only need to enable the two lines for "Echo Request."
</p>
<br />


<b>Part 3: Creating a CNAME record</b>
<p>

![image](https://github.com/lcccodes/dnsconfig/assets/171904823/69e8d3fe-4e0d-4542-8114-76422d439455)


</p>
<p>
[ABOVE]: After Active Directory installs, you should see a yellow exclamation mark in the upper right -- if you click on this, you'll see the option to "promte this to a domain controller." Click on that.
</p>



<b>Part 4: Where to Find Root Hints within Server Manager</b>
</p>
<p>
  
![image](https://github.com/lcccodes/dnsconfig/assets/171904823/403e47d5-61a8-496c-a2c8-d15fa5bf1c68)



</p>
<p>
Root hints allow the DNS to resolve names and addresses that aren't yet in the cache. In Server Manager, you can reach this page from the same Tools menu in the upper right, then click on DNS, then your domain controller and right click "Properties" and find the Root Hints tab.
</p>
<br />


