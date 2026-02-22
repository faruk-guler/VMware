# Canlı Taşıma (Migration) Teknolojileri

vMotion, VMware'in en devrimsel özelliklerinden biridir ve sanal makinelerin servis kesintisi olmadan taşınmasını sağlar.

## 1. vSphere vMotion (Compute Migration)
- VM'in o anki çalışma durumunu (RAM içeriği, CPU state) ağ üzerinden başka bir host'a aktarır.
- **Kesinti Süresi:** Sıfır (Kullanıcılar hissetmez).
- **Gereksinim:** 
  - Host'lar arası vMotion trafiği için dedike ağ (VMkernel port).
  - CPU uyumluluğu (EVC Mode gerekebilir).

## 2. vSphere Storage vMotion
- VM dosyalarını (Diskleri) bir datastore'dan diğerine taşır.
- VM çalışmaya devam ederken depolama alanı değişmiş olur.
- **Senaryo:** Eski bir depolama ünitesinden (Storage) yenisine geçiş veya disk doluluk oranını dengeleme.

## 3. Shared-Nothing vMotion
- Hem host'un hem de depolamanın aynı anda değiştiği taşıma türüdür.
- Paylaşımlı depolama (Shared Storage) olmayan ortamlar arası geçişte kullanılır.

## 4. Enhanced vMotion Compatibility (EVC)
Farklı jenerasyon işlemcilere sahip host'lar barındıran cluster'larda, vMotion işleminin CPU uyumsuzluğu nedeniyle hata vermesini önler.

- **Nasıl Çalışır?** Cluster seviyesinde "ortak bir payda" belirlenir. Örneğin; bir host Intel Ice Lake, diğeri Intel Skylake ise, cluster EVC seviyesi Skylake olarak ayarlanırsa her iki host da VM'e sadece Skylake özelliklerini sunar.
- **Avantajı:** Eski sunucuları yeni cluster'lara dahil ederken veya donanım yenilerken VM'leri kapatmadan geçiş yapmayı sağlar.
- **Not:** EVC'yi yükseltmek için VM'lerin kapatılıp açılması (Power cycle) gerekir.
