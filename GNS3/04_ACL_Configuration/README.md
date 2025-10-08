# 🌐 ACLs for IPv4 Configuration

**IPv4 ACL (Access Control List)**, IPv4 trafiğini filtrelemek için kullanılan kurallar bütünüdür. Cisco cihazlarda IPv4 ACL’leri, güvenlik, trafik yönetimi ve erişim kontrolü amacıyla sıkça yapılandırılır. ACL’ler hangi paketlerin geçmesine izin verileceğini veya engelleneceğini belirler.

---

## 🛠️ IPv4 ACL Yapılandırma Temelleri

**IPv4 ACL yapılandırması**, belirli trafiğe izin verme veya reddetme kuralları oluşturur.

* ACL numarası veya isimle tanımlanır (Standard, Extended, Named ACL)
* Kurallar yukarıdan aşağıya işlenir, ilk eşleşen kural uygulanır
* En sonda varsayılan “deny all” kuralı vardır (implicit deny)
* Permit / Deny ifadeleri ile trafik kontrol edilir

---

## 📍 Standard IPv4 ACL Yapılandırması

**Standard ACL’ler**, sadece kaynak IPv4 adresine göre filtreleme yapar.

* ACL numarası 1–99 veya 1300–1999 aralığında tanımlanır
* Trafiği kaynak IP adresine göre engeller veya izin verir
* Genellikle hedefe yakın konumlandırılır
* Basit ağlarda temel erişim kontrolü sağlar

**Örnek:**

```
access-list 10 permit 192.168.1.0 0.0.0.255
interface g0/0
 ip access-group 10 in
```
---

## ⚙️ Extended IPv4 ACL Yapılandırması

**Extended ACL’ler**, kaynak ve hedef IP adresine ek olarak protokol ve port numarasına göre ayrıntılı filtreleme yapar.

* ACL numarası 100–199 veya 2000–2699 aralığında tanımlanır
* TCP, UDP, ICMP gibi protokollere göre ayrım yapılabilir
* Port bazlı kontrol ile belirli uygulamalar filtrelenebilir
* Genellikle kaynağa yakın konumlandırılır

**Örnek:**

```
access-list 101 deny tcp 192.168.1.0 0.0.0.255 any eq 23
access-list 101 permit ip any any
interface g0/1
ip access-group 101 out
```
---

## 📝 Numbered IPv4 ACL Yapılandırması

**Numbered ACL’ler**, numara ile tanımlandığı için yapılandırmalar genellikle daha kısa olur, ancak okunabilirlik açısından Named ACL'lere göre daha sınırlıdır.

* ACL numarası ile tanımlanır (Örneğin: 1-99 veya 100-199).
* Yapılandırması daha hızlı olabilir fakat düzenleme ve anlaşılırlık açısından daha zor olabilir.
* Büyük ağlarda yönetimi daha karmaşık hale gelebilir, çünkü numara üzerinden kural eklemek ve değiştirmek daha zor olabilir.

**Numbered ACL Yapılandırma Komutları:**

* Standard ACL: ip access-list standard <number>
* Extended ACL: ip access-list extended <number>

**Örnek:**

```    
ip access-list extended 101
deny tcp any any eq 80
permit ip any any
interface g0/2
ip access-group 101 in
```
---

## 📝 Named IPv4 ACL Yapılandırması

**Named ACL’ler**, numara yerine isim ile tanımlandığı için okunabilirliği artırır.

* ip access-list standard <name> veya
* ip access-list extended <name> şeklinde yazılır
* Mevcut kurallar üzerinde düzenleme yapmayı kolaylaştırır
* Büyük ağlarda yönetim avantajı sağlar

**Örnek:**

```    
ip access-list extended BLOCK_HTTP
deny tcp any any eq 80
permit ip any any
interface g0/2
ip access-group BLOCK_HTTP in
```
---

## 🔄 ACL Uygulama Yönleri

**ACL uygulama yönü**, trafiğin hangi akışta denetleneceğini belirler.

* Inbound: Trafik arabirime giriş yaparken kontrol edilir
* Outbound: Trafik arabirimden çıkış yaparken kontrol edilir
* Yanlış yön seçimi, istenmeyen sonuçlara yol açabilir

---

## 🚧 IPv4 ACL Kullanım Alanları

**IPv4 ACL’ler**, yalnızca güvenlik değil trafik yönetimi için de kullanılır.

* Belirli cihazların ağa erişimini sınırlama
* Yönetim erişimini (Telnet, SSH) filtreleme
* Uygulama trafiğini (HTTP, FTP, DNS) engelleme
* QoS politikaları için trafik sınıflandırma
* NAT ve VPN öncesi trafik kontrolü

---

## 🕵️ IPv4 ACL Konfigürasyon İpuçları

**IPv4 ACL yapılandırırken**, dikkat edilmesi gereken bazı noktalar vardır.

* Kurallar yukarıdan aşağıya okunur, ilk eşleşen uygulanır
* Varsayılan olarak tüm trafik reddedilir (implicit deny all)
* ACL’yi doğru arabirime ve doğru yöne uygulamak gerekir
* Gereksiz karmaşık kurallardan kaçınılmalıdır
* Düzenli loglama ile ACL etkinliği takip edilmelidir

---