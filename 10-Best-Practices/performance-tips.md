# vSphere En İyi Uygulamalar (Best Practices) ve Performans İpuçları

Sanallaştırma altyapınızın kararlı ve performanslı çalışması için aşağıdaki önerilere uyun.

## 1. İşlemci ve Bellek Yönetimi
- **Right-sizing:** VM'lere ihtiyaç duyduğundan fazla vCPU veya RAM atamayın. Gereksiz kaynak ataması "CPU Ready" süresini artırarak cluster genelinde performans kaybına yol açar.
- **NUMA Awareness:** VM bellek boyutunu, fiziksel host'un bir NUMA düğüm kapasitesini aşmayacak şekilde belirleyin.
- **Reserved Memory:** vCenter ve kritik VM'ler (Domain Controller vb.) için RAM rezervasyonu yapmayı düşünün.

## 2. Depolama Performansı
- **Paravirtual SCSI (PVSCSI):** Yüksek I/O gerektiren VM'ler için LSI Logic yerine PVSCSI adaptörünü kullanın.
- **Thick vs. Thin Provisioning:** Performans kritik (Database vb.) VM'ler için "Thick Provision Eager Zeroed" disk türünü, genel VM'ler için alan tasarrufu sağlayan "Thin Provision" türünü tercih edin.
- **Unmap:** Silinen verilerin depolama tarafında da serbest kalması için konuk işletim sisteminde "UNMAP" desteğini etkinleştirin.

## 3. Ağ Yapılandırması
- **VMXNET3:** Her zaman en son nesil sanal ağ adaptörü olan VMXNET3'ü kullanın.
- **Separate Traffic:** Management, vMotion ve Storage trafiğini fiziksel veya VLAN bazında mutlaka birbirinden ayırın.
- **Load Balancing:** Fiziksel portlar arasında en verimli yük dağılımı için "Route based on physical NIC load" (VDS gerektirir) ayarını kullanın.

## 4. Genel Operasyonlar
- **Time Sync:** Tüm host'ların ve vCenter'ın aynı NTP sunucusundan zaman aldığından emin olun. Saat farkı kimlik doğrulama hatalarına yol açar.
- **Updates:** ESXi ve vCenter yamalarını (Patches) düzenli olarak uygulayın.
- **Log Management:** Logları merkezi bir sunucuya (vRealize Log Insight vb.) aktarın.
- **Naming Convention:** VM, vSwitch ve Port Grup isimlendirmelerinde standart bir format (Örn: `VM_PROD_DB01`) belirleyin.
