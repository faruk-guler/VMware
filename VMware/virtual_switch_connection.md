
### 🔍 Açıklama:

- Her ağ trafiği türü için **ayrı bir sanal switch** oluşturulur.
- **Avantajlar**:
  - Trafik(isolation) → Güvenlik artar.
  - Performans optimizasyonu → Örneğin, iSCSI trafiği diğer trafiğe karışmaz.
  - Yönetilebilirlik → Hata ayıklama ve izleme daha kolay.
- **Dezavantaj**: Daha fazla ağ adaptörü ve konfigürasyon gerektirir.

> ✅ **Üretim ortamlarında önerilen yaklaşım.**

---

## 📋 Hangi Ağ Türleri Ne İçin Kullanılır?

| Ağ Türü            | Kullanım Amacı                                     |
|--------------------|----------------------------------------------------|
| **Management**     | ESXi host’a erişim, SSH, GUI, SNMP vs.             |
| **vSphere vMotion**| VM’lerin canlı taşınması (live migration)           |
| **Production**     | Kullanıcıya hizmet veren sanal makinelerin trafiği  |
| **TestDev**        | Geliştirme/test ortamındaki VM’ler                 |
| **iSCSI**          | Depolama trafiği (SAN/NAS üzerinden blok erişim)    |

---

## 💡 En İyi Uygulamalar (Best Practices)

- **Üretim ortamlarında** her ağ türü için **ayrı sanal switch** kullanın.
- **Management** ve **vMotion** trafiğini **farklı VLAN’larda** çalıştırın.
- **iSCSI** trafiği için **dedike fiziksel NIC’ler** ve **jumbo frame** desteği önerilir.
- **Security** açısından: Management ağına sadece yetkili kullanıcılar erişebilmeli.

---

