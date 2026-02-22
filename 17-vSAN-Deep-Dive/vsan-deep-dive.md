# vSAN Derin İnceleme (Deep Dive)

VMware vSAN, ESXi host'larının yerel disklerini birleştirerek yazılım tabanlı (Software-Defined) paylaşımlı bir depolama havuzu oluşturan clustered depolama çözümüdür.

## 1. Mimari Yapı (Disk Grupları)
vSAN, performans ve kapasiteyi ayırmak için **Disk Grupları** mantığını kullanır:
- **Cache Tier (Önbellek):** Yazma/Okuma hızını artırmak için kullanılan hızlı disk (Flash/NVMe).
- **Capacity Tier (Kapasite):** Verilerin asıl saklandığı bölüm (Flash veya HDD).

### vSAN ESA (Express Storage Architecture) vs OSA
- **OSA (Original):** Geleneksel Disk Grupları yapısını kullanır.
- **ESA:** vSphere 8 ile gelen, disk grubu kavramını ortadan kaldıran ve doğrudan NVMe disklerin gücünü kullanan yeni nesil yüksek performanslı mimari.

## 2. Depolama Politikaları (SPBM)
VMFS'in aksine, vSAN'da veri koruması VM veya disk bazlı belirlenir:
- **RAID 1 (Mirroring):** Verinin bir kopyası diğer host'ta tutulur. En az 3 host gerektirir.
- **RAID 5/6 (Erasure Coding):** Alan tasarrufu sağlar. RAID 5 için en az 4 host, RAID 6 için en az 6 host gerekir.
- **FTT (Failures to Tolerate):** Sistemin kaç host/disk arızasına dayanabileceğini belirler (FTT=1, FTT=2).

## 3. vSAN Witness Host
2-Node cluster veya Stretched Cluster yapılarında "quorum" (karar çoğunluğu) sağlamak için kullanılan hafif bir sanal appliance'dır. Veri saklamaz, sadece meta-veri tutar.

## 4. Avantajlar
- **Scale-out:** Yeni bir host ekleyerek hem işlem (CPU/RAM) hem de depolama kapasitesini aynı anda artırabilme.
- **Yönetim Kolaylığı:** Ayrı bir Storage Admin ihtiyacı olmadan vCenter üzerinden yönetim.
- **Performans:** Verinin işlemciye yakınlığı sayesinde düşük gecikme.
