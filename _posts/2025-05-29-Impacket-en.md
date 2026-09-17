---
categories: [blog]
layout: post
lang: en
description: "Installing the Python-based penetration testing tool Impacket on Kali, the services it offers, and examples from tools like wmiexec and secretsdump."
logo: "/assets/images/blog_icon/impacket.png"
author: nazy
title: The Impacket Tool
tags: [Impacket, Tools]
permalink: /en/Impacket
translation_url: /Impacket
---

#### What is Impacket?

Impacket is a toolset written in the Python programming language that works with network protocols. It is widely used by security experts, penetration testers, digital forensics experts, and system administrators.

#### Installing Impacket on Kali Linux

We'll install our Impacket tool from Github. Let's click the [Github link](https://github.com/fortra/impacket) and copy our link. Our commands, in order:

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> git clone https://github.com/CoreSecurity/impacket.git <br>
<span class="highlight">nzy@kali$</span> cd impacket <br>
<span class="highlight">nzy@kali [~/impacket]$</span> ls <br>
ChangeLog Dockerfile examples impacket LICENSE MANIFEST.in README.md requirements.txt setup.py tests tox.ini<br>
<span class="highlight">nzy@kali [~/impacket]$</span> sudo python3 setup.py install <br>
</div>

This way, we've successfully completed the installation of our toolset.

#### What Are the Services Inside Impacket?
The main services inside the Impacket toolset we installed on Kali are as follows:
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/impacket/impacket_servis.webp' | relative_url }}" width="900" height="500" alt="List of the services in the Impacket toolset">
</div>

I'll explain the usage of some of these services below.

_Attacked machine: Windows 10_

_IP address of the attacked machine: 192.168.80.132_

_My Kali machine's IP address: 192.168.80.138_

#### · wmiexec.py
Used to run commands via Windows Management Instrumentation (WMI). It's used as follows:

<div class="code-window">
<br>
<span class="highlight">nzy@kali [~/impacket/examples]$</span> python3 wmiexec.py [domain]/[username]:[password]@[target\_ip] <br>
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/impacket/wmiexec.webp' | relative_url }}" width="700" height="200" alt="Example of running a command over WMI with wmiexec.py">
</div>

#### · ping.py
A Python script that sends an ICMP (Internet Control Message Protocol) ping packet to a target on the network. This tool is used to test network connectivity and determine whether a target is online. It's used as follows:

<div class="code-window">
<br>
<span class="highlight">nzy@kali [~/impacket/examples]$</span> python3 ping.py [src_ip][target\_ip] <br>
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/impacket/ping.webp' | relative_url }}" width="500" height="300" alt="Output of the ICMP ping test run by the ping.py script">
</div>

#### · secretsdump.py
You can access SAM and LSA data, hash dumps from NTDS.dit, and more, by dumping them. It's used as follows:

<div class="code-window">
<br>
<span class="highlight">nzy@kali [~/impacket/examples]$</span> python3 secretsdump.py [domain]/[username]:[password]@[target\_ip] <br>
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/impacket/secrets.webp' | relative_url }}" width="900" height="200" alt="SAM/NTLM hash dump obtained with secretsdump.py">
</div>

#### · samrdump.py
The SAM database is a database on Windows operating systems that stores hashes of user accounts and passwords. This tool is used, particularly in penetration tests and Red Team operations, to gather user information from the target system.

<div class="code-window">
<br>
<span class="highlight">nzy@kali [~/impacket/examples]$</span> python3 samrdump.py [domain]/[username]:[password]@[target\_ip] <br>
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/impacket/samr.webp' | relative_url }}" width="800" height="900" alt="SAM database user information obtained with samrdump.py">
</div>
