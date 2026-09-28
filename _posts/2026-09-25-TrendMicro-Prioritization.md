---
categories: [dokumantasyon]
layout: post
description: "TrendAI Vision One platformunun Prioritization bölümü: Attack Surface Discovery, Threat and Exposure Management ve Attack Path Prediction sayfalarının ne işe yaradığı."
tool: Trend Micro
logo: "/assets/images/blog_icon/trendmicro.png"
author: nazy
title: TrendAI Vision One - Prioritization
tags: [Trend Micro, Cyber Risk]
order: 20
wide_content: true
translation_url: /en/TrendMicro-Prioritization
---

İkinci bölümümüzle devam ediyoruz.

## Prioritization

Bu bölümde Attack Surface Discovery, Threat and Exposure Management ve Attack Path Prediction sayfalarını inceleyeceğiz.

<div class="app-frame">
  <div class="doc-tabs">
    <div class="app-frame-nav app-frame-nav-tabs">
      <p class="app-frame-nav-group" lang="en">Prioritization</p>
      <button type="button" class="doc-tab-btn app-frame-nav-item active" data-tab="prio-attack-tr" lang="en">Attack Surface Discovery</button>
      <button type="button" class="doc-tab-btn app-frame-nav-item" data-tab="prio-threat-tr" lang="en">Threat and Exposure Management</button>
      <button type="button" class="doc-tab-btn app-frame-nav-item" data-tab="prio-path-tr" lang="en">Attack Path Prediction</button>
    </div>
    <div class="app-frame-content">
      <div class="doc-tab-content">
        <div class="doc-tab-panel active" id="prio-attack-tr">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Önceliklendirilmiş Cihaz Listesi</p>
  </div>
  <div class="doc-step-body" markdown="1">

Bir önceki bölümde gördüğümüz riskleri bu bölümde daha detaylı inceleyelim. İlk önce Devices sekmesiyle başlayalım, fakat burada göreceğiniz çoğu detay diğer kategoriler (Internet-Facing Assets, Accounts, Applications, Cloud Assets) için de geçerlidir. Bu kategoriler önceliklendirilmiş bir liste sunar, böylece en kritik/önemli varlıkları ilk başlarda görürsünüz. Yanında 🌐 ikonu olan varlıklar internet üzerinden erişilebilir olduğu anlamına gelir.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/attack-surface-device-list.webp' | relative_url }}" width="2560" height="1260" alt="Attack Surface Discovery sayfasında Devices sekmesi ve önceliklendirilmiş cihaz listesi">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Cihaz Profili</p>
  </div>
  <div class="doc-step-body" markdown="1">

Listede bir cihazın üstüne tıklayarak profiline erişebilirsiniz. Burada cihazın etiketlerini yönetebilir, kritikliğini değiştirebilir veya bazı temel bilgilerini düzenleyerek sizin için önemini değerlendirebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/device-profile.webp' | relative_url }}" width="2560" height="1260" alt="Bir cihazın Asset Criticality, platform etiketleri ve aktivite bilgilerini gösteren profil sayfası">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">3</span>
    <p class="doc-step-title">Risk Assessment Sayfası</p>
  </div>
  <div class="doc-step-body" markdown="1">

Profilden sonra cihazın kendi risk skorunu incelemek için Risk Assessment sayfasına bakabilirsiniz. Burada cihazın ne tür siber tehditlere maruz kaldığını görebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/device-risk-assessment.webp' | relative_url }}" width="2560" height="1260" alt="Bir cihazın risk skoru dağılımını ve risk indikatörleri listesini gösteren Risk Assessment sayfası">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">4</span>
    <p class="doc-step-title">Risk Faktörü Detayı</p>
  </div>
  <div class="doc-step-body" markdown="1">

Risk Factor listesinde incelemek istediğiniz bir tehdidin üstüne tıklarsanız, o tehdit hakkında daha detaylı bilgilere erişebilirsiniz. Örneğin tehdidin bağlı olduğu CVE adını, etkilenen işletim sistemini ve riskin kritiklik seviyesini görebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/risk-factor-detail.webp' | relative_url }}" width="2560" height="1260" alt="Bir risk faktörünün genişletilmiş satırında görülen CVE, işletim sistemi ve kritiklik bilgileri">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">5</span>
    <p class="doc-step-title">CVE Detayı</p>
  </div>
  <div class="doc-step-body" markdown="1">

CVE hakkında daha fazla bilgi almak için CVE ismine tıklayarak detay sayfasına erişebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/cve-detail.webp' | relative_url }}" width="2560" height="1260" alt="CVSS skoru, mitigasyon seçenekleri ve önerilen güncellemeleri gösteren CVE detay sayfası">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">6</span>
    <p class="doc-step-title">Bağlantılar ve İnternet Erişimi</p>
  </div>
  <div class="doc-step-body" markdown="1">

Risk Assessment sayfasına geri dönelim. Burada cihazın internet üzerinden erişilebilir olup olmadığını kontrol edebilir veya başka hangi cihazlarla bağlantıda olduğuna bakabilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/risk-assessment-connections.webp' | relative_url }}" width="2560" height="1260" alt="Genişletilmiş bir risk olayında görülen olası saldırı yolu (potential attack path) açıklaması ve remediation önerileri">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">7</span>
    <p class="doc-step-title">Asset Risk Graph</p>
  </div>
  <div class="doc-step-body" markdown="1">

Riski değerlendirebileceğimiz bir diğer yer, Risk Assessment'ın yanında bulunan Asset Risk Graph sayfası. Bu cihaza kimin, nereden bağlandığını ve başka hangi cihazlarla bağlantılı olduğunu burada daha detaylı görebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/asset-risk-graph.webp' | relative_url }}" width="2560" height="1291" alt="Bir cihazın diğer cihaz, kullanıcı ve ağ bileşenleriyle bağlantılarını gösteren Asset Risk Graph">
</div>

  </div>
</div>

        </div>
        <div class="doc-tab-panel" id="prio-threat-tr">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Genel Risk Skoru Kategorileri</p>
  </div>
  <div class="doc-step-body" markdown="1">

Bu sayfada şirketinizin genel risk skorunun kategorilere göre dağılımını inceleyebilir, skorunuzu düşürmek için yapabileceklerinizi görebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/threat-exposure-overview.webp' | relative_url }}" width="2560" height="1294" alt="Cyber Risk Index kategorileri ve Risk Reduction Measures tablosunu gösteren Threat and Exposure Management sayfası">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Risk Azaltma Hedefi Seçme</p>
  </div>
  <div class="doc-step-body" markdown="1">

Ayrıca risk skorunuzu düşürme amacınızı da seçebilirsiniz: genel endüstri seviyesine indirebilir, en yüksek etkili 10 risk faktörüne odaklanabilir veya kendi özel hedefinizi belirleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/threat-exposure-goal-selection.webp' | relative_url }}" width="2560" height="1294" alt="Risk Reduction Goal penceresinde dört farklı hedef seçeneği">
</div>

  </div>
</div>

        </div>
        <div class="doc-tab-panel" id="prio-path-tr">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Saldırı Yolları Genel Görünümü</p>
  </div>
  <div class="doc-step-body" markdown="1">

Attack Path sayfası, şirketinizdeki varlıklara yönelik potansiyel saldırı senaryolarını gösterir. Saldırganların bakış açısından, değerli verilerinize nasıl erişebileceklerini gösterir. Saldırı yolları bir skora göre sıralanır. Skor şu iki faktöre göre hesaplanır:

- **Gerçekleşme Olasılığı:** Saldırganların bu yolu kullanma olasılığı hesaplanır.
- **Etki:** Bu saldırı gerçekleşirse ne kadar kritik sonuçlar oluşturacağı hesaplanır.

Bir varlığın üstüne tıklayarak solda açılan menüde saldırı yolunun detaylarını görebilirsiniz. Örneğin attack path skorunu, giriş noktasının riskli olaylarını, saldırı yolunun açıklamasını ve önlem olarak yapılabilecekleri bulabilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/attack-path-overview.webp' | relative_url }}" width="1920" height="911" alt="Attack Path Prediction sayfasında skora göre sıralanmış saldırı yolları listesi ve görsel harita">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Giriş Noktası Risk Olayları</p>
  </div>
  <div class="doc-step-body" markdown="1">

Entry point risk events üstüne tıklarsanız, saldırı yolu olarak belirlenen zafiyetleri detaylı şekilde görüntüleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_prioritization/attack-path-risk-events.webp' | relative_url }}" width="1920" height="911" alt="Bir saldırı yoluna ait Entry Point Risk Events listesi">
</div>

  </div>
</div>

        </div>
      </div>
    </div>
  </div>
</div>
