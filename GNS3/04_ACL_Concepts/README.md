# 🔐 ACL Concepts  

**Access Control List (ACL)**, ağ trafiğini filtrelemek, güvenlik politikalarını uygulamak ve belirli kaynaklara erişimi kontrol etmek için kullanılan kurallar bütünüdür. ACL’ler, yönlendiriciler ve güvenlik cihazları üzerinde tanımlanır ve ağ trafiğinin izinli mi yoksa engelli mi olduğunu belirler.  

---

## 🛡️ ACL Temelleri  

**ACL temelleri**, hangi trafiğin geçeceğine veya engelleneceğine karar verir.  

- Paketlerin kaynağına ve hedefine göre filtreleme  
- Protokol (IP, TCP, UDP, ICMP) bazlı kontrol  
- Port numaralarına göre izin verme veya reddetme  
- Trafik yönetimi ve güvenlik sağlama  

---

## ⚙️ ACL Türleri  

**ACL türleri**, farklı ihtiyaçlara göre yapılandırılır.  

- Standard ACL: Yalnızca kaynak IP adresine göre filtreleme yapar  
- Extended ACL: Kaynak, hedef, protokol ve portlara göre ayrıntılı filtreleme sağlar  
- Named ACL: Numara yerine isimle tanımlanır, okunabilirliği artırır  
- Dynamic ACL: Zaman bazlı ve kullanıcı doğrulamalı erişim sağlar  
- Reflexive ACL: Geri dönüş trafiğini dinamik olarak kontrol eder  

---

## 📍 ACL Yerleşimi  

**ACL yerleşimi**, performans ve güvenlik açısından kritik öneme sahiptir. 
 
- Standard ACL: Hedefe yakın konumlandırılır (trafik yoğunluğu azaltılır)  
- Extended ACL: Kaynağa yakın konumlandırılır (gereksiz trafik engellenir)  
- “Inbound” ve “Outbound” yönlerinde uygulanabilir  
- Trafik akışına göre doğru arayüz seçimi gerekir  

---

## 🔑 ACL Kullanım Alanları  

**ACL kullanım alanları**, yalnızca güvenlik değil, aynı zamanda trafik yönetimini de içerir.  

- Belirli kullanıcıların veya cihazların erişimini engelleme  
- Yönetim erişimlerini sınırlama (ör. Telnet, SSH)  
- Trafik yönlendirme ve QoS için sınıflandırma  
- NAT ve VPN işlemleri için ön filtreleme  
- DMZ ve iç ağ arasında güvenlik sağlama  

---

## 🧩 ACL Kuralları ve İşleyişi  

**ACL kuralları**, yukarıdan aşağıya doğru sıralı çalışır.  

- İlk eşleşen kural uygulanır, geri kalanlar değerlendirilmez  
- Tüm ACL’lerde varsayılan olarak “deny all” (implicit deny) bulunur  
- Permit ve deny ifadeleri ile trafik kontrol edilir  
- Düzenli loglama ile trafiğin kaydı tutulabilir  

---

## 🛠️ ACL Konfigürasyon Örnekleri  

**ACL konfigürasyonu**, Cisco IOS cihazlarda temel sözdizimiyle yapılır. 
 
- Standard ACL:  
  `access-list 1 permit 192.168.1.0 0.0.0.255`  
- Extended ACL:  
  `access-list 101 deny tcp 10.0.0.0 0.0.0.255 any eq 23`  
- Named ACL:  
  `ip access-list extended BLOCK_HTTP`  

---

## 🚧 ACL Kısıtlamaları ve Zorluklar 
 
**ACL kısıtlamaları**, bazı durumlarda güvenlik yönetimini zorlaştırabilir. 
 
- Karmaşık yapılandırmalarda yönetim zorluğu  
- Büyük ağlarda performans sorunları  
- Yanlış yerleştirme ile istenmeyen trafik bloklanabilir  
- Stateful kontrol olmadığı için yeni nesil güvenlik cihazlarına ihtiyaç duyulabilir  

---

## 🕵️ ACL ve Güvenlik Stratejisi  

**ACL’ler**, güvenlik mimarisinin bir parçasıdır ama tek başına yeterli değildir. 
 
- Firewall, IDS/IPS gibi teknolojilerle birlikte kullanılmalıdır  
- “Defense in Depth” yaklaşımının ilk basamaklarından biridir  
- Küçük ağlarda temel güvenliği sağlar  
- Büyük kurumsal ağlarda destekleyici rol oynar  

---
