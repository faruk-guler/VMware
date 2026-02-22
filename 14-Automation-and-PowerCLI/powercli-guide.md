# vSphere Otomasyon ve PowerCLI

VMware PowerCLI, vSphere ortamını Windows PowerShell üzerinden yönetmek ve otomatize etmek için kullanılan güçlü bir araç takımıdır.

## 1. Kurulum ve Bağlantı
PowerCLI, PowerShell Gallery üzerinden kurulabilir:
```powershell
Install-Module -Name VMware.PowerCLI -Scope CurrentUser
Set-PowerCLIConfiguration -InvalidCertificateAction Ignore -Confirm:$false
```

vCenter sunucusuna bağlantı:
```powershell
Connect-VIServer -Server <vcenter-ip> -User administrator@vsphere.local
```

## 2. Temel Komutlar (Cheat Sheet)

| Amaç | Komut |
| :--- | :--- |
| **VM Listeleme** | `Get-VM` |
| **VM Başlatma** | `Start-VM -VM "VM_Name"` |
| **Snapshot Alma** | `New-Snapshot -VM "VM_Name" -Name "Before_Update"` |
| **Host Durumu** | `Get-VMHost | Select Name, ConnectionState, PowerState` |
| **Datastore Bilgisi** | `Get-Datastore | Select Name, FreeSpaceGB, CapacityGB` |

## 3. Örnek Senaryo: Toplu VM Kapatma
Belirli bir tag'e veya isimlendirmeye sahip tüm sanal makineleri güvenli bir şekilde kapatmak için:
```powershell
Get-VM "TEST_*" | Where-Object {$_.PowerState -eq "PoweredOn"} | Stop-VMGuest -Confirm:$false
```

## 4. Neden Otomasyon?
- **Hız:** Yüzlerce VM üzerinde saniyeler içinde işlem yapma.
- **Standartlaşma:** İnsan hatasını minimize ederek tutarlı bir yapı kurma.
- **Raporlama:** Envanter ve performans raporlarını otomatik oluşturma.
