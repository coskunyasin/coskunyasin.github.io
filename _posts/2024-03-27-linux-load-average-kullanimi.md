---
layout: post
title: Linux Load Average Kullanımı
tags: [linux-load-average]
comments: true
author: Yasin Coskun
---

# LOAD AVARAGE

### Linux'da Load Average ne anlama geliyor?

Linux'ta load average (yük ortalaması) herhangi bir zamanda kaynak kullanımının göstergesidir.Linux'ta load average cpu'nun ne kadar meşgul olduğunu bize gösterir.

#w
#uptime
#htop komutları bize load average çıktısını vermektedir.Nasıl yorumlayacağımız konusu ise sistemizdeki cpu sayısına göre değişmektedir.

## **Nasıl yorumlarız?**

Yukarıda belirttiğimiz gibi çekirdek sayısını tespit ettikten sonra yorumlama kısmına geçebiliriz.Aşağıda "w" komutu çıktısını görüyoruz. load average kısmı aslında 3 farklı zaman aralığını veriyor. 0.01 değeri 1dk, 0.07 5dk, 0.42 15dk'lık ortalamayı veriyor.


```
$ w
 01:43:54 up  1:01,  0 users,  load average: 0.01, 0.07, 0.42
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
```

Hesaplamayı ise 1 çekirdek eğer yüzde yüz cpu kullanıyorsa 1 değerini görürüz. %50 kullanımda ise 0.50 aralığında bir çıktı görürüz.Aşağıda **stress-ng** toolu kullanarak burayı biraz daha açmak istiyorum.Benim sistemimde 4 çekirdek var ama aşağıdaki örnekte 1 çekirdeğe %50 yük göndererek ortalama çıktısını inceleyeceğiz.

İlk olarak stress-ng toolu ile 1 cpu'ya yüzde 50 yük gönder diyorum.

![](./resource/load-average/4.jpg)
<4.jpg>

htop çıktısında ise load average değerimin 50'lerde olduğunu görüyorum.

<5.jpg>

Bir diğer örnekte ise kendi sistemimi biraz zorlayarak örneklendireceğim

>cpu özelliğim: 4/8: 4 core 8 thread 

bu sefer stress-ng ile tüm thr'lere %90 yük gönderiyorum.

Buradaki -c 0 olarak kullanmamızın sebebi core sayımı bilmiyorum tüm corelara gönder anlamında okuyabiliriz. -l ise göndereceğimiz yük yüzdesi


<2.jpg>

Htop çıktısında %90 yük gönderdikten sonra çıktımızı görüyoruz. 7.23'lük bir oran ile karşılaşıyoruz.Yani %100 yük gönderdiğimizde max 8'lik bir average ile karşılaşacağız. Buna göre çıktıyı yorumyabiliriz.

<1.jpg>


Sistemimizde kaç çekirdek olduğunu doğrulamak

```
cat /proc/cpuinfo | grep core
```
<3.jpg>


### Core/Thread?

Bazen core/thread kafa karıştırıcı olabiliyor.Konu dışında olduğu için detaya girmeden burada sisteminizdeki core/thr çıktısını görmek için "lscpu" ve "htop" komutlarını kullanabilirsiniz.Yukarıdaki resimlerde htop çıktısında 0-7 aralığında thr görüyorsunuz.Bu benim toplamda 8 thr bir işlemciye sahip olduğumu gösteriyor.


4/18 core özelliğine sahip sistemimde lscpu çıktısı aşağıdaki gibi

```
$lscpu
Architecture:            x86_64
  CPU op-mode(s):        32-bit, 64-bit
  Address sizes:         43 bits physical, 48 bits virtual
  Byte Order:            Little Endian
CPU(s):                  8
  On-line CPU(s) list:   0-7
Vendor ID:               AuthenticAMD
  Model name:            ###
    CPU family:          23
    Model:               24
    Thread(s) per core:  2
    Core(s) per socket:  4

```







