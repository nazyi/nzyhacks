---
categories: [modul]
layout: post
desc: "Cisco Ethical Hacker kursunun ikinci bölümüdür. Sızma testi sürecinde planlama ve kapsam belirleme aşamalarının neden kritik olduğunu vurgular. Aynı zamanda regülasyonlara uyum, yasal sorumluluklar ve etik ilkeler çerçevesinde nasıl hareket edilmesi gerektiğini detaylandırır."
logo: "/assets/images/cisco.png"
author: Buse Naz Yılmaz
title: Cisco Ethical Hacker Modül 2 
order: 2
---

# Cisco Ethical Hacker

<h2> Module 2: Planning and Scoping a Penetration Testing Assesment </h2>

## 2.1 Regulatory Compliance Considerations

**PCI DSS**: Kredi kartı ve diğer dijital ödemeleri koruma altına almayı amaçlamaktadır.

**HIPAA:** İnsanların sağlık bilgilerini koruma altına almayı amaçlamaktadır.

**FedRAMP:** Bulut hizmetlerinin güvenliğini sağlamayı amaçlamaktadır.

### 2.1.1 Regulations in the Financial Sector

GLBA, finans kuruluşlarının bireylerin özel bilgileriyle başa çıkma biçimlerini kontrol eden bir yasadır ve büyük küçük bütün finans kuruluşlarına uygulanır.

### 2.1.2 Regulations in the Healthcare Sector

HIPAA, elektronik olarak korunmuş sağlık bilgilerine odaklanır. HIPAA güvenlik kuralları kapsanan varlıklar ve iş ortakları için geçerlidir.

·        **Healthcare Provider**: Tedaviyi sağlayan kişi veya kurumları tanımlamaktadır.

·        **Health Plan:** Tedaviyi karşılayan sigorta birimleri veya devlet sağlık planlarını tanımlamaktadır.

·        **Healthcare Clearinghouse:** Standart olmayan sağlık bilgilerini standart formata getirenleri tanımlamaktadır.

·        **Business Associates:** Kişi hizmeti alırken; bilgilerini alani ileten erişen veya sahip kişileri tanımlamaktadır.

### 2.1.3 Payment Card Industry Data Security Standard (PCI DSS)

Kart sahiplerini kişisel bilgilerin kötüye kullanımına karşı korumak ve ödeme kartı kanalındaki kayıpları en aza indirmek amacıyla, büyük ödeme kartı markaları PCI DSS kurup geliştirmiştir.

PCI DSS, kullanıcının kart bilgilerini işleyen veya depolayan bütün kuruluşlar için geçerlidir.

PCI endüstrisinde pentest yapmak için bazı anahtarları bilmeniz gerekir:

·        **Acquirer:** Alıcı banka olarak adlandırılan, ödeme kartlarını kabulünü eden kuruluş.

·        **ASV (Approved Scanning Vendor):** PCI SSC tarafından harici güvenlik açığını yürütmek için onaylanmış kurum.

·        **Merchant:** Bir hizmet vevya servis karşısında ödemeyi kart olarak kabul etmesi durumundaki tüccarlar, kişiler.

·        **PAN:** 19 hanelik kart numarası

·        **Payment Brand:** Visa, MasterCard gibi kart markaları

·        **PCI Forensic Investigator (PFI):** Kart bilgilerinin dahil olduğu olayları inceleyen sertifikalı kişiler.

·        **Qualified Security Assessor (QSA):** PCI DSS uyumluluk değerlendirmelerini gerçekleştirmek üzere sertifikalandırmış kişiler.

·        **Service Provider:** Kart markası olmayan fakat kart sahibinin bilgilerini işleyen ve hizmet sunan şirketlerdir.

PAN bilgisi okunamaz yani encrypted formatta saklanılması beklenmektedir. Luhn algoritması, kredi kartı numarası, IMEI numaraları ve daha farklı kimlik numaralarını doğrulamak için kullanılır.

### 2.1.4 Key Technical Elements in Regulations You Should Consider

Çoğu regülasyon bazı temel unsurlar üzerinde durur ve penetrasyon testçisi değerlendirme sürecinde bunlara dikkat etmelidir.

·        **Data Isolation**: Kart ödeme işlemlerinde yer alan sistemlere tamamen izole bir ağ uygulamalıdır.

·        **Password Management:** Regülasyonlar güçlü parolalar için bazı şartlar koyar. Şifre uzunluğu, karmaşıklığı veya multifaktör doğrulama bunların içindedir.

·        **Key Management:** Anahtar, bir şifreleme algoritmasında hangi yerinde uygulanacağı ve hangi sırayla çalıştıralacağı gibi hususlarda rol alır. Anahtarın korunması sürecine anahtar yönetimi denir.

### 2.1.5 Legal Concepts

Penetrasyon testi gerçekleirmeden önce bazı hukuki kavramlar vardır.

·        **Service-level Agreement**: SLA hem sizin hem de müşteri tarafının hak ve sorumluluklarını belirleyen, hizmet kalitesiyle ilgili anlaşmadır.

·        **Confidentiality:** Bilgilere kimlerin erişebileleceğini kontrol etmek lazım. Penetrasyon testinden sonra bulduğunuz bilgileri kendi sisteminiz üzerinden silmeniz gerekmektedir.

·        **Statement of Work:** Bir penetrasyon testi çalışması sırasında gerçekleştirilecek faaliyetleri ayrıntılı bir şekilde belirten belgedir. Örneğin çalışma tarihleri, çalışma konumu, çalışma kapsamı ve ödeme planı vb.

·        **Master Service Agreement:** Müşteriyle yapılacak işleri daha hızlı ve kolay şekilde müzakere edebilmek için çerçeve oluşturmak.

·        **Non-Disclosure Agreement (NDA):** Bir penetrasyon testi ile beni işe alan kurum arasında yapılan gizlilik sözleşmesidir.

### 2.1.6 Contracts

Sözleşme, testin tüm detaylarını, yapılacak işleri ve ödeme koşullarını belirten belgedir. Oldukça spesifik, anlaşılır ve temiz olmalıdır.

### 2.1.7 Disclaimers

Test sırasında veya öncesinde oluşabilecek bazı durumlara karşı herhangi bir garanti verilmediğinin belgesidir.

## 2.2 Explaining the Importance of Scoping and Organizational or Customer Requirements

### 2.2.1 Rules of Engagement

Sızma testlerinin hangi şartlar altında yapılacağını belirler. Test edilecek IP adresleri, testin yapılacağı zaman veya testin dahil olduğu domain adresleri gibi bilgileri içerir.

### 2.2.2 Target Lists and In-Scope Assets

Kapsam belirleme, pentestin en önemli unsurlarından biridir. Test edilecek cihazlar, varlıkların IP adresi veya proglamlama arayüzleri yani API’ler bu kapsamın içindedir. Api dokümantasyonu türleri hakkında aşağıda bilgi verilmiştir. Api dokümantasyonları uygulamanın arkasında çalışan hangi endpointe cevap gidiyor hangi endpointten cevap geliyor gibi kuralları anlatan bir dökümdür. Halka açık olmaması gerekmektedir. Dokümantasyonu okuyup ona göre saldırı düzenlenebilir.

·        **SOAP:** XML formatını kullanır, mesajların nasıl görüneceğini tanımlayan XSD dosyaları vardır.

·        **Swagger**: API’lerin nasıl çalıştığını tanımlayan yapılandırılmış bir belgedir. RestFUL Api’ler için kullanılır.

·        **WDSL**: Web servislerin işlevselliğini belgelemek için kullanılan XML tabanlı bir dildir. Eski bir tür olan SOAP Api için kullanılır. Bir web servisiyle nasıl etkileşime geçileceğini, hangi yöntemlerin (fonksiyonların) kullanılacağını, hangi parametrelerin gerektiğini ve web servisinin nasıl yanıt vereceğini açıkça tanımlar.

·        **GraphQl:** API'ler için bir sorgu dilidir ve verilerin nasıl alındığını, güncellendiğini ya da silindiğini belirlemek için kullanılan bir yapıdır.

·        **WADL:** Web uygulamalarını tanımlamak için kullanılan XML tabanlı bir dildir.

**WADL vs WSDL?**

![](./assets/images/Resim2.jpg)

Pentest için diğer kullanılan kaynaklardan bazıları aşağıda verilmiştir.

·        **Software Development Kit**: İşletim sistemi, yazılım çerçevesi veya donanım ile etkileşime geçmek için kullanılanların koleksiyonudur.

·        **Source Code Acces**: Uygulamanın kaynak koduna erişim sağlamanın izin verilmesi.

·        **Example of Application Request**: İçeriklere erişmek için bazı web tabanlı uygulamalar örneğin OWASP ZAP veya Burp-Suite kullanılabilir.

·        **System and Network** **Architectural Diagrams**: Sistem ve ağ iç yapısının mimarisi.

## 2.3 Demonstrating an Ethical Hacking Mindset by Maintaining Professionalism and Integrity

### 2.3.1 Overview

Pentesterların profesyonelliğini ve dürüstlüğünü koruması gereken birçok senaryo vardır.

·        **Background Checks of Penetration Testing Teams**: Anlaşılan firma pentesterlara güvenmek için bir arkaplanda kontrol sağlayabilir. Kendi bilgilerini görecek olan insanlara güven sağlamak ister.

·        **Adherence to The Specific Scope of Engagement**: Test yapılması istenilen sistemlerin olduğu listeye “allow list”, test yapılması istenmeyen sistemlerin olduğu listeye ise “disallow list” denmektedir.

·        **Identification of Criminal Activity and İmmediate Reporting of Breaches/Criminal Activities**: Bazen testlerde sizden önce gerçek bir hackerın müşterinin sistemini zaten açığa çıkardığını görürsünüz. Böyle davranışları direkt raporlamanız gerekmektedir.

·        **Limiting the Use of Tools to A Particular Engagement**: Sistemi çökertebileceği için müşteriler bazı toolların kullanılmamasını isteyebilir.

·        **Limiting İnvasiveness Based on Scope**: Sistemlerden elde edilen bilgiler, zafiyet taraması çıktıları ve bu çıktılara dayanarak nasıl sömürüleceğini bazı toollar yardımı ile sağlanabilir. Fakat bu tolların saldırganlığını müşterinin sistemine zarar vermeyecek şekilde ayarlamanız gerekmektedir. 

·        **Confidentiality of Data/İnformation**: Test yapılırken bulduğunuz bilgiler kesinlikle gizli kalmalı ve kimse ile paylaşılmaması gerekmektedir.

·        **Risk to the Professional**: Eğer antlaşma kurallarına uymazsanız cezai suçlamalara veya para cezalarına maruz kalabilirsiniz.
