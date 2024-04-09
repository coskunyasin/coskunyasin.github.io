---
layout: post
title: Kubernetes IDE:LENS
tags: [kubernetes,lens]
cover-img: /resource/pages_logo/k8s.png
comments: true
author: Yasin Coskun
---
Kubernetes'i farklı bir dashboard ile daha iyi anlamak veya denemek isteyebilirsiniz.Bunun için LENS alternatif olarak karşımıza çıkmakta.Projenin web sitesinden ücretli paketlerin detaylarına bakabilirsiniz.Biz bu yazıda free olanı kullanacağız.

Bu post'da minikube ile ilerleyeceğiz.İlk adım olarak minikube start komutu ile minikube ayağa kaldırıyoruz.

![](/resource/kubernetes-ide-lens/1.jpg)

Daha sonra [buradan](https://k8slens.dev/download) lens'i download ediyoruz. Kurulum basit olduğundan dolayı adımlardan bahsetmiyorum.Github, google gibi hesaplarınızla oturum açabilirsiniz.

Kurulum tamamlandıysa Lens'i açarak solda katalog menüsüne tıklıyoruz ve sağda + simgesi > Add from kubeconfig tıklıyoruz.Buraya kubeconfig bilgilerini ekleyeceğiz.Bilgileri almak için tekrar komut satırımızı açarak aşağıdaki komutu yazıyoruz ve çıktıyı LENS'e yapıştırıyoruz

``` 
kubectl config view
``` 

![](/resource/kubernetes-ide-lens/2.jpg)
![](/resource/kubernetes-ide-lens/3.jpg)

Add Cluster dedikten  sonra clusterımıza bağlanıyoruz ve aşağıdaki gibi bir dashboard karşılıyor bizi.Deneme olarak minikube addons enable edebilir veya bir deployment create ederek denemelerinizi yapabilirsiniz.
