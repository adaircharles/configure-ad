<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This outlines the implementation of Active Directory, group policy, and creating users within Azure Virtual Machines.<br />

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
In Azure, I created a Virtual Network and Subnet, then created a Domain Controller VM with a static NIC Private IP address, and disabled the Windows Firewall to test connectivity. I also created a Client VM attached to the same region and Virtual Network as the DC VM. I then set Client-1s DNS settings to the DC Private Ip Address.
</p>

![Azure vms and RGs](https://github.com/user-attachments/assets/4faef19f-680a-4895-9c9a-346b1fedca0f)

<br />
<p>
After logging in to the Domain Controller VM, I installed Active Directory Domain Services, promoted it as a Domain Controller, and set up a new forest - mydomain.com. After, I restarted and logged back into DC-1 as user: mydomain.com\labuser. After logging in, in Active Directory Users and Computers, I created the Organizational Units called "_EMPLOYEES" and "_ADMINS". After, I created user "Jane Doe", set her username and password and added her to the "Domain Admins" Security Group. I then logged out of the DC VM, and relogged into it as mydomain.com\jane_admin. I then logged into the Client VM as the original local admin and joined it to the domain. After the VM restarted, I logged back in to verify Client-1 showed up in ADUC. I then created a new OU named "_CLIENTS" and dragged Client-1 into the folder.
</p>

![screenshot5](https://github.com/user-attachments/assets/ad0620f8-76f7-4c05-a533-dd35dd69a92b)

![1 mydomain tree](https://github.com/user-attachments/assets/62080f6b-c78b-42e8-8108-f97808ec1dc4)

![CLient-1 is now in OU _CLIENTS](https://github.com/user-attachments/assets/596ce150-5fe4-43e8-a7f7-8037ada4c353)



<br />

<p>
As jane_admin on the DC-1 VM, I used Powershell_ise as an administrator to run a script in order to create 10,000 users accounts, which were placed in the OU "_EMPLOYEES". After the employees were created, I intentionally logged in with the incorrect credentials 10 times so that it would be locked out, then I unlocked the users account and reset their password within Active Directory. After doing so, I edited the domain policy to lock users our for 30 minutes after 5 invalid logon attempts.
</p>

![using a script to create 10000 users](https://github.com/user-attachments/assets/9f056ac4-495b-4719-8ff9-77acd959d6b4)

![Resetting users password and unlocking account](https://github.com/user-attachments/assets/47a8b357-88c5-4a17-86be-e62e0b0a0d4e)

![Setting group policy and lockouts](https://github.com/user-attachments/assets/fad3731d-c2f7-43ae-97f9-d72ec1e73d98)


<br />
