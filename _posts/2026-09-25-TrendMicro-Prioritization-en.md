---
categories: [dokumantasyon]
layout: post
lang: en
description: "The Prioritization section of the TrendAI Vision One platform: what the Attack Surface Discovery, Threat and Exposure Management, and Attack Path Prediction pages do."
tool: Trend Micro
logo: "/assets/images/blog_icon/trendmicro.png"
author: nazy
title: TrendAI Vision One Platform - Prioritization
tags: [Trend Micro, Cyber Risk]
order: 20
wide_content: true
permalink: /en/TrendMicro-Prioritization
translation_url: /TrendMicro-Prioritization
---

Continuing with our second part.

## Prioritization

In this section we'll cover the Attack Surface Discovery, Threat and Exposure Management, and Attack Path Prediction pages.

<div class="app-frame">
  <div class="doc-tabs">
    <div class="app-frame-nav app-frame-nav-tabs">
      <p class="app-frame-nav-group">Prioritization</p>
      <button type="button" class="doc-tab-btn app-frame-nav-item active" data-tab="prio-attack-en">Attack Surface Discovery</button>
      <button type="button" class="doc-tab-btn app-frame-nav-item" data-tab="prio-threat-en">Threat and Exposure Management</button>
      <button type="button" class="doc-tab-btn app-frame-nav-item" data-tab="prio-path-en">Attack Path Prediction</button>
    </div>
    <div class="app-frame-content">
      <div class="doc-tab-content">
        <div class="doc-tab-panel active" id="prio-attack-en">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Prioritized Device List</p>
  </div>
  <div class="doc-step-body" markdown="1">

Let's look more closely at the risks we saw in the previous section. Let's start with the Devices tab, but most of what you'll see here also applies to the other categories (Internet-Facing Assets, Accounts, Applications, Cloud Assets). These categories give you a prioritized list, so you see the most critical/important assets first. Assets with a 🌐 icon next to them mean they're accessible from the internet.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/attack-surface-device-list.webp' | relative_url }}" width="2560" height="1260" alt="The Devices tab on the Attack Surface Discovery page showing the prioritized device list">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Device Profile</p>
  </div>
  <div class="doc-step-body" markdown="1">

Clicking a device in the list takes you to its profile. Here you can manage the device's tags, change its criticality, or edit some basic information to assess how important it is to you.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/device-profile.webp' | relative_url }}" width="2560" height="1260" alt="A device's profile page showing Asset Criticality, platform tags, and activity information">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">3</span>
    <p class="doc-step-title">Risk Assessment Page</p>
  </div>
  <div class="doc-step-body" markdown="1">

After the profile, you can check the device's own risk score on its Risk Assessment page. Here you can see what kinds of cyber threats the device is exposed to.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/device-risk-assessment.webp' | relative_url }}" width="2560" height="1260" alt="The Risk Assessment page showing a device's risk score breakdown and list of risk indicators">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">4</span>
    <p class="doc-step-title">Risk Factor Detail</p>
  </div>
  <div class="doc-step-body" markdown="1">

If you click on a threat in the Risk Factor list, you can access more detailed information about it. For example, you can see the CVE it's tied to, the affected operating system, and the risk's criticality level.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/risk-factor-detail.webp' | relative_url }}" width="2560" height="1260" alt="The expanded row of a risk factor showing CVE, operating system, and criticality details">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">5</span>
    <p class="doc-step-title">CVE Detail</p>
  </div>
  <div class="doc-step-body" markdown="1">

To learn more about a CVE, click its name to access its detail page.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/cve-detail.webp' | relative_url }}" width="2560" height="1260" alt="A CVE detail page showing the CVSS score, mitigation options, and recommended updates">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">6</span>
    <p class="doc-step-title">Connections and Internet Exposure</p>
  </div>
  <div class="doc-step-body" markdown="1">

Let's go back to the Risk Assessment page. Here you can check whether the device is accessible from the internet, or see which other devices it's connected to.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/risk-assessment-connections.webp' | relative_url }}" width="2560" height="1260" alt="An expanded risk event showing a potential attack path description and remediation recommendations">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">7</span>
    <p class="doc-step-title">Asset Risk Graph</p>
  </div>
  <div class="doc-step-body" markdown="1">

Another place you can assess risk is the Asset Risk Graph page, next to Risk Assessment. Here you can see in more detail who has connected to this device, from where, and which other devices it's connected to.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/asset-risk-graph.webp' | relative_url }}" width="2560" height="1291" alt="The Asset Risk Graph showing a device's connections to other devices, users, and network components">
</div>

  </div>
</div>

        </div>
        <div class="doc-tab-panel" id="prio-threat-en">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Overall Risk Score Categories</p>
  </div>
  <div class="doc-step-body" markdown="1">

On this page you can review the breakdown of your company's overall risk score by category, and see what you can do to lower your score.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/threat-exposure-overview.webp' | relative_url }}" width="2560" height="1294" alt="The Threat and Exposure Management page showing Cyber Risk Index categories and the Risk Reduction Measures table">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Choosing a Risk Reduction Goal</p>
  </div>
  <div class="doc-step-body" markdown="1">

You can also choose your risk score reduction goal: lower it to the general industry level, focus on the top 10 highest-impact risk factors, or set your own custom goal.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/threat-exposure-goal-selection.webp' | relative_url }}" width="2560" height="1294" alt="The Risk Reduction Goal window with four different goal options">
</div>

  </div>
</div>

        </div>
        <div class="doc-tab-panel" id="prio-path-en">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Attack Paths Overview</p>
  </div>
  <div class="doc-step-body" markdown="1">

The Attack Path page shows potential attack scenarios targeting the assets in your company. It shows, from an attacker's perspective, how they could reach your valuable data. Attack paths are ranked by a score, which is calculated based on two factors:

- **Likelihood:** The probability that attackers would use this path is calculated.
- **Impact:** How critical the consequences would be if this attack occurred is calculated.

Clicking an asset opens a menu on the left where you can see the attack path's details — for example, the attack path score, the entry point's risk events, a description of the attack path, and what you can do about it.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/attack-path-overview.webp' | relative_url }}" width="1920" height="911" alt="The Attack Path Prediction page showing attack paths ranked by score, with a visual map">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Entry Point Risk Events</p>
  </div>
  <div class="doc-step-body" markdown="1">

Clicking on the entry point risk events lets you view, in detail, the vulnerabilities identified as the attack path.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/attack-path-risk-events.webp' | relative_url }}" width="1920" height="911" alt="The Entry Point Risk Events list for an attack path">
</div>

  </div>
</div>

        </div>
      </div>
    </div>
  </div>
</div>
