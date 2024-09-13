# Active-Directory-Implementation-in-Azure
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Active Directory Implementation"/>
</p>

<h1>Active Directory Implementation in Azure</h1>
In this project, we set up and manage Active Directory on Azure Virtual Machines to improve user and permissions management. The lab demonstrates configuring a Domain Controller, managing users, and implementing security features in a cloud environment.

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines)</li>
  <li>Active Directory Domain Services</li>
  <li>Windows Server 2022, Windows 10</li>
  <li>PowerShell</li>
</ul>

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows Server 2022 (Domain Controller)</li>
  <li>Windows 10 (Client)</li>
</ul>

<h2>High-Level Steps</h2>
<ol>
  <li>Setup Domain Controller in Azure</li>
  <li>Setup Client Machine and Connect to Domain</li>
  <li>Install and Configure Active Directory</li>
  <li>Manage Users and Permissions</li>
  <li>Configure Group Policies and Security Measures</li>
</ol>

<h2>Actions and Observations</h2>

<!-- Part 1: Setup Domain Controller in Azure -->
<h3>Part 1: Setup Domain Controller in Azure</h3>
<p>We begin by setting up a Domain Controller VM (Windows Server 2022) named DC-1 in Azure, assigning it a static private IP address, and disabling the firewall for initial connectivity testing.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Setting up Domain Controller" width="80%"/>
</p>
<p>Description of the setup process, including creating the Resource Group, Virtual Network, and setting up the Domain Controller VM.</p>

<h3>Setup Client-1 in Azure</h3>
<p>Next, we set up a client VM (Windows 10) named Client-1, ensuring it is connected to the same Virtual Network as DC-1 and setting its DNS to point to DC-1’s private IP address.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Setting up Client VM" width="80%"/>
</p>
<p>Observations on network connectivity and testing communication between Client-1 and DC-1 using ping and DNS settings.</p>

<!-- Part 2: Install Active Directory -->
<h3>Part 2: Install Active Directory</h3>
<p>We log into DC-1 to install Active Directory Domain Services, promoting it to a Domain Controller and setting up a new forest with a custom domain (e.g., mydomain.com).</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Installing Active Directory" width="80%"/>
</p>
<p>Details on the installation steps, setting up the domain, and the initial setup of the Domain Controller.</p>

<!-- Creating Domain Admin User -->
<h3>Create a Domain Admin User</h3>
<p>We create Organizational Units (OUs) for employees and admins, adding a new Domain Admin user named “Jane Doe” to manage the domain.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Creating Admin User" width="80%"/>
</p>
<p>Steps to create the OU, add users, and set permissions within Active Directory Users and Computers (ADUC).</p>

<!-- Part 3: Join Client-1 to the Domain -->
<h3>Part 3: Join Client-1 to the Domain</h3>
<p>Client-1 is configured to join the domain (mydomain.com), with DNS settings pointing to the Domain Controller. The setup is verified in ADUC, and Client-1 is moved into a designated OU.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Joining Domain" width="80%"/>
</p>
<p>Verification steps to ensure the client is correctly joined to the domain and visible in Active Directory.</p>

<!-- Part 4: Remote Desktop Setup for Non-Admins -->
<h3>Setup Remote Desktop for Non-Administrative Users</h3>
<p>We configure remote desktop access on Client-1, allowing domain users to access the machine, demonstrating typical user access management in a domain environment.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Remote Desktop Configuration" width="80%"/>
</p>
<p>Configuration steps for allowing remote desktop access to domain users and how this is typically managed through Group Policy.</p>

<!-- Part 5: Managing Users and Security Policies -->
<h3>Part 5: Managing Users and Security Policies</h3>
<p>Using PowerShell, we automate the creation of additional user accounts, manage account lockout policies, and explore enabling/disabling user accounts in Active Directory.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Managing Users with PowerShell" width="80%"/>
</p>
<p>Step-by-step walkthrough of scripting user creation, setting security policies, and troubleshooting account-related issues.</p>

<h2>Summary</h2>
<p>This project provides hands-on experience with setting up and managing Active Directory in a cloud environment, emphasizing user and permissions management, security configurations, and practical troubleshooting within Azure.</p>
