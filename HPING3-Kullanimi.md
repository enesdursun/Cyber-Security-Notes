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

+ `-s`: Syn paketi gönderir
+ `-p`: Hedef port numarası
+ `-c`: Gönderilecek paket sayısı
+ `-d`: Gönderilecek veri boyutu
+ `–udp`: Udp protokolünde paket yollar
+ `–tcp`: Tcp protokolünde paket yollar
+ `–fast`: Saniyede 10 paket gönderir
+ `–faster`: Saniyede 100 paket gönderir
+ `–flood`: Paketleri hızlı bir şekilde gönderir.
+ `-a`: Sahte IP adreslerinde paketler gönderir.
+ `–rand-source`: Rastgele IP adresleri üzerinden paketler gönderir.

**_Bazı kısaltmalar ve açıklamaları:_**

+ `len`: Dönen paketlerin boyutu
+ `ip`: Paketin gönderildiği hedef makinenin ip adresi
+ `ttl`: Paketin süresi
+ `DF`: Parçalama baytının aktifliği 
+ `id`: Uniq bilgisi
+ `sport`: Paketlerin göderilgiği port
+ `flags`: TCP bayrağı(flag'i)
+ `seq`: Paketlerin sıra numarası
+ `win`: Win(pencere) paket boyutu
+ `rtt`: Milisaniye cinsinden süre

## *Örnek Senaryo 1: Ping Testi*
*-> ICMP(Internet Control Message Protocol) Testi. Ctrl+C ile durdurana kadar ping atmaya devam eder:*

`hping3 -1 [Site_Link]`

<img src="https://i.hizliresim.com/8oocrgg.png" alt="resim4" width="540">

## *Örnek Senaryo 2: Port Kontrolü*
  *-> Belli bir porta SYN paketleri göndeririz. Hangi yerel(local) porttan kontrol edeceğimizi de belirleriz. Çıktı şu şekilde olur:*

`hping3 -V -S -p 80 -s 5050 [Site_Link]`

<img src="https://i.hizliresim.com/l7lr5zz.png" alt="resim5" width="540">

## *Örnek Senaryo 3: Ack Taraması(Scan)*
  *-> Bir host'un aktif olup olmadığını görmek için kullanılabilir. Port açıksa ping engellenip RST yanıtı göndermelidir:*

`hping3 -c 1 -V -p 80 -s 5050 -A [Site_Link]`

<img src="https://i.hizliresim.com/d1l6stq.png" alt="resim6" width="640">

## *Örnek Senaryo 4: Xmas Taraması(Scan)*
  *-> TCP sıra numarasını(sequence number) sıfıra ayarlarız. URG PSH FIN flaglerini seçeriz. Hedef aygıtın TCP portu kapalıysa, hedef yanıt olarak bir TCP RST paketi gönderir. Hedef aygıtın TCP portu açıksa, Xmas taramasını iptal eder ve yanıt göndermez.*

`hping3 -c 1 -V -p 80 -s 5050 -M 0 -UPF [Site_Link]`

<img src="https://i.hizliresim.com/f21dpn1.png" alt="resim7" width="640">

## *Örnek Senaryo 5: Boş Tarama(Null Scan)*
  *-> Xmas taramasına çok benzerdir fakat ondan farklı olarak flag seçilmez.*

`hping3 -c 1 -V -p 80 -s 5050 -Y [Site_Link]`

<img src="https://i.hizliresim.com/ikq7ipf.png" alt="resim8" width="640">

## *Örnek Senaryo 6: Smurf Attack*
  *-> Hedef sisteme sahte ping mesajları basan bir tür DDoS(Denial of Service) saldırısıdır:*

`hping3 -1 --flood -a [Victim_IP] [Broadcast_Address]`

<img src="https://i.hizliresim.com/smjeuht.png" alt="resim9" width="640">

## *Örnek Senaryo 7:*
*-> Terminali root yetkisiyle açarız ya da komutun başına `sudo` yazıp yetki alırız. Belirlenen IP adresi ve porta SYN paketleri göndeririz.*

`hping3 -S [Hedef IP] -p [Hedef Port]`

<img src="https://i.hizliresim.com/jfl40fi.png" alt="resim10" width="640">

*-> Komut çalıştığı esnada wireshark ile network trafiğini ve saldırıyı görebiliriz,*

<img src="https://i.hizliresim.com/mk9z8vv.png" alt="resim11" width="640">

*-> Makinemizin sürekli olarak hedef makineye syn paketi gönderdiği açıkça görülebilir. Benzer şekilde aynı komutu `–flood` ile gönderirsek paketi olabildiğince hızlı gönderecek ve yanıtları göstermeyecektir.*

`hping3 -S -p [hedef Port] --flood [hedef IP]`

<img src="https://i.hizliresim.com/q0aqg0l.png" alt="resim12" width="960">

## *Örnek Senaryo 8:*
*-> Udp protokolünde belirlenen IP adresine random kaynaktan belirtilen size'da data gönderme işlemi*

`hping3 --count 200 --[Gonderim_Hizi] --udp [Hedef_IP] --rand-source --data [Data Boyutu]`

<img src="https://i.hizliresim.com/htl7qap.png" alt="resim13" width="640">

## *Örnek Senaryo 9: Basit DDoS Saldırısı*
*-> Gönderilecek paket sayısı, veri boyutu, pencere boyutu(default:64), kaynak port, hedef ip girilir, `--rand-source` ile IP gizlenir. Ctrl+C ile saldırıyı sonlandırabiliriz.*

`hping3 -c [Paket_Sayisi] --rand-source -d [Data_Boyutu] -w [Pencere_Boyutu] -p [Port_Numarasi] -S [IP_Adresi]`

<img src="https://i.hizliresim.com/f6ri65s.png" alt="resim14" width="640">

## *Örnek Senaryo 10: Firewall Kontrolü*
*-> Sistemde Firewall olup olmadığının kontrolü şu şekilde yapılır: `-V` ile daha detaylı gösterim için verbose modu aktif olur. `--scan` ile normal bir tarama yapmak istediğimizi belirtiriz. Sonrasında scan edeceğimiz port aralığını gireriz. `-S` parametresi ile de SYN paketleri göndereceğimizi belirtiriz. Örnek bir sonuç yukarıdaki gibidir.*

`hping3 -V --scan [Port_Numarası/aralığı] -S [IP_Adresi]`

<img src="https://i.hizliresim.com/yi348la.png" alt="resim15" width="360">

*-> Üstteki çıktıda boş gözüken portlar firewall ile korunuyor demektir.*

---

### Hping3 ile bu örnek senaryolar çeşitlendirilebilir, çoğaltılabilir. Yanında wireshark gibi yardımcı programlar kullanılarak daha işlevli hale getirilebilir.





