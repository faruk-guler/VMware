# Terraform ile vSphere (Infrastructure as Code)

Modern veri merkezlerinde altyapı artık manuel olarak değil, kod ile (IaC) yönetilmektedir. HashiCorp Terraform, vSphere kaynaklarını otomatik olarak oluşturmak ve yönetmek için en popüler araçtır.

## 1. Neden Terraform?
- **Hız:** Onlarca VM'i saniyeler içinde "blueprint" üzerinden oluşturma.
- **Sürüm Kontrolü:** Altyapı değişikliklerini Git üzerinden takip edebilme.
- **Tutarlılık:** "Dev/Test/Prod" ortamlarının birbirinin aynısı olmasını garanti etme.

## 2. Temel Yapılandırma (vSphere Provider)
Terraform'un vCenter ile konuşabilmesi için bir provider bloğu tanımlanır:
```hcl
provider "vsphere" {
  user                 = "administrator@vsphere.local"
  password             = "Password123!"
  vsphere_server       = "vcenter.sirket.local"
  allow_unverified_ssl = true
}
```

## 3. Örnek: VM Oluşturma Kodu
```hcl
resource "vsphere_virtual_machine" "vm_web01" {
  name             = "WEB-SERVER-01"
  resource_pool_id = data.vsphere_resource_pool.pool.id
  datastore_id     = data.vsphere_datastore.datastore.id

  num_cpus = 2
  memory   = 4096
  guest_id = "ubuntu64Guest"

  network_interface {
    network_id = data.vsphere_network.network.id
  }

  disk {
    label = "disk0"
    size  = 40
  }
}
```

## 4. Terraform İş Akışı
1.  **terraform init:** vSphere provider'ını indirir.
2.  **terraform plan:** Yapılacak değişiklikleri (neler eklenecek, silinecek) gösterir.
3.  **terraform apply:** Planı onaylar ve vCenter üzerinde kaynakları oluşturur.
4.  **terraform destroy:** Oluşturulan tüm altyapıyı tek komutla temizler.

## 5. Terraform State Dosyası
Terraform, altyapının mevcut durumunu `.tfstate` dosyasında tutar. Bu dosya, manuel müdahaleler ile kod arasındaki farkı anlamayı sağlar.
