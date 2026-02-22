# ESXi Kurulum ve Başlangıç Yapılandırması

VMware ESXi kurulumu, sanallaştırma altyapısının ilk ve en kritik adımıdır.

## 1. Donanım Gereksinimleri ve Uyumluluk
- **CPU:** En az 2 çekirdekli 64-bit x86 işlemci (Intel VT-x veya AMD-V desteği zorunludur).
- **RAM:** En az 8 GB (Üretim ortamı için önerilen minimum 32 GB+).
- **Disk:** ESXi boot için 32 GB+ (SD kart, USB veya yerel disk).
- **HCL Kontrolü:** Donanımın [VMware Compatibility Guide](https://www.vmware.com/resources/compatibility/search.php) üzerinden uyumlu olduğundan emin olun.

## 2. Kurulum Adımları
1. ESXi ISO dosyasını indirin ve bir USB/DVD'ye yazdırın.
2. Sunucuyu medyadan başlatın (Boot).
3. "ESXi Installer" menüsünü seçin.
4. Son Kullanıcı Lisans Sözleşmesini (EULA) kabul edin (F11).
5. Kurulum yapılacak diski seçin.
6. Klavye düzenini (Turkish) seçin.
7. `root` şifresini belirleyin.
8. Kurulumu tamamlayın ve sistemi yeniden başlatın.

## 3. İlk Yapılandırma (DCUI)
Sistem açıldıktan sonra F2 ile **Direct Console User Interface (DCUI)** arayüzüne girin:
- **Configure Management Network:** IP adresi, Subnet Mask ve Gateway ayarlarını yapın.
- **DNS Configuration:** DNS sunucu adreslerini ve Hostname'i belirleyin.
- **IPv6:** Gerekmiyorsa devre dışı bırakın.
- **Test Management Network:** Yapılandırmanın doğruluğunu test edin.

## 4. Web Arayüzüne Erişim
Tarayıcıdan sunucunun IP adresini girerek (`https://<esxi-ip>`) **VMware Host Client** arayüzüne root bilgileriyle giriş yapın.
