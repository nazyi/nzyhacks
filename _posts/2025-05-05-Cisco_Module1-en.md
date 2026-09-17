---
categories: [modul]
layout: post
lang: en
description: "The first module of the Cisco Ethical Hacker course. It explains threat actors in cybersecurity, types of test environments, environmental considerations, and different security testing standards and methodologies. The scope and approaches of penetration tests carried out to identify and remediate organizations' security weaknesses are detailed."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 1
tags: [Cisco, Penetration Testing Fundamentals]
order: 1
permalink: /en/Cisco_Module1
translation_url: /Cisco_Module1
---

# Cisco Ethical Hacker

<h2> Module 1: Inroduction to Ethical Hacking and Penetration Testing </h2>

## 1.1 Threat Actors

·        **Organized Crime:** They carry out every kind of cybercrime activity they can turn into money, using the latest attack techniques.

·        **Hacktivists:** These attackers don't attack for money, but for a cause they believe in. To shame their target, they steal sensitive information and expose it to the public.

·        **State-Sponsored:** These are people used by countries to attack a rival country.

·        **Insider Threats:** These can be either malicious people inside the organization, for example people wanting revenge on the company, or people who unintentionally cause an information leak.

## 1.2 Environmental Considerations

·        **Network Infasturcture Tests**: Achieved through the use and testing of network elements such as switches, routers, firewalls, and the resources supporting them, for example (AAA, IPS…).

·        **Application-Based Tests**: The testing of security weaknesses in enterprise applications. It covers things like misconfigurations, input validation issues, injection, and logic errors. The backend database is also included in this test.

·        **Penetration Testing in the Cloud**: Cloud security varies depending on the model used (SaaS, PaaS, IaaS), and both the customer and the provider are responsible. Before performing a penetration test, it is important to clarify the security requirements and agreements. CSPs provide guidelines for security assessments and penetration tests in the cloud environment.

## 1.3 Environmental Considerations

·        **Unknown-Enviromental Test:** The tester is given a small amount of information. Domain names and IP addresses within scope may be given to the attacker. The purpose of this black-box test is to allow the assessment to be made from the perspective of an outside attacker.

·        **Known-Environment Test:** This time the attacker has at least some information about the organization and its internal structure. Network diagrams, IP addresses, configurations, and some user information may be given to the tester. If there is an application, its source code is shared with the tester as part of the test.

·        **Partially-Known Environment Test:** This is a hybrid of the black-box and white-box tests. Testers may be given user information, but not the internal structure of the network.

## 1.4 Surveying Diffrent Standarts and Methologies

·        **MITRE ATT&CK:** A framework created to learn the tactics, techniques, and procedures (TTPs) of attackers.

·        **OWASP WSTG:** A guide developed for web application testing. It covers the high-level stages of web application security testing and goes into more depth on the test methods used.

·        **NIST SP 800-115:** Provides organizations with guidance on planning and conducting information security testing.

·        **OSSTMM:** A guide describing repeatable and consistent security tests.

·        **PTES:** A guide describing attack types and methods, as well as the most up-to-date tools used to carry out the specified attack types.
