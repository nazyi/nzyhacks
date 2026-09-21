---
categories: [dokumantasyon]
layout: post
lang: en
description: "The second part of the second lesson of the JumpCloud University Core course: adding users manually or via CSV, user security settings, user activation, and action buttons."
tool: JumpCloud
logo: "/assets/images/blog_icon/jumpcloud.png"
author: nazy
title: JumpCloud Core 2.2 - Creating Users
tags: [JumpCloud, Identity Management]
order: 3
permalink: /en/Jumpcloud-Core2-2
translation_url: /Jumpcloud-Core2-2
---

We're continuing with the second part of JumpCloud's second course.

## Adding Users Manually or via CSV

You can add users through different methods via **User Management > Users > + Users**.

### Manually

- After clicking **+ Users**, choose the **Manual User Creation** option.
- Enter the required information (first name, last name, username, etc.) and save the user.
- Set when you want the user to be activated.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/new-user-manual.webp' | relative_url }}" width="1000" height="537" alt="JumpCloud's manual new user creation form, showing the User Information fields">
</div>

#### User Security Settings

If you scroll down while creating a user, you'll see the **User Security Setting and Permission** section. From here you can control the user's password security, MFA settings, and permissions.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/user-security-settings.webp' | relative_url }}" width="1000" height="537" alt="User Security Settings and Permissions panel: password authority, MFA, and permission settings">
</div>

> If you want to add a custom attribute, you can do so by scrolling down to the **Custom Attributes** section.

### Via CSV File

- After clicking **+ Users**, choose the **Import from CSV** option.

> There's one small thing to watch out for here. The CSV file you upload has to be in the format JumpCloud expects. You can check the format by clicking **Download CSV Template**.

- You can import your properly formatted CSV file.
- After importing, you can select the people you want and create the users.

### User Activation

When creating an active user, JumpCloud will ask you to send an email so the user can set their password. However, this doesn't apply to users imported from a CSV file — for imported users, you need to trigger that email manually yourself.

#### Action Buttons

Let's go over the actions available in the **Actions** menu at the top right after clicking on a user:

- **Add to User Group**: Adds the selected people in bulk to a user group.
- **Send Activation Mail**: Sends an activation email to the selected person.
- **Send Password Reset Mail**: Only applies to active users. Sends a password reset email.
- **Force Password Change**: Immediately signs the user out of every application JumpCloud controls and forces them to change their password on their next login.
- **Unlock User Account**: Unlocks an account that got locked out from too many incorrect password attempts.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/actions-menu.webp' | relative_url }}" width="1000" height="537" alt="The Actions menu opened for a selected user on the Users page">
</div>

{% include flip-cards.html id="jc-actions-en" items=site.data.jc_actions_en hint="Click the cards to test yourself on what each one does." %}
