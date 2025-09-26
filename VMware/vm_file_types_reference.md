# Virtual Machine Files

A virtual machine (VM) is stored as a set of files within a **VM folder**. Key files include:

- **Configuration file** → `VM_name.vmx` ✅  
- **Swap files**  
  - `VM_name.vswp`  
  - `vmx-VM_name.vswp`  
- **BIOS file** → `VM_name.nvram` ✅  
- **Log files** → `vmware.log`  
- **Template configuration file** → `VM_name.vmtx`  
- **Disk descriptor file** → `VM_name.vmdk`  
- **Disk data file** → `VM_name-flat.vmdk`  
- **Suspend state file** → `VM_name-*.vmss`  

> ✅ Indicates essential files required for basic VM operation.
