# Depolama (Storage) Yönetimi

vSphere ortamında sanal makinelerin dosyalarını saklamak için kullanılan alanlara **Datastore** denir.

## 1. Datastore Türleri
- **VMFS (Virtual Machine File System):** VMware'in kümelenmiş (clustered) dosya sistemidir. Blok tabanlı depolama (Fiber Channel, iSCSI, Local Disk) için kullanılır.
- **NFS (Network File System):** Dosya tabanlı depolama üzerinden erişilir. Standart NAS cihazları ile kullanılır.
- **vSAN (Virtual SAN):** Host'ların üzerindeki yerel diskleri birleştirerek paylaşımlı bir depolama havuzu oluşturur. (Yazılım tabanlı depolama).
- **vVOLs (Virtual Volumes):** Depolama dizisinin (Storage Array) VM bazlı yönetimini sağlar.

## 2. iSCSI Depolama Yapılandırması
Bir iSCSI target'ı bağlamak için izlenmesi gereken adımlar:
1. **vSwitch ve VMkernel Port:** iSCSI trafiği için özel bir VMkernel portu oluşturun.
2. **Software iSCSI Adapter:** ESXi üzerinde iSCSI adaptörünü etkinleştirin.
3. **Dynamic Discovery:** iSCSI sunucusunun (Target) IP adresini ekleyin.
4. **Rescan:** Depolama bağdaştırıcılarını tarayarak LUN'ları görün.
5. **New Datastore:** "New Datastore" sihirbazı ile VMFS bölümünü oluşturun.

- **Disk Filling:** Datastore doluluk oranını %80-%85'in altında tutmaya özen gösterin.

## 4. İleri Seviye Depolama Teknolojileri
- **NVMe-over-Fabrics (NVMe-oF):** Geleneksel SCSI protokolüne göre çok daha yüksek IOPS ve düşük gecikme (latency) sağlar. vSphere 7.0+ ile desteklenir.
- **vSphere Virtual Volumes (vVOLs):** Depolama yönetimini LUN bazlı olmaktan çıkarıp VM bazlı hale getirir. Storage Policy Based Management (SPBM) ile entegre çalışır.

## 5. Storage DRS (SDRS) ve SIOC
Depolama kaynaklarının otomatik yönetimi için:
- **Storage DRS:** Birden fazla datastore'u bir "Datastore Cluster" içinde toplar. Disk doluluk oranı veya I/O gecikmesine göre VM disklerini datastore'lar arasında otomatik taşır.
- **Storage I/O Control (SIOC):** Belirli bir VM'in veya uygulamanın depolama trafiğini diğer VM'lere karşı önceliklendirmesini sağlar (Shares/Limits).
