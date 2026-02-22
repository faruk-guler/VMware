# Disaster Recovery (DR) ve VMware SRM

Felaket Kurtarma (Disaster Recovery), bir veri merkezinin tamamen kullanılamaz hale gelmesi durumunda servislerin başka bir lokasyonda (Secondary Site) otomatik olarak ayağa kaldırılmasıdır.

## 1. VMware Site Recovery Manager (SRM)
SRM, DR süreçlerini otomatize eden bir orkestrasyon aracıdır.
- **Kesintisiz Test:** Canlı sistemi etkilemeden DR planlarını izole bir ağda test etme imkanı sağlar.
- **Hiyerarşik Kurtarma:** VM'lerin belirli bir sırayla (Örn: Önce DB, sonra App, en son Web) açılmasını sağlar.
- **IP Değiştirme:** VM'lerin yeni lokasyondaki ağ yapısına göre IP adreslerini otomatik günceller.

## 2. Replikasyon Yöntemleri
SRM iki ana replikasyon türüyle çalışabilir:
1.  **Array-Based Replication (ABR):** Depolama ünitesinin (Storage) kendi donanımsal replikasyonunu kullanır. (SRA - Storage Replication Adapter gerektirir).
2.  **vSphere Replication:** Host tabanlı, yazılımsal replikasyon. Donanımdan bağımsızdır.

## 3. Temel Kavramlar
- **Protection Groups:** Birlikte kurtarılması gereken VM grupları.
- **Recovery Plans:** Bir felaket anında veya planlı geçişte izlenecek adımların (adım adım senaryo) listesi.
- **RPO (Recovery Point Objective):** Ne kadar veri kaybına tahammül var? (Örn: 15 dk).
- **RTO (Recovery Time Objective):** Sistemlerin ne kadar sürede ayağa kalkması gerekiyor? (Örn: 1 saat).

## 4. Failover ve Failback
- **Planned Migration:** Sistemler tek düğmeyle düzenli bir şekilde diğer tarafa taşınır (Sıfır veri kaybı).
- **Disaster Recovery:** Ana site çöktüğünde kirli (dirty) replika verilerle sistemler ayağa kaldırılır.
- **Failback:** Sorun giderildikten sonra orjinal site'a geri dönme işlemi.
