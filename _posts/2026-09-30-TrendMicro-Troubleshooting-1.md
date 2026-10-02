---
categories: [dokumantasyon]
layout: post
description: "Trend Micro'nun network extension'ı ile eski bir Bitdefender network extension'ının çakışmasından kaynaklanan System Extension (20117) hatası ve SIP nedeniyle systemextensionsctl uninstall'ın neden çalışmadığı."
tool: Trend Micro
doc_type: troubleshooting
logo: "/assets/images/blog_icon/trendmicro.png"
author: nazy
title: Trend Micro Troubleshooting Part 1 - System Extension (20117) Error
tags: [Trend Micro, Troubleshooting]
order: 40
wide_content: true
translation_url: /en/TrendMicro-Troubleshooting-1
---

## Genel Bakış

Eski bir Bitdefender network extension'ı, Trend Micro'nun network extension'ıyla çakışarak System Extension (20117) hatasına sebep olabilir. Eski Bitdefender'ı deaktive edip cihazı yeniden başlatmak sorunu çözer.

## Cihazda Kontrol

Cihazda iki yerde Bitdefender bileşenlerinin aktif olup olmadığı kontrol edilmelidir:

- **System Settings > Network > Filters** — Bitdefender DCI filtreleri aktif olmamalı.
- **System Settings > General > Login Items & Extensions > Network Extensions** — `dci-net-ext` aktif olmamalı.

## Uzaktan Kontrol

Bitdefender'ın aktif olup olmadığını kontrol edebilirsiniz:

<div class="code-window">
<br>
<span class="highlight">%</span> systemextensionsctl list
</div>

Eğer komutun çıktısında şöyle bir satır varsa, Bitdefender açık ve çalışmaya devam ediyor demektir:

<div class="code-window">
<br>
com.bitdefender.cst.net.dci.dci-network-extension (7.21.53.200097/7.21.53.200097) dci-net-ext [activated enabled]
</div>

## Neden systemextensionsctl uninstall Yapamıyoruz?

Normal bir Mac'te `systemextensionsctl uninstall <teamID> <bundleID>` komutu SIP (System Integrity Protection) tarafından engellenir:

<div class="code-window">
<br>
At this time, this tool cannot be used if System Integrity Protection is enabled.
</div>

SIP, macOS'ta yerleşik olan ve root kullanıcısının bile korunan sistem dosyalarını değiştirmesine engel olan bir güvenlik mekanizmasıdır.

SIP'in hedef cihazda açık olup olmadığını kontrol edebilirsiniz:

<div class="code-window">
<br>
<span class="highlight">%</span> csrutil status
</div>
