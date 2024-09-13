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

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Create a Resource Group in Azure:
    <ul>
      <li>Go to the Azure portal and click on "Resource Groups."</li>
      <li>Click "Create" and enter a name for your resource group (e.g., `AD-ResourceGroup`).</li>
      <li>Select your preferred region (keep this consistent for all resources).</li>
      <li>Click "Review + Create" and then "Create" to finish.</li>
    </ul>
  </li>

  <li>Create a Virtual Network and Subnet:
    <ul>
      <li>Navigate to "Virtual Networks" in the Azure portal and click "Create."</li>
      <li>Enter the name of the VNet (e.g., `AD-VNet`), choose your resource group, and set the region.</li>
      <li>In the IP Addresses section, configure the address space (e.g., `10.0.0.0/16`).</li>
      <li>Create a Subnet (e.g., `Subnet-1`) with a range (e.g., `10.0.1.0/24`).</li>
      <li>Click "Review + Create" and then "Create."</li>
    </ul>
  </li>

  <li>Create the Domain Controller VM (DC-1):
    <ul>
      <li>Go to "Virtual Machines" and click "Create."</li>
      <li>Choose Windows Server 2022 for the image, name the VM `DC-1`, and select your previously created resource group and VNet.</li>
      <li>Set the authentication method to password, and enter the credentials (Username: `labuser`, Password: `Cyberlab123!`).</li>
      <li>Once created, navigate to the VM’s Network Interface and set the Private IP to static.</li>
    </ul>
  </li>

  <li>Disable Windows Firewall on DC-1 (for testing):
    <ul>
      <li>Log into the VM using RDP with the credentials you set.</li>
      <li>Open PowerShell as an administrator and run: <code>Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled False</code></li>
    </ul>
  </li>
</ol>

<h3>Setup Client-1 in Azure</h3>
<p>Next, we set up a client VM (Windows 10) named Client-1, ensuring it is connected to the same Virtual Network as DC-1 and setting its DNS to point to DC-1’s private IP address.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Setting up Client VM" width="80%"/>
</p>

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Create the Client VM (Client-1):
    <ul>
      <li>Go to "Virtual Machines" and click "Create."</li>
      <li>Select Windows 10 for the image, name the VM `Client-1`, and choose the same resource group and VNet as DC-1.</li>
      <li>Use the same credentials as DC-1 (Username: `labuser`, Password: `Cyberlab123!`).</li>
      <li>Once the VM is created, navigate to its network settings and set the DNS to the private IP of DC-1.</li>
      <li>Restart Client-1 from the Azure portal to apply DNS settings.</li>
    </ul>
  </li>

  <li>Testing Connectivity:
    <ul>
      <li>Log into Client-1 via RDP and attempt to ping DC-1’s private IP to ensure connectivity.</li>
      <li>Open PowerShell on Client-1 and run <code>ipconfig /all</code> to verify DNS settings point to DC-1.</li>
    </ul>
  </li>
</ol>

<!-- Part 2: Install Active Directory -->
<h3>Part 2: Install Active Directory</h3>
<p>We log into DC-1 to install Active Directory Domain Services, promoting it to a Domain Controller and setting up a new forest with a custom domain (e.g., mydomain.com).</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Installing Active Directory" width="80%"/>
</p>

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Install Active Directory Domain Services:
    <ul>
      <li>Log into DC-1 and open Server Manager.</li>
      <li>Click "Add roles and features," select "Active Directory Domain Services," and install.</li>
    </ul>
  </li>

  <li>Promote DC-1 as a Domain Controller:
    <ul>
      <li>After installation, click "Promote this server to a domain controller."</li>
      <li>Choose "Add a new forest" and enter your domain name (e.g., `mydomain.com`).</li>
      <li>Follow the prompts, setting a DSRM password, and complete the promotion process.</li>
      <li>Restart DC-1 and log back in as `mydomain.com\labuser`.</li>
    </ul>
  </li>
</ol>

<h3>Create a Domain Admin User</h3>
<p>We create Organizational Units (OUs) for employees and admins, adding a new Domain Admin user named “Jane Doe” to manage the domain.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Creating Admin User" width="80%"/>
</p>

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Create Organizational Units (OUs):
    <ul>
      <li>Open Active Directory Users and Computers (ADUC) on DC-1.</li>
      <li>Create an OU named `_EMPLOYEES` and another named `_ADMINS`.</li>
    </ul>
  </li>

  <li>Create a Domain Admin User:
    <ul>
      <li>Within `_ADMINS`, create a user named `Jane Doe` with the username `jane_admin` and password `Cyberlab123!`.</li>
      <li>Add `jane_admin` to the "Domain Admins" security group.</li>
      <li>Log out of DC-1 and log back in as `mydomain.com\jane_admin`.</li>
    </ul>
  </li>
</ol>

<h3>Join Client-1 to the Domain</h3>
<p>Client-1 is configured to join the domain (mydomain.com), with DNS settings pointing to the Domain Controller. The setup is verified in ADUC, and Client-1 is moved into a designated OU.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Joining Domain" width="80%"/>
</p>

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Join Client-1 to the Domain:
    <ul>
      <li>Log into Client-1 and go to System Properties > Computer Name > Change.</li>
      <li>Enter the domain name (e.g., `mydomain.com`) and provide domain admin credentials.</li>
      <li>Restart Client-1 to complete the domain join.</li>
    </ul>
  </li>

  <li>Verify in ADUC:
    <ul>
      <li>On DC-1, open ADUC and ensure Client-1 appears in the domain.</li>
      <li>Create an OU named `_CLIENTS` and move Client-1 into it.</li>
    </ul>
  </li>
</ol>

<h3>Setup Remote Desktop for Non-Administrative Users</h3>
<p>We configure remote desktop access on Client-1, allowing domain users to access the machine, demonstrating typical user access management in a domain environment.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Remote Desktop Configuration" width="80%"/>
</p>

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Configure Remote Desktop Access:
    <ul>
      <li>Log into Client-1 as `mydomain.com\jane_admin`.</li>
      <li>Open System Properties, go to "Remote Desktop," and allow access for "Domain Users."</li>
    </ul>
  </li>

  <li>Test Remote Access:
    <ul>
      <li>Log out and attempt to log into Client-1 as a standard domain user.</li>
    </ul>
  </li>
</ol>

<h3>Managing Users and Security Policies</h3>
<p>Using PowerShell, we automate the creation of additional user accounts, manage account lockout policies, and explore enabling/disabling user accounts in Active Directory.</p>
<p align="center">
  <img src="INSERT_IMAGE_URL" alt="Managing Users with PowerShell" width="80%"/>
</p>

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Create Additional Users with PowerShell:
    <ul>
      <li>Log into DC-1 as `jane_admin` and open PowerShell ISE as an administrator.</li>
      <li>Create a new script to add multiple users, specifying the username, password, and OU.</li>
    </ul>
  </li>

  <li>Manage Account Lockout Policies:
    <ul>
      <li>Use Group Policy Management to set lockout thresholds (e.g., lock after 5 failed attempts).</li>
      <li>Test account lockouts by entering incorrect credentials multiple times.</li>
      <li>Unlock and reset passwords as needed in ADUC.</li>
    </ul>
  </li>
</ol>

### Purpose of the Lab

The purpose of this lab is to provide hands-on experience in setting up and managing Active Directory in a cloud environment using Azure Virtual Machines. This lab demonstrates how to configure a Domain Controller, manage user accounts, and implement security measures such as account lockout policies. It aims to simulate real-world scenarios commonly encountered in IT support roles, enhancing skills in user and permissions management, security configurations, and troubleshooting within an Active Directory domain.

### Key Learnings

- **Active Directory Setup:**  
  Learn how to install and configure Active Directory Domain Services, promote a server to a Domain Controller, and set up a new forest and domain.

- **User and Permissions Management:**  
  Gain practical experience in creating and managing user accounts, security groups, and organizational units (OUs) within Active Directory.

- **Account Security Policies:**  
  Understand how to configure account lockout policies, reset passwords, and manage account security settings to enhance network security.

- **Domain Joining and Client Management:**  
  Learn the steps to join client machines to a domain, manage them within Active Directory, and apply group policies for consistent configuration across the network.

- **Troubleshooting AD Issues:**  
  Develop skills in diagnosing and resolving common Active Directory issues, such as account lockouts, DNS resolution problems, and domain connectivity failures.

### Concepts Taught by This Lab

- **Directory Services Management:**  
  Understand the core functions of Active Directory as a centralized management system for user authentication, permissions, and security.

- **Organizational Units and Group Policies:**  
  Learn how OUs and GPOs are used to structure and manage users and computers within a domain, applying policies to enforce security and configuration standards.

- **Security Best Practices in AD:**  
  Explore best practices for securing Active Directory environments, including the management of administrative accounts, implementation of security groups, and configuration of access controls.

- **Remote Access Configuration:**  
  Set up and configure remote desktop access for users, demonstrating the ability to manage access permissions and troubleshoot connectivity issues.

- **Automation with PowerShell:**  
  Use PowerShell scripts to automate common administrative tasks in Active Directory, such as user creation and bulk management operations.


