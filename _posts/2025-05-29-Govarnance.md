---
categories: [blog]
layout: post
description: "Veri sınıflandırma, GDPR gibi regülasyonlar, yaygın siber saldırı türleri ve Bilgi Güvenliği Yönetim Sistemi'nin (BGYS) temellerine kısa bir bakış."
logo: "/assets/images/blog_icon/govarnance.png"
author: nazy
title: Bilgi Yönetişimi 202 
tags: [Bilgi Yönetişimi, GDPR]
translation_url: /en/Govarnance
---

Bilgi yönetişiminin temel kavramlarına, veri koruma regülasyonlarına ve en yaygın siber saldırı türlerine kısa bir bakış.

## Terminoloji

- **Veri**: Anlamlı işlenmemiş parça.
- **Bilgi**: İşlenmiş veri.
- **Bilgi Sistem ve Yönetim**: Altyapı ve servisler.

## Regülasyon

_GDPR (General Data Protection Regulation)_, Avrupa Birliği tarafından kişisel verilerin korunmasına yönelik hazırlanmış bir veri güvenliği regülasyonudur. Bireylerin kişisel verilerinin işlenmesi, saklanması ve paylaşılması süreçlerinde gizlilik haklarını korumayı amaçlar. GDPR, yalnızca AB sınırları içerisindeki şirketleri değil, AB vatandaşlarının verilerini işleyen tüm dünya çapındaki kuruluşları da kapsar. Türkiye'deki KVKK gibidir.

_NIS (Network and Information Systems) Direktifi_, ağ ve bilgi sistemlerinin güvenliğini artırmayı amaçlayan bir siber güvenlik regülasyonudur. Kritik altyapıların (enerji, ulaşım, sağlık, finans gibi) ve dijital hizmet sağlayıcılarının siber saldırılara karşı güvenliğini sağlamak için gerekli önlemleri almasını zorunlu kılar.

_PCI DSS (Payment Card Industry Data Security Standard)_, kartlı ödeme sistemlerinde kullanılan **kredi kartı bilgilerini korumak** amacıyla oluşturulmuş küresel bir güvenlik standardıdır. Visa, Mastercard, American Express gibi kart sağlayıcıları tarafından geliştirilmiştir. Bu standart, kart sahibi bilgilerini işleyen, depolayan veya ileten tüm kuruluşların belirli güvenlik önlemlerine uymasını zorunlu kılar.

## Bilgi Türleri

- **Çok Gizli**: Banka müşterilerinin kart bilgileri.
- **Gizli**: Sızarsa itibar zedelenmesi.
- **Hizmete Özel**: Şirkette belirli kişilere açık.
- **Herkese Açık**: Kamuya açık bilgiler.

### Kişisel Veri Türleri

- **Kişisel Veri**: Kimliği belirten her türlü veri. Örn; TC, ad soyad…
- **Özel Nitelikli**: Irk, köken, mezhep, din…

## Siber Ataklar

En yaygın saldırı türleri ve kısa tanımları:

{% include flip-cards.html id="gov-attacks-tr" items=site.data.gov_attacks hint="14 saldırı türü — kartlara tıklayıp tanımlarını gör." %}

## BGYS (Bilgi Güvenliği Yönetim Sistemi) Adımları

1. Planla
2. Uygula
3. Kontrol Et
4. Önlem Al
