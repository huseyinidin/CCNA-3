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

## 🔹 CHAP (Challenge Handshake Authentication Protocol)

**CHAP**, PPP bağlantılarında **güvenli kimlik doğrulama** sunar. Şifreler açık gönderilmez; hash tabanlı doğrulama yapılır. Periyodik olarak yeniden doğrulama yapılabilir.

### 🎯 Amaçları

- PPP bağlantısında güvenli kimlik doğrulama sağlamak
- Şifrelerin düz metin ile gönderilmesini engellemek
- Bağlantı sırasında güvenliği sürekli kontrol etmek

### ✅ Avantajları

- Şifreler hashlenmiş olarak gönderilir → yüksek güvenlik
- Periyodik doğrulama ile bağlantı güvenliği sağlanır
- Tek taraflı veya iki taraflı doğrulama yapılabilir

### ⚠️ Dezavantajları

- PAP’a göre konfigürasyonu daha karmaşık
- Eski cihazlarda veya protokollerde uyumsuzluk olabilir
- Hash algoritması kırılabilir → modern şifreleme kadar güçlü değil

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
 ppp authentication chap
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
 ppp authentication chap
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