---
categories: [modul]
layout: post
lang: en
description: "The second part of the fourth module of the Cisco Ethical Hacker course. Covers hooking a browser, sending fake notifications, and TabNabbing attacks with the Browser Exploitation Framework (BeEF), and summarizes the persuasion methods used in social engineering."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 4 (2/2)
tags: [Cisco, Social Engineering]
order: 6.5
permalink: /en/Cisco_Module4_2
translation_url: /Cisco_Module4_2
---

#### 4.4.5 Lab – Using the Browser Exploitation Framework (BeEF)

##### Part 1 Load the BeEF GUI Environment

**Step 1: Start BeEF**

Let's run our tool from the Application> All Application> beef start menu. The first time we run it, it will ask us to change the password. Change the password and don't forget it.

After the GUI opens, we log in with our information.

- Username: beef
- Password: your password

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

##### Part 2 Investigate BeEF Exploit Capabilities

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

- **Green**: This command module works against the target and is invisible to the user.
- **Orange**: This command module works against the target but may be visible to the user.
- **White**: This command module has not been verified against the target.
- **Red:** This command module cannot be used against the user.

**Note**: The Module Tree is also used like a filter, and you can search here.

Let's go to the Network menu. Here you can see the network topology with the victim. Since we're working locally, it will only show one network and one host.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/hooked.webp' | relative_url }}" width="400" height="240" alt="Network topology view with the victim in the BeEF Network tab">
</div>

**Step 2: Use BeEF to initiate a social engineering attack**

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

- Open a new Mozilla page.
- Open [http://127.0.0.1:3000/ui/authentication](http://127.0.0.1:3000/ui/authentication) on a new page.
- Log in to the system with your credentials.
- Access [http://127.0.0.1:3000/demos/butcher/index.html](http://127.0.0.1:3000/demos/butcher/index.html) via Mozilla.
- Open the Command tab from the Online Browsers menu in the BeEF control panel.
- Select TabNabbing from the Social Engineering category.

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

### 4.5 Methods of Influence

- **Authority**: In social engineering, this shows both confidence and perhaps authority.
- **Scarcity and Urgency**: A method used to manipulate the victim by increasing their sense of urgency.
- **Social Proof**: When people don't know how to behave in a situation, they take others' behavior as an example.
- **Likeness**: Since people are more easily influenced by people they like, using someone attractive and likeable works better.
- **Fear**: People may act carelessly out of anxiety, thinking something bad is about to happen to them.
