---
categories: [dokumantasyon]
layout: post
description: "TrendAI Vision One platformunun Mitigation bölümü: Workflow and Automation sekmesindeki Security Playbooks sayfasının ne işe yaradığı."
tool: Trend Micro
logo: "/assets/images/blog_icon/trendmicro.png"
author: nazy
title: TrendAI Vision One Platform - Mitigation
tags: [Trend Micro, Cyber Risk]
order: 30
wide_content: true
translation_url: /en/TrendMicro-Mitigation
---

Üçüncü bölümümüzle devam ediyoruz.

## Mitigation

Workflow and Automation sekmesindeki **Security Playbooks** kısmına bakalım.

<div class="app-frame">
  <div class="app-frame-nav">
    <p class="app-frame-nav-group" lang="en">Workflow and Automation</p>
    <p class="app-frame-nav-item active" lang="en">Security Playbooks</p>
  </div>
  <div class="app-frame-content">
  <div class="doc-tab-content">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Security Playbooks Sayfası</p>
  </div>
  <div class="doc-step-body" markdown="1">

Bu sayfada birçok aksiyonu otomatikleştirip iş yükünüzü azaltabilirsiniz. Sıfırdan veya hazır taslakları kullanarak bir otomasyon oluşturabilir, otomasyonun tipine göre ne zaman tetiklenmesi gerektiğini periyodik, manuel veya otomatik şekilde ayarlayabilirsiniz. Örnek olarak oluşturulmuş "Leaked account" playbook'una bakalım.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_mitigation/security-playbooks-list.webp' | relative_url }}" width="2560" height="1292" alt="Security Playbooks sayfasında oluşturulmuş playbook listesi">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Leaked Account Playbook'u</p>
  </div>
  <div class="doc-step-body" markdown="1">

Buradan tetiklenmeyi ayarlayabilirsiniz. Bu senaryoda örnek olarak görev saat başı çalışacaktır. Görevin amacı sızdırılmış hesapların teşhisini yapıp bulunan hesapları görev dışına almaktır.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_mitigation/leaked-account-playbook-flow.webp' | relative_url }}" width="2560" height="860" alt="Leaked account playbook'unun Trigger, Target ve Action akış şeması">
</div>

Bu playbook çalıştığında neler olduğunu adım adım görebilirsiniz:

{% include flow-steps.html data=site.data.playbook_flow %}

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">3</span>
    <p class="doc-step-title">Hazır Taslaklar</p>
  </div>
  <div class="doc-step-body" markdown="1">

Yapılacak görevleri TrendAI platformunun kendisinin sağladığı hazır taslakları kullanabilir ya da kendiniz şirketinizin ihtiyaçları doğrultusunda görevleri oluşturabilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_mitigation/playbook-templates.webp' | relative_url }}" width="2560" height="1292" alt="Yeni bir playbook oluşturmak için seçilebilecek hazır taslak listesi">
</div>

  </div>
</div>

  </div>
  </div>
</div>
