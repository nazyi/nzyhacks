---
categories: [modul]
layout: post
description: "Cisco Ethical Hacker kursunun ilk bölümüdür. Siber güvenlikte tehdit aktörlerini, test ortamı türlerini, çevresel değerlendirmeleri ve farklı güvenlik test standartları ile metodolojilerini açıklamaktadır. Kurumların güvenlik zafiyetlerini belirlemek ve önlem almak amacıyla gerçekleştirilen sızma testlerinin kapsamı ve yaklaşımları detaylandırılmıştır. "
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Modül 1 
tags: [Cisco, Sızma Testi Temelleri]
order: 1
translation_url: /en/Cisco_Module1
---

## Module 1: Introduction to Ethical Hacking and Penetration Testing

### 1.1 Threat Actors

- **Organized Crime:** En son saldırı tekniklerini kullanarak paraya çevirebilecekleri her türlü siber suç yönetimini gerçekleştirirler.
- **Hacktivists:** Bu tür saldırganlar para uğruna değil, inandıkları amaç uğruna saldırı gerçekleştirirler. Hedefi utandırmak adına hassas bilgi çalıp halka ifşa ederler.
- **State-Sponsored:** Ülkelerin karşı rakip ülkeye saldırı yapmak için kullandıkları kişilerdir.
- **Insider Threats:** Organizasyonun içerisindeki ya kötü amaçlı insanlar örneğin kurumdan intikam almak isteyen insanlar ya da farkında olmadan bilgi sızıntısına sebebiyet veren insanlar olabilmektedir.

{% include mc-quiz.html id="ta-scenario-tr" question=site.data.mc_threat_actor.question options=site.data.mc_threat_actor.options correct_label="Doğru!" wrong_label="Yanlış, doğru cevap:" %}

### 1.2 Environmental Considerations

- **Network Infrastructure Tests**: Switchler, routerlar, firewallar ve bunları destekleyen kaynaklar örneğin (AAA, IPS…) gibi network elemanlarının kullanımı ve test edilmesi ile sağlanır.
- **Application-Based Tests**: Kurumsal uygulamalardaki güvenlik zayıflıklarının testidir. Yanlış yapılandırmalar, giriş doğrulama sorunları, enjeksiyon ve mantık hataları gibi durumları içerir. Arkadaki uç veritabanı da bu teste dahildir.
- **Penetration Testing in the Cloud**: Bulut güvenliği, kullanılan modele (SaaS, PaaS, IaaS) göre değişir ve hem müşteri hem de sağlayıcı sorumludur. Sızma testi yapılmadan önce, güvenlik gereksinimleri ve sözleşmelerin netleştirilmesi önemlidir. CSP'ler, bulut ortamında güvenlik değerlendirmeleri ve sızma testleri için yönergeler sunar.

### 1.3 Threat Assessment Types

- **Unknown-Environment Test:** Testçiye az miktarda bilgi verilmiştir. Domain isimleri ve scope dahilindeki IP adresleri attacker için verilmiş olabilir. Bu black-box testinin amacı dışarıdan bir saldırganın perspektifi ile bakılmasını sağlar.
- **Known-Environment Test:** Bu sefer saldırgan kurum hakkında ve kurumun iç yapısı hakkında az da olsa bilgi sahibi olur. Network diyagramları, IP adresleri, ayarlamalar ve bazı kullanıcı bilgileri tester için verilebilir. Eğer bir uygulama varsa testin içinde uygulamanın kaynak kodu tester ile paylaşılır.
- **Partially-Known Environment Test:** Black-box ve white-box testinin hibrit halidir. Testerlara belki kullanıcı bilgileri verilebilir fakat ağ yapısının iç yapısı verilmez.

### 1.4 Surveying Different Standards and Methodologies

- **MITRE ATT&CK:** Saldırganların taktik, teknik ve prosedürlerini (TTP) öğrenmek için yapılmış bir çerçevedir.
- **OWASP WSTG:** Web uygulaması testleri için geliştirilmiş bir rehberdir. Web uygulaması güvenliği testinin yüksek seviyedeki aşamalarını kapsar ve kullanılan test yöntemlerine daha derinlemesine iner.
- **NIST SP 800-115:** Organizasyonlara bilgi güvenliği testi planlama ve yürütme konusunda rehberlik sağlar.
- **OSSTMM:** Tekrarlanabilen ve istikrarlı güvenlik testlerini anlatan bir rehberdir.
- **PTES:** Saldırı türleri ve metodları ve belirtilen saldırı türlerini gerçekleştirebilmek için kullanılan en güncel toolları anlatan bir rehberdir.
