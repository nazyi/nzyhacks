---
categories: [modul]
layout: post
lang: en
description: "The passive information gathering section of the third module of the Cisco Ethical Hacker course. It covers passive reconnaissance, a method of gathering information without directly interacting with target systems. Techniques such as OSINT tools, DNS queries, and WHOIS are used to gather information about systems without leaving a trace."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 3 - Passive Recon
tags: [Cisco, Passive Recon]
order: 3
permalink: /en/Cisco_Module3_Passive
translation_url: /Cisco_Module3_Passive
---

# Cisco Ethical Hacker

## Module 3: Information Gathering and Vulnerability Scanning

## 3.1 Perform Passive Reconnaissance

### 3.1.1 Reconnaissance  

Gathering information about a target is called reconnaissance. It is the first step of the Cyber Kill Chain. This term, used in its military sense to mean scouting, covers information such as the enemy's location and capabilities.

### 3.1.2 Active Reconnaissance vs Passive Reconnaissance

**Active Reconnaissance** is when the tools used to gather information are more aggressive and noticeable. It performs various scans by sending requests to the target system or network.

**Passive Reconnaissance** is when the tools used do not directly interact with the target system or network. Information is gathered by following a passive path without making the target aware.

Some active information gathering tools:

·        Host Enumeration

·        Network Enumeration

·        User or Group Enumeration

·        Application, Service, Packet Enumeration

Some passive information gathering tools:

·        OSINT

·        Recon-ng

·        Domain Enumeration
### 3.1.3 Lab – Using OSINT Tools

#### Part 1 Examine OSINT Resources

You can search for a nickname using the OSINT Framework at [https://osintframework.com/](https://osintframework.com/). The site [https://whatsmyname.app/](https://whatsmyname.app/) lets you search for any nickname you want. You can find the results along with their URLs.

#### Part 2 Use SpiderFoot

To use the tool after opening SpiderFoot on Kali
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> spiderfoot -l 127.0.0.1:5001
</div>

After entering this command, you can access the SpiderFoot interface through your browser by opening the IP address and port.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/spiderscan.webp' | relative_url }}" width="660" height="230" alt="View of the SpiderFoot web interface opened in the browser">
</div>

**Step 1: Run SpiderFoot scan for a Domain**

Let's run a new scan on the interface by clicking New Scan. We enter our scan name in the Scan Name field and our target domain in the Scan Target field. You can make the necessary settings from the "By Use Case", "By Required Data" and "By Module" sections below. For now, we're testing with the h4cker.org site using the Footprint case.

**Step 2: Investigate Scan Results**

By looking at the Scan tab, we can view previous scans or scans currently in progress. By clicking on our test scan named Cisco1, you can view the information gathered so far by various modules.

**Step 3: Register for API Keys**

Some modules require API keys to use. These API keys can be obtained free of charge for some modules. By going to the page content of the module you want to use and clicking the question mark, you can see step by step how to obtain the API key.

#### Part 3 Investigate Recon-ng

**Step 1: Create a Workspace**

We open our recon-ng tool on Kali. You can find it either through the terminal or by searching the Kali menu.

Each query performed has its own separate workspace. This way, queries don't get mixed up with each other and work becomes easier.

We use the "workspaces create" command to create a workspace.

**Step 2: Investigate Modules**

The recon-ng tool is a modular framework. That is, it consists of many modules. You can download and use these modules from an external marketplace. We can look at the modules using the "modules search" command.
<div class="code-window">
<br>
<span class="highlight">[recon-ng][default]</span> > marketplace search
</div>

**Step 3: Investigate the Module Marketplace**

Modules can be accessed from the Github repository. Detailed information about the modules can be accessed using marketplace info <module\_name>.

**Step 4: Install a new module**

To download a new module, let's first view the modules with modules search.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/search.webp' | relative_url }}" width="700" height="300" alt="Module list output of the 'modules search' command in Recon-ng">
</div>


As an example, let's download the bing\_domain\_web module. To download it;
<div class="code-window">
<br>
<span class="highlight">[recon-ng][default]</span> > marketplace install recon/domain-hosts/bing_domain_web
</div>

Apply the same process for the hackertarget module and download it too.

**Step 5: Run the New Modules**

Let's create a new workspace. Let's use the following command to work with the module.
<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco]</span> > modules load hackertarget 
</div>

If you want more information about the module, you can use the command below.
<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > info 
</div>

As shown in the info output, the only setting we need is to set the source.
<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > options set source hackxor.net<br>SOURCE -> hackxor.net
</div>


Let's set our target with this command. We can check again with info whether it has been set. Let's run our module with the "run" command.
<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > run
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/run.webp' | relative_url }}" width="500" height="420" alt="Output of the hackertarget module's 'run' command in Recon-ng">
</div>


If we want to see a general summary of the collected information in table form, we can use the "dashboard" command.

<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > dashboard
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/dashboard.webp' | relative_url }}" width="400" height="550" alt="Summary table of the information collected by the Recon-ng dashboard command">
</div>


To look at the headings shown in the dashboard view, we can use the "Show" command. Example usage "show hosts".

<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > show hosts
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/showhost.webp' | relative_url }}" width="750" height="180" alt="Host information listed by the 'show hosts' command in Recon-ng">
</div>


**Step 6: Investigate the Web Interface**

Recon-ng has a web interface to better view the results in its database.

Let's open a new terminal and type recon-web. This starts the process of gathering the information in the database. You can access the interface by clicking the URL that appears in the output. The interface initially shows the results of the default workspace; you can select your own workspace by clicking on the orange "default" text above.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/recon.webp' | relative_url }}" width="600" height="400" alt="Workspace results displayed in Recon-ng's recon-web interface">
</div>


#### Part 4 Find Interesting Files with Recon-ng

Let's download a new module to find various files on the site.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/interest.webp' | relative_url }}" width="1100" height="60" alt="Search result listing the interesting_files module in Recon-ng">
</div>

To download and use the module;
<div class="code-window">
<br>
<span class="highlight">[recon-ng][default]</span> > marketplace install discovery/info/disclosure/interesting_files<br><span class="highlight">[recon-ng][default]</span> >	modules load interesting_files<br><span class="highlight">[recon-ng][cisco][interesting_files]</span> > info
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/custom.webp' | relative_url }}" width="760" height="100" alt="Settings shown by the 'info' command for the interesting_files module">
</div>


After checking the required settings, let's set the source to hackxor.net again.
<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][interesting_files]</span> > options set source hackxor.net<br><span class="highlight">[recon-ng][cisco][interesting_files]</span> > run
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/robots.webp' | relative_url }}" width="650" height="310" alt="Output of the files found by the interesting_files module for hackxor.net">
</div>


You can read the saved output from the file /root/.recon-ng/workspaces/cisco/http\_hackxor.net\_robots.txt.

You can also read the results in the csv file inside the recon-ng/data folder.

### 3.1.4 DNS Lookups

DNS queries can be used to try to learn the target system's IP address or any other subdomains it uses.

Tools such as dnsrecon and dig can be used.

### 3.1.5 Identification of Technical and Administrative Contacts

We can use the whois command to look at the technical and administrative contact information for a domain. As an example, let's look at the h4cker.org site.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> whois h4cker.org
</div>

### 3.1.6 Lab – DNS Lookups

#### Part 1 Use nslookup to Obtain Domain and IP Adress Information

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

#### Part 2 Use Whois Function to Obtain Domain Information

Whois is a tool used, instead of DNS server records, to access where and by whom a domain is registered, along with physical address and technical information.

 **Step 1: Use whois to determine IP address registration information**

Using the information we obtained from the nslookup cisco.com output, we found the IP information for ns1.cisco.com, which is cisco.com's name server. The IP address was 72.163.5.201. Let's scan this IP address with whois. This way, let's find the scope range of the IP address.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/whois.webp' | relative_url }}" width="660" height="330" alt="IP address registration and scope information obtained from the whois query">
</div>


#### Part 3 Compare te Output of the Nslookup and Dig Functions

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

#### Part 4 Perform Reverse DNS Lookups

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

### 3.1.7 Cryptographic Flaws

By examining the SSL certificates of sites, various information such as weak certificates or cryptographic weaknesses can be accessed.

Through a site like Crt.sh, you can query the certificate of any organization or page you want. Let's examine the address h4cker.org as an example.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/lets.webp' | relative_url }}" width="630" height="210" alt="Certificate Transparency (CT) query results for h4cker.org on crt.sh">
</div>

We can also see subdomain addresses we didn't know about before, here.

### 3.1.8 Lab – Finding Information from SSL Certificates

Some SSL certificates are stored locally on a host on the network. They ensure secure communication is established between the client and server. For the SSL certificate verification chain, the host holds both intermediate and root SSL certificates.

#### Part 1 Access Detailed Certificate Information Online

Certificate Transparency is an open framework used to monitor and audit the issuance of both SSL and TLS certificates.

Every new certificate or certificate action is logged, giving rise to the term we call CT log. Both attackers and defenders can obtain information suited to their purpose using these CT logs.

#### Part 2 Use SSL Analysis Tools in Kali

Let's go over the names and purposes of some SSL tools on Kali.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/arac.webp' | relative_url }}" width="630" height="340" alt="List of names and descriptions of SSL analysis tools on Kali Linux">
</div>


#### Part 3 Use Kali Tools to Gather Certificate Information

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


### 3.1.9 Company Reputation and Security Posture

If a company has a history of data breaches, attackers can make use of

·        Password dumps

·        File metadata

·        Website archiving

·        Public source code repositories

left over from the previous attack.

#### Password Dumps

Attackers have many tools to access previously stolen password dumps. One of these is the h8mail tool.

To install it with pip on Kali, let's first create our isolated environment.

·        python3 -m venv cisco

·        source cisco/bin/activate

·        pip install h8mail

This way, we can install our h8mail tool. Some other tools similar to this one are given below along with their links.

*   **WhatBreach:** [_https://github.com/Ekultek/WhatBreach_](https://github.com/Ekultek/WhatBreach)
*   **LeakLooker:** [_https://github.com/woj-ciech/LeakLooker_](https://github.com/woj-ciech/LeakLooker)
*   **Buster:** [_https://github.com/sham00n/buster_](https://github.com/sham00n/buster)
*   **Scavenger:** [_https://github.com/rndinfosecguy/Scavenger_](https://github.com/rndinfosecguy/Scavenger)
*   **PwnDB:** [_https://github.com/davidtavarez/pwndb_](https://github.com/davidtavarez/pwndb)

#### File Metadata

We can learn a lot of information from the metadata of photos, Word, Excel, and similar files. There are many tools that let us see this information. One of these is the ExifTool tool.

#### Strategic Search Engine Analysis/Enumeration

Today there are many different search engines on the market. Users can use search engines like Yandex, Bing, or DuckDuckGo depending on their preferences. However, thanks to its advanced search operators, Google allows for much more detailed and targeted searches. This method is known especially in the cybersecurity world as Google Dorking and can also be used by malicious individuals to access sensitive information.

An example of some special search operators is below.

·        **Filetype:** Searches on Google for only a specific file type.

·        **Inurl:** Specifies a word that will be in the URL on Google.

·        **Link**: Searches Google only for links containing a specific term.

·        **Intitle:** Makes Google search for a specific term in a document title.

An example search is below.

"public $user =" | "public $password = " | "public $secret =" | "public $db =" ext:txt | ext:log -git

You can find and examine dork examples on the site [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database).

#### Website Archiving/Caching

Some sites archive and store information about sites on the internet. Through [https://web.archive.org/](https://web.archive.org/) you can go back in time and view the older state of the site you're looking at.

#### Public Source Code Repositories

Attackers can obtain valuable information or find a system's vulnerability by accessing public source code on Github or Gitlab.

### 3.1.10 Lab – Finding Out About the Orginization

#### Part 1 Find Information about Email Breaches.

If an employee's work email has been leaked before, this information can be used. Some online services can be used to find out whether an email has been leaked.

·        haveibeenpwned.com

·        f-secure.com

·        hacknotice.com

·        breachdirectory.com

·        keepersecurity.com

**Step 1: Use a tool to find email adresses for a domain**

As an example, we can use the emailharvester tool that comes pre-installed on Kali.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> emailharvester -d example.com
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/searching.webp' | relative_url }}" width="400" height="380" alt="Email addresses found by the emailharvester tool for example.com">
</div>


**Step 2: Use Spiderfoot to research email adresses**

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> spiderfoot -l 127.0.0.1:5001
</div>


After running our interface with this command, we can access it. Here, we can search with the modules meant for email by clicking new scan. To give a few examples of email modules: Ahmia, AccountFinder, Archive.org, EmailCrawl.

You can also scan by researching other modules.

#### Part 2 View File Metadata

File metadata can contain a lot of valuable information for attackers. For example, it can give information about the device on which a photo was created. The attacker can also learn about this by researching the device's potential vulnerabilities, or, as another example, information such as the file creator's name and when the file was created can be learned.

**Step 1: Use Exiftool**

After completing the installation of Exiftool, you can search for various dorks on [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database), download hidden documents, and then examine the file's metadata with exiftool.

To scan an entire file, the -csv parameter can be used.
