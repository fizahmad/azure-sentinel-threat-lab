# Windows 10 Pro VM – Victim (Target Machine)

## Purpose:
Serve as the primary attack target in the lab to generate security-relevant logs for Microsoft Sentinel.

## VM Specifications:

| Setting        | Value                         |
|----------------|-------------------------------|
| Role           | Victim / Target               |
| OS             | Windows 10 Pro (64-bit)       |
| Version        | Latest ISO from Microsoft     |
| Platform       | VirtualBox v7.0.22            |
| Disk Size      | 50 GB (Dynamically Allocated) |
| RAM            | 4096 MB (4 GB)                |
| CPU            | 4 vCPUs                       |

## VirtualBox Network Configuration:

| Adapter       | Type             | Purpose                      |
|---------------|------------------|------------------------------|
| Adapter 1     | NAT              | Internet access              |

## Screenshots:

- VM powered on, showing desktop or system info  
  `setup/screenshots/windows_vm.png`

## References:
- 🔗 [Download Windows 10 ISO (Official)](https://www.microsoft.com/software-download/windows10)
- 🔗 [VirtualBox Official Site](https://www.virtualbox.org/)
