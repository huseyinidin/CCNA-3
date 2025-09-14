# 🌐 PPP, PAP ve CHAP: WAN Bağlantılarında Güvenli Veri İletimi

## 🔹 PPP (Point-to-Point Protocol)

**PPP**, iki nokta arasındaki seri bağlantılarda veri iletimi sağlayan **evrensel bir WAN protokolüdür**. Telefon hatları, seri kablolar, DSL ve VPN gibi bağlantılarda kullanılır.

### 🎯 Amaçları

- Noktadan noktaya güvenli veri bağlantısı kurmak
- IP, IPX, AppleTalk gibi farklı protokolleri desteklemek
- Kimlik doğrulama sağlamak (PAP ve CHAP)

### ✅ Avantajları

- Çok protokollü iletişim sağlar
- Kimlik doğrulama ile güvenliği artırır
- Hata kontrolü ve paket bölümlendirme sunar (LCP & NCP)

### ⚠️ Dezavantajları

- Seri bağlantılar modern Ethernet kadar hızlı değildir
- Konfigürasyonu bazen karmaşık olabilir
- Çok noktalı veya kablosuz bağlantılar için uygun değildir

---

## 🔹 PAP (Password Authentication Protocol)

**PAP**, PPP bağlantılarında kullanılan **basit bir kimlik doğrulama protokolüdür**. Kullanıcı adı ve şifreyi düz metin olarak gönderir.

### 🎯 Amaçları

- PPP bağlantısında kullanıcı doğrulaması yapmak
- Sadece yetkili kullanıcıların bağlantı kurmasını sağlamak

### ✅ Avantajları

- Kurulumu basittir
- Eski cihazlarla uyumludur

### ⚠️ Dezavantajları

- Şifreler düz metin ile gönderilir → güvenlik düşer
- Paket yakalama (sniffing) saldırılarına açık
- Sunucu kimliği doğrulanmaz → tek taraflı doğrulama

---

## 📊 Özet Karşılaştırma

| Protokol | 🔒 Güvenlik | ⚙️ Kullanım Kolaylığı | 🎯 Amaç |
|-----------|------------|--------------------|----------|
| PPP       | Orta       | Orta               | Noktadan noktaya veri iletimi, çok protokollü destek |
| PAP       | Düşük      | Yüksek             | Basit kullanıcı doğrulama |
| CHAP      | Yüksek     | Orta               | Güvenli kullanıcı doğrulama, hash tabanlı |

> 💡 **Not:** Modern ağlarda CHAP tercih edilir. PAP daha çok eski cihazlar veya uyumluluk gerektiren senaryolarda kullanılır.

---

## 🛠️ Konfigürasyon Adımları

### PAP Konfigürasyonu 

**Router 1**
```
username R2 password 0 Cisco123
interface Serial2/0
 ip address 10.0.1.1 255.255.255.252
 no shutdown
 encapsulation ppp
 ppp authentication pap
 ppp pap sent-username R1 password 0 Cisco123
```
```
interface FastEthernet0/1
 ip address 192.168.1.3 255.255.255.0
 no shutdown
```
```
VPCS 
PC1 
ip 192.168.1.10 255.255.255.0 192.168.1.1
```
---

**Router 2**
```
username R1 password 0 Cisco123
interface Serial2/0
 ip address 10.0.1.2 255.255.255.252
 no shutdown
 encapsulation ppp
 ppp authentication pap
 ppp pap sent-username R2 password 0 Cisco123
```
```
interface FastEthernet0/1
 ip address 192.168.2.1 255.255.255.0
 no shutdown
```
```
VPCS 
PC2 
ip 192.168.2.10 255.255.255.0 192.168.2.1
```
---
