---
date: '2025-02-10'
title: Blog Hakkında
---

Bir blog sitesi açma fikri aklıma geldiğinde, yazılarımı nasıl pratik bir şekilde yayınlayabileceğimi araştırmaya başladım. Bu süreçte Hugo ile tanıştım ve sunduğu kolaylıklar beni oldukça etkiledi. Hugo’nun temalarını incelediğimde, ihtiyaçlarımı fazlasıyla karşılayabileceğini fark ettim. Sonunda Hugo/Congo temasını kullanmaya karar verdim.

## Kurulum Aşaması

Kurulumu congo'nun kendi web sitesindeki adımlardan takip ederek yaptım.[Burada](https://jpanther.github.io/congo/docs/installation/#install-using-hugo) birçok adım var ama ben hugo modülünü yükledim ve hugo komutuyla website oluşturdum daha sonrasında congo temasını github reposundan indirerek themes/congo dizinine yapıştırdım.

Sonraki adımım ise coskunyasin.github.io adında bir repo oluşturmak oldu.Hugo ince ayarları dökümanı takip ederek yapabilirsiniz tüm bunlar bitiğinde ise oluşturduğunuz repoda master ve gh-pages adında iki tane branch oluşturdum.Github Pages'da sitemin yayınlandığı branch gh-pages ve bu branchde /public klasörü var.Github hesabımdan ilgili repoyu inceleyerek branchleri kontrol edebilirsiniz.

En son adımda ise github linkimi yasincoskun.tech adresine yönlendirmek olacak. İlk adımda github hesabınızda settings kısmında Pages alanına giderek verifieds domains kısmından Add Domain diyerek verilen kayıtları dns yönettiğiniz alanda girmelisiniz. Daha sonra github iplerini A kaydı olarak girmeniz gerekiyor bunlar şöyle 

<ul>
  <li>185.199.108.153</li>
  <li>185.199.109.153</li>
  <li>185.199.110.153</li>
  <li>185.199.111.153</li>
</ul>

Bu işlemler tamamlandıktan sonra verified edebiliriz.En son işlemimiz ise ilgili repository settings kısmından Pages alanında Custom domain alanına domain adresimizi yazıyoruz ve save ile işlemi bitiriyoruz.