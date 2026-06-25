# SMB Hardening

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

## Purpose

This document defines the Server Message Block (SMB) hardening baseline for the Project Horus Active Directory environment.

The objective of this baseline is to secure Windows file-sharing communications by disabling legacy protocols, enabling message signing, restricting anonymous access, and validating secure SMB configuration across domain systems.

SMB hardening is a critical component of Windows security because Active Directory relies on SMB for services such as SYSVOL and NETLOGON.

---

## Scope

This baseline applies to:

* Domain Controllers
* Domain-joined Windows Servers
* Domain-joined Windows Workstations
* Future file servers deployed within Project Horus

---

## Configuration Locations

SMB security settings are configured through Group Policy and PowerShell.

Group Policy path:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Local Policies
                └── Security Options
```

Additional validation is performed using PowerShell.

---

## Baseline Configuration

| Setting                                                                    | Baseline Value |
| -------------------------------------------------------------------------- | -------------- |
| SMBv1                                                                      | Disabled       |
| SMBv2 / SMBv3                                                              | Enabled        |
| Microsoft network client: Digitally sign communications (always)           | Enabled        |
| Microsoft network client: Digitally sign communications (if server agrees) | Enabled        |
| Microsoft network server: Digitally sign communications (always)           | Enabled        |
| Microsoft network server: Digitally sign communications (if client agrees) | Enabled        |
| Guest access                                                               | Disabled       |
| Anonymous access                                                           | Restricted     |

---

# Security Rationale

## Disable SMBv1

SMBv1 is a legacy protocol with known security weaknesses and should never be enabled unless absolutely required for legacy compatibility.

Disabling SMBv1 helps protect against attacks such as:

* EternalBlue
* WannaCry
* NotPetya
* Unauthorized legacy SMB exploitation

---

## SMB Signing

SMB signing helps ensure the integrity of SMB communications by preventing unauthorized modification of SMB traffic.

This reduces the risk of:

* Man-in-the-Middle (MitM) attacks
* Session hijacking
* SMB traffic tampering

---

## Disable Guest Access

Guest authentication should remain disabled.

All access to shared resources should require authenticated domain credentials.

---

## Restrict Anonymous Access

Restricting anonymous access reduces information disclosure and prevents unauthenticated users from enumerating network resources.

---

## SMBv2 / SMBv3

Modern SMB versions provide significant security improvements over SMBv1, including:

* Improved encryption
* Better authentication
* Performance improvements
* Protocol hardening

---

# Implementation Notes

Project Horus follows Microsoft's recommendation of disabling SMBv1 and using modern SMB protocol versions.

SMB signing is enabled to provide integrity protection for SMB communications.

Because Active Directory depends on SMB services for SYSVOL and NETLOGON, all changes should be validated before deployment.

---

# Implementation Steps

## Disable SMBv1

Verify current status:

```powershell
Get-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
```

Disable SMBv1 if installed:

```powershell
Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol -NoRestart
```

Restart the server if required.

---

## Configure SMB Signing

Open **Group Policy Management**.

Navigate to:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Local Policies
                └── Security Options
```

Configure:

* Microsoft network client: Digitally sign communications (always)
* Microsoft network client: Digitally sign communications (if server agrees)
* Microsoft network server: Digitally sign communications (always)
* Microsoft network server: Digitally sign communications (if client agrees)

Run:

```powershell
gpupdate /force
```

---

# Validation Commands

View SMB Server configuration:

```powershell
Get-SmbServerConfiguration |
Select EnableSMB1Protocol,
       EnableSMB2Protocol,
       RequireSecuritySignature,
       EnableSecuritySignature
```

View SMB Client configuration:

```powershell
Get-SmbClientConfiguration |
Select RequireSecuritySignature,
       EnableSecuritySignature
```

Verify SMBv1 status:

```powershell
Get-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
```

Refresh Group Policy:

```powershell
gpupdate /force
```

---

# Functional Validation

## Test 1

Confirm SMBv1 is disabled.

Expected Result:

* SMBv1 = Disabled

---

## Test 2

Confirm SMBv2/SMBv3 remain enabled.

Expected Result:

* SMBv2 = Enabled

---

## Test 3

Confirm SMB signing is enabled.

Expected Result:

* SecuritySignature = True

---

## Test 4

Validate SYSVOL.

```text
\\corp.horustech.local\SYSVOL
```

Expected Result:

* Share accessible.

---

## Test 5

Validate NETLOGON.

```text
\\corp.horustech.local\NETLOGON
```

Expected Result:

* Share accessible.

---

## Test 6

Run:

```powershell
Get-SmbServerConfiguration
```

Confirm:

* SMBv1 Disabled
* SMBv2 Enabled
* Signing Enabled

---

# Expected Results

| Validation   | Expected Result |
| ------------ | --------------- |
| SMBv1        | Disabled        |
| SMBv2        | Enabled         |
| SMB Signing  | Enabled         |
| SYSVOL       | Accessible      |
| NETLOGON     | Accessible      |
| Group Policy | Functional      |

---

# Evidence

Store screenshots under:

```text
04-Security-Baseline/Screenshots/
```

Suggested screenshot names:

```text
01-SMBv1-Disabled.png
02-SMB-Server-Configuration.png
03-SMB-Client-Configuration.png
04-SMB-Signing-GPO.png
05-SYSVOL-Validation.png
06-NETLOGON-Validation.png
```

---

# Operational Considerations

SMB hardening should always be validated after implementation.

Disabling legacy protocols without testing can interrupt legacy applications or unsupported devices.

Before enabling mandatory SMB signing in production, organizations should verify compatibility across all supported operating systems and applications.

For Project Horus, SMB hardening is implemented within a controlled lab environment to demonstrate secure Windows file-sharing practices while preserving Active Directory functionality.

---

## Status

```text
Planned
```

---

## References

* Microsoft Learn – SMB Security Enhancements
  https://learn.microsoft.com/windows-server/storage/file-server/smb-security

* Microsoft Learn – SMB Overview
  https://learn.microsoft.com/windows-server/storage/file-server/file-server-smb-overview

* Microsoft Learn – Disable SMBv1
  https://learn.microsoft.com/windows-server/storage/file-server/troubleshoot/detect-enable-and-disable-smbv1-v2-v3

---

## Last Updated

* 2026-06-25
