# Active Directory Build Guide

---

## Step 1 - Create the Virtual Machine

A Windows Server 2022 virtual machine was created in VMware Workstation Pro using a custom hardware configuration.

![VM Creation](Screenshots/01-VM-Creation.png)

---

## Step 2 - Install Windows Server 2022

The Windows Server 2022 ISO was mounted to the virtual machine and the operating system installation wizard was launched.

![Windows Server 2022 Installation](Screenshots/02-Windows-Installation.png)

### Configuration Selected

- Operating System: Windows Server 2022 Standard Evaluation (Desktop Experience)
- Installation Type: Custom Installation
- Disk Configuration: Default Virtual Disk
- Hypervisor: VMware Workstation Pro

### Validation

The installation completed successfully and the server booted into the initial configuration screen without errors.

---

## Step 3 - Configure a Static IP Address

After installation, a static IP address was configured to ensure consistent network communication within the lab environment.

![Static IP Configuration](Screenshots/03-Static-IP-Configuration.png)
