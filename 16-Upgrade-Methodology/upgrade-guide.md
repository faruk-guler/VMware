# Versiyon Yükseltme (Upgrade) Metodolojisi

vSphere ortamını yeni versiyonlara yükseltirken (örneğin 7.0'dan 8.0'a) belirli bir sıra ve strateji izlemek kesinti süresini ve riskleri minimize eder.

## 1. Yükseltme Sırası (Upgrade Order)
VMware tarafından önerilen kritik yükseltme sırası şu şekildedir:
1.  **vCenter Server:** Her zaman ilk olarak vCenter yükseltilir.
2.  **ESXi Hosts:** vCenter yükseltildikten sonra host'lar tek tek (veya vLCM ile) güncellenir.
3.  **VMware Tools:** Sanal makineler üzerindeki sürücüler güncellenir.
4.  **VM Hardware:** Sanal makine donanım versiyonu yükseltilir.
5.  **VMFS:** Depolama dosya sistemi güncellenir.

## 2. vCenter In-place Upgrade Adımları
vCSA (vCenter Server Appliance) yükseltmesi iki aşamalıdır:
- **Aşama 1 (Deployment):** Yeni versiyona sahip geçici bir vCenter VM'i kurulur.
- **Aşama 2 (Data Migration):** Eski vCenter'daki veriler (konfigürasyon, DB) yeni VM'e aktarılır, eski VM kapatılır ve yeni VM eskisinin IP/Hostname'ini devralır.

## 3. Ön Hazırlık Listesi (Pre-Upgrade Checklist)
- [ ] **HCL Kontrolü:** Donanımın yeni versiyonla uyumlu olduğunu kontrol edin.
- [ ] **Backup:** vCenter ve kritik VM'lerin yedeğini alın.
- [ ] **Interoperability:** Backup ve Monitoring araçlarının yeni versiyonu desteklediğinden emin olun.
- [ ] **Disk Alanı:** `/` ve `/storage/archive` bölümlerinde yeterli yer olduğundan emin olun.

## 4. Geri Dönüş Planı (Rollback)
Eğer yükseltme başarısız olursa:
- vCenter için eski VM'i tekrar açın (Yükseltme öncesi aldığınız snapshot/backup ile).
- ESXi için "Rollback" özelliğini (Boot sırasında Shift+R) kullanarak bir önceki versiyona dönün.
