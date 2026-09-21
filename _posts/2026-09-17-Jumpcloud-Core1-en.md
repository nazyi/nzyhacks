---
categories: [dokumantasyon]
layout: post
lang: en
description: "The first lesson of the JumpCloud University Core course: the Admin Console and User Portal interfaces, organization settings, admin roles/permissions, and recommended security/password policies."
logo: "/assets/images/blog_icon/jumpcloud.png"
author: nazy
title: JumpCloud Core 1 - Admin Settings
tags: [JumpCloud, Admin Console]
order: 1
permalink: /en/Jumpcloud-Core1
translation_url: /Jumpcloud-Core1
---

Hi, in this series I'll be working through the lessons of JumpCloud University's Core course one by one.

Our first lesson covers admin settings.

JumpCloud has two main UI pages. The first is the Admin Console, used by IT admins, and the other is the User Portal, the general interface for end users.

In the Admin Console you can make various configurations — for example, user and device management, security management, organization settings, and account information.

## Organization Settings

- **Settings > Organization Profile**: From here you can manage and change things like your company name, a contact email address for emergencies, and the company's logo. You can also manage users' permissions within the User Portal and how long the portal stays open (session timeout).

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core1/org-profile.webp' | relative_url }}" width="1000" height="538" alt="Settings > Organization Profile page showing organization name, contact info, organization ID, and logo customization">
</div>

- **Settings > Customize Email**: From here you can create and edit your ready-made email templates. For example, you can customize the email JumpCloud sends when a user's account gets locked.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core1/customize-email.webp' | relative_url }}" width="1000" height="538" alt="Settings > Customize Email page showing the template preview for the password expiration warning email">
</div>

You can configure your company's password settings using two options:

1. **Settings > Security**: From the security settings, you can configure password strength, complexity, or account lockout.
2. **Security > Password Policies**: You can create a new policy and attach it to the user group you want it to affect. If a user belongs to multiple user groups, you can manage which group's password policy should apply from here.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core1/password-policies.webp' | relative_url }}" width="1000" height="319" alt="Security > Password Policies page showing the prioritized list of password policies">
</div>

## Admin Management

**Settings > Administrators**

You can choose one of two ways to add an admin to the console:

1. Click the "+ Admin" button and grant admin privileges to an existing user.
2. Click the "+ Admin" button and choose "new" to create a brand-new admin account.

## Role Permissions

- **Administrator with Billing**: Also called a super admin. Has every permission; can access the MTP (Multi-Tenant Portal), manage billing, and activate API keys.
- **Administrator**: Can do everything except API keys, MTP, and billing.
- **Manager**: Can manage users, devices, and groups.
- **Command Runner**: Can only run commands.
- **Command Runner with Billing**: Can run commands and also update billing.
- **Help Desk**: Can create, delete, or reset users.
- **Billing Only**: Permissions are limited to read-only. Can view payment-related information.
- **Read Only**: These admins can only view/read.

{% include match-quiz.html id="jc-roles-en" items=site.data.jc_roles_en hint="Drag each role onto its correct permission description." left_label="Role" right_label="Permission Description" success_text="🎉 You matched them all!" reset_text="Reset" %}

## Notes

- Require the new password to differ from the last 4 passwords.
- Limit failed login attempts to 6.
- Set password length to 8–12 characters.
- Lock the session after 8 hours of inactivity.
- Set password expiration to 90 days.
- Turn on MFA verification.
- Restrict admin privileges and assign roles correctly.
