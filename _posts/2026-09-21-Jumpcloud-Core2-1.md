---
categories: [dokumantasyon]
layout: post
description: "JumpCloud University Core kursunun ikinci dersinin ilk bölümü: kullanıcı oluşturma/içe aktarma yöntemleri, kullanıcı durumları, şifre durumları ve kullanıcı adı/yerel hesap eşleştirmesi."
tool: JumpCloud
logo: "/assets/images/blog_icon/jumpcloud.png"
author: nazy
title: JumpCloud Core 2.1 - Kullanıcı Oluşturma
tags: [JumpCloud, Identity Management]
order: 2
translation_url: /en/Jumpcloud-Core2-1
---

JumpCloud Core kursunun ikinci dersi kullanıcı oluşturma ve içe aktarma ile devam ediyor.

## Kullanıcı Ekleme Hazırlığı

**Identity Management > Users**

Kullanıcı eklemek için farklı metodlar kullanabiliriz. **+ Users** butonuna basınca çıkan yöntemleri inceleyelim:

- **Manuel**: El ile manuel kullanıcı ekleyebilirsiniz.
- **Import via CSV**: CSV dosyasından kullanıcıları içe aktarabilirsiniz.
- **Via API**: JumpCloud REST API desteği sağlayarak kullanıcı ekleyebilirsiniz.
- **Via External Apps**: Google, Microsoft 365 veya çeşitli HR uygulamaları desteklenerek kullanıcı ekleyebilirsiniz.

### Kullanıcı Durumları

- **Staged**: Kullanıcı işe alındığında hesabını aktive etmeden önceki durumdur.
- **Active**: Aktivasyon mailinden sonra kullanıcı hesabını aktive ettikten sonraki durumdur.
- **Suspended**: Kullanıcının hesabının askıya alındığı durumdur. Kullanıcının hiçbir yetkisi yoktur.

> İşe alımlarda kullanıcının varsayılan durumunu **User > Settings** kısmından düzenleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/users-list.webp' | relative_url }}" width="1000" height="416" alt="JumpCloud Users sayfasında kullanıcı listesi, durum sekmeleri ve şifre/MFA sütunları">
</div>

### Kullanıcı Durumlarını Yönetme

Kullanıcının durumunu değiştirebileceğiniz birkaç seçenek var:

- Yeni işe girmiş kullanıcının varsayılan hesap durumunu staged veya active yapabilirsiniz.
- Kullanıcıyı active hale getirmeyi ya zamanlayabilirsiniz ya da manuel olarak elinizle yapabilirsiniz.
- Aynı şekilde hesabı askıya almak için de zamanlayabilir ya da manuel olarak halledebilirsiniz.

{% include state-diagram.html id="jc-user-states-tr" states=site.data.jc_user_states placeholder="Bir duruma tıklayarak tanımını gör." %}

### Şifre Durumu

- **Pending**: Kullanıcı mailine gönderilen adımları tamamlamalıdır.
- **Active**: Kullanıcı JumpCloud hesabını rahatça kullanabilir.
- **Expired**: Eğer kullanıcı hala mail hesabına ulaşabiliyorsa, şifre yenileme linki mail yoluyla iletilebilir.
- **Lock Out**: Eğer kullanıcı mail adresine ulaşabiliyorsa, şifre sıfırlama linki mail hesabına gönderilebilir.
- **Federated**: Üçüncü parti şifre uygulaması kullanılıyor demektir.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/password-status.webp' | relative_url }}" width="1000" height="598" alt="Users sayfasında Active filtresiyle listelenen kullanıcılar ve Password Status sütunu">
</div>

### Kullanıcı Adı Kurallarını Belirleme

Kullanıcıları doğru isimlendirmenin önemli bir rolü var. Eğer şirketinizde birden fazla IdP kullanılıyorsa ya da birçok uygulamadan kullanıcı içe aktarılıyorsa, düzeni sağlamak için kullanıcı isimlendirmesini tek bir şekilde yapmaya dikkat etmelisiniz.

### Kullanıcı Adı vs. Yerel Kullanıcı Hesabı

Kullanıcı adı ve yerel kullanıcı hesabı, kullanıcıları cihaza bağlamada önemli rolleri olan iki farklı kavramdır.

Diyelim ki, halihazırda cihazında hesabı olan ve bu hesabı aktif olarak kullanan (içinde önemli belgeler olan) bir kullanıcının bilgisayarını JumpCloud hesabına bağlayacaksınız; hesabı bağlamadan önce **+ local account**'a tıklayıp cihazda kullanılan yerel kullanıcı hesap adını yazmanız gerekir. Böylece JumpCloud hesabı cihazla bağlandığında JumpCloud yeni bir hesap oluşturmaz; kullanıcının belgeleri vb. korunur.

Bu işleme **yerel kullanıcı hesabını devralmak** denir.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/username-vs-local.webp' | relative_url }}" width="900" height="206" alt="Kullanıcı adı (bobfay) ile yerel kullanıcı hesabının (bob.fay) cihaza bağlanma şeması">
</div>

Bazı önemli noktalar:

- Kullanıcının JumpCloud kullanıcı adı ve yerel kullanıcı hesabının adı birbirinden farklı olmalıdır.
- Devralma işlemi için kullanıcı cihaza bağlanmamış olmalıdır.
- Eğer kullanıcı bağlanmışsa ve yerel hesap adı eklenmek isteniyorsa, kullanıcının bağlantısı kaldırılması gerekir.
