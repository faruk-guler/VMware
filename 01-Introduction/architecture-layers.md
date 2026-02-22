# VMware vSphere Mimari Katmanları

VMware vSphere, modern veri merkezlerinde sanallaştırma altyapısının temelini oluşturur. Sistem dört ana katmandan oluşur:

```markdown
+-------------------------+
|   Server Virtualization | <-- vSphere (ESXi & vCenter)
+-------------------------+
              v
+-------------------------+
|  Network Virtualization | <-- NSX-T / vDS
+-------------------------+
              v
+-------------------------+
|  Storage Virtualization | <-- vSAN / vVOL / VMFS
+-------------------------+
              v
+-------------------------+
|  Desktop Virtualization | <-- Horizon (VDI)
+-------------------------+
```

## Temel Bileşenler

### 1. VMware ESXi
- Tip-1 Hypervisor (Bare-metal).
- Fiziksel donanım üzerinde doğrudan çalışır.
- Sanal makinelerin (VM) çalıştırılmasından sorumludur.

### 2. VMware vCenter Server
- ESXi host'larının merkezi yönetim platformudur.
- vMotion, HA, DRS ve depolama yönetimi gibi gelişmiş özellikleri sağlar.
- HTML5 tabanlı vSphere Client arayüzü ile yönetilir.

### 3. vSphere Client
- Yöneticilerin vCenter veya doğrudan ESXi host'larına bağlanmak için kullandığı web tabanlı arayüzdür.

### 4. Platform Services Controller (PSC)
- Kimlik doğrulama, sertifika yönetimi ve lisanslama gibi altyapı servislerini sağlar. (Modern sürümlerde vCenter içine gömülüdür).
