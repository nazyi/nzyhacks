---
categories: [dokumantasyon]
layout: post
lang: en
description: "The third part of the second lesson of the JumpCloud University Core course: importing users through external directory integrations (M365/Entra ID, Google Workspace, Active Directory), custom API integrations, and HR integration."
tool: JumpCloud
logo: "/assets/images/blog_icon/jumpcloud.png"
author: nazy
title: JumpCloud Core 2.3 - Importing Users from External Sources
tags: [JumpCloud, Identity Management]
order: 4
permalink: /en/Jumpcloud-Core2-3
translation_url: /Jumpcloud-Core2-3
---

We're continuing with the third part of JumpCloud's second course.

## Importing Users from External Sources

JumpCloud supports a variety of cloud services and HR applications for importing users.

### Directory Integrations

By integrating JumpCloud with the applications it supports, you can import users or synchronize user accounts.

How does it work?

- A continuous, secure connection is established with the service you use.
- User data is imported from the service you use.
- Accounts that already exist in the service you use are imported.
- Data is exported from JumpCloud out to the service.
- User accounts can be deprovisioned from the service.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/directory-integrations-diagram.webp' | relative_url }}" width="1000" height="453" alt="Diagram of JumpCloud's Open Directory Platform importing/exporting and syncing with Google Workspace, Microsoft EntraID/365, BambooHR, and Personio on one side, and bob, Namely, Okta, and Workday on the other">
</div>

#### Selecting a Directory Integration

JumpCloud supports directories such as Google Workspace, Microsoft 365, and Active Directory. To integrate the directory you want:

- Go to **User Management > Cloud Directories**.
- Click the **+** button and select the directory you want to add.

### Importing Users from M365 & Google Workspace

You'll notice that the sync process is similar across every integration.

#### M365 & Entra ID Integration

With M365/Entra ID you can easily import users into JumpCloud and maintain control through continuous synchronization.

You'll need to re-trigger the connection if any of the following happens:

- The API key has expired.
- The API key is no longer valid.
- The Global Admin account has been deprovisioned.

To connect M365/Entra ID:

- Go to **User Management > Cloud Directories**.
- Click **+** and select **M365/Entra ID**.
- Name the directory, then sign in with the global admin account.
- Select the users you want to import.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/m365-import-users-modal.webp' | relative_url }}" width="1000" height="509" alt="The Import Users from M365/Entra ID window, showing the list of users selected to be imported">
</div>

- After importing the users, go to the **Users** section and select the user you want to sync.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/m365-directory-users-tab.webp' | relative_url }}" width="1000" height="294" alt="The Users tab in the Cloud Directories detail panel, showing users syncing to the M365/Entra ID instance">
</div>

- You can create a user group to collect these users together and bind it to the directory.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/m365-directory-user-groups-tab.webp' | relative_url }}" width="1000" height="359" alt="The User Groups tab in the Cloud Directories detail panel, showing the JumpCloud, LDAP, Linux Group, Managers, and Microsoft 365 groups">
</div>

#### Google Integration

With Google you can set up an import and sync connection similarly to M365/Entra ID.

> You need to connect JumpCloud using your Google Super Admin account.

To connect Google:

- Go to **User Management > Cloud Directories**.
- Click **+** and select **Google Workspace**.
- Name the directory, then sign in with the global admin account.
- Click **Start Manual Import**.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/google-import-users-panel.webp' | relative_url }}" width="1000" height="389" alt="The Google Cloud Directory detail panel, Import Users section, and the Start Manual Import button">
</div>

- Choose the action you want to take from here.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/google-import-options-modal.webp' | relative_url }}" width="1000" height="451" alt="The Import New Users and Update Existing Users from Google window, showing the import options">
</div>

- Select the user.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/google-select-user-import.webp' | relative_url }}" width="1000" height="301" alt="The Import New Users from Google window, showing a user selected to be imported">
</div>

- Just like with M365/Entra ID, remember to link the user and the user group with Google Workspace.

#### Attribute Mapping and Settings

You can manage your attribute selections with 3 different options:

- **Import**: The selected attributes are imported from Google Workspace into JumpCloud.
- **Export**: The selected attributes are exported from JumpCloud to the directory being used.
- **Exclude**: The selected attributes are left untouched.

#### User Flows

##### Staged User Flow

<div class="doc-tabs">
  <div class="doc-tab-buttons">
    <button type="button" class="doc-tab-btn active" data-tab="flow-staged-nopw-en">Without a Password</button>
    <button type="button" class="doc-tab-btn" data-tab="flow-staged-pw-en">With a Password</button>
    <button type="button" class="doc-tab-btn" data-tab="flow-staged-access-en">Access</button>
  </div>
  <div class="doc-tab-content">
    <div class="doc-tab-panel active" id="flow-staged-nopw-en" markdown="1">

**Staged User Without a Password**: If you bind a passwordless user to an external directory, you can choose to send the user an activation email.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/staged-user-flow-detail.webp' | relative_url }}" width="1000" height="538" alt="Detail page of a user in the Staged state, showing Password Expired and TOTP MFA enrollment statuses">
</div>

  </div>
    <div class="doc-tab-panel" id="flow-staged-pw-en" markdown="1">

**Staged User With a Password**: If you bind a user who has a password to an external directory, you can choose to send the user a welcome email.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/staged-user-flow-detail.webp' | relative_url }}" width="1000" height="538" alt="Detail page of a user in the Staged state, showing Password Expired and TOTP MFA enrollment statuses">
</div>

  </div>
    <div class="doc-tab-panel" id="flow-staged-access-en" markdown="1">

**Staged User Access**: If an account doesn't already exist, it's created once the user is bound.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/staged-user-flow-detail.webp' | relative_url }}" width="1000" height="538" alt="Detail page of a user in the Staged state, showing Password Expired and TOTP MFA enrollment statuses">
</div>

  </div>
  </div>
</div>

##### Active User Flow

<div class="doc-tabs">
  <div class="doc-tab-buttons">
    <button type="button" class="doc-tab-btn active" data-tab="flow-active-pw-en">With Password</button>
    <button type="button" class="doc-tab-btn" data-tab="flow-active-nopw-en">Without Password</button>
    <button type="button" class="doc-tab-btn" data-tab="flow-external-en">Externally Managed</button>
  </div>
  <div class="doc-tab-content">
    <div class="doc-tab-panel active" id="flow-active-pw-en" markdown="1">

**Active User With a Password**: JumpCloud sends users a notification email letting them know they've been added via the external directory, and that their password will be synced on their next login.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/active-user-with-password.webp' | relative_url }}" width="1000" height="538" alt="Detail page of an Active user whose Security Status shows Password Active">
</div>

  </div>
    <div class="doc-tab-panel" id="flow-active-nopw-en" markdown="1">

**Active Users Without a Password**: Once the user is bound, their password syncs when they log into the user portal.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/active-user-without-password.webp' | relative_url }}" width="1000" height="538" alt="Detail page of an Active user with Password Pending status, showing the option to send an activation email">
</div>

  </div>
    <div class="doc-tab-panel" id="flow-external-en" markdown="1">

**Externally Managed Passwords**: If a different password manager is being used, JumpCloud doesn't send the user any password-related emails.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/externally-managed-password.webp' | relative_url }}" width="1000" height="538" alt="Detail page of a user whose Security Status shows Federated, managed by an external IdP">
</div>

  </div>
  </div>
</div>

### Active Directory Integration

You can synchronize JumpCloud with your Active Directory structure. Doing this uses 2 agents (the import agent and the sync agent). There are 3 basic approaches you can take:

- Manage users, groups, and passwords within the AD structure.
- Manage users and passwords in AD, in JumpCloud, or in both.
- Manage users, groups, and passwords in JumpCloud.

To add an AD domain to JumpCloud:

- Go to **User Management > Active Directories**.
- Click **+ Add ADI Domain**.
- Select whichever of the 3 approaches mentioned above you want to use.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/ad-integration-define-step.webp' | relative_url }}" width="1000" height="383" alt="The New Active Directory (AD) Integration wizard, Define step: choosing where users and passwords are managed">
</div>

- Give your ADI a name.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/ad-integration-setup-step.webp' | relative_url }}" width="1000" height="227" alt="The New Active Directory (AD) Integration wizard, Setup step: entering the domain name">
</div>

- Configure the settings for how you'll be using the attributes.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/ad-integration-map-step.webp' | relative_url }}" width="1000" height="316" alt="The New Active Directory (AD) Integration wizard, Map step: JumpCloud and AD attribute mappings">
</div>

- You can review the details on the page that appears confirming your domain has been saved.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/ad-integration-configure-step.webp' | relative_url }}" width="1000" height="305" alt="The New Active Directory (AD) Integration wizard, Configure step: configuration summary and agent download links">
</div>

### External Identity Sources

If none of the existing applications fit your needs, you can build custom API integrations instead.

What you'll need:

- Documentation containing the technical information needed to set it up.
- Supported authentication methods (API Key, Bearer Token, OAuth 2.0).
- The JSON request and JSON response.

#### Creating a New Application

- Go to **Access > SSO Applications**.
- Click **+ Add New Application**.
- In the window that opens, click **Custom Application** at the bottom right.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/custom-app-select-application.webp' | relative_url }}" width="1000" height="356" alt="The Create New Application Integration wizard, Select Application step, with the Custom Application card highlighted">
</div>

- Since we're importing users, check **Import Users from this app**.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/custom-app-select-options.webp' | relative_url }}" width="1000" height="707" alt="The Create New Application Integration wizard, Select Options step, with Import users from this app selected">
</div>

- Enter the required information.

#### HR Integration

Because HR applications and JumpCloud provide a two-way connection, this removes the sync headaches around onboarding and offboarding in particular, making the whole process more consistent and easier to manage.
