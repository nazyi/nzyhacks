---
categories: [makine]
layout: post
lang: en
desc: "As part of scoping, I'm trying to find wifi networks in a wireless network penetration test. However, I discovered that some SSID values were hidden. Can you help me with this?"
logo: "/assets/images/hidden_wifi.png"
author: nazy
title: CyberExam Uncovering Hidden SSID 
tags: [CyberExam, WiFi]
order: 5
permalink: /en/CyberExam-Unhidden
translation_url: /CyberExam-Unhidden
---
# Introduction
Our task, as stated above, is to find a hidden SSID. To do this, we first connect to our machine over the web. After connecting, we switch to our root user with the password "user".
We use our command to view the wireless network interfaces.
·        iwconfig

In the output of this command, we see the wlan0 interface. The wlan0 interface's mode is manually set to managed.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/iwconfig.webp' | relative_url }}" width="600" height="200" alt="Output of the iwconfig command showing the wlan0 interface in managed mode">
</div>
Now that we know the name of our interface, we can put it into monitor mode.

·        airmon-ng start wlan0
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/airmon.webp' | relative_url }}" width="600" height="200" alt="Monitor mode output of the airmon-ng start wlan0 command">
</div>
To verify that we've switched to monitor mode, we can check again with the iwconfig command, and if you notice, the interface we put into monitor mode had "mon" appended to its name, so its new name became wlan0mon.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/iw2.webp' | relative_url }}" width="600" height="200" alt="Interface name changed to wlan0mon in the iwconfig output">
</div>

# Attack
Now that we know the name of our interface, we can move on to the attack stage. The tool we'll use is called airodump-ng. With this tool we can listen to traffic and save it to a packet capture. Let's enter our command.

·        airodump-ng wlan0mon

After entering the command, we wait a while for packets to flow so we can capture values such as the BSSID.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/air2.webp' | relative_url }}" width="600" height="200" alt="List of BSSIDs captured by the airodump-ng wlan0mon command">
</div>
After the command has been running for a while, we capture a BSSID value. This value is the MAC address belonging to a nearby wireless access point. We're now going to start listening on this address. To pass the BSSID value we found to the command, we'll use the –bssid parameter, the -c parameter to specify the channel it's on, and the -w parameter to save the output to a file.

·        airodump-ng –bssid 0A:F6:14:E7:8A:6B -c 6 -w capture wlan0mon
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/airodump.webp' | relative_url }}" width="600" height="90" alt="airodump-ng listening output for a specific BSSID and channel">
</div>
You can tell whether the attack was successful from the [WPA handshake: 0A:F6:14:E7:8A:6B] shown in the top right of the output. This indicates that the capture was successful and a 4-way handshake was captured. After we start listening for this BSSID value in this terminal, in order to access this network's ESSID value we'll carry out a deauthentication attack, meaning disconnecting a device connected to this network from the network. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/wpa_handshake.webp' | relative_url }}" width="600" height="200" alt="WPA handshake notification captured in the airodump-ng output">
</div>
After waiting a while, the MAC address of a device connected to the network appears in the STATION section below. We'll use this STATION value to carry out a deauth attack against it. This way, when the device tries to reconnect to the network, the ESSID value will be sent in the clear. 

# Deauth
A deauth attack means forcibly disconnecting a device from the network. We'll carry out this attack using the aireplay-ng tool. The purpose of this tool is to force certain behaviors to occur.

·        aireplay-ng –deauth 10 -a 0A:F6:14:E7:8A:6B -c 6 7E:F4:4D:D9:5B:31 wlan0mon
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/aireplay.webp' | relative_url }}" width="600" height="200" alt="Output of the deauth attack carried out with aireplay-ng">
</div>
When we return to the terminal where we're still listening with airodump-ng, you'll see on the far right the network's ESSID value, which is normally hidden but which we've now found. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/cyberexa.webp' | relative_url }}" width="600" height="200" alt="Hidden ESSID value revealed in airodump-ng after the deauth attack">
</div>
I wanted to take the attack one step further and also find the network's password. We can try cracking the password using the file named capture-01.cap, in which we previously saved the traffic.

·        aircrack-ng -w wordlist.txt -b 0A:F6:14:E7:8A:6B capture-01.cap
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/şifre.webp' | relative_url }}" width="500" height="300" alt="WiFi password cracked from the capture file with aircrack-ng">
</div>
