---
categories: [modul]
layout: post
lang: en
description: "This is the second module of the Cisco Ethical Hacker course. It emphasizes why the planning and scoping stages are critical in the penetration testing process. It also details how to act within the framework of regulatory compliance, legal responsibilities, and ethical principles."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Module 2
tags: [Cisco, Planning and Scoping]
order: 2
permalink: /en/Cisco_Module2
translation_url: /Cisco_Module2
---

# Cisco Ethical Hacker

<h2> Module 2: Planning and Scoping a Penetration Testing Assesment </h2>

## 2.1 Regulatory Compliance Considerations

**PCI DSS**: Aims to protect credit card and other digital payments.

**HIPAA:** Aims to protect people's health information.

**FedRAMP:** Aims to ensure the security of cloud services.

### 2.1.1 Regulations in the Financial Sector

GLBA is a law that controls how financial institutions handle individuals' private information, and it applies to all financial institutions, large and small.

### 2.1.2 Regulations in the Healthcare Sector

HIPAA focuses on electronically protected health information. The HIPAA security rules apply to covered entities and business associates.

·        **Healthcare Provider**: Defines the people or institutions that provide treatment.

·        **Health Plan:** Defines the insurance entities or government health plans that cover treatment.

·        **Healthcare Clearinghouse:** Defines those that convert non-standard health information into a standard format.

·        **Business Associates:** Defines the parties that transmit, access, or hold a person's information while they receive a service.

### 2.1.3 Payment Card Industry Data Security Standard (PCI DSS)

In order to protect cardholders' personal information from misuse and minimize losses in the payment card channel, the major payment card brands established and developed PCI DSS.

PCI DSS applies to all organizations that process or store users' card information.

To perform a pentest in the PCI industry, you need to know some key terms:

·        **Acquirer:** The institution, referred to as the acquiring bank, that accepts payment cards.

·        **ASV (Approved Scanning Vendor):** An organization approved by the PCI SSC to carry out external vulnerability scans.

·        **Merchant:** Merchants or individuals who accept card payments in exchange for a product or service.

·        **PAN:** A 19-digit card number

·        **Payment Brand:** Card brands such as Visa and MasterCard

·        **PCI Forensic Investigator (PFI):** Certified individuals who investigate incidents involving card information.

·        **Qualified Security Assessor (QSA):** Individuals certified to carry out PCI DSS compliance assessments.

·        **Service Provider:** Companies that are not a card brand but process cardholder information and provide services.

PAN information is expected to be stored in an unreadable, i.e., encrypted, format. The Luhn algorithm is used to validate credit card numbers, IMEI numbers, and various other identification numbers.

### 2.1.4 Key Technical Elements in Regulations You Should Consider

Most regulations focus on certain core elements, and a penetration tester should pay attention to these during the assessment process.

·        **Data Isolation**: A fully isolated network should be applied to the systems involved in card payment transactions.

·        **Password Management:** Regulations set certain requirements for strong passwords. These include password length, complexity, or multi-factor authentication.

·        **Key Management:** A key plays a role in matters such as where it will be applied within an encryption algorithm and in what order it will run. The process of protecting the key is called key management.

### 2.1.5 Legal Concepts

There are certain legal concepts to know before carrying out a penetration test.

·        **Service-level Agreement**: An SLA is an agreement about service quality that defines the rights and responsibilities of both you and the customer's side.

·        **Confidentiality:** You need to control who can access the information. After the penetration test, you must delete the information you found from your own system.

·        **Statement of Work:** A document that specifies in detail the activities to be carried out during a penetration testing engagement. For example, the engagement dates, engagement location, engagement scope, and payment schedule, etc.

·        **Master Service Agreement:** Establishing a framework to negotiate work with the customer more quickly and easily.

·        **Non-Disclosure Agreement (NDA):** A confidentiality agreement made between a penetration tester and the organization that hired them.

### 2.1.6 Contracts

A contract is a document that specifies all the details of the test, the work to be done, and the payment terms. It should be quite specific, clear, and clean.

### 2.1.7 Disclaimers

A document stating that no warranty is given against certain situations that may arise during or before the test.

## 2.2 Explaining the Importance of Scoping and Organizational or Customer Requirements

### 2.2.1 Rules of Engagement

Determines the conditions under which penetration tests will be carried out. It includes information such as the IP addresses to be tested, the time the test will be conducted, or the domain addresses included in the test.

### 2.2.2 Target Lists and In-Scope Assets

Scoping is one of the most important elements of a pentest. The devices to be tested, the IP addresses of the assets, or the programming interfaces — i.e., APIs — fall within this scope. Information about API documentation types is given below. API documentation is a document that describes rules such as which endpoint a response goes to and which endpoint a response comes from behind the scenes of the application. It should not be publicly accessible. An attacker can read the documentation and plan an attack accordingly.

·        **SOAP:** Uses the XML format; there are XSD files that define what the messages will look like.

·        **Swagger**: A structured document that describes how APIs work. Used for RESTful APIs.

·        **WDSL**: An XML-based language used to document the functionality of web services. Used for the older SOAP API type. It clearly defines how to interact with a web service, which methods (functions) will be used, which parameters are required, and how the web service will respond.

·        **GraphQl:** A query language for APIs, and a structure used to determine how data is fetched, updated, or deleted.

·        **WADL:** An XML-based language used to describe web applications.

**WADL vs WSDL?**

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule2/wadl.jpg' | relative_url }}" width="770" height="340" alt="Table comparing the WADL and WSDL API documentation types">
</div>

Some of the other resources used for pentesting are given below.

·        **Software Development Kit**: A collection of tools used to interact with an operating system, software framework, or hardware.

·        **Source Code Acces**: Being granted permission to access the application's source code.

·        **Example of Application Request**: Some web-based applications, such as OWASP ZAP or Burp Suite, can be used to access content.

·        **System and Network** **Architectural Diagrams**: The architecture of the internal structure of the system and network.

## 2.3 Demonstrating an Ethical Hacking Mindset by Maintaining Professionalism and Integrity

### 2.3.1 Overview

There are many scenarios in which pentesters must maintain their professionalism and integrity.

·        **Background Checks of Penetration Testing Teams**: The contracted firm may run a background check to be able to trust the pentesters. It wants to be able to trust the people who will see its information.

·        **Adherence to The Specific Scope of Engagement**: The list of systems that are permitted to be tested is called the "allow list," and the list of systems that must not be tested is called the "disallow list."

·        **Identification of Criminal Activity and İmmediate Reporting of Breaches/Criminal Activities**: Sometimes during a test you find that a real hacker has already compromised the customer's system before you. You must report such activity immediately.

·        **Limiting the Use of Tools to A Particular Engagement**: Since it could crash the system, customers may request that certain tools not be used.

·        **Limiting İnvasiveness Based on Scope**: The information obtained from the systems, the vulnerability scan outputs, and how to exploit them based on these outputs can be provided with the help of certain tools. However, you must configure the aggressiveness of these tools so that they don't damage the customer's system.

·        **Confidentiality of Data/İnformation**: The information you find while testing must remain strictly confidential and must not be shared with anyone.

·        **Risk to the Professional**: If you don't comply with the terms of the agreement, you may face criminal charges or fines.
