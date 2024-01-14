<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resources in Azure (Virtual Machines | Windows Server 2022)
- Set Connectivity between Domain Controller (DC) with Client-11
- Install Active Directory
- Create Admin and User accounts in AD
- Join client-1 to Domain Controller-1
- Set up Remote Desktop for non-administrative users on client 1

<h2>Deployment and Configuration Steps</h2>

<p>

![Screen Shot 2024-01-14 at 11 48 49](https://github.com/TheTechPrince/configure-ad/assets/128175325/dc21e14b-3769-4d22-87b2-2a18b749e6ec)

 ![Screen Shot 2024-01-14 at 12 09 24](https://github.com/TheTechPrince/configure-ad/assets/128175325/b1938f34-c3b2-4d91-bbdf-b3ad228b8583)


</p>
<p>
    
My first step is to create a Resource Group and VMs (DC-1 and Client-1). Once I have created the Domain Controller VM I take the following steps:
   
- Set DC-1 NIC Private IP address to static
- I create the Client-1 VM on a Windows 10 using the same Resource Group created for the Domain Controller(DC-1).
- Confirm connectivity between Client-1 and DC-1
  - Using Remote Desktop on Client-1 and ping with perpetual ping
  - Login to DC-1: enable ICMPv4 on the local Windows Firewall (view ping success on Client-1 perpetual ping)

</p>
<br />

<p>

  ![Screen Shot 2024-01-14 at 13 03 57](https://github.com/TheTechPrince/configure-ad/assets/128175325/3ac64d14-e901-40a4-bfef-02c86c48cddb)

</p>
<p>
In this step, I install Active Directory within our DC-1.  I take a few steps to complete this action as follows:

- Log in to DC-1
   - Server Manager -> add roles and features -> select server role : _active_ _directory_ _domain_ _services_
- Set up a new forest, ex: _mydomain.com_ restart -> log back into DC-1
- In Active Directory User and Computers I create an Organizational Unit (OU) called "_EMPLOYEES" and "_ADMINS"
      - Created a sample employee as an admin and added to the "Domain Admins" Security Group
</p>
<br />

<p>
 
  ![Screen Shot 2024-01-14 at 13 47 01](https://github.com/TheTechPrince/configure-ad/assets/128175325/95bc754e-96ce-4e16-8bdd-aadc86149f3b)

</p>
<p>
For the final steps, I will join Client-1 in the domain I created and set up a remote desktop for non-administrative users on Client-1. Here are the steps I took to complete this action

  - From the Azure portal, I set Client-1's DNS settings to the DC-1 Private IP address
  - I restarted Client-1, logged in as the original local admin to join the domain
  - Logged in to DC-1 to verify Client-1 is active on Active Directory Users and Computers
  - I created a new OU (Organizational Unit) named "_Clients" and moved Client-1 into this folder

Setup for Remote Desktop non-admin users on Client-1 

- Logged into Client-1 as an admin
- System “Remote Desktop”
- Allow “domain users” group access to remote desktop
- You can now log into Client-1 as a normal, non-administrative user


</p>
<br />
