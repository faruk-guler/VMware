# VMware vSphere Profesyonel Sanallaştırma Kütüphanesi

Bu proje, kurumların veri merkezlerinde kullandığı **VMware vSphere** ekosistemini uçtan uca kapsayan, her seviyedeki sistem mühendisi ve yöneticisi için tasarlanmış devasa bir bilgi bankasıdır. Basit bir dökümantasyondan öte, bu çalışma vSphere dünyasının kurulumu, güvenliği, sürekliliği ve optimize edilmesi için bir ana rehber niteliğindedir.

---

## 🏗 Proje Kapsamı ve Detaylı Teknik Modüller

Proje, birbirini tamamlayan 26 stratejik modülden oluşmaktadır. Her bir modül, vSphere altyapısının farklı bir kritik alanına odaklanmaktadır:

### 1. Mimari ve Temel Kavramlar (Introduction)
Modern veri merkezlerinin "Software-Defined Data Center" (SDDC) vizyonundaki VMware katmanlarını inceler. ESXi hypervisor yapısı, vCenter Server'ın yönetimsel rolü ve vSphere Client'ın hiyerarşisi burada detaylandırılır. Sistemdeki katmanlar arasındaki veri akışını anlamak için temel oluşturur.

### 2. Kurulum ve İlk Yapılandırma (Installation)
Bare-metal sunucular üzerine ESXi kurulumunun teknik gereksinimlerini (HCL uyumluluğu gibi) ve DCUI üzerinden yapılan kritik başlangıç ayarlarını kapsar. Host'un networke erişimi, DNS yapılandırması ve yönetimsel ilk giriş adımları burada adım adım tarif edilir.

### 3. Depolama Yönetimi (Storage)
Sanallaştırmanın kalbi olan depolama katmanını; VMFS dosya sistemi, NFS depolama ve yazılım tabanlı vSAN yapılarını ele alarak açıklar. iSCSI adaptörlerinin yapılandırılması, LUN yönetimi ve multipathing politikaları ile yüksek performanslı veri erişim yollarını detaylandırır.

### 4. Ağ Tasarımı ve Güvenliği (Networking)
Sanal ağ trafiğinin izolasyonu ve güvenliği için Standart Switch (VSS) ve Distributed Switch (VDS) mekanizmalarını karşılaştırır. Port grupları, VMkernel servisleri ve sanal ağda trafik güvenliği için uygulanan güvenlik politikalarını (Promiscuous mode vb.) derinlemesine işler.

### 5. Sanal Makine (VM) Hayat Döngüsü
Bir sanal makinenin disk dosyalarından (.vmdk) konfigürasyon dosyalarına (.vmx) kadar tüm anatomisini inceler. VMware Tools'un konuk işletim sistemi üzerindeki etkisi, vCPU core mapping stratejileri ve snapshot mekanizmasının teknik sınırlarını açıklar.

### 6. Kümeleme ve Süreklilik (HA & DRS)
Veri merkezinde fiziksel sunucu arızalarına karşı High Availability (HA) korumasını ve kaynakların (CPU/RAM) otomatik dengelenmesi için DRS mekanizmasını detaylandırır. Bir Cluster yapısının nasıl ölçekleneceği ve kesintisiz hizmetin nasıl sunulacağı bu bölümün odağıdır.

### 7. Gelişmiş Taşıma Teknolojileri (Migration)
Sanal makinelerin ve disklerinin canlı olarak taşınmasını (vMotion & Storage vMotion) ve farklı işlemci nesillerine sahip sunucular arasında uyumluluğu sağlayan **EVC (Enhanced vMotion Compatibility)** teknolojisini tüm detaylarıyla ele alır.

### 8. Güvenlik ve Yetkilendirme (RBAC)
Sistem yöneticilerinin yetkilerinin belirlendiği Rol Tabanlı Erişim Kontrolü (RBAC) sistemini, SSO (Single Sign-On) entegrasyonlarını ve kurum içi güvenlik politikalarının ESXi/vCenter seviyesinde nasıl uygulanacağını açıklar.

### 9. vCenter Yönetimi ve Troubleshooting (Sorun Giderme)
Gerçek zamanlı sorun giderme stratejilerini içerir. Özellikle vCenter Server Appliance (vCSA) üzerindeki disk doluluğu sorunları, VAMI (Port 5480) arayüz yönetimi ve vCenter HA gibi ileri seviye operasyonel konuları kapsar.

### 10. En İyi Uygulamalar (Best Practices)
Kurumsal bir ortamda sistemin "best-in-class" seviyesine taşınması için gereken; doğru kaynak atama (right-sizing), ağ trafiği segmentasyonu ve depolama optimizasyon yollarını detaylı bir kontrol listesi olarak sunar.

### 11. Yaşam Döngüsü Yönetimi (Lifecycle)
Sunucu ve sanal makine güncellemelerinin vSphere Lifecycle Manager (vLCM) üzerinden imaj tabanlı olarak nasıl yönetileceğini anlatır. Sistemlerin güncel ve güvenli kalması için izlenmesi gereken yolları tarif eder.

### 12. Yedekleme ve Replikasyon (Backup)
VADP API mimarisi, Changed Block Tracking (CBT) teknolojisi ve felaket kurtarma senaryoları (Replikasyon) üzerine kuruludur. Veri kaybını sıfıra indirmek için kurumsal yedekleme yazılımlarının VMware ile nasıl entegre olduğunu açıklar.

### 13. Lisanslama ve Stratejik Seçimler
Broadcom sonrası değişen vSphere lisanslama modellerini, farklı sürümler (Standard vs Enterprise Plus) arasındaki özellik farklarını ve işletmenin ihtiyacına en uygun paketin nasıl seçileceğini detaylandırır.

### 14. Otomasyon ve PowerCLI
Sistem yönetimini PowerShell üzerinden otomatize etmek için PowerCLI kurulumu, temel komut setleri ve örnek script senaryolarını içerir.

### 15. Monitoring ve İzleme
vCenter alarmları, kritik performans metrikleri (CPU Ready, Latency) ve SNMP entegrasyonu ile proaktif izleme stratejilerini kapsar.

### 16. Yükseltme (Upgrade) Metodolojisi
vCenter ve ESXi versiyon yükseltme adımları, yükseltme sırası (interoperability) ve hata durumunda geri dönüş (rollback) planlarını detaylandırır.

### 17. vSAN Derin İnceleme (Deep Dive)
Yazılım tabanlı depolama (vSAN) mimarisi, disk grupları, ESA/OSA farkları ve politika bazlı (SPBM) depolama yönetimini kapsar.

### 18. Disaster Recovery (SRM)
Site Recovery Manager (SRM) ile felaket kurtarma orkestrasyonu, replikasyon yöntemleri ve kurtarma planlarının (Recovery Plans) oluşturulmasını detaylandırır.

### 19. Gelişmiş Ağ Yönetimi (Advanced Networking)
VDS üzerinde LACP, Network I/O Control (NIOC), Port Mirroring ve NetFlow gibi kurumsal ağ özelliklerini kapsar.

### 20. GPU ve AI İş Yükleri
NVIDIA vGPU sanallaştırma, GPU Passthrough (DirectPath I/O) ve vSphere üzerinde AI/ML iş yüklerinin optimizasyonunu içerir.

### 21. Otomatik Dağıtım (Auto Deploy)
Büyük ölçekli ortamlarda Host Profiles ve PXE tabanlı Auto Deploy ile sunucu kurulumlarının standartlaştırılmasını ve otomasyonunu anlatır.

### 22. Güvenlik Sıkılaştırma (Hardening)
VMware Security Configuration Guide standartları, STIG uyumluluğu, sertifika yönetimi ve sistem zırhlama tekniklerini detaylandırır.

### 23. Operasyonel Verimlilik (Content Library & ELM)
Şablon yönetimi (Content Library), Enhanced Linked Mode (ELM) ve politika bazlı (SPBM) depolama yönetimi ile operasyonel hızı artırma yollarını kapsar.

### 24. Gelecek Nesil Mimariler (DPU & SmartNICs)
vSphere 8 ile gelen DPU (Data Processing Unit) desteği ve altyapı servislerinin akıllı ağ kartlarına devredilmesini (Distributed Services Engine) detaylandırır.

### 25. Veri Şifreleme ve KMS
vSphere Native Key Provider, VM Encryption ve vSAN Encryption teknolojileri ile verilerin donanımsal ve yazılımsal olarak zırhlanmasını kapsar.

### 26. Terraform ile vSphere (IaC)
Altyapının kod olarak yönetilmesi (Infrastructure as Code) felsefesini, Terraform vSphere Provider kullanımını ve otomatik VM dağıtım senaryolarını içerir.

---

## 🎯 Projenin Amacı

Bu proje, VMware vSphere dünyasına dair "hiçbir eksik konu kalmaması" hedefiyle oluşturulmuştur. Her modül, sadece teorik bilgi değil, gerçek dünya tecrübelerine dayanan pratik uygulama yollarını ve operasyonel ipuçlarını içermektedir.

---
> [!IMPORTANT]
> Tüm içerikler sistematik olarak klasörlenmiştir. Detaylı içeriklere ve teknik rehberlere ilgili klasörler altındaki dosyalar üzerinden ulaşılabilir.
