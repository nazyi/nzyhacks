---
categories: [makine]
layout: post
lang: en
description: "In the brute force vulnerability lab on DVWA (Damn Vulnerable Web Application), we learned how to bypass authentication mechanisms in web applications by using automated tools to try username and password combinations. In this lab, we saw hands-on how to use tools like Hydra to detect weak or guessable passwords and gain unauthorized access to a system."
logo: "/assets/images/dvwa1.png"
author: nazy
title: DVWA Brute Force
order: 6
tags: [web, Hydra]
permalink: /en/DVWA_BruteForce
translation_url: /DVWA_BruteForce
---

### Low Sec

#### Character Set

I tried a brute force attack at the low security level. First, I captured the outgoing packet in Burp and sent it to Intruder. I set the Attack Type as Spider. I set the Payload Type as Brute Force. After marking the parameters I would work with, I entered the letters, numbers, and symbols to be tried using the character set.

My username is admin and my password is password.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/lowsec1.webp' | relative_url }}" width="850" height="270" alt="Character set brute force attack settings in Burp Suite Intruder">
</div>

#### Dictionary Attack

In this attack, we write the possible usernames and passwords into separate txt files and upload them to Burp as payload lists. The commands to create the txt files are below:

·        nano olasinick.txt

·        nano olasisifre.txt

This time I selected the Cluster Bomb Attack Type. Again, I marked the parameters I would test. Since we have 2 parameters, I selected the appropriate payload file for each parameter from the Payload List section. For example, since my first parameter is username, I selected Payload List 1 and chose olasinick.txt from the Load button. The Payload Type stayed as Simple list. I went to the Settings tab, cleared the list in the Grep - Match section, and added incorrect. The reason I added this was that I needed a marker to know when I logged in correctly. Since Burp detects the "password is incorrect" error that comes back on every attempt and classifies the ones that have it as 1 and the ones that don't as 0, I would be able to directly pick out the values for the correct login attempt.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/cluster.webp' | relative_url }}" width="850" height="270" alt="Selecting the Cluster Bomb attack type and parameters in Intruder">
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/grep.webp' | relative_url }}" width="560" height="470" alt="Adding the term incorrect to the Grep - Match settings">
</div>

The values are marked in the output below. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/adminpass.webp' | relative_url }}" width="800" height="250" alt="The correct username and password marked in the Intruder attack results">
</div>

### Wfuzz

To find all the users, let's go to [http://localhost./hackable/users/](http://localhost./hackable/users/). Let's save the usernames here into a txt file to make our job easier. Using the following wfuzz command

·        wfuzz --hs "Username and/or password incorrect." -c -z file,olasinick.txt -z file,rockyou.txt -b 'security=low; PHPSESSID=0gdtua47fc647dgjj7sitbqaa1' 'http://localhost./vulnerabilities/brute/index.php?username=FUZZ&password=FUZ2Z&Login=Login' | grep -v '250'

let's try all the users' passwords.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/target.webp' | relative_url }}" width="1000" height="180" alt="Password attempt results for all users using the Wfuzz tool">
</div>
### Medium Sec

#### Burp

The trick here becomes apparent when we examine the source code. In the DVWA interface, when we click view source at the bottom and select view all, we see the source code for every level. If we look at the source code differences between low and medium here, you'll notice the following:
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/sleep.webp' | relative_url }}" width="750" height="150" alt="The sleep(2) delay function in the medium level source code">
</div>
The sleep(2) code here means the user is made to wait 2 seconds every time they enter an incorrect login. Applying this generally, since brute-force attacks already take a long time, making each attempt wait an extra 2 seconds makes the job even harder.

#### Hydra

Our command for brute-forcing with Hydra is as follows:
<div class="code-window">
<br>
<span class="highlight">root@kali$</span> hydra -l admin -P /root/Desktop/olasisifre.txt 127.0.0.1 http-get-form "/vulnerabilities/brute/:username=^USER^&password=^PASS^&user_token=%CSRF%&Login=Login:H=Cookie: PHPSESSID=hdbj798bma7cpkjsdr42ja8r73; security=medium:F=Username and/or password incorrect." -t 6 -v
</div>
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/hydra.webp' | relative_url }}" width="850" height="270" alt="Terminal output of the brute force attack carried out with the Hydra tool">
</div>
###  High Sec

When we examine the source code at the high level, we see that an anti-CSRF token is used to prevent brute-force attacks. So what is this anti-CSRF token, and what does it do?

An anti-CSRF token is a randomly generated value that provides protection against CSRF attacks. Every time the user makes a request, this token is sent along with the form data or header. The server verifies that the request is authorized by comparing the incoming token with the value it has stored. If the token doesn't match, the request is rejected, thereby preventing unauthorized actions.

Now let's look at how we carry out this process in Burp. First, we capture the packet by making a random attempt. After that, we go to the Session tab from the settings section in the top right. We click add from the Session handling rules section.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/session.webp' | relative_url }}" width="1050" height="255" alt="The Session Handling Rules add screen in Burp Suite">
</div>
We select the Run macro option from the Rule actions section. Run Macro allows dynamic values to be added to requests by repeating automated processes such as logging in or refreshing a token.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/runmacro.webp' | relative_url }}" width="500" height="320" alt="Selecting the Run Macro option in the Rule Actions section">
</div>
After clicking add from the Select Macro section, we enable the Tolerate URL mismatch option below. This feature allows requests with the same parameter names to match by ignoring URL differences when matching parameters. It especially makes it easier to track parameters across different URLs in processes such as session authentication or token refreshing.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/addmacro.webp' | relative_url }}" width="700" height="400" alt="Checking the Tolerate URL mismatch setting on the macro add screen">
</div>
After uploading our macro packet with Add, we click on Configure Item.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/configure.webp' | relative_url }}" width="850" height="80" alt="Clicking the Configure Item button after the macro is uploaded">
</div>
Inside Configure Item, we click add on the custom parameter section below. On the page that opens, we type the parameter name and, in place of search at the bottom, type token and search for it. We take the token value from the result that appears. We press OK and close it.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/macroitem.webp' | relative_url }}" width="860" height="490" alt="Defining the custom token parameter in Configure Item">
</div>
Coming back to the Session handling rule editor page, this time from the Scope tab, we leave only Intruder checked under Tools Scope, and under URL Scope we check Use Suite Scope.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/tool.webp' | relative_url }}" width="855" height="400" alt="Tools Scope and URL Scope settings in the session handling rule">
</div>
Once everything is finished, we go to Intruder and redo our operations on our packet.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/dvwa_bruteforce/son.webp' | relative_url }}" width="850" height="230" alt="Intruder attack results after the anti-CSRF token bypass">
</div>
