---
categories: [modul]
layout: post
lang: en
description: "The first part of the active information gathering section of the third module of the Cisco Ethical Hacker course. Nmap scan types and enumeration methods are explained with example tools and commands."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 3 - Active Recon (1/2)
tags: [Cisco, Active Recon]
order: 4
permalink: /en/Cisco_Module3_Active
translation_url: /Cisco_Module3_Active
---

## Module 3: Information Gathering and Vulnerability Scanning

### 3.2 Performing Active Reconnaissance

After passive information gathering, it's time for active information gathering. In the first stage, we obtained passive information about the targets, for example host names, various email or subdomain names, etc. Next comes checking whether these detected systems are publicly accessible on the internet or sit behind a firewall. We try to gather more information about the system by performing a port scan.

I wanted to briefly explain the output of nmap, the most commonly used tool for port scanning.

| State | Nmap Output | Example |
|---|---|---|
| open | `80/tcp open http` | Web server active |
| closed | `22/tcp closed ssh` | SSH service not running |
| filtered | `443/tcp filtered https` | Firewall present, response may be blocked |

#### 3.2.1 Nmap Scan Types

There are many scan types in Nmap depending on the purpose. Some of them are listed below.

**TCP Connect Scan ( -sT)**

By default, unless otherwise specified, Nmap tries to establish a TCP connection with the target system. By sending a TCP packet to each port, the port's state is determined based on the response received. In other words, this scan type genuinely walks through the door or knocks on the door to check whether it's open. Because of this, if logs are kept on the target systems, the attacker's IP information may appear in those logs.

| State | Description |
|---|---|
| Open | The target port is open and an application is listening. The TCP 3-way handshake usually succeeds. |
| Closed | The port is active but no service is listening on it. The target responds with an RST (Reset) packet. |
| Filtered | The packet doesn't reach the target or is being blocked. It may be filtered by a firewall. |

**UDP Scan (-sU)**

TCP ports are generally searched, but since servers such as DNS, SNMP, and DHCP use UDP, you may also need to scan UDP ports depending on the purpose.

| State | Description |
|---|---|
| Open | The port is open and a valid response came back from the application layer (for example, a DNS reply). |
| Closed | The target sent an ICMP "Port Unreachable" message (Type 3, Code 3). |
| Filtered | No response was received at all, either the packet was filtered or the ICMP response was blocked. |

**TCP FIN Scan (-sF)**

Sometimes a SYN scan can be blocked because it's picked up by a network filter or firewall. If that happens, you may need to perform a different type of scan. You can achieve this with a TCP FIN scan. A FIN packet is sent to the target port; if the port is genuinely closed, it sends an RST packet, and if the port sends no packet at all, you can assume the port is open. That's because a port's natural behavior upon seeing a FIN packet would be to ignore it.

\*Scanning Windows machines with this scan may not give correct results, because Windows machines respond to the packet regardless of the port's state.

| State | Description |
|---|---|
| Open | If the port is open, the target sends no response at all (no connection attempt is made, since a port ignores a FIN packet when it's open). |
| Closed | If the port is closed, the target sends an RST (Reset) packet. |
| Filtered | No response is received at all, or the response may have been blocked by a firewall. |

**Host Discovery Scan (-sn)**

Used to discover hosts on a network. It determines which hosts are active by sending various ICMP messages specific to the network.

**Timing Options**

6 types of timing options can be set with the -T parameter. The options are below.

\-T0: Also known as paranoid, sends packets very slowly to avoid detection.

\-T1: Sneaky, sends packets slowly.

\-T2: Polite, slows down to use less bandwidth.

\-T3: Default, sends packets dynamically based on the target's response.

\-T4: Aggressive, sends packets quickly.

\-T5: Insane, sends packets very quickly, may even skip open ports.

#### 3.2.2 Types Of Enumeration

Now it's time for the enumeration techniques that need to be performed during the information gathering stage. The term enumeration refers to discovering the active resources and services on the target system in more detail.

In other words, it's not just checking whether the door is open, but checking what's behind the door, who's there.

Let's look at a few enumeration topics.

##### Host Enumeration

Host enumeration is one of the first tasks that needs to be done during the information gathering stage. It can happen in two ways:

- **External network**: Take care to scan only the IP addresses within the scope of the test.
- **Internal network:** All IP subnets used by the target are scanned.

##### User Enumeration

There are multiple tools and methods for gathering user information. The simplest example of these is the SMB (Server Message Block) protocol, which uses port 445.

Let's look at the SMB message illustration below.

<pre class="ascii-diagram">
[Attacker]                              [Target SMB Server]
    |                                            |
    | -----> TCP connection (port 445) -------->|
    |                                            |
    | -----> Negotiate Protocol Request ------->|
    | <----- Negotiate Protocol Response -------|
    |                                            |
    | -----> Session Setup Request ------------>|
    |        (with anonymous or blank user)      |
    | <----- Session Setup Response ------------|
    |                                            |
    | -----> Tree Connect Request (IPC$) ------>|
    | <----- Tree Connect Response --------------|
    |                                            |
    | -----> NetShareEnum / NetUserEnum -------- |
    |        (user, share, or group query)       |
    | <----- Enumeration Response (if any) ------|
    |                                            |
    | -----> Close TCP connection --------------|
    |                                            |
</pre>

SMB\_COM\_NEGOTIATE: This is the message asking the server which protocols or flags it supports. The server replies with a message stating the protocols and flags it supports.

SMB\_COM\_SESSION\_SETUP\_ANDX: In this message, the attacker requests permission to open a session. I am the guest user. This is my password, can I connect?

##### Group Enumeration

This process is done to understand which authority roles are used by the users in the target environment. This makes the roadmap a bit clearer. It acts as a guide for privilege escalation attempts.

Example nmap syntax;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap --script smb-enum-groups.nse -p 445 host
</div>

Let's examine the RID and SID terms that appear in the output resulting from the nmap scan.

- **SID:** A unique identification number belonging to a group or user.
- **RID:** The part at the end of the SID, and it identifies the user or group on a Windows basis.

| RID | Description |
|---|---|
| 500 | Administrator |
| 501 | Guest |
| 512 | Domain Admins (Group) |
| 513 | Domain Users (Group) |
| 1000+ | Usually a regular user |

##### Network Share Enumeration

Detecting systems that share files, folders, and printers on a network is called Network Share Enumeration. An example nmap command for finding these is below.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap --script smb-enum-shares.nse -p 445 host
</div>

##### Additional SMB Enumeration Examples

To more thoroughly identify the applications and operating systems running on a system and to learn additional information;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sC  target\_ip
</div> 
  
If you want both more detailed information and operating system detection;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sC -sV -0  target\_ip
</div> 

And I wanted to give some information about nmap smb enum scripts with a table.

| Script Name | Description |
|---|---|
| `smb-enum-shares.nse` | Lists the files and folders shared on the target system. |
| `smb-enum-users.nse` | Lists user accounts on the system (if any). |
| `smb-enum-groups.nse` | Lists user groups on the target system. |
| `smb-enum-processes.nse` | Lists processes running via SMB (requires privileges). |
| `smb-enum-sessions.nse` | Lists active SMB sessions (connected users, etc.). |
| `smb-enum-domains.nse` | Lists domain names. |
| `smb-enum-services.nse` | Gathers service information (such as started services). |
| `smb-enum-lsa.nse` | Lists Local Security Authority (LSA) information (detailed security info). |
| `smb-enum-servers.nse` | Identifies SMB server information and features. |

There's also a different tool for extracting information via SMB, called enum4linux.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> enum4linux target\_ip
</div> 
 
Another example is the smbclient tool.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> smbclient -L target\_ip<br><span class="highlight">kali@kali</span> smbclient  //target\_ip/user
</div> 

##### Web Page Enumeration/Web Application Enumeration

If we determine that a web server is running on the target host, we can use the nmap script http-enum to identify the attack surface. Thanks to this script, we can find folder or file paths using brute force.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sV –script=http-enum -p 80 target\_ip
</div>  

Another tool worth mentioning is Nikto. Nikto is a tool that scans for open-source web vulnerabilities. A simple usage command for nikto is below.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nikto -h target_ip
</div>

##### Service Enumeration

This is the process of identifying the services running on a remote system. With the command below, it's possible to identify in detail which services are running on a remote Windows system.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap –script smb-enum-process.nse -p 445 –script-args smbuser=user , smbpass=pass
</div> 

##### Exploring Enumeration via Packet Crafting

When gathering information by crafting packets, Scapy is among the most preferred tools. Scapy is a Python-based system used for packet crafting. Root permission is required to use Scapy, and it can be used by typing sudo scapy directly into the terminal.

For example, we can use the command below to craft an ICMP packet with malicious\_payload.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> send(IP(dst=”192.168.88.251”)/ICMP()/”malicious\_payload”)
</div>

If we listen to our own network with tshark while sending this packet at the same time, we can view the ICMP packet request.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/tshark.webp' | relative_url }}" width="700" height="200" alt="Scapy ICMP packet request captured while listening with tshark">
</div>

\*tshark is the terminal version of Wireshark.

There are many protocols that can be used in Scapy. You can use the **ls()** function to list these protocols. For example, you can use the **ls(TCP)** command to see the formats supporting the TCP protocol.

You can access the Scapy interface and examine formats and protocols with the explore() command.

#### 3.2.3 Lab – Enumeration with Nmap

##### Part 1 Investigate Nmap

**Step 1: Investigate Nmap Options and Features**

Let's look at the common NMAP settings. You can find the parameters below by typing man nmap.

- **-A:** Aggressive scan (covers OS detection, version detection, script scanning, and traceroute)
- **-O:** OS detection
- **-p:** Port scope
- **-sF:** TCP FIN scan
- **-sS:** TCP SYN scan
- **-sT:** TCP scan
- **-sV:** Finding the service and version information of open ports
- **-T<0-5>:** Setting the scan speed
- **-v:** Increases the verbosity of the output
- **--open:** Shows only open ports

##### Part 2 Perform Basic Nmap Scans

According to our scenario, there's suspicious behavior on a host in the DMZ area. First, let's look at how many active hosts there are in the DMZ scope range.

**Step 1: Initiate a basic Nmap scan of the target computer**
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sn 10.6.6.0/24
</div> 

The output shows that a total of 7 hosts are active.

Wireshark indicates that the 10.6.6.23 host is suspicious, so let's examine it specifically.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sudonmap.webp' | relative_url }}" width="500" height="360" alt="List of 7 active hosts detected by the nmap -sn scan">
</div>

**Step 2: Obtain additional information about the host and services**

Let's get more information about the host's FTP service on port 21.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/21ftp.webp' | relative_url }}" width="400" height="100" alt="Additional information obtained about FTP port 21">
</div>

The -A parameter covers most items such as OS discovery, version discovery, and script scanning. However, using it may get you detected by an IDS. Let's enter the command below to get more information.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -p21 -sV -A 10.6.6.23
</div> 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/ftpvstpf.webp' | relative_url }}" width="650" height="360" alt="Anonymous FTP login and txt files seen in the nmap -A scan">
</div>

As shown in the output, anonymous login is accepted and there are a few txt files.

**Step 3: Investigate SMB services with scripts**

Server Message Block, or SMB, supports file sharing on both Windows and Linux machines. It runs on ports 139 and 445. Let's learn more about these ports with nmap.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/worksgruup.webp' | relative_url }}" width="600" height="400" alt="SMB workgroup information obtained with nmap on ports 139 and 445">
</div>

As mentioned before, some scripts within nmap allow you to get more detailed information about the desired system. Now that we've seen the SMB ports are open, we can run the SMB scripts in nmap to get more information.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap –script smb-enum-users.nse -p139,445 10.6.6.23
</div> 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/netbios.webp' | relative_url }}" width="600" height="230" alt="Arbiter and Masterchief users found in the smb-enum-users.nse output">
</div>

As shown in the output, we were able to find two usernames: Arbiter and Masterchief.

Now let's again use a script to see the files shared over SMB.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/hostscripy.webp' | relative_url }}" width="400" height="440" alt="Hidden shares found by the SMB share scan and anonymous access permission">
</div>

Here we found 2 hidden shares starting with a $ sign, and the fact that Anonymous Access: read/write is shown below is a very critical risk.
