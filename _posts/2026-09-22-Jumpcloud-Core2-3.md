---
categories: [dokumantasyon]
layout: post
description: "JumpCloud University Core kursunun ikinci dersinin üçüncü bölümü: harici dizin entegrasyonları (M365/Entra ID, Google Workspace, Active Directory), özel API entegrasyonları ve İK entegrasyonu ile kullanıcı içe aktarma."
tool: JumpCloud
logo: "/assets/images/blog_icon/jumpcloud.png"
author: nazy
title: JumpCloud Core 2.3 - Harici Kaynaklardan Kullanıcı İçe Aktarma
tags: [JumpCloud, Identity Management]
order: 4
translation_url: /en/Jumpcloud-Core2-3
---

JumpCloud'un ikinci kursunun üçüncü bölümü ile devam ediyoruz.

## Harici Kaynaklardan Kullanıcı İçe Aktarma

JumpCloud, kullanıcı içe aktarmada çeşitli bulut servislerini ve insan kaynakları programlarını desteklemektedir.

### Dizin Entegrasyonları

JumpCloud tarafından desteklenen uygulamalarla JumpCloud'u entegre ederek kullanıcı içe aktarabilir veya kullanıcı hesaplarını senkronize edebilirsiniz.

Nasıl işe yarıyor?

- Kullandığınız servis ile sürekli ve güvenli bağlantı kurulur.
- Kullandığınız servisten kullanıcı verileri aktarılır.
- Kullandığınız servisten halihazırda var olan hesaplar aktarılır.
- JumpCloud üzerinden servise doğru dışarı aktarım yapılır.
- Kullanıcı hesapları hizmetten alınabilir.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/directory-integrations-diagram.webp' | relative_url }}" width="1000" height="453" alt="JumpCloud Open Directory Platform'un Google Workspace, Microsoft EntraID/365, BambooHR, Personio ile bob, Namely, Okta, Workday arasındaki içe/dışa aktarım ve senkronizasyon şeması">
</div>

#### Dizin Entegrasyonu Seçme

JumpCloud; Google Workspace, Microsoft 365 ve Active Directory gibi dizinleri desteklemektedir. İstediğiniz dizini entegre etmek için:

- **User Management > Cloud Directories** üstüne tıklayın.
- **+** işaretine basın ve eklemek istediğiniz dizini seçin.

### M365 & Google Workspace'ten Kullanıcı İçe Aktarma

Her entegrasyonda senkronizasyon işleminin birbirine benzediğini fark edeceksiniz.

#### M365 & Entra ID Entegrasyonu

M365/Entra ID ile kolayca JumpCloud'a kullanıcıları içe aktarabilir, sürekli senkronizasyon yaparak kontrol sağlayabilirsiniz.

Aşağıdaki durumlardan biri varsa bağlantıyı tekrar tetiklemeniz gerekmektedir:

- API anahtarının süresi dolmuşsa.
- API anahtarı artık geçersizse.
- Global Admin hesabı hizmet dışı kalmışsa.

M365/Entra ID bağlantısı yapmak için:

- **User Management > Cloud Directories**
- **+** işaretine basarak **M365/Entra ID** seçeneğini seçin.
- Dizine isim verdikten sonra global admin hesabına giriş yapın.
- Aktarmak istediğiniz kullanıcıları seçin.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/m365-import-users-modal.webp' | relative_url }}" width="1000" height="509" alt="Import Users from M365/Entra ID penceresi, içe aktarılacak kullanıcıların seçildiği liste">
</div>

- Kullanıcıları içeri aktardıktan sonra **Users** kısmına gelip senkronize etmek istediğiniz kullanıcıyı seçin.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/m365-directory-users-tab.webp' | relative_url }}" width="1000" height="294" alt="Cloud Directories detay panelinde Users sekmesi, M365/Entra ID instance'ına senkronize olan kullanıcı listesi">
</div>

- Bu kullanıcıları tek bir grupta toplamak için kullanıcı grubu oluşturabilir ve dizine bağlayabilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/m365-directory-user-groups-tab.webp' | relative_url }}" width="1000" height="359" alt="Cloud Directories detay panelinde User Groups sekmesi, JumpCloud, LDAP, Linux Group, Managers, Microsoft 365 grupları">
</div>

#### Google Entegrasyonu

Google ile de M365/Entra ID'ye benzer şekilde bağlantı sağlayarak kullanıcı içe aktarması ve senkronizasyonunu sağlayabilirsiniz.

> Google Super Admin hesabınız ile JumpCloud'u bağlamanız gerekmektedir.

Google bağlantısı yapmak için:

- **User Management > Cloud Directories**
- **+** işaretine basarak **Google Workspace** seçeneğini seçin.
- Dizine isim verdikten sonra global admin hesabına giriş yapın.
- **Start Manuel Import** butonuna tıklayın.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/google-import-users-panel.webp' | relative_url }}" width="1000" height="389" alt="Google Cloud Directory detay paneli, Import Users bölümü ve Start Manual Import butonu">
</div>

- Buradan yapmak istediğiniz işlemi seçin.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/google-import-options-modal.webp' | relative_url }}" width="1000" height="451" alt="Import New Users and Update Existing Users from Google penceresi, içe aktarma seçenekleri">
</div>

- Kullanıcıyı seçin.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/google-select-user-import.webp' | relative_url }}" width="1000" height="301" alt="Import New Users from Google penceresi, içe aktarılacak kullanıcının seçilmesi">
</div>

- Aynı M365/Entra ID'de yaptığımız gibi kullanıcıyı ve kullanıcı grubunu Google Workspace ile bağlamayı unutmayın.

#### Özellik Eşleştirme ve Ayarlar

Özellik seçimlerinizi 3 farklı seçenek ile yönetebilirsiniz:

- **Import**: Seçilen özellikler Google Workspace'ten JumpCloud'a içe aktarılır.
- **Export**: Seçilen özellikler JumpCloud'dan kullanılan dizine aktarılır.
- **Exclude**: Seçilen özelliklere dokunulmaz.

#### Kullanıcı Akışları

##### Staged Kullanıcı Akışı

<div class="doc-tabs">
  <div class="doc-tab-buttons">
    <button type="button" class="doc-tab-btn active" data-tab="flow-staged-nopw-tr">Şifresiz</button>
    <button type="button" class="doc-tab-btn" data-tab="flow-staged-pw-tr">Şifreli</button>
    <button type="button" class="doc-tab-btn" data-tab="flow-staged-access-tr">Access</button>
  </div>
  <div class="doc-tab-content">
    <div class="doc-tab-panel active" id="flow-staged-nopw-tr" markdown="1">

**Staged User Without a Password**: Eğer şifresiz bir kullanıcıyı harici bir dizine bağlarsanız, kullanıcıya aktivasyon maili göndermeyi seçebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/staged-user-flow-detail.webp' | relative_url }}" width="1000" height="538" alt="Staged durumundaki bir kullanıcının detay sayfası, Password Expired ve TOTP MFA enrollment durumları">
</div>

  </div>
    <div class="doc-tab-panel" id="flow-staged-pw-tr" markdown="1">

**Staged User With a Password**: Eğer şifreli bir kullanıcıyı harici bir dizine bağlarsanız, kullanıcıya hoş geldin maili atmayı seçebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/staged-user-flow-detail.webp' | relative_url }}" width="1000" height="538" alt="Staged durumundaki bir kullanıcının detay sayfası, Password Expired ve TOTP MFA enrollment durumları">
</div>

  </div>
    <div class="doc-tab-panel" id="flow-staged-access-tr" markdown="1">

**Staged User Access**: Eğer zaten halihazırda bir hesap yoksa, kullanıcı bağlandıktan sonra hesap oluşturulur.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/staged-user-flow-detail.webp' | relative_url }}" width="1000" height="538" alt="Staged durumundaki bir kullanıcının detay sayfası, Password Expired ve TOTP MFA enrollment durumları">
</div>

  </div>
  </div>
</div>

##### Aktif Kullanıcı Akışı

<div class="doc-tabs">
  <div class="doc-tab-buttons">
    <button type="button" class="doc-tab-btn active" data-tab="flow-active-pw-tr">Şifreli</button>
    <button type="button" class="doc-tab-btn" data-tab="flow-active-nopw-tr">Şifresiz</button>
    <button type="button" class="doc-tab-btn" data-tab="flow-external-tr">Harici Yönetilen</button>
  </div>
  <div class="doc-tab-content">
    <div class="doc-tab-panel active" id="flow-active-pw-tr" markdown="1">

**Active User With a Password**: JumpCloud kullanıcılara bilgilendirme maili atarak, harici dizine eklendiklerini ve bir sonraki girişlerinde şifrelerinin senkronize olacağını söyler.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/active-user-with-password.webp' | relative_url }}" width="1000" height="538" alt="Active durumunda ve Password Active olan bir kullanıcının detay sayfası">
</div>

  </div>
    <div class="doc-tab-panel" id="flow-active-nopw-tr" markdown="1">

**Active Users Without a Password**: Kullanıcı bağlandıktan sonra, kullanıcı portala giriş yapınca şifresi senkronize olacaktır.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/active-user-without-password.webp' | relative_url }}" width="1000" height="538" alt="Active durumunda ve Password Pending olan, aktivasyon maili gönderilebilen bir kullanıcının detay sayfası">
</div>

  </div>
    <div class="doc-tab-panel" id="flow-external-tr" markdown="1">

**Externally Managed Passwords**: Eğer farklı bir şifre yöneticisi kullanılıyorsa, JumpCloud kullanıcıya şifre ile alakalı mail göndermez.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/externally-managed-password.webp' | relative_url }}" width="1000" height="538" alt="Federated (harici bir IdP tarafından yönetilen) şifre durumuna sahip bir kullanıcının detay sayfası">
</div>

  </div>
  </div>
</div>

### Active Directory Entegrasyonu

Active Directory yapınız ile JumpCloud'u senkronize edebilirsiniz. Bunu yaparken kullanılan 2 agent vardır (import agent ve sync agent). Temel alınan 3 farklı yaklaşım vardır:

- Kullanıcıları, grupları ve şifreleri AD yapısında yönetmek.
- Kullanıcı ve şifreleri AD, JumpCloud'da veya her ikisinde de yönetmek.
- Kullanıcı, grupları ve şifreleri JumpCloud'da yönetmek.

JumpCloud'a AD domaini eklemek için:

- **User Management > Active Directories**
- **+ Add ADI Domain**
- Yukarıda bahsedilen 3 temel yaklaşımdan hangisini kullanacaksanız onu seçin.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/ad-integration-define-step.webp' | relative_url }}" width="1000" height="383" alt="New Active Directory (AD) Integration sihirbazı, Define adımı: kullanıcı ve şifrelerin nerede yönetileceğinin seçilmesi">
</div>

- ADI isminizi verin.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/ad-integration-setup-step.webp' | relative_url }}" width="1000" height="227" alt="New Active Directory (AD) Integration sihirbazı, Setup adımı: domain adının girilmesi">
</div>

- Özellikleri nasıl kullanacaksanız onun ayarlarını yapın.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/ad-integration-map-step.webp' | relative_url }}" width="1000" height="316" alt="New Active Directory (AD) Integration sihirbazı, Map adımı: JumpCloud ve AD özellik eşleştirmeleri">
</div>

- Domaininizin kaydedildiğine dair çıkan sayfada detayları inceleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/ad-integration-configure-step.webp' | relative_url }}" width="1000" height="305" alt="New Active Directory (AD) Integration sihirbazı, Configure adımı: yapılandırma özeti ve agent indirme linkleri">
</div>

### Harici Kimlik Kaynakları

Eğer hazırda var olan uygulamalar sizin işinize yaramıyorsa, özel olarak API entegrasyonları yapabilirsiniz.

Gerekenler:

- Ayarlama yapabilmek için teknik bilgileri içeren dokümantasyon.
- Desteklenen doğrulama yöntemleri (API Key, Bearer Token, OAuth 2.0).
- JSON isteği ve JSON cevaplaması.

#### Yeni Uygulama Oluşturma

- **Access > SSO Applications**
- **+ Add New Application**
- Açılan pencereden sağ en alttaki **Custom Application** seçeneğine tıklayın.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/custom-app-select-application.webp' | relative_url }}" width="1000" height="356" alt="Create New Application Integration sihirbazı, Select Application adımı ve Custom Application kartı">
</div>

- Kullanıcı içe aktaracağımız için **Import Users from this app** seçeneğini işaretleyin.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/jumpcloud_core2/custom-app-select-options.webp' | relative_url }}" width="1000" height="707" alt="Create New Application Integration sihirbazı, Select Options adımı: Import users from this app seçeneği">
</div>

- Gerekli bilgileri girin.

#### İK (HR) Entegrasyonu

HR uygulamaları ve JumpCloud iki taraflı bir bağlantı sağladığı için, özellikle işe alım veya işten çıkma süreçlerinde senkronizasyon sorununu ortadan kaldırıp daha düzenli ve kolay bir işlem haline getiriyor.
