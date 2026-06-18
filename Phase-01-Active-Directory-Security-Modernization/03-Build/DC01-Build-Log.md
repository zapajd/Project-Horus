# DC01 Build Log

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document records the deployment, configuration, validation, and security hardening activities performed during the implementation of the first Domain Controller (DC01).

The purpose is to provide a repeatable deployment record and demonstrate operational execution throughout the project lifecycle.

---

# Server Information

| Item             | Value                        |
| ---------------- | ---------------------------- |
| Hostname         | DC01                         |
| Role             | Domain Controller            |
| Operating System | Windows Server 2022 Standard Evaluation (Desktop Experience) |
| Domain           | corp.horustech.local         |
| IP Address       | 192.168.10.10                |
| Deployment Date  | 2026-06-14                   |

---

# Deployment Timeline

| Step                         | Status      |
| ---------------------------- | ----------- |
| Create VM                    | Completed   |
| Install Windows Server       | Completed   |
| Configure Networking         | Completed   |
| Rename Server                | Completed   |
| Install Updates              | Completed   |
| Install AD DS                | Completed   |
| Install DNS                  | Completed   |
| Promote to Domain Controller | Completed   |
| Validate AD DS               | Pending     |
| Validate DNS                 | Pending     |
| Document Deployment          | In Progress |

---

# Step 1 - Create Virtual Machine

## Objective

Deploy the Windows Server virtual machine that will become DC01.

---

## Configuration

| Setting    | Value |
| ---------- | ----- |
| VM Name    | Horus-DC-01  |
| Generation | VMW Workstation 25H2 or later   |
| CPU        | 2 Cores   |
| RAM        | 4096 MB   |
| Storage    | 80 GB   |
| Network    | VMnet10  |

---

## Screenshot

<p align="center">
  <img src="Screenshots/01-VM-Creation.png" width="500">
</p>

<p align="center">
  <em>Figure 1: DC01 virtual machine configuration prior to deployment.</em>
</p>

---

## Validation

* VM created successfully
* VM powers on successfully

Status:

```Completed```

---

# Step 2 - Install Windows Server

## Objective

Install Windows Server 2022 Standard.

---

## Actions Performed

* Mounted Windows Server 2022 installation ISO.
* Booted virtual machine from ISO media.
* Selected Windows Server 2022 Standard Evaluation (Desktop Experience).
* Started operating system installation.
---

## Screenshot

<p align="center">
  <img src="Screenshots/02-Windows-Installation.png" width="650">
</p>

<p align="center">
  <em>Figure 2: Windows Server 2022 Standard Evaluation (Desktop Experience) installation.</em>
</p>

---

## Validation

* Installation completed successfully
* Administrator account creation screen displayed

Status:

```Completed```

---

# Step 3 - Configure Networking

## Objective

Configure static networking for DC01.

---

## Planned Configuration

| Setting       | Value         |
| ------------- | ------------- |
| IP Address    | 192.168.10.10 |
| Subnet Mask   | 255.255.255.0 |
| Gateway       | N/A (Host-Only) |
| Preferred DNS | 192.168.10.10 |

---

## Screenshot

<p align="center">
  <img src="Screenshots/08-Static-IP-Configuration.png" width="500">
</p>

<p align="center">
  <em>Figure 8: Static IPv4 configuration assigned to DC01 prior to Active Directory deployment.</em>
</p>

---
## Validation

* Successful ping test
* Internet connectivity verified
* DNS resolution verified

Status:

```Completed```

---

# Step 4 - Rename Server

## Objective

Rename the server according to Project Horus naming standards.

---

## Target Name

```DC01```

---

## Screenshot

<p align="center">
  <img src="Screenshots/07-Computer-Rename.png" width="600">
</p>

<p align="center">
  <em>Figure 7: Computer name change completed. Restart hasn't been done at this point, therefore name change won't reflect until system restart.</em>
</p>

---
## Validation

* Hostname updated successfully changed from default serveer name to DC01
* Reboot completed successfully
* New hostname verified after login

Status:

```Completed```

---

# Step 5 - Install Updates

## Objective

Apply latest Windows updates prior to domain promotion.

---
## Screenshot

<p align="center">
  <img src="Screenshots/09-Windows-Updates.png" width="500">
</p>

<p align="center">
  <em>Figure 9: Windows updates prior and after installation.</em>
</p>


---

## Validation

* Windows Update executed successfully
* Latest available updates installed
* Reboot completed successfully
* System reported "You're up to date"

Status:

```Completed```

---

# Step 6 - Install AD DS and DNS

## Objective

Install required Active Directory services.

---

## Roles

* Active Directory Domain Services
* DNS Server

---

## Screenshot

<p align="center">
  <img src="Screenshots/10-ADDS-DNS-Installation.png" width="600">
</p>

<p align="center">
  <em>Figure 10: AD DS and DNS Server installation.</em>
</p>

---

## Validation

* AD DS role installed successfully
* DNS Server role installed successfully
* Installation wizard completed without errors
* Server Manager displayed successful installation status

Status:

```Completed```

---

# Step 7 - Promote Server

## Objective

Create the Horus Technologies Active Directory forest.

---

## Screenshot

<p align="center">
  <img src="Screenshots/11-Domain-Deployment-Configuration.png" width="600">
</p>

<p align="center">
  <em>Figure 11: Server promotion and new forest creation.</em>
</p>

---

## Forest

```corp.horustech.local```

---

## Validation

* Forest created successfully
* Domain created successfully
* Domain Controller operational

Status:

```Completed```

---

# Step 8 - Post-Deployment Validation

## Active Directory Validation

Checks:

* Active Directory Users and Computers opens successfully
* Domain Controllers OU present
* SYSVOL present
* NETLOGON share present

Status:

```text
Pending
```

---

## DNS Validation

Checks:

* Forward Lookup Zone created
* SRV records present
* Host records created

Status:

```text
Pending
```

---

## Authentication Validation

Checks:

* Domain authentication successful
* Kerberos functioning correctly

Status:

```text
Pending
```

---

# Issues Encountered

Document deployment issues, troubleshooting steps, and resolutions.

| Issue | Resolution |
| ----- | ---------- |
| DNS delegation warning during domain promotion  | Expected behavior in isolated lab environment. No action required. |
| None  | N/A        |
---

# Lessons Learned

Document observations and recommendations for future deployments.

* Configure static networking installing Active Directories before installing Active Directory services.
* Verify hostname and Windows updates prior to domaion promotion.
* DNS delegation warnings are common in standalone lab deplouments and do not prvent successful promotion.
* Capturing screenshots during each deployment phase simplifies documentation and porfolio development.

---

# Build Completion Status

```85% Complete```

Remaining Activities:

* Validate SYSVOL and NETLOGON shares
* Validate DNS records
* Join workstation(s) to domain
* Continue with security hardening and GPO deployment

---

# Reviewer

Project Horus Team

---

# Last Updated

2026-06-17
