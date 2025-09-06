# 🌐 Single-Area OSPFv2 Concepts

## 📌 OSPF Temelleri  

- Link-state routing protokolüdür.  
- Açık standarttır (RFC 2328).  
- Hızlı yakınsama sağlar.  
- Area (bölge) yapısı ile ölçeklenebilir.  

## 🗺️ Tek Alanlı (Single-Area) Yapı  

- Tüm yönlendiriciler **aynı area içinde** bulunur.  
- Genellikle **Area 0 (Backbone)** kullanılır.  
- Küçük ve orta ölçekli ağlarda tercih edilir.  

## 🔗 OSPF Adjacency (Komşuluk)  

- Router’lar birbirini **Hello paketleri** ile tanır.  
- **Hello ve Dead timer** değerleri uyumlu olmalıdır.  
- Aynı subnet, aynı area ID, aynı authentication gereklidir.  

## 📶 OSPF Paket Türleri  

- **Hello** → Komşuluk keşfi.  
- **DBD (Database Description)** → LSDB özeti.  
- **LSR (Link-State Request)** → Detay istek.  
- **LSU (Link-State Update)** → Güncel bilgi paylaşımı.  
- **LSAck** → Paket onayı.  

## 👑 DR ve BDR Seçimi  

- Çoklu erişimli ağlarda (Ethernet) yapılır.  
- **DR (Designated Router):** LSDB paylaşımını koordine eder.  
- **BDR (Backup Designated Router):** DR yedeğidir.  
- Diğerleri **DROther** olarak çalışır.  

## 📂 LSDB (Link-State Database) 
 
- Her router kendi link-state bilgisini paylaşır.  
- LSDB tüm routerlarda senkronize edilir.  
- SPF (Dijkstra) algoritması ile en kısa yol hesaplanır.  

## 🛠️ OSPF Konfigürasyon Temeli  

- `router ospf <process-id>` → OSPF başlatma.  
- `network <ip> <wildcard> area <id>` → Ağları OSPF’e dahil etme.  
- `show ip ospf neighbor` → Komşuluk kontrolü.  
- `show ip route ospf` → OSPF rotaları görüntüleme.  

## 📊 OSPF Metric (Cost)  

- **Cost = 100,000,000 / Bandwidth (bps)**  
- Daha yüksek bant genişliği → Daha düşük cost.  
- Manuel olarak `ip ospf cost <value>` ile ayarlanabilir.  

## 🔐 OSPF Authentication  

- Simple password veya MD5 kullanılır.  
- Güvenlik için router’lar aynı kimlik doğrulama değerine sahip olmalıdır.  

## ⚡ Avantajlar  

- Hızlı yakınsama.  
- Döngü (loop) oluşmaz.  
- Hiyerarşik yapı ile büyük ağlara uyumlu.  
- Open standard olduğu için vendor bağımsızdır.  
