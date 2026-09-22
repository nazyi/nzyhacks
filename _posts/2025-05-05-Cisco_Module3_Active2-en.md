---
categories: [modul]
layout: post
lang: en
description: "The second part of the active information gathering section of the third module of the Cisco Ethical Hacker course. Covers hands-on labs on packet inspection, packet crafting with Scapy, and network traffic analysis with Wireshark."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 3 - Active Recon (2/2)
tags: [Cisco, Active Recon]
order: 4.5
permalink: /en/Cisco_Module3_Active2
translation_url: /Cisco_Module3_Active2
---

#### 3.2.4 Packet Inspection and Eavesdropping

Packet captures can be performed, packets can be inspected and listened to, with tools such as Wireshark, tshark, and tcpdump. For penetration testers, such tools can be useful for performing passive reconnaissance. Of course, this kind of reconnaissance requires a physical or wireless connection to the target.

#### 3.2.5 Lab – Packet Crafting with Scapy

##### Part 1 Investigate the Scapy Tool

Before sending an IP packet, it's important to understand the contents of the IP packet. Every IP packet is accompanied by a header that provides information about the packet structure. Each binary value has a different meaning within the IP packet.

You can examine the details about the fields with the ls() function. The general logic of using a function within Scapy is function\_name (arguments). To get more information about the fields, you can run the ls(IP) command.

The table below gives the field names and their descriptions.

| Field Name | Description |
|---|---|
| Version | Indicates the version of the IP protocol (4 for IPv4). |
| Header Length | Indicates the length of the header. |
| Type of Service (ToS) | Indicates the type of service; contains information such as priority. |
| Total Length | The total length of the whole packet (header + data). |
| Identification | Used to identify the packet; important for fragmentation. |
| Flags | Control information related to packet fragmentation. |
| Fragment Offset | Indicates the order of fragmented packets. |
| Time to Live (TTL) | Determines how long the packet can travel on the network. |
| Protocol | Indicates the upper-layer protocol it carries (for example, TCP: 6, UDP: 17). |
| Header Checksum | Used to check the integrity of the header. |
| Source IP Address | The IP address of the device sending the packet. |
| Destination IP Address | The IP address of the packet's destination device. |
| Options (Optional) | Optional fields for certain special cases. |
| Data | The actual data carried by the IP packet. |

##### Part 2 Use Scapy to Sniff Network Traffic

We can use the Scapy tool to view network traffic like tcpdump or tshark.

**Step 1: Use the sniff() function**

To listen on the eth0 network by default, directly;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff()
</div>

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

**Step 2: Capture and save traffic on a specific interface**

Let's note down the interface name for the 10.6.6.1 IP address in ifconfig. Let's go to the Scapy tool's terminal and type the command below;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff(iface=”br-internal”)
</div>

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

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a=\_<br>a.summary()
</div>

**Step 3: Examine the collected packets**

Let's again listen on our interface named br-internal via Scapy. But this time, let's have it capture only ICMP protocol packets and a total of 10 packets.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff(iface=”br-internal”,filter=”ICMP”,count=10)
</div>

Let's go to a different tab and ping the IP address 10.6.6.23.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> ping -c 10 10.6.6.23
</div>

Going to the Scapy terminal, you can see how many ICMP packets were captured. An example is given in the output above. To save and view the captured packets;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a=\_<br>a.nsummary()
</div>

\*nsummary() and summary() are similar but different commands. The nsummary() command is used to view multiple packets, while the summary() command is used to view only a single packet.

If you want more information about a packet, you can get information by typing the packet's number without the leading zeros. An example is given below;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a\[2\]
</div>

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

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff(iface=”br-internal”)
</div>

After starting to listen, let's open a new terminal and open another Scapy terminal with sudo permission. Here, we'll craft our own ICMP packet and send it to the IP address 10.6.6.23.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> send(IP(dst="10.6.6.23")/ICMP()/"This is a test")
</div>

Let's examine this command section by section.

- **IP(dst="10.6.6.23")**: This part creates the IP layer. With dst, we specify where the packet will go.
- **/ICMP()**: The ICMP layer is added on top of the IP layer. By default, an echo-request message is created; if you want to create a different type of ICMP message, you can use the type function, for example type=0.
- **/"This is a test"**: This part adds raw data to the packet.

After sending this message, we can go back to the Scapy terminal where we're listening and press CTRL + C. The output we get is as follows;

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sniffed3.webp' | relative_url }}" width="600" height="80" alt="Scapy sniff output after sending the custom-crafted ICMP packet">
</div>

Let's save this output and examine its content.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a=\_<br>a.nsummary()<br>a\[2\]
</div>

\*This type of ICMP packet is generally used to **test whether the target is reachable**.

##### Part 4 Create and Send a TCP SYN Packet

Now it's time to create and send a TCP SYN packet. Again, as we did at the start, let's put our interface into listening mode.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff(iface=”br-internal”)
</div>

Let's switch to the other Scapy terminal and start creating the packet.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> send(IP(dst="10.6.6.23")/TCP(dport=445, flags="S"))
</div>

We can see the similarity with the ICMP packet we created earlier. Let's break this packet down into sections as well and examine it.

- **IP(dst="10.6.6.23")**: This part defines the IP layer. It points to the destination the packet will go to.
- **TCP(dport=445, flags="S")**: This part defines the TCP layer. It points to the destination TCP port and the flag. Since the flag value is S, this is a TCP SYN, i.e., a connection initiation operation.

This is actually roughly a port scanning operation; while tools like nmap automate this, we can also perform port scanning like this manually. To understand whether the port is open, you need to examine the packets in the flow. If the flags value in the response packet is "SA", i.e., SYN-ACK, that means the port is open.

After sending the command, let's stop listening by pressing CTRL + C on the listening terminal. Let's save and examine the traffic.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a=\_<br>a.nsummary()<br>a\[2\]<br>a\[3\]
</div>

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

- **-i eth0:** Specifies which interface the traffic will be listened on.
- **-s 0:** Means capture the packet completely, don't skip any part of it.
- **-w packetdump.pcap:** Save the captured packets to a file instead of printing them to the screen.

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
