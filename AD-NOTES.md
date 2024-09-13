# Learning Notes: Active Directory Implementation in Azure

## Overview
This lab involves setting up Active Directory in a cloud environment using Azure Virtual Machines. It covers creating a Domain Controller, configuring user management, and implementing security policies to simulate a typical enterprise setup.

---

### 1. Setting Up a Domain Controller in Azure

- **Purpose:**  
  A Domain Controller (DC) centralizes authentication, permissions, and directory services, making it the backbone of any Windows-based network. Setting up a DC in Azure allows for managing resources and users securely in the cloud.

- **Key Points to Remember:**
  - **Resource Group:** Acts as a container for Azure resources. Keep all related resources in the same group for easier management.
  - **Virtual Network (VNet):** Isolates resources in a secure, private network. This setup is crucial for ensuring that VMs can communicate securely without exposing them to the public internet.
  - **Static IP for DC:** Ensures that DNS resolution remains consistent. A dynamic IP could cause DNS failures, making the domain unreliable.
  - **Firewall Disabled (Testing Only):** Disabling the firewall is useful for initial connectivity tests but should be re-enabled for security after testing.

---

### 2. Configuring Active Directory Domain Services (AD DS)

- **Purpose:**  
  AD DS enables centralized management of users, computers, and security policies. It allows administrators to enforce rules, manage permissions, and secure resources across the domain.

- **Key Points:**
  - **Promoting to Domain Controller:** Involves setting up a new forest and domain (e.g., `mydomain.com`). This establishes the foundational structure of your network.
  - **Organizational Units (OUs):** OUs help organize users, computers, and other resources, allowing administrators to apply specific policies to different groups.
  - **Domain Admin User:** Creating domain-specific admin accounts helps manage the domain securely, separating everyday tasks from high-level administration.

---

### 3. Joining Clients to the Domain

- **Purpose:**  
  Joining a client to the domain centralizes management, allowing users to access resources with single sign-on (SSO) and receive consistent policy enforcement.

- **Key Points:**
  - **DNS Configuration:** Clients must have their DNS set to the Domain Controller’s IP to resolve the domain and join correctly.
  - **Verification:** After joining, always verify that the client appears in Active Directory Users and Computers (ADUC) to confirm successful integration.

---

### 4. Managing Users and Permissions

- **Purpose:**  
  Efficient user and permissions management is crucial for maintaining security and operational integrity within the domain.

- **Key Points:**
  - **Creating Domain Admins:** Domain Admins have extensive privileges; creating specific accounts for these roles enhances security.
  - **OUs and Security Groups:** Use OUs to group similar users and apply policies consistently. Security groups determine access levels and permissions within the domain.
  - **Remote Desktop Configuration:** Allowing domain users access through Remote Desktop is usually managed via Group Policies to apply settings across multiple systems efficiently.

---

### 5. Security Policies and Account Management

- **Purpose:**  
  Implementing security policies helps protect against unauthorized access, enforce compliance, and maintain the integrity of user accounts.

- **Key Points:**
  - **Account Lockout Policies:** Configuring policies to lock accounts after multiple failed login attempts protects against brute force attacks.
  - **Enabling/Disabling Accounts:** Use these settings to control access when employees leave or transition roles.
  - **Password Reset and Unlocking Accounts:** Be familiar with resetting passwords and unlocking accounts through ADUC, a common helpdesk task.

---

## Troubleshooting Tips

- **Failed Domain Joins:**  
  Check DNS settings on the client. Ensure it points to the Domain Controller’s IP. Verify network connectivity by pinging the DC.

- **Account Lockouts:**  
  Use Event Viewer and ADUC to track failed login attempts. Reset passwords and unlock accounts as necessary.

- **Connectivity Issues:**  
  Ensure the firewall settings are correctly configured, and that NSGs in Azure allow the required traffic between VMs.

---
