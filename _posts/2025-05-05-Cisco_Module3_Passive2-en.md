---
categories: [modul]
layout: post
lang: en
description: "The second part of the passive information gathering section of the third module of the Cisco Ethical Hacker course. Covers DNS queries, WHOIS, SSL certificate analysis, and researching a company's reputation and security posture."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 3 - Passive Recon (2/2)
tags: [Cisco, Passive Recon]
order: 3.5
permalink: /en/Cisco_Module3_Passive2
translation_url: /Cisco_Module3_Passive2
---

#### 3.1.4 DNS Lookups

DNS queries can be used to try to learn the target system's IP address or any other subdomains it uses.

Tools such as dnsrecon and dig can be used.

#### 3.1.5 Identification of Technical and Administrative Contacts

We can use the whois command to look at the technical and administrative contact information for a domain. As an example, let's look at the h4cker.org site.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> whois h4cker.org
</div>

#### 3.1.6 Lab – DNS Lookups

##### Part 1 Use nslookup to Obtain Domain and IP Address Information

Nslookup, available on both Linux and Windows machines, essentially retrieves domain name and IP address information.

**Step 1: Using the nslookup command**

If we just type nslookup, we can enter interactive mode. After entering this mode, let's look at the domain cisco.com as an example.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup<br>>cisco.com
</div>

In this output, you can see both IPv4 and IPv6 addresses. 
To see the name server information for the domain address;
<div class="code-window">
<br>
> set type=ns<br>> cisco.com
</div>

**Step 2: Change the server used to perform lookups**

Sometimes, as a solution to a DNS server failing to resolve an address or finding no answer, we can use a different DNS server.

In the given output, we're trying to resolve skillsforall.com using Google's DNS server. Google's DNS server IP address is 8.8.8.8.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup skillsforall.com 8.8.8.8
</div>

To change the server in interactive mode;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup<br>> server 8.8.8.8<br>> set type=any<br>> skillsforall.com
</div>

When we select "any" as the type, it shows all the information it can find about the domain.

##### Part 2 Use Whois Function to Obtain Domain Information

Whois is a tool used, instead of DNS server records, to access where and by whom a domain is registered, along with physical address and technical information.

 **Step 1: Use whois to determine IP address registration information**

Using the information we obtained from the nslookup cisco.com output, we found the IP information for ns1.cisco.com, which is cisco.com's name server. The IP address was 72.163.5.201. Let's scan this IP address with whois. This way, let's find the scope range of the IP address.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/whois.webp' | relative_url }}" width="660" height="330" alt="IP address registration and scope information obtained from the whois query">
</div>


##### Part 3 Compare the Output of the Nslookup and Dig Functions

Dig is a tool similar to Nslookup. It resolves the target's hostname and IP address.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig cisco.com
</div>

To see the IPv6 IP address;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig cisco.com AAAA
</div>

To get extra information using dig;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig cisco.com 8.8.8.8 ns
</div>

Or, using the equivalent of the set type=any command we used in nslookup, with dig;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig cisco.com any
</div>

##### Part 4 Perform Reverse DNS Lookups

Reverse DNS, or rDNS, tries to find the server names corresponding to an IP address by using that address.

**Step 1: Use Dig to perform rDNS lookups**

Let's try the IP address of ns1.cisco.com that we found earlier.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig -x 72.163.5.201
</div>

As seen in the output below, we found the hostname.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/dig.webp' | relative_url }}" width="660" height="370" alt="Hostname result of the reverse DNS lookup performed with the dig -x command">
</div>


**Step 2: Use the host utility to perform rDNS lookups**

Let's try the "host" command on a different IP address.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> host 72.163.10.1
</div>

**Step 3: Use nslookup to perform rDNS lookups**

We can use nslookup as we did before.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup 72.163.10.1
</div>

#### 3.1.7 Cryptographic Flaws

By examining the SSL certificates of sites, various information such as weak certificates or cryptographic weaknesses can be accessed.

Through a site like Crt.sh, you can query the certificate of any organization or page you want. Let's examine the address h4cker.org as an example.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/lets.webp' | relative_url }}" width="630" height="210" alt="Certificate Transparency (CT) query results for h4cker.org on crt.sh">
</div>

We can also see subdomain addresses we didn't know about before, here.

#### 3.1.8 Lab – Finding Information from SSL Certificates

Some SSL certificates are stored locally on a host on the network. They ensure secure communication is established between the client and server. For the SSL certificate verification chain, the host holds both intermediate and root SSL certificates.

##### Part 1 Access Detailed Certificate Information Online

Certificate Transparency is an open framework used to monitor and audit the issuance of both SSL and TLS certificates.

Every new certificate or certificate action is logged, giving rise to the term we call CT log. Both attackers and defenders can obtain information suited to their purpose using these CT logs.

##### Part 2 Use SSL Analysis Tools in Kali

Let's go over the names and purposes of some SSL tools on Kali.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/arac.webp' | relative_url }}" width="630" height="340" alt="List of names and descriptions of SSL analysis tools on Kali Linux">
</div>


##### Part 3 Use Kali Tools to Gather Certificate Information

Sslscan, as the name suggests, provides information about SSL certificates. Another tool we'll use is "aha". It's used to convert the output into an HTML file.

**Step 1: Run sslscan and save the output to a HTML file**

On Kali, we run an sslscan scan for our target.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sslscan skillsforall.com | aha > sfa_cert.html
</div>

After finding the file's location, you can open the html file in Mozilla.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/html.webp' | relative_url }}" width="500" height="410" alt="Browser view of the HTML report generated by aha from the sslscan output">
</div>


#### 3.1.9 Company Reputation and Security Posture

If a company has a history of data breaches, attackers can make use of

- Password dumps
- File metadata
- Website archiving
- Public source code repositories

left over from the previous attack.

##### Password Dumps

Attackers have many tools to access previously stolen password dumps. One of these is the h8mail tool.

To install it with pip on Kali, let's first create our isolated environment.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> python3 -m venv cisco<br>source cisco/bin/activate<br>pip install h8mail
</div>

This way, we can install our h8mail tool. Some other tools similar to this one are given below along with their links.

*   **WhatBreach:** [_https://github.com/Ekultek/WhatBreach_](https://github.com/Ekultek/WhatBreach)
*   **LeakLooker:** [_https://github.com/woj-ciech/LeakLooker_](https://github.com/woj-ciech/LeakLooker)
*   **Buster:** [_https://github.com/sham00n/buster_](https://github.com/sham00n/buster)
*   **Scavenger:** [_https://github.com/rndinfosecguy/Scavenger_](https://github.com/rndinfosecguy/Scavenger)
*   **PwnDB:** [_https://github.com/davidtavarez/pwndb_](https://github.com/davidtavarez/pwndb)

##### File Metadata

We can learn a lot of information from the metadata of photos, Word, Excel, and similar files. There are many tools that let us see this information. One of these is the ExifTool tool.

##### Strategic Search Engine Analysis/Enumeration

Today there are many different search engines on the market. Users can use search engines like Yandex, Bing, or DuckDuckGo depending on their preferences. However, thanks to its advanced search operators, Google allows for much more detailed and targeted searches. This method is known especially in the cybersecurity world as Google Dorking and can also be used by malicious individuals to access sensitive information.

An example of some special search operators is below.

- **Filetype:** Searches on Google for only a specific file type.
- **Inurl:** Specifies a word that will be in the URL on Google.
- **Link**: Searches Google only for links containing a specific term.
- **Intitle:** Makes Google search for a specific term in a document title.

An example search is below.

"public $user =" | "public $password = " | "public $secret =" | "public $db =" ext:txt | ext:log -git

You can find and examine dork examples on the site [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database).

##### Website Archiving/Caching

Some sites archive and store information about sites on the internet. Through [https://web.archive.org/](https://web.archive.org/) you can go back in time and view the older state of the site you're looking at.

##### Public Source Code Repositories

Attackers can obtain valuable information or find a system's vulnerability by accessing public source code on Github or Gitlab.

#### 3.1.10 Lab – Finding Out About the Organization

##### Part 1 Find Information about Email Breaches.

If an employee's work email has been leaked before, this information can be used. Some online services can be used to find out whether an email has been leaked.

- haveibeenpwned.com
- f-secure.com
- hacknotice.com
- breachdirectory.com
- keepersecurity.com

**Step 1: Use a tool to find email addresses for a domain**

As an example, we can use the emailharvester tool that comes pre-installed on Kali.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> emailharvester -d example.com
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/searching.webp' | relative_url }}" width="400" height="380" alt="Email addresses found by the emailharvester tool for example.com">
</div>


**Step 2: Use Spiderfoot to research email addresses**

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> spiderfoot -l 127.0.0.1:5001
</div>


After running our interface with this command, we can access it. Here, we can search with the modules meant for email by clicking new scan. To give a few examples of email modules: Ahmia, AccountFinder, Archive.org, EmailCrawl.

You can also scan by researching other modules.

##### Part 2 View File Metadata

File metadata can contain a lot of valuable information for attackers. For example, it can give information about the device on which a photo was created. The attacker can also learn about this by researching the device's potential vulnerabilities, or, as another example, information such as the file creator's name and when the file was created can be learned.

**Step 1: Use Exiftool**

After completing the installation of Exiftool, you can search for various dorks on [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database), download hidden documents, and then examine the file's metadata with exiftool.

To scan an entire file, the -csv parameter can be used.
