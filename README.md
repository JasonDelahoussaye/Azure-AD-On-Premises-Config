# On-premises Active Directory Deployment in Azure Virtual Machines

![Microsoft Active Directory Logo](https://i.imgur.com/pU5A58S.png)

This tutorial provides a guide on how to deploy on-premises Active Directory within Azure Virtual Machines. The aim is to simplify the process and make it as easy to use as possible. We will focus on setting up Active Directory Domain Services (AD DS) on a Windows Server 2022 machine and joining a Windows 10 client to the domain. Additionally, we will cover creating user accounts, enabling remote desktop access, and other related tasks.

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

## Operating Systems Used

- Windows Server 2022
- Windows 10 (21H2)

<h2>Video Demonstration</h2>

- ### [How to Deploy on-premises Active Directory within Azure Virtual Machines](https://drive.google.com/file/d/11CHLY2jd5xKqcplNmbpM1vO99dYDDjzH/view?usp=drive_link)

## High-Level Deployment and Configuration Steps

1. **Setup Resources in Azure**

   - Create a Resource Group and Virtual Network (VNet) in Azure.
   - Create a Windows Server 2022 Virtual Machine (VM) named "DC-1" in the Resource Group and VNet.
   - Set the NIC Private IP address of the DC-1 VM to static.
   - Create a Windows 10 VM named "Client-1" in the same Resource Group and VNet.

2. **Ensure Connectivity between the Client and Domain Controller**

   - Connect to Client-1 using Remote Desktop and ping DC-1's private IP address.
   - If the ping fails, log in to DC-1 and enable ICMPv4 in the local Windows Firewall.
   - Verify that the ping from Client-1 to DC-1 succeeds.

3. **Install Active Directory**

   - Log in to DC-1 and install Active Directory Domain Services.
   - Promote DC-1 as a domain controller and set up a new forest with a domain name (e.g., mydomain.com).

4. **Create an Admin and Normal User Account in AD**

   - Open Active Directory Users and Computers (ADUC) on DC-1.
   - Create an Organizational Unit (OU) called "_EMPLOYEES" and "_ADMINS" within ADUC.
   - Create a new employee account named "Jane Doe" with the username "jane_admin" and add her to the "Domain Admins" Security Group.
   - Log out and log back in to DC-1 as "mydomain.com\jane_admin".

5. **Join Client-1 to the Domain**

   - Set Client-1's DNS settings to the private IP address of DC-1.
   - Restart Client-1 and log in as the local admin user.
   - Join Client-1 to the domain and wait for the machine to restart.
   - Log in to DC-1 and verify that Client-1 appears in ADUC under the "Computers" container.
   - Create a new OU named "_CLIENTS" and move Client-1 into it.

6. **Setup Remote Desktop for Non-Administrative Users on Client-1**

   - Log in to Client-1 as "mydomain.com\jane_admin" and open system properties.
   - Click on "Remote Desktop" and allow "domain users" access to Remote Desktop.
   - Non-administrative users can now log in to Client-1 using Remote Desktop.

7. **Create Additional User Accounts and Test Login**

   - Log in to DC-1 as "mydomain.com\jane_admin".
   - Open PowerShell ISE as an administrator and run the provided PowerShell script to create additional user accounts.
   - Verify that the accounts are created in the appropriate OU within ADUC.
   - Attempt to log in to Client-1 using one of the newly created user accounts.

By following these steps, you will successfully configure on-premises Active Directory within Azure Virtual Machines and establish a domain environment for user and resource management.

## Summary

This project involved the setup and configuration of on-premises Active Directory within Azure Virtual Machines. We created a Windows Server 2022 VM as a domain controller and a Windows 10 VM as a client. The deployment process included configuring network settings, ensuring connectivity, installing Active Directory, creating user accounts, joining the client to the domain, enabling Remote Desktop access, and testing user logins.
