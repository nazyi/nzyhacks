---
categories: [dokumantasyon]
layout: post
description: "TrendAI Vision One platformunun Visibility bölümü: Cyber Risk Overview sayfasındaki Risk Overview, Exposure Overview, Attack Overview ve Security Configuration Overview sekmelerinin ne işe yaradığı."
tool: Trend Micro
logo: "/assets/images/blog_icon/trendmicro.png"
author: nazy
title: TrendAI Vision One - Visibility
tags: [Trend Micro, Cyber Risk]
order: 10
wide_content: true
translation_url: /en/TrendMicro-Vision-Visibility
---

Selam, bu seride Trend Micro'nun TrendAI Vision One platformunu size anlatmaya çalışacağım.

## Visibility

İlk bahsetmek istediğim sayfa, sol menüde **Cyber Risk Exposure Management** altında yer alan **Cyber Risk Overview**. Bu sayfa şirketinizin genel siber güvenlik skorunu, kategori bazlı tehlike değerlendirmelerini ve genel duruma dair detaylı bir bakış sunar. Sayfanın üstünde dört sekme bulunur, sırayla bakalım.

<div class="app-frame">
  <div class="app-frame-nav">
    <p class="app-frame-nav-group" lang="en">Cyber Risk Exposure Management</p>
    <p class="app-frame-nav-item active" lang="en">Cyber Risk Overview</p>
  </div>
  <div class="app-frame-content">
  <div class="doc-tabs">
  <div class="doc-tab-buttons">
    <button type="button" class="doc-tab-btn active" data-tab="tm-risk-tr">Risk</button>
    <button type="button" class="doc-tab-btn" data-tab="tm-exposure-tr">Exposure</button>
    <button type="button" class="doc-tab-btn" data-tab="tm-attack-tr">Attack</button>
    <button type="button" class="doc-tab-btn" data-tab="tm-secconf-tr">Config</button>
  </div>
  <div class="doc-tab-content">
    <div class="doc-tab-panel active" id="tm-risk-tr" markdown="1">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Genel Skor Karşılaştırması</p>
  </div>
  <div class="doc-step-body" markdown="1">

Grafikte genel skorunuzu görebilmekle beraber **Compare with other orgs** seçeneği ile şirketinizi diğer kurumlarla karşılaştırabilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/risk-overview-score.webp' | relative_url }}" width="1000" height="176" alt="Cyber Risk Index grafiği ve Compare with other orgs seçeneği">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Skor Değişim Detayı</p>
  </div>
  <div class="doc-step-body" markdown="1">

Grafiğin üstüne gelerek skorunuzun neden arttığını/azaldığını detaylarıyla görebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/risk-score-detail.webp' | relative_url }}" width="443" height="501" alt="Grafik üzerine gelince çıkan, skorun neden değiştiğini gösteren detay kutusu">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">3</span>
    <p class="doc-step-title">Kategorilere Ayrılmış Güvenlik Sorunları</p>
  </div>
  <div class="doc-step-body" markdown="1">

Grafiğin aşağısında kategorilere ayrılmış güvenlik problemlerini bulabilirsiniz. Üzerlerine tıklayarak detayları inceleyebilirsiniz.

<div class="doc-tabs">
  <div class="doc-tab-buttons">
    <button type="button" class="doc-tab-btn cat-tab-btn active" data-tab="cat-devices-tr"><span class="cat-icon">🖥️</span> Devices <span class="cat-risk-dot cat-risk-high" title="Risk level: High"></span></button>
    <button type="button" class="doc-tab-btn cat-tab-btn" data-tab="cat-internet-tr"><span class="cat-icon">🌐</span> Internet Facing <span class="cat-risk-dot cat-risk-medium" title="Risk level: Medium"></span></button>
    <button type="button" class="doc-tab-btn cat-tab-btn" data-tab="cat-accounts-tr"><span class="cat-icon">👤</span> Accounts <span class="cat-risk-dot cat-risk-high" title="Risk level: High"></span></button>
    <button type="button" class="doc-tab-btn cat-tab-btn" data-tab="cat-apps-tr"><span class="cat-icon">🧩</span> Applications <span class="cat-risk-dot cat-risk-medium" title="Risk level: Medium"></span></button>
    <button type="button" class="doc-tab-btn cat-tab-btn" data-tab="cat-cloud-tr"><span class="cat-icon">☁️</span> Cloud Assets <span class="cat-risk-dot cat-risk-high" title="Risk level: High"></span></button>
  </div>
  <div class="doc-tab-content">
    <div class="doc-tab-panel active" id="cat-devices-tr">
      <table>
        <thead><tr><th>Başlık</th><th>Açıklama</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>İlgili başlık ile aylık güvenliğinizi gösteren grafik</td></tr>
          <tr><td>Risk Factors</td><td>Üstüne basarak diğer sayfalarda daha detaylı inceleyebilirsiniz</td></tr>
          <tr><td>Attack Surface</td><td><strong>Discovered Devices:</strong> TrendAI'ın cihazlara olan erişim düzeyi<br><strong>Devices Can Be Assessed for Risk:</strong> Riskte olan cihazların risk düzeyi<br><strong>Devices with Managed Agents:</strong> TrendAI tarafından yönetilen cihazların risk düzeyi</td></tr>
        </tbody>
      </table>
    </div>

    <div class="doc-tab-panel" id="cat-internet-tr">
      <table>
        <thead><tr><th>Başlık</th><th>Açıklama</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>İlgili başlık ile aylık güvenliğinizi gösteren grafik</td></tr>
          <tr><td>Risk Factors</td><td>Üstüne basarak diğer sayfalarda daha detaylı inceleyebilirsiniz</td></tr>
          <tr><td>Attack Surface</td><td><strong>Domains:</strong> Internet taraması ile bulunmuş domain adresleri<br><strong>IPs:</strong> Internet taraması ile bulunmuş IP adresleri</td></tr>
        </tbody>
      </table>
    </div>

    <div class="doc-tab-panel" id="cat-accounts-tr">
      <table>
        <thead><tr><th>Başlık</th><th>Açıklama</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>İlgili başlık ile aylık güvenliğinizi gösteren grafik</td></tr>
          <tr><td>Risk Factors</td><td>Üstüne basarak diğer sayfalarda daha detaylı inceleyebilirsiniz</td></tr>
          <tr><td>Attack Surface</td><td><strong>Domain Accounts:</strong> AD ve ajanlardan gelen domain hesap sayısı<br><strong>Service Accounts:</strong> Entra ID/Active Directory tarafından tamamlanan servis hesap sayısı</td></tr>
        </tbody>
      </table>
    </div>

    <div class="doc-tab-panel" id="cat-apps-tr">
      <table>
        <thead><tr><th>Başlık</th><th>Açıklama</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>İlgili başlık ile aylık güvenliğinizi gösteren grafik</td></tr>
          <tr><td>Risk Factors</td><td>Üstüne basarak diğer sayfalarda daha detaylı inceleyebilirsiniz</td></tr>
          <tr><td>Attack Surface</td><td><strong>Public Cloud Apps:</strong> TrendAI tarafından tanımlanan bulut tabanlı uygulamalar<br><strong>Local Apps:</strong> TrendAI tarafından keşfedilen yerel uygulamalar<br><strong>Connected SaaS apps:</strong> TrendAI ve şirketiniz tarafından yönetilen SaaS uygulamaları</td></tr>
        </tbody>
      </table>
    </div>

    <div class="doc-tab-panel" id="cat-cloud-tr">
      <table>
        <thead><tr><th>Başlık</th><th>Açıklama</th></tr></thead>
        <tbody>
          <tr><td>Risk Summary</td><td>İlgili başlık ile aylık güvenliğinizi gösteren grafik</td></tr>
          <tr><td>Risk Factors</td><td>Üstüne basarak diğer sayfalarda daha detaylı inceleyebilirsiniz</td></tr>
          <tr><td>Attack Surface</td><td><strong>Cloud Assets:</strong> Bulut tabanlı sistemlerden keşfedilen bulut tabanlı varlıklar</td></tr>
        </tbody>
      </table>

    </div>
  </div>
</div>

  </div>
</div>

  </div>
    <div class="doc-tab-panel" id="tm-exposure-tr" markdown="1">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Skoru Etkileyen Faktörler</p>
  </div>
  <div class="doc-step-body" markdown="1">

Skorunuzu etkileyen faktörleri buradan görüntüleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/exposure-overview-factors.webp' | relative_url }}" width="1000" height="492" alt="Exposure Overview sayfası, Vulnerabilities ve System Configuration katkı faktörleri">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Güvenlik Açıkları Değerlendirme Kapsamı</p>
  </div>
  <div class="doc-step-body" markdown="1">

Güvenlik açıkları sayfasında Güvenlik Açıkları Değerlendirme Kapsamını görebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/exposure-vuln-assessment-scope.webp' | relative_url }}" width="1000" height="492" alt="Vulnerability Assessment Coverage: değerlendirilen varlıkların kapsam yüzdesi">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">3</span>
    <p class="doc-step-title">Tespit Edilen Güvenlik Açıkları</p>
  </div>
  <div class="doc-step-body" markdown="1">

Aynı zamanda şirkette tespit edilen güvenlik açıklarını da görüntüleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/exposure-detected-vulns.webp' | relative_url }}" width="1000" height="492" alt="Detected Vulnerabilities ve Mean Time to Patch metrikleri">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">4</span>
    <p class="doc-step-title">Yanlış Yapılandırılmış Ayarlar</p>
  </div>
  <div class="doc-step-body" markdown="1">

Sistem ayarlarına gelerek yanlış yapılandırılmış ayarlara bakabilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/exposure-misconfigurations.webp' | relative_url }}" width="1000" height="492" alt="Cloud Asset Misconfigurations ve Compliance Violations sayısı">
</div>

  </div>
</div>

  </div>
    <div class="doc-tab-panel" id="tm-attack-tr" markdown="1">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Tespit Edilen Saldırılar</p>
  </div>
  <div class="doc-step-body" markdown="1">

Burada şirketinizde tespit edilen saldırıları inceleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/attack-overview-list.webp' | relative_url }}" width="1000" height="492" alt="Attack Overview grafiği ve Attack Phase Overview ısı haritası">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">2</span>
    <p class="doc-step-title">Siber Tehditler ve İyileştirme Aksiyonları</p>
  </div>
  <div class="doc-step-body" markdown="1">

Aşağıda siber tehditler hakkında bilgi ve bu saldırılar için yapabileceğiniz iyileştirme aksiyonlarını görebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/attack-threat-detail.webp' | relative_url }}" width="1000" height="492" alt="Cyber threats tablosu ve her tehdit için mevcut Remediation Action sayısı">
</div>

  </div>
</div>

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">3</span>
    <p class="doc-step-title">Tehdit Detayı ve Aksiyon Önerileri</p>
  </div>
  <div class="doc-step-body" markdown="1">

Bir siber tehdide tıklayıp incelediğinizde, genel risk skorunuzu nasıl düşürebileceğinize dair aksiyon önerileri karşınıza çıkar.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/attack-remediation-actions.webp' | relative_url }}" width="1000" height="492" alt="Phishing tehdidi detay sayfası ve risk azaltmak için önerilen aksiyonlar">
</div>

  </div>
</div>

  </div>
    <div class="doc-tab-panel" id="tm-secconf-tr" markdown="1">

<div class="doc-step">
  <div class="doc-step-header">
    <span class="doc-step-number">1</span>
    <p class="doc-step-title">Güvenlik Yapılandırma Özeti</p>
  </div>
  <div class="doc-step-body" markdown="1">

Burada son kullanıcı güvenlik yapılandırmalarını, e-posta güvenliğini ve ağ güvenliği unsurlarını inceleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/trendmicro_vision1/security-configuration-overview.webp' | relative_url }}" width="1000" height="492" alt="Security Configuration Overview: Endpoint, Email ve Network Security risk seviyeleri">
</div>

  </div>
</div>

  </div>
  </div>
</div>
  </div>
</div>
