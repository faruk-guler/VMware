# Güvenlik, İzinler ve Rol Tabanlı Erişim (RBAC)

vSphere güvenliğinin temelinde, doğru kişiye doğru yetkinin verilmesi prensibi yatar.

## 1. Single Sign-On (SSO) ve Kimlik Kaynakları
vCenter, kullanıcıları yönetmek için kendi iç veritabanını (`vsphere.local`) kullanabildiği gibi dış kaynaklara da bağlanabilir:
- **Active Directory (AD):** Kurumsal ortamlarda en yaygın kullanılan yapıdır.
- **OpenLDAP:** Açık kaynaklı dizin servisleri.

## 2. İzin Mekanizması (Permissions)
vSphere'de bir izin üç bileşenden oluşur:
1. **User/Group:** Kim? (Örn: `domain\admin`)
2. **Role:** Ne yapabilir? (Örn: `Virtual Machine User`)
3. **Object:** Nerede yapabilir? (Örn: `Production-Cluster`)

## 3. Varsayılan Roller
- **Administrator:** Her şeye tam yetki.
- **Read-only:** Sadece görüntüleme, ayar değiştiremez.
- **No access:** Hiçbir şeyi göremez.
- **VM Power User:** VM'leri kapatıp açabilir ve bazı ayarları değiştirebilir.

## 4. Güvenlik Best Practices
- **En Az Yetki İlkesi (Principle of Least Privilege):** Kullanıcılara sadece işlerini yapmaları için gereken minimum yetkiyi verin.
- **ESXi Firewall:** Gerekmeyen servis portlarını kapalı tutun.
- **Lockdown Mode:** ESXi host'a doğrudan (DCUI/SSH) girişi engelleyerek tüm yönetimi vCenter üzerinden zorunlu kılın.
- **Sertifika Yönetimi:** Kendinden imzalı (self-signed) sertifikalar yerine güvenilir bir CA'dan alınan sertifikaları kullanın.
