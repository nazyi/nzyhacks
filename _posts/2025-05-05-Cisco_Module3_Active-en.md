---
categories: [modul]
layout: post
lang: en
description: "This is the active information gathering section of the third module of the Cisco Ethical Hacker course. Within the scope of active information gathering techniques, Nmap scan types and enumeration methods are covered in detail. To gain deeper insight into target systems, the detection of components such as services, users, groups, and shared resources is explained with example tools and commands."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 3 - Active Recon
tags: [Cisco, Active Recon]
order: 4
permalink: /en/Cisco_Module3_Active
translation_url: /Cisco_Module3_Active
---

## Cisco Ethical Hacker

### Module 3: Information Gathering and Vulnerability Scanning

### 3.2 Performing Active Reconnaissance

After passive information gathering, it's time for active information gathering. In the first stage, we obtained passive information about the targets, for example host names, various email or subdomain names, etc. Next comes checking whether these detected systems are publicly accessible on the internet or sit behind a firewall. We try to gather more information about the system by performing a port scan.

I wanted to briefly explain the output of nmap, the most commonly used tool for port scanning.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/1.webp' | relative_url }}" width="600" height="160" alt="Example output of a basic nmap scan">
</div>

#### 3.2.1 Nmap Scan Types

There are many scan types in Nmap depending on the purpose. Some of them are listed below.

**TCP Connect Scan ( -sT)**

By default, unless otherwise specified, Nmap tries to establish a TCP connection with the target system. By sending a TCP packet to each port, the port's state is determined based on the response received. In other words, this scan type genuinely walks through the door or knocks on the door to check whether it's open. Because of this, if logs are kept on the target systems, the attacker's IP information may appear in those logs.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/stopen.webp' | relative_url }}" width="680" height="160" alt="Example output of a scan performed with TCP Connect Scan (-sT)">
</div>

**UDP Scan (-sU)**

TCP ports are generally searched, but since servers such as DNS, SNMP, and DHCP use UDP, you may also need to scan UDP ports depending on the purpose.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/suopen.webp' | relative_url }}" width="680" height="160" alt="Example output of a scan performed with UDP Scan (-sU)">
</div>

**TCP FIN Scan (-sF)**

Sometimes a SYN scan can be blocked because it's picked up by a network filter or firewall. If that happens, you may need to perform a different type of scan. You can achieve this with a TCP FIN scan. A FIN packet is sent to the target port; if the port is genuinely closed, it sends an RST packet, and if the port sends no packet at all, you can assume the port is open. That's because a port's natural behavior upon seeing a FIN packet would be to ignore it.

\*Scanning Windows machines with this scan may not give correct results, because Windows machines respond to the packet regardless of the port's state.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sfopen.webp' | relative_url }}" width="680" height="160" alt="Example output of a scan performed with TCP FIN Scan (-sF)">
</div>

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

·        **External network**: Take care to scan only the IP addresses within the scope of the test.

·        **Internal network:** All IP subnets used by the target are scanned.

##### User Enumeration

There are multiple tools and methods for gathering user information. The simplest example of these is the SMB (Server Message Block) protocol, which uses port 445.

Let's look at the SMB message illustration below.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/smbenum.webp' | relative_url }}" width="460" height="460" alt="Illustration showing the messaging process in the SMB protocol">
</div>

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

·        **SID:** A unique identification number belonging to a group or user.

·        **RID:** The part at the end of the SID, and it identifies the user or group on a Windows basis.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/rid.webp' | relative_url }}" width="460" height="300" alt="RID and SID values seen in the nmap smb-enum-groups.nse output">
</div>

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
<span class="highlight">kali@kali</span> nmap -sC  target\_ip
</div> 
  
If you want both more detailed information and operating system detection;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sC -sV -0  target\_ip
</div> 

And I wanted to give some information about nmap smb enum scripts with a table.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/smbnmap.webp' | relative_url }}" width="650" height="400" alt="Table summarizing Nmap SMB enumeration scripts">
</div>

There's also a different tool for extracting information via SMB, called enum4linux.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> enum4linux target\_ip
</div> 
 
Another example is the smbclient tool.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> smbclient -L target\_ip<br><span class="highlight">kali@kali</span> smbclient  //target\_ip/user
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

·        \-A: OS detection

·        \-O: OS detection

·        \-p: Port scope

·        \-sF: TCP FIN scan

·        \-ss: TCP SYN scan

·        \-sT: TCP scan

·        \-sV: Finding the service and version information of open ports

·        \-T<0-5>: Setting the scan speed

·        \-v: Increases the verbosity of the output

·        \--open: Shows only open ports

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

**Step3: Investigate SMB services with scripts**

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

#### 3.2.4 Packet Inspection and Eavesdropping

Packet captures can be performed, packets can be inspected and listened to, with tools such as Wireshark, tshark, and tcpdump. For penetration testers, such tools can be useful for performing passive reconnaissance. Of course, this kind of reconnaissance requires a physical or wireless connection to the target.

#### 3.2.5 Lab – Packet Crafting with Scapy

##### Part 1 Investigate the Scapy Tool

Before sending an IP packet, it's important to understand the contents of the IP packet. Every IP packet is accompanied by a header that provides information about the packet structure. Each binary value has a different meaning within the IP packet.

You can examine the details about the fields with the ls() function. The general logic of using a function within Scapy is function\_name (arguments). To get more information about the fields, you can run the ls(IP) command.

The table below gives the field names and their descriptions.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/version.webp' | relative_url }}" width="600" height="600" alt="Table of IP packet field names listed with the ls(IP) command in Scapy">
</div>

##### Part 2 Use Scapy to Sniff Network Traffic

We can use the Scapy tool to view network traffic like tcpdump or tshark.

**Step 1: Use the sniff() function**

To listen on the eth0 network by default, directly;

·        sniff()

While listening to our network with sniff, let's view the number of packets sent by pinging from a side terminal.

We turned on listening in the Scapy command terminal. Let's send our ping command from another terminal on the side.


<div class="code-window">
<br>
<span class="highlight">kali@kali</span> ping -c 5 www.cisco.com
</div>

After pressing Ctrl + C in the Scapy terminal, the resulting output shows the number of packets received.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sniffed.webp' | relative_url }}" width="600" height="80" alt="Output showing the number of ping packets captured after Scapy sniff()">
</div>

**Step 2: Capture and save traffic on a spesific interface**

Let's note down the interface name for the 10.6.6.1 IP address in ifconfig. Let's go to the Scapy tool's terminal and type the command below;

·        sniff(iface=”br-internal”)

As we did above, the sniff function is used to listen to the network. But as we mentioned, by default it listens on the eth0 interface. This time, we're listening on a specific interface with this command. Br-internal is the bridge interface for the virtual machines.

After entering the command, this time we open the address 10.6.6.23 in Mozilla.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/gravemind.webp' | relative_url }}" width="650" height="330" alt="The Gravemind web page opened at address 10.6.6.23 in the browser">
</div>

After the Gravemind page loads, we can stop listening from the Scapy terminal; you can view the output by pressing Ctrl + C.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sniffed2.webp' | relative_url }}" width="600" height="80" alt="Scapy output for traffic captured on the br-internal interface">
</div>

To view the traffic, we can first save it to a variable and then view it.

·        a=\_

·        a.summary()

**Step 3: Examine the collected packets**

Let's again listen on our interface named br-internal via Scapy. But this time, let's have it capture only ICMP protocol packets and a total of 10 packets.

·        sniff(iface=”br-internal”,filter=”ICMP”,count=10)
Let's go to a different tab and ping the IP address 10.6.6.23.

·        ping -c 10 10.6.6.23

Going to the Scapy terminal, you can see how many ICMP packets were captured. An example is given in the output above. To save and view the captured packets;

·        a=\_

·        a.nsummary()
\*nsummary() and summary() are similar but different commands. The nsummary() command is used to view multiple packets, while the summary() command is used to view only a single packet.

If you want more information about a packet, you can get information by typing the packet's number without the leading zeros. An example is given below;

·        a\[2\]

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/ether.webp' | relative_url }}" width="900" height="80" alt="Packet detail information displayed with the a[2] command in Scapy">
</div>

We can save these outputs as a pcap file and examine them in Wireshark as well. We can use the commands below to do this.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> wrpcap(“capture1.pcap”, a)
</div> 

We can examine the saved pcap file in Wireshark.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/pcap.webp' | relative_url }}" width="650" height="220" alt="Wireshark view of the capture1.pcap file saved with wrpcap">
</div>

##### Part 3 Create and Send an ICMP Packet

ICMP is a protocol designed to send control messages between network devices. There are many different types of ICMP packets.

**Step 1: Use interactive mode to create and send a custom ICMP packet.**

Let's start listening on the interface named "br-internal" via the Scapy terminal.

·        sniff(iface=”br-internal”)

After starting to listen, let's open a new terminal and open another Scapy terminal with sudo permission. Here, we'll craft our own ICMP packet and send it to the IP address 10.6.6.23.

·        send(IP(dst="10.6.6.23")/ICMP()/"This is a test")

Let's examine this command section by section.

·        **IP(dst="10.6.6.23")** : This part creates the IP layer. With dst, we specify where the packet will go.

·        **/ICMP()** : The ICMP layer is added on top of the IP layer. By default, an echo-request message is created; if you want to create a different type of ICMP message, you can use the type function, for example type=0.

·        **/”This is a test”** : This part adds raw data to the packet.

After sending this message, we can go back to the Scapy terminal where we're listening and press CTRL + C. The output we get is as follows;

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sniffed3.webp' | relative_url }}" width="600" height="80" alt="Scapy sniff output after sending the custom-crafted ICMP packet">
</div>

Let's save this output and examine its content.

·        a=\_

·        a.nsummary()

·        a\[2\]
\*This type of ICMP packet is generally used to **test whether the target is reachable**.

##### Part 4 Create and Send a TCP SYN Packet

Now it's time to create and send a TCP SYN packet. Again, as we did at the start, let's put our interface into listening mode.

·        sniff(iface=”br-internal”)

Let's switch to the other Scapy terminal and start creating the packet.

·        send(IP(dst="10.6.6.23")/TCP(dport=445, flags="S"))

We can see the similarity with the ICMP packet we created earlier. Let's break this packet down into sections as well and examine it.

·        **IP(dst="10.6.6.23")** : This part defines the IP layer. It points to the destination the packet will go to.

·        **TCP(dport=445, flags="S")** : This part defines the TCP layer. It points to the destination TCP port and the flag. Since the flag value is S, this is a TCP SYN, i.e., a connection initiation operation.

This is actually roughly a port scanning operation; while tools like nmap automate this, we can also perform port scanning like this manually. To understand whether the port is open, you need to examine the packets in the flow. If the flags value in the response packet is "SA", i.e., SYN-ACK, that means the port is open.

After sending the command, let's stop listening by pressing CTRL + C on the listening terminal. Let's save and examine the traffic.

·        a=\_

·        a.nsummary()

·        a\[2\]

·        a\[3\]

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sniffed4.webp' | relative_url }}" width="1000" height="300" alt="SYN and SYN-ACK packets captured after sending the TCP SYN packet">
</div>

Packet 2 is the packet we sent to initiate the connection, with a flags value of "S". When we examine packet 3, we see that the flags value is SA, i.e., SYN-ACK. This means port 445 is open and has confirmed our connection request.

#### 3.2.6 Lab – Network Sniffing with Wireshark

##### Part 1 Capture and Save Network Traffic

In this part, we'll capture traffic using tcpdump from the CLI. After saving the traffic as a pcap file, we'll examine it with Wireshark or a similar application.

Let's open the terminal and enter the command below;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> ifconfig
</div> 

Here, copy the name of the Ethernet adapter (usually eth0). Then, to use the tcpdump tool, in the terminal;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo tcpdump -i eth0 -s 0 -w packetdump.pcap
</div> 

let's type this. Let's explain this command;

·        **\-i eth0 :** Specifies which interface the traffic will be listened on.

·        **\-s 0 :** Means capture the packet completely, don't skip any part of it.

·        **\-w packetdump.pcap :** Save the captured packets to a file instead of printing them to the screen.

After typing this command, tcpdump starts listening for us. We can go to the web browser and start generating traffic. After generating it, we can come back to the terminal and stop the traffic with CTRL + C. We can examine the file where the results were saved in Wireshark.

##### Part 2 View and Analyze the Packet Capture

After opening the Wireshark interface, we can open the file named packetdump.pcap from the **File>Open** tab to examine it.

When you want to access a website in the browser, your computer sends a DNS query to the DNS server IP address. If we examine the DNS records in the captured pcap file, we can also see the domain names and IP addresses of the sites the user visited.

Let's filter for the skillsforall.com site we visited while generating web traffic in Wireshark.

**Step 1: Analyze DNS traffic**

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/skillsforall.webp' | relative_url }}" width="880" height="120" alt="DNS traffic filtered for skillsforall.com in Wireshark">
</div>

After typing skillsforall.com into the search icon, let's select the "String" value from the menu that appears below and type the word skillsforall. You can see what we did in the screenshot above. Let's click on the first packet that appears to examine it.

In the Ethernet II section here, you can see both the destination and source MAC addresses. To confirm, you can type the ifconfig command in the terminal and check the MAC address of the eth0 interface.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/destination.webp' | relative_url }}" width="1000" height="180" alt="Source and destination MAC addresses in the Ethernet II layer in Wireshark">
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/eth0.webp' | relative_url }}" width="950" height="200" alt="MAC address of the eth0 interface displayed with the ifconfig command">
</div>

In the packet details section, let's examine the Domain Name System query section. Here you can find the details of what was sent to the DNS server. There's also a Response In section indicating which packet in Wireshark is the DNS server's response.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/response.webp' | relative_url }}" width="600" height="450" alt="Detail and Response In information of the DNS query packet in Wireshark">
</div>

**Step 2: Analyze an HTTP session**

We'll try to log in to the DVWA page already installed on our Kali machine. We'll try to obtain the user credentials by viewing this in Wireshark as well. To do this, we first need to find out the interface name for the DVWA server's IP block. DVWA is located at address 10.6.6.13.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/br-inter.webp' | relative_url }}" width="890" height="200" alt="Detection of the br-internal network interface where the DVWA server is located">
</div>

As seen here, br-internal is the name of our interface. After opening Wireshark, we select the br-internal interface from the list of interface names shown below. This way, Wireshark starts listening on the br-internal interface.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/capture.webp' | relative_url }}" width="800" height="270" alt="br-internal listening interface selected in the Wireshark interface list">
</div>

After starting to listen, we access the address 10.6.6.13, i.e., the DVWA page, through the browser. To log in, we enter the values **admin** and **password**. After entering the values, we close the browser and stop listening in Wireshark by clicking the red square above. We type String in the search menu and POST in the search field.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/postt.webp' | relative_url }}" width="1200" height="70" alt="Login request packet found by the String POST search in Wireshark">
</div>

In the resulting packet, we see that information is sent via login.php. You can see the login credentials in the HTML Form URL Encoded section of the packet.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/hypertext.webp' | relative_url }}" width="830" height="250" alt="DVWA login credentials seen in the HTML Form URL Encoded field">
</div>

Cookies are used for many different purposes. Most commonly, they're used to store a user's session information. Cookies can be hijacked and a user's session can be stolen. The first cookie is sent within the HTTP response with a Set-Cookie value.

We can find the first cookie in Wireshark by searching for 302 Found.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/set.webp' | relative_url }}" width="880" height="620" alt="PHPSESSID cookie assigned via Set-Cookie in the 302 Found response">
</div>

As shown in the output, the PHPSESSID cookie has been assigned.
