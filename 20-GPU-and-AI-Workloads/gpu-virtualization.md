# GPU Sanallaştırma ve AI/ML İş Yükleri

Modern veri merkezlerinde Yapay Zeka (AI), Derin Öğrenme (Deep Learning) ve Grafik Tasarım iş yükleri için fiziksel GPU kaynaklarının sanallaştırılması kritik öneme sahiptir.

## 1. NVIDIA vGPU (Virtual GPU)
Bir fiziksel GPU'nun dilimlenerek (Slicing) birden fazla sanal makine tarafından aynı anda kullanılmasını sağlar.
- **vGPU Profiles:** Her VM'e ne kadar GPU belleği (VRAM) ve işlem gücü verileceğini belirler (Örn: `grid_p4-2q`).
- **NVIDIA Licensing:** vGPU kullanımı için NVIDIA lisans sunucusu gereklidir.

## 2. VMware vSphere DirectPath I/O (Passthrough)
Fiziksel bir PCI aygıtını (GPU, FPGA vb.) doğrudan bir sanal makineye atar. 
- **Performans:** "Bare-metal" performansına en yakın sonucu verir.
- **Kısıtlama:** vMotion ve Snapshot gibi özellikleri devre dışı bırakabilir (Modern sürümlerde GPU passthrough ile vMotion desteği limitli de olsa mevcuttur).

## 3. Bitfusion ve Dinamik GPU Paylaşımı
vSphere 7+ ile gelen Bitfusion teknolojisi, GPU kaynaklarını ağ üzerinden bir havuz haline getirerek VM'lerin ihtiyacı olduğunda bu havuzdan GPU gücü almasını sağlar.

## 4. AI/ML Optimizasyonları
- **vMotion for GPU:** vSphere 7.0 Update 1 ile birlikte NVIDIA vGPU kullanan sanal makinelerin canlı taşınması (stun time minimize edilerek) desteklenmektedir.
- **Ready for AI:** VMware'in NVIDIA ile ortaklaşa geliştirdiği "AI-Ready Enterprise Platform" mimarisi.
