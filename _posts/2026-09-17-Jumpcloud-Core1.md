---
categories: [dokumantasyon]
layout: post
description: "JumpCloud University Core kursunun ilk dersi: Admin Console ve User Portal arayüzleri, organizasyon ayarları, admin rolleri/izinleri ve önerilen güvenlik/şifre politikaları."
logo: "/assets/images/blog_icon/jumpcloud.png"
author: nazy
title: JumpCloud Core 1 - Admin Ayarları
tags: [JumpCloud, Admin Console]
order: 1
translation_url: /en/Jumpcloud-Core1
---

Selam, bu seride JumpCloud University'nin Core kursunun derslerini sırasıyla işlemeye çalışacağım.

İlk kurs içeriğimiz Adminlik ayarları.

JumpCloud'da iki ana UI sayfası var. Birincisi IT adminlerinin kullandığı Admin Console, diğeri ise kullanıcıların genel arayüzü olan User Portal.

Admin Console'da çeşitli ayarlamaları yapabilirsiniz. Örneğin; kullanıcı ve cihaz yönetimi, güvenlik yönetimi, organizasyon ayarları ve hesap bilgileri vb.

## Org Ayarları

- **Settings > Organization Profile**: Buradan şirket isminizi, olası bir durumda ulaşılabilecek mail adresini ve şirketin logosu gibi özellikleri yönetebilir ve değiştirebilirsiniz. Aynı zamanda kullanıcıların User Portal'ı tarafındaki yetkisini veya portalın açık durma süresini de yönetebilirsiniz.
- **Settings > Customize Email**: Buradan hazır olan mail taslağınızı oluşturup değiştirebilirsiniz. Örneğin kullanıcı hesabını kilitleyince JumpCloud tarafından atılacak maili düzenleyebilirsiniz.

Şirketinizin şifre ayarlarını 2 seçenek ile düzenleyebilirsiniz:

1. **Settings > Security**: Güvenlik ayarlarından şifre zorluğunu, kompleksliğini veya hesap kilitlenmesini ayarlayabilirsiniz.
2. **Security > Password Policies**: Yeni bir politika oluşturarak, politikayı etkilemesini istediğiniz kullanıcı grubuna bağlayabilirsiniz. Eğer kullanıcı birçok kullanıcı grubunda ise, hangi grubun şifre politikasının uygulanması gerektiğini buradan yönetebilirsiniz.

## Admin Yönetimi

**Settings > Administrators**

Konsola admin eklemek için 2 yol tercih edebilirsiniz:

1. "+ Admin" butonuna tıklayıp halihazırdaki bir kullanıcıya adminlik yetkisi verebilirsiniz.
2. "+ Admin" butonuna tıklayıp "yeni" seçeneğini seçerseniz yeni bir admin hesabı oluşturursunuz.

## Rol İzinleri

- **Administrator with Billing**: Super admin diye de adlandırılır. Bütün yetkilere sahiptir; MTP (Multi-Tenant Portal) portalına erişebilir, faturalandırmayı düzenleyebilir ve API anahtarı aktive edebilir.
- **Administrator**: API anahtarı, MTP ve faturalandırma harici her şeyi yapabilir.
- **Manager**: Kullanıcıları, cihazları ve grupları yönetebilir.
- **Command Runner**: Sadece komut çalıştırabilir.
- **Command Runner with Billing**: Komut çalıştırabilme yanında faturalandırmayı da güncelleyebilir.
- **Help Desk**: Kullanıcıları oluşturabilir, silebilir veya resetleyebilir.
- **Billing Only**: Yetkileri sadece okuma ile sınırlıdır. Ödeme ile ilgili bilgileri görebilirler.
- **Read Only**: Bu yetkili adminler sadece okuyabilirler.

## Notlar

- Yeni şifre, eski 4 şifreden farklı olsun.
- Başarısız girilme sınırını 6 ile sınırlayın.
- Şifre uzunluğunu 8-12 haneli yapın.
- Oturum, 8 saat inaktiflik sonrasında kilitlensin.
- Şifre ömrünü 90 gün olarak belirleyin.
- MFA doğrulamasını açın.
- Adminlik yetkilerini kısıtlayın, rolleri doğru verin.
