# Yaşam Döngüsü Yönetimi (Lifecycle Management)

vSphere ortamında host'ların, VM donanımlarının ve araçlarının (Tools) güncel tutulması güvenlik ve performans için kritiktir.

## 1. vSphere Lifecycle Manager (vLCM)
vLCM, host yönetimi için kullanılan yeni nesil çözümdür. 

- **İmaj Tabanlı Yönetim:** Bir cluster'daki tüm host'lar için tek bir "Desired State" (Hedef Durum) belirlenir. Bu imaj; ESXi versiyonu, sürücüler (drivers) ve firmware bilgilerini içerir.
- **Remediation:** Bir host belirlenen imajdan farklıysa, vLCM bu farkı tespit eder ve host'u hedef duruma getirmek için günceller.
- **Donanım Uyumluluğu:** Sunucu üreticilerinin (HPE, Dell, Lenovo vb.) araçlarıyla entegre çalışarak firmware güncellemelerini de vCenter üzerinden yapabilir.

## 2. vSphere Update Manager (Baselines) - Klasik Yöntem
Eski sürümlerde ve imaj moduna geçmemiş cluster'larda kullanılır.
- **Patch Baseline:** Kritik güvenlik yamalarını içeren liste.
- **Stage & Remediate:** Yamaların host'a önceden yüklenmesi (Stage) ve ardından uygulanması (Remediate).

## 3. Sanal Makine Güncellemeleri
- **VMware Tools:** Guest OS performans sürücülerini günceller. "Check and upgrade VMware Tools before each power on" seçeneği ile otomatikleştirilebilir.
- **VM Hardware Version:** Sanal makinenin taklit ettiği donanım seviyesidir. Yeni özelliklerden yararlanmak için (Örn: vNVMe desteği) bu sürümün yükseltilmesi gerekir.

> [!CAUTION]
> Hardware Version yükseltme işlemi geri alınamaz. İşlemden önce mutlaka VM yedeği veya snapshot alınmalıdır.
