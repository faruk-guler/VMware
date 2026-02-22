# Gelişmiş Ağ Yönetimi (VDS & NIOC)

vSphere Distributed Switch (VDS), sadece merkezi yönetim sunmakla kalmaz, aynı zamanda kurumsal ağ ihtiyaçları için kritik performans ve izleme özellikleri sağlar.

## 1. LACP (Link Aggregation Control Protocol)
Fiziksel Switch ve ESXi host arasındaki uplink'leri sanal tek bir kanal (Port Channel) olarak birleştirir.
- **Avantaj:** Bant genişliğini artırır ve fiziksel link arızalarına karşı yedeklilik sağlar.
- **Gereksinim:** Fiziksel switch tarafında da LACP yapılandırması yapılmalıdır.

## 2. Network I/O Control (NIOC - Version 3)
Ağ kaynaklarının trafik türlerine göre (vMotion, Management, VM Traffic, iSCSI) önceliklendirilmesini sağlar.
- **Shares:** Ağ darboğazı oluştuğunda kimin ne kadar bant genişliği alacağını belirler.
- **Reservation:** Kritik trafik türlerine (Örn: iSCSI) minimum bant genişliği garantisi verir.
- **Limit:** Belirli bir trafik türünün toplam bant genişliğini aşmamasını sağlar.

## 3. Port Mirroring ve NetFlow
Ağ trafiğinin analizi ve güvenliği için kullanılır:
- **Port Mirroring (RSPAN/ERSPAN):** Bir porttaki trafiği analiz cihazına (IDS/IPS veya Wireshark) aynalar.
- **NetFlow:** IP trafik istatistiklerini toplayarak ağ akış diyagramlarını görmenizi sağlar.

## 4. MAC Learning
vSphere 6.7+ ile gelen bu özellik, iç içe geçmiş (nested) sanallaştırma veya konteyner yapılarında ağ performansını artırır ve Promiscuous Mode bağımlılığını azaltır.
