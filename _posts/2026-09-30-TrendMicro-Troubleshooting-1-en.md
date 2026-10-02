---
categories: [dokumantasyon]
layout: post
lang: en
description: "The System Extension (20117) error caused by an old Bitdefender network extension conflicting with Trend Micro's network extension, and why SIP blocks systemextensionsctl uninstall."
tool: Trend Micro
doc_type: troubleshooting
logo: "/assets/images/blog_icon/trendmicro.png"
author: nazy
title: Trend Micro Troubleshooting Part 1 - System Extension (20117) Error
tags: [Trend Micro, Troubleshooting]
order: 40
wide_content: true
permalink: /en/TrendMicro-Troubleshooting-1
translation_url: /TrendMicro-Troubleshooting-1
---

## Overview

An old Bitdefender network extension can conflict with Trend Micro's network extension and cause a System Extension (20117) error. Deactivating the old Bitdefender and restarting the device resolves the issue.

## Checking on the Device

There are two places on the device where you should check whether Bitdefender components are active:

- **System Settings > Network > Filters** — the Bitdefender DCI filters should not be active.
- **System Settings > General > Login Items & Extensions > Network Extensions** — `dci-net-ext` should not be active.

## Checking Remotely

You can check whether Bitdefender is active:

<div class="code-window">
<br>
<span class="highlight">%</span> systemextensionsctl list
</div>

If the command's output contains a line like this, it means Bitdefender is still active and running:

<div class="code-window">
<br>
com.bitdefender.cst.net.dci.dci-network-extension (7.21.53.200097/7.21.53.200097) dci-net-ext [activated enabled]
</div>

## Why Can't We Run systemextensionsctl uninstall?

On a normal Mac, the `systemextensionsctl uninstall <teamID> <bundleID>` command is blocked by SIP (System Integrity Protection):

<div class="code-window">
<br>
At this time, this tool cannot be used if System Integrity Protection is enabled.
</div>

SIP is a security mechanism built into macOS that prevents even the root user from modifying protected system files.

You can check whether SIP is enabled on the target device:

<div class="code-window">
<br>
<span class="highlight">%</span> csrutil status
</div>
