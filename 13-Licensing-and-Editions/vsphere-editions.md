# vSphere Sürümleri ve Lisanslama Rehberi

VMware vSphere, farklı ölçekteki ihtiyaçlar için çeşitli sürümler ve lisanslama modelleri sunar.

## 1. ESXi Sürümleri (Edition)
- **vSphere Standard:** Temel sanallaştırma özellikleri, HA ve vMotion içerir. Küçük ve orta ölçekli işletmeler için uygundur.
- **vSphere Enterprise Plus:** DRS, vDS (Distributed Switch), Host Profiles ve Proactive HA gibi ileri seviye özellikleri içerir.
- **vSphere+:** Abonelik tabanlı bulut bağlantılı yönetim modeli.

## 2. vCenter Server Sürümleri
vCenter, yöneteceği host sayısına göre lisanslanır:
- **vCenter Server Essentials:** Sadece Essentials paketleri ile gelir (Maksimum 3 Host).
- **vCenter Server Foundation:** Küçük ortamlar için (Maksimum 4 Host).
- **vCenter Server Standard:** Sınırsız sayıda host yönetimi ve tüm özellikler.

## 3. Kritik Özellik Karşılaştırması

| Özellik                | Standard | Enterprise Plus |
|------------------------|:--------:|:---------------:|
| **vMotion**            | ✅       | ✅             |
| **High Availability**  | ✅       | ✅             |
| **DRS**                | ❌       | ✅             |
| **Distributed Switch** | ❌       | ✅             |
| **Host Profiles**      | ❌       | ✅             |
| **SR-IOV**             | ❌       | ✅             |

## 4. Lisanslama Değişiklikleri (Broadcom Sonrası)
Yeni modeller genellikle kurumsal paketler (vSphere Foundation veya VMware Cloud Foundation) halinde abonelik bazlı sunulmaktadır. Lisans alırken CPU çekirdek sayısı (Core based) dikkate alınır.
