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

## vCenter High Availability (VCHA)
vCenter'ın kendisinin kesintisiz çalışmasını sağlayan bir yapıdır. Üç düğümden (Node) oluşur:
- **Active Node:** vCenter servislerinin çalıştığı ana sunucu.
- **Passive Node:** Verilerin aktif düğümden senkronize edildiği yedek sunucu.
- **Witness Node:** "Split-brain" durumlarını önlemek için oylama yapan küçük bir bileşen.
Active düğüm çökerse, Passive düğüm otomatik olarak (5 dakikadan kısa sürede) devralır.

## Hybrid Cloud ve Multi-Cloud Vizyonu
vSphere sadece yerel veri merkezinde değil; **VMware Cloud on AWS**, Azure VMware Solution ve Google Cloud VMware Engine gibi platformlarla hibrit bulut mimarisinde de merkez rol oynar.
