---
categories: [dokumantasyon]
layout: post
description: "JumpCloud University Core kursunun ikinci dersinin ikinci bölümü: manuel/CSV ile kullanıcı ekleme, kullanıcı güvenlik ayarları, kullanıcı aktivasyonu ve aksiyon butonları."
tool: JumpCloud
logo: "/assets/images/blog_icon/jumpcloud.png"
author: nazy
title: JumpCloud Core 2.2 - Kullanıcı Oluşturma
tags: [JumpCloud, Identity Management]
order: 3
translation_url: /en/Jumpcloud-Core2-2
---

JumpCloud'un ikinci kursunun ikinci bölümü ile devam ediyoruz.

## Manuel veya CSV'den Kullanıcı Ekleme

**User Management > Users > + Users** butonuna tıklayarak farklı yöntemlerle kullanıcı ekleyebilirsiniz.

### Manuel Olarak

- **+ Users** butonuna tıkladıktan sonra **Manuel User Creation** seçeneğini seçin.
- Gerekli bilgileri (isim, soyad, kullanıcı adı...) girdikten sonra kullanıcıyı kaydedin.
- Kullanıcıyı ne zaman aktive etmek istiyorsanız onu ayarlayın.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/new-user-manual.webp' | relative_url }}" width="1000" height="537" alt="JumpCloud'da manuel yeni kullanıcı oluşturma formu, User Information alanları">
</div>

#### Kullanıcı Güvenlik Ayarları

Kullanıcıyı oluştururken eğer aşağıya kaydırırsanız **User Security Setting and Permission** kısmını göreceksiniz. Buradan kullanıcının şifre güvenliğini, MFA ayarlarını ve izinlerini kontrol edebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/user-security-settings.webp' | relative_url }}" width="1000" height="537" alt="User Security Settings and Permissions paneli: şifre yetkisi, MFA ve izin ayarları">
</div>

> Custom özellik eklemek isterseniz aşağı kaydırınca **Custom Attributes** kısmından ekleyebilirsiniz.

### CSV Üzerinden

- **+ Users** butonuna tıklayınca **Import from CSV** seçeneğini seçin.

> Burada dikkat etmeniz gereken ufak bir nokta var. Yükleyeceğiniz CSV dosyası JumpCloud'un istediği formatta olmalı. Bunu kontrol etmek için **Download CSV Template** diyerek formatı kontrol edebilirsiniz.

- Formata uygun hazırladığınız CSV dosyasını içe aktarabilirsiniz.
- Aktardıktan sonra istediğiniz kişileri seçerek kullanıcıları oluşturabilirsiniz.

### Kullanıcı Aktivasyonu

Aktif durumda bir kullanıcı oluştururken, JumpCloud size kullanıcı şifresi oluşturmak için e-posta göndermenizi isteyecek. Fakat bu durum, CSV dosyasından içe aktarılan kullanıcılar için geçerli değildir. İçeri aktarılan kullanıcılar için e-posta gönderimini manuel olarak sizin tetiklemeniz gerekmektedir.

#### Aksiyon Butonları

Kullanıcıyı tıkladıktan sonra sağ yukarıdaki **Actions** menüsündeki aksiyonlardan bahsedelim:

- **Add to User Group**: Tıklediğiniz toplu kişileri bir kullanıcı grubuna ekler.
- **Send Activation Mail**: Seçtiğiniz kişiye aktivasyon e-postası gönderir.
- **Send Password Reset Mail**: Sadece aktif olan kullanıcılar için geçerlidir. Şifre sıfırlama e-postası gönderir.
- **Force Password Change**: JumpCloud'un kontrol ettiği bütün uygulamalardan hemen atarak, kullanıcıyı bir sonraki girişinde şifresini değiştirmeye zorlar.
- **Unlock User Account**: Birden fazla yanlış şifre girilmesinden dolayı kilitlenen hesabı açar.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/actions-menu.webp' | relative_url }}" width="1000" height="537" alt="Users sayfasında seçili kullanıcı için açılan Actions menüsü">
</div>

{% include flip-cards.html id="jc-actions-tr" items=site.data.jc_actions hint="Kartlara tıklayıp ne işe yaradıklarını hatırlamaya çalış." %}
