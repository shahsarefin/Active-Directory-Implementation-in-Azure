# Active Directory Lab Setup and Management

In this project, we set up and manage an Active Directory environment using Azure Virtual Machines. The lab is divided into four parts: preparing the infrastructure, deploying Active Directory, managing Remote Desktop access, automating user creation, and managing account policies and logs.

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Windows Server 2022
- Windows 10
- Active Directory Domain Services
- PowerShell

## Operating Systems Used

- Windows Server 2022
- Windows 10 (21H2)

## High-Level Steps

- Part 1: Prepare AD Infrastructure in Azure
- Part 2: Deploying AD and Configuring Domain
- Part 3: Remote Desktop Setup and Automated User Creation with PowerShell
- Part 4: Group Policy and Managing Account Lockouts

## Actions and Observations

### Part 1: Prepare AD Infrastructure in Azure

In this part, we set up the initial Active Directory infrastructure by creating a Domain Controller and a client machine within the same virtual network.

#### High-Level Steps

- Create Resource Group and Virtual Network
- Set up Domain Controller VM (DC-1)
- Configure Client VM (Client-1)
- Set static IPs and test connectivity

#### Actions and Observations

1. **Create Resource Group and Virtual Network**:
   - Created `AD-Infra-RG` in Canada Central.
   - Set up `AD-VNet` with `10.0.0.0/16` address space.

2. **Set up Domain Controller VM (DC-1)**:
   - Deployed Windows Server 2022 with the name `DC-1`.
   - Configured static IP and disabled the firewall for testing.

3. **Configure Client VM (Client-1)**:
   - Set up Windows 10 VM named `Client-1`.
   - Configured DNS to point to `DC-1` and verified connectivity with `ping`.

---

### Part 2: Deploying AD and Configuring Domain

This part covers the deployment of Active Directory, creating an admin account, and joining the client machine to the domain.

#### High-Level Steps

- Install Active Directory Domain Services
- Create Domain Admin Account
- Join Client-1 to the Domain
- Configure Organizational Units

#### Actions and Observations

1. **Install Active Directory Domain Services**:
   - Promoted `DC-1` to a domain controller with the domain `mydomain.com`.

2. **Create Admin Account**:
   - Created an admin user `jane_admin` and assigned Domain Admin rights.

3. **Join Client-1 to the Domain**:
   - Successfully joined `Client-1` to the domain `mydomain.com` and moved it to `_CLIENTS` OU.

---

### Part 3: Remote Desktop Setup and Automated User Creation with PowerShell

In this part, we configure Remote Desktop access for non-admin users and automate the creation of multiple user accounts using PowerShell.

#### High-Level Steps

- Configure Remote Desktop for Domain Users
- Automate User Creation with PowerShell
- Test Remote Access with Non-Admin Users

#### Actions and Observations

1. **Configure Remote Desktop for Non-Admin Users**:
   - Enabled Remote Desktop access for `Domain Users` on `Client-1`.

2. **Automate User Creation**:
   - Ran PowerShell script to create multiple users in the `_EMPLOYEES` OU.
   - Verified accounts in Active Directory.

3. **Test User Access**:
   - Logged into `Client-1` using a non-admin user created in this part, confirming successful configuration.

---

### Part 4: Group Policy and Managing Account Lockouts

This part covers configuring account lockout policies, managing user accounts, and observing security logs.

#### High-Level Steps

- Simulate Account Lockouts
- Configure Group Policy for Account Lockout Thresholds
- Manage User Account Status (Enable/Disable)
- Review Security Logs on DC-1 and Client-1

#### Actions and Observations

1. **Simulate Account Lockouts**:
   - Attempted multiple failed logins to trigger account lockout.

2. **Configure Group Policy**:
   - Set account lockout threshold to 5 attempts using Group Policy.

3. **Manage Account Status**:
   - Disabled and re-enabled a user account to observe login behavior.

4. **Review Security Logs**:
   - Observed relevant security events in Event Viewer on both `DC-1` and `Client-1`.

---
