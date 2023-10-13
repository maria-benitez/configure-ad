<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This project outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/336a30e0-1225-4038-85ba-985cf0516b81">
</p>
<p>
Created two virtual machines using Microsoft Azure. Domain Controller will be the VM1 and Client 1 will be VM2. I have also changed the Domain Controller's NIC Private IP address to be static.
</p>
<br />

<p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/5e06aa94-5cf6-4985-a88e-8d75e38fbfb1">
</p>
<p>
I initiated a perpetual ping from Client 1 to Domain Controller. I did this because I am going to modify the firewall on Domain Controller to allow ICMP traffic. I want to then observe that modification on Client 1.
</p>
<br />

<p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/74d7595a-1ff8-41a2-86c3-725ba3e61289">
</p>
<p>
After modifying the firewall on Domain Controller, I can observe that ICMP traffic has been established between both virtual machines.
</p>
<br />

<p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/ce9fad56-0ecc-400e-bd25-b0eb6c1a17b2">
<p>
<img width="754" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/dfa47939-2d35-4e6e-8495-88e0d1f03a19">
</p>
<p>
Active Directory Domain Services has been installed on Domain Controller and a new forest has been created. I will now create Admins and Employees Organizational Units (OU) in Active Directory Users and Computers (ADUC).
<p></p>
<br />

<p>
<img width="754" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/803478fa-1d04-4167-9e5e-589d531c81fc">
</p>
I created a new user named 'Jane Doe' and she will be part of the _ADMINS group. She will also be added to the "Domain Admins" security group. I will then log out of Domain Controller and use the Jane Doe admin account I created from here on out.
</p>
<br />

<p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/1ff8b9d1-ba1b-4e6b-b92c-07058d91e0b1">
</p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/7e0c6823-7d18-479e-a3fe-92bb26ab2866">
<p>
Next, I will join Client 1 to the domain created on Domain Controller. For this, I have to change the DNS of Client 1. To make this change, I will obtain Domain Controller's NIC Private IP through Azure. 
</p>
<br />

<p>
<img width="754" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/4f5fad27-dc8d-4641-a38b-6231747c207c">
</p>
Once Client 1 is joined to the domain, it will restart. once it comes back online, I will be able to log into it with the domain admin account even though it never existed on Client 1. This is because Client 1 is now part of the domain and jane_admin is an admin within the domain, that account can be used to log into any computer that is on the domain.
</p>
<br />

<p>
<img width="549" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/edf4e893-a5b5-4b5c-886a-9e2d60ac13b3">
</p>
As it stands, only domain admins/administrators are able to remotely log into Client 1. I am going to change this by allowing all domain users to log into Client 1.
</p>
<br />

<p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/22229b14-ba87-4f13-bd67-69e08f048fc2">
</p>
From Domain Controller I can observe that all domain users are now allowed to log into Client 1. I will now test this.
</p>
<br />

<p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/20efb4d3-0a8d-4e80-8d69-88c041d99535">
</p>
On Domain Controller, I will be using Powershell ISE as an administrator and a script (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1/)  to create additional users to attempt to log into Client 1 with one of the said users.
</p>
<br />

<p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/a66ff06f-fda5-4096-8c0f-868d36d4288d">
</p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/6499e072-6f1d-4e12-9fb5-0dded0ce6c17">
</p>
I will use one of the users randomly generated to log into Client 1.
</p>
<br />

<p>
<img width="866" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/7972d262-a255-41a2-b905-2c49018e4ec6">
</p>
In Client 1, by using whoami command and by looking at the users who have logged into Client 1, I can see that I was succesfully able to log into Client 1 with a random user. 
</p>
<br />

<p>
<img width="1440" alt="image" src="https://github.com/maria-benitez/configure-ad/assets/147643771/f3de3bd8-33c3-4ee4-9086-52c9c4e39861">
</p>
To finish off, I will delete the virtual machines and research groups on Azure. 
