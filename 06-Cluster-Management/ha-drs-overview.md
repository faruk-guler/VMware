# Kümeleme (Cluster) ve Kaynak Yönetimi: HA & DRS

Bir vSphere Cluster, birden fazla ESXi host'un kaynaklarını tek bir havuzda birleştirerek yüksek erişilebilirlik ve performans sağlar.

## 1. High Availability (HA) - Yüksek Erişilebilirlik
HA, bir donanım arızası durumunda kesinti süresini minimize eder.
- **Nasıl Çalışır?** Host'lar "Heartbeat" (nabız) sinyalleri ile birbirini izler. Bir host çökerse, üzerindeki VM'ler diğer sağlam host'lar üzerinde **otomatik olarak yeniden başlatılır.**
- **Gereksinim:** Paylaşımlı depolama (Shared Storage) zorunludur.
- **Admission Control:** Cluster içinde yeni VM başlatılabilmesi için yeterli kaynak yedeği (failover capacity) olup olmadığını kontrol eder.

## 2. Distributed Resource Scheduler (DRS)
DRS, cluster içindeki yükü host'lar arasında dengeler.
- **Nasıl Çalışır?** İşlemci ve bellek taleplerini sürekli izler. Eğer bir host çok yoğunsa, üzerindeki VM'leri vMotion kullanarak daha boş bir host'a **canlı olarak taşır.**
- **Automation Levels:**
  - *Manual:* Öneri sunar, taşımayı yönetici onaylar.
  - *Partially Automated:* VM'in ilk açılacağı host'u seçer, ancak sonrasındaki dengelemeler için onay ister.
  - *Fully Automated:* Her şeyi otomatik yapar (Önerilen).

- **Fault Tolerance (FT):** Sıfır kesinti (Zero Downtime) sağlar. VM'in bir ikizini (shadow copy) başka bir host'ta çalıştırır. Ana VM çökerse, ikizi milisaniyeler içinde devralır.

## 4. Kaynak Havuzları (Resource Pools)
Cluster kaynaklarını (CPU/RAM) departmanlara veya projelere göre bölmek için kullanılır. "Expandable Reservation" özelliği ile dinamik kaynak paylaşımı sağlar.

## 5. Predictive DRS
vRealize Operations (vROps) ile entegre çalışarak, geçmiş verilere dayanarak gelecekteki yük artışlarını tahmin eder ve VM'leri darboğaz oluşmadan önce taşır.
