
> ⚠️ Not: Bu örneklerde, her VM’ye atanan vCPU sayısına göre toplam VM sayısı hesaplanmıştır.

---

## VM Sayısı Hesaplama Tablosu

| vCPU / VM | Toplam vCPU | Max VM Sayısı |
|-----------|-------------|---------------|
| 1 vCPU    | 144         | 144 VM        |
| 2 vCPU    | 192         | 72 VM         |
| 4 vCPU    | 240         | 36 VM         |
| ...       | ...         | ...           |

> 📌 Formül:  
> **Max VM Sayısı = Toplam vCPU / vCPU per VM**

---

## Açıklamalar

- **vCPU**: Sanal makineye atanmış sanal işlemci.
- **Hyper-Threading (HT)**: Eğer HT aktif olsaydı, toplam logical thread sayısı `96` olurdu. Ancak bu örnekte **HT kullanılmıyor**, sadece `48` fiziksel core dikkate alınıyor.
- VMware’de önerilen en iyi uygulama: **Fiziksel core başına 1-2 vCPU** oranını aşmamaktır (özellikle performans kritik ortamlarda).

---
