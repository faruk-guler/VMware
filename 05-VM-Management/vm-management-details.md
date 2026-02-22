# Sanal Makine (VM) Yönetimi ve Dosya Yapısı

Sanal makine, bir fiziksel sunucunun sunduğu kaynakları (CPU, RAM, Disk, Network) yazılımsal olarak simüle eden yapıdır.

## 1. Sanal Makine Dosyaları
Bir VM klasörü içinde yer alan temel dosyalar şunlardır:

- **`.vmx` (Configuration File):** VM'in donanım ayarlarını tutan metin dosyası. ✅
- **`.vmdk` (Disk Descriptor):** Sanal diski tanımlayan dosya (pointer).
- **`-flat.vmdk` (Disk Data):** Verilerin fiziksel olarak tutulduğu büyük dosya.
- **`.nvram` (BIOS/EFI):** VM'in BIOS veya EFI ayarlarını saklar. ✅
- **`.vswp` (Swap File):** RAM yetmediğinde disk üzerinde kullanılan takas dosyası.
- **`.log` (Log Files):** VM'in çalışma loglarını tutar.
- **`.vmtx` (Template):** Template olarak işaretlenmiş VM'in yapılandırma dosyası.

## 2. VMware Tools Neden Kritiktir?
VMware Tools, Guest OS (Misafir İşletim Sistemi) içine kurulan ve şu avantajları sağlayan bir sürücü paketidir:
- **Video Çözünürlüğü:** SVGA sürücüsü ile optimize görüntü.
- **Ağ Performansı:** VMXNET3 sürücü desteği.
- **Bellek Yönetimi:** Balloon driver ile etkin RAM kullanımı.
- **Zaman Senkronizasyonu:** Host ve Guest saatlerinin eşlenmesi.
- **Yönetim:** VM'i düzgün kapatma (Soft Reboot/Shutdown) yeteneği.

## 3. vCPU ve Çekirdek Atama (Mapping)
vCPU (Virtual CPU), fiziksel işlemci çekirdeklerinin (Cores) VM'e paylaştırılmasıdır.
- **Hyper-Threading (HT):** Fiziksel bir çekirdeğin iki "Logical Processor" olarak görülmesini sağlar.
- **vCPU Ratio:** Performans için fiziksel core başına 1-2 vCPU, genel sunucular için 1-4 vCPU oranı önerilir.
- **Wait Time:** Bir VM'e gerekenden çok vCPU atamak "CPU Ready" süresini artırarak performansı düşürebilir.

## 4. Snapshots (Anlık Görüntüler)
- Değişiklikler öncesi geri dönüş noktası oluşturur.
- **Önemli:** Snapshot bir yedekleme (backup) yöntemi değildir! Uzun süreli tutulan snapshot'lar disk performansını düşürür ve depolama alanını kirletir. En fazla 24-72 saat tutulması önerilir.
