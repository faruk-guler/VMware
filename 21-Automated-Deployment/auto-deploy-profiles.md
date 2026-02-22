# Otomatik Dağıtım (Auto Deploy) ve Host Profiles

Büyük ölçekli veri merkezlerinde (100+ host), sunucu kurulumlarını standartlaştırmak ve otomatize etmek için kullanılan üst düzey yönetim araçlarıdır.

## 1. VMware vSphere Auto Deploy
ESXi host'ların yerel disk veya SD kart olmadan, ağ üzerinden (PXE Boot) açılmasını sağlayan bir teknolojidir.
- **Stateless (Durum bilgisi olmayan):** ESXi imajı host'un RAM'inde çalışır. reboot sonrası imaj tekrar ağdan yüklenir.
- **Stateful Install:** Auto Deploy, imajı host'un yerel diskine kalıcı olarak kurmak için de kullanılabilir.
- **Bileşenler:** TFTP Server, DHCP Server, vCenter Auto Deploy Service ve Image Builder.

## 2. Host Profiles
Bir "Referans Host" üzerinden alınan konfigürasyonun, cluster içindeki diğer tüm host'lara uygulanmasını sağlar.
- **Standartlaşma:** Tüm sunucuların (NTP, DNS, vSwitch, Firewall vb.) ayarlarının birebir aynı olmasını garanti eder.
- **Compliance Check:** Bir host'un profil ile uyumlu olup olmadığını denetler. Eğer sapma (drift) varsa "Remediate" butonu ile saniyeler içinde düzeltir.

## 3. Çalışma Mantığı
1.  **Image Builder:** İstenilen sürücüleri içeren bir ESXi Image Profile oluşturulur.
2.  **Deploy Rule:** Hangi donanımın hangi imajı ve hangi Host Profile'ı alacağı belirlenir.
3.  **Boot:** Sunucu açıldığında vCenter'a danışır, imajı ve konfigürasyonu alarak ayağa kalkar.

## 4. Kullanım Senaryosu
- **Cloud Service Providers:** Yeni bir fiziksel sunucu rafa takılıp ağa bağlandığında, hiçbir manuel işlem yapılmadan dakikalar içinde cluster'a dahil olur.
- **Bakım (Patching):** Sadece vCenter üzerindeki merkezi imajı güncelleyerek binlerce sunucuyu tek seferde güncel tutma imkanı sağlar.
