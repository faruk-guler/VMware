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

## 3. Best Practices (En İyi Uygulamalar)
- **Multipathing:** Depolama erişimi için en az iki fiziksel yol (path) kullanın.
- **Round Robin:** Yüksek performans için Native Multipathing (NMP) seçiminde "Round Robin" politikasını tercih edin.
- **Jumbo Frames:** iSCSI ve vSAN trafiği için MTU değerini 9000 olarak ayarlayın.
- **Disk Filling:** Datastore doluluk oranını %80-%85'in altında tutmaya özen gösterin.
