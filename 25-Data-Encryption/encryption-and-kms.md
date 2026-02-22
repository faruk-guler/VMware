# Veri Şifreleme ve Anahtar Yönetimi (KMS)

Sanallaştırma ortamındaki verilerin (VM diskleri, vSAN datastore vb.) çalınmaya veya yetkisiz fiziksel erişime karşı korunması için uygulanan şifreleme teknolojileridir.

## 1. vSphere Native Key Provider
vSphere 7.0 U2 ile gelen bu özellik, dışarıdan bir KMS (Key Management Server) satın alma zorunluluğunu ortadan kaldırır.
- **Kendi Kendine Yeten Yapı:** vCenter'ın kendi içinde güvenli bir anahtar üretim merkezi oluşturmasını sağlar.
- **Güvenlik:** Anahtarlar ESXi host'lar arasında güvenli bir şekilde dağıtılır ve yedeklenmesi çok kritiktir.

## 2. vSphere Trust Authority
vSphere 7+ ile gelen, "Trusted Hosts" (Güvenilir Hostlar) kümesi oluşturarak şifreleme anahtarlarının sadece donanımsal olarak doğrulanmış (Attestation) güvenli sunuculara dağıtılmasını sağlayan ileri seviye güvenlik mimarisidir.

## 3. Sanal Makine Şifreleme (VM Encryption)
VM'in `.vmdk` disk dosyalarını ve `.vmx` konfigürasyon dosyalarını şifreler.
- **Hypervisor Seviyesi:** Şifreleme işlemi misafir işletim sisteminden (Guest OS) bağımsız olarak ESXi katmanında yapılır.
- **Performans:** Modern işlemcilerdeki AES-NI komut setini kullanarak performans kaybını minimize eder.

## 4. vSAN Şifreleme (vSAN Encryption)
vSAN datastore üzerindeki tüm verileri (Data-at-Rest) şifreler.
- **Sektör Bazlı Şifreleme:** Veriler diske yazılmadan hemen önce şifrelenir.
- **Deduplication & Compression:** vSAN şifrelemesi, veri tekilleştirme ve sıkıştırma özellikleriyle uyumlu çalışır (önce şifre çözülür, veri işlenir, sonra tekrar şifrelenir).

## 5. TPM ve vTPM Kullanımı
- **Fiziksel TPM:** ESXi host'un açılış güvenliğini (Secure Boot) sağlar.
- **vTPM (Virtual TPM):** Sanal makinelerin "BitLocker" gibi Windows güvenlik özelliklerini kullanabilmesi için gerekli olan sanal güvenlik modülüdür.

## 6. Kritik Uyarı: Anahtar Yedekleme
Native Key Provider veya KMS kullanırken, anahtar setinin (Key Set) yedeğini alıp vCenter dışında güvenli bir yerde saklamak zorunludur. Anahtarlar kaybolursa, şifrelenmiş VM'ler bir daha asla açılamaz.
