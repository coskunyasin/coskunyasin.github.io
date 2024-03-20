---
layout: post
title: Terraform ile AWS Üzerinde EC2 Uygulaması
subtitle: 
tags: [terraform]
comments: true
author: Yasin Coskun
---


>Bu yazıda free aws hesabı oluşturma, windows'a terraform kurulumu ve free ec2 altyapısını kullanarak altyapı oluşturmayı açıklayacağım.

### Adım1: AWS Free Account Oluşturma

Google'da  "**free aws account**" diyerek ilgili sayfada kullanıcı oluşturuyoruz.Bu kısımlarda kişisel bilgileri isteyecektir.Burda kullandığınız e-posta ve telefon numarasını girmenizde dikkatli olun çünkü doğrulama isteyecek.Kredi kartı bilgilerinde ise sanal kart girmenizi tavsiye ederim bu kartı şimdilik 1TL limiti olması önemli çünkü kredi kartı doğrulama adımında 1TL çekiyor.

### Adım2: AWS Hesap Ayarları

Hesabınızı başarıyla oluşturduktan sonra Konsol Ana Sayfasına erişim sağlayabiliyor olmanız lazım.Sonraki adımımız arama kutucuğuna IAM yazarak kullanıcı ayarlarını yapmamız olacak.IAM panosundan solda Kullanıcılar kısmına girerek yeni bir user oluşturuyoruz.

***IAM > Erişim Yönetimi > Kullanıcılar > Kullanıcı oluşturun***

- Kullanıcı adını giriyoruz.Altta bulunan AWS Yönetimi Konsolun'na erişimi sağlayın kutucuğunu işaretlemiyoruz. > Sonraki

- İzin ekleyin adımında kullanıcı grupları boş gözükecektir.Grup oluştur diyoruz ve herhangi bir isim vererek grup oluşturalım ve İzin politikasında en üstte bulunan **AdministratorAccess** olanı işaretleyerek kullanıcı grubu oluştur diyebiliriz.

- Şimdi son olarak Erişim Yönetimi > Kullanıcı grupları kısmından oluşturduğumuz gruba kullanıcımızı ekliyoruz.

- Kullanıcılar kısmından kullanıcı adımıza tıklıyoruz ve Güvenlik kimlik bilgilerine geliyoruz.Burada Erişim anahtarları kısmından Erişim anahtarı oluşturun diyoruz.

- AWS dışında çalışan uygulama diyerek ilerliyoruz ve bize verilen access key ve secret keyi localimize kaydediyoruz. Burası önemli çünkü terraformda aws'e deploy etmemiz için bu bilgileri kullanacağız.

Herşey tamamsa terraform'u windows'a yükleme adımına geçebiliriz.

### Adım3: Terraform'u Windows'a Yükleme

- Google'a terraform install diyerek Windows altında 386 olanı download ediyoruz.
- Zip olarak ineceği için klasöre çıkartıyoruz.Klasör ismini terraform olarak değiştirelim.
- terraform klasörünü C:\ dizini altına kopyalıyoruz.
- Windows'da arama kısmına environment variable yazarak Environment Variables kısmına giriyoruz.
- Path kısmına çift tıklayarak açılan pencerede new diyerek C:\terraform\ yazıyoruz ve kaydediyoruz.
- Cmd veya powershell'de terraform veya terraform --version yazarak versiyon kontrolümüzü yapıyoruz.
- Eğer cmd veya ps ekranında terraform yazdığınızda hata aldıysanız environment variable kısmını incelemeniz gerekiyor burda bir yanlışlık yapmış olabilirsiniz.


### Terraform'u Hazırlama

İlk olarak C:\terraform dizini altında demo diye bir klasör açarak .tf dosyalarımızı burda oluşturacağız.Bu demo'da 5 tane .tf dosyası oluşturacağız sırasıyla:

1. instance.tf
2. provider.tf
3. vars.tf
4. version.tf
5. terraform.tfvars

yukarıdaki dosyaları oluşturduysak editleyip notepad veya edit programınızla aşağıda herbir dosya için yazan komutları girip kaydedebilirsiniz.

- .instance.tf

```shell
resource "aws_instance" "example" {
  ami           = lookup(var.AMIS, var.AWS_REGION, "") # last parameter is the default value
  instance_type = "t2.micro"
}

```

<br>
- .provider.tf

```shell
provider "aws" {
  access_key = "${var.AWS_ACCESS_KEY}"
  secret_key = "${var.AWS_SECRET_KEY}"
  region     = "${var.AWS_REGION}"
}
```

<br>
- .vars.tf

```shell
variable "AWS_ACCESS_KEY" {
}

variable "AWS_SECRET_KEY" {
}

variable "AWS_REGION" {
  default = "eu-west-1"
}

variable "AMIS" {
  type = map(string)
  default = {
    us-east-1 = "ami-13be557e"
    us-west-2 = "ami-06b94666"
    eu-west-1 = "ami-0d0099f3f21d6b80e"
  }
}
```
<br>

- .version.tf

```shell
terraform {
  required_version = ">= 1.7.5"
}
```
<br>
- .terraform.tfvars \
***Access key ve secret key kısımlarını "" arasında kendi bilgilerinizi gireceksiniz.***

```shell
AWS_ACCESS_KEY =""
AWS_SECRET_KEY =""
AWS_REGION = "eu-west-1"
```
<br>

### Terraform'u Başlatma

cmd veya ps ekranımızdan C:\terraform\demo klasörüne gidiyorum ve sırasıyla aşağıdaki komutları yazıyoruz.
```
terraform init
```
```
terraform plan
```
```
terraform apply
```
Herşey yolunda giderse **Apply complete! Resources: 1 added, 0 changed, 0 destroyed.** çıktısı alacağız.Aws konsolundan EC2 panosundan deploy olan sunucumuzu görüyoruz.

Kurduğumuz ortamı kaldırmak için aşağıdaki komutu kullıyoruz.
```
terraform destroy
```

### NOTLAR

terraform komutlarında kullandığımız variablelara bu yazıda değinmedik.Basit olarak bir instansce yaratma mantığını gördük.Bu yazıda dikkat etmemiz gereken önemli nokta .vars.tf içerisindeki aşağıdaki alan. Buradaki AMI değeri değişklik gösterebilir. Bu değeri [burdan](https://cloud-images.ubuntu.com/locator/ec2/) bulabilirsiniz. Bu sitede search kısmında eu-west-1 yazarak bu regiondaki AMI-ID'leri göreceğiz. Aşağıdaki değerde bunlardan bir tanesi

```
eu-west-1 = "ami-0d0099f3f21d6b80e" 
```
.instance.tf altındaki instance_type = t2.micro olmasının sebebi ise AWS'in ücretsiz olarak sunduğu instance olmasından kaynaklı.Region'a göre instance typeları değişkenlik gösterebiliyor bu yazıda eu-west-1 üzerinden ilerledik.Bu kısmı araştırarak ücretsiz instance typeları ile kendinize göre terraformu özelleştirebilirsiniz.

