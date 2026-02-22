# Operasyonel Verimlilik (Content Library & ELM)

Büyük ölçekli ve çok lokasyonlu vSphere ortamlarında yönetimi merkezileştirmek ve operasyonel hızı artırmak için kullanılan mimari özelliklerdir.

## 1. vSphere Content Library (İçerik Kütüphanesi)
Sanal makine şablonları (templates), ISO dosyaları, scriptler ve OVF paketlerini merkezi bir depoda toplar.
- **Local Library:** Sadece tek bir vCenter içinde kullanılır.
- **Subscribed Library:** Başka bir vCenter'daki kütüphaneyi takip eder ve güncellemeleri (senkronizasyon) otomatik çeker.
- **Version Control:** Şablonlar üzerinde yapılan değişiklikleri versiyonlar (V1, V2 vb.), hata durumunda eski sürüme geri dönmeyi sağlar.

## 2. Enhanced Linked Mode (ELM)
Farklı lokasyonlarda bulunan (veya aynı veri merkezindeki farklı cluster'ları yöneten) birden fazla vCenter sunucusunun tek bir SSO (Single Sign-On) domain'i altında birleştirilmesidir.
- **Single Pane of Glass:** Tüm vCenter'ları, rolleri, izinleri ve envanteri tek bir web arayüzünden (`https://vcenter-site1/ui`) görmenizi ve yönetmenizi sağlar.
- **Kapasite:** 15 adede kadar vCenter sunucusunu birbirine bağlayabilir (Modern sürümlerde).

## 3. vCenter Server Profiles
vCenter ayarlarını bir profil olarak dışarı aktarmanızı (export) ve başka vCenter'lara uygulamanızı (import) sağlar. vCenter konfigürasyonlarını standartlaştırmak için kullanılır.

## 4. Global Inventory Search
ELM sayesinde, binlerce sanal makine arasından arama yaparken tüm veri merkezleri (New York, Londra, İstanbul vb.) taranarak saniyeler içinde sonuca ulaşılır.

## 4. Cross vCenter vMotion
Sanal makineleri sadece host'lar arasında değil, farklı vCenter sunucuları arasında da (farklı veri merkezlerine) canlı olarak taşımayı imkanlı kılar.

## 5. Storage Policy Based Management (SPBM)
Depolama ayarlarını bir kural seti (Policy) olarak belirleyip VM'lere atamayı sağlar.
- **Örn:** "Kritik VM Politikası -> NVMe Disk + RAID 1 + IOPS Limit 5000".
- Depolama donanımı değişse bile politika aynı kalır, sistem uygun diski otomatik seçer.
