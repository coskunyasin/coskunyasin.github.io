---
layout: post
title: Regex nedir ve nerelerde kullanılır?
tags: [regex]
comments: true
author: Yasin Coskun
---

# Regex nedir ve nerde kullanılır ?
```
/((\d{3})(?:\.|-))?(\d{3})(?:\.|-)(\d{4})/
```
Yukarıda bir regex örneği görüyoruz. Başta korkutucu gelmesi çok doğal ama biraz bakmaya başlayınca aslında işlerin basitleştiğini farkediyorsunuz.

Regex namıdiğer Regular Expressions (Düzenli İfadeler) bir yazılım dili değil.Yazılım dilinden belirli ifadeleri belirli bir kombinasyonda yakalamamızı sağlayan bir araçtır.

Bir diğer kullanım alanı ise bir dizenin doğru biçimde kullanıldığını doğrulamak için kullanmaktır.

Go, Java, C#, Python ve JavaScript gibi programlama dilleri regex destekler.

**Doğrulamayı** python re modülü kullanarak aşağıdaki gibi örneklendirebiliriz.
```
import re

def is_valid_phone_number(phone_number):
  """
  Telefon numarasının doğru biçimde olup olmadığını kontrol eder.
  """
  pattern = re.compile(r'^(\d{3})(\d{3})(\d{2})(\d{2})$')
  return pattern.match(phone_number)

phone_number = "2125551212"

if is_valid_phone_number(phone_number):
  print("Telefon numarası doğru.")
else:
  print("Telefon numarası yanlış.")
  ```

Cep telefonu bilgisi **yakalamak** için bir örnek 

555-555-55-55

```
\d{3}-\d{3}-\d{2}-\d{2}
```

### *Sık kullanılan karakterler*

- \d  tüm sayı karakterleriyle eşleşir
```
regex: \d
input:123456789yas
output:123456789
```
- \D  sayı olmayan karakterlerle eşleşir
```
regex: \D
input: 123YAS_-*
output: _-*
```
- \w  alfanümerik ve alt çizgi olan karakterlerle eşleşir
```
regex: \w
input: 123yas_-*
output: 123yas_
```
- \W  alfanümerik ve alt çizgi olmayan herşeyle eşleşir
```
regex: \W
input: 123YAS_-*
output: -*
```
- \s  boşluk, sekme ve yeni satır ile eşleşir
```
regex: \s
input: 123YAS_-*   123YAS_-*
output: boşluğu alır
```
- \S  boşluk, sekme ve yeni satır olmayanlarla eşleşir
```
regex: \S
input: 123YAS_-*   123YAS_-*
output:123YAS_-*123YAS_-*
```
- .   Nokta, ister rakam, ister alfabe, ister özel karakter olsun, herhangi bir karakterle eşleşir
```
regex: .
input: Yas123*._-/
output: Yas123*._-/
```
- $ Bir dizenin sonuyla eşleşir.Belirli bir kalıpta biten dizeleri eşleştirir.
``` 
regex: $_
input: Yas123*._
output:_
```
- ^ belirli bir kalıpla başlayan dizeleri eşleştirmek için kullanılır
``` 
regex: ^The
input: The end
output: The
``` 

- | OR operatörü gibi davranır.
```
regex: yasin|tech
input: yasin tech post
output: yasin tech
```

***Basit olarak regex'in kullanımına baktık ama bundan daha fazlası olduğunu unutmamak gerekir.Örneklerinizi ve regexi daha iyi anlamak için [https://regex101.com](https://regex101.com/) faydalı olacaktır.***





