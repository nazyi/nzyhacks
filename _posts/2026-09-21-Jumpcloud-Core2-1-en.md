---
categories: [dokumantasyon]
layout: post
lang: en
description: "The first part of the second lesson of the JumpCloud University Core course: user creation/import methods, user states, password status, and matching usernames with local user accounts."
logo: "/assets/images/blog_icon/jumpcloud.png"
author: nazy
title: JumpCloud Core 2.1 - Creating Users
tags: [JumpCloud, Identity Management]
order: 2
permalink: /en/Jumpcloud-Core2-1
translation_url: /Jumpcloud-Core2-1
---

The second lesson of the JumpCloud Core course continues with creating and importing users.

## Preparing to Add Users

**Identity Management > Users**

There are different methods you can use to add users. Let's look at the options that appear when you click the **+ Users** button:

- **Manual**: You can add a user by hand.
- **Import via CSV**: You can import users from a CSV file.
- **Via API**: You can add users using JumpCloud's REST API support.
- **Via External Apps**: You can add users through supported integrations like Google, Microsoft 365, or various HR applications.

### User States

- **Staged**: The state before a newly hired user's account is activated.
- **Active**: The state after the user activates their account via the activation email.
- **Suspended**: The state where the user's account is suspended. The user has no permissions at all.

> You can configure a new hire's default account state from **User > Settings**.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/users-list.webp' | relative_url }}" width="1000" height="416" alt="JumpCloud Users page showing the user list, state tabs, and password/MFA columns">
</div>

### Managing User States

There are a few ways to change a user's state:

- You can set a new hire's default account state to staged or active.
- You can either schedule when a user becomes active, or do it manually yourself.
- Likewise, you can either schedule suspending an account or handle it manually.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/user-states-flow.webp' | relative_url }}" width="700" height="173" alt="User state flow: transitions between Staged, Active, Suspended, and Deleted">
</div>

### Password Status

- **Pending**: The user needs to complete the steps sent to their email.
- **Active**: The user can use their JumpCloud account without any issues.
- **Expired**: If the user can still access their email, a password reset link can be sent there.
- **Lock Out**: If the user can access their email address, a password reset link can be sent to their inbox.
- **Federated**: Means a third-party password provider is being used.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/password-status.webp' | relative_url }}" width="1000" height="598" alt="Users page filtered to Active, with the Password Status column highlighted">
</div>

### Determining Username Conventions

Naming users correctly plays an important role. If your company uses multiple IdPs, or imports users from many different applications, you need to be careful to follow a single, consistent convention when naming users to keep things organized.

### Username vs. Local User Account

A username and a local user account are two different concepts that both play an important role in binding a user to a device.

Say you're about to bind a JumpCloud account to a computer that already has an account on it, actively in use (with important documents already on it). Before binding the account, you need to click **+ local account** and enter the local user account name used on that device. That way, when the JumpCloud account gets bound to the device, JumpCloud won't create a brand-new account — the user's documents and everything else are preserved.

This process is called **taking over a local user account**.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/username-vs-local.webp' | relative_url }}" width="900" height="206" alt="Diagram showing how the username (bobfay) and the local user account (bob.fay) both connect to the device">
</div>

A few important points:

- The user's JumpCloud username and their local user account name must be different from each other.
- For the takeover to work, the user must not already be bound to the device.
- If the user is already bound and you want to add the local account name, you need to unbind the user first.
