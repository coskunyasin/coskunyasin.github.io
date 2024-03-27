---
layout: post
title: Linux yetki ve sahiplik izinleri
tags: [linux-yetki-sahiplik,linux]
comments: true
author: Yasin Coskun
---

### Linux Yetkiler ve Sahiplik

Bu yazıda linux'da yetki,sahiplik ve okuma-yazma-çalıştırma yetkilerinin sayısal ifadelerine değineceğiz.

**Dosya izinlerini anlamak**

![](/resource/linux-sahiplik/2.jpg)

Yukarıdaki örnekte demo dizini altında deneme.txt adında bir dosya var. Bunun dosya olduğunu **-** ifadesi ile anlıyoruz.Dizin olduğunu ise **d** ifadesiyle anlıyoruz.Örneğimize dahil olmasa da **l** ifadesi sembolik linki temsil etmektedir.Ekstra olarak hard link ve sembolik link için ayrı bir konu başlığı açacağım.

Örnekte görüldüğü üzere 3 oktet olarak izinleri ayırabiliriz.Soldan sağa user, group, herkes gibi ayırabiliriz.


**Dosya izinlerinin sayısal ifadesi:**
![](/resource/linux-sahiplik/1.jpg)

deneme.txt dosyasının sayısal ifadesi 

1.oktet: rw- =6 

2.oktet: rw-=6 

3.oktet: r-- =4

Toplam= 664

Yukarıdaki hesaplama ile dosya izninin sayısal ifadesini bulmuş olduk.Sayısal ifadeler ile yetki vermek daha pratik olduğu için bu ifadelere aşina olmak faydalı olacaktır. Tabi sihirli rakam olan 777'yide atlamamak gerekir.Tavsiye edilmemekle birlikte full yetki vermek için 777 rakamını kullanabilirsiz.

```
chmod 777 deneme.txt
```
![](/resource/linux-sahiplik/3.jpg)

**Sahiplik Değiştirme**

deneme1.txt dosyamızın sahipliğini root'a atama işlemi yapalım.Root yetkisi olmayan kullanıcıda olduğum için başında sudo kullanarak "sudo chown root:root deneme1.txt" komutunu kullandım.Dosyamın root kullanıcısı ve root grubuna dahil olarak değiştiğini görmekteyiz.

![](/resource/linux-sahiplik/4.jpg)








