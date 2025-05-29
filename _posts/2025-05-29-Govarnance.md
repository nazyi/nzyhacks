---
categories: [blog]
layout: post
desc: " Veri ve bilgi gibi temel kavramlardan yola çıkarak, kişisel verilerimizi koruyan GDPR gibi önemli regülasyonları ve şirketlerde bilgilerin nasıl sınıflandırıldığını anlattım. Ayrıca, dijital dünyada karşılaştığımız siber saldırı türlerini (zararlı yazılımlar, oltalama, fidye yazılımları gibi) detaylıca inceleyerek, bu tehditlere karşı nasıl korunabileceğimize dair bilgiler sundum. Son olarak da Bilgi Güvenliği Yönetim Sistemi'nin (BGYS) temel adımlarını ele aldım. "
logo: "/assets/images/blog_icon/govarnance.png"
author: Buse Naz Yılmaz
title: Bilgi Yönetişimi 202 
---

**Terminoloji**

Veri: Anlamlı işlenmemiş parça

Bilgi: İşlenmiş veri

Bilgi Sistem ve Yönetim: Altyapı ve servisler

**Regülasyon**

_GDPR (General Data Protection Regulation)_, Avrupa Birliği tarafından kişisel verilerin korunmasına yönelik hazırlanmış bir veri güvenliği regülasyonudur. Bireylerin kişisel verilerinin işlenmesi, saklanması ve paylaşılması süreçlerinde gizlilik haklarını korumayı amaçlar. GDPR, yalnızca AB sınırları içerisindeki şirketleri değil, AB vatandaşlarının verilerini işleyen tüm dünya çapındaki kuruluşları da kapsar. Türkiye’deki KVKK gibidir. 

_NIS (Network and Information Systems) Direktifi_, ağ ve bilgi sistemlerinin güvenliğini artırmayı amaçlayan bir siber güvenlik regülasyonudur. Kritik altyapıların (enerji, ulaşım, sağlık, finans gibi) ve dijital hizmet sağlayıcılarının siber saldırılara karşı güvenliğini sağlamak için gerekli önlemleri almasını zorunlu kılar.

_PCI DSS (Payment Card Industry Data Security Standard),_ kartlı ödeme sistemlerinde kullanılan **kredi kartı bilgilerini korumak** amacıyla oluşturulmuş küresel bir güvenlik standardıdır. Visa, Mastercard, American Express gibi kart sağlayıcıları tarafından geliştirilmiştir. Bu standart, kart sahibi bilgilerini işleyen, depolayan veya ileten tüm kuruluşların belirli güvenlik önlemlerine uymasını zorunlu kılar.

**Bilgi Türleri**

Çok Gizli: Banka müşterilerinin kart bilgileri

Gizli: Sızarsa itibar zedelenmesi

Hizmete Özel: Şirkette belirli kişilere açık

Herkese Açık: Kamuya açık bilgiler

Kişisel Veri

Kişisel Veri: Kimliği belirten her türlü veri. Örn; Tc, Ad Soyad…

Özel Nitelikli: Irk, köken, mezhep, din…

**Siber Ataklar**

*   **Kötü Amaçlı Yazılım (Malware):** Virüsler, Truva atları ve solucanlar gibi zararlı yazılımları içerir. Bu yazılımlar, cihazlara izinsiz erişim sağlayarak sistemleri bozabilir veya saldırganlara uzaktan kontrol imkanı tanıyabilir. 
*   Virüs → Dosyaya tutunur, yayılmak için açılmayı bekler.
*   Truva Atı → Dost görünümlü düşmandır, kendi isteğinle indirirsin.
*   Solucan → Ağları kullanarak kendi kendine yayılır, kimseye sormaz bile!
*   **Oltalama (Phishing):** Güvenilir kaynaklardan geliyormuş gibi görünen e-postalar veya mesajlar aracılığıyla, kullanıcıların kişisel bilgilerini (şifreler, kredi kartı bilgileri) ele geçirmeyi amaçlar. Genellikle sahte web sitelerine yönlendirme yapılarak bilgiler toplanır.
*   **Hizmet Engelleme (DoS) ve Dağıtılmış Hizmet Engelleme (DDoS):** Bir web sitesi veya ağa aşırı miktarda istek göndererek, hizmetin yavaşlamasına veya tamamen çökmesine neden olan saldırılardır. DDoS saldırıları, birden fazla bilgisayardan eşzamanlı olarak gerçekleştirilir.
*   **Ortadaki Adam (Man in The Middle):** Saldırganlar, iki taraf arasındaki iletişimi gizlice dinleyerek veya değiştirerek, hassas bilgilere erişim sağlar. Örneğin, sahte Wi-Fi ağları oluşturularak kullanıcıların verileri ele geçirilebilir.
*   **SQL Enjeksiyonu (SQL Injection):** Güvenlik açıkları bulunan veri tabanlarına zararlı SQL kodları enjekte edilerek, saldırganların yetkisiz veri erişimi veya manipülasyonu yapmasına olanak tanır.
*   **Fidye Yazılımları (Ransomware):** Kullanıcıların dosyalarını şifreleyerek erişimi engeller ve şifrelerin çözülmesi için fidye talep eder. Son yıllarda bu tür saldırılarda önemli artışlar gözlemlenmiştir.
*   **Kripto Madenciliği (Cryptojacking):** Kullanıcıların cihazlarına izinsiz olarak kripto para madenciliği yazılımları yüklenerek, cihazların işlemci gücü kötüye kullanılır. Bu durum, cihaz performansının düşmesine ve enerji tüketiminin artmasına neden olur.
*   **Sıfırıncı Gün Açıkları (Zero Day Exploit):** Henüz keşfedilmemiş veya yamalanmamış yazılım açıklarından yararlanarak gerçekleştirilen saldırılardır. Bu tür açıklar, saldırganlara sistemlere sızma fırsatı sunar.
*   **Fileless Malware**: Geleneksel zararlı yazılımlardan farklı olarak, dosya tabanlı (file-based) bir yapıya sahip olmayan ve sistemde fiziksel bir dosya bırakmayan bir kötü amaçlı yazılım türüdür. Bu tür kötü amaçlı yazılımlar, hafıza (RAM) üzerinde çalışarak, sistemin işletim sistemini ve güvenlik yazılımlarını geçici olarak atlatır.
*   **Drive-By-Download:** kullanıcının farkında olmadan bir web sitesine girdiğinde zararlı bir yazılımın otomatik olarak indirildiği bir siber saldırı türüdür.
*   **Rootkit Atakları:** Rootkit saldırıları, bir saldırganın sisteme gizlice sızmasını, yetkisiz erişim elde etmesini ve bu erişimi uzun süre fark edilmeden sürdürmesini sağlar.
*   **Tailgaiting:** Bir kişinin, güvenli bir alana girmeye çalışan başka bir kişiyi takip etmesiyle gerçekleşen bir saldırı türüdür. 
*   **Quid Pro Quo**: Saldırganın bir hedefi manipüle etme amacıyla karşılıklı bir şey vaat etmesi durumudur. Yani, saldırgan, hedef kişiye belirli bir fayda veya avantaj teklif ederek ondan **bilgi** veya **yardım** almak için çalışır.

**BGYS (Bilgi Güvenliği Yönetim Sistemi) Adımları**

Planla, Uygula, Kontrol Et, Önlem Al
