---
categories: [modul]
layout: post
lang: en
description: "The first part of the passive information gathering section of the third module of the Cisco Ethical Hacker course. Covers passive vs. active reconnaissance concepts, OSINT tools, and hands-on information gathering labs with Recon-ng."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 3 - Passive Recon (1/2)
tags: [Cisco, Passive Recon]
order: 3
permalink: /en/Cisco_Module3_Passive
translation_url: /Cisco_Module3_Passive
---


## Module 3: Information Gathering and Vulnerability Scanning

### 3.1 Perform Passive Reconnaissance

#### 3.1.1 Reconnaissance  

Gathering information about a target is called reconnaissance. It is the first step of the Cyber Kill Chain. This term, used in its military sense to mean scouting, covers information such as the enemy's location and capabilities.

#### 3.1.2 Active Reconnaissance vs Passive Reconnaissance

**Active Reconnaissance** is when the tools used to gather information are more aggressive and noticeable. It performs various scans by sending requests to the target system or network.

**Passive Reconnaissance** is when the tools used do not directly interact with the target system or network. Information is gathered by following a passive path without making the target aware.

Some active information gathering tools:

- Host Enumeration
- Network Enumeration
- User or Group Enumeration
- Application, Service, Packet Enumeration

Some passive information gathering tools:

- OSINT
- Recon-ng
- Domain Enumeration

#### 3.1.3 Lab – Using OSINT Tools

##### Part 1 Examine OSINT Resources

You can search for a nickname using the OSINT Framework at [https://osintframework.com/](https://osintframework.com/). The site [https://whatsmyname.app/](https://whatsmyname.app/) lets you search for any nickname you want. You can find the results along with their URLs.

##### Part 2 Use SpiderFoot

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

##### Part 3 Investigate Recon-ng

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


##### Part 4 Find Interesting Files with Recon-ng

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

