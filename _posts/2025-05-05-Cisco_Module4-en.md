---
categories: [modul]
layout: post
lang: en
desc: "This is the fourth part of the Cisco Ethical Hacker course. It covers social engineering attacks (pretexting, email phishing, tabnabbing, etc.) and hands-on examples using BeEF and DVWA."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 4
tags: [Cisco, Social Engineering]
order: 6
permalink: /en/Cisco_Module4
translation_url: /Cisco_Module4
---

# Cisco Ethical Hacker

# Module 4: Social Engineering Attacks

## 4.1 Pretexting for an Approach and Impersonation

Let me explain some of the terms that come up in social engineering.

·        **Pretexting**: Creating a false pretext

·        **Impersonation**: Assuming an identity, for example acting like an IT staff member.

·        **Pharming**: Making a fake site look real and redirecting the user to it.

## 4.2 Social Engineering Attacks

### 4.2.1 Email Phishing

In a phishing attack, the attacker sends the user a site that looks trustworthy and legitimate and asks them to enter their information.

**Spear Phishing**

This is phishing tailored to a specific person or targeted at specific company groups.

**Whaling**

Essentially similar to phishing and spear phishing, but the targets are senior executives or other important people.

### 4.2.2 Vishing

A social engineering attack carried out over a phone call. It tries to obtain various pieces of information about the target.

### 4.2.3 Short Message Service (SMS) Phishing

There are also various phishing methods carried out via short messages sent to mobile devices. They may have content like "you've won a prize" or "there's an issue with your Amazon order," etc.

### 4.2.4 Universal Serial Bus (USB) Drop Key

Another tactic attackers use is leaving USB drives containing malicious software in random places. People plug USB drives they find on the ground into their own computers without hesitation.

### 4.2.5 Watering Hole Attacks

The attacker analyzes the websites the target user regularly visits and tries to inject code into them. This way, the code runs on the victim's next visit and they're redirected to another malicious site. This type of redirection is also known as a **pivot attack**.

## 4.3 Physical Attacks

### 4.3.1 Tailgating

Piggybacking happens when an authorized person allows entry into a restricted area with their permission. In other words, if someone asks another person to hold the door for them while entering, that's piggybacking.

Tailgating, on the other hand, refers to sneaking in behind people without an authorized person's permission.

### 4.3.2 Dumpster Diving

The attacker tries to gather information about the target person by going through their trash.

### 4.3.3 Shoulder Surfing

This is learning a person's personal information by looking over their shoulder while they type on their laptop or phone without their permission.

### 4.3.4 Badge Cloning

This refers to the process of cloning and duplicating the badges or cards of people working at an organization.

## 4.4 Social Enginerring Tools

### 4.4.1 Social-Engineer Toolkit (SET)

Let's see how easily a spear phishing email can be made using SET.

**Step 1**

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo setoolkit
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/fsoci.webp' | relative_url }}" width="300" height="500" alt="Running the sudo setoolkit command in the terminal">
</div>

**Step 2**

Let's select the Social-Engineering Attack option from the menu.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/socialeng.webp' | relative_url }}" width="500" height="250" alt="Selecting the Social-Engineering Attacks option in the SET menu">
</div>

**Step 3**

From the menu that appears, let's select the Spear-Phishing Attack Vectors option.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/spearp.webp' | relative_url }}" width="500" height="250" alt="View of the Spear-Phishing Attack Vectors menu option">
</div>

**Step 4**

Here we're offered a few more options again, we select option 2.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/createf.webp' | relative_url }}" width="400" height="100" alt="Selecting the file creation option for the spear-phishing attack">
</div>

**Step 5**

Here we're asked to select a file format. We continue with option 13.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/adobe.webp' | relative_url }}" width="600" height="460" alt="List of file format options for the malicious PDF">
</div>

**Step 6**

We choose the format of the PDF file we'll put into the email. We select option 2, the blank pdf option.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/built.webp' | relative_url }}" width="600" height="70" alt="Selecting the blank PDF template option">
</div>

**Step 7**

We choose which type of reverse shell we'll use. We select the first option.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/reverse.webp' | relative_url }}" width="1000" height="150" alt="Reverse shell payload type selection list">
</div>

**Step 8 – 9**

After giving the IP address and port the shell will listen on, it asks whether or not we want to change the file's name.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/setpayload.webp' | relative_url }}" width="640" height="450" alt="Entering the listener IP and port information and the file name question">
</div>

**Step 10**

We determine whether this payload will be sent to an email group or to a single email address. We choose a single address.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/email.webp' | relative_url }}" width="600" height="130" alt="Choosing to send the malicious file to a single email address">
</div>

**Step 11 – 14**

After creating the content of the email, it's ready to send.

### 4.4.2 Browser Exploitation Framework (BeEF)

Using an XSS attack, the attacker redirects the user to a different malicious site and tries to steal their cookies.

The Browser Exploitation Framework is used to try to steal cookies by exploiting XSS vulnerabilities.

Below is a sample view of the stolen cookies.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/cookie1.webp' | relative_url }}" width="650" height="600" alt="Screenshot of cookies stolen via XSS using BeEF">
</div>
After the cookie is stolen, a fake notification can even be sent to the user.

### 4.4.3 Call Spoofing Tools

You can very easily change the number that appears as the caller. A few example tools for this:

·        **SpoofApp**: An application used to spoof numbers on both Android and iOS.

·        **SpoofCard**: This tool is also an application used to spoof numbers, change your voice, and create different background noise on both Android and iOS.

·        **Arterisk**: A Voice over IP control tool.

### 4.4.4 Lab – Explore the Social Engineer Toolkit (SET)

#### Part 1 Cloning a Website to Obtain User Credentials

**Step 1: Investigate Web Attack Vectors in SET**

From the Setoolkit tool's menu, we first select the "Social-Engineering Attacks" option.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/social2.webp' | relative_url }}" width="420" height="180" alt="Selecting the Social-Engineering Attacks option in the SET menu">
</div>
After this menu, we select option 2, "Website Attack Vectors".

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/website.webp' | relative_url }}" width="420" height="270" alt="Selecting the Website Attack Vectors menu option">
</div>

After reading the description of the attacks here, for our attack we select option 3, "Credential Harvester Attack Method".

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/credential.webp' | relative_url }}" width="500" height="200" alt="Selecting the Credential Harvester Attack Method option">
</div>

**Step 2: Clone the DVWA.vm login screen**

In this step we'll clone the DVWA.vm login website. SET creates a website hosted on the computer. If victims enter their information here, it will be captured.

Let's select the Site Cloner option from the menu below.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/site.webp' | relative_url }}" width="300" height="120" alt="Selecting the Site Cloner option from the menu">
</div>
It asks us for the web attacker's IP address; since our Kali machine is on the 10.6.6.0/24 block, we enter the address 10.6.6.1.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/podt.webp' | relative_url }}" width="800" height="20" alt="Entering 10.6.6.1 as the attacker IP address">
</div>

Now we enter the URL of the website we want to clone.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/createf.webp' | relative_url }}" width="400" height="10" alt="Entering the URL address of the DVWA website to be cloned">
</div>

We successfully started listening.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/webattack.webp' | relative_url }}" width="500" height="160" alt="Output showing that listening has started successfully on the cloned site">
</div>

#### Part 2 Capturing and Viewing User Credentials

In a real attack, this website would be delivered to the victim via a link or QR code. However, in this lab environment we'll just create an html document to redirect to the website.

**Step 1: Create the Social Engineering Exploit**

Let's create our HTML file and then write the html code given below into it.

 **<html>**

**<head>**

meta http-equiv="refresh" content="0; url=http://10.6.6.1/" 

**</head>**

**</html>**

After writing the code, let's name it Great\_link.html and save it.

**Step 2: Capture User Credentials**

After saving the HTML file, let's double-click on it to open the page we cloned. So what's the difference from the original page? Let's take a look right away. The first image is my cloned page.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/dvwa1.webp' | relative_url }}" width="530" height="450" alt="View of the fake DVWA login page cloned with SET">
</div>

Below is the original page; let's pay attention to the page's extensions.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/dvwa2.webp' | relative_url }}" width="530" height="450" alt="View of the original DVWA login page and its URL extension">
</div>

Now let's test it by entering our information. Let's enter the following information.

·        Username: [some.user@gmail.com](mailto:some.user@gmail.com)

·        Password: Pa55w0rdd!

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/dvwa3.webp' | relative_url }}" width="530" height="450" alt="Entering a username and password on the fake DVWA page">
</div>

The moment we click the Login button, it will redirect us to the original DVWA page. You can follow this from the page's URL.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/dvwa4.webp' | relative_url }}" width="530" height="450" alt="View after being redirected to the original DVWA page after logging in">
</div>

As seen above.

**Step 3: View the Captured Information**

Let's go back to the SET tool's terminal. You can see the entered information in the output.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/username.webp' | relative_url }}" width="730" height="150" alt="Captured username and password output in the SET terminal">
</div>

You can create and save a report in XML format with CTRL + C. You can access the saved file with cat to view its contents.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/cat.webp' | relative_url }}" width="530" height="450" alt="XML-format capture report viewed with the cat command">
</div>

### 4.4.5 Lab – Using the Browser Exploitation Famework (BeEF)

#### Part 1 Load the BeEF GUI Environment

**Step 1: Start BeEF**

Let's run our tool from the Application> All Application> beef start menu. The first time we run it, it will ask us to change the password. Change the password and don't forget it.

After the GUI opens, we log in with our information.

·        Username: beef

·        Password: your password

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/beef1.webp' | relative_url }}" width="450" height="370" alt="BeEF control panel login screen">
</div>

**Step 2: Hook the local browser to simulate a client-side attack**

Before exploitation, you first need to "hook" the target browser. For this lab we'll use the local system. If this were a real test, we would identify the websites the victim visits frequently and place the BeEF hook JavaScript code into them to carry out the process. In this lab we'll go with the demo version.

A website has been created for us for the demo version.

[http://127.0.0.1:3000/demos/butcher/index.html](http://127.0.0.1:3000/demos/butcher/index.html)

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/beef2.webp' | relative_url }}" width="720" height="370" alt="View of the BeEF hook demo site's butcher page">
</div>

We can access the site via this address. Let's take a closer look after accessing the site. We know a JS code runs in the background to create the hook. Let's view the source code with CTRL + U.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/script.webp' | relative_url }}" width="950" height="100" alt="View of the hook.js script reference in the page source code">
</div>

We can see here that the hook.js file is what creates the beef hook.
Let's go back to the page with the control panel. We see that new information has been added in the Hooked Browsers menu on the left.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/online.webp' | relative_url }}" width="300" height="200" alt="New target appearing in the Hooked Browsers menu in the BeEF panel">
</div>

We click on the Online Browsers menu and the information appears in front of us.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/online2.webp' | relative_url }}" width="620" height="570" alt="Hooked browser information in the BeEF Online Browsers menu">
</div>

#### Part 2 Investigate BeEF Exploit Capabilities

**Step 1: Investigate the commands and network tabs**

Let's also get familiar with the other menus. Let's start examining by clicking on the Commands menu.

The Module Tree found here shows all the attacks, information gathering, and social engineering capabilities that can be carried out against the browser, categorized.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/browser.webp' | relative_url }}" width="500" height="330" alt="List of Module Tree categories in the BeEF Commands tab">
</div>

If we expand the items in this menu, you'll notice the color codes next to each function. Each color code has a different meaning.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/renkkod.webp' | relative_url }}" width="200" height="600" alt="View of BeEF modules listed by color code">
</div>

·        **Green**: This command module works against the target and is invisible to the user.

·        **Orange**: This command module works against the target but may be visible to the user.

·        **White**: This command module has not been verified against the target.

·        **Red:** This command module cannot be used against the user.

**Note**: The Module Tree is also used like a filter, and you can search here.

Let's go to the Network menu. Here you can see the network topology with the victim. Since we're working locally, it will only show one network and one host.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/hooked.webp' | relative_url }}" width="400" height="240" alt="Network topology view with the victim in the BeEF Network tab">
</div>

**Step 2: Use BeEF to iniate a social enginerring attack**

In this step, we'll send a fake notification to the hooked web page to get the user to install a malicious plugin.

Let's click on the Commands menu. Let's scroll down to the Social Engineering category. Let's select the Fake Notification Bar (Firefox) option found here.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/fake.webp' | relative_url }}" width="350" height="340" alt="Selecting the Fake Notification Bar module in the Social Engineering category">
</div>

After selecting it, the URL the module will run on and the message the notification will send are displayed in the menu on the right side.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/fake2.webp' | relative_url }}" width="460" height="240" alt="URL and message settings panel for the Fake Notification Bar module">
</div>

Change the URL to http://10.6.6.13. This URL redirects to the login screen of the DVWA virtual server. The URL can point to any web page, whether local or on the network. In a live environment, this could also be a cloned site or a page containing a malicious script.
Let's also change the message to be sent to "AdBlocker Security Extension is out of date. Install the new version now."
We can run the module by pressing the Execute button. When you go back to the butcher page, you can see the warning.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/plugin.webp' | relative_url }}" width="660" height="100" alt="Fake extension update warning displayed on the target browser">
</div>

When you click the Install plug-in button, you're redirected to our cloned malicious DVWA login page, as shown in the screenshot below.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/login.webp' | relative_url }}" width="360" height="330" alt="Cloned DVWA login page redirected to after the fake extension warning">
</div>

**Step 3: Use TabNabbing to display malicious website**

This is a function that, if a hooked browser tab stays idle for too long, redirects to a different URL address.

Let's repeat the steps we did above.

·        Open a new Mozilla page.

·        Open [http://127.0.0.1:3000/ui/authentication](http://127.0.0.1:3000/ui/authentication) on a new page.

·        Log in to the system with your credentials.

**·**        **Access** [http://127.0.0.1:3000/demos/butcher/index.html](http://127.0.0.1:3000/demos/butcher/index.html) **via Mozilla.**

**·**        **Open the** **Command** **tab from the Online Browsers menu in the BeEF control panel.**

**·**        **Select** **TabNabbing** **from the** **Social Engineering** **category.**

Here you can again see the module's general settings.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/tabnab.webp' | relative_url }}" width="430" height="240" alt="General settings screen for the TabNabbing module">
</div>

Type 1 instead of 15 minutes and don't touch your browser for 1 minute. The site normally open in the browser
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/butcher.webp' | relative_url }}" width="750" height="440" alt="The original butcher demo page open in the browser">
</div>
is this, while below is the site it redirects to once left idle for 1 minute.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/secret.webp' | relative_url }}" width="510" height="480" alt="Fake page redirected to after one minute via TabNabbing">
</div>

Let's type "This is my secret" into the box in the middle. Then you can see the value written in the box in the Logs menu on the Control Panel page.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/thisismy.webp' | relative_url }}" width="810" height="200" alt="The captured This is my secret text in the BeEF Logs menu">
</div>

## 4.5 Methods of Influence

·        **Authority**: In social engineering, this shows both confidence and perhaps authority.

·        **Scarcity and Urgency**: A method used to manipulate the victim by increasing their sense of urgency.

·        **Social Proof**: When people don't know how to behave in a situation, they take others' behavior as an example.

·        **Likeness**: Since people are more easily influenced by people they like, using someone attractive and likeable works better.

·        **Fear**: People may act thoughtlessly out of anxiety over the thought that something bad will happen to them.
