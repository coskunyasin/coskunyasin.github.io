---
layout: post
title: Kubernetes IDE:LENS
tags: [kubernetes,k8s,minikube,metallb]
cover-img: /resource/pages_logo/k8sheader.png
comments: true
author: Yasin Coskun
---

Bu post'da metallb detayına girmeden sadece minikube üzerinde yapılandırmayı nasıl yapabilir konusuna değineceğiz.Metallb projesini farklı bir yazıda detaylı ele alacağız.Özet olarak kubernetes ortamlarında LoadBalancer çözümü olarak kullanılan bir açık kaynak kodlu proje.

İlk olarak minikube'de hazır addonsları kullanacağız.Komut satırımızda "**minikube addons list**" yazarak addonsları listeliyoruz.

resim1




metallb'yi disabled olarak görmekteyiz. Şimdi aşağıdaki komut ile enable ediyoruz.
```
minikube addons enable metallb
```

Komut satırımızda "**minikube ip**" yazıyoruz.Çıktıdaki ip aralığını metallb'de kullanacağız.

```
C:\Windows\system32>minikube ip
192.168.59.100
```

Metallb konfigürasyonu yapmak için aşağıdaki komutu kullanacağız.Burada iki adımı aşağıdaki gibi verdim sizde kendinize göre düzenleyebilirsiniz.

```
minikube addons configure metallb
```
 Enter Load Balancer Start IP: 192.168.59.150

 Enter Load Balancer End IP: 192.168.59.155

Herşey tamam şimdi bir tane örnek yapalım.Normalde "**minikube dashboard**" komutu ile minikube'de dashboarda gidebiliyorduk.Dashboard servisini düzenleyerek loadbalancer üzerinden gideceğiz.
```
kubectl get svc -A
```

resim2

kubernetes dashoard servisimizin "**type: ClusterIP**" kısmını LoadBalancer olarak değiştiriyoruz.

```
kubectl edit svc kubernetes-dashboard -n kubernetes-dashboard
```

"**kubectl get svc -A**" komutu ile servisimizin EXTERNAL-IP kısmının ip aldığını görüyoruz.

resim4

Browserda external ip'yi yazarak dashboarda ulaştığımızı görmekteyiz.

resim5

