# Yedekleme (Backup) ve Kurtarma Stratejileri

Sanal makinelerin ve vCenter altyapısının yedeklenmesi, veri kaybına karşı en önemli savunma hattıdır.

## 1. vSphere APIs for Data Protection (VADP)
Modern yedekleme yazılımları (Veeam, Commvault, Veritas vb.) ESXi host'a ajan yüklemek yerine bu API'yi kullanır.
- **Ajansız Yedekleme:** VM içerisinde ajan çalıştırmadan hypervisor seviyesinde veri çekilir.
- **Changed Block Tracking (CBT):** Sadece bir önceki yedekten sonra değişen disk bloklarını tespit eder. Bu sayede yedekleme süresi ve depolama alanı %90'a varan oranda azalır.

## 2. Snapshot Bazlı Yedekleme Akışı
1. Yedekleme yazılımı vCenter'dan bir snapshot oluşturulmasını ister.
2. VM diski dondurulur ve değişen veriler yeni bir dosyaya yazılmaya başlar.
3. Yedekleme yazılımı asıl disk dosyasını (flat-vmdk) okur ve kopyalar.
4. İşlem bitince snapshot silinir ve veriler ana diskle birleştirilir (Consolidation).

## 3. vSphere Replication
Verilerin bir host'tan veya veri merkezinden diğerine asenkron olarak kopyalanmasıdır.
- **RPO (Recovery Point Objective):** Veri kaybı toleransı (Örn: 15 dakika).
- **Kullanım:** Donanım arızası veya site kaybı durumunda VM'lerin diğer uçta hızlıca ayağa kaldırılması için kullanılır.

## 4. vCenter Server Backup (File-Based)
vCenter'ın kendisi VAMI (`https://vcenter-ip:5480`) üzerinden yedeklenmelidir:
- **Protokoller:** FTPS, HTTP, HTTPS, SCP, NFS.
- **İçerik:** vCenter veritabanı, konfigürasyon ve envanter bilgileri.
