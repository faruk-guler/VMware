# vCenter Server Appliance (vCSA) Disk Temizleme Rehberi

vCenter Server'da `/storage/archive` bölümünün dolması yaygın bir durumdur ve genellikle PostgreSQL WAL loglarından kaynaklanır.

## 1. Sorunun Tespiti (Semptomlar)
- vCenter alarmı: `"Amount of free disk space "/storage/archive" is below a defined threshold"`
- vCenter yedekleme veya yükseltme işlemlerinin hata vermesi.

## 2. Çözüm Adımları

### Adım 1: Hazırlık
Değişiklik yapmadan önce vCenter Server'ın çalışan bir **Snapshot'ını** alın.

### Adım 2: SSH Erişimi ve Shell
vCenter'a SSH ile bağlanın ve shell'i etkinleştirin:
```bash
shell.set --enabled true
shell
```

### Adım 3: Eski Dosyaların Tespiti
Aşağıdaki komut, 300 günden eski arşivlenmiş WAL segmentlerini listeler:
```bash
find /storage/archive/vpostgres/ -mtime +300 -print
```

### Adım 4: Otomatik Temizlik İşlemi (Cronjob)
Disk doluluğunun tekrar etmemesi için her gece çalışacak bir görev ekleyin:
1. `crontab -e` komutunu çalıştırın.
2. En alt satıra şunu ekleyin:
   ```bash
   0 23 * * * find /storage/archive/vpostgres/ -mtime +300 | xargs rm
   ```
   *(Bu komut her gece saat 23:00'te 300 günden eski dosyaları siler).*
3. `Esc` tuşuna basın ve `:wq` yazarak kaydedip çıkın.

## 3. Alternatif: Disk Genişletme
Eğer temizlik yetersiz kalırsa, vCenter sanal makinesinin donanımından ilgili diski artırdıktan sonra işletim sistemine şu komutu verin:
```bash
vpxd-service-control --stop vmware-vpxd
/usr/lib/applmgmt/support/scripts/autogrow.sh
vpxd-service-control --start vmware-vpxd
```

## 4. vCenter Appliance Management Interface (VAMI)
Arayüz üzerinden yönetim için `https://<vcenter-ip>:5480` adresini kullanın. VAMI size şu imkanları sunar:
- **Health Status:** Servislerin ve disklerin sağlık durumunu izleme.
- **Update:** vCenter güncellemelerini tetikleme.
- **Backup:** Dosya tabanlı (File-based) yedekleme planlama.
- **Network:** IP ve DNS ayarlarını canlı olarak değiştirme.

## 5. vCenter High Availability (vCenter HA)
vCenter Server'ın kendisinin çökmesine karşı koruma sağlar.
- **Yapı:** 1 Active, 1 Passive ve 1 Witness node'dan oluşur.
- **Failover:** Active node çökerse Passive node saniyeler içinde yönetimi devralır.
- **Gereksinim:** Self-managed bir vCenter ortamı ve vCenter HA ağı için özel bir subnet.

## 6. Gelişmiş Sorun Giderme Araçları
- **ESXTOP:** ESXi host'un kaynak kullanımını (CPU Ready, Disk Latency vb.) komut satırından anlık izlemek için kullanılır. SSH üzerinden `esxtop` komutuyla çalıştırılır.
- **Log Analizi:** Kritik sistem logları `/var/log/vmkernel.log` dosyasında tutulur. `tail -f /var/log/vmkernel.log` komutuyla canlı izlenebilir.

> **Not:** Arşiv partition'ının dolması vCenter'ın durmasına neden olmaz ancak yönetimsel işlemleri engelleyebilir.
