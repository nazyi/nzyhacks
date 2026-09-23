---
categories: [dokumantasyon]
layout: post
lang: en
description: "The Visibility section of the TrendAI Vision One platform: what the Risk Overview, Exposure Overview, Attack Overview, and Security Configuration Overview tabs on the Cyber Risk Overview page do."
tool: Trend Micro
logo: "/assets/images/blog_icon/trendmicro.png"
author: nazy
title: TrendAI Vision One - Visibility
tags: [Trend Micro, Cyber Risk]
order: 10
wide_content: true
permalink: /en/TrendMicro-Vision-Visibility
translation_url: /TrendMicro-Vision-Visibility
---

Hi, in this series I'll try to walk you through Trend Micro's TrendAI Vision One platform.

## Visibility

The first page I want to cover is **Cyber Risk Overview**, found under **Cyber Risk Exposure Management** in the left menu. This page gives you your company's overall cybersecurity score, category-based risk assessments, and a detailed look at the overall situation. There are four tabs at the top of the page — let's go through them one by one.

<div class="app-frame">
  <div class="app-frame-nav">
    <p class="app-frame-nav-group">Cyber Risk Exposure Management</p>
    <p class="app-frame-nav-item active">Cyber Risk Overview</p>
  </div>
  <div class="app-frame-content">
  <div class="doc-tabs">
  <div class="doc-tab-buttons">
    <button type="button" class="doc-tab-btn active" data-tab="tm-risk-en">Risk</button>
    <button type="button" class="doc-tab-btn" data-tab="tm-exposure-en">Exposure</button>
    <button type="button" class="doc-tab-btn" data-tab="tm-attack-en">Attack</button>
    <button type="button" class="doc-tab-btn" data-tab="tm-secconf-en">Config</button>
  </div>
  <div class="doc-tab-content">
    <div class="doc-tab-panel active" id="tm-risk-en" markdown="1">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Comparing Your Overall Score</p>
  </div>
  <div class="doc-step-body" markdown="1">

The chart shows your overall score, and with the **Compare with other orgs** option you can compare your company against other organizations.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/risk-overview-score.webp' | relative_url }}" width="1000" height="176" alt="The Cyber Risk Index chart and the Compare with other orgs option">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Score Change Detail</p>
  </div>
  <div class="doc-step-body" markdown="1">

Hovering over the chart shows the details of why your score went up or down.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/risk-score-detail.webp' | relative_url }}" width="443" height="501" alt="The detail box shown when hovering over the chart, explaining why the score changed">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">3</span>
    <p class="doc-step-title">Security Issues by Category</p>
  </div>
  <div class="doc-step-body" markdown="1">

Below the chart you'll find security issues broken down by category. Click on them to see the details.

<div class="doc-tabs">
  <div class="doc-tab-buttons">
    <button type="button" class="doc-tab-btn cat-tab-btn active" data-tab="cat-devices-en"><span class="cat-icon">🖥️</span> Devices <span class="cat-risk-dot cat-risk-high" title="Risk level: High"></span></button>
    <button type="button" class="doc-tab-btn cat-tab-btn" data-tab="cat-internet-en"><span class="cat-icon">🌐</span> Internet Facing <span class="cat-risk-dot cat-risk-medium" title="Risk level: Medium"></span></button>
    <button type="button" class="doc-tab-btn cat-tab-btn" data-tab="cat-accounts-en"><span class="cat-icon">👤</span> Accounts <span class="cat-risk-dot cat-risk-high" title="Risk level: High"></span></button>
    <button type="button" class="doc-tab-btn cat-tab-btn" data-tab="cat-apps-en"><span class="cat-icon">🧩</span> Applications <span class="cat-risk-dot cat-risk-medium" title="Risk level: Medium"></span></button>
    <button type="button" class="doc-tab-btn cat-tab-btn" data-tab="cat-cloud-en"><span class="cat-icon">☁️</span> Cloud Assets <span class="cat-risk-dot cat-risk-high" title="Risk level: High"></span></button>
  </div>
  <div class="doc-tab-content">
    <div class="doc-tab-panel active" id="cat-devices-en">
      <table>
        <thead><tr><th>Heading</th><th>Description</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>A chart showing your monthly security for this category</td></tr>
          <tr><td>Risk Factors</td><td>Click through to review these in more detail on other pages</td></tr>
          <tr><td>Attack Surface</td><td><strong>Discovered Devices:</strong> TrendAI's level of access to devices<br><strong>Devices Can Be Assessed for Risk:</strong> Risk level of devices at risk<br><strong>Devices with Managed Agents:</strong> Risk level of devices managed by TrendAI</td></tr>
        </tbody>
      </table>
    </div>

    <div class="doc-tab-panel" id="cat-internet-en">
      <table>
        <thead><tr><th>Heading</th><th>Description</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>A chart showing your monthly security for this category</td></tr>
          <tr><td>Risk Factors</td><td>Click through to review these in more detail on other pages</td></tr>
          <tr><td>Attack Surface</td><td><strong>Domains:</strong> Domain addresses found via internet scanning<br><strong>IPs:</strong> IP addresses found via internet scanning</td></tr>
        </tbody>
      </table>
    </div>

    <div class="doc-tab-panel" id="cat-accounts-en">
      <table>
        <thead><tr><th>Heading</th><th>Description</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>A chart showing your monthly security for this category</td></tr>
          <tr><td>Risk Factors</td><td>Click through to review these in more detail on other pages</td></tr>
          <tr><td>Attack Surface</td><td><strong>Domain Accounts:</strong> Number of domain accounts from AD and agents<br><strong>Service Accounts:</strong> Number of service accounts completed by Entra ID/Active Directory</td></tr>
        </tbody>
      </table>
    </div>

    <div class="doc-tab-panel" id="cat-apps-en">
      <table>
        <thead><tr><th>Heading</th><th>Description</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>A chart showing your monthly security for this category</td></tr>
          <tr><td>Risk Factors</td><td>Click through to review these in more detail on other pages</td></tr>
          <tr><td>Attack Surface</td><td><strong>Public Cloud Apps:</strong> Cloud-based applications identified by TrendAI<br><strong>Local Apps:</strong> Local applications discovered by TrendAI<br><strong>Connected SaaS apps:</strong> SaaS applications managed by TrendAI and your company</td></tr>
        </tbody>
      </table>
    </div>

    <div class="doc-tab-panel" id="cat-cloud-en">
      <table>
        <thead><tr><th>Heading</th><th>Description</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>A chart showing your monthly security for this category</td></tr>
          <tr><td>Risk Factors</td><td>Click through to review these in more detail on other pages</td></tr>
          <tr><td>Attack Surface</td><td><strong>Cloud Assets:</strong> Cloud-based assets discovered from cloud-based systems</td></tr>
        </tbody>
      </table>

    </div>
  </div>
</div>

  </div>
</div>

  </div>
    <div class="doc-tab-panel" id="tm-exposure-en" markdown="1">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Factors Affecting Your Score</p>
  </div>
  <div class="doc-step-body" markdown="1">

You can view the factors affecting your score here.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/exposure-overview-factors.webp' | relative_url }}" width="1000" height="492" alt="The Exposure Overview page, with Vulnerabilities and System Configuration as contributing factors">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Vulnerability Assessment Coverage</p>
  </div>
  <div class="doc-step-body" markdown="1">

On the vulnerabilities page you can see the Vulnerability Assessment Coverage.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/exposure-vuln-assessment-scope.webp' | relative_url }}" width="1000" height="492" alt="Vulnerability Assessment Coverage: the percentage of assessed assets">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">3</span>
    <p class="doc-step-title">Detected Vulnerabilities</p>
  </div>
  <div class="doc-step-body" markdown="1">

You can also view the vulnerabilities detected in your company.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/exposure-detected-vulns.webp' | relative_url }}" width="1000" height="492" alt="Detected Vulnerabilities and Mean Time to Patch metrics">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">4</span>
    <p class="doc-step-title">Misconfigured Settings</p>
  </div>
  <div class="doc-step-body" markdown="1">

Going to the system configuration section, you can check for misconfigured settings.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/exposure-misconfigurations.webp' | relative_url }}" width="1000" height="492" alt="Cloud Asset Misconfigurations and the number of Compliance Violations">
</div>

  </div>
</div>

  </div>
    <div class="doc-tab-panel" id="tm-attack-en" markdown="1">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Detected Attacks</p>
  </div>
  <div class="doc-step-body" markdown="1">

Here you can review the attacks detected in your company.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/attack-overview-list.webp' | relative_url }}" width="1000" height="492" alt="The Attack Overview chart and the Attack Phase Overview heat map">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Cyber Threats and Remediation Actions</p>
  </div>
  <div class="doc-step-body" markdown="1">

Below, you can see information about cyber threats, along with the remediation actions available for each attack.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/attack-threat-detail.webp' | relative_url }}" width="1000" height="492" alt="The cyber threats table and the number of available remediation actions for each threat">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">3</span>
    <p class="doc-step-title">Threat Detail and Recommended Actions</p>
  </div>
  <div class="doc-step-body" markdown="1">

If you click on a cyber threat to inspect it, you'll find recommended actions for lowering your overall risk score.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/attack-remediation-actions.webp' | relative_url }}" width="1000" height="492" alt="The Phishing threat detail page and the recommended actions to reduce risk">
</div>

  </div>
</div>

  </div>
    <div class="doc-tab-panel" id="tm-secconf-en" markdown="1">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Security Configuration Summary</p>
  </div>
  <div class="doc-step-body" markdown="1">

Here you can review end-user security configurations, email security, and network security elements.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/security-configuration-overview.webp' | relative_url }}" width="1000" height="492" alt="Security Configuration Overview: risk levels for Endpoint, Email, and Network Security">
</div>

  </div>
</div>

  </div>
  </div>
</div>
  </div>
</div>
