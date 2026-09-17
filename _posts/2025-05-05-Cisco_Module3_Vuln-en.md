---
categories: [modul]
layout: post
lang: en
desc: "This is the vulnerability scanning section of the third module of the Cisco Ethical Hacker course. It covers, in a hands-on way, how vulnerability scanners work, scan types (authenticated, unauthenticated, stealth, compliance, etc.), and vulnerability analyses performed with Nmap and GVM tools on Kali Linux. It also introduces points to consider when analyzing scan results, along with security resources such as CVE, CWE, and CVSS."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 3 - Vulnerability Scans
tags: [Cisco, Vulnerability Scanning]
order: 5
permalink: /en/Cisco_Module3_Vuln
translation_url: /Cisco_Module3_Vuln
---
# Cisco Ethical Hacker

# Module 3: Information Gathering and Vulnerability Scanning

## 3.3 Understanding the Art of Performing Vulnerabilitiy Scans

### 3.3.1 How a Typical Automated Vulnerability Scanner Works

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_vuln/scanner.webp' | relative_url }}" width="600" height="430" alt="Step-by-step diagram showing how an automated vulnerability scanner works">
</div>

Although they differ from one another, most vulnerability scanners follow a similar process. A visualized version is given above.

**Step 1: Discovery Phase**

The scanner performs host and port discovery on the network using a tool like nmap.

**Step 2: Service Identification and Recording**

When the scanner sees that a port is open, it tries to gather more information about it. It tries to determine which software and version is being used, for example via banner grabbing.

**Step 3: Vulnerability Comparison**

The scanner compares the information it has found against its own vulnerability database to check whether the system is vulnerable to known vulnerabilities.

**Step 4: Report Generation**

The scanner produces a report containing the potential vulnerabilities.

### 3.3.2 Types of Vulnerability Scans

Scanning methods and types can vary depending on the environment being tested.

#### Unauthenticated Scans

Scanners generally scan without any user credentials. They scan for services exposed on the network or open ports. If the connection is blocked by a firewall, the ports appear as closed.

#### Authenticated Scans

Scanning using credentials is a scan type where the scanner gains root-level access. The scanner actually logs into the target system via SSH or another service, and while inside the system it tries to gather information by running commands such as netstat.

#### Discovery Scans

Discovery scanning is used to determine the attack surface. The scanner tries to gather information by searching in more detail for both the ports and the services running on top of them. For example, if ports 80, 22, and 443 are found open as a result of a port scan, it can determine which web server and which version is running on 80 and 443 and set the attack surface accordingly.

#### Full Scans

This occurs by enabling the scan types described so far. It can vary depending on the operating system or machine being used.

For example, on Nessus, a popular scanning tool, there are various plugins depending on the operating system or machine type.

#### Stealth Scans

This is a stealthy scan type performed without the target noticing. For instance, we had previously learned which of the nmap scan types is the quietest. The same applies to other vulnerability scanning tools as well — they also have options for performing quiet scans.

#### Compliance Scans

As we've seen earlier in this course, companies must comply with certain governance rules. A vulnerability scanner can be used to test whether companies and their products comply with these rules.

Most vulnerability scanners have the ability to create custom compliance policies.

### 3.3.3 Lab – Vulnerability Scanning with Kali Tools

As in our previous scenario, the device with IP address 10.6.6.23 is displaying suspicious behavior, so we're investigating it.

#### Part 1 Run a Nmap Scan on a Target Computer

**Step 1: Identify open ports and services**

I run an nmap scan to find out the ports and the service versions.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sV 10.6.6.23
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_vuln/nmapsv.webp' | relative_url }}" width="660" height="230" alt="Open ports and service versions seen in the output of the nmap -sV command">
</div>

And the following command is used to find the operating system;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo nmap -O 10.6.6.23
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_vuln/running.webp' | relative_url }}" width="760" height="90" alt="Target operating system information detected with the nmap -O command">
</div>

**Step 2: Use the nmap Vulners script tos can for vulnerabilities**

The Vulners script keeps the open port and software version information and compares it against the CPE database. This way, it checks whether the system is exposed to known vulnerabilities.

Let's enter the following command to scan for vulnerabilities on the system with a CVE score of 4 or higher.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sV –script vulners –script-args mincvss=4 10.6.6.23
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_vuln/21.webp' | relative_url }}" width="800" height="400" alt="High CVSS-score vulnerabilities listed in the output of the Nmap Vulners script">
</div>

As can be seen, the system has many high-potential vulnerabilities.

#### Part 2 Use GVM to Scan for Vulnerabilities

GVM is one of the most widely used open-source security scanners. Even though GVM is installed on the Cisco Kali machine, we can use the following command to verify it.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo gvm-check-setup
</div>

To access the interface;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo gvm-start
</div>

After accessing the interface, go to the Scans > Tasks page to start a scan. From the three icons in the upper left, select the one that looks like a wand.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_vuln/asa.webp' | relative_url }}" width="700" height="350" alt="The icon for starting a new scan on the Scans-Tasks page in the GVM interface">
</div>

**Step 3: Scan the target host for vulnerabilities**

As seen in the output above, instead of the IP address you can enter our target, 10.6.6.23, or the address gravemind.vm. After entering it, click the Start Scan button. It may take a while for the scan to finish.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_vuln/reports.webp' | relative_url }}" width="700" height="350" alt="The Start Scan screen in GVM where the target IP address is entered and the scan is started">
</div>

We're greeted by a page like this. On this page, if we click the Date information, we can access more information about the CVEs found or the host.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_vuln/tue.webp' | relative_url }}" width="700" height="250" alt="The page listing the CVE and host details found in the GVM scan report">
</div>

### 3.3.4 Challanges to Consider When Running a Vulnerability Scan

·        **Considering the best time to run a scan**: Running tests on live applications instead of lab environments brings various risks along with it.

·        **Determing what protocols are in use:** Among the first things to do before starting a scan is to determine which protocols the target system uses.

·        **Network Topology:** Network topology is very important for planning an attack. It is not recommended to test over networks like a WAN. It is recommended to perform the scan while positioned as close to the target as possible.

·        **Bandwith Limitations:** The bandwidth of the network being scanned must be taken into account. For example, if you're scanning over low-bandwidth networks such as a VPN or a WAN, you should adjust your scan options accordingly.

·        **Query Throttling:** This refers to slowing down the scanner's traffic on a network with limited bandwidth. For example, there's no need to scan for Windows machine vulnerabilities on a Linux machine.

·        **Fragile Systems:** There are devices that can't withstand the traffic generated during scanning. When scanning such systems, you should either send less traffic or exclude them from the scan scope.

## 3.4 Understanding How to Analyze Vulnerability Scan Results

### 3.4.1 Sources for Further Investigation of Vulnerabilities

·        **US-CERT**: Aims to increase vulnerability information-sharing activity together with public and private organizations.

·        **The CERT Division of Carneige Mellon University**: Conducts research on security vulnerabilities and contributes to work in the field of cybersecurity.

·        **NIST**: Summarizes standards and industry best practices that organizations can use to improve their cybersecurity posture.

·        **JPCERT**: Like US-CERT, but it is Japan's cybersecurity union.

·        **CAPEC**: A dictionary of known attacks.

·        **CVE**: A CVE Identifier (ID) begins with the letters "CVE" and contains the publication year followed by a sequence number of four or more digits (for example, CVE-YYYY-NNNN with a four-digit sequence number; CVE-YYYY-NNNNN with a five-digit sequence number; CVE-YYYY-NNNNNNN with a seven-digit sequence number, etc.).

·        **CWE**: Creating a common language for describing the software security weaknesses that are the root causes of vulnerabilities

**CVSS**: One of the most widely used standards for calculating the severity of a vulnerability is the Common Vulnerability Scoring System (CVSS).

