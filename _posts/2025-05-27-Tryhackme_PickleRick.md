---
categories: [makine]
layout: post
title: TryHackMe Pickle Rick
desc: ""
logo: "/assets/images/cap.png"
author: Buse Naz Yılmaz
media_subpath: /images/tryhackme_picklerick/
image:
  path: room_image.webp
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

!(first.webp){: width="400" height="300" }

