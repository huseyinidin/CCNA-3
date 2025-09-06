# 🌍 Multi-Area OSPFv2 Concepts

🔹 **Temel Fikir**  
- OSPF, büyük ve karmaşık ağlarda tek bir LSDB ile ölçeklenemez.  
- Multi-area yapısı, topolojiyi **daha küçük alanlara bölerek** verimlilik sağlar.  
- **Backbone (Area 0)** her zaman merkezde bulunur.  

---

## 🏛️ Area Türleri
- **Backbone Area (Area 0):** Tüm diğer alanların bağlanması gereken merkez.  
- **Regular Area:** Normal alan, tüm LSA tiplerini kabul eder.  
- **Stub Area:** Dış yönlendirmeleri (Type 5 LSA) kabul etmez, tek çıkış noktası vardır.  
- **Totally Stubby Area (TSA):** Hem external (Type 5) hem inter-area (Type 3) LSA’ları kısıtlar.  
- **NSSA (Not-So-Stubby Area):** Stub mantığında ama dış rotaları (Type 7) içeri alabilir.  

---

## 🚦 Router Türleri
- **Internal Router (IR):** Tek bir alana ait router.  
- **Backbone Router (BR):** Area 0 içinde çalışan router.  
- **Area Border Router (ABR):** İki veya daha fazla area’ya bağlı router. LSDB özetleme yapar.  
- **Autonomous System Boundary Router (ASBR):** OSPF dışı rotaları içeri aktaran router.  

---

## 📡 LSA Türleri (kısa özet)
- **Type 1:** Router LSA (her area için lokal).  
- **Type 2:** Network LSA (DR tarafından üretilir).  
- **Type 3:** Summary LSA (ABR özetleme için).  
- **Type 4:** ASBR Summary (ASBR’ye yol bilgisi).  
- **Type 5:** External LSA (dış rotalar).  
- **Type 7:** NSSA External (Type 5’in NSSA versiyonu).  

---

## 📊 Multi-Area Avantajları
- LSDB boyutu küçülür → Router’lar daha hızlı SPF hesaplar.  
- Trafik yükü dengelenir → CPU ve hafıza kullanımı azalır.  
- Daha hızlı konverjans → Hata durumunda SPF daha az alanda hesaplanır.  
- Özetleme (summarization) mümkün olur → Routing tabloları sadeleşir.  

---

## ⚠️ Dezavantajlar
- Tasarım ve konfigürasyon daha karmaşık.  
- Yanlış area planlaması → erişim problemleri.  
- ABR’lerde ek CPU yükü (çok area bilgisi tutar).  
- Backbone (Area 0) olmadan yapı kurulamaz (virtual-link dışında).  

---

## 🔑 Önemli Kurallar
- Her area, **Area 0’a doğrudan bağlı olmalı**.  
- Eğer doğrudan bağlı değilse, **virtual-link** ile bağlanabilir (ama önerilmez).  
- ABR üzerinde area özetleme yapılabilir (`area X range`).  
- Stub ve NSSA alanlarda varsayılan rota genellikle **ABR tarafından** dağıtılır.  

---

# 🔹 Workaround ve OSPF Virtual-Link

## Workaround Nedir?
- **Workaround**, bir sorunu kalıcı olarak çözmek yerine, geçici veya dolaylı bir yöntemle çalışır hale getirmektir.  
- Yani asıl problemi çözmek yerine "işi yürütmek için bir yol" sağlar.

## OSPF Virtual-Link Neden Önerilmez?
- Virtual-link, **Area 0’a doğrudan bağlantısı olmayan bir OSPF alanını backbone’a bağlamak için geçici çözümdür**.  
- Dezavantajları:
  - Karmaşık yapılandırma ve yönetim zorluğu
  - Hatalara açık ve stabil olmayan topoloji
  - Büyük ağlarda ölçeklenemez

**Önerilen tasarım:**  
- Tüm alanlar backbone (Area 0) ile **doğrudan bağlantılı olmalı**.  
- Virtual-link yalnızca **geçici veya kaçınılmaz durumlarda** kullanılmalıdır.
