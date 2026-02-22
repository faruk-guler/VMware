# Sanal Anahtar (Virtual Switch) Tasarımı ve Ağ Yönetimi

vSphere ağ yapısı, fiziksel NIC'lerin sanal dünyaya aktarılmasını ve trafik izolasyonunu sağlar.

## 1. Sanal Anahtar Türleri

### Standard Switch (VSS)
- Her ESXi host bazında manuel olarak yapılandırılır.
- Basit yapılar için uygundur.
- vSwitch0, vSwitch1 gibi isimler alır.

### Distributed Switch (VDS)
- vCenter seviyesinde merkezi olarak yönetilir.
- Tüm host'lar üzerinde tutarlı bir yapılandırma sağlar.
- **Port Mirroring**, **LACP**, **NetFlow** gibi gelişmiş özellikleri destekler.
- Enterprise Plus lisansı gerektirir.

## 2. Port Grubu Türleri
- **Virtual Machine Port Group:** VM'lerin ağa erişimi için kullanılır.
- **VMkernel Port:** ESXi host'un kendisinin kullandığı servisler (Management, vMotion, vSAN, iSCSI) için kullanılır.

## 3. Önerilen Ağ Yapılandırması (Ayrı Switch Yaklaşımı)

| Ağ Türü            | Kullanım Amacı                                     | vSwitch Önerisi |
|--------------------|----------------------------------------------------|-----------------|
| **Management**     | ESXi host’a erişim, SSH, GUI, SNMP vs.             | Dedicated VSS   |
| **vSphere vMotion**| VM’lerin canlı taşınması (live migration)           | Dedicated VSS   |
| **Production**     | Kullanıcı işlemlerinin yapıldığı ana ağ            | VDS / Trunk     |
| **iSCSI / vSAN**   | Depolama trafiği (Hız ve izolasyon kritik)         | Dedicated VSS   |

## 4. Güvenlik ve Performans (Best Practices)
- **Trafik İzolesi:** Farklı trafik türleri için farklı VLAN'lar kullanın.
- **NIC Teaming:** Hata toleransı ve yük dengeleme için en az 2 fiziksel NIC'i (Uplink) aynı switch'e bağlayın.
- **Security Policies:** 
  - *Promiscuous Mode:* Reject
  - *MAC Address Changes:* Reject
  - *Forged Transmits:* Reject
- **Jumbo Frame:** Depolama ve vMotion ağlarında MTU 9000 kullanarak paket başlığı yükünü azaltın.

## 5. Ağ Sanallaştırmasının Geleceği: VMware NSX
vSphere ağ yapısının üzerine kurulan NSX, "Software-Defined Networking" (SDN) imkanı sağlar:
- **Mikro-Segmentasyon:** VM seviyesinde firewall kuralları ile lateral (doğu-batı) trafiği korur.
- **Logical Switching:** Fiziksel ağdan bağımsız sanal katman 2 ağları oluşturur.
