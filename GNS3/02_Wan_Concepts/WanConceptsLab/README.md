# 🔗 Point-to-Point Protocol (PPP)

**PPP (Point-to-Point Protocol)**, iki cihaz arasında **seri bağlantı** üzerinden veri iletişimini sağlamak için geliştirilmiş bir **WAN protokolüdür**. OSI modelinin **2. katmanında (Data Link Layer)** çalışır ve farklı ağ katmanı protokollerini (IPv4, IPv6, IPX, AppleTalk vb.) taşıyabilir. Özellikle seri hatlarda, modem bağlantılarında, DSL hatlarda ve **router-to-router** iletişiminde kullanılmıştır.

---

## 🎯 PPP’nin Amacı

- 🌐 Farklı ağ katmanı protokollerini aynı seri hat üzerinden iletmek  
- 🔒 Kimlik doğrulama (authentication) desteği sunmak  
- ⚙️ Standart bir encapsulation yöntemi sağlamak  
- 🔄 Esnek, taşınabilir ve cihazdan bağımsız iletişim kurmak  
- 🛠️ Hata kontrolü ve link yönetimi yapmak  

---

## ✅ Avantajları

- 📦 **Çok protokollü destek:** IPv4, IPv6, IPX, AppleTalk vb.  
- 🔑 **Kimlik doğrulama:** PAP (Password Authentication Protocol) ve CHAP (Challenge Handshake Authentication Protocol) desteği  
- 🧩 **Basit yapı:** Konfigürasyonu kolaydır, çoğu cihaz tarafından desteklenir  
- 🔍 **Hata kontrolü:** LCP (Link Control Protocol) ile link yönetimi ve hata tespiti yapılır  
- 🔀 **Esneklik:** Senkron ve asenkron hatlarda çalışabilir  

---

## ❌ Dezavantajları

- 🐢 **Performans:** Modern WAN teknolojilerine göre yavaştır  
- 🛡️ **Şifreleme eksikliği:** Veri şifreleme sağlamaz, ek protokollere ihtiyaç vardır  
- 📉 **Yerini yeni teknolojilere bırakması:** Ethernet, MPLS ve VPN çözümleri daha çok tercih edilmektedir  
- 🔌 **Donanım bağımlılığı:** Seri bağlantılara özgü olduğundan kullanım alanı sınırlıdır  

---

## 📌 Özet

PPP, geçmişte WAN bağlantılarında **temel rol** oynamış, basitliği ve çok protokollü desteğiyle yaygın kullanılmıştır. Günümüzde **Ethernet tabanlı WAN çözümleri, MPLS ve VPN teknolojileri** ile yerini büyük ölçüde kaybetmiştir. Ancak **ağ sertifikasyonları (CCNA, CCNP)** için hâlâ öğrenilmesi gereken önemli bir protokoldür.  

---

## 🛠️ Konfigürasyon Adımları

```
interface Serial2/0
 ip address 192.168.1.1 255.255.255.252
 encapsulation ppp
 no shutdown
```

```
interface Serial2/0
 ip address 192.168.1.2 255.255.255.252
 encapsulation ppp
 no shutdown
```
---