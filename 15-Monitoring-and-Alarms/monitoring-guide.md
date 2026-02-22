# İzleme (Monitoring) ve Alarm Yönetimi

vSphere altyapısının sağlığını korumak için performans metriklerinin izlenmesi ve kritik durumlarda uyarı alınması hayati önem taşır.

## 1. vCenter Alarmları
vCenter, nesne bazlı (VM, Host, Datastore) alarmlar tanımlamanıza olanak tanır.
- **Kritik Alarmlar:** Host bağlantı kaybı, VM CPU kullanımı (%90+), Datastore doluluğu.
- **Aksiyonlar (Actions):** Alarm tetiklendiğinde e-posta gönderimi, SNMP trap atımı veya script çalıştırılması.

## 2. Performans Metrikleri
vSphere Client üzerinden "Monitor -> Performance" sekmesinden şu kritik metrikler takip edilmelidir:
- **CPU Ready:** VM'in işlemci sırası bekleme süresi. (%5 üzeri detaylı inceleme gerektirir).
- **Disk Latency:** Depolama erişim gecikmesi. (15-20ms üzeri performans sorunlarına yol açar).
- **Memory Ballooning:** Host'un RAM'i bittiğinde VM'den bellek geri alma işlemi.

## 3. SNMP Yapılandırması
Dış izleme araçları (Zabbix, PRTG, Nagios vb.) ile entegrasyon için ESXi üzerinde SNMP etkinleştirilmelidir:
```bash
esxcli system snmp set -r
esxcli system snmp set -c public
esxcli system snmp set -e yes
```

## 4. VMware Aria Operations (vROps)
Büyük ölçekli ortamlar için gelişmiş analitik, kapasite planlama ve proaktif sorun giderme sağlayan profesyonel izleme çözümüdür.
