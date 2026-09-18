---
categories: [makine]
layout: post
lang: en
description: "This Rick and Morty themed challenge requires you to exploit a web server and find three ingredients that will help Rick make his potion and turn himself from a pickle back into a human."
logo: "/assets/images/picklerick.png"
author: nazy
title: TryHackMe Pickle Rick
tags: [TryHackMe, Command Injection]
order: 4
permalink: /en/Tryhackme_PickleRick
translation_url: /Tryhackme_PickleRick
---
## Port Scan

It asks us for the three ingredients needed to turn Rick back into a human.

Our machine IP address: 10.10.246.186

I start by gathering information with an nmap scan.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> nmap -sC -sV 10.10.246.186<br>  
PORT   STATE SERVICE VERSION<br>  
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)<br>  
| ssh-hostkey:<br>  
|   3072 03:b8:cc:f9:aa:e4:d5:dd:cb:a7:e8:9c:22:1b:4a:5e (RSA)<br>   
|   256 b3:ac:ad:44:04:b9:3f:ee:b6:7a:9c:bc:19:c9:04:86 (ECDSA)<br>   
|_  256 7c:06:dd:f0:cd:4f:6f:05:ef:94:d7:81:21:67:e5:12 (ED25519)<br>  
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))<br>  
|_http-title: Rick is sup4r cool<br>  
|_http-server-header: Apache/2.4.41 (Ubuntu)<br>  
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel<br>    
</div>
As a result of the nmap scan, we find that the ssh and http ports are open. Since we don't have an obvious vulnerability for SSH, I access port 80 through the browser. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/first.webp' | relative_url }}" width="500" height="400" alt="The website titled 'Rick is sup4r cool' opened in the browser">
</div>

Rick asks us to access his computer and find the last three hidden ingredients, but states that he doesn't remember his password. Let's try to gather information from the web page. Let's first start by inspecting the page's source code. While inspecting the source code, we see that we're given a username. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/sec.webp' | relative_url }}" width="700" height="400" alt="The hidden username comment found in the page source code">
</div>

Great! Now, to learn more details, we'll scan for hidden files.

## File Scanning

We'll use a tool called gobuster for this process. Gobuster is a fast and powerful directory and file discovery scanner that uses brute force. We'll use the following command to use this tool.

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> gobuster dir -u http//10.10.246.186 -w /root/Desktop/SecLists-master/Discovery/Web-Content/directory-list-2.3-medium.txt -x php,sh,txt,cgi,html,css,js,py
</div>
This command will let us find hidden files by trying the wordlist items we specified with the -w parameter. In the command's output, we see that we're able to find a few hidden files. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/th.webp' | relative_url }}" width="650" height="100" alt="The list of hidden directories and files found by the Gobuster scan">
</div>

Let's view these files in the browser. First, let's go to the login.php address. At this address, a login page like the screenshot below greets us. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/fort.webp' | relative_url }}" width="380" height="440" alt="Screenshot of the login form on the login.php page">
</div>

We have a username but we still don't know the password. Gobuster told us there were a few other files as well. One of those files is robots.txt (it doesn't appear in the screenshot because it's further down in the output). The robots.txt file is a page that tells Google bots which pages and directories they can and cannot crawl and index. 
This page gives us a value. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/fif.webp' | relative_url }}" width="400" height="100" alt="The hidden password value found in the robots.txt file">
</div>
## First Ingredient

Let's try this value as the password when logging in. Bingo! We were able to log in. A command panel greets us.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/si.webp' | relative_url }}" width="500" height="100" alt="The view of the command execution panel accessed after logging in">
</div>
Let's list the files on the panel using the ls command. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/seve.webp' | relative_url }}" width="200" height="200" alt="The file list output of the 'ls' command on the command panel">
</div>
The name of the first file looks quite suspicious. Let's go to the URL [http://10.10.246.186/Sup3rS3cretPickl3Ingred.txt](http://10.10.246.186/Sup3rS3cretPickl3Ingred.txt) to access the file.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/ei.webp' | relative_url }}" width="500" height="100" alt="The first ingredient found in the Sup3rS3cretPickl3Ingred.txt file">
</div>
Bingo, we find our first hidden ingredient. Let's continue to collect more ingredients. Let's take another look at the files we found with the ls command. Among the files, we can find a clue with the clue.txt file. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/nin.webp' | relative_url }}" width="400" height="100" alt="The hint to look at the file system in the clue.txt file">
</div>
## Second Ingredient

It tells us that we need to look at the file system.

·        ls /home

Let's use this to view the contents of our home folder. In the output, we see two different folders named rick and ubuntu. Let's view the rick one.

·        ls /home/rick

We see there's a file here called second ingredients. However, we can't view the content of this file with commands like cat, nano, or vim.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/ten.webp' | relative_url }}" width="300" height="180" alt="The error showing the 'second ingredients' file cannot be opened with cat">
</div>
Let's research cat-like commands and try our luck again. I'm able to get the output with the following command.  
·        less ‘/home/rick/second ingredients’
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/el.webp' | relative_url }}" width="150" height="50" alt="The second ingredient content viewed with the less command">
</div>
Let's continue our research to find the other ingredient.

## Third Ingredient

Let's try to view the contents of the root folder. Let's try the ls /root command, but I guess we don't have access to the root folder. Let's use the sudo -l command to view our privileges. But what's this?
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/twe.webp' | relative_url }}" width="750" height="100" alt="The NOPASSWD privilege for www-data in the sudo -l output">
</div>
What the output indicates is that the www-data user can run any command without a password. So we can view the contents of the root folder.

·        sudo ls /root
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/13.webp' | relative_url }}" width="75" height="60" alt="The 3rd.txt file seen with the 'sudo ls /root' command">
</div>
And we see the txt file containing our third ingredient. Let's use the less command to view its content and grab our final flag too.

·        less /root/3rd.txt
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_picklerick/14.webp' | relative_url }}" width="250" height="50" alt="The third ingredient flag obtained with less /root/3rd.txt">
</div>
