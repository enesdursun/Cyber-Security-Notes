<img src="https://i.hizliresim.com/84rpaa3.jpg" alt="resim" width="280">

# HPING3
## *HPING3 Nedir?*
**HPING3**, Linux sistemleri üzerine kurulabilen veya bazı linux sürümlerinde kurulu olarak gelen bir güvenlik uygulamasıdır. Ping’in gelişmiş versiyonudur. Hping3 ile tıpkı ping'de olduğu gibi hedef IP adresine paketler gönderilir. Ping'den farklı olarak bu uygulama: 

+ TCP, UDP ve RAW-IP paketleri gönderilmesine izin verip Firewall, Ips, Anti-DDoS gibi cihazların test edilmesi için kullanılabilir. 
+ IP Spoofing(IP Sahtekarlığı) yaparak hedef sistemi korumak için kullanılan cihazların session(oturum) limitlerini doldurup hizmetin servis veremez hale gelmesini amaçlar. 
+ Güvenlik duvarları oluşturabilir ve DOS saldırılarına karşı önlemler alınabilir.
+ Gelişmiş bir port tarayıcısıdır ve dosya transferi yapabilir.
+ TCP/IP paketleri toplaması yapabilir ve bunların testlerini gerçekleştirebilir.

## *Nasıl Yüklenir?*

**HPING3** uygulaması hem Windows hem de Linux işletim sistemlerinde kullanılabilir. Aşağıda Kali Linux üzerinden örnek bir kurulumu görebiliriz:

<img src="https://i.hizliresim.com/rl4qoqu.png" alt="resim1" width="540">

## *HPING3 Kullanımı ve Tüm Parametreleri*

Uygulama hakkında detaylı bilgi edinmek ve genel parametreleri öğrenmek için `hping3 -h` yazabiliriz:

<img src="https://i.hizliresim.com/kvhx6uc.png" alt="resim2" width="540">
<img src="https://i.hizliresim.com/hfv4hzp.png" alt="resim3" width="540">

**_Önemli parametrelerin kullanımı:_**

+ `-s`: syn paketi gönderir
+ `-p`: hedef port numarası
+ `-c`: gönderilecek paket sayısı
+ `-d`: gönderilecek veri boyutu
+ `–udp`: udp protokolünde paket yollar
+ `–tcp`: tcp protokolünde paket yollar
+ `–fast`: saniyede 10 paket gönderir
+ `–faster`: saniyede 100 paket gönderir
+ `–flood`: paketleri hızlı bir şekilde gönderir.
+ `-a`: sahte ıp adreslerinde paketler gönderir.
+ `–rand-source`: rastgele ıp adresleri üzerinden paketler gönderir.

**_Bazı kısaltmalar ve açıklamaları:_**

+ `len`: Dönen paketlerin boyutu
+ `ip`: Paketin gönderildiği hedef makinenin ip adresi
+ `ttl`: paketin süresi
+ `DF`: Parçalama baytının aktifliği 
+ `id`: Uniq bilgisi
+ `sport`: paketlerin göderilgiği port
+ `flags`: TCP bayrağı
+ `seq`: paketlerin sıra numarası
+ `win`: Win(pencere) paket boyutu
+ `rtt`: Milisaniye cinsinden süre

## *Örnek Senaryo 1: Belirlenen IP Adresi ve Port'a SYN Flag'i Gönderilir*
*-> Terminali root yetkisiyle açarız ya da komutun başına `sudo` yazıp yetki alırız. Girilen IP ve port değerleri örnektir.*

`hping3 -S 192.168.1.1 -p 80`

<img src="https://i.hizliresim.com/jfl40fi.png" alt="resim4" width="540">

*-> Komut çalıştığı esnada wireshark ile network trafiğini ve saldırıyı görebiliriz*

<img src="https://i.hizliresim.com/mk9z8vv.png" alt="resim5" width="540">

