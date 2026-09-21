---
categories: [blog]
layout: post
lang: en
description: "A short introduction to breach types, APTs, the CIA triad, the NIST Cybersecurity Framework, and the Cyber Kill Chain."
logo: "/assets/images/blog_icon/corporate.png"
author: nazy
title: Corporate Security 101
tags: [Corporate Security, NIST]
permalink: /en/Kurumsal
translation_url: /Kurumsal
---

A short introduction to the fundamentals of corporate cybersecurity, the CIA triad, the NIST Cybersecurity Framework, and the Cyber Kill Chain.

## Terminology

- **Intrusion**: All attempts, successful or unsuccessful.
- **APT (Advanced Persistent Threat)**: Advanced attack organizations.
- **RAT (Remote Access Trojan)**: Malicious remote access software.
- **TTP**: Attack planning and tactics.

## Objectives

- **Confidentiality**: Being accessible only to authorized people. E.g. encryption, access control, identity verification.
- **Integrity**: Information not being altered or tampered with. E.g. hashing, digital signature.
- **Availability**: Timely access to systems or data.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/kurumsal/cia.webp' | relative_url }}" width="800" height="480" alt="Diagram showing the CIA triad (Confidentiality, Integrity, Availability)">
</div>

## NIST

- **NIST**: National Institute of Standards and Technology.
- **CSF**: Cybersecurity Framework.

1. **Identify**: Identifying digital assets.
2. **Protect**: Protective methods.
3. **Detect**: Possible breaches and anomalies.
4. **Respond**: Response to a potential threat.
5. **Recover**: Restoring a compromised system.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/kurumsal/nist.webp' | relative_url }}" width="700" height="420" alt="Diagram showing the five core functions of the NIST Cybersecurity Framework">
</div>

## Maturity Model

1. **Architecture**: The foundations of the cyber infrastructure.
2. **Passive Defense**: Preventive barriers against unauthorized access to systems.
3. **Active Defense**: Proactive and dynamic response to threats.
4. **Intelligence**: Threat intelligence, trying to predict in advance.
5. **Offence**: Attacker detection, counter-attack when necessary.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/kurumsal/olgunluk.webp' | relative_url }}" width="900" height="320" alt="Diagram showing the five levels of the cybersecurity maturity model">
</div>

## Cyber Kill Chain

1. **Reconnaissance**: Information gathering, divided into active and passive.
2. **Weaponization**: Preparing malicious software based on the information gathered.
3. **Delivery**: Delivering the prepared malicious content to the target.
4. **Exploitation**: The attacker gaining unauthorized access by exploiting the weakness.
5. **Installation**: Persisting on the system and advancing the attack.
6. **Command and Control (C2)**: Remotely managing malicious activities.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/kurumsal/cyberkill.webp' | relative_url }}" width="600" height="400" alt="Diagram showing the six stages of the Cyber Kill Chain">
</div>

