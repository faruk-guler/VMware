# Güvenlik Sıkılaştırma (Security Hardening)

vSphere altyapısını kurumsal güvenlik standartlarına (STIG, NIST, GDPR vb.) göre zırhlamak için izlenmesi gereken "best-in-class" güvenlik adımlarıdır.

## 1. vSphere Security Configuration Guide
VMware'in her büyük sürüm için yayınladığı resmi sıkılaştırma rehberidir. Temel öneriler:
- **Shell & SSH:** ESXi Shell ve SSH servislerinin sadece gerektiğinde açılması ve ardından otomatik kapanması için zaman aşımı (Timeout) ayarlanması.
- **Mobility:** vMotion trafiğinin şifrelenmesi (Encrypted vMotion).
- **VBS (Virtualization-Based Security):** Windows 10/11 ve Server 2016+ VM'ler için donanımsal güvenlik özelliklerinin (TPM 2.0) sanallaştırılması.

## 2. Kimlik Doğrulama ve Rol Yönetimi
- **MFA (Multi-Factor Authentication):** vCenter girişlerinde akıllı kart (Smart Card) veya RSA gibi çok faktörlü doğrulama kullanımı.
- **Identity Federation:** AD FS veya Okta gibi modern kimlik sağlayıcıları ile entegrasyon.
- **No Permissions on Root:** ESXi host'a root ile doğrudan erişimin kısıtlanması (Lockdown Mode).

## 3. Sertifika Yönetimi (vSphere Certificate Manager)
- **VECS (VMware Endpoint Certificate Store):** Sertifikaların merkezi depolama alanı.
- **VMCA (VMware Certificate Authority):** varsayılan olarak vCenter sertifika üretir. Daha güvenli olması için kurumsal bir CA'dan alınan sertifikaların (Custom Certificates) yüklenmesi önerilir.

## 4. Kaynak İzolasyonu
- **Cores per Socket:** L1 Terminal Fault (L1TF) gibi donanım açıklarına karşı "Side-Channel-Aware Scheduler" yapılandırması.
- **TPM (Trusted Platform Module):** Sunucu donanımındaki fiziksel TPM'in, sanal makineler için "vTPM" olarak sunulması.

## 5. Audit ve Logging
- **Syslog Export:** Tüm logların (ESXi/vCenter) merkezi bir Log Analytics aracına (Aria Operations for Logs vb.) gerçek zamanlı aktarılması.
