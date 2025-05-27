---
categories: [makine]
layout: post
title: TryHackMe Pickle Rick
desc: ""
logo: "/assets/images/picklerick.jpeg"
author: Buse Naz Yılmaz
---
# Port Taraması

Bizden Rick’i tekrardan insana çevirmek için gereken üç tane malzemeyi soruyor.

Makine IP adresimiz: 10.10.246.186

Bilgi toplamak için nmap taraması yaparak başlıyorum.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> nmap -sC -sV 10.10.246.186  
PORT   STATE SERVICE VERSION  
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)  
| ssh-hostkey:  
|   3072 03:b8:cc:f9:aa:e4:d5:dd:cb:a7:e8:9c:22:1b:4a:5e (RSA)   
|   256 b3:ac:ad:44:04:b9:3f:ee:b6:7a:9c:bc:19:c9:04:86 (ECDSA)   
|_  256 7c:06:dd:f0:cd:4f:6f:05:ef:94:d7:81:21:67:e5:12 (ED25519)  
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))  
|_http-title: Rick is sup4r cool  
|_http-server-header: Apache/2.4.41 (Ubuntu)  
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel    
</div>
Nmap taraması sonucunda ssh ve http portlarının açık olduğunu buluyoruz. SSH hakkında elimizde açık bir zafiyet olmadığı için 80 portuna tarayıcı üzerinden erişiyorum. 

<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/first.webp" width="500" height="400">
</div>

Rick bizden bilgisayarına erişip son üç tane gizli malzemeyi bulmamızı istiyor fakat şifresini hatırlamadığını belirtiyor. Web sayfası üzerinden bilgi edinmye çalışalım. İlk öncelikle sayfanın kodunu incelemeyle başlayalım. Kaynak kodunu incelerken bize verilen bir kullanıcı adı olduğunu görüyoruz. 

<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/sec.webp" width="700" height="400">
</div>

Harika! Şimdi ise daha fazla detay öğrenmek için gizli dosyaları tarayacağız.

# Dosya Tarama

Bu işlem için gobuster isimli bir aracı kullanacağız. Gobuster, hızlı ve güçlü brute-force kullanarak dizin ve dosya bulma tarayıcısıdır. Bu aracı kullanmak için aşağıdaki komutu kullancağız.

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> gobuster dir -u http//10.10.246.186 -w /root/Desktop/SecLists-master/Discovery/Web-Content/directory-list-2.3-medium.txt -x php,sh,txt,cgi,html,css,js,py
</div>
Bu komut bizim -w parametresi ile belirttiğimiz wordlist ögelerini deneyerek gizli dosyaları bulmamızı sağlayacak.  Komutun çıktısında birkaç tane gizli dosya bulabildiğimizi görüyoruz. 

<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/th.webp" width="600" height="100">
</div>
